## MERN stack: how to build a RESTful API with Node.js and Express

# MERN stack introduction

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1648954444439/EQTKghtH7.png)
MERN stack stands for MongoDB, Express, React and Node. It's widely popular due to the fact that you can use JavaScript on the backend and frontend, or TypeScript. It's also fast as scalable, with millions of developers writing code and contributing to the documentation and the ecosystem.

There are variations where instead of React for the frontend you will find Angular, Vue, or even Svelte nowadays, although this last one is still not as popular. Additionally you also have Next.js, Nuxt.js, Remix.js, etc. You can do everything with JavaScript or TypeScript nowadays.

This is the first article of the MERN stack series that will progress in complexity. At the end of it you will be able to create a full stack web app and deploy it anywhere with Docker. But now we will focus on building the simplest RESTful API with Node and Express.

*NB: There's an 'older' stack, called [LAMP](https://en.wikipedia.org/wiki/LAMP_(software_bundle)) that consists of Linux, Apache, MySQL, PHP/Perl/Python, depending on your focus you might want to check it out*

# Concepts and memes
[Node.JS](https://en.wikipedia.org/wiki/Node.js) is a runtime environment for JavaScript, it basically allows you to ruin everything with JavaScript anywhere.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1649018707425/_kIdBfVeE.png)

[Express or Express.js](https://en.wikipedia.org/wiki/Express.js) is the most famous backend framework for Node.js. It allows you to build web applications and APIs.

Once you have your project you can put Express.js on top of Node.js in a machine and it will act as a server for requests, you can also connect it to a database and it will server you as an intermediary between user events and the information you want to show.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1649018754742/396GM2m5f.png)

# Write code, not docs - our first server
No, you should totally write documentation but let's start this tutorial.

The first thing we need to do is go to our directory and 
``` npm init
``` this will start the package.json, you can just press yes to everything. We will have all the dependencies stored in this file. Instead of [npm](https://www.npmjs.com/) you could also check out another package manager called [Yarn](https://yarnpkg.com/).

Once that's done follow with 
```npm install express
```  and make a index.js file, that's where our code is going to be. 
If you are using git or any sort of version control remember to ignore the node_modules folder. That's where all your dependencies are, you shouldn't be touching that folder at all.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1648955301700/AWyk_GZjv.png)

Let's write our first server, put this into index.js:

```
//we import the express dependency
const express = require('express')
//assign express to a variable so it's easiet to work with
const app = express()
//this is our first route
//we want to get http://localhost:3001/
//the app already knows that we are on localhost
//we just need to indicate that's the entry point with '/'
//req stands for request and res for response
app.get('/', (req, res) => {
    //we reply to the get endpoint by sending a text back
    res.send('hello world!')
})
//define the port where our app is gonna run
const PORT = 3001
//make the server listen to that port
app.listen(PORT, () => {
    //the console.log is for your CLI
    //so you know the server has started
    console.log(`server running on localhost with port ${PORT}`)
})
``` 

Once you have it you can run your server through CLI by typing ```
node index.js
``` in your terminal (remember you have to be in the folder where index.js is). We are using our Node runtime to execute the code in our index.js file.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1648956926254/2QQom6BWW.png)
*NB: Every time you make a change in your code you need to restart your server, you exit it with CTRL+C from the terminal and every time you want to run it again you need to type 'node index.js'. 
In order to get around this you could install [nodemon](https://www.npmjs.com/package/nodemon)*

Afterwards in your browser go to ```http://localhost:3001/ ```
You should see the following:
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1648956866243/bfYaUT-55.png)

# RESTful API
There are several discrepancies between the theory and the practice of building a RESTful API, as well as different definitions, here we will go with a CRUD example. Which stands for Create, Read, Update and Delete. We will build endpoints for all these operations.

Before starting make sure you have this middleware on top of your file

```
//middleware so the server can parse json data
app.use(express.json())
``` 
and also make a "database" like this:

```
let infoDB = [
    {
        id: 1,
        info: "example of information",
        date: "2022-04-03T20:00:22.158Z"
    },
    {
        id: 2,
        info: "example of information2, put anything here",
        date: "2022-03-03T20:00:22.158Z"
    }
]
``` 

This is how the top of your file should look like:

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1649016699860/EyZXDqzLp.png)

Additionally I will be using [Postman](https://www.postman.com/) to make calls to my endpoints, it's free and simplifies the process of development, however there are many alternatives.


## GET or Read
The code is very straightforward, we make a call to /api/info and get a response with all the data back in JSON format.


```
//an endpoint to return all our infor back
app.get('/api/info', (req, res) => {
    //we send the information back in JSON format
    //along with a 200 status which means it's successful
    res.status(200).json(infoDB)
})
``` 

The call to Postman should return:


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1649019491643/RBznULp9_.png)

We will also add a way to get a specific item from the database through the id but you can check it out later, first get familiar with the rest of the code.

```
//and endpoint to return an object with a specific id
app.get('/api/info/:id', (req, res ) =>{
    //we parse the request id since it's a string
    const id = Number(req.params.id)
    //find the object the user wants in our database
    const infoObject = infoDB.find(info => info.id === id)
    //return with the needed status and the object if you find it
    infoObject
        ? res.status(200).json(infoObject).end()
        : res.status(404).json({
            error: `an object doesn't exist with the id ${id} in our database`
        }).end()
})
``` 


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1649019507961/9u_Y5CSV8.png)


## POST or Create
In order to make this endpoint we will need an additional helper function to generate ids for our data:

```
//a helper function to generate an id
//if you want to make it simpler just return infoDB.length + 1
const generateId = () => {
    const maxId = infoDB.length > 0
        ? Math.max(...infoDB.map(i => i.id))
        : 0
    return maxId + 1
}
``` 
If you are unfamiliar with the methods what you do here is first make an array of items with the ids through [map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) then we use the [spread operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax) (the three dots) to spread the array and pass it to [Math.max](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/max) which will return the maximum item.

Afterwards we use a [ternary operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_Operator) to assign either the maximum id or 0.

Here's the Express endpoint for a POST method:

```
//an endpoint to add a note
app.post('/api/info', (req, res) => {
    //without the middleware express.json() on L6 we wouldn't be able to read this data
    //extract the body from the request
    const body = req.body
    //check if the body doesn't contain any info
    if(!body.info) {
        //return an error status and a json response
        return res.status(400).json({
            error: 'you need to type the information'
        })
    }
    //we make an object from the request to add it to our database
    //in order to generate the id and the date we use helper functions
    //read more about how to use Date: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date
    const infoObject = {
        id: generateId(),
        info: body.info,
        date: new Date()
    }
    //we modify our database by adding our object to it
    //first we copy the data (so we don't modify existing data), add our object and finally store everything back
    //feel free to read about ACID: Atomicity, Consistency, Isolation, and Durability
    infoDB = infoDB.concat(infoObject)
    //we send a response with the stored object
    //and a status of 201 which means created
    res.status(201).json(infoObject)
})
``` 

In order to make a call to our post endpoint and send the data it needs we use Postman as follows:

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1649019617639/mVnVzD3tr.png)

Make sure to select all the parameters in the picture: body -> raw and JSON format.
After clicking the SEND button you should get back this:

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1649019673143/l1yVDCvx-.png)

## DELETE

```
//an endpoint to delete information from our db
//the ":id" at the end means we will be using that as a parameter
//we get the id from params.id in the request
app.delete('/api/info/:id', (req, res) => {
    //parse the data as a number since req.params.id is a string
    const id = Number(req.params.id)
    //filer back all the data that doesn't contain the requested id
    infoDB = infoDB.filter(i => i.id !== id)
    //return a code with no content and close the operation
    res.status(204).end()
})
``` 
If we want to delete the information object with the id 3 this is our call on Postman:

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1649019770003/GLyBgBIZE.png)


## PUT or Update
We will be using a helper function to obtain the object we want to modify and its id:

```
//helper function for the update operation
//we get the id of the object we want to modify
//then return the object to modify and its index in infoDB
const getInfoObjectAndIndex = (id) => {
    //declare our variables
    let infoToModify = {}
    let indexOfInfo = 0
    //find the object through the id and assign our values
    for(let i = 0; i < infoDB.length; i++){
        if(id === infoDB[i].id) {
            infoToModify = infoDB[i]
            indexOfInfo = i
        } 
    }
    //return our values in form of an array
    //so we can use destructuring to assign our variables
    return [infoToModify, indexOfInfo]
}
``` 
The actual endpoint call is as follows:

```
//an endpoint to update info
app.put('/api/info/:id', (req, res) => {
    //get the data from the body
    const body = req.body
    //if we don't get the information for our object throw an error
    if(!body.info) return res.status(400).json({
        error: 'the content is missing'
    })
    //check what you are getting(feel free to add console logs everywhere)
    console.log(body)
    //parse the date into a number
    const id = Number(req.params.id)
    //we use destructuring assignment here: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment
    const [infoToModify, indexOfInfo] = getInfoObjectAndIndex(id)
    //a console log to show the object we got
    console.log(infoToModify)
    //we make a new object with the new values
    const modifiedInfo = {
        id: infoToModify.id,
        info: body.info,
        date: infoToModify.date
    }
    //insert (or overwrite) our object into the database
    infoDB[indexOfInfo] = modifiedInfo
    //send a success status
    res.status(200).json(modifiedInfo).end()
})
``` 
In order to update our data through Postman the call should be:

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1649019856208/hE3N_6Gjc.png)
(that's the data you get after you press SEND, check through a GET call that you have all your data in the database)

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1649019917517/_LZOmX87P.png)


# GitHub and disclaimer
You can find the source code on my [Github](https://github.com/bgdnvk/MERN-stack-1) here you have the [index.js](https://github.com/bgdnvk/MERN-stack-1/blob/main/index.js) alone.

Note that this is the first chapter in a series of guides, here I haven't followed the best practices and this guide was solely made for learning purposes. If you are developing a proper product remember to use the [best security practices](https://expressjs.com/en/advanced/best-practice-security.html).

To get in direct touch with me you can hit me up on Twitter [@tekbog](https://twitter.com/tekbog)

