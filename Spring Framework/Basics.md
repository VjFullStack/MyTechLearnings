# Q. what if we create some object using new keyword in spring. and some using Depedancy Injection?

If you create an object using the new keyword in a Spring application, it will not be managed by the
Spring container and will not be eligible for dependency injection. This means that the dependencies of
the object will not be automatically injected by the Spring container, and you will have to manually
create and manage the dependencies of the object.

On the other hand, if you use dependency injection to create an object in a Spring application,
the object will be managed by the Spring container and its dependencies will be automatically injected
by the container. This makes it easier to manage the dependencies of the object and allows the object
to be easily tested with different implementations of its dependencies.

In general, it is a good practice to use dependency injection in a Spring application to create objects,
rather than using the new keyword, as it makes it easier to manage dependencies and test the application.
However, there may be cases where using the new keyword is necessary or appropriate, such as when creating
utility classes that do not have dependencies or when creating objects that are not eligible for
dependency injection.

****************************************************************************************************************

# Q. what kind of objects are not eligible for dependancy injection

There are a few types of objects that are not eligible for dependency injection in the Spring framework:

- Objects that are not managed by the Spring container: Only objects that are created and managed by
the Spring container can be eligible for dependency injection. Objects created using the new
keyword or created by another framework are not managed by the Spring container and are not eligible
for dependency injection.

- Objects with complex construction: Some objects may have complex constructors or may require
special initialization logic that cannot be easily expressed in a Spring configuration file.
In these cases, it may not be practical to use dependency injection to create the object.

- Objects with circular dependencies: If two objects have a circular dependency, where one
object depends on the other and vice versa, it can be difficult to use dependency injection to
create them. This is because one object cannot be created until the other object is created, and
vice versa, which creates a chicken-and-egg problem.

Overall, it is generally a good practice to use dependency injection in a Spring application to
create objects, as it makes it easier to manage dependencies and test the application. However,
there may be cases where using the new keyword or other means of object creation is necessary or
appropriate.

****************************************************************************************************************

# Q. can you explain point no 3 from previous ans with code

Sure, here is an example of two classes that have a circular dependency:
```
class ClassA {
  private ClassB classB;

  public ClassA(ClassB classB) {
    this.classB = classB;
  }
}

class ClassB {
  private ClassA classA;

  public ClassB(ClassA classA) {
    this.classA = classA;
  }
}
```
In this example, ClassA depends on ClassB, and ClassB depends on ClassA. This creates a circular
dependency, as ClassA cannot be created until ClassB is created, and ClassB cannot be created until
ClassA is created.

To use dependency injection to create these classes in a Spring application, you would need to use a
special type of dependency injection called circular dependency injection, which involves using
a third party object to break the circular dependency. Here is an example of how this could be done:
```
@Configuration
class AppConfig {
  @Bean
  public ClassA classA() {
    return new ClassA(classB());
  }

  @Bean
  public ClassB classB() {
    return new ClassB(classA());
  }
}
```
In this example, the classA and classB beans are created using circular dependency injection,
where the classA bean depends on the classB bean, and the classB bean depends on the classA bean.
The Spring container will manage these beans and ensure that they are properly initialized.

Overall, circular dependency injection can be used to manage circular dependencies in a Spring
application, but it should be used with caution, as it can make the application more complex and
harder to understand. In some cases, it may be better to refactor the code to eliminate the circular
dependency.

****************************************************************************************************************

# Q. how appconfig class in above example will work?

The AppConfig class in the above example is a configuration class that is used to define beans for
a Spring application. The AppConfig class is annotated with the @Configuration annotation,
which indicates that it is a configuration class.

The classA and classB methods in the AppConfig class are annotated with the @Bean annotation,
which indicates that they are methods that create beans. When the Spring container starts up,
it reads the AppConfig class and creates the classA and classB beans based on the methods defined
in the class.

The classA bean depends on the classB bean, and the classB bean depends on the classA bean,
which creates a circular dependency. To manage this circular dependency, the classA and classB
methods use circular dependency injection, where the classA bean is created with an instance of the
classB bean, and the classB bean is created with an instance of the classA bean.

The Spring container will manage the classA and classB beans and ensure that they are properly
initialized. You can then use the classA and classB beans in your application by injecting them into
other classes using dependency injection.

Overall, the AppConfig class in the above example serves as a configuration class for
a Spring application, defining beans that are managed by the Spring container and using circular
dependency injection to manage a circular dependency between the classA and classB beans.

****************************************************************************************************************

# Q. Does Spring use Separate heap space to create spring context.

No, the Spring framework does not use a separate heap space to create the Spring context.
The Spring context is created within the same heap space as the rest of the application.

The Spring context is the container that manages the beans and their dependencies in a
Spring application. It is created when the application starts up and is responsible for
creating and managing the beans, as well as injecting the dependencies of the beans into their
respective objects.

The Spring context is created using the Spring application context, which is an interface that
provides access to the Spring container and its features. There are several implementations of the
Spring application context, such as the ClassPathXmlApplicationContext and the
AnnotationConfigApplicationContext, which can be used to create the Spring context in different ways.

Overall, the Spring context is created within the same heap space as the rest of the application,
and it is responsible for managing the beans and their dependencies in the application.

****************************************************************************************************************

# Q. If we create objects using new in Spring application. Will it affect performance.

Creating objects using the new keyword in a Spring application will not necessarily affect the
performance of the application. However, it can make the application more difficult to manage and
test, as the dependencies of the objects will not be automatically injected by the Spring container.

Using dependency injection to create objects in a Spring application can make the application easier
to manage and test, as the dependencies of the objects will be automatically injected by the
Spring container. This can make it easier to switch between different implementations of the
dependencies and to test the application with different configurations.

Overall, the performance of a Spring application will depend on a variety of factors, such as the
complexity of the application, the efficiency of the code, and the resources available on the machine.
Using dependency injection to create objects can make the application easier to manage and test,
but it may not necessarily have a significant impact on the performance of the application.

****************************************************************************************************************




