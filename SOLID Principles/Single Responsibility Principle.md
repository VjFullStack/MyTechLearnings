# Q. Explain Single Responsibility Principle with exampLe in java?

The Single Responsibility Principle (SRP) is a software design principle that states that every class should have a single responsibility, or a single reason to change. In other words, a class should have only one job, and it should do that job well.

Here is an example of a Java class that violates the Single Responsibility Principle:
--------------------------------------------------------------------------------------

```public class Employee {
  private String name;
  private String address;
  private String email;
  private String phone;

  public Employee(String name, String address, String email, String phone) {
    this.name = name;
    this.address = address;
    this.email = email;
    this.phone = phone;
  }

  public String getName() {
    return name;
  }

  public void setName(String name) {
    this.name = name;
  }

  public String getAddress() {
    return address;
  }

  public void setAddress(String address) {
    this.address = address;
  }

  public String getEmail() {
    return email;
  }

  public void setEmail(String email) {
    this.email = email;
  }

  public String getPhone() {
    return phone;
  }

  public void setPhone(String phone) {
    this.phone = phone;
  }

  public void save() {
    // code to save employee to database
  }

  public void sendEmail() {
    // code to send email to employee
  }
}
```

This Employee class has two responsibilities: storing employee information and saving it to a database,
and sending emails to employees. A better design would be to split these responsibilities into two
separate classes, such as an Employee class and an EmailService class. This would make the code
easier to understand and maintain, because changes to the employee information would not affect the
email sending functionality, and vice versa.

Here is an example of how the Employee class could be refactored
to follow the Single Responsibility Principle:
-----------------------------------------------------------------------------------------------------
```
public class Employee {
  private String name;
  private String address;
  private String email;
  private String phone;

  public Employee(String name, String address, String email, String phone) {
    this.name = name;
    this.address = address;
    this.email = email;
    this.phone = phone;
  }

  public String getName() {
    return name;
  }

  public void setName(String name) {
    this.name = name;
  }

  public String getAddress() {
    return address;
  }

  public void setAddress(String address) {
    this.address = address;
  }

  public String getEmail() {
    return email;
  }

  public void setEmail(String email) {
    this.email = email;
  }

  public String getPhone() {
    return phone;
  }

  public void setPhone(String phone) {
    this.phone = phone;
  }
}

public class EmailService {
  public void sendEmail(String email, String message) {
    // code to send email
  }
}
```

Now the Employee class has only one responsibility, which is to store employee information,
and the EmailService class

*************************************************************************************************************


# Q. What problems can occur if we violate SRP, can you show me with example?

The Single Responsibility Principle (SRP) is a software design principle that states that a class or
module should have only one reason to change. In other words, a class or module should have only one
responsibility or job. Violating the SRP can lead to several problems, including:

- Increased complexity: If a class or module has multiple responsibilities, it becomes more complex and harder to understand and maintain. 
- Reduced reusability: If a class or module has multiple responsibilities, it may not be easily reusable in other contexts because it is tightly coupled to its specific responsibilities. 
- Decreased maintainability: If a class or module has multiple responsibilities, changes to one responsibility may require changes to other parts of the class or module, which can make it more difficult to maintain.

Here is an example of a class that violates the SRP:
```
class Employee
{
  private String name;
  private String address;
  private String phone;

  public void setName(String name) { this.name = name; }
  public String getName() { return name; }

  public void setAddress(String address) { this.address = address; }
  public String getAddress() { return address; }

  public void setPhone(String phone) { this.phone = phone; }
  public String getPhone() { return phone; }

  public double calculatePay() { /* code to calculate employee pay */ }
  public void save() { /* code to save employee to database */ }
}
```

In this example, the Employee class has three responsibilities: storing employee information, calculating
employee pay, and saving employee information to a database. This violates the SRP because the class has
multiple reasons to change. For example, if the way that employee pay is calculated changes, the
calculatePay method will need to be updated. If the way that employee information is saved to the
database changes, the save method will need to be updated. These changes could potentially affect other
parts of the Employee class, making it more difficult to maintain.

To fix this violation of the SRP, the Employee class could be refactored into two separate classes,
one for storing and retrieving employee information and another for calculating and saving employee pay.
This would make the code more modular and easier to maintain.

*************************************************************************************************************

# Q. Show me the example with Single responsibility principle in Java?

example of the Single Responsibility Principle (SRP) in Java:
```
public class Employee {
  private String name;
  private String address;
  private String phoneNumber;

  public String getName() {
    return name;
  }

  public void setName(String name) {
    this.name = name;
  }

  public String getAddress() {
    return address;
  }

  public void setAddress(String address) {
    this.address = address;
  }

  public String getPhoneNumber() {
    return phoneNumber;
  }

  public void setPhoneNumber(String phoneNumber) {
    this.phoneNumber = phoneNumber;
  }
}

public class EmployeeReportFormatter {
  private Employee employee;
  private FormatType formatType;

  public EmployeeReportFormatter(Employee employee, FormatType formatType) {
    this.employee = employee;
    this.formatType = formatType;
  }

  public String getFormattedEmployee() {
    switch (formatType) {
      case CSV:
        return employee.getName() + "," + employee.getAddress() + "," + employee.getPhoneNumber();
      case XML:
        return "<employee><name>" + employee.getName() + "</name><address>" + employee.getAddress() + "</address><phone>" + employee.getPhoneNumber() + "</phone></employee>";
      default:
        throw new IllegalArgumentException("Invalid format type");
    }
  }
}

public enum FormatType {
  CSV,
  XML
}
```

In this example, the Employee class has a single responsibility: to store and provide access to
information about an employee. The EmployeeReportFormatter class has a single responsibility: to format
employee information in a specific way (either as CSV or XML).

By following the Single Responsibility Principle, we have created two classes that are highly cohesive
and have a clear purpose. This makes the code easier to understand and maintain, as the responsibilities
of each class are well-defined and separate from each other.

*************************************************************************************************************



