## What is IIFE in JavaScript?

There are few topics in JavaScript, which you might have seen in action somewhere in code but you may not point it out and say, "Ohh! this is  ___  concept in JavaScript". One of those topics is **IIFE**. An acronym for: 

> ***Immediately Invoked Functional Expression***

Well, you might ask me that, *"Hey! I know how a normal Functional Expression look like, but what the heck is IIFE?".* Well, this is the exact question I am going to answer today in this article.

#  Functional Expressions

Before knowing about Immediately Invoked Functional Expressions, lets quickly recap what is a normal Functional Expression in JavaScript looks like. 


![code.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1643374039857/5YNQO9c9J.png)


Makes sense? This is how we generally write a function in JavaScript. There will be `function` keyword, followed by `nameOfTheFunction` and followed by `{/*Some code here*/}`.

I know I know! There are few other ways of writing a function considering we are living in a Modern JavaScript world! Like, arrow functions and also function assigned to a variable. These forms will look like this:


![code2.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1643374630073/z5r3ETmjm.png)

But hey, you get the idea.

### Here comes the important part

Finally, here comes the important part. In order to invoke that function you wrote, you need to call it explicitly wherever you wanted. Right? In fact, that's the main reason we write a normal Functional Expression at first place. This will look something like this if you remember:


![code3.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1643375906505/il-ofA6Jo.png)

# Immediately Invoked Function Expression

Now, we understand how a normal functional expressions work in JavaScript, lets move slowly towards IIFE's. Lets try to understand the  phrase *Immediately Invoked Functional Expressions*.  It means:

> **Immediately Invoked**: Something that invokes immediately.

> **Functional Expressions**: We already studied about them till now!

### If we understand the whole picture:


> **An IIFE (Immediately Invoked Function Expression) is a JavaScript function that runs as soon as it is defined.** - MDN

So, we don't need to call this function explicitly in order for it to invoke/run. It will run as soon as the JavaScript file is being called. An IIFE will look something like this:


![code4.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1643379076424/61c3Hvkf4.png)

If we look at the syntax itself we have two pairs of closed parentheses, the first one contains the logic to be executed and the second one is generally what we include when we invoke a function, the second parenthesis is responsible to tell the compiler that the function expression has to be executed immediately. 

## Here is how you can convert a normal function to IIFE


![code5.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1643380191762/1BztC2oVI.png)


Notice we are not including explicit call for a IIFE as its not required. Also these are just anonymous functions as they do not require a function name. Because we don't call them anywhere. But keep in mind, you can also give name to it if you want to. Also they can even be a arrow function as well!

And, if you wanted to know, here is how you generally pass a value to an IIFE that accepts some parameters:



![code6.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1643380100544/Io1exkQLV.png)


## Features/Behaviors of IIFE's
- IIFE follow their own scope like any other function/variable in JavaScript. The part of the name immediately invoked is sometimes confusing to new developers as they expect the IIFE to execute irrespective of function scope, this is wrong. For example, let us take the following example where the IIFE is defined within a function and will only be immediately invoked if we call the Parent Function.

![code7.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1643380474421/mFDm-8KvH.png)

**Output:**

```
Welcome to
charandev.com blog
Hi There!
```


- Similarly to other function IIFEs can also be named or anonymous, but even if an IIFE does have a name it is impossible to refer/invoke it.

- IIFEs have there own scope i.e. the variables you declare in the Function Expression will not be available outside the function.

----------------------------------------------------------------------------------

And there you go. We have came to the end. I have tried to give you elaborated explanation about IIFE in JavaScript so that you will never forget. Have you heard of this before? Or came across freshly? Comment down your thoughts.


