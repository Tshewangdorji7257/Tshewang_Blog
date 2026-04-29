---
title:  Key-Value Databases (Redis)
published: 2026-04-29
description: A simple note about NoSQL Databases.
tags: [Markdown, Blogging]
category:  NoSQL Databases
draft: false
---

# Unit II: Key-Value Databases (Redis)

## 2.1 Introduction to Key-Value Databases

Key-value databases are a type of NoSQL database designed to store data as a collection of key–value pairs. Each key acts as a unique identifier, and the value contains the associated data. These databases are optimized for simplicity, high performance, and scalability.

### 2.1.1 Concept and Architecture

In a key-value database, data is stored as:

```

key → value

```

The key is used to retrieve the value efficiently. The value can be anything such as a string, number, JSON object, or binary data.

Architecture characteristics:

- Simple data model
- Fast read and write operations
- In-memory storage (in many systems)
- Distributed architecture support

A typical architecture includes:

Client → Key-Value Store → Memory/Disk Storage

### 2.1.2 Advantages and Limitations

**Advantages**

- Extremely fast data retrieval
- Simple data model
- Easy horizontal scalability
- Flexible schema
- Ideal for caching and session storage

**Limitations**

- Limited querying capabilities
- No complex relationships like relational databases
- Data modeling may require careful design
- Not suitable for complex analytics

### 2.1.3 Common Use Cases

Key-value databases are commonly used for:

- Caching systems
- Session management
- User preference storage
- Shopping carts
- Leaderboards
- Real-time analytics

---

# 2.2 Redis Fundamentals

Redis is an open-source, in-memory key-value data store widely used for caching, real-time applications, and message brokering.

## 2.2.1 Redis Data Model

Redis stores data as key-value pairs where keys are strings and values can be multiple data structures.

Example:

```

SET username "tshewang"
GET username

```

Redis keeps most of its data in memory, which allows extremely fast operations.

## 2.2.2 Redis Data Types

Redis supports several powerful data structures.

### Strings

The simplest Redis data type.

```

SET name "Alice"
GET name

```

### Lists

Ordered collection of strings.

```

LPUSH tasks "task1"
LPUSH tasks "task2"
LRANGE tasks 0 -1

```

### Sets

Unordered collection of unique elements.

```

SADD users "Alice"
SADD users "Bob"
SMEMBERS users

```

### Hashes

Used to store objects with fields and values.

```

HSET user:1 name "Alice"
HSET user:1 age 25
HGETALL user:1

```

### Sorted Sets

Similar to sets but with scores used for ranking.

```

ZADD leaderboard 100 "Alice"
ZADD leaderboard 200 "Bob"
ZRANGE leaderboard 0 -1 WITHSCORES

```

---

# 2.3 Redis Data Structures and Algorithms

Redis provides advanced probabilistic and specialized data structures.

## 2.3.1 Bitmaps and Bitfields

Bitmaps allow efficient storage of binary data and are often used for tracking boolean values.

Example use case:
- Tracking user logins

```

SETBIT login:2026-04-01 1001 1
GETBIT login:2026-04-01 1001

```

Bitfields allow manipulation of specific bits inside a value.

---

## 2.3.2 HyperLogLog for Cardinality Estimation

HyperLogLog is a probabilistic data structure used to estimate the number of unique elements in a dataset.

It uses very little memory (about 12 KB).

Example:

```

PFADD visitors user1 user2 user3
PFCOUNT visitors

```

Common uses:

- Unique website visitors
- Unique IP counting

---

## 2.3.3 Bloom Filters for Membership Testing

Bloom filters help determine whether an element might exist in a set.

Features:

- Very memory efficient
- No false negatives
- Small chance of false positives

Use cases:

- Checking if an item already exists
- Spam filtering
- Cache optimization

---

## 2.3.4 Geospatial Indexes

Redis supports location-based queries.

Example:

```

GEOADD locations 85.3240 27.7172 "Thimphu"
GEODIST locations "Thimphu" "Paro"

```

Use cases:

- Location-based services
- Ride-sharing apps
- Nearby restaurant searches

---

# 2.4 Redis Persistence and Durability

Although Redis is in-memory, it supports persistence mechanisms to store data on disk.

## 2.4.1 RDB Snapshots

RDB (Redis Database) snapshots save the dataset at specific intervals.

Advantages:

- Compact storage
- Fast recovery
- Good for backups

Disadvantages:

- Possible data loss between snapshots

---

## 2.4.2 AOF (Append-Only File)

AOF logs every write operation received by the server.

Advantages:

- Better durability
- Minimal data loss

Disadvantages:

- Larger file sizes
- Slower than RDB

---

## 2.4.3 Hybrid Persistence Strategies

Redis can combine **RDB + AOF** for improved performance and reliability.

Benefits:

- Faster startup
- Stronger durability
- Reduced data loss risk

---

# 2.5 Redis Clustering and High Availability

Redis supports scaling and fault tolerance through clustering and replication.

## 2.5.1 Redis Sentinel for Automatic Failover

Redis Sentinel monitors Redis instances and performs automatic failover.

Functions:

- Monitoring servers
- Notification system
- Automatic master election

If a master node fails, Sentinel promotes a replica.

---

## 2.5.2 Redis Cluster for Horizontal Scaling

Redis Cluster distributes data across multiple nodes.

Key features:

- Data sharding
- Automatic failover
- High scalability

The keyspace is divided into **16,384 hash slots**.

---

## 2.5.3 Replication and Data Synchronization

Redis replication allows one master server to replicate data to multiple replicas.

Benefits:

- Data redundancy
- Load balancing
- Improved read performance

Example:

```

replicaof <master-ip> <port>

```

---

# 2.6 Redis Modules and Extensions

Redis can be extended using modules.

## 2.6.1 RediSearch for Full-Text Search

RediSearch adds powerful full-text search capabilities.

Features:

- Indexing
- Query filtering
- Ranking results

---

## 2.6.2 RedisJSON for JSON Document Storage

RedisJSON allows storing and querying JSON documents.

Example:

```

JSON.SET user:1 $ '{"name":"Alice","age":25}'
JSON.GET user:1

```

---

## 2.6.3 RedisTimeSeries for Time-Series Data

RedisTimeSeries is optimized for time-stamped data.

Use cases:

- IoT sensors
- Monitoring metrics
- Financial data tracking

---

## 2.6.4 RedisAI for Machine Learning Model Serving

RedisAI enables serving machine learning models directly inside Redis.

Supported frameworks:

- TensorFlow
- PyTorch
- ONNX

Use cases:

- Real-time predictions
- AI-powered applications

---

# 2.7 Redis Performance Optimization

## 2.7.1 Pipelining and Transactions

Pipelining allows sending multiple commands without waiting for responses.

Example:

```

PIPELINE
SET key1 value1
SET key2 value2
SET key3 value3

```

Transactions ensure multiple commands execute sequentially.

```

MULTI
SET a 10
SET b 20
EXEC

```

---

## 2.7.2 Memory Management and Eviction Policies

Redis supports eviction policies when memory limits are reached.

Common policies:

- **noeviction**
- **allkeys-lru**
- **volatile-lru**
- **allkeys-random**

LRU (Least Recently Used) is commonly used for caching systems.

---

## 2.7.3 Benchmarking and Monitoring Tools

Tools used to monitor Redis performance:

- `redis-benchmark`
- `redis-cli`
- Redis Insight
- Prometheus + Grafana

These tools help analyze performance, latency, and memory usage.

---

# 2.8 Redis Security Considerations

Security is important when deploying Redis in production.

## 2.8.1 Authentication and Access Control

Redis supports password authentication.

Example:

```

requirepass strongpassword

```

Access control lists (ACLs) allow role-based access.

---

## 2.8.2 SSL/TLS Encryption

Redis can secure connections using TLS.

Benefits:

- Encrypted communication
- Protection from network attacks

---

## 2.8.3 Redis Security Best Practices

Best practices include:

- Disable protected mode only when necessary
- Use strong authentication
- Restrict network access
- Enable TLS encryption
- Regularly update Redis
- Monitor logs and activity

---

# Conclusion

Redis is a powerful in-memory key-value database designed for speed, scalability, and flexibility. Its support for diverse data structures, advanced algorithms, and high availability features makes it ideal for modern applications such as caching, real-time analytics, and distributed systems. By understanding Redis fundamentals, persistence mechanisms, clustering, and security practices, developers can build high-performance and reliable systems.

