# API Full Concepts

API stands for Application Programming Interface, it is a set of rules and protocols that allows different applications, systems, or services to communicate with each other.

API acts as a bridge between software applications, it allows one application to request data or services from another application.

APIs are widely used in web applications, mobile apps, cloud services, DevOps tools, Kubernetes, microservices, and automation systems.

APIs help applications exchange data securely and efficiently without exposing internal implementation details.

## Why APIs are Used

APIs enable communication between different software systems.

APIs allow applications to share data and functionality.

APIs simplify integration between services and platforms.

APIs improve automation and scalability.

APIs support microservices and cloud-native architectures.

APIs reduce development time by reusing existing services.

## Real-Time API Example

When a mobile weather app shows weather information, the app requests weather data from a weather server API.

The weather server processes the request and sends response data back to the application.

The application displays the weather information to the user.

## API Architecture

API communication mainly contains Client, API Server, Request, Response, Endpoint, and Protocols.

### Client

Client is the application or user sending requests to the API.

Examples are browsers, mobile apps, frontend applications, and automation tools.

### API Server

API Server receives requests, processes them, and sends responses back to clients.

API Servers connect with databases, services, or backend applications.

### Request

Request is the message sent by client to API server asking for data or operations.

Requests contain methods, headers, parameters, and body data.

### Response

Response is the data returned by API server to the client.

Responses usually contain status codes and response data.

### Endpoint

Endpoint is a specific URL used to access API resources.

Example endpoint:

```text id="jlwm1a"
https://api.example.com/users
```

### Protocols

APIs commonly use HTTP and HTTPS protocols for communication.

## API Workflow

Client sends request to API endpoint.

API server receives and processes the request.

API server interacts with databases or services if needed.

API server generates response data.

Response is sent back to the client.

Client displays or processes the response data.

## API Methods

API methods define the type of operation performed.

### GET

GET retrieves data from server.

Example:

```http id="’wini2b"
GET /users
```

### POST

POST sends new data to server.

Example:

```http id="’wini3c"
POST /users
```

### PUT

PUT updates existing data completely.

Example:

```http id="’wini4d"
PUT /users/1
```

### PATCH

PATCH partially updates existing data.

### DELETE

DELETE removes data from server.

Example:

```http id="’wini5e"
DELETE /users/1
```

## API Request Components

### URL

URL identifies API resource location.

### Headers

Headers contain metadata information like content type and authentication tokens.

Example header:

```http id="’wini6f"
Content-Type: application/json
```

### Parameters

Parameters pass additional information in requests.

Example query parameter:

```text id="’wini7g"
https://api.example.com/users?id=1
```

### Body

Body contains data sent to API server mainly in POST and PUT requests.

Example JSON body:

```json id="’wini8h"
{
  "name": "Priyanka",
  "role": "DevOps Engineer"
}
```

## API Response

API response usually contains status code, headers, and response body.

Example response:

```json id="’wini9i"
{
  "status": "success",
  "message": "User created"
}
```

## HTTP Status Codes

### 200 OK

Request completed successfully.

### 201 Created

Resource created successfully.

### 400 Bad Request

Client request contains invalid data.

### 401 Unauthorized

Authentication required or failed.

### 403 Forbidden

Access denied for the requested resource.

### 404 Not Found

Requested resource does not exist.

### 500 Internal Server Error

Server encountered an unexpected error.

## Types of APIs

### REST API

REST called Representational State Transfer is the most commonly used API architecture.

REST APIs use HTTP methods and JSON data format.

REST APIs are stateless, each request contains all required information.

Example REST endpoint:

```text id="’wini0j"
GET /api/users
```

### SOAP API

SOAP called Simple Object Access Protocol is a protocol-based API architecture using XML format.

SOAP provides strict standards and security features.

SOAP is commonly used in enterprise applications.

### GraphQL API

GraphQL allows clients to request only required data.

GraphQL reduces over-fetching and under-fetching problems.

### gRPC

gRPC is a high-performance API framework developed by Google.

gRPC uses Protocol Buffers instead of JSON for fast communication.

## REST API Concepts

### Stateless

REST APIs do not store client session information on server.

Each request is independent.

### Resource

Resource is any data object managed by API.

Example resources are users, products, and orders.

### JSON

JSON called JavaScript Object Notation is the most common API data format.

JSON is lightweight and human-readable.

Example JSON:

```json id="’wini1k"
{
  "id": 1,
  "name": "Priyanka"
}
```

## API Authentication

Authentication verifies client identity before allowing access.

### API Key

API Key is a unique token used to access APIs.

### Basic Authentication

Basic Authentication uses username and password.

### Bearer Token

Bearer Token authentication uses tokens for secure access.

Example header:

```http id="’wini2l"
Authorization: Bearer token123
```

### OAuth

OAuth provides secure third-party authentication and authorization.

OAuth is commonly used by Google, GitHub, and cloud services.

## API Security

Use HTTPS for encrypted communication.

Validate all client input data.

Use authentication and authorization mechanisms.

Avoid exposing sensitive information in responses.

Implement rate limiting to prevent abuse.

Use tokens instead of hardcoded credentials.

## API Testing Tools

### Postman

Postman is used for API testing and debugging.

Postman sends API requests and displays responses visually.

### Curl

`curl` command-line tool sends HTTP requests from terminal.

Example GET request:

```bash id="’wini3m"
curl https://api.example.com/users
```

Example POST request:

```bash id="’wini4n"
curl -X POST https://api.example.com/users \
-H "Content-Type: application/json" \
-d '{"name":"Priyanka"}'
```

## API Gateway

API Gateway acts as a central entry point for APIs.

API Gateway handles authentication, routing, rate limiting, and monitoring.

Popular API Gateways are NGINX, Kong, and Apache APISIX.

## APIs in Microservices

Microservices communicate with each other using APIs.

Each microservice exposes APIs for communication.

APIs enable independent service deployment and scalability.

## APIs in Kubernetes

Kubernetes uses APIs extensively for cluster management.

`kubectl` communicates with Kubernetes API Server.

Kubernetes resources like Pods and Deployments are managed through APIs.

## APIs in DevOps

CI/CD tools expose APIs for automation.

Cloud providers provide APIs for infrastructure management.

Terraform, Jenkins, Docker, and Kubernetes use APIs internally.

Automation scripts commonly interact with APIs.

## API Documentation

API documentation explains endpoints, methods, request formats, and responses.

Swagger and OpenAPI are commonly used for API documentation.

Swagger helps visualize and test APIs.

## API Versioning

Versioning manages API changes without breaking old clients.

Example API versions:

```text id="’wini5o"
/api/v1/users
/api/v2/users
```

## API Advantages

APIs improve software integration and communication.

APIs support automation and scalability.

APIs reduce development time using reusable services.

APIs enable cloud-native and microservices architectures.

APIs improve interoperability between platforms.

## API Limitations

Poorly designed APIs may reduce performance.

Insecure APIs may expose sensitive data.

Managing large numbers of APIs can become complex.

Version compatibility issues may occur between clients and servers.

## API Workflow Example

Frontend application sends API request.

API Gateway receives the request.

Authentication validates the client.

API server processes business logic.

Database operations are performed if needed.

Response data is generated in JSON format.

API server sends response back to client.

Frontend application displays data to the user.
