Spring framework supply us with Spring Web components, which basically is a Spring sub framework for web app development. 
Spring Web stick with CSR concept where:
- **C** - *controller*, layer which is handle request from server, and return back response in application context
- **S** - *service*, layer which supply business logic in the scope of web application
- **R** - *repository*, layer which perform communication with a storage, and abstract storage details from application
## Controllers
When we need create controller in Spring framework, we need create a java class and mark it with  `@Controller` or `@RestController` attribute.  
Use `@Controller` when you need return data within frontend layout, something like React or something else. Commonly say return HTML page back to client side.
In case of API use `@RestController` attribute. Controller is marked with this attribute return bare `String` to client side.
Also we need create a special  method, which will handle a special endpoint in our web application.
In below example we have `HomeController` which has `home` method to handle HTTP request for `/` space in the web app scope and return `String` to client.

```java
package com.ggghosthat.firstleaf;  
  
import org.springframework.web.bind.annotation.RequestMapping;  
import org.springframework.web.bind.annotation.RestController;  
  
@RestController  //resolve controller class for Spring
public class HomeController {  
  
    @RequestMapping("/")  //resolve endpoint for Spring
    public String home() {  
        return "welcome to the first ggghosthat Spring Web app.";  
    }  
}
```
