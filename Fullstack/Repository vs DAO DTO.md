# Repository vs DAO/DTO

DAO (Data Access Object), DTO (Data Transfer Object), and Repository are design patterns used in software development, particularly in applications that deal with data storage, retrieval, and manipulation. Each pattern serves a specific purpose and helps maintain a clean architecture and separation of concerns.

---

### Repository

The Repository pattern is an abstraction used to manage the persistence and retrieval of domain objects in an application.

Repositories are similar to DAOs, but they operate at a higher level of abstraction, focusing on the domain model and business logic rather than the details of data access.

A repository defines methods for querying and storing domain objects, and it can encapsulate complex data access operations, such as joining or filtering data.

<aside>
<img src="https://www.notion.so/icons/snippet_green.svg" alt="https://www.notion.so/icons/snippet_green.svg" width="40px" /> Purpose

The main purpose of the Repository pattern is to provide a clean separation between the domain model and the data access logic, making it easier to maintain and test the application.

</aside>

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> Usage

Repositories are typically used in conjunction with service classes and domain objects, where the service classes contain the business logic and interact with the repositories to perform data access tasks.

In the context of the Spring framework, repositories are often implemented using the `@Repository` annotation and extend Spring Data interfaces, such as JpaRepository or MongoRepository.

</aside>

### DAO (Data Access Object)

The DAO pattern is an abstraction used to separate the data access logic from the rest of the application.

DAOs define methods for performing CRUD (Create, Read, Update, and Delete) operations and other data access tasks, while hiding the implementation details (such as database connections or ORM interactions) from the rest of the application.

<aside>
<img src="https://www.notion.so/icons/snippet_green.svg" alt="https://www.notion.so/icons/snippet_green.svg" width="40px" /> Purpose

The main purpose of the DAO pattern is to provide a consistent and flexible way to access and manipulate data, regardless of the underlying data storage mechanism (e.g., relational databases, NoSQL databases, or web services).

</aside>

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> Usage

DAOs are typically used in conjunction with service classes, which contain the business logic and interact with the DAOs to perform data access tasks.

</aside>

### DTO (Data Transfer Object)

The DTO pattern is used to transfer data between different layers or components of an application, particularly when the data needs to be serialized or deserialized, such as when sending data over a network or between different processes.

DTOs are simple objects that contain only data fields and no business logic.

They are often used to represent a subset of the data model, containing only the data needed for a specific operation or view.

<aside>
<img src="https://www.notion.so/icons/snippet_green.svg" alt="https://www.notion.so/icons/snippet_green.svg" width="40px" /> Purpose

The main purpose of the DTO pattern is to improve performance and maintainability by reducing the amount of data that needs to be transferred between components or layers and by keeping the data structure simple and focused.

</aside>

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> Usage

DTOs are typically used to transfer data between the presentation layer and the service layer, or between the service layer and the data access layer. They can also be used to represent API request and response objects.

</aside>

---

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> Summary

- Repository is an abstraction for managing the persistence and retrieval of domain objects, focusing on the domain model and business logic.Each pattern plays a specific role in the architecture of a software application, and using them effectively can help create a clean, maintainable, and efficient codebase.
- DAO is an abstraction for data access logic, hiding the implementation details of data storage and retrieval.
- DTO is a simple data structure used to transfer data between different layers or components of an application.
</aside>