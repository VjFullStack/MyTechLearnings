# Proxy design patttern

---

The Proxy pattern is a structural design pattern that allows you to provide a surrogate or placeholder for another object. This proxy object acts as a proxy to the real object, which is hidden from the client. The proxy object can control access to the real object, perform additional functionality before or after accessing the real object, or even create the real object on demand.

Here's an example of how the Proxy pattern can be implemented in Java:

*  Create an interface that represents the functionality of the real object. For example, let's say we have an interface called Internet that represents the ability to browse the internet.

```
public interface Internet {
    public void browse(String website);
}
```

* Create a class that implements the interface and represents the real object. For example, let's say we have a class called RealInternet that represents the actual internet browsing functionality.
```
public class RealInternet implements Internet {
    @Override
    public void browse(String website) {
        System.out.println("Browsing " + website);
    }
}

```
* Create a class that implements the same interface as the real object, but acts as a proxy to the real object. For example, let's say we have a class called ProxyInternet that represents a proxy for the real internet.

```
public class ProxyInternet implements Internet {
    private Internet realInternet = new RealInternet();
    private List<String> bannedWebsites = new ArrayList<String>();

    public ProxyInternet() {
        bannedWebsites.add("facebook.com");
        bannedWebsites.add("twitter.com");
        bannedWebsites.add("instagram.com");
    }

    @Override
    public void browse(String website) {
        if (bannedWebsites.contains(website.toLowerCase())) {
            System.out.println("Access to " + website + " is blocked");
        } else {
            realInternet.browse(website);
        }
    }
}

```
In this example, the ProxyInternet class acts as a proxy for the RealInternet class. The ProxyInternet class maintains a list of banned websites and blocks access to those websites. If the requested website is not in the list of banned websites, the proxy forwards the request to the real internet object.


Here's an example of how the code can be used:
```
Internet internet = new ProxyInternet();
internet.browse("google.com"); // Outputs "Browsing google.com"
internet.browse("facebook.com"); // Outputs "Access to facebook.com is blocked"
```
In this example, the Internet object is created as a ProxyInternet object. When the browse method is called with google.com as the argument, the proxy forwards the request to the real internet object and the output is "Browsing google.com". When the browse method is called with facebook.com as the argument, the proxy blocks the request and the output is "Access to facebook.com is blocked".

---
## Q. why do we do.
```
Internet internet = new ProxyInternet();
```
## We can also do like
```
ProxyInternet internet = new ProxyInternet();
```
## is there added benefit?

## Ans :
Both Internet internet = new ProxyInternet(); and ProxyInternet internet = new ProxyInternet(); are valid ways of creating an instance of the ProxyInternet class.

However, the former approach of creating an instance of the ProxyInternet class and storing it in an Internet reference variable is more flexible and adheres to the Dependency Inversion principle of SOLID design principles.

By storing the ProxyInternet instance in an Internet reference variable, we can pass this instance to any client code that expects an Internet object. This allows us to swap out the actual implementation of the Internet object (in this case, the RealInternet and ProxyInternet classes) without affecting the client code.

For example, imagine if we had another class that expects an Internet object as a constructor argument:
```
public class WebBrowser {
private Internet internet;

    public WebBrowser(Internet internet) {
        this.internet = internet;
    }

    public void browseWebsite(String website) {
        internet.browse(website);
    }
}
```
We can create an instance of the WebBrowser class and pass it the ProxyInternet instance that we created earlier:
```
Internet internet = new ProxyInternet();
WebBrowser webBrowser = new WebBrowser(internet);
webBrowser.browseWebsite("google.com"); // Outputs "Browsing google.com"
webBrowser.browseWebsite("facebook.com"); // Outputs "Access to facebook.com is blocked"
```

By using the Internet interface as the type of the internet variable, we can create different implementations of the Internet interface (such as RealInternet or any other future implementations) and pass them to the WebBrowser class without changing the WebBrowser class itself.

In summary, using an interface as the type of a reference variable provides more flexibility and adheres to the Dependency Inversion principle, making our code more modular and easier to maintain.

---

## Q. Where does Spring use Proxy Design Pattern internally? 

## Ans: 

* AOP: Suppose you have a service that performs some business logic and you want to add logging functionality to it without modifying the service code. In this case, you can use Spring's AOP support to create an aspect that intercepts the method calls and adds the logging functionality. Here's an example:
```
@Aspect
@Component
public class LoggingAspect {
    @Before("execution(* com.example.MyService.doSomething(..))")
    public void logBefore(JoinPoint joinPoint) {
        System.out.println("Before " + joinPoint.getSignature().getName() + " method execution");
    }
}

```
In this example, we define an aspect called LoggingAspect that intercepts the doSomething method of the MyService class and logs a message before its execution. Spring creates a dynamic proxy around the MyService bean and delegates the method call to the proxy, which applies the aspect before invoking the actual method.

* Declarative transaction management: Suppose you have a service that performs some database operations and you want to manage transactions declaratively using Spring's @Transactional annotation. 
  Here's an example:
```
@Service
@Transactional
public class MyService {
    public void doSomething() {
        // database operations
    }
}

```
In this example, we mark the MyService class with the @Transactional annotation, which tells Spring to create a proxy around the bean and manage transactions for the annotated methods. When a client calls the doSomething method, Spring applies transaction management before and after the method execution.

* Remote method invocation: Suppose you have a service that provides some functionality remotely and you want to expose it using Spring's RMI support. Here's an example:
```
public interface MyService {
    void doSomething();
}

@Service
public class MyServiceImpl implements MyService {
    public void doSomething() {
        // implementation
    }
}

@Bean
public RmiServiceExporter rmiServiceExporter() {
    RmiServiceExporter exporter = new RmiServiceExporter();
    exporter.setServiceInterface(MyService.class);
    exporter.setService(new MyServiceImpl());
    exporter.setServiceName("MyService");
    exporter.setRegistryPort(1099);
    return exporter;
}

```
In this example, we define a remote service interface called MyService and a corresponding implementation called MyServiceImpl. We then configure a RmiServiceExporter bean that creates a dynamic proxy around the MyService implementation and exports it as a remote service using RMI. When a client calls the remote method, Spring applies the RMI invocation logic through the dynamic proxy.

---
## Explain Lazy Loading and explain how Proxy design pattern can be used in lazy loading. 

Lazy loading is a technique used in software engineering to defer the initialization of an object until it is actually needed. In other words, instead of loading all objects and their dependencies upfront, objects are only loaded when they are actually required.

Using a proxy is a common way to implement lazy loading. A proxy is a placeholder object that acts as an intermediary between the client and the real object. The proxy object is created initially, and when a method is called on the proxy, it initializes the real object and delegates the method call to it. This way, the real object is only loaded when it is actually needed, and not upfront.

Here's an example of how a proxy can be used for lazy loading in Java:

```
public interface MyService {
    void doSomething();
}

public class MyServiceImpl implements MyService {
    public MyServiceImpl() {
        // initialization code that takes a long time
    }

    public void doSomething() {
        // method implementation
    }
}

public class MyServiceProxy implements MyService {
    private MyService target;

    public MyServiceProxy() {
        // create the proxy object without initializing the real object
        target = null;
    }

    public void doSomething() {
        // initialize the real object and delegate the method call
        if (target == null) {
            target = new MyServiceImpl();
        }
        target.doSomething();
    }
}

```

In this example, we have an interface called MyService and a corresponding implementation called MyServiceImpl. The MyServiceImpl constructor contains some initialization code that takes a long time to execute. To avoid loading the real object upfront, we create a proxy object called MyServiceProxy that implements the MyService interface. The MyServiceProxy constructor creates the proxy object without initializing the real object.

When a method is called on the proxy, the doSomething method of the MyServiceProxy class initializes the real object and delegates the method call to it. The first time doSomething is called, the real object is loaded and subsequent calls use the initialized object.

Using a proxy for lazy loading can be particularly useful in situations where you have a large number of objects that are not always needed, or where the initialization process is expensive.

---


