# Stateless API

Stateless API is an API architecture where the server does not store client session information between requests.

Each request from the client is independent, the server treats every request as a completely new request.

In Stateless APIs, the client must send all required information with every request.

The server does not remember previous requests or user sessions.

REST APIs are commonly designed as Stateless APIs.

Example, when accessing a protected API, the client sends authentication token in every request.

Example request:

```http
GET /users
Authorization: Bearer token123
```

The server validates the token for every request separately.

If the client sends another request, the server again checks the token because no session information is stored.

Stateless APIs are easier to scale, because any server can handle any request.

Load balancers work efficiently with Stateless APIs, requests can go to different servers without session dependency.

Stateless APIs improve reliability and scalability in cloud and microservices environments.

Stateless APIs reduce server memory usage because session data is not stored on the server.

Stateless APIs are commonly used in REST APIs, Kubernetes APIs, cloud-native applications, and microservices.

## Advantages of Stateless APIs

Stateless APIs are highly scalable.

Stateless APIs are easier to distribute across multiple servers.

Stateless APIs improve fault tolerance and reliability.

Stateless APIs reduce server-side memory usage.

Stateless APIs are simpler for load balancing.

## Disadvantages of Stateless APIs

Each request may become larger because all information must be sent repeatedly.

Repeated authentication validation may slightly increase processing overhead.

Client applications must manage session-related information themselves.

# Stateful API

Stateful API is an API architecture where the server stores client session information between requests.

The server remembers previous interactions and maintains session state for each client.

Stateful APIs depend on stored session data during communication.

The client does not need to send complete information in every request because the server already remembers session details.

Traditional web applications commonly use Stateful APIs.

Example, when a user logs into a website, the server creates a session and stores session information.

The server sends a session ID to the client.

Future requests use the session ID to identify the user session.

Example request:

```http
GET /profile
Cookie: sessionid=abc123
```

The server checks the stored session using the session ID.

The server remembers login state, user preferences, and previous actions.

Stateful APIs require session storage on the server side.

If the session server fails, users may lose their active sessions.

Stateful APIs can become difficult to scale because requests may need to go to the same server holding session information.

Sticky sessions are sometimes used in load balancers for Stateful APIs.

## Advantages of Stateful APIs

Stateful APIs simplify session handling for clients.

Stateful APIs reduce repeated authentication data in requests.

Stateful APIs are useful for applications requiring continuous user interaction.

## Disadvantages of Stateful APIs

Stateful APIs consume server memory for session storage.

Stateful APIs are harder to scale across multiple servers.

Session management increases infrastructure complexity.

Server failures may affect active user sessions.

# Stateless vs Stateful APIs

Stateless APIs do not store client session information, Stateful APIs store session information on the server.

Stateless APIs treat every request independently, Stateful APIs remember previous requests.

Stateless APIs scale more easily in cloud environments, Stateful APIs require session management.

Stateless APIs are commonly used in REST APIs and microservices, Stateful APIs are commonly used in traditional web applications and banking systems.

Stateless APIs usually use tokens for authentication, Stateful APIs usually use sessions and cookies.

Stateless APIs reduce server-side memory usage, Stateful APIs require additional memory for session storage.

Stateless APIs are preferred in modern cloud-native architectures because they support scalability, load balancing, and distributed systems efficiently.
