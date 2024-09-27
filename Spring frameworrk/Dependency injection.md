In Spring framework there is a special way to perform dependency injection. It is using a **spring.xml** file. In this file we should define our class which will be injected into our application.  

In the beginning, we will define some classes and common interface to perform dependency injection.

Lets jump into interface definition:

``` java
package com.example.project;

//interface for our classes
public interface IVehicle
{
	void drive();
}
```

Now jump into class definition:

``` java
package com.example.project;

public class Car implements IVehicle
{
	public void drive()
	{
		System.Out.Println("Bip bip!");
	}
}

public class Bike implements IVehicle
{
	public void drive()
	{
		System.Out.Println("Vroom vroom!");
	}
}
```

Define bike class to **spring.xml** with associated key to perform dependency injection:

```xml
<?xml version="1.0" encoding="UTF-8"?>

<beans>
	<!-- id: bean's key for defined class, class: desired class to resolve-->
	<bean id="vehicle" class="com.example.project.Bike"></bean>
</beans>
```

After class definition step performed above, we can perform resolution operation such as shown in example below. But we should to discuss some things. In Spring Framework there is a special class which will resolve all of our dependency injection issues. That's called `ApplicationContext`. Without his participation we won't resolve desired class (`Bike`). 
Also there is another important one, it is `ClassPathXmlApplicationContext` class.
This class which will negotiate with our defined `spring.xml` file and will parse it to resolve desired classes. In it's constructor we need pass a path to our `spring.xml` file.

``` java
package com.example.project;

import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class App
{
	public static void main( String[] args)
	{
		// define application context based on predefined spring.xml file with needed classes
		ApplicationContext context = new ClassPathXmlApplicationContext("spring.xml");
		//resolve desired with `getBean` method, here we pass a bean key which is defined in our spring.xml file for needed class
		Vehiclee obj = (Vehicle)context.getBean("vehicle");
		//using resolved method from IoC (Instance Of Container)
		obj.drive();
	}
}
```


## Attribute based approach 
In Spring boot we can implement DI with special attribute like `@Component`. Lets takes example with `Developer` class. We have class which perform some  operations like `compile`, `debug`.

``` java
@Component
public class Developer
{
	//field basde binding
	@Autowired
	Laptop laptop;

	//constructor based binding
	public Developer(Laptop laptop){
		this.laptop = laptop;
	}
	
	//setter based binding
	public void setLaptop(Laptop laptop) {
		this.laptop = laptop;
	}

	public void compile() {
		laptop.compile();
	}

	public void debug() {
		laptop.debug();
	}
}

@Component
public class Laptop 
{
	public void compile() {
		System.out.println("compile");		
	}
	
	public void debug() {
		System.out.println("debug");		
	}
}
```

As we can see it has link with Laptop class. It shows us 3 approaches:
 - constructor based
 - setter based 
 - field based (with `@Autowired` attribute)

Each class in spring must `@Component` attribute, which make know that `Developer` and `Laptop` classes are registered in instance of container (IoC).

## Loose couple dependency injection (DI)

Based on the previous example lets say that company may give not Laptop but also Desktop to Developer for development purposes. For best practice we can implement `IComputer` interface.

``` java
public interface IComputer {
	void compile();
	void debug();
}

@Component
public class Laptop 
{
	public void compile() {
		System.out.println("compile with laptop");		
	}
	
	public void debug() {
		System.out.println("debug with laptop");		
	}
}

@Component
public class Desktop 
{
	public void compile() {
		System.out.println("compile with desktop");		
	}
	
	public void debug() {
		System.out.println("debug with desktop");		
	}
}
```

Also lets rewrite `Developer` class:

``` java
@Component
public class Developer
{
	//field basde binding
	@Autowired
	private IComputer computer;

	//constructor based binding
	public Developer(IComputer computer){
		this.computer = computer;
	}
	
	//setter based binding
	public void setLaptop(IComputer computer) {
		this.computer = computer;
	}

	public void compile() {
		computer.compile();
	}

	public void debug() {
		computer.debug();
	}
}
```

### `@Primary` and `@Qualifier` resolution
in this case we can see that we have 2 `IComputer` based classes (`Desktop` and `Laptop`)  in this case it will cause exception, because there are 2 classes with this attribute and `ApplicatioContext` cant resolve suitable class (> 1). We can resolve with `@Primary` attribute. If we will mark `Laptop` with this attribute, it will be resolved by default.  
However with have cases when `Laptop` and `Desktop` classes should have the same attributes. for this case we need mark our field with `@Qualifier`.

``` java
public interface IComputer {
	void compile();
	void debug();
}

@Component
public class Laptop 
{
	public void compile() {
		System.out.println("compile with laptop");		
	}
	
	public void debug() {
		System.out.println("debug with laptop");		
	}
}

@Component
public class Desktop 
{
	public void compile() {
		System.out.println("compile with desktop");		
	}
	
	public void debug() {
		System.out.println("debug with desktop");		
	}
}

@Component
public class Developer
{
	//field basde binding
	@Autowired
	@Qualifier("Laptop") //resolve Laptop class with its bean name
	private IComputer computer;

	//constructor based binding
	public Developer(IComputer computer){
		this.computer = computer;
	}
	
	//setter based binding
	public void setLaptop(IComputer computer) {
		this.computer = computer;
	}

	public void compile() {
		computer.compile();
	}

	public void debug() {
		computer.debug();
	}
}
```


