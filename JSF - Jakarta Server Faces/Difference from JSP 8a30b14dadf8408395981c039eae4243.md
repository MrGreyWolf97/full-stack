# Difference from JSP

## JSP

JSP (JavaServer Pages) is a technology used for building web pages that support dynamic content.

It uses Java programming language and is part of the Java EE platform.

<aside>
<img src="https://www.notion.so/icons/snippet_green.svg" alt="https://www.notion.so/icons/snippet_green.svg" width="40px" /> JSPs are compiled into Servlets by the web server, which means they have all the capabilities of Java Servlets.

</aside>

In a JSP page, you can embed Java code directly into your HTML using special JSP tags.

These tags typically start with `<%` and end with `%>`. For example, you can use `<%= ... %>` to output the value of a Java expression and `<% ... %>` to include a block of Java code.

Here's a simple example of a JSP page:

```html
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
    <title>JSP Example</title>
</head>
<body>
    <h1>Welcome to JSP!</h1>
    <%-- This is a JSP comment --%>
    <p>Current time: <%= new java.util.Date() %></p>
</body>
</html>

```

In this example, `<%= new java.util.Date() %>` is a JSP expression that outputs the current date and time. Note that unlike in a regular HTML comment, JSP comments are not included in the output sent to the client.

JSP also supports JSP tags libraries (JSTL), custom tags, and Expression Language (EL), which can help to reduce the need for scriptlets (Java code embedded in the HTML).

---

## Difference

JavaServer Faces (JSF) and JavaServer Pages (JSP) are both Java technologies used for building web applications, but they have some key differences:

1. **Architecture**: JSF is a component-based MVC framework, which means it provides a structured way to separate application responsibilities into model, view, and controller components.
JSP is a view technology that allows you to embed Java code in HTML, but it doesn't provide a full MVC architecture on its own.
2. **Component Reusability**: JSF provides a set of standard UI components (like text boxes, buttons, tables, etc.) that you can reuse across your application.
In JSP, you typically have to write the HTML for these components yourself, although you can use custom tag libraries to create reusable components.
3. **Event Handling**: JSF supports event-driven programming. You can attach listener methods to UI components that get triggered when a certain event (like a button click) occurs.
In JSP, you typically handle events on the server side using servlets.
4. **Data Binding**: JSF supports automatic data binding between UI components and server-side model objects using Expression Language (EL).
In JSP, you can use EL to display data, but it doesn't support automatic data binding.
5. **Validation**: JSF provides built-in support for validation, conversion, and error handling. You can easily validate user input using standard or custom validators, convert input data to other types, and display error messages.
In JSP, you typically have to write this logic yourself.
6. **State Management**: JSF provides automatic state management. It saves the state of UI components between requests, which is important for handling user interactions in a stateless protocol like HTTP.
JSP doesn't provide automatic state management, so you have to manage state yourself using sessions, cookies, or hidden form fields.

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> **Summary**

While JSP can be used as the view technology in a JSF application, JSF provides a more comprehensive solution for building web applications, with built-in support for MVC architecture, component reusability, event handling, data binding, validation, and state management.

</aside>