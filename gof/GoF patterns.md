**Gangs of Four Design patterns** (GoF) is the collection of 23 design patterns from the book "Design Patterns: Elements of Reusable Object-Oriented Softaware". (pic. 1)

![[gangs-of-four-design-patterns-book.png]]
Pic. 1 - Design Patterns: Elements of Reusable Object-Oriented Software


## Types of GoF design pattern

- ==Creational== - these patterns deal with creation of an object.
- ==Structural== - these patterns deal with class structure such as **inheritance** and **composition**. Also, ease the design by identifying a simple way to realize relationships among entities. 
- ==Behavioral== - these type of design patterns provide solution for the better interaction between object, how to provide lose coupling, and flexibility to extend in future

## Creational design patterns

1) ==Singleton== - this design pattern restrict the initialization of a class to ensure that only one instance of the class can be created. For example, object to interact with database, or resource accession etc.
2) ==Factory== - the factory pattern takes out the responsibility of object creation from class to a Factory class (special dedicated class). For example model entity creation, DTO creation, etc.
3) ==Abstract factory== - allows create a Factory for a factory classes. this pattern manipulates with object factories (entity factory, database connection factory, etc)
4) ==Builder== - create object step by step. It's coming useful when consistency of object initialization is important or structure of one is very complex and depended. For example, computer booting, OS initialization, etc. 
5) ==Prototype== - creating a new object instance from another similar instance then modify according to our requirements. Very useful, when object creation is a costly affair and requires a lot of time and resources. Also you have  a similar object already existing. So, `Prototype` design pattern provides a mechanism to copy the original object to a new object and then modify it according to our needs. Come useful for object cloning. (**BRO learn it up**)

## Structural design patterns

1) ==Adapter== - provides interface between two unrelated entities so that they can work together. For example we have user entities and computer entities. they can not store together according their own class type and interface, but we can add another abstraction layer above their interfaces. So, now  we can operate on Computers and Users such as simple `IEntity` entities and store in single collection.
2) ==Composite== - this design pattern provides a tree structed group of object, where client treat each object in the same way and do not distinct anything. (Pic. 2 'Composite diagram')

	![[Pasted image 20240118202844.png]]
	Pic. 2 - Composite design pattern diagram.
	
	As you can see for better experience composite class support dynamic addition and deletion. This pattern very use in plugin system where we awaiting a predefined result from different outcoming plugins. 
3) ==Proxy==  - provides a special class functioning as an interface to something else.  For example, we have special fully secured nuclear reactor where each operation is very consistent and takes a huge control of deferent parameters. So we implement `proxy` object which project us this reactor and we interact with proxy like a real nuclear reactor. Indeed each of our action projecting in special secure consistence of operation and sending to reactor. Also, there is second example, aircraft remote control. person from land can control the pane via special interface on board, where each received command  is interpreted in special plane action (checking wind direction, weather forecast, etc)
4) ==Flyweight==  - provides memory efficient concept of resource using. For example we have text editor (like Word, Open Office, etc) each character is represented as a special structure:
	- character of text
	- glyph to show
	when we store each character such as `{a: AGlyphObject}` we trashing up the memory space. So we can express two types of properties:
		- **intrisic** properties: immutable properties in each object
		- **extrisic** properties: muttable properties in each object
	so each intrisic prop we can store in special **once** predefined associated array (dictionary, map, etc) data structure and increase memory efficient with the '**Flyweight**' pattern.
5) ==Bridge== - provides interface abstraction from its implementation. Help us to hide details from the client side. So two can be very independently.
6) ==Decorator== - used to modify the functionality of object at runtime.
7) ==Facade== - this pattern provides wrapper interface on top of the existing interfaces to ease using for client side.

## Behavioral design patterns

1) ==Template method== - defines the skeleton of an algorithm as an abstract class, allowing its subclasses to provide concreate behavior.
2) ==Mediator== - used to provide centralized communication medium between different objects in a system.
3) ==Chan of Responsibility==  - used to achieve loose coupling in software where each client request is passed to a chain of objects to process them. Delegates command to a chain of processing objects.
4) ==Observer== - useful when you are interested in  the state of an object and want to get notified whenever there is any change.
5) ==Strategy== - used when we have multiple algorithms for a specific task and client decides the actual implementation to be used in runtime
6) ==Command== - creates objects that encapsulate actions and parameters to be performed. Loose coupling in a request-response model.
7) ==State== - this design pattern is used when an object change it's own behavior based on it's internal state
8) ==Visitor== - used when we have to perform operation on a group of similar objects. With the help of visitor pattern we can move the operational logic from the objects to another class. For example, we have multiple goods in shopping cart. Each item has it's own `accept` method which perform counting functionality and summing price to the total bill for a customer. So, in this example shopping cart visit each selected item from store and pass through each of ones and perform item specific price-count operation and total summing.
9) ==Interpreter== - design pattern that specifies how to evaluate sentence in a language. basic idea is to have a class for each symbol in specialized computer language. The syntax tree of a sentence in the language is an instance of the `Composite`and is used to interpret the sentence for a client
10) ==Iterator== - used to provide a standard way to travers through a group of objects.
11) ==Memento== - this design pattern is used when we want to save the state of an object so that we can restore later. Provides ability to restore an object to its previous state (undo).