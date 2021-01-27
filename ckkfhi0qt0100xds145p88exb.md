## Let us finally understand `var`, `let` and `const` in JavaScript!

**Ever wondered why people use different methods to declare a variable in Java Script? Or, did you ever used var / let / const to declare a variable and don't know what it actually mean but just for the sake that its working fine in that context? If so, you are probably at a right place. Don't worry, I was in this situation before and that is why I am writing this article in first place XD! **

So, today let us try to understand the differences between different ways to declare variables using `var`, `let` and `const`.


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1611744989589/j-4J_pIFh.png)

The release of ES2015 in 2015 introduced two new keywords, `let` and `const`, which are important **block-scoped** variables in JavaScript. Until that point, a variable was declared in JavaScript by using the `var` keyword.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1611745103429/yjzYFFlIV.png)

Before I dive into the core explanation with differences, here is the TR;DR; version of it.

### var:

As we know, its the only way to declare variables in JavaScript before 2015. But it has some issues:

1. It has function scope


> 
Function Scope: It means, the variable is available to access within a function where it is defined. 

2. It can be declared more than one time in the same project.

3. You can re-assign the value of the variable any time.

### let:

It’s quite similar to var keyword, the difference is that it has **block scope**.

> 
Block scope: is anything between curly braces { } like: functions, if statement, loops or anything. Variable declared in block scope remains available only in this scope.

Here’s some benefits you have when you’re using let keyword:

1. You can re-assign the value of the variable any time.

2. You can’t declare the variable more than one time.

### const:

It also has **block scope** like `let` keyword.
It has all benefits that `let` keyword has except for one:

1. You can’t re-assign the value of the variable again.


> 
Beware when you’re dealing with arrays and objects while using const keyword because:

1. when you’re declaring a new array using const keyword, you can change the value of any element in the array but, you can’t change the value of the entire array as it is.

2. For objects you can change the value of any property in the object but, you can’t change the value of the whole object and also you can add more keys in object.

---------------------------------------------------------------------------

# Examples

Let's start with a piece of code 


```
if (true) {
    var varVariable = 'Var Variable - This is true'
}

console.log(varVariable);

if (true){
    let letVariable = 'Let Variable - This is true'
}

console.log(letVariable);
``` 

We have a `varVariable` which is functional scoped, assigned to some value and `letVariable` which is block scoped, assigned to some value in if conditions.

If we run this code:


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1611746889350/e4iM1BDd6.png)

As you can see, the text which was assigned to `varVariable` that is `Var Variable - This is true` is being logged in console, because that variable has the global scope in this case as there is no function wrapping it.

On the other hand, the text which was assigned to `letVariable` that is `Let Variable - This is true` is not logged outside `if` block. Because, `let` variables are block scoped, you can only access in the same block that you have assigned it and not outside of it. The same thing can bee understood from the error message which says `Uncaught ReferenceError: letVariable is not defined`.

So, if you keep the `console.log(letVatiable)` in the same `if` block, then you can able to see the data, as you can see in the picture.


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1611747434532/T-mM9CLgF.png)


When it comes to `const`, it will act same like `let`. But there is a small difference which we will look into later. Example of using `const` is given below:


```
if (true) {
    var varVariable = 'Var Variable - This is true'
}

console.log(varVariable);

if (true){
    const constVariable = 'const Variable - This is true'
    console.log(constVariable);
}

console.log(constVariable);
``` 

if we run the above code:


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1611747574396/MZJ2oEowb.png)

----------------------------------------------------------------------------------

Another thing that is a **problem** for `var` is that we can re-assign `var` variables multiple times by re-declaring them. 

```
if (true) {
    var varVariable = 'This is true'
}

var varVariable = 'This is false'

console.log(varVariable);
``` 

In the above code-snippet, we are trying to re declare the same `var` variable with some other value, that is `This is false`. If we run it:


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1611748056986/w_xgIJp_p.png)

It has completely re defined the `varVariable`. 

But if we do the same with `let` variable, things will be little bit different. For example if we try to re declare the same variable like this:

```
let letVeriable = 'true'
let letVeriable = 'false'

console.log(letVeriable);
``` 
The output will be like as follows:

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1611748406715/Tq6Z7EA0l.png)

We are getting an error saying `Uncaught SyntaxError: Identifier 'letVeriable' has already been declared`.


> 
This is actually the biggest problem with var. Because it allows you to override variables accidentally. Normally, when we declare variable with a keyword, weather it is var, const or let, we must be thinking that that is the fist time we are declaring it. Let takes care of this problem and wont let you declare another variable with the same name.

  
Another way that actually `var` and `let` will be differed is that, `var` allows us to access the variable / use the variable before we actually declare it. For example:


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1611749712353/zcEG4xNw_.png)

In the above image, we are console log-ing the `varVariable` before we declare it in the next line. Instead of giving an error, it is printing `undefined`. This means it already knows that the variable already exists somewhere after it.

But `let` and `const` does not work this way.  For example, 


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1611750128291/d7u4sGFBq.png)


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1611750182559/gCVbnWFx8.png)



> `let` and `const` will work exactly the same way except that `const` will not allow us to initialize the same variable with new value. 

For example, we have a piece of code as below where we want to re initialize the same const and let variable with different values


```
const constVar = 1;
let letVar = 1;

constVar = 2;
letVar = 2

``` 

If we run it,


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1611752506650/RjCOzNGY-.png)
 
as you can see we are getting an error saying, `Uncaught TypeError: Assignment to constant variable.`. 


> 
That means, if we have initialized a `const` variable, the value value of it cannot be changed at any point of time by re-initializing it. That variable becomes constant. **And this is the only way that `const` differ from `let`** and it exactly same as `let` otherwise.

But, one thing to keep in mind that, **`const` does allow us to change a property in an object, if the const variable is an object. **

For example, if our `const` variable is an object containing some key-value pairs, then we can modify any value using its corresponding key.

For example,


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1611753322888/hMAkNjOLLL.png)

So, from above image we can conclude that:


> `const` only prevents us from changing the actual value by re assigning the value to a different value, but not actually changing the different properties in that value.

---------------------------------------------------------------------------------

## Conclusion

These are the difference between `var`, `let` and `const` keywords. I recommend using only `const` for declaring your variables most of the times because of avoiding accidental changes to already assigned variable. Sometimes if we need to re-initialize a variable after declared, like in `loops` we can use let to declare variables.

Hopefully you have understood the clear picture of how different ways of declaring variables in JavaScript works. 

If this article helps you, please share it with your friends whom you want to help understanding it. And as always, you can provide your thoughts n the comments below!

