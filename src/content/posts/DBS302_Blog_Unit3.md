---
title:  Unit III: Document Stores (MongoDB)
published: 2026-04-29
description: A simple note about NoSQL Databases.
tags: [Markdown, Blogging]
category:  NoSQL Databases
draft: false
---

# Unit III: Document Stores (MongoDB)

## Introduction

Modern applications generate large amounts of unstructured and semi-structured data. Traditional relational databases sometimes struggle to manage this type of data efficiently. Document databases were introduced to solve this challenge by storing information in flexible document formats.

One of the most popular document databases is **MongoDB**, which stores data as JSON-like documents. This blog explores the concept of document databases, MongoDB architecture, its data model, CRUD operations, query language, scaling techniques, and ecosystem tools.

---

# 3.1 Introduction to Document Databases

## 3.1.1 Concept and Characteristics of Document Stores

A **document database** stores data in documents instead of tables and rows. These documents are typically formatted in **JSON** or **BSON** and can contain nested structures.

### Key Characteristics

- **Schema flexible** – No fixed structure is required.
- **JSON-like documents** – Data is stored in document format.
- **Hierarchical data support** – Nested objects and arrays are supported.
- **High scalability** – Designed for distributed environments.
- **Fast development** – Developers can modify structure easily.

Example document:

```json
{
  "name": "Tshewang Dorji",
  "course": "Software Engineering",
  "skills": ["React", "MongoDB", "JavaScript"]
}
````

---

## 3.1.2 Comparison with Relational and Key-Value Databases

| Feature          | Relational DB           | Key-Value DB    | Document DB            |
| ---------------- | ----------------------- | --------------- | ---------------------- |
| Structure        | Tables & rows           | Key-value pairs | JSON/BSON documents    |
| Schema           | Fixed                   | Flexible        | Flexible               |
| Relationships    | Strong relational model | Limited         | Embedded relationships |
| Query capability | SQL                     | Simple lookups  | Rich queries           |

---

## 3.1.3 Use Cases and Applications

Document databases are widely used in modern applications such as:

* Content management systems
* E-commerce platforms
* Mobile applications
* Real-time analytics
* IoT applications
* Social media platforms

---

# 3.2 MongoDB Architecture

MongoDB uses a distributed architecture designed for performance and scalability.

## 3.2.1 Core Components

### mongod

The **mongod** process is the primary database server that stores and manages data.

### mongos

The **mongos** acts as a query router in sharded clusters.

### Config Servers

Config servers store metadata about the cluster and data distribution.

---

## 3.2.2 Storage Engines

MongoDB supports different storage engines.

### WiredTiger

* Default storage engine
* Provides compression
* Supports document-level concurrency

### In-Memory

* Stores data entirely in RAM
* Extremely fast performance
* Used for high-speed applications

---

## 3.2.3 Replication and Sharding Concepts

### Replication

Replication copies data across multiple servers to ensure availability and fault tolerance.

### Sharding

Sharding distributes data across multiple machines to support horizontal scaling.

---

# 3.3 MongoDB Data Model

MongoDB stores data in flexible documents.

## 3.3.1 BSON (Binary JSON)

MongoDB stores documents using **BSON (Binary JSON)** which extends JSON by supporting additional data types such as:

* Date
* Binary data
* ObjectId

---

## 3.3.2 Document Structure and Embedded Documents

Documents can contain nested structures.

Example:

```json
{
  "name": "Dorji",
  "address": {
    "city": "Thimphu",
    "country": "Bhutan"
  }
}
```

Embedded documents help represent relationships within a single document.

---

## 3.3.3 Collections and Databases

MongoDB organizes data into:

* **Database** → Container for collections
* **Collection** → Group of documents
* **Document** → Individual data record

Structure:

```
Database
 └── Collection
      └── Document
```

---

## 3.3.4 Schema Design Patterns and Best Practices

Good schema design improves performance.

Best practices:

* Embed related data when possible
* Avoid excessive nesting
* Use indexing for frequently queried fields
* Keep documents reasonably sized

---

# 3.4 CRUD Operations in MongoDB

CRUD stands for **Create, Read, Update, and Delete** operations.

---

## 3.4.1 Insert Operations

Insert a single document:

```javascript
db.users.insertOne({
  name: "Dorji",
  age: 22
})
```

Insert multiple documents:

```javascript
db.users.insertMany([
  {name: "Sonam"},
  {name: "Pema"}
])
```

---

## 3.4.2 Read Operations

Retrieve documents:

```javascript
db.users.find()
```

Retrieve one document:

```javascript
db.users.findOne({name: "Dorji"})
```

Projection example:

```javascript
db.users.find({}, {name: 1})
```

---

## 3.4.3 Update Operations

Update one document:

```javascript
db.users.updateOne(
 {name: "Dorji"},
 {$set: {age: 23}}
)
```

Update multiple documents:

```javascript
db.users.updateMany(
 {age: {$gt: 20}},
 {$set: {status: "active"}}
)
```

Replace a document:

```javascript
db.users.replaceOne(
 {name: "Dorji"},
 {name: "Dorji", age: 23}
)
```

---

## 3.4.4 Delete Operations

Delete a single document:

```javascript
db.users.deleteOne({name: "Dorji"})
```

Delete multiple documents:

```javascript
db.users.deleteMany({age: {$lt: 18}})
```

---

# 3.5 MongoDB Query Language

MongoDB provides powerful query capabilities.

---

## 3.5.1 Query Operators

Some common operators include:

| Operator | Meaning               |
| -------- | --------------------- |
| $eq      | Equal                 |
| $gt      | Greater than          |
| $lt      | Less than             |
| $in      | Value exists in array |

Example:

```javascript
db.users.find({age: {$gt: 20}})
```

---

## 3.5.2 Aggregation Framework

Aggregation processes data through pipelines.

Example:

```javascript
db.sales.aggregate([
 {$group: {_id: "$product", total: {$sum: "$amount"}}}
])
```

Stages include:

* `$match`
* `$group`
* `$sort`
* `$limit`

---

## 3.5.3 Text Search and Geospatial Queries

MongoDB supports advanced queries.

### Text Search

```javascript
db.articles.find({$text: {$search: "database"}})
```

### Geospatial Queries

Used for location-based applications.

---

## 3.5.4 Indexes and Query Optimization

Indexes improve query performance.

Example:

```javascript
db.users.createIndex({name: 1})
```

Benefits:

* Faster searches
* Efficient sorting
* Reduced query time

---

# 3.6 MongoDB Transactions and Consistency

MongoDB supports **ACID transactions** for reliability.

---

## 3.6.1 Multi-document ACID Transactions

Transactions allow multiple operations to be executed atomically.

Example scenario:

* Transfer money between accounts
* All operations must succeed or fail together.

---

## 3.6.2 Read and Write Concerns

These settings control data reliability.

* **Read concern** → Level of consistency when reading data
* **Write concern** → Level of acknowledgement required when writing data

---

## 3.6.3 Consistency Models in Distributed Environments

MongoDB provides:

* **Strong consistency** in replica sets
* **Eventual consistency** in distributed clusters

---

# 3.7 Scaling MongoDB

MongoDB is designed to scale easily.

---

## 3.7.1 Replication and Replica Sets

A **replica set** is a group of MongoDB servers that maintain the same data.

Components:

* Primary node
* Secondary nodes

Primary handles writes, secondaries replicate data.

---

## 3.7.2 Sharding Strategies and Shard Keys

Sharding distributes data across servers.

A **shard key** determines how data is distributed.

Good shard keys:

* evenly distribute data
* avoid hotspots

---

## 3.7.3 Horizontal Scaling Techniques

MongoDB scales horizontally by adding more servers to the cluster.

Benefits:

* increased storage
* improved performance
* better fault tolerance

---

## 3.7.4 Load Balancing and Data Distribution

The **mongos router** balances queries across shards ensuring efficient resource usage.

---

# 3.8 MongoDB Ecosystem and Tools

MongoDB provides several tools to improve development and management.

---

## 3.8.1 MongoDB Atlas

MongoDB Atlas is a **cloud-based database service** that manages deployment, backups, and scaling automatically.

Features:

* Fully managed service
* Automated backups
* Built-in monitoring

---

## 3.8.2 Compass

MongoDB Compass is a **GUI tool** used to interact with MongoDB visually.

Features:

* query data
* create indexes
* analyze schema

---

## 3.8.3 Mongoose

Mongoose is an **Object Data Modeling (ODM) library for Node.js**.

Features:

* schema-based models
* validation
* middleware support

Example:

```javascript
const User = mongoose.model("User", {
 name: String,
 age: Number
});
```

---

## 3.8.4 MongoDB Charts and BI Connector

### MongoDB Charts

Used to visualize data through charts and dashboards.

### BI Connector

Allows MongoDB data to be accessed using **SQL-based BI tools** such as Tableau or Power BI.

---

# Conclusion

MongoDB is a powerful and flexible document-oriented database designed for modern applications. Its schema flexibility, horizontal scalability, and strong ecosystem make it a popular choice for developers building scalable web and mobile applications.

Understanding MongoDB architecture, data modeling, CRUD operations, and scaling techniques helps developers design efficient and reliable database systems.

MongoDB continues to evolve as a leading solution in the NoSQL ecosystem, supporting modern cloud-native applications and large-scale distributed systems.



