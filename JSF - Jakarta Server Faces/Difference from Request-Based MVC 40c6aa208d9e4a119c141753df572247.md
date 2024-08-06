# Difference from Request-Based MVC

JavaServer Faces (JSF) is a Java web application framework and is part of the Java EE standard. It is different from the standard request-based Model-View-Controller (MVC) in several ways:

### **Component-based**

JSF is a component-based MVC framework, which means it allows developers to build server-side reusable UI components and a page is constructed by assembling and configuring these components.

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> This is different from request-based MVC frameworks where each request is tied to a controller, and the controller is responsible for dispatching the request to the appropriate handler.

</aside>

### **Event-driven**

JSF has a built-in event handling mechanism.
Components in JSF can fire events and also listen for events to handle.
This is not typically found in standard request-based MVC frameworks.

### **Stateful**

JSF maintains the state of the UI components on the server side.
This is different from the stateless nature of the HTTP protocol used in standard request-based MVC frameworks.

### **Uses Facelets**

JSF uses Facelets as its default templating system.
Facelets supports reusability through templating, composite components, and custom tags.
In contrast, standard request-based MVC frameworks might use JSP or Thymeleaf for view layer.

[Facelets](Facelets%207c4b9c49848e4d9bbf95f6ce4d79f3d2.md)

### **Navigation model**

JSF provides a navigation model for defining the sequence of pages that the user will interact with. This is not typically found in standard request-based MVC frameworks.

### **Validation, Conversion, and Internationalization**

JSF provides built-in tag libraries for input validation, data conversion, and internationalization. This is different from standard request-based MVC frameworks where you might need to manually handle these aspects.

### **Integration with other Java EE technologies**

JSF is designed to integrate easily with other Java EE technologies like EJB, JPA, CDI, etc. This level of integration is not typically found in standard request-based MVC frameworks.

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> **Summary**

JSF is a more feature-rich framework that provides a higher level of abstraction for building web applications compared to standard request-based MVC frameworks.

It is different from a request-based MVC framework wherein the developer needs to write more boilerplate code in the “controller” class associated with the view in order to define which request parameters need to be applied and/or how they should be converted and validated before populating the entity.

The developer also often needs to manually populate the entity by manually invoking a bunch of getters and setters before passing the entity to the service layer while invoking the action.

This all is unnecessary in a component-based MVC framework like Jakarta Faces.

</aside>

It should be noted that the backing bean has a rather unique position in the MVC paradigm. It can act as a Model, a View, and a Controller, depending on the point of view. This is detailed in Chapter [8](https://learning.oreilly.com/library/view/the-definitive-guide/9781484273104/html/454457_2_En_8_Chapter.xhtml).