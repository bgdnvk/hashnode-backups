## Introduction to Golang: build a mini Twitter clone

# TL;DR

This article is for those who want to quickly glance over Golang and build a small project, it serves as an introduction into the language.

After going through the post you will know how to build a simple CRUD app and you will be somehow familiar with Go syntax to start your own project.

If you have feedback you can reach me out on Twitter [@tekbog](https://twitter.com/tekbog) or leave a comment here.

The repo for this project can be found [HERE](https://github.com/bgdnvk/mini-twitter-clone).

If you are unfamiliar with API/backend development I have starting series with both [Node](https://bognov.tech/series/mern-stack) and [Spring Boot](https://bognov.tech/series/spring-boot) you can check.

# Why Golang?


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1656552531384/dXq6mAQvC.png align="center")

If you want to build loosely coupled micro services that are low on memory and scalable Go is probably one of the best choices, if not the best, considering the fact that [Kubernetes](https://github.com/kubernetes/kubernetes), [Docker](https://github.com/docker) and [Terraform](https://github.com/hashicorp/terraform).  

Additionally many other companies use it such as [Uber](https://eng.uber.com/go-geofence-highest-query-per-second-service/) and of course the tech giant [Google](https://go.dev/solutions/google/) is using it heavily internally.

Overall Go excels in the back end with Goroutines and Channels. It offers quick development with a minimalist C-like language.


# Go Syntax


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1656552612011/4tVkG1g4D.png align="center")

You can use this page as the [Go syntax cheat sheet](https://devhints.io/go) or start the [Go tour](https://go.dev/tour/welcome/1) from the official site.

## Concurrency

I'm not going to go into concurrency, however [here](https://www.golangprograms.com/go-language/concurrency.html)'s a good enough tutorial to get you started.  
To paraphrase a bit:  
>**Goroutine **is a lightweight thread.  

>**Channel **allows to send data between Goroutines.

Now keep in mind that while looking for Go docs the last release as of today **[1.18 has introduced Generics](https://go.dev/blog/go1.18)** so some of the old tutorials might be outdated.

Let's get through some basics to get you started.

## Imports and exports

In every new file you will need to declare its package right at the start such as:
`  
package services
`


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1656468732456/0tRSwyUcI.png align="center")

Then in order to use export (or expose) a function you need to start it with a capital letter. In the example above you can see that the function `GetFeedTweets` starts with a capital letter, this means I'm making it "public".  
Afterwards just import the package like: `import ("project-folder-name/package")` and you will be use the function by invoking the package name followed by the dot and the function like: `package.FunctionName`.  

Note that when working with Structs you have to make the fields start with capital letter if you want to expose them. Otherwise you will end [like me](https://twitter.com/tekbog/status/1539787225692602373):

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1656469197291/1DnQAPtJU.png align="left")

## Golang is case sensitive

**REMEMBER THIS OR YOU WILL SUFFER**

## Pointers


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1656470773044/LO-XsoIDD.png align="center")

I won't be covering pointers in detail as it's a lengthy topic, however [here's an article](https://medium.com/@annapeterson89/whats-the-point-of-golang-pointers-everything-you-need-to-know-ac5e40581d4d#:~:text=%E2%80%9C%20Pointers%20are%20used%20for%20efficiency,we%20want%20to%20mutate%20it%20.%E2%80%9D) that should make a good introduction.

The [Go tour](https://go.dev/tour/moretypes/1) also offers a quick introduction.

To sum it up (badly, please read up on it):


```
//declare int variable that equals to 42
var i = 42
//make p an int pointer
var p *int
//assign the i memory address to p
p = &i
	
//p is just a pointer holding memory
//will print 0xc0000b8000
fmt.Println(p)

//p* points to the memory address it's holding
//will print 42
fmt.Println(*p)
```

You will see functions getting parameters like ```func FuncName (p *pointerType)``` just use p as you normally would.

## Variadic functions:

If you come from the JavaScript world you will know how useful this is as it works the same as the spread operator, [here's a quick tutorial](https://www.geeksforgeeks.org/variadic-functions-in-go/?ref=lbp).

Here's a quick example from [StackOverflow](https://stackoverflow.com/a/17556146/14356309):

```
package main
import "fmt"

func my_func( args ...int) int {
   sum := 0
  //the underscore in golang is called the "blank identifier"
   for _, v := range args {
      sum = sum + v
   }

   return sum;
}

func main() {
    arr := []int{2,4}
    sum := my_func(arr...)
    //prints: Sum is  6
    fmt.Println("Sum is ", sum)
}
``` 

However it's easier to understand how it works with strings:

```
package main

import (
	"fmt"
	"strings"
)

func joinString(element ...string) string {
	return strings.Join(element, ",")
}

func main() {
  
    //will print "join,this"
	fmt.Println(joinString("join", "this"))
    //will print "a,a,a"
	fmt.Println(joinString("a", "a", "a"))

}
``` 



## Make

The quickest way to *make * a slice, which is a dynamic array, just do 
```
a := make([]int, 5)
``` 
Here's the page from the [Go tour](https://go.dev/tour/moretypes/13)

## Range

Golang doesn't have a forEach function however it uses range instead so if you want to loop through all the elements of an array or slice just do:

```
for index, element := range yourSlice{
        fmt.Println(index)
        fmt.Println(element)
}
``` 

You can find more examples in this site with [golang code examples](https://gobyexample.com/range).


## Maps

Maps, hash tables or dictionaries - in Golang they are used as follows:

```
	m := map[string]int{
		"first-key": 5,
		"second-key":  10,
	}
	fmt.Println(m) 

	for key, value := range m { // Order not specified
		fmt.Println(key, value)
	}
``` 

[Here](https://gobyexample.com/maps)'s a quick summary about maps.


## Methods:

Golang doesn't have classes however it has methods. It sounds counter intuitive but it works great, if you have worked with OOP before just think of Structs as classes/objects. You define a function for them and then use that function on the Struct with a dot call, here's an example.


```
import "fmt"

type User struct {
	Id   int
	Name string
}

//method to set user's name
func (u *User) setName(newName string) {
	(*u).Name = newName
}

func main() {

	//initialize a new user
	newUser := User{
		Id:   0,
		Name: "First Name",
	}
	//User's ID:  0
	fmt.Println("User's ID: ", newUser.Id)
	//User's Name:  First Name
	fmt.Println("User's Name: ", newUser.Name)

	// make a pointer to the newUser
	pointerNewUser := &newUser

	// call your method
	pointerNewUser.setName("Name From Pointer")
	//User's Name:  First Name
	fmt.Println("Same User's Id: ", pointerNewUser.Id)
	//User's new name: Name From Pointer
	fmt.Println("User's new name:", pointerNewUser.Name)
}
``` 


## Print


When you want to print something to the console remember to use the proper verbs:

```
%v	the value in a default format when printing structs, the plus flag (%+v) adds field names
%#v	a Go-syntax representation of the value
%T	a Go-syntax representation of the type of the value
%%	a literal percent sign; consumes no value
``` 
 That's from the [official documentation](https://pkg.go.dev/fmt).

For example a normal expression would be:

```
fmt.Printf("checking user: %v\n", user)
``` 



## TypeOf: Reflection

If you want to examine types during runtime then you need to use the reflect package:

```
package main

import (
	"fmt"
	"reflect"
)

type user struct {
	Id   int
	Name string
}

type blog struct {
	User_id int
	Data    string
	Date    string
}

//this is a generic function since I'm using the keyword "any"
func checkTypeAndValue(x any) {
	userType := reflect.TypeOf(x)
	userValue := reflect.ValueOf(x)
	fmt.Println("Type ", userType)
	fmt.Println("Value ", userValue)

}
func main() {
	newUser := user{
		Id:   1,
		Name: "myUser",
	}
	checkTypeAndValue(newUser)

	newBlog := blog{
		User_id: 1,
		Data:    "this is my first blog",
		Date:    "01-01-1990",
	}
	checkTypeAndValue(newBlog)

}
``` 


## Blank identifier

You might find blank identifiers in loops or when you import a package, like:

```
  //the underscore in golang is called the "blank identifier"
   for _, v := range args {
      sum = sum + v
   }
``` 
You can find a good explanation from [Effective Go](https://go.dev/doc/effective_go#blank) about it. However to put it simple: the compiler complains if you aren't using a variable, so if you need to store something but never use it then use the underscore.

## Generics

Finally here! The type of jokes no longer work:

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1656552719138/b1Ra2TXFP.png align="center")

With 1.18 Golang has introduced generics, so be careful when you look at old tutorials.  

I'd recommend you to read on Generics if you haven't heard the term before but the gist of it is that you can use one function for many types of data, just like I did in the example of TypeOf: Reflection, there's a generic function there that accepts **any** type of data: 

```
//this is a generic function since I'm using the keyword "any"
func checkTypeAndValue(x any) {
	userType := reflect.TypeOf(x)
	userValue := reflect.ValueOf(x)
	fmt.Println("Type ", userType)
	fmt.Println("Value ", userValue)

}
``` 

This [FreeCodeCamp](https://www.freecodecamp.org/news/generics-in-golang/) article makes it quick to understand. And you can also refer to the [official Golang docs](https://go.dev/doc/tutorial/generics).

# The project: mini Twitter backend

## Notes before you start
Keep in mind this project was made mainly to show off Golang a bit, you can copy the architecture but the project is missing proper [ORM](https://en.wikipedia.org/wiki/Object%E2%80%93relational_mapping), there's no authentication or authorization in place, I'm completely disregarding middleware and there are no tests.  

I will talk about all this issues in its own sections but it's important that you are aware that this is not ready for production. 

If I had to start from scratch or remake the project I'd add libraries such as [sqlx](https://github.com/jmoiron/sqlx) and [Gorm](https://github.com/go-gorm/gorm). As well as improve the API and other changes that I go through below.

Additionally I'd like to address the routing library I'm using: [Fiber](https://github.com/gofiber/fiber). Note that it's version 2, however a lot of tutorials and blog posts are showing and talking about v1, a bit has changed since then so when looking for additional information make sure the import is ```github.com/gofiber/fiber/v2```.

Also, you should definitely have a configuration file and an .env in your project to hide your data. 

There's also a disclaimer in the [README](https://github.com/bgdnvk/mini-twitter-clone#readme):


> Disclaimer
> 
> This is an introductory project to look at Golang a bit.
> This project is not production ready and it has bad practices like the way pagination works or how we interact with the database. 
> 
> Through the codebase you will find different "prints" that are used to debug the project, feel free to play with them.
> What's missing for production ready?
> 
> You should add a proper logger, configuration, middleware, a different way to handle the data, perhaps an ORM, and a better way to handle the pagination, as well as a better API.
> 
> Note that you can make yourself vulnerable to SQL ingections if you copy and paste the code. This has been made for learning purposes.



## Database

You should probably have [Docker](https://hub.docker.com/_/mysql) running MySQL (or any other SQL database). If not you can always install MySQL on your system and use something like [MySQL Workbench](https://www.mysql.com/products/workbench/) to work with it.

### Database design

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1656481862578/yQBkZ5PgS.png align="left")

I'm using [QDBD](https://www.quickdatabasediagrams.com/) for the diagram.

The database itself is fairly simple, you have the users that tweet tweets and a table of followers to keep the data of who follows who. The followers table is mainly to implement the feed/timeline for our users.

### Create Database
In the scripts folder you will find the main script to run to start your MySQL database:


```
use twitterdb;

DROP TABLE IF EXISTS tweets;
DROP TABLE IF EXISTS users;
DROP TABLE IF EXISTS followers;

CREATE TABLE users (
  user_id INT NOT NULL AUTO_INCREMENT,
  user VARCHAR(255) NOT NULL,
  passhash VARCHAR(40) NOT NULL,
  email VARCHAR(255) NOT NULL,
  first_name VARCHAR(255) NOT NULL,
  last_name VARCHAR(255) NOT NULL,
  dob DATE,
  PRIMARY KEY (user_id)
);

CREATE TABLE tweets (
  tweet_id INT NOT NULL AUTO_INCREMENT,
  user_id INT NOT NULL,
  tweet VARCHAR(140) NOT NULL,
  date_tweet DATETIME NOT NULL,
  PRIMARY KEY (tweet_id),
  FOREIGN KEY user_id(user_id) REFERENCES users(user_id) 
  ON UPDATE CASCADE ON DELETE CASCADE
);

CREATE TABLE followers (
  id_user INT NOT NULL REFERENCES users (user_id),
  id_follower INT NOT NULL REFERENCES users (user_id),
  PRIMARY KEY (id_user, id_follower)
);

INSERT INTO users (user, passhash, email, first_name, last_name, dob) VALUES
("foo", "asdsad1", "test@gmail.com", "bob", "bobbinson", "2006-01-01"),
("foo2", "asdsad2", "test2@gmail.com", "bob2", "bobbinson2", "1992-01-01"),
("foo3", "asdsad3", "test3@gmail.com", "bob3", "bobbinson3", "1993-01-01"),
("foo4", "asdsad4", "test4@gmail.com", "bob4", "bobbinson4", "1994-01-01"),
("foo5", "asdsad5", "test5@gmail.com", "bob5", "bobbinson5", "1995-01-01"),
("foo6", "asdsad6", "test6@gmail.com", "bob6", "bobbinson6", "1996-01-01"),
("foo7", "asdsad7", "test7@gmail.com", "bob7", "bobbinson7", "1925-01-01"),
("foo8", "asdsad8", "test8@gmail.com", "bob8", "bobbinson8", "1980-01-01"),
("foo9", "asdsad9", "test9@gmail.com", "bob9", "bobbinson9", "1980-01-01"),
("foo10", "asdsad10", "test10@gmail.com", "bob10", "bobbinson10", "1970-01-01");

INSERT INTO tweets(user_id, tweet, date_tweet) VALUES
(1, "test tweet", "2001-01-01 22:00:00"),
(2, "test tweet2", "2002-01-01 22:00:00"),
(3, "test tweet3", "2003-01-01 22:00:00"),
(4, "test tweet4", "2004-01-01 22:00:00"),
(5, "test tweet5", "2005-01-01 22:00:00");

INSERT INTO followers(id_user, id_follower) VALUES
(5,1),
(4,1),
(3,1),
(2,1),
(6,1),
(2,5),
(4,5);
``` 
The other files are examples of queries that we will be using later.

## Project Architecture


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1656546490437/vnWxBjlbq.png align="left")

If you are familiar with building software this should be familiar if not, first let me tell you what's missing and afterwards we will go through every folder.

The project is missing folders like config, middleware, logger and testing. And if you would organize the controller better you'd have a routes folder where you organize the API better.

## Quick note on imports

In this project you might get confused by imports such as:

```
import (
	"goexample/database"
	"goexample/models"
	"goexample/services/utils"
)
``` 
The goexample here is the name of the project, I just renamed my repo afterwards so it would make sense, so instead of having "mini-twitter-clone/database" we use "goexample/database" to import the database package.  
With any other new projects just use the name of the folder.

## API
You store your endpoints/routes in controller.go:


```
package api

import (
	"goexample/services"

	"github.com/gofiber/fiber/v2"
)

func SetupRoutes(app *fiber.App) {

	api := app.Group("/api")

	//get all unordened users
	api.Get("/users", services.GetUsers)
	//get all users ordered by age ASC
	api.Get("/users/age", services.GetUsersByAgeAsc)

	//get all unordened tweets from db
	api.Get("/tweets", services.GetTweets)

	//http://localhost:3000/api/feed/1
	//get MOST RECENT feed/timeline for the user
	api.Get("/feed/:id", services.GetFeedTweets)
	//pagination
	api.Get("/feed/:id/:limit/:offset", services.GetFeedTweetsPaginated)
	//can try https://github.com/gofiber/fiber/issues/193#issuecomment-591976894
	//a whole presentation on why you shouldn't do what I did:
	//https://use-the-index-luke.com/no-offset

}

``` 

I'm using the Fiber library, which is similar to Express, here we have several endpoints that we call with a Get request and once the server gets a request its response is to call the functions that I have exposed from the services package - that's where our business logic is.

**NB: pagination isn't properly implemented.**  

This is just a quick example, this endpoint has security issues just like others but you should understand how the library and Golang works through the example.

Note that in the /feed/:id the id parameter pertains to the user we want to get the feed for.

### Start the project

You can start the project by doing
```go run .```
inside the folder.  
Your terminal should look like this:

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1656547397790/zr2MQc7eU.png align="left")

Let's visit the different endpoints to see the responses, I'm going to use a normal browse but you should check [Postman](https://www.postman.com/) if you are not familiar with debugging the backend.

Let's run the endpoints from the controller:
```
http://127.0.0.1:3000/api/users
``` 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1656547627951/SNvlI9-Od.png align="left")

I left a lot of prints so if you check your terminal with every call you should see stuff like:

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1656547694916/a4iv6o79v.png align="left")

Next is a call where we order users by age:


```
http://127.0.0.1:3000/api/users/age
``` 


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1656547733559/lBoD6UZ0O.png align="left")

When we ask for tweets we get all of them:


```
http://127.0.0.1:3000/api/tweets
``` 


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1656547797655/74sC-x3oC.png align="left")

And now we get the feed or timeline for the user with the id 1:


```
http://127.0.0.1:3000/api/feed/1
``` 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1656547879923/-3pmsWt0p.png align="left")

Remember that pagination isn't production ready but the core concepts are the same:

```
http://127.0.0.1:3000/api/feed/1/2/1
``` 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1656547958522/a8KyOayEB.png align="left")

All the calls work thanks to the business logic we have in the services package and the functions we have exposed.

## Services
Inside the services package we have the functions that are called when someone or something hits one of the endpoints. Remember that we expose the functions by using a capital letter in the package.

Let's look at timeline_tweets.go which contains two functions for two different endpoints in the controller.go file:


```

package services

import (
	"fmt"
	"goexample/database"
	"goexample/models"
	"goexample/services/utils"
	"log"

	"github.com/gofiber/fiber/v2"
)

func GetFeedTweets(c *fiber.Ctx) error {

	//you shouldn't do this by the way, but it's just a demo
	// dbQuery := fmt.Sprintf("SELECT users.user_id, users.user, users.first_name, users.last_name, tweets.tweet, tweets.date_tweet FROM users INNER JOIN tweets ON users.user_id = tweets.user_id INNER JOIN followers ON users.user_id = followers.id_user WHERE followers.id_follower = %s ORDER BY tweets.date_tweet DESC;", c.Params("id"))
	// rows, err := database.DB.Query(dbQuery)

	//avoid the SQL injection by rewriting it like
	dbQuery := "SELECT users.user_id, users.user, users.first_name, users.last_name, tweets.tweet, tweets.date_tweet FROM users INNER JOIN tweets ON users.user_id = tweets.user_id INNER JOIN followers ON users.user_id = followers.id_user WHERE followers.id_follower = ? ORDER BY tweets.date_tweet DESC;"
	rows, err := database.DB.Query(dbQuery, c.Params("id"))

	//check for errors
	if err != nil {
		return utils.DefaultErrorHandler(c, err)
	}
	//close db connection
	defer rows.Close()

	//create a slice of tweets
	var timelineTweets []models.TimelineTweet
	//loop through the result set
	for rows.Next() {
		timelineTweet := models.TimelineTweet{}
		err := rows.Scan(&timelineTweet.User_id, &timelineTweet.User, &timelineTweet.First_name, &timelineTweet.Last_name, &timelineTweet.Tweet, &timelineTweet.Date_tweet)
		if err != nil {
			log.Fatal(err)
		}
		timelineTweets = append(timelineTweets, timelineTweet)
	}
	fmt.Print(timelineTweets)

	utils.ResponseHelperJSON(c, timelineTweets, "timeline", "No timeline found")

	return err
}

func GetFeedTweetsPaginated(c *fiber.Ctx) error {

	// dbQuery := fmt.Sprintf("SELECT users.user_id, users.user, users.first_name, users.last_name, tweets.tweet, tweets.date_tweet FROM users INNER JOIN tweets ON users.user_id = tweets.user_id INNER JOIN followers ON users.user_id = followers.id_user WHERE followers.id_follower = %s ORDER BY tweets.date_tweet DESC LIMIT %s OFFSET %s;", c.Params("id"), c.Params("limit"), c.Params("offset"))
	// avoid a SQL injection by rewriting it like
	dbQuery := "SELECT users.user_id, users.user, users.first_name, users.last_name, tweets.tweet, tweets.date_tweet FROM users INNER JOIN tweets ON users.user_id = tweets.user_id INNER JOIN followers ON users.user_id = followers.id_user WHERE followers.id_follower = ? ORDER BY tweets.date_tweet DESC LIMIT ? OFFSET ?;"

	rows, err := database.DB.Query(dbQuery, c.Params("id"), c.Params("limit"), c.Params("offset"))
	if err != nil {
		return utils.DefaultErrorHandler(c, err)
	}

	defer rows.Close()

	var timelineTweets []models.TimelineTweet
	for rows.Next() {
		timelineTweet := models.TimelineTweet{}
		err := rows.Scan(&timelineTweet.User_id, &timelineTweet.User, &timelineTweet.First_name, &timelineTweet.Last_name, &timelineTweet.Tweet, &timelineTweet.Date_tweet)
		if err != nil {
			log.Fatal(err)
		}
		timelineTweets = append(timelineTweets, timelineTweet)
	}
	//TODO: implement a response with pages and all that pagination jazz
	utils.ResponseHelperJSON(c, timelineTweets, "timeline", "No timeline found")

	return err
}


``` 

The first that you can notice is how we pass the context to GetFeedTweets and afterwards we use the variable 'c' to use that context as the [Fiber library says](https://docs.gofiber.io/api/ctx).

Afterwards we use the exposed variable DB from the package database to open the DB, read the data and close it afterwards.

In order to store and scan the data properly we use a struct from our models package.

Afterwards you will see several functions from the utils package. Those functions are mainly helpers so you can check out how Golang does loops and certain other things.

The two other files inside our services package are very similar, our work here is get the data from the database, scan it through our array of structs and send it back to the user in JSON format. As well as we run some functions from the utils package.

### Utils
This package contains helper functions, perhaps the most interesting being inside user_helper as it has functions that interact with data from slices, **however be careful**, they are not as well implemented as you might think.

Let's look at the most helpful one, response_helper.go:

```
package utils

import (
	"github.com/gofiber/fiber/v2"
)

//response JSON for services after you loop and scan
func ResponseHelperJSON(c *fiber.Ctx, data any, dataType string, dataError string) {
	if data != nil {
		c.Status(200).JSON(&fiber.Map{
			"success": true,
			dataType:  data,
		})
	} else {
		c.Status(404).JSON(&fiber.Map{
			"success": false,
			"error":   dataError,
		})
	}
}

``` 

Note that this functions contains a generic type of data as I'm using the keyword any and I'm interacting with the context given from Fiber through the variable 'c'.


## Models
The models folder contains the different structs we use as entities to interact with our database as shown in the services folder.

Here's an example, note that even that if you want to expose the entire struct everything has to start with capital letter:

```
package models

type UserWithAge struct{
	Id         int   `json:"id"`
	User       string `json:"user"`
	Passhash   string `json:"passhash"`
	Email      string `json:"email"`
	First_name string `json:"first_name"`
	Last_name  string `json:"last_name"`
	Age        int    `json:"age"`
}
``` 

## Database
The database package is very straightforward and remember to use a config file and an .env to store your sensitive data.


```
package database

import (
	"database/sql"
	"fmt"
	"log"
)

var DB *sql.DB

func Connect() error{
	var err error
	//use a config file for this
	DB, err = sql.Open("mysql", "root:password@tcp(127.0.0.1:3306)/twitterdb")

	if err != nil {
		log.Fatal(err)
		return err
	}

	if err = DB.Ping(); err != nil {
		log.Fatal(err)
		return err
	}

	fmt.Println("Connected to database")

	return nil
	
}
``` 

## Main.go

Finally, this is where we start our server:

```
package main

import (
	"github.com/gofiber/fiber/v2"
	"goexample/database"
	"log"

	"goexample/api"

	_ "github.com/go-sql-driver/mysql"
)

func main() {

	if err := database.Connect(); err != nil {
		log.Fatal(err)
	}

	app := fiber.New()
	api.SetupRoutes(app)


    log.Fatal(app.Listen(":3000"))

}

``` 

# Bonus Ukrainian meme

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1656553993404/_Qbqn3-5h.png align="left")
