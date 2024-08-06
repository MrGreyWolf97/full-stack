# HTTP

|  | GET | POST | PUT | DELTE |
| --- | --- | --- | --- | --- |
| PURPOSE | Used to retrieve data from a server | Used to create a new resource on the server or submit data for processing | Used to update an existing resource or create a new one if it does not exist | Used to remove a resource from the server |
| IDEMPOTENT | ✅ | ❌ | ✅ | ✅ |
| SAFE | ✅ | ❌ | ❌ | ❌ |
| PAYLOAD | ❌ | ✅ | ✅ | ❌ |
| CACHEABLE | ✅ | ❌ | ❌ | ❌ |

## GET

| PURPOSE | The GET method is used to retrieve data from a server. It requests information about a specific resource or a collection of resources. |
| --- | --- |
| IDEMPOTENT | Yes, GET is idempotent. Repeating a GET request multiple times should yield the same result without causing any side effects. |
| SAFE | Yes, GET is considered safe, as it should not modify the resource or cause any side effects on the server. |
| PAYLOAD | GET requests typically do not have a message body or payload. Instead, they pass parameters through the request's URL (query string). |
| CACHEABLE | GET responses can be cached, which helps improve performance and reduce server load. |

## POST

| PURPOSE | The POST method is used to create a new resource on the server or submit data for processing. It can also be used for other non-idempotent actions. |
| --- | --- |
| IDEMPOTENT | No, POST is not idempotent. Repeating a POST request may create multiple resources or cause unintended side effects. |
| SAFE | No, POST is not considered safe, as it can create new resources or modify existing ones on the server. |
| PAYLOAD | POST requests include a message body or payload, which contains the data to create a new resource or perform a specific action. |
| CACHEABLE | POST responses are typically not cached. |

## PUT

| PURPOSE | The PUT method is used to update an existing resource or create a new one if it does not exist. It replaces the entire resource with the supplied data. |
| --- | --- |
| IDEMPOTENT | Yes, PUT is idempotent. Repeating a PUT request with the same data will have the same effect as performing it once. |
| SAFE | No, PUT is not considered safe, as it can modify or create resources on the server. |
| PAYLOAD | PUT requests include a message body or payload, which contains the data to update or create the resource. |
| CACHEABLE | PUT responses are typically not cached. |

## DELETE

| PURPOSE | The DELETE method is used to remove a resource from the server. |
| --- | --- |
| IDEMPOTENT | Yes, DELETE is idempotent.
Repeating a DELETE request should have the same effect as performing it once.
After the initial deletion, subsequent DELETE requests should either return a "Not Found" status or indicate that the resource is already deleted. |
| SAFE | No, DELETE is not considered safe, as it modifies the server by removing resources. |
| PAYLOAD | DELETE requests typically do not have a message body or payload. |
| CACHEABLE | DELETE responses are typically not cached. |

---

|  | HEAD | OPTIONS | CONNECT | PATCH |
| --- | --- | --- | --- | --- |
| PURPOSE | retrieves information about a resource without actually returning its content | retrieves information about the communication options available for a resource | used to establish a network connection to a resource | used to partially update a resource on the server |
| IDEMPOTENT | ✅ | ✅ | ❌ | 🔶 |
| SAFE | ✅ | ✅ | ❌ | ❌ |
| PAYLOAD | ❌ | ✅ | ✅ | ✅ |
| CACHEABLE | ✅ | ❌ | ❌ | ❌ |

## HEAD

| PURPOSE | The HEAD method is similar to GET, but it retrieves information about a resource without actually returning its content. It is used to check if a resource exists or to retrieve metadata, such as content type or content length, without downloading the entire resource. |
| --- | --- |
| IDEMPOTENT | Yes, HEAD is idempotent, as it should not cause any side effects. |
| SAFE | Yes, HEAD is considered safe, as it should not modify the resource. |
| PAYLOAD | HEAD requests typically do not have a message body or payload. |
| CACHEABLE | Cacheable: HEAD responses can be cached. |

## OPTIONS

| PURPOSE | The OPTIONS method retrieves information about the communication options available for a resource or the server itself. It returns the HTTP methods supported by the resource or server, as well as any communication-related preferences or requirements. |
| --- | --- |
| IDEMPOTENT | Yes, OPTIONS is idempotent, as it should not cause any side effects. |
| SAFE | Yes, OPTIONS is considered safe, as it should not modify the resource. |
| PAYLOAD | OPTIONS requests may have a message body or payload, depending on the implementation. |
| CACHEABLE | OPTIONS responses are typically not cached. |

## CONNECT

| PURPOSE | The CONNECT method is used to establish a network connection to a resource, typically for use with a proxy server.
It is primarily used for SSL/TLS connections (HTTPS) when a client communicates with a proxy server. |
| --- | --- |
| IDEMPOTENT | CONNECT is not considered idempotent, as establishing a connection can have various side effects. |
| SAFE | No, CONNECT is not considered safe, as it can modify the state of the proxy server. |
| PAYLOAD | CONNECT requests may have a message body or payload, depending on the implementation. |
| CACHEABLE | CONNECT responses are typically not cached. |

## PATCH

| PURPOSE | The PATCH method is used to partially update a resource on the server. Unlike PUT, which replaces the entire resource, PATCH only modifies the parts of the resource specified in the request. |
| --- | --- |
| IDEMPOTENT | PATCH is not guaranteed to be idempotent, as the outcome can depend on the specific changes being made.
However, it can be idempotent if implemented carefully. |
| SAFE | No, PATCH is not considered safe, as it can modify resources on the server. |
| PAYLOAD | PATCH requests include a message body or payload, which contains the changes to be applied to the resource. |
| CACHEABLE | PATCH responses are typically not cached. |