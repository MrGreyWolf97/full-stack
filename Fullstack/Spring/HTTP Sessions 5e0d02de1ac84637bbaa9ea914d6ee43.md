# HTTP Sessions

In a Spring web application, an HTTP session represents a series of interactions between a user's web browser and the web application within a certain time period.

It is a server-side mechanism that allows the application to store and manage session-specific information, such as user preferences, authentication data, and temporary data across multiple HTTP requests from the same client.

<aside>
<img src="https://www.notion.so/icons/snippet_green.svg" alt="https://www.notion.so/icons/snippet_green.svg" width="40px" /> HTTP is a stateless protocol, which means that each request is treated as an independent transaction without any knowledge of previous requests.

**To maintain state between requests, web applications use HTTP sessions to associate requests from the same client and keep track of user-specific data.**

</aside>

---

In a Spring web application, the HttpSession interface (from the javax.servlet.http package) is used to interact with the HTTP session.

The HttpSession object is created by the web container when a new session is initiated, either automatically when the first request is received from the client or explicitly by the application.

Here are some key aspects of an HTTP session in a Spring web application:

1. ***Session ID***
A unique identifier, typically a long alphanumeric string, is assigned to each session.
The session ID is sent to the client as a cookie or URL parameter, and the client includes it in subsequent requests to identify the associated session.
2. ***Session attributes***
The session can store key-value pairs called session attributes.
These attributes can be used to store user-specific data, such as user authentication, shopping cart items, or user preferences.
In Spring web applications, you can use the HttpSession.setAttribute() and HttpSession.getAttribute() methods to set and retrieve session attributes.
3. ***Session timeout***
An HTTP session has a timeout period, after which the session is invalidated and its data is discarded.
The timeout can be configured in the web application, and it helps prevent excessive resource usage by removing stale sessions.
If a client sends a request after the session has expired, a new session will be created.
4. ***Session management***
In Spring web applications, you can use the @SessionAttributes annotation in a controller to store model attributes in the session, or the SessionStatus.setComplete() method to clear session attributes when they are no longer needed.
Additionally, Spring Security provides advanced session management features, such as concurrent session control and session fixation protection.

---

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> Summary

An HTTP session in a Spring web application is a server-side mechanism for maintaining state between multiple HTTP requests from the same client.

It allows the application to store and manage session-specific data, such as user preferences and authentication information, *across different requests within a certain time period*.

</aside>