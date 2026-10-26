
Considerate 
- Make notes as if you have to teach someone all of this in simple language 

Benefits of using these principles? 

### Solid Principles 
 - S ~ Single Responsibility Principle  
 - O ~ Open Closed Principle 
 - L ~  Liskov Substitution Principle 
 - I ~ Interface Segregration Principle 
 - D ~ Dependency Inversion Principle 

##### S ~ Single Responsibility Principle  
 - A CLASS SHOULD HAVE ONLY ONE REASON TO CHANGE
 - (based on dividing one class into multiple ones)
- There should never be more than one reason for a class to change -
    - focused, single functionality
    - addresses a specific concern
	
![[Screenshot 2024-09-15 at 8.19.19 PM.png]]

-  so basically each class should have one resposibility -- if more than one, than divide into multiple classes and improve the design
-  In the example, we have moved the logic for validating and storing from the controller class to different classes

##### O ~ Open Closed Principle 
- OPEN FOR EXTENDSION, CLOSED FOR MODIFICATION 
- Open for extension - Extend the existing behaviour
- Closed for modification - Existing code should not be changed
- (based on inheritance entirely)
- Software entities should be open for extension, but closed for modification

- To avoid modifying existing base classes, and using override and inheritance in order to extend the functionality
-  So basically extract out the common part from different classes, create one base abstract class which is closed for modification and add abstract functions inside it for extension among child classes, also use protected members to access the base class members in child classes

 ##### L ~  Liskov Substitution Principle 
 - (those who do not have same behaviour should not inherit each other)

- The Liskov Substitution Principle (LSP) is one of the SOLID principles in object-oriented programming, stating that objects of a superclass should be replaceable with objects of its subclasses without affecting the correctness of the program.

 - We should be able to substitute base class objects with child class objects & this should not alter the behavior of program

- Example - Why modifying behaviour of base classes is dangerous, because we normally think every square is a rectangle, but in reality it is not like
    They both have difference in behaviour how they setWidth, setHeight and hence square should not be a child of rectangle
    Alternatively we should have a shape class - which have only one function - to compute area - and then rectangle and square should be child of shape class
    This way we would know the only thing they both will have is a function to compute area & nothing else
 
 ##### I ~ Interface Segregation Principle 
- Clients should not be forced to depend upon interfaces that they do not use - (interface pollution)
    large interfaces - nope
    unrelated methods - nope
    Write highly cohesive interfaces -- please!!

-  Interface Pollution
    -> Classes have empty method implementations
    -> Method implementations throw UnsupportedOperationException
    -> Methods implementation return null or default/dummy values

 -  In the example, someone created an interface from the given service class, and added functions which were specific to that service class
-  Now when other person created a service using that interface, he had to implement all the functions of that interface, even though he did not need them
-  Hence only keep the functions that are shared among all in the interface, and add your own functions later on in the service

##### D ~ Dependency Inversion Principle 
- High level modules should not depend on low level modules, both should depend upon Abstractions
- Abstractions should not depend on details, rather details should depend upon abstractions

-  Dependency ?
    -> When some code is tighlty dependent on other class - (business logic)
    -> Rather use interfaces/abstractions in the place of that class, so that anyone can easily change the implementation by creating a new class and it won't be affecting our code
    -> It is said inversion because earlier the responsibility of creating the object was ours, now it is of client - hence dependency inversion

-  Example
    public void writeReport(){
        Report report = new Report();
        //Build the report
        JsonFormatter formatter = new JsonFormatter();
        String report = formatter.format(report);
        FileWrite writer = new FileWriter("report.json")
        //write out report
    }
	
- Do this instead - get implemented object from user of this function only
    public void writeReport(Formatter formatter, Writer writer){
         Report report = new Report();
         //Build the report
         String report = formatter.format(report);
         writer.write("report.json")
         //write out report
    }


### Design Principles 

These are divided into three categories 
-  Creational  -> creational patterns deal with the process of creation of object of classes
-  Structural  -> structural patterns deal with the composition/arranged of classes or objects.
- Behavioural -> behavioural patterns deal with the interaction/communicate between classes and objects

#### Creational Patterns
- Builder
- Simple Factory
- Factory Method
- Prototype
- Singleton
- Abstract Factory
- Object Pool 

##### Builder Design Pattern 

Problem it solves - 
- Whenever we have a complex process to construct an object involing multiple steps, then builder design pattern can help us
-  In builder we remove the logic related to object construction from "client" code & abstract it in separate class
- Objects that needs other objects or "parts" to construct them

Steps to implement 
-  We start by creating a builder
-  Identify the "parts" of the product & provide methods to create those parts
-  It should provide a method to "assemble" or build the product/object
-  It must provide a way/method to get fully built object out. Optionally builder can keep reference to an
product it has built so the same class be returned again in future
-  A director can be a seperated class or client can play the role of director

Implementation Considerations -
-  You can easily create an immutable class by implementing builder as an inner static class. You'll find this type of implementation
Quite frequently even if immutability is not an concern. (ALWAYS PREFFERED METHOD)
-  The director role is rarely implemented as a seperate class, typically the consumer of the object instance or client handles that role
-  Abstract builder is also not required if "product" itself is not part of any inheritance hierarchy. You can directly create concrete builder
-  "To many constructor argument" -- might be the best scenario to use this bad boy

Real world Example -
-  Stringbuilder is not 100% but real world example of builder design pattern

Imagine a complex object that requires laborious, step-by-step initialization of many fields and nested objects. Such initialization code is usually buried inside a monstrous constructor with lots of parameters. Or even worse: scattered all over the client code.

Basic Idea - 
- Basically don't use contructors with so many fields, or make subclasses for each different functionality
- Create one builder class and make it such that you can use .getName().getAddress(). and so on sort of structure. 

![[Screenshot 2024-09-12 at 6.50.44 PM.png]]

- Above should be good enough, implementation practise and what not to do you can learn with problem solving probably 
- Or just put those implementation on github or somewhere

https://refactoring.guru/design-patterns/builder/java/example

#### Simple Factory  (No need for UML Diagram)

- Simply a method that encapsulates object instantiation. Nothing else complex is going on
- often confused with "Factory Method" pattern

Implementation 
- A static class with one method, which returns an object of some other class on the basis of the string provided to it. 
- Anyone can use this static class in the entire codebase, could have been a function as well 

``` 
public static class simpleFactory {
	public static Shape getShapeObject(String shape){
		if(shape === 'circle') return new Circle();
		if(shape === 'rectangle) return new Rectangle();
	}
}
```


#### Factory Method 

- When we want to move the object creation logic from our code to a seperate subclass
- We use this pattern when we do not know in advance which class we may need to instantiate beforehand & also to allow new classes to be added to the system and handle their creation without affecting client code.
- It is primarily used to isolate client code from object creation & delegate object creation to subclasses.









