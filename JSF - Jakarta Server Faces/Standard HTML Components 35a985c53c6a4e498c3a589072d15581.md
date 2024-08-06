# Standard HTML Components

The default Jakarta Faces implementation already provides an extensive set of components for authoring HTML pages with the help of the Facelets view technology.

Those HTML components are available under the jakarta.faces.html XML namespace URI (Uniform Resource Identifier) that should be assigned to the “h” XML namespace prefix.

```tsx
xmlns:h="jakarta.faces.html"
```

The most important HTML components that should always be present in your Jakarta Faces page are the <h:head> and <h:body>. Without them, Jakarta Faces won’t be able to auto-include any script or stylesheet resources associated with a particular component.

<aside>
<img src="https://www.notion.so/icons/snippet_green.svg" alt="https://www.notion.so/icons/snippet_green.svg" width="40px" /> **Example**

The <h:commandButton>, which generates an HTML submit button, can optionally contain Ajax functionality via a <f:ajax> tag.

This Ajax functionality requires the faces.js script file to be included in the HTML document.

The renderer of that component will automatically take care of that, but that would only work properly if the <h:head> is present.

The <h:body> is not necessary for the Ajax functionality, but there may exist components that need to add a script to the end of the HTML body in order to perform initialization during page load, such as the <f:websocket> that needs to create a new window.

</aside>

| Component tag | Component superclass | Value type | HTML output | Since |
| --- | --- | --- | --- | --- |
| <h:body> | UIOutput | - | <body> | 2.0 |
| <h:button> | UIOutcomeTarget | String | <button onclick=window.location> | 2.0 |
| <h:column> | UIColumn | - | <td> (for h:dataTable) | 1.0 |
| <h:commandButton> | UICommand | String | <input type=submit> | 1.0 |
| <h:commandLink> | UICommand | String | <a onclick=form.submit()> | 1.0 |
| <h:commandScript> | UICommand | - | <script> (function to submit a form) | 2.3 |
| <h:dataTable> | UIData | Object[ ] | <table> (dynamic) | 1.0 |
| <h:doctype> | UIOutput | - | <!DOCTYPE> | 2.0 |
| <h:form> | UIForm | - | <form method=post> | 1.0 |
| <h:graphicImage> | UIGraphic | - | <img src> | 1.0 |
| <h:head> | UIOutput | - | <head> | 2.0 |
| <h:inputFile> | UIInput | Part | <input type=file> | 2.2 |
| <h:inputHidden> | UIInput | Object | <input type=hidden> | 1.0 |
| <h:inputSecret> | UIInput | Object | <input type=password> | 1.0 |
| <h:inputText> | UIInput | Object | <input type=text> | 1.0 |
| <h:inputTextarea> | UIInput | Object | <textarea> | 1.0 |
| <h:link> | UIOutcomeTarget | String | <a href> | 2.0 |
| <h:message> | UIMessage | - | <span> (if necessary) | 1.0 |
| <h:messages> | UIMessages | - | <ul> | 1.0 |
| <h:messages layout=table> | UIMessages | - | <table> | 1.0 |
| <h:outputFormat> | UIOutput | Object | <span> (if necessary) | 1.0 |
| <h:outputLabel> | UIOutput | String | <label> | 1.0 |
| <h:outputText> | UIOutput | Object | <span> (if necessary) | 1.0 |
| <h:outputScript> | UIOutput | - | <script> | 2.0 |
| <h:outputStylesheet> | UIOutput | - | <link rel=stylesheet> | 2.0 |
| <h:panelGrid> | UIPanel | - | <table> (static) | 1.0 |
| <h:panelGroup> | UIPanel | - | <span> | 1.0 |
| <h:panelGroup layout=block> | UIPanel | - | <div> | 1.2 |
| <h:selectBooleanCheckbox> | UIInput | Boolean | <input type=checkbox> | 1.0 |
| <h:selectManyCheckbox> | UIInput | Object[ ] | <table><input type=checkbox>* | 1.0 |
| <h:selectManyCheckbox layout=list> | UIInput | Object[] | <ul><li><input type=checkbox>* | 4.0 |
| <h:selectManyListbox> | UIInput | Object[ ] | <select multiple size=n><option>* | 1.0 |
| <h:selectManyMenu> | UIInput | Object[ ] | <select multiple size=1><option>* | 1.0 |
| <h:selectOneListbox> | UIInput | Object | <select size=n><option>* | 1.0 |
| <h:selectOneMenu> | UIInput | Object | <select size=1><option>* | 1.0 |
| <h:selectOneRadio> | UIInput | Object | <table><input type=radio>* | 1.0 |
| <h:selectOneRadio layout=list> | UIInput | Object | <ul><li><input type=radio>* | 4.0 |
| <h:selectOneRadio group> | UIInput | Object | <input type=radio name=group> | 2.3 |
- **Component superclass**: specifies the most important UIComponent superclass which the component extends from.
    
    You must interpret the specified class to be from the **jakarta.faces.component** package.
    
- **Value type**: specifies the supported type of the model value behind the component’s value attribute, if it has any.
    - If the value type is String, then it means that only the model value’s toString() outcome will be used as value of the component, generally in components which would render it as some sort of label.
    - If it’s Object, it means that it supports any kind of value, generally in components which would render it as text or parse it as input value, if necessary with help of an implicit or explicit Converter.
    - If the value type is Object[], it means that it requires an array or collection of objects as model value, generally in data and multiselection input components, if necessary with an implicit or explicit Converter.
- **HTML output**: specifies the minimum generated HTML output.
    - If the HTML output says “if necessary,” then it means that the specified HTML element is only emitted when the component has any attribute specified that requires being outputted as an HTML element attribute, such as id, styleClass, and onclick.
        
        That is, a component can have attributes that don’t end up in the generated HTML output at all, such as binding, rendered, and converter.
        
    - If a component can have multiple HTML element representations, then that’s usually controlled by the layout attribute as you can see with <h:messages> and <h:panelGroup>.
    - If the HTML output contains “*” (an asterisk), then it means that the component may emit zero or more of the specified nested HTML elements.