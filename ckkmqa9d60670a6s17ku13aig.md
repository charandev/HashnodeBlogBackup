## Memory Management and Garbage Collection in JavaScript

Hi everyone!

Today, we will learn about **Memory Management** and how **Garbage Collection** works in JavaScript.

## What is Garbage Collection (GC)?

When you declare a variable, an object, an array or a function, all are stored somewhere in the memory. Assume that you have an `Object A`. When your program starts, a location is created and data stored in this location, lets say the location is `Location A`. So now the `Object A` which has some data and stored in the previously created location `Location A`, in between there might be some read/write operations. 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1612191540075/Og7rOCj7m.png)

What happens when the program ends? Once the program ends, the party is over. Now this location needs to be cleaned as it is of no use. So, the data that was there in that memory needs to be cleaned.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1612191697782/DkIu1sQSd.png)

## What is Memory Management

Normally, **Memory Management** or **Memory Lifecycle** can be thought of like this - You have lets say an object, a variable or a function, there is an allocation of memory happens first, then there might be some read/write process happens till the program ends. 


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1612191989419/SeicEwxv_.png)


And when the program ends, free these locations or release the memory. 


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1612192074500/LWE3_svNg.png)


> 
TL;DR; 
### Memory Lifecycle:
1. Allocate the memory you need
2. Use the allocated memory (read, write)
3. Release the allocated memory when it is not needed anymore


Low-level languages like C, have manual memory management. We will make use of commands such as `malloc()` and `free()`. In contrast, JavaScript automatically allocates memory when objects are created and frees it when they are not used anymore (garbage collection). 


> The JavaScript garbage collector runs automatically.


The JavaScript garbage collector runs automatically, keeps track of memory locations, and determines which memory locations are free (i.e., safe for reuse). The garbage collector uses the mark and sweep algorithm with some optimizations.

## Reachability

The main concept of memory management in JavaScript is reachability.

Simply put, “reachable” values are those that are accessible or usable somehow. They are guaranteed to be stored in memory.

There’s a base set of inherently reachable values, that cannot be deleted for obvious reasons.

For instance:

- The currently executing function, its local variables and parameters.
- Other functions on the current chain of nested calls, their local variables and parameters.
- Global variables.

These values are called *roots*.

Any other value is considered reachable if it’s reachable from a root by a reference or by a chain of references.

For instance, if there’s an object in a global variable, and that object has a property referencing another object, that object is considered reachable. And those that it references are also reachable. Detailed examples to follow.

There’s a background process in the JavaScript engine that is called garbage collector. It monitors all objects and removes those that have become unreachable.


## Mark and Sweep algorithm
JavaScript internally uses Mark and Sweep algorithm for Garbage Collection.

As we already know, Reachable objects refer to those objects that are accessible and stored in the memory. A root refers to objects that are inherently reachable, these​ include:

- global variables
- local variables of the current function
- parameters of the current function

Starting from the root, the garbage collector traverses the objects and marks them as visited. The objects which are unreachable from the roots are unmarked and considered garbage (memory reserved for these objects is later freed).

## Garbage collector in action


```
let fruit = {
  name: "Orange",
  weight: 130,
};
let orange = fruit;
``` 
Fruit contains a reference to the object:


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1612192692144/XsKCnWXUr.png)


```
fruit = null;
``` 
`fruit` no longer contains a reference to the object. However, it is still reachable from `orange` and cannot be treated as garbage.


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1612192738563/SIqzCb8GM.png)


```
orange = null;
``` 

`orange` no longer contains a reference to the object. The object is now unreachable and the memory that it occupied will be declared safe for reuse by the garbage collector.


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1612192782168/SjthdgZw-.png)

-----------------------------------------------------------------------------

We came to an end of this article. Hopefully you have learned something new today.