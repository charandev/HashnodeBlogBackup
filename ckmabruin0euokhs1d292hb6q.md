## CRUD Application Using Node JS - PART 3 : Configuring the API's (CREATE, RETRIEVE)

Now that we et to our main goal of this tutorial, that is creating API's that plays around with the real data. If you are seeing this article for the first time, I recommend you to look at my previous parts of the series as well.

In this part of the tutorial, I am going to be explaining you about how to configure the API's in Node JS and test them in Postman. So, lets get started.

In the last part, we were able to start the Nodejs server and also we have connected successfully with MongoDB database. As I already discussed about the problem statement, we are going to be dealing with a Programmer information which has some properties like this.

```
Programmer:
     - name (string)
     - age (number)
     - skill (string)
     - hasJob (boolean)

```
# MVC Pattern

The very first step would be creating a **Model** file. If you stuck at this point and scratching your head asking what the heck is **Model**. Don't worry I got you covered. There are some design principles or design patterns that we generally follow for creating our applications. One of which is called as MVC (Model View Controller) pattern. 


> When using an MVC pattern, you can lay out the solution to any problem you expect to solve with the software you intend to build. The three components included by name in the pattern are:

- The model, which describes the behavior of the application regarding data, logic, and rules

- The view, which includes any information that the application may output (from tabular data to representations)

- And the controller, which accepts and translates input

Note that the model, which is the core component on which you will wind up focusing, is independent of any user interface you are planning to create eventually.

For more information visit this article:  [MVC Architecture](https://www.appdynamics.com/blog/engineering/a-practical-guide-to-popular-node-js-mvc-frameworks/) 

----------------------------------------------------------------------------------

# Stop saying stories, SHOW ME CODE!!

Ok, I can understand your inner feeling. Lets dive into creating the stuff. We will create a simple `Programmer` model that holds all the properties. We will create a folder called **models** and inside it Programmer.js file. Go ahead and create them.


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1615790783177/OLdY4kc8T.png)

Now, remember that, whatever the model that we create, would be replicated as a schema in mongodb database. So, we need to specify that here. So, our model - Programmer.js file will look like:


```
const mongoose = require('mongoose')

const ProgrammerSchema = new mongoose.Schema({
  name: {
    type: String,
    required: true
  },
  age: {
    type: Number,
    required: true
  },
   skill: {
    type: String,
    required: true
  },
  hasJob : {
    type: Boolean,
    required: true,
  }
})

module.exports = mongoose.model('Programmer', ProgrammerSchema)
``` 
In the above code, most of the things are self explanatory. `const ProgrammerSchema = new mongoose.Schema()` is used to create a schema with the specified values in MongoDB database.

--------------------------------------------------------------------------------------

Next, let us write a simple `/test` API endpoint to just check everything is working. So go ahead and add this piece of code in our `app.js` file:


```
app.get('/test',(req,res) =>{
    res.send('Hello world')
})
``` 

`app` has all the methods of `express()` as you already know. So, here we are making a simple `get` call when we hit the `/test` path. And we pass a callback having two kinds of parameters - `req` and `res`, req object is used to receive any value and res object is used to send any request. We are sending a string `Hello World` for testing purposes.

So, if the nodejs server is running in port 9000, we can hit the API endpoint in Postman. And if we do that, we can say its working properly as shown below:


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1615791805429/vgltoEwKn.png)

As you can see it is returning 'Hello World'.

--------------------------------------------------------------------------------

So all things set up, we will go ahead and create `Save a Programmer`, `Get All Programmers` API's which are:

- **Saving** the programmer details

```
POST : http://localhost:9000/programmer
``` 



- **Fetch all** the programmer details

```
GET : http://localhost:9000/programmers
```
 
Before getting into it, just make sure you have imported the `Programmer.js` file in `app.js` file:

```
const Programmer = require('./models/Programmer')
```

And we also may need to use a `Middleware`, which something that express() provides that will run just after the application gets the request from user and before it sends to the database or server.

Write the below piece of code in `app.js` file:

```
app.use(express.json())
```

What we are basically saying by this is, whatever request that user gives, we are asking it to convert into a JSON object before processing it.


## 1. **Saving** the programmer details

So, the first API that we need to create is Saving a programmer. To do that we need to follow three simple steps:

1. Create a POST method and give an endpoint path as `/programmer`.
2. Create a new instance of `Programmer` model that we have created.
3. Assign all the properties with user request object, which is present in `req.body` and save it to database.

- So, in **first step** we will create a POST method using the following code:

```
app.post('/programmer', async (req, res) => {
   //code to save a programmer
})
```
- The **second step** is to create new Instance of Programmer:


```
app.post('/programmer', async (req, res) => {
    const programmer = new Programmer({
       // assign values of Programmer from request.body
    })
    
})
```
- In the **third step** we need to assign the values of Programmer with the input values from the user, which will be in `req.body` object and save it.

```
app.post('/programmer', async (req, res) => {
    const programmer = new Programmer({
        name: req.body.name,
        age: req.body.age,
        skill: req.body.skill,
        hasJob: req.body.hasJob
    })
    try {
        const newProgrammer = await programmer.save() // saving in DB
        res.status(201).json(newProgrammer)
    } catch (err) {
        res.status(400).json({ message: err.message })
    }
})
```

Here in this step, we have used async/await calls for handling methods. And also used try-catch blocks to handle possible errors.


Now, we will test this in postman. The request object for the POST endpoint `http://localhost:9000/programmer` in our case is :

```
{
   "name":"Sai Charan",
   "age": "23",
   "skill":"Angular, JavaScript",
   "hasJob": true
}
```


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1615794136741/doHn6TXUo.png)


If we click **Send**, we can see the response object that has saved, which has unique ID:


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1615794273856/DdhDaHRNI.png)


## 2. **Fetch all** the programmer details

To do that we need to follow three simple steps:

1. Write a `GET` method using express and give a path `/programmers`.
2. Fetch all the Programmers from Programmer object using `.find` method that `mongoose` provides.
3. Send the response back in the form of JSON.


- In the **first step**, we will write a GET method:

```
app.get('/programmers', async (req, res) => {
  // code for getting all programmers
})
```
- Next in the **second step**, we will Fetch all the details from MongoDB database using `.find()` method:

```
app.get('/programmers', async (req, res) => {

    const programmers = await Programmer.find()
  
})
```

- Finally in the **last step** we will return the `programmers` constant variable which holds the data of all Programmers in DB, by converting into JSON format:

```
app.get('/programmers', async (req, res) => {
  try {
    const programmers = await Programmer.find()
    res.json(programmers) // converting into json
  } catch (err) {
    res.status(500).json({ message: err.message })
  }
})
```

Now we have done it, lets try to hit the `http://localhost:9000/programmers` API endpoint in postman:


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1615796615360/UVbwbfgGa.png)

The response is: 

```
[
    {
        "_id": "604f0b9cfcb2383ab47c1fa8",
        "name": "Sai Charan",
        "age": 23,
        "skill": "Angular, JavaScript",
        "hasJob": true,
        "__v": 0
    },
    {
        "_id": "604f0fa3fcb2383ab47c1fa9",
        "name": "Vamsi Varun",
        "age": 23,
        "skill": "Java, JavaScript",
        "hasJob": true,
        "__v": 0
    },
    {
        "_id": "604f0fb6fcb2383ab47c1faa",
        "name": "Ram Gopal",
        "age": 23,
        "skill": "HTML, JavaScript",
        "hasJob": true,
        "__v": 0
    },
    {
        "_id": "604f1004fcb2383ab47c1fab",
        "name": "Chiruhas",
        "age": 23,
        "skill": "Angular, JavaScript",
        "hasJob": true,
        "__v": 0
    }
]
```

---------------------------------------------------------------------------------

So, we have successfully created CREATE and RETRIEVE parts of **CR**UD operations. We will look into other API's like **Get a particular Programmer by ID, Update a Programmer with new details and Delete a programmer** in the next part of the series.

> 
The source code for the code until this part will be available here in GitHub :  [https://github.com/charandev/NodeJS-tutorial/tree/Part-3](https://github.com/charandev/NodeJS-tutorial/tree/Part-3) 

So, I am wrapping up this article now, hope you learned something today.