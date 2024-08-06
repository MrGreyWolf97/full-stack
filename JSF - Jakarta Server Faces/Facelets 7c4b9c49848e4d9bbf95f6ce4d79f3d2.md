# Facelets

## Overview

Facelets is a view technology for the JavaServer Faces (JSF) web framework.

It was introduced in JSF 2.0 as a replacement for JavaServer Pages (JSP).

---

### Templating (Components)

Facelets supports a powerful templating mechanism.

It allows you to define a layout in one file and then reuse it across multiple pages. This promotes code reuse and helps maintain a consistent look and feel across the application.

### Composite Components

Facelets allows you to create composite components. These are custom UI components that are composed of existing components.

They can be reused across the application, which can significantly reduce code duplication.

### Expression Language (EL) Enhancements

Facelets supports the unified expression language (EL), which allows you to bind components in your pages to server-side objects.

Facelets enhances EL by allowing method parameters, making it more powerful and flexible than in JSP.

### Ease of Use

Facelets is often considered easier to use than JSP for JSF applications.

It provides better error reporting, doesn't require you to write any scriptlet code, and generally works more seamlessly with JSF than JSP does.

### Performance

Facelets includes several features designed to improve performance, such as partial state saving and view caching.

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> **Summary**

Facelets is a powerful and flexible view technology for JSF that offers several advantages over JSP, including templating, composite components, enhanced EL support, ease of use, and improved performance.

</aside>

---

## How to use

Here's a step-by-step guide on how to use Facelets in JSF:

1. Create a new Facelets page (`.xhtml` file) in your project.
This will serve as the view in your JSF application.
2. Define the UI components in the Facelets page using JSF tags.
These tags are usually prefixed with `h:` or `f:`.
You can also use custom tags from libraries like PrimeFaces.
3. Create a managed bean (or a CDI bean) that will serve as the [backing bean](Facelets%207c4b9c49848e4d9bbf95f6ce4d79f3d2.md) for your Facelets page. This bean will contain the data and the action methods for your page.
4. Bind the UI components in your Facelets page to the properties and methods in your backing bean using EL expressions (`#{...}`).

## Example

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
"<http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd>">
<html xmlns="<http://www.w3.org/1999/xhtml>"
      xmlns:h="<http://java.sun.com/jsf/html>">
<h:head>
    <title>Facelets Example</title>
</h:head>
<h:body>
    <h:form>
        <h:inputText value="#{myBean.name}" />
        <h:commandButton value="Submit" action="#{myBean.doAction}" />
    </h:form>
</h:body>
</html>

```

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

    public String doAction() {
        // Perform some action based on the user's input
        return "success";
    }
}

```

In this example, the `h:inputText` tag is bound to the `name` property in `MyBean`, and the `h:commandButton` tag is bound to the `doAction` method.

When the button is clicked, the `doAction` method is invoked, and the result of this method is used for navigation.

---

### *References*

[Page Backing Bean](Page%20Backing%20Bean%20a1f806e6af7741bb9dd0ed6011f41e1e.md)