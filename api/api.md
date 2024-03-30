# APi = Application Programming Language
An API, or Application Programming Interface, is like a bridge that allows different software applications to communicate with each other. Imagine you're at a restaurant. You, the client, interact with the waiter (the API) to place your order (send a request) to the kitchen (the server). The kitchen then prepares your food (processes the request) and serves it back to you through the waiter. In this analogy, the waiter is the intermediary that abstracts away the complexity of what happens in the kitchen, allowing you to simply place your order and get your food.

APIs can be used for a variety of purposes, such as accessing data from a remote server, integrating with third-party services, or enabling communication between different parts of a complex software system. They make it easier for developers to build new software applications by providing standardized interfaces for interacting with existing systems or services, without needing to understand the inner workings of those systems.

## Difference Between REST API vs Web API vs SOAP API Explained
### 1. REST API
- REST Architectural Style
- HTTP Method (GET,PUT,POST,DELETE)
- return JSON,XML
- stateless client-server model(That's means server don't store any kinds of request data, everything sent by request for checking data validaty)
- suitable for simple application
- REST is an architectural style for designing networked applications.
- REST APIs use standard HTTP methods such as GET, POST, PUT, DELETE to perform CRUD (Create, Read, Update, Delete) operations on resources.
- REST APIs typically use JSON (JavaScript Object Notation) or XML (eXtensible Markup Language) as the data format for requests and responses.
- They are lightweight, scalable, and easy to understand, making them popular for building web services.
- REST APIs are stateless, meaning each request from a client to the server must contain all the information necessary to understand and fulfill that request.

### 2. Web API
- Doestn't follow any structure
- use any protocol or technology
- use any data format
- can be sateful and sateless
- sutable for building complex application

### 3. SOAP(Simple Object Access Protocol)
- SOAP is a protocol for exchanging structured information in the implementation of web services.
- SOAP APIs use XML for messaging format and are typically transported over HTTP or SMTP (Simple Mail Transfer Protocol).
- They often rely on XML schemas for defining the structure of messages and use a set of well-defined standards for security, transactions, and other features.
- SOAP APIs are more rigid and have more overhead compared to REST APIs, but they can offer more advanced features like built-in security, reliable messaging, and standardized error handling.
- SOAP APIs are commonly used in enterprise environments where interoperability and reliability are critical.

#### Here [Ref](https://stackoverflow.com/questions/13025417/what-is-the-different-between-restful-and-restless)

### REST
REST determines how the API will look and work and what architectural pattern developers will follow to build it.
Some of the key principles REST APIs follow are:

**Layered system** – REST elements cannot see beyond their appointed layer. This results in improved scalability and easier addition of proxies and load balancers.

**Uniform interface** – The most important feature of the REST architectural pattern is its emphasis on the uniformity of interfaces between all the components.

**Cacheability** – REST servers have to identify their responses as cacheable or not so that disposing of non–cacheable information and caching required information is possible for performance improvement.

**Statelessness** – In REST applications, clients maintain the application state, but servers do not manage any client state. The service requests comprise all the information needed for processing.

### RESTful API:

- A RESTful API is simply a REST API that adheres to the principles of REST closely or entirely.
- It implements the key principles of REST, such as statelessness, uniform interface (using standard HTTP methods and URIs), client-server architecture, and the use of hypermedia for application state transitions (HATEOAS).
- A RESTful API is designed to be intuitive, scalable, and maintainable, following the constraints and recommendations outlined by the REST architectural style.