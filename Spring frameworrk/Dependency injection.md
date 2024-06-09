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


