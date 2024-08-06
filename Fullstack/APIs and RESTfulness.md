# APIs and RESTfulness

## API

An API, or **Application Programming Interface**, is a set of rules, protocols, and tools that allows different software applications to communicate with each other.

It acts as an intermediary between two systems, enabling them to exchange data and perform various tasks.

> In simpler terms, an API is like a menu in a restaurant. The menu provides a list of dishes and their descriptions, enabling you to choose what you want to eat. The kitchen (the system) then prepares your order based on your selection. Similarly, the API provides a list of functions and commands that developers can use to interact with a service or system, without needing to understand its internal workings.
> 

APIs are widely used in software development to create more efficient, modular, and scalable applications.

They allow developers to integrate services, like social media platforms or payment gateways, into their own applications, or to access data from other sources, like databases or web servers.

---

## RESTfulness

RESTfulness refers to the architectural style and principles of REST, which stands for **Representational State Transfer**.

REST is a set of guidelines for building scalable, maintainable, and reliable web services.

It is often used to design APIs (Application Programming Interfaces) for web-based applications.

### Key principles

1. ***Stateless***
Each request from a client to a server must contain all the information needed to process the request.
The server should not store any information about the client's state between requests.
2. ***Client-Server***
RESTful systems are based on the client-server architecture, where the client and server are separate entities that communicate over a network.
The separation of concerns allows for better scalability and maintainability.
3. ***Cacheable***
Responses from the server can be cached by the client.
This improves performance by reducing the load on the server and decreasing the latency for the client.
4. ***Layered System***
RESTful systems can be composed of multiple layers, with each layer providing specific functionality.
This allows for better separation of concerns and makes the system more modular and maintainable.
5. ***Uniform Interface***
RESTful APIs should have a consistent and uniform interface, making it easier for developers to understand and use the API.
This is typically achieved by using standard HTTP methods (GET, POST, PUT, DELETE, etc.) and adhering to a consistent naming convention for resources and endpoints.