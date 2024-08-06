# Cache

Caching is a technique used to store the results of expensive operations or frequently accessed data in memory for faster retrieval.

In Java, there are several ways to implement caching, as well as libraries and design patterns that can help.

---

## Cache implementations

1. **Use data structures like HashMap or ConcurrentHashMap**

For simple caching scenarios, you can use built-in data structures like HashMap or ConcurrentHashMap (for thread-safe access) to store key-value pairs.

```java
Map<String, ExpensiveObject> cache = new ConcurrentHashMap<>();

public ExpensiveObject getFromCache(String key) {
    return cache.get(key);
}

public void addToCache(String key, ExpensiveObject value) {
    cache.put(key, value);
}

```

1. **Implement caching with a Least Recently Used (LRU) eviction policy**

If you need to limit the cache size and evict the least recently used items when the cache is full, you can use a LinkedHashMap to implement an LRU cache.

```java
class LRUCache<K, V> extends LinkedHashMap<K, V> {
    private final int cacheSize;

    public LRUCache(int cacheSize) {
        super(cacheSize + 1, 1.0f, true);
        this.cacheSize = cacheSize;
    }

    @Override
    protected boolean removeEldestEntry(Map.Entry<K, V> eldest) {
        return this.size() > cacheSize;
    }
}

```

1. **Use caching libraries**

There are several Java libraries available that provide advanced caching features, such as expiration policies, eviction strategies, and distributed caching. Some popular caching libraries are:

- **Google Guava**: Provides a simple and flexible in-memory cache implementation with various options for cache size, eviction policies, and concurrency levels.
- **Caffeine**: A high-performance caching library that provides an in-memory cache with a near-optimal eviction policy and support for asynchronous operations.
- **Ehcache**: A robust caching library that supports in-memory as well as disk-based caching, distributed caching, and integration with popular frameworks like Spring and Hibernate.
- **Redis**: An in-memory data structure store that can be used as a distributed cache with support for various data structures and atomic operations.

1. **Apply the Proxy design pattern**

The Proxy design pattern can be used to create a wrapper around the original object that implements caching. This pattern is useful when you want to add caching functionality without modifying the original class.

```java
public interface ExpensiveOperation {
    ExpensiveObject perform(String key);
}

public class ExpensiveOperationImpl implements ExpensiveOperation {
    // ...implementation
}

public class CachedExpensiveOperation implements ExpensiveOperation {
    private final ExpensiveOperation expensiveOperation;
    private final Map<String, ExpensiveObject> cache;

    public CachedExpensiveOperation(ExpensiveOperation expensiveOperation) {
        this.expensiveOperation = expensiveOperation;
        this.cache = new ConcurrentHashMap<>();
    }

    @Override
    public ExpensiveObject perform(String key) {
        ExpensiveObject result = cache.get(key);
        if (result == null) {
            result = expensiveOperation.perform(key);
            cache.put(key, result);
        }
        return result;
    }
}

```

---

## Best practices

- Choose the right caching strategy based on your application's requirements, such as cache size, eviction policies, and expiration times.
- Ensure that your cache implementation is thread-safe if it will be accessed by multiple threads.
- Be mindful of cache invalidation issues, such as stale data or cache coherency, especially in distributed environments.
- Monitor and optimize cache performance, such as hit rates and memory usage, to ensure that your caching strategy is effective.