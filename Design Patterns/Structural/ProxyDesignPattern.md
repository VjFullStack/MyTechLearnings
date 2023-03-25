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