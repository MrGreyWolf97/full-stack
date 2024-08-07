
## [Transaction Propagation](https://www.baeldung.com/spring-transactional-propagation-isolation#transaction-propagations)

Propagation defines our business logic’s transaction boundary. Spring manages to start and pause a transaction according to our _propagation_ setting.

Spring calls _TransactionManager::getTransaction_ to get or create a transaction according to the propagation. It supports some of the propagations for all types of _TransactionManager_, but there are a few of them that are only supported by specific implementations of _TransactionManager_.

Let’s go through the different propagations and how they work.

### 3.1. **_REQUIRED_ Propagation**[](https://www.baeldung.com/spring-transactional-propagation-isolation#1-required-propagation)

_REQUIRED_ is the default propagation. Spring checks if there is an active transaction, and if nothing exists, it creates a new one. Otherwise, the business logic appends to the currently active transaction:

```java
@Transactional(propagation = Propagation.REQUIRED)
public void requiredExample(String user) { 
    // ... 
}
```

Furthermore, since _REQUIRED_ is the default propagation, we can simplify the code by dropping it:

```java
@Transactional
public void requiredExample(String user) { 
    // ... 
}
```

Let’s see the pseudo-code of how transaction creation works for _REQUIRED_ propagation:

```java
if (isExistingTransaction()) {
    if (isValidateExistingTransaction()) {
        validateExisitingAndThrowExceptionIfNotValid();
    }
    return existing;
}
return createNewTransaction();
```

### 3.2. **_SUPPORTS_ Propagation**[](https://www.baeldung.com/spring-transactional-propagation-isolation#2supports-propagation)

For _SUPPORTS_, Spring first checks if an active transaction exists. If a transaction exists, then the existing transaction will be used. If there isn’t a transaction, it is executed non-transactional:

```java
@Transactional(propagation = Propagation.SUPPORTS)
public void supportsExample(String user) { 
    // ... 
}
```

Let’s see the transaction creation’s pseudo-code for _SUPPORTS_:

```java
if (isExistingTransaction()) {
    if (isValidateExistingTransaction()) {
        validateExisitingAndThrowExceptionIfNotValid();
    }
    return existing;
}
return emptyTransaction;
```

### 3.3. **_MANDATORY_ Propagation**[](https://www.baeldung.com/spring-transactional-propagation-isolation#3mandatory-propagation)

When the propagation is _MANDATORY_, if there is an active transaction, then it will be used. If there isn’t an active transaction, then Spring throws an exception:

```java
@Transactional(propagation = Propagation.MANDATORY)
public void mandatoryExample(String user) { 
    // ... 
}
```

Let’s again see the pseudo-code:

```java
if (isExistingTransaction()) {
    if (isValidateExistingTransaction()) {
        validateExisitingAndThrowExceptionIfNotValid();
    }
    return existing;
}
throw IllegalTransactionStateException;
```

### 3.4. **_NEVER_ Propagation**[](https://www.baeldung.com/spring-transactional-propagation-isolation#4never-propagation)

For transactional logic with _NEVER_ propagation, Spring throws an exception if there’s an active transaction:

```java
@Transactional(propagation = Propagation.NEVER)
public void neverExample(String user) { 
    // ... 
}
```

Let’s see the pseudo-code of how transaction creation works for _NEVER_ propagation:

```java
if (isExistingTransaction()) {
    throw IllegalTransactionStateException;
}
return emptyTransaction;
```

### 3.5. **_NOT_SUPPORTED_ Propagation**[](https://www.baeldung.com/spring-transactional-propagation-isolation#5notsupported-propagation)

If a current transaction exists, first Spring suspends it, and then the business logic is executed without a transaction:

```java
@Transactional(propagation = Propagation.NOT_SUPPORTED)
public void notSupportedExample(String user) { 
    // ... 
}
```

**The _JTATransactionManager_ supports real transaction suspension out-of-the-box. Others simulate the suspension by holding a reference to the existing one and then clearing it from the thread context**

### 3.6. **_REQUIRES_NEW_ Propagation**[](https://www.baeldung.com/spring-transactional-propagation-isolation#6requiresnew-propagation)

When the propagation is _REQUIRES_NEW_, Spring suspends the current transaction if it exists, and then creates a new one:

```java
@Transactional(propagation = Propagation.REQUIRES_NEW)
public void requiresNewExample(String user) { 
    // ... 
}
```

**Similar to _NOT_SUPPORTED_, we need the _JTATransactionManager_ for actual transaction suspension.**

The pseudo-code looks like so:

```java
if (isExistingTransaction()) {
    suspend(existing);
    try {
        return createNewTransaction();
    } catch (exception) {
        resumeAfterBeginException();
        throw exception;
    }
}
return createNewTransaction();
```

### 3.7. **_NESTED_ Propagation**[](https://www.baeldung.com/spring-transactional-propagation-isolation#7nested-propagation)

For _NESTED_ propagation, Spring checks if a transaction exists, and if so, it marks a save point. This means that if our business logic execution throws an exception, then the transaction rollbacks to this save point. If there’s no active transaction, it works like _REQUIRED_.

**_DataSourceTransactionManager_ supports this propagation out-of-the-box. Some implementations of _JTATransactionManager_ may also support this.**

**[_JpaTransactionManager_](https://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/orm/jpa/JpaTransactionManager.html) supports _NESTED_ only for JDBC connections. However, if we set the _nestedTransactionAllowed_ flag to _true_, it also works for JDBC access code in JPA transactions if our JDBC driver supports save points.  
**

Finally, let’s set the _propagation_ to _NESTED_:

```java
@Transactional(propagation = Propagation.NESTED)
public void nestedExample(String user) { 
    // ... 
}
```

---
***References***
- [Baeldung article](https://www.baeldung.com/spring-transactional-propagation-isolation)
