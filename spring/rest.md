# REST

## Table of Content

- [Web Services / API](#web-services-/-api)
- [HTTP Verbs](#http-vers)
- [Caching](#caching)
- [Stateless](#stateless)
- [Stateful vs Stateless](#stateful-vs-stateless)

Representational State Transfer (REST) is a type of software design that helps create web services. It's lightweight, easy to maintain and scale.

Web services are software systems that allow machines to talk to each other over a network, and is also commonly referred to as an API.

## Web Services / API

RESTful web services usually use JSON (JavaScript Object Notation) to represent data. JSON is a lightweight and easy-to-read format that machines can easily understand and create. It is often preferred over XML because it has a simpler syntax and parsing times are faster. However, other data formats can also be used depending on the needs of the service.

- RESTful web services use JSON to represent data
- JSON is lightweight and easy-to-read
- JSON is preferred over XML due to simpler syntax and faster parsing times
- Other data formats can also be used depending on the needs of the service

JSON example:

```JSON
{
  "firstnam": "Bao",
  "lastname": "Duong",
  "job": "Software Engineer"
}
```

The left side of the JSON example represents the key, or property name, and the right side represents the value associated with that key. In the example, "firstname" is a key with the value "Bao", "lastname" is a key with the value "Duong", and so on.

## HTTP Verbs

REST is lightweight and easy to maintain and scale because it uses HTTP commands to create, read, update and delete web service resources. Resources are identified by URIs, which are used to make requests to the web service.

- REST uses HTTP commands to create, read, update, and delete web service resources
  - **Create**: The HTTP POST command is used to create new resources.
  - **Read**: The HTTP GET command is used to retrieve existing resources.
  - **Update**: The HTTP PUT or PATCH commands are used to modify existing resources.
  - **Delete**: The HTTP DELETE command is used to remove existing resources.
- Resources are identified by URIs
  - An example of a URI (Uniform Resource Identifier) is `https://www.example.com/api/users/123`. This URI identifies the resource of a user with ID 123 in an API hosted on the domain `www.example.com`.
    - **`https`** is the scheme, which identifies the protocol to be used to access the resource on the Internet.
    - **`www.example.com`** is the authority (typically includes the server name).
    - **`/api/users/123`** is the path, which identifies the specific resource in the host that the web client wants to access.

In summary, REST is a popular and widely-used software design for creating web services that are easy to develop, scalable, and maintainable.

## Caching

Caching is important for RESTful web services because it reduces the amount of network traffic and improves performance. This is done by storing frequently requested data on the client side, so that future requests for the same data can be served from the cache instead of making a new request to the server. This makes retrieving data faster, especially for large datasets.

- Caching helps reduce network traffic and improve performance
- A copy of frequently requested data is stored on the client side
- Instead of making a new request to the server, the cache can serve subsequent requests for the same data.
- This greatly reduces the amount of time required to retrieve data, especially for large datasets

## Stateless

REST is stateless, meaning that each request contains the necessary information to complete it. The server does not need to keep track of any previous requests or sessions. This makes RESTful web services scalable and easy to maintain, as they can handle many requests without keeping track of any state information.

- REST is stateless
- Each request made to the server contains all the necessary information to complete the request
- The server does not need to keep track of any previous requests or sessions
- RESTful web services are very scalable and easy to maintain, as they can easily handle a large number of requests without needing to keep track of any state information

### Stateful vs Stateless

- **Stateful Restaurant (Fine Dining):** When you go to a high-end restaurant, you're often assigned a specific waiter for your table. This waiter is responsible for your experience during your stay at the restaurant. They will remember what you ordered, any special requests you made, your allergies, whether you need a refill on your drink, etc. The waiter maintains a "state" of your experience throughout your meal. If the waiter leaves in the middle of your meal, they need to pass all that information to a new waiter to ensure your experience isn't interrupted. This is similar to a stateful system.
- **Stateless Restaurant (Fast Food):** On the other hand, when you go to a fast-food restaurant, your experience is different. You place your order at the counter, the person at the counter gives you a receipt with a number. They don't really care who you are or what your previous orders were. When your order is ready, your number is called, you pick up your order, and that's it. If you want to place another order, the process starts all over again without any knowledge of the previous transaction. This is akin to a stateless system.

In computing, a stateful system remembers previous interactions and uses that information for future transactions. A stateless system treats each transaction as new and doesn't keep any information from previous ones.

Stateless web services are faster than stateful ones because the server does not need to remember previous requests or sessions. Each request to the server contains everything needed to complete it, so the server can easily process the request and return the result without needing to get or save any extra information. This makes RESTful web services very scalable and easy to maintain since they can handle many requests without needing to remember any state information.
