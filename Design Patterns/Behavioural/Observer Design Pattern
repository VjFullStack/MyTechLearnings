# Q. What is Observer design pattern? Explain in detail in Java

The Observer design pattern is a behavioral design pattern that allows an object (known as the subject)
to notify a set of objects (known as observers) when its state changes. The subject and the observers are
loosely coupled, meaning that the subject does not need to know the details about the observers, and the
observers do not need to know the details about the subject.

In Java, the Observer design pattern can be implemented using the java.util.Observable class and the
java.util.Observer interface.

Here is an example of how the Observer design pattern can be implemented in Java:
import java.util.Observable;
import java.util.Observer;

// The subject class extends the Observable class
```class Subject extends Observable {
  private int state;

  public int getState() {
    return state;
  }

  public void setState(int state) {
    this.state = state;
    // Mark the subject as having been changed
    setChanged();
    // Notify all observers of the change
    notifyObservers();
  }
}
```

// The observer class implements the Observer interface
```class Observer implements java.util.Observer {
  private Subject subject;

  public Observer(Subject subject) {
    this.subject = subject;
    // Add the observer as an observer of the subject
    subject.addObserver(this);
  }

  @Override
  public void update(Observable o, Object arg) {
    // The update method is called whenever the observed object is changed
    System.out.println("State changed to: " + subject.getState());
  }
}

public class Main {
  public static void main(String[] args) {
    Subject subject = new Subject();
    new Observer(subject);
    subject.setState(1);
    subject.setState(2);
  }
}
```

In this example, the Subject class represents the object being observed, and the Observer
class represents the object observing the subject. The Observer class registers itself as an observer
of the Subject using the addObserver method of the Observable class. When the Subject's state changes,
it calls the setChanged method of the Observable class to mark itself as having changed, and then calls
the notifyObservers method to notify all of its observers. The Observer's update method is then called,
and it can use the new state of the subject to perform any necessary updates.

The Observer design pattern is useful for implementing distributed event handling systems, where the state
of one object needs to be reflected in other objects without the objects being explicitly linked. It is
also useful for implementing Model-View-Controller (MVC) architectures, where the Model represents the
subject and the View represents the observer.

****************************************************************************************************************

# Q. How Spring uses Observer design pattern?

In the Spring framework, the Observer design pattern is used in various places to allow objects to be
notified of changes in the state of other objects.

One example of where the Observer design pattern is used in Spring is in the ApplicationContext.
The ApplicationContext is a container that holds and manages the lifecycle of beans. It is possible to
register objects as listeners for events that occur within the ApplicationContext, such as the creation
or destruction of beans. These objects are known as ApplicationListeners, and they can be registered
with the ApplicationContext using the addApplicationListener method.

Here is an example of how to register an ApplicationListener in a Spring application:

``` import org.springframework.context.ApplicationListener;
import org.springframework.context.event.ContextRefreshedEvent;

public class MyApplicationListener implements ApplicationListener<ContextRefreshedEvent> {

  @Override
  public void onApplicationEvent(ContextRefreshedEvent event) {
    // This method is called whenever the ApplicationContext is refreshed
    System.out.println("ApplicationContext refreshed!");
  }
}
```

To register the ApplicationListener, you can add it to the list of listeners in the ApplicationContext:

``` import org.springframework.context.annotation.AnnotationConfigApplicationContext;

public class Main {
  public static void main(String[] args) {
    AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext();
    context.addApplicationListener(new MyApplicationListener());
    context.refresh();
  }
}
```


In this example, the MyApplicationListener class is registered as an ApplicationListener with the
ApplicationContext. When the ApplicationContext is refreshed, the onApplicationEvent method of the
MyApplicationListener is called.

The Observer design pattern is also used in other parts of the Spring framework, such as in the Spring
MVC framework for handling HTTP requests and in the Spring Data framework for interacting with databases.

****************************************************************************************************************

Q. How Spring uses Observer design pattern to handle HTTP requests

In the Spring MVC framework, the Observer design pattern is used to handle HTTP requests. The
DispatcherServlet is the front controller of the Spring MVC framework, and it is responsible for routing
incoming HTTP requests to the appropriate handler.

The DispatcherServlet uses the HandlerMapping interface to map incoming requests to the appropriate
handler. The HandlerMapping interface has a single method, getHandler, which takes an HTTP request and
returns an object that can handle the request. The DispatcherServlet then uses the returned object to
handle the request.

There are several implementations of the HandlerMapping interface in the Spring framework, including the
following:

+ RequestMappingHandlerMapping: Maps incoming requests to methods annotated with the @RequestMapping
annotation
+ BeanNameUrlHandlerMapping: Maps incoming requests to beans in the ApplicationContext based on their
bean names
+ SimpleUrlHandlerMapping: Maps incoming requests to handler objects based on a predefined mapping of
URL patterns to handler objects

The DispatcherServlet also uses the HandlerAdapter interface to invoke the handler for the incoming
request. The HandlerAdapter interface has a single method, handle, which takes an HTTP request and an
object that can handle the request, and returns an object that represents the result of the request.
The DispatcherServlet then uses this object to generate the HTTP response.

There are several implementations of the HandlerAdapter interface in the Spring framework, including the following:
+ HttpRequestHandlerAdapter: Adapts objects that implement the HttpRequestHandler interface to the
HandlerAdapter interface
+ SimpleControllerHandlerAdapter: Adapts objects that implement the Controller interface to the
HandlerAdapter interface
+ AnnotationMethodHandlerAdapter: Adapts objects that have methods annotated with the @RequestMapping
annotation to the HandlerAdapter interface

In this way, the DispatcherServlet uses the Observer design pattern to handle incoming HTTP requests.
It registers a number of HandlerMappings and HandlerAdapters as observers, and then delegates the
handling of incoming requests to the appropriate handler based on the mapping and adapter that are chosen.
The handler is then invoked to handle the request, and the result is used to generate the HTTP response.

****************************************************************************************************************

