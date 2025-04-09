# API's

## 🧭 TL;DR Comparison

Feature | REST |  GraphQL | gRPC
---- | ----- | ------ | -----
Protocol | HTTP | HTTP | HTTP/2
Data Format |JSON | JSON | Protobuf
Flexibility |Medium | High | Low (RPC-based)
Speed| Moderate | Moderate|  Very fast
Browser use| Easy | Easy | Hard
Tooling |Mature | Good | Strong (esp. internal use)
Learning curve | Easy | Medium | Higher

## 🚀 What is an API?

API stands for Application Programming Interface. It's like a menu in a restaurant: it tells you what you can ask for and how to ask for it.\

More technically, an API lets different software systems communicate with each other.\

You (the client) make a request.\
The server (the API provider) processes it and sends back a response.

### 🛡️ Auth & Security

APIs often require authentication, using:
* API keys
* OAuth tokens
* JWT (JSON Web Tokens)

### 🔧 Real-World Use Cases

* Frontend websites fetching data from a backend (e.g., weather, stock prices)
* Mobile apps communicating with a server
* Automating tasks (e.g., sending emails via the Gmail API)
* Integrating 3rd-party services (e.g., Stripe for payments)

### Terminology

Term | Meaning
---- | ------
Endpoint | A specific URL path in the API
Payload | The data you send in a request
JSON | A lightweight data format (very common)
Status | Code HTTP response indicator (e.g. 200 OK, 404 Not Found, 500 Error)

## 🌐 REST APIs

REST stands for Representational State Transfer. It's the most common type of API on the web.

### 🔑 Key concepts of REST APIs:
* Based on HTTP (the same protocol browsers use).
* Uses URLs to identify resources (like https://api.site.com/users/1)
* Uses HTTP methods:
  * GET – retrieve data
  * POST – send (create) data
  * PUT/PATCH – update data
  * DELETE – delete data
* Returns data usually in JSON format (sometimes XML).

✅ REST is stateless: each request stands alone — no memory of previous interactions.


## 🧬 GraphQL – Query Language for APIs

### 🧠 What is GraphQL?
GraphQL is a query language and runtime for APIs developed by Facebook. It solves many of the limitations of REST by allowing clients to ask for exactly the data they need, and nothing more.

### 📦 How GraphQL works:
* Single endpoint (usually /graphql)
* You send a query describing the shape of the data you want
* You get only that data in return — not more, not less

#### 🧾 Example:
You might send this:
```
{
  user(id: "1") {
    name
    email
    posts {
      title
      createdAt
    }
  }
}
```
The response:
```
{
  "data": {
    "user": {
      "name": "Alice",
      "email": "alice@example.com",
      "posts": [
        {
          "title": "Intro to APIs",
          "createdAt": "2025-04-01"
        }
      ]
    }
  }
}
```

### 🔥 Why use GraphQL?
* Feature Benefit
* Ask for what you need Avoid under- or over-fetching data
* Flexible and powerful Nest queries to match your UI structure
* Schema-driven Strongly typed: introspection and tooling like GraphiQL
* Versionless Avoid versioning like /v1/ and /v2/

### ❌ Downsides:
* Slightly steeper learning curve
* Complex for simple CRUD-only apps
* Caching and file uploads are more complicated
* Needs more backend setup and tooling


## ⚡ gRPC – High Performance, Remote Procedure Calls

### 🧠 What is gRPC?
gRPC is an open-source framework from Google. It’s used to define and call functions on remote servers, not just fetch data.

It’s ideal for microservices communication — fast, efficient, and strongly typed.

### 🔧 How it works:
You define your API with Protocol Buffers (protobuf):
```
service UserService {
  rpc GetUser (UserRequest) returns (UserResponse);
}
```

* The system generates code in many languages (e.g., Go, Java, Python, etc.)
* Communication happens over HTTP/2, using a binary format — much faster than JSON

### 🚀 Why use gRPC?
Feature | Benefit
----- | -----
Super fast & lightweight | Binary encoding via Protocol Buffers
Ideal for microservices | Especially for internal service-to-service communication
Code generation | Automatically get client & server code from .proto files
Streaming support | Built-in support for real-time, long-lived streams
HTTP/2 |  Enables multiplexing and better performance

### ❌ Downsides:
* Not human-readable (binary format)
* Not ideal for public APIs or browser use (no native browser support without extra work)
* Requires learning and working with Protocol Buffers

## 💬 Other Types of APIs

### SOAP (Simple Object Access Protocol)
* Older, strict, XML-based.
* Heavy on security and structure.
* Used in enterprise environments (e.g., banking, telecom).

### WebSockets
- Not a typical API, but allows real-time, two-way communication (e.g., chat apps, live dashboards).


## 🔄 When to use what?

Use Case |  Best API Type
----- | -----
Public API for web/mobile | REST or GraphQL
Complex, interrelated data (like social feeds) |  GraphQL
Microservices in high-performance environments | gRPC
Enterprise systems with legacy support | SOAP (rare today)
Real-time updates (chat, games) | WebSockets or gRPC streaming

