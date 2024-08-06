# Standard Core Tags

Next to the standard HTML components, Jakarta Faces also provides a set of “core” tags.

Those are essentially “helper” tags that allow you to declaratively configure one or more target HTML components by either nesting in them or wrapping around them.

Those core tags are available under the XML namespace URI of jakarta.faces.core which should be assigned to the “f” XML namespace prefix.

```tsx
xmlns:f="jakarta.faces.core"
```

Technically, those tags are intended to be reusable on non-HTML components.

Jakarta Faces also offers the possibility of attaching a different render kit to the component tree that doesn’t generate HTML output but a different markup, hence the different XML namespace.

| Core tag | Creates/handles | Target component | Since |
| --- | --- | --- | --- |
| <f:actionListener> | jakarta.faces.event.ActionListener | ActionSource | 1.0 |
| <f:ajax> | jakarta.faces.component.behavior.AjaxBehavior | ClientBehaviorHolder(s) | 2.0 |
| <f:attribute> | UIComponent#getAttributes( ) | UIComponent | 1.0 |
| <f:attributes> | UIComponent#getAttributes( ) | UIComponent | 2.2 |
| <f:convertDateTime> | jakarta.faces.convert.DateTimeConverter | (Editable)ValueHolder | 1.0 |
| <f:convertNumber> | jakarta.faces.convert.NumberConverter | (Editable)ValueHolder | 1.0 |
| <f:converter> | jakarta.faces.convert.Converter | (Editable)ValueHolder | 1.0 |
| <f:event> | jakarta.faces.event.ComponentSystemEvent | UIComponent | 2.0 |
| <f:facet> | UIComponent#getFacets( ) | UIComponent | 1.0 |
| <f:importConstants> | jakarta.faces.component.UIImportConstants | UIViewRoot (metadata) | 2.3 |
| <f:loadBundle> | java.util.ResourceBundle | UIViewRoot | 1.0 |
| <f:metadata> | jakarta.faces.view.ViewMetadata | UIViewRoot | 2.0 |
| <f:param> | jakarta.faces.component.UIParameter | UIComponent | 1.0 |
| <f:passthroughAttribute> | UIComponent#getPassthroughAttributes( ) | UIComponent | 2.2 |
| <f:passthroughAttributes> | UIComponent#getPassthroughAttributes( ) | UIComponent | 2.2 |
| <f:phaseListener> | jakarta.faces.event.PhaseListener | UIViewRoot | 1.0 |
| <f:selectItem> | jakarta.faces.component.UISelectItem | UISelectOne/UISelectMany | 1.0 |
| <f:selectItems> | jakarta.faces.component.UISelectItems | UISelectOne/UISelectMany | 1.0 |
| <f:setPropertyActionListener> | jakarta.faces.event.ActionListener | ActionSource | 1.0 |
| <f:subview> | jakarta.faces.component.NamingContainer | UIComponents | 1.0 |
| <f:validateBean> | jakarta.faces.validator.BeanValidator | UIForm | 2.0 |
| <f:validateDoubleRange> | jakarta.faces.validator.DoubleRangeValidator | EditableValueHolder | 1.0 |
| <f:validateLength> | jakarta.faces.validator.LengthValidator | EditableValueHolder | 1.0 |
| <f:validateLongRange> | jakarta.faces.validator.LongRangeValidator | EditableValueHolder | 1.0 |
| <f:validateRegex> | jakarta.faces.validator.RegexValidator | EditableValueHolder | 2.0 |
| <f:validateRequired> | jakarta.faces.validator.RequiredValidator | EditableValueHolder | 2.0 |
| <f:validateWholeBean> | jakarta.faces.validator.BeanValidator | UIForm | 2.3 |
| <f:validator> | jakarta.faces.validator.Validator | EditableValueHolder | 1.0 |
| <f:valueChangeListener> | jakarta.faces.event.ValueChangeListener | EditableValueHolder | 1.0 |
| <f:view> | jakarta.faces.component.UIViewRoot | UIComponents | 1.0 |
| <f:viewAction> | jakarta.faces.component.UIViewAction | UIViewRoot (metadata) | 2.2 |
| <f:viewParam> | jakarta.faces.component.UIViewParameter | UIViewRoot (metadata) | 2.0 |
| <f:websocket> | jakarta.faces.component.UIWebsocket | UIViewRoot (body resource) | 2.3 |
- **Creates/handles**: specifies the thing which the core tag creates or handles on the specified target component.
- **Target component**: specifies the target component superclass or interface supported by the core tag. You must interpret the specified superclass or interface to be from the jakarta.faces.component package.
If the target component is optionally pluralized as in UIComponent(s), then it means that the core tag can either be nested in the target component or wrapped in one or more target components.
If the target component is explicitly pluralized as in UIComponents, then it means that the core tag can only wrap one or more target components and thus not be nested.