## Creational Design Pattern: Factory Method with Java code examples

# Intro 
This is the first article on [design patterns](https://en.wikipedia.org/wiki/Software_design_pattern). It has a brief dive into tools and architecture as well as explaining the Factory Method.

Let's pretend you are a software engineer at a big corporation and you are tasked with designing a program. Now, since the majority of software is a hot mess you can just load up the bloated [Electron](https://www.electronjs.org/) app and do as many nested for loops as possible with one giant class. The manager is going to LGTM your PR anyway. 

![imagen.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1651808044151/HX43-3Lz-.png align="center")

However, while working on your own projects you might want to have nice performance and architecture. This is where the design patterns come into play. Nowadays everything is handled by whatever frameworks you use but it's still easy to make a mess.

If you want to start somewhere simpler check out my [previous article about software engineering principles](https://bognov.tech/software-engineering-oop-principles-and-good-practices-to-avoid-spaghetti-code).  

For questions/feedback or anything you can find me on twitter [@tekbog](https://twitter.com/tekbog).

# Resources 
[Design Patterns](https://en.wikipedia.org/wiki/Design_Patterns) is a famous book that was written by the [Gang of Four](https://en.wikipedia.org/wiki/Design_Patterns) that shows 23 design patterns so the peasants like us could design better software. If you have the opportunity to buy the book you probably should.  

Additionally there's a friendlier version called Head First Design Patterns.  

Although the **best resource** I've found is [**Refactor Guru**](https://refactoring.guru/), it's completely free and if you want more information you can buy their book. I can not recommend it enough.

Now, if the social media has rotted your brain and you can't read for 5 minutes straight like me then an entertaining [video series from Christopher Okhravi](https://www.youtube.com/playlist?list=PLrhzvIcii6GNjpARdnO4ueTUAVR9eMBpc) might be better suited for your needs. 

If someone can teach programming and software engineering it's definitely this man:

![imagen.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1651809725509/2xz7u8kiZ.png align="center")

If you clicked on the picture you should definitely learn more about git, especially the good command.  

![imagen.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1651810028004/HEMIVFVVd.png align="left")

# Concepts to know
- Composition over inheritance
- SOLID principles

You can find information on this topics in my [previous article](https://bognov.tech/software-engineering-oop-principles-and-good-practices-to-avoid-spaghetti-code).

## Inheritance: Interface VS Abstract Class  
Before jumping into designing software architecture you need to really understand how Inheritance works.  
The most confusing concept is [Abstract Class](https://docs.oracle.com/javase/tutorial/java/IandI/abstract.html). Mainly because it's a thing between an interface and a normal class. You can't instantiate it, you HAVE to extend it (make subclasses) and if it has abstract methods then you also have to implement those.  

Please read up on OOP and inheritance if you aren't familiar with the terms.

## UML  
I will only be using the basics to explain inheritance and so on.  
Here's a picture from [Ivencia](http://www.ivencia.com/index.html?/softwarearchitect/chapter1/chapter1.htm): 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1651959844452/ahrqYZ2zt.png align="center")


# Design Patterns 
There are three types of design patterns:  
- Creational
- Structural 
- Behavioral 

I will do an article for each of them as the content is too big (and I need articles for my blog hehehe). However I insist that [Refactoring Guru](https://refactoring.guru/) might have everything you need, just scroll a bit.  

## Factory Method
Let's say you [want to build a horse](https://toggl.com/blog/build-horse-programming)..

![imagen.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1651810755212/XsxG6FvL-.png align="left")

The Factory Method allows you to simplify the procedure of building similar objects by having one main interface (or class) from which you can build concrete objects, and then the client will use the class factory to make more of whatever objects they need.  
[Refactor Guru](https://refactoring.guru/design-patterns/factory-method) sums it well: 
> Factory Method is a creational design pattern that provides an interface for creating objects in a superclass, but allows subclasses to alter the type of objects that will be created.

The diagram for Factory Method is as follows: 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1651973177975/rvViwx_pe.png align="center")
I'm using [draw.io](https://app.diagrams.net/) for doing these UML diagrams.

Design patterns are all about adding abstraction and simplify any changes to the code you want to make, basically they are there so you follow the SOLID principles as much as you can. 

### Practical example
Let's imagine we have a store and we have a lot of different clothes, in our example however we will only two types: basic clothes and fancy clothes. However thanks to the design pattern you can extend the app with more products. **Additionally you could also have only one main Creator (factory) and cut the client completely from being associated with the interface and the abstract class.**

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1652060090046/XhPi3TEd2.png align="center")

I'm using [BlueJ](https://www.bluej.org/) for this diagram.

Let's break it down: 
- concrete products that implement the general product interface
- concrete creators with the factory methods that extend a general creator class  

Rest of the arrows are associations, it means in one way or another the classes are related and use each other.  As you can see in the middle of everything the Client is using every class because we are using casting, if we made it simpler and more abstract this wouldn't be the case.  

Here is a simpler implementation of the [Factory Method](https://www.journaldev.com/1392/factory-design-pattern-in-java). And of course you can check [Refactor Guru](https://refactoring.guru/design-patterns/factory-method/java/example), they are using an UI example which I might recommend checking out and comparing it with my implementation.

#### Code
Let's get dirty and look at the code:

```
public interface Product {

    String getName();
    void setName(String name);

    double getPrice();
    void setPrice(double price);

    boolean isDiscount();
    void setDiscount(boolean discount);
}
``` 
This is the interface for the products we want to make produce with our factories.

Next we will see the two implementations we have:

```
//basic product
public class ProductA implements Product {
    //variables for all products
    private String name;
    private double price;
    private boolean discount;
    //additional variable for productA
    private int weight;

    public ProductA(String name, double price, boolean discount) {
        this.name = name;
        this.price = price;
        this.discount = discount;
    }

    @Override
    public String getName() {
        return name;
    }

    @Override
    public void setName(String name) {
        this.name = name;
    }

    @Override
    public double getPrice() {
        return price;
    }

    @Override
    public void setPrice(double price) {
        this.price = price;
    }

    @Override
    public boolean isDiscount() {
        return discount;
    }

    @Override
    public void setDiscount(boolean discount) {
        this.discount = discount;
    }

    public int getWeight() {
        return weight;
    }

    public void setWeight(int weight) {
        this.weight = weight;
    }

    @Override
    public String toString() {
        return "ProductA{" +
                "name='" + name + '\'' +
                ", price=" + price +
                ", discount=" + discount +
                ", weight=" + weight +
                '}';
    }
}
``` 

A slightly different product:

```
//extra product
public class ProductB implements Product{
    //variables for all products
    private String name;
    private double price;
    private boolean discount;
    //additional variable for productB
    private String type;
    private int items;

    public ProductB(String name, double price, boolean discount) {
        this.name = name;
        this.price = price;
        this.discount = discount;
    }

    @Override
    public String getName() {
        return name;
    }

    @Override
    public void setName(String name) {
        this.name = name;
    }

    @Override
    public double getPrice() {
        return price;
    }

    @Override
    public void setPrice(double price) {
        this.price = price;
    }

    @Override
    public boolean isDiscount() {
        return discount;
    }

    @Override
    public void setDiscount(boolean discount) {
        this.discount = discount;
    }

    public String getType() {
        return type;
    }

    public void setType(String type) {
        this.type = type;
    }

    public int getItems() {
        return items;
    }

    public void setItems(int items) {
        this.items = items;
    }

    @Override
    public String toString() {
        return "ProductB{" +
                "name='" + name + '\'' +
                ", price=" + price +
                ", discount=" + discount +
                ", type='" + type + '\'' +
                ", items=" + items +
                '}';
    }
}
``` 
Whenever you'd want to modify the implementation or add methods you could just go to this class and modify it, and thanks to the interface you can keep making new products that fit your needs.  

Now let's look at the Creator, the only requirement here is that it has to have the factory method, so we keep it simple.


```
public abstract class Creator{
    //factory method
    public abstract Product createProduct(String name, double price, boolean discount);
}

``` 
Note that you could make a createProduct method without arguments, it all depends on what you wanna do. 

Once we have the Creator we will implement the creators for our 2 products:
```
public class CreatorA extends Creator{

    public CreatorA(){
        System.out.println("FactoryA running, add additional logic here");
    }

    //factory method
    @Override
    public Product createProduct(String name, double price, boolean discount) {
        return new ProductA(name, price, discount);
    }

}
``` 

The second is almost the same, keep in mind that in a real application you might have to include some business logic as things aren't usually this simple (but sometimes they are).

```
public class CreatorB extends Creator{

    public CreatorB(){
        System.out.println("FactoryB running, add additional logic here");
    }

    //factory method
    @Override
    public Product createProduct(String name, double price, boolean discount) {
        return new ProductB(name, price, discount);
    }
}
``` 

The Factory Method design pattern is ready to use, let's implement the Client. Now, since this is just an example for educational purposes keep in mind that the ArrayList could be a connection to the database and the client could be a layer that communicates with the frontend which listen to different user inputs. And of course you could add more business logic here and there:


```
import java.util.ArrayList;

public class Client{
    //store the products from the factories
    //imagine as you are storing the data in a db
    ArrayList<Product> products = new ArrayList<>();

    public Client(){

    }

    public void printItems(){
        for(Product p: products){
            String name = p.toString();
            System.out.println("product on the list: "+name);
        }
    }
    //initialize the app, everything runs on the Client object
    public static void main(String[] args) {
        Client runClient = new Client();
        runClient.createProductsA();
        runClient.createProductsB();
        runClient.printItems();
    }

    //the next 2 methods are to build different objects
    //you could move this logic anywhere and ask the client for the input
    //or listen to events, etc
    public void createProductsA() {
        Creator factoryA = new CreatorA();
        //we have to cast in order to use the specific class methods
        ProductA p1 = (ProductA) factoryA
                .createProduct("shirt", 20, true);
        p1.setWeight(1);
        products.add(p1);
        ProductA p2 = (ProductA) factoryA
                .createProduct("shoes", 30, true);
        p1.setWeight(3);
        products.add(p2);
    }

    public void createProductsB() {
        Creator factoryB = new CreatorB();
        ProductB p1 = (ProductB) factoryB
                .createProduct("fancy shirt", 50, false);
        p1.setType("special edition");
        p1.setItems(3);
        products.add(p1);
    }
}
``` 

After you compile and run you should get this output:

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1652061212703/_FhKkbLJo.png align="center")

*NB: I'm using Java 17 but it shouldn't be a problem to run the code on previous versions.*





