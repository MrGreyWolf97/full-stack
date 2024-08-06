# Internals

You can be a good racer just by driving a car but you will never become the best one without knowing its internals.

Spring
 Framework is the most popular solution in Java world development. It 
provides dozens of functionalities, has a huge community, and is a 
feature-rich — production-ready tool.

![https://miro.medium.com/v2/resize:fit:1135/0*rP7BjGQ3t3jKbkZC.png](https://miro.medium.com/v2/resize:fit:1135/0*rP7BjGQ3t3jKbkZC.png)

With
 this article, I’m starting a series about Spring internals to tell you 
how the framework works under the hood. So, the first talk is going to 
be about the most important features of the framework — DI container and
 *ApplicationContext*. We will take a fast and simple overview of the core functionality and lifecycle.

First
 of all, let’s talk a bit about a lifecycle of a standard Spring 
application. If we create a simple application using Spring Framework, 
we should create an application context first. To do so, we have a few 
implementations standard implementations:

- **ClassPathXmlApplicationContext** — it used to be the most common way of context creation a few years
before. This implementation consumes a path to the XML file that
describes the beans to be created for the context.
- **AnnotationConfigApplicationContext** — this one reads the configuration from Java annotations for the same purposes instead of reading an XML file.

There are a few more default application context implementations out of the box. For example, **GroovyWebApplicationContext** allows reading a Groovy script describing beans. But all of them have something in common. It’s — the lifecycle:

![https://miro.medium.com/v2/resize:fit:1135/1*QG75pvnBGNPhZMGcNdK1pA.jpeg](https://miro.medium.com/v2/resize:fit:1135/1*QG75pvnBGNPhZMGcNdK1pA.jpeg)

Resource: [https://www.youtube.com/watch?v=BmBr5diz8WA](https://www.youtube.com/watch?v=BmBr5diz8WA)

Every
 application context implements one of the most important interfaces — 
BeanFactory. This interface is the main way for the users to access 
beans in the DI container. So, to enrich the container with beans, an 
application context implementation must do the following steps:

- read the configuration: as we’ve seen before, it may be an XML file, Java
config, or Groovy script or even we may write our own implementation
- compile a collection of bean definitions: *BeanDefinition* — it’s a description of the future beans. It contains information and
metadata that helps the DI container to create beans. We will talk about it more in the following articles
- call points of user integration before bean creation (*BeanFactoryPostProcessor*) to allow user code to change any metadata of the bean definitions
- call points of user integration after bean creation but before init callbacks (*BeanPostProcessor.postProcessBeforeInitialization*) to allow user code to change beans. For example, we may wrap a bean with proxy
- call points of user integration after bean initializations (init methods, after properties set) (*BeanPostProcessor.postProcessAfterInitialization*). This point of integration allows a user to manipulate a bean after all initializations
- and store the beans in the *BeanFactory* implementation to allow access to them via the interface API

![https://miro.medium.com/v2/resize:fit:1135/1*CfSq14HpIHU8a66AU2gXFg.png](https://miro.medium.com/v2/resize:fit:1135/1*CfSq14HpIHU8a66AU2gXFg.png)

As
 you can see, an application context implementation should find 
configuration, build bean definitions, create beans, and store the beans
 inside. Also, it should provide a common API for integration and 
accessing the beans in the DI container.

Moreover,
 there is an additional class of application context — Web Application 
Context. This is a special case when the DI container should maintain an
 embedded or external servlet container.

Moreover, we have a bunch of lifecycle events that can be handled:

- ***ContextRefreshedEvent*** — published when all beans are loaded, post-processor beans are detected
and activated, singletons are pre-instantiated, and the
ApplicationContext object is ready for use
- ***ContextStartedEvent*** — published when all lifecycle beans receive an explicit start signal that is usually the *start()* method
- ***ContextStoppedEvent*** — published when the *stop()* method is called on the *ConfigurableApplicationContext* interface
- ***ContextClosedEvent*** — published when the *close()* method is called on the *ConfigurableApplicationContext* interface or via a JVM shutdown hook
- ***RequestHandledEvent*** — this event is published after the request is complete, only applicable to web applications that use Spring’s DispatcherServlet
- ***ServletRequestHandledEvent*** — a subclass of RequestHandledEvent that adds Servlet-specific context information

All
 these events can be handled by user code. It adds additional 
integration points into the Application Context of the application. We 
will talk about it in the upcoming articles in more detail.

To
 summarize, Application Context is a way of detecting configuration, 
bean metadata, bean instancing, and lifecycle management with 
integration points.

![https://miro.medium.com/v2/resize:fit:808/0*UlCZjRa1-BEcb8ms.png](https://miro.medium.com/v2/resize:fit:808/0*UlCZjRa1-BEcb8ms.png)

In the next article, we will write our own application context using a JSON configuration file.

---

**References**

- [YouTube video](https://www.youtube.com/watch?v=BmBr5diz8WA)
- [Spring doc](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html)
- [Medium article](https://medium.com/@alexeynovikov_89393/spring-internals-1-applicationcontext-simple-overview-416cbcfc07a3)