# Q. What is happening behind when Json request comes to Controller method in Springboot

When a JSON request is sent to a Spring Boot controller method, the following steps occur:

+ The request is received by the controller method and is mapped to the appropriate handler method based
on the request path and HTTP method (e.g., GET, POST, PUT, DELETE).

+ The request payload (i.e., the JSON data) is automatically deserialized by the framework into a Java
object, using a suitable ObjectMapper. This object is then passed as an argument to the controller method.

+ The controller method processes the request and performs any necessary business logic.

+ The controller method returns a response, which can be a Java object. The framework will automatically
serialize this object into JSON and send it back to the client as the response payload.

The client receives the response and can process the data as needed.

It's important to note that the steps described above are a simplified version of what happens when a JSON request is handled by a Spring Boot controller. There are many additional details and configurations that can be applied to customize the way the request is processed and the response is generated.
****************************************************************************************************************
Q. How do we configure ObjectMapper using applciation.yml file?

To configure the ObjectMapper using the application.yml file in a Spring Boot application, you can use the following syntax:
```
spring:
  jackson:
    serialization:
      indent-output: true
    property-naming-strategy: SNAKE_CASE

```
This configuration will instruct the ObjectMapper to use a property naming strategy of "SNAKE_CASE" and
to indent the output when serializing Java objects to JSON.

You can also specify other options for the ObjectMapper, such as the date format, timezone, and whether
to include null values in the serialized output. For example:
```
spring:
  jackson:
    serialization:
      write-dates-as-timestamps: false
      date-format: yyyy-MM-dd HH:mm:ss
      time-zone: UTC
      write-null-map-values: true
```
This configuration will instruct the ObjectMapper to write dates as strings using the specified date
format, to use the UTC timezone when serializing dates, and to include null values in the serialized
output.

It's important to note that these are just a few examples of the options that can be configured for the
ObjectMapper. There are many other options available, and you can find more information about them in
the Jackson documentation.

****************************************************************************************************************
# Q. Is it really required or optional?

Configuring the ObjectMapper in a Spring Boot application is optional. If you do not specify any
configuration for the ObjectMapper, the framework will use the default settings provided by the Jackson
library.

The default settings for the ObjectMapper are usually sufficient for most applications, and you may not
need to configure the ObjectMapper at all. However, if you need to customize the way the ObjectMapper
serializes and deserializes JSON data, you can do so by specifying the appropriate configuration in the
application.yml file or programmatically using the @EnableConfigurationProperties annotation.

For example, you might want to customize the way dates are formatted in the JSON output, or you might
want to use a different property naming strategy for the Java object fields. In these cases, you can use
the configuration options provided by the Jackson library to customize the ObjectMapper to suit your
needs.
****************************************************************************************************************
# Q. In my application, there is boolean field in my Java class. Client is sending 1 or 0. it is throwing
bad request because it is expecting either true or false. Can customize in serialiazer?

Yes, you can customize the way the ObjectMapper handles boolean values in the JSON payload when
deserializing data into a Java object.

One way to do this is to use a custom JsonDeserializer. A JsonDeserializer is a class that implements the
com.fasterxml.jackson.databind.JsonDeserializer interface and defines how to deserialize a specific
type of data.

To use a custom JsonDeserializer for boolean values, you can create a class like this:
```
public class BooleanSerializer extends JsonSerializer<Boolean> {

    @Override
    public void serialize(Boolean value, JsonGenerator gen, SerializerProvider serializers)
            throws IOException {
        gen.writeNumber(value ? 1 : 0);
    }
}
```
-----------------------------------------------------------------------------------------

```
public class BooleanDeserializer extends JsonDeserializer<Boolean> {

    @Override
    public Boolean deserialize(JsonParser parser, DeserializationContext context)
            throws IOException {
        int value = parser.getIntValue();
        return value == 1;
    }
}
```
These serializer and deserializer will serialize and deserialize boolean values using the integer values
1 and 0, respectively.

To use these serializer and deserializer globally, you can register them with the ObjectMapper by
creating a configuration class and annotating it with the @Configuration and
@EnableConfigurationProperties annotations. For example:

```
@Configuration
@EnableConfigurationProperties
public class CustomObjectMapperConfiguration {

    @Bean
    public ObjectMapper objectMapper() {
        ObjectMapper mapper = new ObjectMapper();
        SimpleModule module = new SimpleModule();
        module.addSerializer(Boolean.class, new BooleanSerializer());
        module.addDeserializer(Boolean.class, new BooleanDeserializer());
        mapper.registerModule(module);
        return mapper;
    }
}
```
This configuration will create a new ObjectMapper with the custom serializer and deserializer registered,
and it will be used by the framework to serialize and deserialize JSON data.

It's important to note that this is just one way to customize the way the ObjectMapper handles boolean
values globally.
****************************************************************************************************************
# Q. When some request comes to Controller, Does it go through all the three handler adapter above?

No, when a request comes to a controller in the Spring MVC framework, it does not go through all of the
handler adapters mentioned above. Instead, the DispatcherServlet uses the registered handler mappings to
determine which handler is responsible for handling the request, and then uses the appropriate handler
adapter to invoke the handler.

For example, consider the following controller:
```
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;

@Controller
public class MyController {

  @RequestMapping("/hello")
  @ResponseBody
  public String handleRequest() {
    return "Hello, World!";
  }
}
```
In this example, the MyController class is annotated with the @Controller annotation, which indicates
that it is a controller in the Spring MVC framework. The handleRequest method is annotated with the
@RequestMapping annotation, which maps it to the /hello URL.

When an HTTP request is made to the /hello URL, the DispatcherServlet will use the registered handler
mappings to determine which handler is responsible for handling the request. If the
RequestMappingHandlerMapping is registered as a handler mapping, it will use the @RequestMapping
annotations to map the request to the handleRequest method of the MyController class.

Next, the DispatcherServlet will use the registered handler adapters to determine how to invoke the
handler. If the AnnotationMethodHandlerAdapter is registered as a handler adapter, it will use the
@RequestMapping annotations to determine how to invoke the handleRequest method.

In this way, the DispatcherServlet uses the Observer design pattern to route incoming requests to the
appropriate handler and invoke the handler to handle the request. Only the handler mappings and handler
adapters that are registered with the DispatcherServlet will be used to handle the request.

****************************************************************************************************************

# Q. How Dispatcher servlet uses registered handler mapping to determine
which handler is responsible for handling the request?

In the Spring MVC framework, the DispatcherServlet uses the registered handler mappings to
determine which handler is responsible for handling an incoming request. The DispatcherServlet iterates
through the registered handler mappings and calls the getHandler method on each one, passing in the
incoming request. The first handler mapping that returns a non-null value is used to handle the request.

For example, consider the following handler mapping:
```
import org.springframework.web.servlet.HandlerMapping;
import org.springframework.web.servlet.ModelAndView;
import org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerMapping;

public class MyHandlerMapping implements HandlerMapping {

  private RequestMappingHandlerMapping delegate;

  public MyHandlerMapping(RequestMappingHandlerMapping delegate) {
    this.delegate = delegate;
  }

  @Override
  public ModelAndView getHandler(HttpServletRequest request) throws Exception {
    // Delegate to the RequestMappingHandlerMapping to get the handler
    Object handler = delegate.getHandler(request);
    if (handler != null) {
      return new ModelAndView(handler);
    }
    return null;
  }
}
```
In this example, the MyHandlerMapping class is an implementation of the HandlerMapping interface
that delegates to the RequestMappingHandlerMapping to get the handler for the incoming request.
When the DispatcherServlet calls the getHandler method on the MyHandlerMapping, it will pass the
request to the RequestMappingHandlerMapping, which will use the @RequestMapping annotations to map
the request to the appropriate handler. If the RequestMappingHandlerMapping returns a non-null value,
the MyHandlerMapping will return a ModelAndView object with the handler as its view.

To use the MyHandlerMapping in a Spring MVC application, you can register it as a bean in the
ApplicationContext:
```
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurationSupport;

@Configuration
public class MyConfiguration extends WebMvcConfigurationSupport {

  @Bean
  public MyHandlerMapping myHandlerMapping(RequestMappingHandlerMapping delegate) {
    return new MyHandlerMapping(delegate);
  }
}
```
This will register the MyHandlerMapping as a bean in the ApplicationContext, and the DispatcherServlet will use it to determine which
handler to use for incoming requests.

****************************************************************************************************************

# Q. So RequestMappingHandlerMapping gives us which adapter to use?

No, the RequestMappingHandlerMapping does not give us which handler adapter to use. Instead,
it gives us the handler object that is responsible for handling the request. The handler adapter is
then used to invoke the handler and handle the request.

The RequestMappingHandlerMapping is an implementation of the HandlerMapping interface that maps incoming
requests to handler objects based on the @RequestMapping annotations on the handler methods. It does not
have any knowledge of the handler adapters that are registered with the DispatcherServlet.

Here is an example of how the RequestMappingHandlerMapping works:
```
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;

@Controller
public class MyController {

  @RequestMapping("/hello")
  @ResponseBody
  public String handleRequest() {
    return "Hello, World!";
  }
}
```
In this example, the MyController class is annotated with the @Controller annotation, which indicates
that it is a controller in the Spring MVC framework. The handleRequest method is annotated with the
@RequestMapping annotation, which maps it to the /hello URL.

When an HTTP request is made to the /hello URL, the RequestMappingHandlerMapping will use the
@RequestMapping annotations to map the request to the handleRequest method of the MyController class.
It will then return the handleRequest method as the handler for the request.

The DispatcherServlet will then use the registered handler adapters to determine how to invoke the
handler and handle the request. If the AnnotationMethodHandlerAdapter is registered as a handler adapter,
it will use the @RequestMapping annotations to determine how to invoke the handleRequest method.

In this way, the RequestMappingHandlerMapping maps incoming requests to handler objects, and the
handler adapters are used to invoke the handlers and handle the requests.

****************************************************************************************************************

