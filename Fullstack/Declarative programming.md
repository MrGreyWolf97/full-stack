# Declarative programming

Declarative programming is a style of programming where you express what you want to achieve without explicitly detailing how to do it.

This is in contrast to imperative programming, where you must provide a step-by-step process to achieve the desired outcome.

In declarative programming, the programmer specifies the desired result, but the language's implementation figures out the control flow to achieve that result.

<aside>
<img src="https://www.notion.so/icons/info-alternate_blue.svg" alt="https://www.notion.so/icons/info-alternate_blue.svg" width="40px" /> It is more concerned with the "what" rather than the "how."

</aside>

This can lead to more concise, readable code, and it can make it easier to reason about the program's behaviour.

---

Two common examples of declarative programming paradigms are:

1. **Functional Programming**: In functional programming, you write functions that receive inputs and produce outputs without side effects (i.e., no changes to the state outside the function). The focus is on the use of functions and the composition of these functions to form more complex operations.
Languages that support this paradigm include Haskell, Scala, and Erlang.
2. **Logic Programming**: In logic programming, you define a set of rules and facts.
A logic programming system uses these to draw conclusions or solve problems.
Prolog is one of the most well-known logic programming languages.

Other examples include:

- **SQL (Structured Query Language)**: Instead of telling the database how to gather the data, you specify what data you want, and the database engine determines the most efficient way to get it.
- **Markup languages**: HTML and XML are declarative languages used for web pages and data formatting, where you describe the structure and layout of the document, and the browser or parser handles the rendering or processing.
- **Configuration management systems**: Tools like Puppet, Ansible, and Terraform allow you to specify the desired state of a system or infrastructure, and the tool ensures that the system matches that state.

---

### Conclusion

Declarative programming can be more abstract and *can sometimes result in performance being less transparent,* as the control over the flow of the program is handled by the language's implementation.

However, the higher level of abstraction can make code easier to understand and maintain, and it can also reduce the likelihood of bugs since the implementation details are handled by the underlying system.