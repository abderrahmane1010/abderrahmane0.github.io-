# Hypertext Transfer Protocol principles :

## 1. Stateless :

- Each request from a client to a server is **independent**.
- The server does not retain any information about previous requests.

## 2. Request-Response Model :

- This model is based on the client initiating communication with the server.

## 3. Connectionless :

- After each request-response cycle, the connection between the client and server is closed.
- Connectionless => statelessness of HTTP

## 4. Text-Based :

* HTTP messages are human-readable.
* HTTP messages : headers and content

## 5. Uniform Resource Identifiers (URIs) :

- HTTP uses URIs (known as URLs) to identify resources on the WEB.

## 6. Methods :

- HTTP defines several request methods that indicate the desired action (ex : GET (retrieve data), POST (submit data), PUT (update date), DELETE (remove data))...

## 7. Status Codes :

- HTTP responses include status codes to indicate the outcome of the request.

	[Les réponses informatives](https://developer.mozilla.org/fr/docs/Web/HTTP/Status#réponses_informatives) (`100` - `199`),

[	Les réponses de succès](https://developer.mozilla.org/fr/docs/Web/HTTP/Status#réponses_de_succès) (`200` - `299`),

[	Les messages de redirection](https://developer.mozilla.org/fr/docs/Web/HTTP/Status#messages_de_redirection) (`300` - `399`),

[	Les erreurs du client](https://developer.mozilla.org/fr/docs/Web/HTTP/Status#réponses_derreur_côté_client) (`400` - `499`),

	[Les erreurs du serveur](https://developer.mozilla.org/fr/docs/Web/HTTP/Status#réponses_derreur_côté_serveur) (`500` - `599`)

## 8. Stateless Cookies and Sessions :

- We can implement mechanisms like cookies and sessions to maintain state and user sessions across multiple HTTP requests.

## 9. Extensible :

- Allows flexibility and the addition of new feautures or functionality (Custom headers for example can be defined by developers to carry specific data or instructions)

## 10. Caching :

- HTTP supports caching meachinsms (allowing clients to store and reuse responses from the server to reduce latency and bandwidth usage).