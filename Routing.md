# Routing Things 

## 🧠 TL;DR

* Reverse Proxy = A "traffic director" that hides backend servers.
* Load Balancer = A "traffic distributor" that spreads load.
* API Gateway = A "smart doorman" that manages, secures, and routes API requests.

## 🔁 1. Reverse Proxy

### 📌 What it is:
A reverse proxy sits between the client and one or more backend servers. It forwards client requests to those servers and sends back the responses.

### 🛠️ What it does:
- Hides internal server architecture.
- Handles SSL termination (HTTPS decryption).
- Caches responses.
- Compresses content.
- Adds security by preventing direct access to backend servers.

### 🧠 Simple Example:
```
Client ---> Reverse Proxy ---> Web Server
```
Say you're using Nginx or Apache HTTPD to forward traffic to a Node.js app running on port 3000. That’s a reverse proxy.

## ⚖️ 2. Load Balancer

### 📌 What it is:
A load balancer distributes incoming traffic across multiple servers to ensure no single server is overwhelmed.

### 🛠️ What it does:
- Balances traffic using algorithms (Round Robin, Least Connections, IP Hash).
- Monitors health of servers (health checks).
- Increases availability and fault tolerance.
- Can do SSL termination like a reverse proxy.

### 🧠 Simple Example:
``` 
           				/--> Server 1
Client --> Load Balancer
           				\--> Server 2
```
HAProxy, AWS ELB, and Nginx can act as load balancers.

### 🔍 Types:
- Layer 4 Load Balancer: Based on IP and port (TCP/UDP).
- Layer 7 Load Balancer: Based on HTTP(S) headers, cookies, URLs (more intelligent routing).

## 🧭 3. API Gateway

### 📌 What it is:
An API Gateway is a specialized reverse proxy tailored for managing API traffic. It sits between clients and microservices.

### 🛠️ What it does:
- Request routing and protocol translation.
- Authentication and authorization.
- Rate limiting, throttling, and quotas.
- API versioning and analytics.
- Can aggregate responses from multiple services.
- Often comes with a developer portal.

### 🧠 Simple Example:
```
Client --> API Gateway --> Auth Service
                      \-> User Service
                       \-> Product Service
``` 
Kong, Apigee, AWS API Gateway, and Zuul are examples.

## 🆚 Summary Table:

Feature	| Reverse Proxy	| Load Balancer	| API Gateway
------- | ------------- | ------------- | ----------
Main Goal	| Forward traffic	| Distribute traffic	| Manage APIs
Traffic Routing	| Yes	| Yes	| Yes
Load Distribution	| ❌	| ✅	| ✅ (to services)
Auth/Rate Limit	| ❌ (basic)	| ❌	| ✅
SSL Termination	| ✅	| ✅	| ✅
Protocol Handling	| Basic	| Basic	| Advanced (REST, gRPC, WebSocket)
Request Aggregation	| ❌	| ❌	| ✅

