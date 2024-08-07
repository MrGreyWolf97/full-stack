> [!info] Topics
> - Spring
> - JPA
> - Hibernate

> See this [article](https://www.baeldung.com/bootstraping-a-web-application-with-spring-and-java-based-configuration) for a step-by-step introduction to setting up the Spring context using Java-based configuration and the basic Maven pom for the project.

---
## [**JPA in Spring Boot**](https://www.baeldung.com/the-persistence-layer-with-spring-and-jpa#boot)

The Spring Boot project is intended to make creating Spring applications much faster and easier.
This is done using ==starters== and ==auto-configuration== for various Spring functionalities, *JPA among them*.

### [1. Maven Dependencies](https://www.baeldung.com/the-persistence-layer-with-spring-and-jpa#1-maven-dependencies)

To enable JPA in a Spring Boot application, we need the _[spring-boot-starter](https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-starter)_ and _[spring-boot-starter-data-jpa](https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-starter-data-jpa)_ dependencies:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter</artifactId>
    <version>3.1.0</version>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
    <version>3.1.0</version>
</dependency>
```

The _spring-boot-starter_ contains the necessary auto-configuration for Spring JPA.
Also, the _spring-boot-starter-jpa_ project references all the necessary dependencies, such as _hibernate-core_.

### [2. Configuration](https://www.baeldung.com/the-persistence-layer-with-spring-and-jpa#2-configuration)

**Spring Boot configures ==_Hibernate_ as the default JPA provider==**, so it’s no longer necessary to define the _entityManagerFactory_ bean unless we want to customize it.

**Spring Boot can also auto-configure the _dataSource_ bean, depending on the database we’re using.**

In the case of an in-memory database of type _H2_, _HSQLDB_ and _Apache Derby_, Boot automatically configures the _DataSource_ if the corresponding database dependency is present on the classpath.

For example, if we want to use an in-memory _H2_ database in a Spring Boot JPA application, we only need to add the [_h2_](https://mvnrepository.com/artifact/com.h2database/h2) dependency to the _pom.xml_ file:

```xml
<dependency>
    <groupId>com.h2database</groupId>
    <artifactId>h2</artifactId>
    <version>2.1.214</version>
</dependency>
```

This way, we don’t need to define the _dataSource_ bean, but we can if we want to customize it.

If we want to use JPA with _MySQL_ database, we need the _mysql-connector-java_ dependency.
We’ll also need to define the _DataSource_ configuration.

We can do this in a _@Configuration_ class or by using standard Spring Boot properties.

The Java configuration looks the same as it does in a standard Spring project:

```java
@Bean
public DataSource dataSource() {
    DriverManagerDataSource dataSource = new DriverManagerDataSource();

    dataSource.setDriverClassName("com.mysql.cj.jdbc.Driver");
    dataSource.setUsername("mysqluser");
    dataSource.setPassword("mysqlpass");
    dataSource.setUrl(
      "jdbc:mysql://localhost:3306/myDb?createDatabaseIfNotExist=true"); 
    
    return dataSource;
}
```

**To configure the data source using a properties file, we have to set properties prefixed with _spring.datasource_**:

```plaintext
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.datasource.username=mysqluser
spring.datasource.password=mysqlpass
spring.datasource.url=
  jdbc:mysql://localhost:3306/myDb?createDatabaseIfNotExist=true
```

Spring Boot will automatically configure a data source based on these properties.

Also, in Spring Boot 1, the default connection pool was _Tomcat_, but it has been changed to _HikariCP_ with Spring Boot 2.

We have more examples of configuring JPA in Spring Boot in the [GitHub project](https://github.com/eugenp/tutorials/tree/master/persistence-modules/spring-jpa).

As we can see, the basic JPA configuration is fairly simple if we’re using Spring Boot.

However, **if we have a standard Spring project, we need a more explicit configuration using Java or XML.** That’s what we’ll focus on in the next sections.

### [**3. The JPA Spring Configuration With Java in a Non-Boot Project**](https://www.baeldung.com/the-persistence-layer-with-spring-and-jpa#javaconfig)
To use JPA in a Spring project, **we need to set up the _EntityManager_.**

This is the main part of the configuration, and we can do it via a Spring factory bean.
This can be either the simpler _LocalEntityManagerFactoryBean_ or, **the more flexible _LocalContainerEntityManagerFactoryBean_.**

Let’s see how we can use the latter option:

```java
@Configuration
@EnableTransactionManagement
public class PersistenceJPAConfig {

   @Bean
   public LocalContainerEntityManagerFactoryBean entityManagerFactory() {
      LocalContainerEntityManagerFactoryBean em 
        = new LocalContainerEntityManagerFactoryBean();
      em.setDataSource(dataSource());
      em.setPackagesToScan("com.baeldung.persistence.model");

      JpaVendorAdapter vendorAdapter = new HibernateJpaVendorAdapter();
      em.setJpaVendorAdapter(vendorAdapter);
      em.setJpaProperties(additionalProperties());

      return em;
   }
   
   // ...

}
```

**We also need to explicitly define the _DataSource_ bean** we’ve used above:

```java
@Bean
public DataSource dataSource(){
    DriverManagerDataSource dataSource = new DriverManagerDataSource();
    dataSource.setDriverClassName("com.mysql.cj.jdbc.Driver");
    dataSource.setUrl("jdbc:mysql://localhost:3306/spring_jpa");
    dataSource.setUsername( "tutorialuser" );
    dataSource.setPassword( "tutorialmy5ql" );
    return dataSource;
}
```

The final part of the configuration is the additional Hibernate properties and the _TransactionManager_ and _exceptionTranslation_ beans:

```java
@Bean
public PlatformTransactionManager transactionManager() {
    JpaTransactionManager transactionManager = new JpaTransactionManager();
    transactionManager.setEntityManagerFactory(entityManagerFactory().getObject());

    return transactionManager;
}

@Bean
public PersistenceExceptionTranslationPostProcessor exceptionTranslation(){
    return new PersistenceExceptionTranslationPostProcessor();
}

Properties additionalProperties() {
    Properties properties = new Properties();
    properties.setProperty("hibernate.hbm2ddl.auto", "create-drop");
    properties.setProperty("hibernate.dialect", "org.hibernate.dialect.MySQL5Dialect");
       
    return properties;
}
```

### [**4. JPA Spring Configuration With XML**](https://www.baeldung.com/the-persistence-layer-with-spring-and-jpa#xmlconfig)

Next, let’s see the same Spring configuration with XML:

```xml
<bean id="myEmf" 
  class="org.springframework.orm.jpa.LocalContainerEntityManagerFactoryBean">
    <property name="dataSource" ref="dataSource" />
    <property name="packagesToScan" value="com.baeldung.persistence.model" />
    <property name="jpaVendorAdapter">
        <bean class="org.springframework.orm.jpa.vendor.HibernateJpaVendorAdapter" />
    </property>
    <property name="jpaProperties">
        <props>
            <prop key="hibernate.hbm2ddl.auto">create-drop</prop>
            <prop key="hibernate.dialect">org.hibernate.dialect.MySQL5Dialect</prop>
        </props>
    </property>
</bean>

<bean id="dataSource" 
  class="org.springframework.jdbc.datasource.DriverManagerDataSource">
    <property name="driverClassName" value="com.mysql.cj.jdbc.Driver" />
    <property name="url" value="jdbc:mysql://localhost:3306/spring_jpa" />
    <property name="username" value="tutorialuser" />
    <property name="password" value="tutorialmy5ql" />
</bean>

<bean id="transactionManager" class="org.springframework.orm.jpa.JpaTransactionManager">
    <property name="entityManagerFactory" ref="myEmf" />
</bean>
<tx:annotation-driven />

<bean id="persistenceExceptionTranslationPostProcessor" class=
  "org.springframework.dao.annotation.PersistenceExceptionTranslationPostProcessor" />
```

There’s a relatively small difference between the XML and the new Java-based configuration.
Namely, in XML, a reference to another bean can point to either the bean or a bean factory for that bean.

But in Java, since the types are different, the compiler doesn’t allow it, and so the _EntityManagerFactory_ is first retrieved from its bean factory and then passed to the transaction manager:

```java
transactionManager.setEntityManagerFactory(entityManagerFactory().getObject());
```

### [**5. Going Full XML-less**](https://www.baeldung.com/the-persistence-layer-with-spring-and-jpa#noxml)

> [!example] <aside><img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> </aside> Usually, JPA defines a persistence unit through the _META-INF/persistence.xml_ file.
> ---
> **Starting with Spring 3.1, the _persistence.xml_ is no longer necessary.**
> 
> The _LocalContainerEntityManagerFactoryBean_ now supports a _packagesToScan_ property where the packages to scan for _@Entity_ classes can be specified.

This file was the last piece of XML we need to remove.
**We can now set up JPA fully with no XML.**

We would usually specify JPA properties in the _persistence.xml_ file.
Alternatively, we can add the properties directly to the entity manager factory bean:

```java
factoryBean.setJpaProperties(this.additionalProperties());
```

As a side note, if Hibernate is the persistence provider, this would be the way to specify Hibernate-specific properties as well.

### [**6. The Maven Configuration**](https://www.baeldung.com/the-persistence-layer-with-spring-and-jpa#maven)

In addition to the Spring Core and persistence dependencies — shown in detail in the [Spring with Maven tutorial](https://www.baeldung.com/spring-with-maven "Spring Maven dependencies") — we also need to define JPA and Hibernate in the project as well as a MySQL connector:

```xml
<dependency>
   <groupId>org.hibernate</groupId>
   <artifactId>hibernate-core</artifactId>
   <version>6.5.2.Final</version>
</dependency>

<dependency>
   <groupId>mysql</groupId>
   <artifactId>mysql-connector-java</artifactId>
   <version>8.0.19</version>
   <scope>runtime</scope>
</dependency>
```

Note that the MySQL dependency is included here as an example.

We need a driver to configure the data source, **but any Hibernate-supported database will do.**

---
***References:***
https://www.baeldung.com/the-persistence-layer-with-spring-and-jpa