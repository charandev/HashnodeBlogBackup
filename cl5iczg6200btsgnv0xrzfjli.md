## The problem of  '<div> Soup' in React. How to get rid of it?

In React we work with JSX all the time. JSX allows us to write HTML in React. JSX is the code that you return in your Components, which in the end will be rendered to the real DOM by a React.



![code1.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1657633500723/8LmV8zJki.png align="left")


But JSX has certain limitations. Specifically there is this limitation where if we have adjacent root level JSX elements like in this example below, we'll get an error. And with root level, I mean that when we have two JSX elements next to each other and not wrapped by another JSX element. And we then return these side by side JSX elements or we try to store them in variables.


![code2.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1657633415289/AmrB1I0SP.png align="left")

And the error is -

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1657633806581/9A77koVm7.png align="left")


This is because in React or in JSX in general, you can't have more than one root JSX element. So if you return a value or if you store a value in a variable, that value must only be **exactly one JSX element** not two or three or four side by side adjacent elements.

Understanding this is simple, even in JavaScript we cannot return multiple statements or more than one thing at a time. For example the below return statement is not valid in JavaScript either!


![code3.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1657634205707/BGq1tNMcc.png align="left")

So, because of this natural limitation of JavaScript, we can only have one root JSX element.


# The `<div>` Soup

Now, we have some understanding about the limitation. But how can we work around that? Actually there is a solution. You might have already guessed it, it is to wrap a `<div>` around all the elements in the return statement, this technically make the return statement to return only one value as a whole.


![code4.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1657634848578/OUsk111UH.png align="left")

> **Note:** This doesn't have to be a `<div>` but can also be *ANY* element like a custom component as a wrapper.

However with a wrapping `<div>` or generally any wrapping element, a new problem arises, which is called **div soup**.

We can end up with a real DOM that's being rendered where you have many nested React Components and all those Components for various reasons need wrapping divs or have wrapping Components. And you have all these unnecessary divs being rendered into real DOM even though they're only there because of this requirement or this limitation of JSX that we have talked about earlier.

For more understanding, just see this image.


![code5.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1657635984789/vBwDoIXtR.png align="left")


### And this is not an unrealistic scenario!

> In bigger apps, you can easily end up with **tons of unnecessary `<div>`s** (or other elements) which add **no semantic meaning or structure** to the page but **are only there because of React's/ JSX' requirement**.

Now of course it's not a good practice even the things are working fine with this approach. You're rendering too many HTML elements and ultimately that also makes your application slower because the browser needs to render all those elements and React needs to check all those elements, or at least some of those elements if content needs to change. So rendering unnecessary content is generally never a good idea in programming. Hence this wrapping div or this wrapping element approach is **okay but not ideal**.

# Using Fragments to solve the problem

> React Fragments let you group a list of children without adding extra nodes to the DOM.

In React, there is a solution to tackle this problem out of the box. There is a component available in React library called `Fragment`. We can access that component like `React.Fragment` or you can just import Fragment from React in the file. 


![code6.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1657637897961/al2gzkpzw.png align="left")

### or

We can also use another kind of syntax with empty HTML tags as shown below to achieve the same.


![code7.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1657638176492/WUvdcjK8e.png align="left")


> **Note:** The second way where we used `<> </>` might not work in some old React projects as it depends on some configurations. But using `<React.Fragment>` will always work.

Now what's actually happening under the hood is, `React.Fragment` will **render an empty wrapper**, meaning it doesn't render any real HTML element to the DOM. But it **fulfills React's/ JSX' requirement**.

-----------------------------------------------------------------

Hope you got some understanding of why we should not to use div as wrapper, instead leverage the future of React Fragments for the same purpose. 

If you found this article useful, share it with your friends who might need to know this and also leave your thoughts in the comments down below.


