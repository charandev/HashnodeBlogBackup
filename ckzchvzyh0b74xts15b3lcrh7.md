## Understanding JavaScript "this" | Different Runtime Binding techniques

There is no doubt that many JS developers may have come across `this` while writing code and confused about what it is.

So, who the hell is `this`? 🤔

> Technically, JavaScript `this` is a keyword, refers to the **object** that the **function** belongs to. And the value of this depends on how the function is called, something known as runtime binding.



![InkedUntitled_LI.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1644219518515/agJYKG2o6.jpeg)

In layman’s terms, `this` points to the owner of the **function call**, I repeat, the function call, and **NOT** the function itself. The same function can have different owners in different scenarios on how that function is being called.

4 rules decide the value of `this`

> **Note: **
  `this` is not a variable. It is a keyword. You cannot change the value of `this`.


# 1. Default binding / Direct invocation

In Default binding, `this` points to global object. Global object is nothing but `window` object. Default binding is applied for standalone functions which are not a part of any nested function/object. Also, it is the fallback option for all other types.


```
function myFunction() {
    console.log(this)
}
myFunction();           // Window {}
``` 

# 2. Implicit binding / Method invocation

Implicit Binding is applied when you invoke a function in an Object using the dot notation. `this` in such scenarios will point to the object using which the function was invoked. Or simply the object on the left side of the dot.


```
function myFunction() {
    console.log(this)     
  }
 
const obj = {
  someKey: 1, 
  myFunction: myFunction,
}

obj.myFunction();   
// {someKey: 1, myFunction: ƒ}. ie. obj
``` 

## 2.a Nested Function

When a function is nested inside a method of an object, the context of the inner function depends only on its invocation type and not on the outer function’s context. Means, the value of `this` of inner function depends on how the inner function is called inside the parent function.  



```
const obj = {
  someKey: 1, 
  outer: function() {
    function inner(){
       console.log(this);
    }     
    inner();
  },
}

obj.outer();      // Window {}
``` 
In this example, even though `outer` was called using implicit binding, `inner` was called using **default binding**. We already know how default binding works. Hence,  `this` points to the Window Object.

## 2.b Method separated from the object

When we copy an object method to a new variable, we are creating a reference to the **function**. That means, the new variable to which the method coped to will directly point to the method and not parent object containing it.


```
function myFunction() {
  console.log(this);
}

const obj = {
  someKey: 1,
  myFunction: myFunction,
}

const newFunction = obj.myFunction;
newFunction();    // Window {}
``` 

In this example, newFunction directly refers to myFunction. So it will print Window Object as its indirectly become like default binding. 

# 3. Explicit binding / Indirect invocation

In this method, you can force a function to use a certain object as its `this`. Explicit Binding can be applied using call(), apply(), and bind().

**call():** Pass in the required object as the first parameter during the function call. The actual parameters are passed after the object.

**apply():** Similar to call() with a difference in the way the actual arguments are passed. Here, the actual arguments are passed as an array.


```
function myFunction(param1, param2) {
    console.log(this)     
  }
 
const obj = {
  someKey: 1, 
}

const param1 = 1, param2 = 2;
myFunction.call(obj, param1, param2)       // {someKey: 1}
myFunction.apply(obj, [param1, param2])    // {someKey: 1}
``` 

**bind(): **In this method, you create a new function with a fixed `this`. These types of functions created using bind() are commonly known as **bound functions**.


```
function myFunction() {
    console.log(this)     
  }
 
const obj = {
  someKey: 1, 
}

const boundFunction = myFunction.bind(obj)
boundFunction();      // {someKey: 1}
``` 


# 4. New binding / Constructor invocation

New binding is applied when we create an object using Function Constructors.

## 4.a Function without Return

When we invoke a function using the new operator, internally the following steps are done:

1. The constructor function is invoked and an object is internally created, inheriting the prototype of the constructor function used.
2. The properties and functions are added to this object as per the function definition.
3. This newly created object is returned and is assigned to the LHS variable at the functional call.


```
function myFunction(){
  // JS internally creates an object and refers it as this
  
  // User explicitly adds required properties and methods to the object
  this.someKey = 1;
  this.inner = function(){
    console.log(this);
  }
  
  // JS internally returns the object
}

const obj = new myFunction();
obj.inner()           // {someKey: 1, inner: ƒ} with myFunction prototype
``` 

## 4.b Function with Return

The returned object is assigned to the LHS variable at the function call and the prototype of the constructor function is NOT inherited.


```

function myFunction(){
  return {
    someKey: 1,
  }
}

const obj = new myFunction();
console.log(obj);    // {someKey: 1} without myFunction prototype
``` 

------------------------------------------------------------------

# Arrow Functions

Normal functions in JS abide by the 4 rules mentioned above. But ES6 introduces a special kind of function that does not use these rules, known as arrow functions.

>Arrow functions use “lexical scoping” to figure out what the value of `this` should be. Lexical scoping is a fancy way of saying it uses “this” from the outer function in which it is defined.

Simply put, when an arrow function is invoked, JS literally takes the `this` value from the outer function where the arrow function is declared. I repeat, the outer function, **NOT** the outer object in which it is defined.

1. If the outer function is a normal function, this depends upon the type of binding of the outer function.
2. If the outer function is an arrow function, JS again checks for the next outer function and this process continues till the global object.

See this code for getting an idea:


```
function outer(){ 
    let inner = () => { 
      console.log(this);
    };
    inner()
  } 

const objA = {
  someKey: 1,
  outer : outer, 
};
const objB = {
  someKey: 2,
}

// In this example, each time when inner function is called, 
// JS simply takes the this value from outer function
outer();            // Window {}
objA.outer();       // {someKey: 1, outer: ƒ} --> objA
outer.call(objB)    // {someKey: 2} --> objB
``` 

*Note: None of the binding rules has any Direct Effect on arrow function*


```
const myFunction = () => {
  console.log(this);
}

const objA = {
  myFunction: myFunction,
  inner: () => {
    console.log(this);
  }
}

const objB = {}

myFunction();                   // Window {}
objA.myFunction()               // Window {}
objA.inner()                    // Window {}
myFunction.call(objB);          // Window {}
const objC = new myFunction()   // myFunction is not a constructor
``` 

----------------------------------------------------------------------------

### Conclusion

1. The this value in a function depends on how the function is called.
2. Default Binding: Window Object
3. Implicit Binding: Object on the LHS of dot notation.
4. Explicit Binding: Object passed as first parameter in call(), apply(), bind().
5. New Binding: The LHS object in the function call will be referred to as this in the function.
6. Arrow functions simply use the this value from its surroundings.
