## MERN Stack: test Node.js and Express with Jest

# Introduction
[We will be using the code from the 2nd part of this series.](https://bognov.tech/mern-stack-use-mongodb-with-nodejs-and-express-through-a-restful-api)

You can find the code in this [Github repository](https://github.com/bgdnvk/MERN-stack-2/tree/testing), note that you are on the *testing* branch.

hmu [@tekbog](https://twitter.com/tekbog) if you find any bugs or want to annoy me.

# About testing and QA

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1649361358546/XmZ3pUiUj.png)


People still fight over definition and how it should be done, however [this article from IBM](https://www.ibm.com/topics/software-testing) might give you some insight if you are unfamiliar with software testing.

To **largely** simplify testing we can define some concepts:
- Unit tests: as the definition implies we will test simple units of code, one function at a time. 
- Integration tests or I&T: is when you test several functions or different pieces of code that work together
- End to End testing: as the name implies you fully test your whole application, often as an emulated user
- Test Driven Development: write the test for the function you want, then write the function

A lot of different tools exist for almost any language, in JavaScript the most famous ones are [Jest, Mocha and Cypress for E2E](https://bognov.tech/full-stack-development-in-2022-trends-frameworks-and-languages#heading-testing-do-people-actually). However the overall most famous E2E tool might be [Selenium](https://www.selenium.dev/).


# Git
I'm not going to go into detail here, if you unfamiliar with Git and want to learn more about check out this [tutorial from Atlassian](https://www.atlassian.com/git/tutorials/using-branches/git-checkout). 
Start at the beginning if you are confused. A few key points for newbies:
- Git is a version control tool
- Github is the *hub* that hosts Git projects, it's owned by others and there are other companies such as Bitbucket and Gitlab that do the same.

I'm using my old project so I'm going to make a new branch with


```
git checkout -b testing main
``` 
and stay here as this will be the branch for this article.

# Jest (or Mocha)
We will be using [Jest](https://jestjs.io/) since we want to focus on React, however if you are working with Node.js and Mongoose [it's discouraged even in the official Mongoose docs](https://mongoosejs.com/docs/jest.html) so feel free to use an alternative like [Mocha](https://mochajs.org/). We will use Jest as our application isn't complex enough to run into problems and we will focus on React in the future.  

Let's install Jest

```
npm install --save-dev jest
``` 
Afterwards inside ```
package.json
``` modify the test script

```
"test": "jest --verbose"
``` 
You should have this:


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1649360552459/9ebuWy5lS.png)

### Start testing
Now that we have Jest installed let's make some dummy tests to see how it works.

*NB: I will be using normal import/export as ES6 module exports might give you some issues.*

Let's make a helper file inside utils folder that will contain our function we want to test ``` test_helper.js ```:


```
//return the sum of two numbers
const sumFunction = (a,b) => {
    return a+b
}

module.exports = {
    sumFunction
}
``` 

Next we will make a folder called tests and inside a file called dummy.test.js where we will test the function above:


```
const { sumFunction } = require("../utils/test_helper")
//tests take a description and a function
test('test sumFunction, expected to pass', () => {
    const a = 5
    const b = 6
    const result = sumFunction(a, b)
    //through expect we indicate the expected result of the test
    //the .toBe method expects a specific value you pass
    //https://jestjs.io/docs/expect#tobevalue
    expect(result).toBe(11)
})
test('test sumFunction, expected to fail', () => {
    const a = 5
    const b = 6
    const result = sumFunction(a, b)

    expect(result).toBe(12)
})
``` 

Note that .test is needed so Jest knows to read your tests from this file.
Now let's do

```
npm run test
``` 
This should be the result:

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1649365476196/mlhvacqEp.png)

Check out many of the Expect methods Jest has [here](https://jestjs.io/docs/expect)

# Testing a RESTful API
We will be using ES6 modules so we need to make some changes in our package.json as follows:

```
"test": "node --experimental-vm-modules node_modules/jest/bin/jest.js --verbose --runInBand --forceExit"


``` 
[Jest gives you more information here.](https://jestjs.io/docs/ecmascript-modules)

We will be using [Supertest](https://www.npmjs.com/package/supertest), so let's install it

```
npm install supertest
``` 

Now let's make a file inside tests called ```api.test.js``` where we will be importing everything we need to make our tests:

```
import supertest from 'supertest'
import { app } from '../app.js'
//use the supertest object as our API
const api = supertest(app)

import { Item } from '../models/item'
``` 
Then remember to run our server with ```npm start dev``` so it restarts every time we make changes and open a new window terminal so we can type our Jest commands.

## GET test
Since we are getting our data from a server we will need to use async functions, keep that in mind.

This is a test for our GET call expecting a 200 status:

```
test('GET call', async () => {
    await api
        .get('/api/items')
        .expect(200)
})
``` 

You can run this test through this command

```
run npm test -- -t "GET call"
```
That's how you run individual tests.  

In order to make the test a bit more complete we will also add a method to expect JSON data:

```
test('GET call', async () => {
    await api
        .get('/api/items')
        .expect(200)
        .expect('Content-Type', /application\/json/)
})
``` 
Your ```api.test.js``` file should look like this by now

```
import supertest from 'supertest'
import { app } from '../app.js'
//use the supertest object as our API
const api = supertest(app)

//run npm test -- -t "GET call"
//test GET or READ call on localhost:3001/api/items endpoint
test('GET call', async () => {
    await api
        .get('/api/items')
        .expect(200)
        .expect('Content-Type', /application\/json/)
})
``` 

## POST test
In order to interact with the database properly we will use our Mongoose model

```
import { Item } from '../models/item'
``` 
Afterwards we will proceed to make a POST call

```
test('POST call', async () => {
    //build a new item
    const newItem = {
        description:"sent from Jest!",
        likes: 10
    }
    //we send the item object to the DB through the API
    //we expect a successful result
    await api
        .post('/api/items')
        .send(newItem)
        .expect(201)
    //get all the items in our DB
    const items = await Item.find({})
    //let's check that the last item added was indeed newItem object
    //it should contain the description "sent from Jest!"
    expect(items[items.length-1].description).toBe("sent from Jest!")
})
``` 
## GET item by id

In this test we are going to check if the GET route by specific id works as expected.

```
test('GET one', async () => {
    //get all the items
    const items = await Item.find({})
    //get the the first item parsed to JSON
    const firstItem = items[0].toJSON()
    //get the result expecting success and JSON data
    const resItem = await
        api.get(`/api/items/${firstItem.id}`)
        .expect(200)
        .expect('Content-Type', /application\/json/)
    //check if the item has the same id and the route works as expected
    expect(resItem.body.id).toEqual(firstItem.id)
})
``` 

## Check all items have an id

Let's add one more simple test

```
    test('check all items have ids', async () => {
        //get all the items
        const items = await api.get('/api/items')
        //check that every item in our DB has the id property
        for(const item of items.body){
            expect(item.id).toBeDefined()
        }
    })
``` 


## Refactoring GET calls
Let's use [describe](https://jestjs.io/docs/api#describename-fn) to put our three GET calls together as follows:

```
describe('GET calls', () => {
    //run npm test -- -t "GET call"
    //test GET or READ call on localhost:3001/api/items endpoint
    test('GET call', async () => {
        await api
            .get('/api/items')
            .expect(200)
            .expect('Content-Type', /application\/json/)
    })
    //npm test -- -t "GET one"
    //GET item by id
    test('GET one', async () => {
        //get all the items
        const items = await Item.find({})
        //get the the first item parsed to JSON
        const firstItem = items[0].toJSON()
        //get the result expecting success and JSON data
        const resItem = await
            api.get(`/api/items/${firstItem.id}`)
            .expect(200)
            .expect('Content-Type', /application\/json/)
        //check if the item has the same id and the route works as expected
        expect(resItem.body.id).toEqual(firstItem.id)
    })
    test('check all items have ids', async () => {
        //get all the items
        const items = await api.get('/api/items')
        //check that every item in our DB has the id property
        for(const item of items.body){
            expect(item.id).toBeDefined()
        }
    })
})
``` 
Afterwards we can use this cmd to call this block of tests

```
npm test -- -t "GET calls"
``` 

If everything is successful we will get this in the console:

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1649376311674/cFVqbAhDh.png)

## DELETE

Let's check that we can delete an item and all its data is gone

```
test('DELETE item', async () => {
    //get items and parse the one you want to delete to JSON
    const itemsAtStart = await Item.find({})
    const itemToDelete = itemsAtStart[0].toJSON()
    //delete the item by id
    await api
        .delete(`/api/items/${itemToDelete.id}`)
        .expect(204)
    //get all items from the database again
    const itemsNow = await Item.find({})
    //check if the number of current items is one less than before
    expect(itemsNow).toHaveLength(itemsAtStart.length-1)
    //get an array of all the descriptions inside the DB
    //could get any other info like the id
    const itemsDescriptions = itemsNow.map(i => i.toJSON().description)
    //expect the description from the deleted item to not be there
    expect(itemsDescriptions).not.toContain(itemToDelete.description)
})
``` 

## beforeEach
If you want to run any code before tests start you need to use [beforEach](https://jestjs.io/docs/api#beforeeachfn-timeout). In our case we want our database to reset every time we start testing so let's make some data to insert inside a file called ```test_helper.js``` 

```
const initialItems = [
    {
        description: "first item",
        likes: 5
    },
    {
        description: "second item",
        likes: 7
    },
    {
        description: "third item",
        likes: 10
    }
]

export {
    initialItems
}
``` 

then import that data and use it to reset our database every time we start testing. We delete everything and then insert our initial data again:

```
beforeEach(async () => {
    await Item.deleteMany({})
    await Item.insertMany(initialItems)
})
``` 

## afterAll
If you want to run something after all our tests are done then use afterAll

```
afterAll(() => mongoose.connection.close())
``` 
In our case we just close the connection to the database.



