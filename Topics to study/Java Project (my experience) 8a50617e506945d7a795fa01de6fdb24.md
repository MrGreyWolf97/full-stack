# Java Project (my experience)

A Java project is a project realized with the Java programming language, which is an Object-Oriented, class-based language that allows multi-threading.

Programming in Java gives the opportunity to apply many sophisticated solutions for a set of well-known problems (called Design Patterns, which are built upon OOP's most powerful mechanisms like Polymorphism, Inheritance, or Abstraction).
Other than that, a Java project has access to all Java APIs and allows to build microservices capable to connect to databases, elaborate requests received from clients, and perform high-level Data-Ingestion.

A Java project can also rely on many frameworks and libraries, Spring (for the Inversion of Control) and Hibernate (for the Object Relational Mapping) are good examples, but also Lombok, and it’s even possible to create custom annotations to create Aspects and delete some boilerplate code.

I had a small experience with Apache Flink which is largely used in Targa Telematics, but not enough to call me an expert; it's still an amazing example of how Java can be used for state-of-the-art stateful-stream-processing.

I’ve been coding with Java for the last year and a half in my current company, but I studied it and programmed other projects during my university years.

The monolith I’ve worked on for most of the time is a Servlet deployed in a Tomcat, but we happened to recently build a new project (with Kotlin) that made use of Spring Boot (so, we used its embedded server).
It was a client-server microservice used to track a particular set of vehicles equipped with sensors to monitor and measure roads parameters; we designed a UI with maps displaying the vehicle's movement during the months, and we created various workflows to help the users schedule their vehicle trips, and worked on the database with spatial data to query over geographical road representation (with PostGIS).

Every project we create is usually deployed inside a docker container through Jenkins.

I have no direct experience with Kubernetes, even if my company is planning to adopt it in the next years, among all its functionalities what we will gain from its use is Autoscaling (considering that we have a fixed number of instances per project and some of them are completely useless during half of the day and not enough for the rest of the day), Service discovery (we currently use Eureka) and Environment isolation.