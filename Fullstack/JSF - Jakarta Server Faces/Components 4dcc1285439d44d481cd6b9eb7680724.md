# Components

Jakarta Faces is a component-based MVC (model-view-controller) framework.

In essence, Jakarta Faces parses the view definition into a “component tree.”

The root of this tree is represented by the “view root” instance associated with the current instance of the faces context.

```html
**UIComponent tree = FacesContext.getCurrentInstance().getViewRoot();**
```

The view is usually defined using XHTML+XML markup in a Facelets file.

<aside>
<img src="https://www.notion.so/icons/snippet_green.svg" alt="https://www.notion.so/icons/snippet_green.svg" width="40px" /> XML is a markup language that is very suitable for defining a tree hierarchy using a minimum of code.

</aside>

The component tree can also be created and manipulated using Java code in a Java class, but this generally ends up in very verbose code in order to declare value or method expressions and to correlate parents and children with one another.

It’s much better to use tag handlers such as Jakarta Tags (formerly known as Jakarta Tags, Jakarta Pages Standard Tag Library) to manipulate the component tree using just XML.

---

### Component tree

The component tree basically defines how Jakarta Faces should consume the HTTP request in order to:

1. apply request values coming from input components
2. convert and validate them
3. update the managed bean model values
4. invoke the managed bean action

It also defines how Jakarta Faces should produce the HTTP response by generating the necessary HTML output using renderers tied to the components whose attributes can in turn reference managed bean properties.

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> **In other words**

The component tree defines how the phases of the Jakarta Faces life cycle should be processed.

The diagram shows how an HTTP postback request is usually being processed by Jakarta Faces.

![https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9781484273104/files/images/454457_2_En_3_Chapter/454457_2_En_3_Fig1_HTML.png](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9781484273104/files/images/454457_2_En_3_Chapter/454457_2_En_3_Fig1_HTML.png)

The following is a brief description of each step:

1. End user sends an HTTP request using a URL that matches the mapping of the FacesServlet, and thus the FacesServlet gets invoked. 
2. The FacesServlet will build the component tree based on the Facelets file identified by the HTTP request path. 
3. The component tree will, if necessary, get the current model values from the backing bean during building the view. Any attribute of a Facelets template tag and a Jakarta Tags core tag and only the “id” and “binding” attributes of a Jakarta Faces component will get executed. 
4. The FacesServlet will restore the Jakarta Faces view state on the component tree. 
5. The FacesServlet will let the component tree apply the HTTP request parameters, and the input components will store them as “submitted value.” 
6. The input and command components will, if necessary, get the current model values from the backing bean during consulting their “rendered”, “disabled”, and “readonly” attributes in order to check whether they are allowed to apply the request parameters. 
7. The command components will queue the ActionEvent when it detects, based on HTTP request parameters, that the HTML representation of the command component was being invoked in the client side. 
8. The FacesServlet will let the component tree process all registered converters and validators on the submitted values, and the input components will store the newly converted and validated value as “local value.” 
9. The input components will get the old model value from the backing bean and compare them with the new value. 
10. If the new value is different from the old model value, then the input component will queue the ValueChangeEvent. 
11. When all conversion and validation are finished, then the FacesServlet will invoke the listener methods of any queued ValueChangeEvent on the backing bean. 
12. The FacesServlet will let the component tree update all model values. 
13. The input components will set the new model values in the backing bean. 
14. The FacesServlet will invoke the listener methods of any queued ActionEvent on the backing bean. 
15. The final action method of the backing bean will, if necessary, return a non-null String outcome referring the target view. 
16. The FacesServlet will let the component tree render the HTTP response. 
17. The component tree will, if necessary, get the current model values from the backing bean during generating the HTML output. Practically any attribute of a Facelets component and a Jakarta Faces component that is involved in generating the HTML output will get executed. 
18. The component tree will write the HTML output to the HTTP response. 
19. The FacesServlet will return the HTTP response to the end user.
</aside>