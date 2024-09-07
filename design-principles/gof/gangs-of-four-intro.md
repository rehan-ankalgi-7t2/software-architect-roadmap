# Gangs of Four (GoF) Design Patterns

### History & book origin
This book was first published in 1994 and it’s one of the most popular books to learn design patterns. The book was authored by Erich Gamma, Richard Helm, Ralph Johnson, and John Vlissides. It got nicknamed as Gangs of Four design patterns because of four authors. Furthermore, it got a shorter name as “GoF Design Patterns”.

### GoF Design Pattern Types
GoF Design Patterns are divided into three categories:

`Creational`: The design patterns that deal with the creation of an object.

`Structural`: The design patterns in this category deals with the class structure such as Inheritance and Composition.

`Behavioral`: This type of design patterns provide solution for the better interaction between objects, how to provide lose coupling, and flexibility to extend easily in future.

## Creational Design Patterns
There are 5 design patterns in the creational design patterns category.

| Pattern Name | Description |
| --- | --- |
| Singleton | The singleton pattern restricts the initialization of a class to ensure that only one instance of the class can be created. |
| Factory | The factory pattern takes out the responsibility of instantiating a object from the class to a Factory class. |
| Abstract Factory | Allows us to create a Factory for factory classes. |
| Builder | Creating an object step by step and a method to finally get the object instance. |
| Prototype | Creating a new object instance from another similar instance and then modify according to our requirements. |

## Structural Design Patterns
There are 7 structural design patterns defined in the Gangs of Four design patterns book.

| Pattern Name | Description |
| --- | --- |
| Adapter | Provides an interface between two unrelated entities so that they can work together. |
| Composite | Used when we have to implement a part-whole hierarchy. For example, a diagram made of other pieces such as circle, square, triangle, etc. |
| Proxy | Provide a surrogate or placeholder for another object to control access to it. |
| Flyweight | Caching and reusing object instances, used with immutable objects. For example, string pool. |
| Facade | Creating a wrapper interfaces on top of existing interfaces to help client applications. |
| Bridge | The bridge design pattern is used to decouple the interfaces from implementation and hiding the implementation details from the client program. |
| Decorator | The decorator design pattern is used to modify the functionality of an object at runtime. |


## Behavioral Design Patterns
There are 11 behavioral design patterns defined in the GoF design patterns.

| Pattern Name | Description |
| --- | --- |
| Template Method | used to create a template method stub and defer some of the steps of implementation to the subclasses. |
| Mediator | used to provide a centralized communication medium between different objects in a system. |
| Chain of Responsibility | used to achieve loose coupling in software design where a request from the client is passed to a chain of objects to process them. |
| Observer | useful when you are interested in the state of an object and want to get notified whenever there is any change. |
| Strategy | Strategy pattern is used when we have multiple algorithm for a specific task and client decides the actual implementation to be used at runtime. |
| Command | Command Pattern is used to implement lose coupling in a request-response model. |
| State | State design pattern is used when an Object change it’s behavior based on it’s internal state. |
| Visitor | Visitor pattern is used when we have to perform an operation on a group of similar kind of Objects. |
| Interpreter | defines a grammatical representation for a language and provides an interpreter to deal with this grammar. |
| Iterator | used to provide a standard way to traverse through a group of Objects. |
| Memento | The memento design pattern is used when we want to save the state of an object so that we can restore later on. |

## Which Ones to Focus on First?
**Creational**: Singleton, Factory Method, Builder
**Structural**: Adapter, Decorator, Facade
**Behavioral**: Strategy, Observer, Command

These design patterns are practical and widely applicable in many software development projects, especially in web development, where you often face the need for flexible and scalable architectures.

**Note**:If you're working on *React/Node.js/Django projects*, focus on patterns like Observer, `Factory`, `MVC`, and `Strategy`, as these are highly relevant to frameworks and libraries you likely use.