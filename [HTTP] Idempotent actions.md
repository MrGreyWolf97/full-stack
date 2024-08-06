# [HTTP] Idempotent actions

### Idempotent actions

An idempotent action is ***an operation that can be performed multiple times without changing the result or causing unintended side effects*** beyond the initial application.
In other words, repeating an idempotent action has the same effect as performing it only once.

In the context of REST APIs, idempotence is an important principle for certain HTTP methods to ensure reliability and predictability when interacting with resources.
The following HTTP methods are idempotent:

1. ***GET***
Retrieving a resource should not modify it or cause any side effects. Repeating a GET request will yield the same result each time.
2. ***PUT***
Updating a resource with the same data multiple times should have the same effect as updating it once. The state of the resource after several identical PUT requests should be the same as after a single request.
3. ***DELETE***
Deleting a resource multiple times should have the same effect as deleting it once.
After the initial deletion, subsequent DELETE requests should either return a "Not Found" status or indicate that the resource is already deleted.
4. ***HEAD***
Similar to GET, the HEAD method retrieves information about a resource without actually returning its content.
Repeating a HEAD request should not cause any side effects.
5. ***OPTIONS***
This method retrieves information about the communication options available for a resource. Repeated OPTIONS requests should not affect the resource or cause side effects.

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> By adhering to the idempotent principle for these HTTP methods, REST APIs can provide consistent behavior and reduce the risk of unintended consequences when requests are retried, duplicated, or performed out of order due to network issues or other factors.

However, it's worth noting that ***not all HTTP methods are idempotent***, such as POST, which may create new resources or change the state of existing ones when repeated.

</aside>