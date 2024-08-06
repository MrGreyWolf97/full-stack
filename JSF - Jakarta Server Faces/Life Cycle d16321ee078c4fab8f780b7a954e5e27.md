# Life Cycle

Jakarta Faces has a very well-defined life cycle, it is broken down into six phases.

Each of those phases runs the HTTP request through the component tree, performs operations on it, and fires component system events.

---

# Phases

## 1. Restore View Phase

First, create the UIViewRoot instance and set its properties such as locale from any <f:view> tag.

The component tree is at that moment usually empty. Only when the current request is a postback request, or when the view has a <f:metadata> with children, then build the full component tree based on the view definition.

Basically, a specific UIComponent subclass will be instantiated based on the component tag defined in the view and populated with all attributes defined in the view, and then UIComponent#setParent() will be invoked, passing the actual parent component.
The UIComponent#setParent() method will first check if there isn’t already an existing parent, and if so, then it will fire the PreRemoveFromViewEvent on the old parent. Then, when the new parent has been set, and thus the current component has become part of the component tree, it will fire the PostAddToViewEvent with the current component.
If the current request is a postback request, then it will restore the “view state” identified by the jakarta.faces.ViewState request parameter into the freshly built component tree. After that, the PostRestoreStateEvent is explicitly fired for each component in the tree, even when the component tree has actually not been restored. In other words, even when it’s not a postback request, that event is fired. You’d better reinterpret that event as “PostRestoreViewPhase”. In case when you’re, during the PostRestoreStateEvent, actually interested in whether it’s a postback request or not, then you should consult the FacesContext#isPostback() as well.
By the end of the restore view phase, if the component tree is still empty, then the life cycle will immediately advance to the render response phase (sixth phase), hereby skipping any phase in between.

## 2. Apply Request Values Phase

The UIComponent#processDecodes() method will be invoked on the UIViewRoot. The processDecodes() method will first invoke the processDecodes() method on each child and facet and then invoke UIComponent#decode() on itself. Finally, the UIViewRoot#broadCastEvents() will be invoked to fire any FacesEvent queued for the current phase. The default Jakarta Faces API (application programming interface) doesn’t offer such events for the apply request values phase, but developers can create and queue their own.
The default implementation of the decode() method will delegate to the Renderer#decode() method . In the decode() method of either the component or the renderer, the implementation has the opportunity to extract the submitted value from the HTTP request parameter and set it as an internal property. From the standard HTML component set, the only components that do that are the HTML form–based components deriving from UIForm, UIInput, and UICommand. The UIForm component will invoke UIForm#setSubmitted() with true. The UIInput component will invoke UIInput#setSubmittedValue() with the HTTP request parameter value. The UICommand component will queue the ActionEvent for the invoke application phase (fifth phase).

## 3. Process Validations Phase

The UIComponent#processValidators() will be invoked on the UIViewRoot. The processValidators() method will basically first fire the PreValidateEvent for the current component, then invoke processValidators() on each child and facet, and then invoke the PostValidateEvent for the current component. Finally, the UIViewRoot#broadCastEvents() will be invoked to fire any FacesEvent queued for the current phase, which is usually an instance of ValueChangeEvent.
From the standard HTML component set, only UIInput components behave differently here. Right before calling processValidators() on each child and facet, they will first invoke UIInput#validate() on itself. If there’s a submitted value set during the apply request values phase (second phase), then they will first invoke Converter#getAsObject() on any attached Converter. When it doesn’t throw ConverterException, then they will invoke Validator#validate() on every single attached Validator instance, regardless of whether any of them has thrown a ValidatorException.
When no ConverterException or ValidatorException was thrown, then UIInput#setValue() will be invoked with the converted and validated value, and the UIInput#isLocalValueSet() flag will return true and UIInput#setSubmittedValue() will be invoked with null.
When any ConverterException or ValidatorException was thrown, then UIInput#setValid() will be invoked with false, and the message of the exception will be added to the faces context via FacesContext#addMessage(). Finally, when UIInput#isValid() returns false, then FacesContext#setValidationFailed() will be invoked with true.
By the end of the phase, when FacesContext#isValidationFailed() returns true, then the life cycle will immediately advance to the render response phase (sixth phase), hereby skipping any phase in between.

## 4. Update Model Values Phase

The UIComponent#processUpdates() method will be invoked on the UIViewRoot. The processUpdates() method will in turn invoke the processUpdates() method on each child and facet. Finally, the UIViewRoot#broadCastEvents() will be invoked to fire any FacesEvent queued for the current phase. The default Jakarta Faces API doesn’t offer such events for the update model values phase, but developers can create and queue their own.
Also during this phase, from the standard HTML component set, only UIInput components have additional functionality here. After calling processUpdates() on each child and facet, they will invoke UIInput#updateModel() on itself. When both the UIInput#isValid() and UIInput#isLocalValueSet() return true, then they will invoke the setter method behind the value attribute with getLocalValue() as argument and immediately invoke UIInput#setValue() with null and clear out the UIInput#isLocalValueSet() flag by letting it return false.
When a RuntimeException is thrown here, usually caused by a bug in the setter method itself, then it will invoke UIInput#setValid() with false and queue the UpdateModelException, and the life cycle will immediately advance to the render response phase (sixth phase), hereby skipping any phase in between.

## 5. Invoke Application Phase

The UIViewRoot#processApplication() method will be invoked. This method will in turn invoke the UIViewRoot#broadCastEvents() to fire any FacesEvent queued for the current phase, which is usually an instance of AjaxBehaviorEvent or ActionEvent. Note that the processApplication() method is only defined on the UIViewRoot class and does not traverse the component tree.

## 6. Render Response Phase

When the component tree is still empty, i.e., when the HTTP request is not a postback request, or when the view has no <f:metadata> with children, or when the developer has in the meanwhile explicitly invoked FacesContext#setViewRoot() with its own instance, then build the full component tree based on the view definition. When the component tree is present, first, fire the PreRenderViewEvent for the UIViewRoot, then invoke UIComponent#encodeAll() on the UIViewRoot, and finally fire the PostRenderViewEvent for the UIViewRoot.
The UIComponent#encodeAll() method of each component will basically first invoke its own encodeBegin() method . Then, if the getRendersChildren() method returns true, the component will invoke its own encodeChildren() method , else it will invoke encodeAll() on each child. Finally, the component will invoke its own encodeEnd() method . This all happens only if UIComponent#isRendered() returns true—that is, when the rendered attribute of the component tag doesn’t evaluate to false.
The default implementation of the encodeBegin() method will first fire the PreRenderComponentEvent for the current component and then delegate to Renderer#encodeBegin(). The default implementation of the encodeChildren() method will delegate to Renderer#encodeChildren(). The default implementation of the encodeEnd() method will delegate to Renderer#encodeEnd(). If the component has no renderer attached, that is, when UIComponent#getRendererType() returns null, then no HTML output will be rendered to the response.
In the encodeBegin() method , the component or the renderer implementation has the opportunity to write the opening HTML element and all of its attributes to the response. In the encodeChildren() method , the component or the renderer implementation has the opportunity to decorate or override the rendering of the children if necessary. In the encodeEnd() method, the component or the renderer implementation has the opportunity to write the closing HTML tag. Writing to the response happens with the response writer as available by FacesContext#getResponseWriter().
For any mentioned XxxEvent class that has been fired in any phase, if any listener method throws jakarta.faces.event.AbortProcessingException,[1](https://learning.oreilly.com/library/view/the-definitive-guide/9781484273104/html/454457_2_En_3_Chapter.xhtml#Fn1) then the currently running phase will be immediately aborted, and the life cycle will immediately advance to the render response phase (sixth phase), hereby skipping any phase in between.