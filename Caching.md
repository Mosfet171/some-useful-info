# Caching in the Cloud

**Redis vs Memcached?**

## TL;DR:

- Use Memcached when you need simple, fast, volatile caching.
- Use Redis when you need richer features, persistent data, or advanced use cases like queues and pub/sub.

Both are:
- Key-value stores: You store and retrieve data using a key.
- In-memory: All data is stored in RAM, making it very fast.
- Used for caching: To reduce database load and speed up web apps.

## 1. Memcached

- Simple and lightweight
- Stores strings only (no complex data types)
- Good for simple, high-speed caching
- Designed for horizontal scaling (you can add more nodes easily)

### Use cases:
- Caching HTML
- API responses
- Session data
- Database query results
__Very fast for basic use-cases__

## 2. Redis (REmote DIctionary Server)

### More powerful and flexible
Supports many data types:
- Strings, Lists, Sets, Hashes, Sorted Sets, Streams, Bitmaps, etc.
- Can persist data to disk (optional)
- Can be used as a message broker (like a lightweight queue)
- Supports pub/sub, Lua scripting, atomic operations, transactions

### Use cases:
- Caching (like Memcached)
- Session storage
- Real-time analytics
- Queues (e.g., task queues in Celery)
- Leaderboards, rate limiting, pub/sub systems

## Quick Comparison:

Feature	| Redis	| Memcached
--------| --------| -----------
Data types	| Strings, Lists, Sets, etc.	| Strings only
Persistence| 	Optional disk persistence	| No persistence
Pub/Sub support	| Yes	| No
TTL support	| Yes	| Yes
Scalability	| Single-threaded (but supports clustering)	| Multi-threaded
Use for queues	| Yes	| Not recommended