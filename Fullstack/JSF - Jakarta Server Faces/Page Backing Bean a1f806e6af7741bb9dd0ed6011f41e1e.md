# Page Backing Bean

A JSF (JavaServer Faces) Page Backing Bean is a Java class that acts as a bridge between the JSF UI components in the view and the model (business logic and data). It is responsible for handling user interactions, managing state, and updating the model based on the user's actions.

Here's a basic example of a JSF Page Backing Bean:

```java
import javax.faces.bean.ManagedBean;
import javax.faces.bean.RequestScoped;

@ManagedBean
@RequestScoped
public class MyBean {
    private String name;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    // Action method
    public String doAction() {
        // Perform some action based on the user's input
        return "success";
    }
}

```

In this example, `MyBean` is a managed bean that is request-scoped, meaning a new instance of this bean is created for each HTTP request.

The `name` property is bound to a UI component in the view, and the `doAction` method is invoked when a certain user action occurs (like clicking a button). The returned string "success" is used for navigation, typically to another view.