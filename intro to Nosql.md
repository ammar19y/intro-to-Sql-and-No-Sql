# **NoSQL Database Notes**

## **What is NoSQL?**
**NoSQL** databases are non-relational and schema-less databases optimized for handling **big data** and **real-time applications**. They are known for their flexibility in data models, horizontal scalability, and efficient performance.

it can store structured, semi-structured, and unstructured data, making them ideal for web applications, IoT, and mobile apps that handle dynamic and massive datasets.

---

## **Types of NoSQL Databases**

NoSQL databases come in four primary types: `Document-oriented`, `Key-Value`,` Column-Family`, and` Graph databases`. Here’s a breakdown with syntax and examples for each type:

### **1. Document-Oriented Databases**
Document-oriented databases store data in JSON-like documents. Each document is a self-contained unit of data, making it flexible for handling complex and hierarchical data structures.

- **Popular Databases**: MongoDB, CouchDB
- **Use Cases**: Content management systems, e-commerce, product catalogs, user profiles

#### **Basic Syntax in Document Stores (MongoDB)**
1. **Database Creation** (Implicit):
    - MongoDB automatically creates a database when data is inserted.
  
2. **Insert Document**:
    ```javascript
    db.collectionName.insertOne({
      "name": "Alice",
      "age": 29,
      "email": "alice@example.com",
      "location": { "city": "New York", "zip": "10001" }
    });
    ```

3. **Query Documents**:
    ```javascript
    db.collectionName.find({ "location.city": "New York" });
    ```

4. **Update Document**:
    ```javascript
    db.collectionName.updateOne(
      { "name": "Alice" },
      { $set: { "age": 30 } }
    );
    ```

5. **Delete Document**:
    ```javascript
    db.collectionName.deleteOne({ "name": "Alice" });
    ```

#### **Example of Document-Oriented Database**
Imagine a `products` collection in an e-commerce database to store product details:
```javascript
db.products.insertOne({
  "productName": "Smartphone",
  "brand": "TechBrand",
  "price": 499.99,
  "categories": ["electronics", "smartphone"],
  "inStock": true
}); 
```
---
### **2. Key-Value Stores**
Key-value stores use a simple model that pairs unique keys with values. This type is highly efficient for scenarios where data is frequently accessed by key.

* Popular Databases: Redis, DynamoDB, Riak

* Use Cases: Caching, session management, user preferences, shopping cart data

#### **Basic Syntax in Key-Value Stores (Redis)**

1. **Set Key-Value Pair:**

```sql 
SET user:1001 "session12345"
```

2. **Get Value by Key:**

```sql 
GET user:1001
```

3. **Delete Key-Value Pair:**

```sql 
DEL user:1001
```
#### **Example of Key-Value Store**
Consider storing user session data in Redis:
``` sql 
SET session:userID "session_token_ABC123"
GET session:userID
```
#### **Explanation:**

Each session is stored with a unique key, making retrieval fast and efficient.
---
### **3. Column-Family Stores :**

Column-family stores, or column-oriented databases, organize data by columns rather than rows. This model is suited for analytics and applications that require fast read and write access to large volumes of data.

* Popular Databases: Cassandra, HBase
* Use Cases: Time-series data, analytics, log processing, recommendation engines

Basic Syntax in Column-Family Stores (Cassandra)

1. **Create Keyspace (Database):**

 ``` sql 
 CREATE KEYSPACE my_keyspace
WITH replication = {'class': 'SimpleStrategy', 'replication_factor': 3};
```
2. Create Table:

``` sql
CREATE TABLE my_keyspace.users (
  user_id UUID PRIMARY KEY,
  name text,
  email text,
  age int
);
```
3. **Insert Data:**

``` sql
INSERT INTO my_keyspace.users (user_id, name, email, age)
VALUES (uuid(), 'Alice', 'alice@example.com', 29);
```
4. Query Data:
    
```sql
SELECT name, email FROM my_keyspace.users WHERE user_id = <uuid>;
```

**Example of Column-Family Store**

Consider a user_activity table that stores user actions over time
```sql
CREATE TABLE user_activity (
  user_id UUID,
  timestamp timestamp,
  action text,
  PRIMARY KEY (user_id, timestamp)
);
```
**Explanation:**
Data is organized by columns (e.g., action, timestamp) allowing efficient access to specific data segments

### **4. Graph Databases**
Graph databases store data as nodes (entities) and edges (relationships). This model is ideal for applications that require managing and querying data with complex relationships.

* Popular Databases: Neo4j, Amazon Neptune
* Use Cases: Social networks, recommendation systems, fraud detection, knowledge graphs

**Basic Syntax in Graph Databases (Neo4j)**

1. **Create Node:**
 ```sql
   CREATE (n:User {name: 'Alice', age: 29})
```
2. **Create Relationship:**
 ```sql
 MATCH (a:User {name: 'Alice'}), (b:User {name: 'Bob'})
CREATE (a)-[:FRIEND]->(b)
```
3. **Query Nodes and Relationships:**
 ```sql
MATCH (a:User)-[:FRIEND]->(b:User)
RETURN a.name, b.name
 ```
**Example of Graph Database**
In a social network application:

```sql
CREATE (alice:User {name: 'Alice'})-[:FRIEND]->(bob:User {name: 'Bob'})
MATCH (u:User)-[:FRIEND]->(f:User)
RETURN u.name, f.name

```

**Explanation :**

Nodes (User entities) are connected by FRIEND relationships, allowing traversal through the network

---

# SQL vs. NoSQL: Comparison

| **Aspect**               | **SQL (Relational Databases)**                                 | **NoSQL (Non-Relational Databases)**                           |
|--------------------------|---------------------------------------------------------------|----------------------------------------------------------------|
| **Structure**            | Based on fixed tables with a predefined schema                | Flexible and heterogeneous databases supporting multiple models like documents, key-value, column-family, and graph-based models |
| **Schema Flexibility**   | **Fixed** – Schema must be defined in detail before data entry | **Flexible** – Schema can be modified without updating existing data |
| **Data Integrity & Consistency** | **High** – Enforces strict data validation and relational integrity | **Flexible** – May be less consistent to prioritize performance, often using eventual consistency |
| **Scalability**          | **Vertical** – Increases system capacity by adding resources to a single server | **Horizontal** – Expands by adding multiple servers, facilitating scalability |
| **Data Types**           | Suitable for complex, diverse data connected by primary and foreign keys | Suitable for unstructured, diverse data, allowing heterogeneous data storage in a single database |
| **Transactions**         | Uses ACID (Atomicity, Consistency, Isolation, Durability) to ensure transaction reliability | Uses BASE (Basically Available, Soft state, Eventually consistent) for faster performance with less strict consistency |
| **Use Cases**            | Preferred for financial applications, accounting systems, and any system requiring high data integrity | Preferred for dynamic applications like social media, product recommendations, and IoT data |
| **Examples**             | MySQL, PostgreSQL, Oracle, SQL Server                         | MongoDB, Cassandra, Redis, Neo4j, CouchDB                       |
| **Data Relationships**   | **Complex relationships** – Managed efficiently with primary and foreign keys | **Simple or no relationships** – Preferred for applications with simple or no relational data needs |
| **Performance**          | **Relatively slower** when handling unstructured or non-relational data | **Relatively faster** when managing large volumes of unstructured data, optimized for heavy performance |
| **Development Time**     | Requires upfront schema design and table structure           | Allows for rapid development, especially with dynamic or evolving data models |
| **Community & Support**  | Established community with long-term support, suitable for enterprise systems requiring high security | Growing community with broad support, ideal for fast-growing, innovative applications |

---

## When to Use SQL vs. NoSQL

- **Use SQL Databases** if you need:
  - To manage complex, interconnected data.
  - High data integrity and strict validation.
  - To handle critical transactions, like in banking or accounting systems.
  - Detailed reporting and analysis on fairly stable data.

- **Use NoSQL Databases** if you need:
  - To manage large volumes of constantly changing data (e.g., social media user data).
  - Support for easy and quick horizontal scaling.
  - Flexibility to store diverse, unstructured data.
  - Faster performance, even with relaxed consistency.

---

## Conclusion

SQL databases are ideal for systems requiring strong data structures and complex relationships, while NoSQL is a flexible, high-performance choice for applications managing large, dynamic datasets. The decision between SQL and NoSQL depends on the project type, performance needs, and expected data growth.


# **Resources for Further Learning**
[MongoDB Documentation](https://www.mongodb.com/docs/manual/) : Comprehensive guide and tutorials on MongoDB.

[Redis Documentation](https://redis.io/docs/latest/) : Detailed Redis commands and usage.

[Apache Cassandra Documentation](https://cassandra.apache.org/doc/latest/) : Official Cassandra guide.

[Neo4j Cypher Query Language](https://neo4j.com/docs/cypher-manual/current/introduction/) : Intro to Neo4j’s query language, Cypher.