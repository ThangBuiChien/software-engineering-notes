## Table of Contents

- [📌 Object-Oriented Programming](#📌-object-oriented-programming)
- [📌 Java Core](#📌-java-core-)
- [📌 Database (SQL & NoSQL)](#📌-database-sql-and-nosql)
- [📌 Data Structures & Algorithms (DSA)](#📌-data-structures-and-algorithms)
- [📌 System Design](#📌-system-desgin)
- [📌 Networking Essential](#📌-networking)
- [📌Operating System](#📌-operating-system)
- [📌 Spring Framework](#📌-spring-framework)
- [📌 Microservices](#📌-microservices)

## **📌 Object-Oriented Programming (OOP)**

- **4 Principles** (Encapsulation, Abstraction, Inheritance, Polymorphism)
  - Encapsulation (Data Hiding & Protection)
    - Wraps data (fields) and methods in a single unit (class).
    - Restricts direct access to data using private variables.
    - Provides getters/setters for controlled access.
  - Abstraction (Hiding Implementation, Showing Only Essentials)
    - Hides complex details and only exposes functionality.
    - Focus on what an object does instead of how it does it.
    - Achieved using abstract classes or interfaces.
  - Inheritance (Code Reusability & Hierarchy)
    - Allows a new class to inherit properties and behavior from an existing class.
    - Promotes code reusability and reduces redundancy.
    - Supports the `is-a` relationship.
  - Polymorphism (Many Forms)
    - Allows methods to have multiple implementations.
    - Two types:
      - Method Overloading (Compile-time) → Same method name, different parameters.
      - Method Overriding (Runtime) → Same method name in parent & child, different behavior.
- **SOLID Principles**
  - Single Responsibility Principle (SRP)
    - A class should have only one reason to change.
  - Open/Closed Principle (OCP)
    - A class should be open for extension but closed for modification.
  - Liskov Substitution Principle (LSP)
    - Objects of a superclass should be replaceable with objects of its subclasses without affecting the functionality.
  - Interface Segregation Principle (ISP)
    - A client should never be forced to implement an interface that it doesn't use.
  - Dependency Inversion Principle (DIP)
    - High-level modules should not depend on low-level modules. Both should depend on abstractions.
    - Abstractions should not depend on details. Details should depend on abstractions.
- **Design Patterns** (Singleton, Factory, Observer, Strategy, etc.)
- **Composition vs Inheritance**
  - **Composition**: Has-A Relationship
    - Combining multiple classes to create a more complex class.
    - Better code reuse, flexibility, and testability.
    - Ex: Car has an Engine, Car has a Wheel
  - **Inheritance**: Is-A Relationship
    - Creating a new class by inheriting properties and behavior from an existing class.
    - Promotes code reusability but can lead to tight coupling.
    - Ex: Car is a Vehicle, Dog is an Animal
      => The best way rather than make it inherit from a class. We should keep the same, abstract what difference and use composition to combine them. The even better is composition using interface rather than class to make it more flexible and easy to change in the future.
    - Ex:
      ```java
      public class Car {
        private Engine engine;
        private Wheel wheel;
        // constructor, methods
      }
      ```
- **Interfaces & Abstract Classes**

  - **Abstract Class vs Interface (Java)**
    | Feature | Abstract Class | Interface |
    |---------|--------------|-----------|
    | **Method Implementation** | Can have both abstract & concrete methods | Only abstract methods (default/static allowed from Java 8) |
    | **Variables** | Can have instance variables | Only `public static final` (constants) |
    | **Access Modifiers** | `public`, `protected`, `private` allowed | Methods are `public` by default |
    | **Constructors** | Allowed | Not allowed |
    | **Multiple Inheritance** | Not supported | Supported |
    | **Use Case** | Code reuse, common fields, base class | Define a contract, multiple inheritance |

  **When to Use?**

  - **Abstract Class** → Common fields, shared behavior, base class
  - **Interface** → Define a contract, multiple inheritance

  **Rule of Thumb:**

  - **Use abstract classes** when objects share behavior **and** state.
  - **Use interfaces** when unrelated classes need a common behavior.

---

## **📌 Java Core**

- **JVM (Memory Model, Garbage Collection)**
- **Collections Framework** (List, Set, Map, Queue)
- **Java 8+ Features** (Streams, Lambda, Optional)
- **Concurrency (Threads, Executor Service, Synchronization)**
- **Exception Handling**
- **Generics**
- **I/O Streams & Serialization**
- **Functional Interfaces & Default Methods**
- **Reflection API**

---

## **📌 Database (SQL & NoSQL)**

- **SQL Basics** (DDL, DML, DCL, TCL)

  - DDL( Data definition language): Create, Alter, Drop, Truncate
    - Used for defining the database schema
    - Create: Create a new table, database, index, etc
    - Alter: Modify the structure of the table
    - Drop: Delete the table, database, index, etc
    - Truncate: Delete all records from the table
  - DML( Data manipulation language): Insert, Update, Delete, Select
    - Used for managing data within the database
    - Insert: Add new records to the table
    - Update: Modify existing records in the table
    - Delete: Remove records from the table
    - Select: Retrieve data from the table
  - DCL( Data control language): Grant, Revoke
    - Used for controlling access to the database
    - Grant: Give permission to users
    - Revoke: Take back permission from users
  - TCL( Transaction control language): Commit, Rollback, Savepoint
    - Used for managing transactions
    - Commit: Save the transaction
    - Rollback: Undo the transaction
    - Savepoint: Set a point within a transaction

- **SQL basics2**

  - Aggregate function and Group by

    - Aggregate:
      - Perform calculations on a set of values and return a single result
      - Include: COUNT, SUM, AVG, MIN, MAX
    - Group by: Group rows that have the same values in specified columns into summary rows
    - Having: Filter groups based on a specified condition

  - Set Operation (Union, Intersect, Except)
    - Set operation: Combine the result of two or more SELECT statements => same number of columns, same data type
    - Union: Combines results from two queries without duplicates.
    - Union All: Combines results from two queries with duplicates.
    - Intersect: Only common rows between two SELECT statements.
    - Except: Return the rows that are in the first SELECT statement but not in the second SELECT statement

- **Indexes** (B-Tree, Hash Index, Invert Index)

  - What is Index?

    - Instead of scanning the whole table, the database can use an index to look up the data at specific locations => faster query

  - Type of Index

    - **B-Tree Index**
      - Balanced Tree => fast search, insert, delete
      - Suitable for range queries (e.g., BETWEEN, >, <)
      - Used in most databases (MySQL, PostgreSQL, Oracle)
    - **Hash Index**
      - Directly map the key to the value => fast search
      - Suitable for equality queries (e.g., WHERE id = 5)
      - Used in memory-based databases (Redis, Memcached)
    - **Inverted Index**

      - Map from the value to the key => fast search
      - Suitable for full-text search (e.g., search engine)
      - Used in search engines (Elasticsearch, Solr)

    - When to use Index
      - **Selectivity**: Low selectivity => not use index, High selectivity => use index
      - **Cardinality**: High cardinality => use index, Not use index in gender (M, F) => low cardinality
      - **Query Performance**: Index can improve query performance but slow down write operation
      - **Data Modification**: Frequent data modification => not use index

- **Joins** (INNER, LEFT, RIGHT, FULL)
  - **Join** => combine rows from two or more tables based on a related column
  - **Inner Join** => Returns only matching rows from both tables.
  - **Left Join** => returns all records from the left table, and the matched records from the right table. No match => NULL values
  - **Right Join** => returns all records from the right table, and the matched records from the left table. No match => Null values
  - **Full Join** => returns all records when there is a match in either left (table1) or right (table2) table records
- **Normalization & Denormalization**
  - **Normalization**
    - Break larger table into smaller tables and define relationships between them
    - Eliminates redundancy, ensures data consistency, and prevents anomalies.
    - Ex: we have customer tables, in order tables, we have orderId, customerID but also customerName, customerPhone, etc
      =>info of customer is redundancy, duplicate => when we try to update customer info, we have to update in many places => inconsistency and anomalies
    - Used NF (1NF, 2NF, 3NF, BCNF)
    - Slower queries due to more Join
    - Best for transactional system such as banking, financial system
  - **Denormalization**
    - Merge tables into one to reduce the number of joins => improve read Performance
    - Add some redundancy but speed up read operation
    - It is useful in read-heavy applications (like analytics, reporting systems).
    - It improves performance but increases storage needs and risks data inconsistency.
  - **NF**
    - 1NF: Each column should have a single value
    - 2NF: 1NF + no partial dependency, each non-key attribute is fully functional dependent on the primary key
    - 3NF: 2NF + no transitive dependency, non-key attribute is not dependent on another non-key attribute
    - BCNF: 3NF + no dependency on a candidate key
- **Transactions** (ACID, isolation levels)

  - What is **transaction**
    - **set of database operations** that must be executed as a **single unit** (commit or rollback)
  - ACID Properties (Ensure Data Integrity)
    - **Atomicity**: All operations in a transaction must be completed successfully, or none of them should be completed.
    - **Consistency**: The database must remain in a consistent state before and after the transaction.
    - **Isolation**: Transactions should be isolated from each other until they are completed.
    - **Durability**: Once a transaction is completed, the changes made by it should be permanent and survive system failure.
  - **Isolation Levels**

    - **Read Uncommitted**: No rule at all => transaction can read uncommitted data
    - **Read Committed**: Transaction can only read committed data => prevent dirty read
    - **Repeatable Read**: Transaction can read data that has been read before => prevent non-repeatable read but still have phantom read
    - **Serializable**: No Concurrency but need to wait for other transaction to finish => no problem with Concurrency but slow

  - **Locking** (Optimistic vs. Pessimistic Locking)
    - **Optimistic Locking**: Assume no conflict => check for conflict at the end of the transaction
    - **Pessimistic Locking**: Assume conflict => lock the data until the transaction is completed
  - **Deadlocks** (Detection, Prevention, Avoidance)
    - **Deadlock**: Two or more transactions are waiting for each other to release the lock => none of them can proceed
    - **Detection**: Periodically check for deadlocks and kill one of the transactions
    - **Prevention**: Lock all resources at once => no deadlock but slow
    - **Avoidance**: Lock resources based on a priority => prevent deadlock but not 100% guarantee

- **Stored Procedures, Trigger, View, Function, Constrain**
  - Stored Procedures: Precompiled SQL statements that are stored in the database and can be executed multiple times.
  - Trigger: A set of SQL statements that are automatically executed when a specified event occurs.
  - View: A virtual table that is based on the result of a SELECT statement.
  - Function: A set of SQL statements that can be called by other SQL statements, return a value, not change the database state.
  - Constrain: Rules that enforce data integrity in a database.
- **Query Optimization** (EXPLAIN, slow queries)
- **NoSQL Basics** (Key-Value, Document, Column, Graph)
  - Key-Value: Stores data as key-value pairs (Redis, DynamoDB)
  - Document: Stores data in documents such as JSON or XML (MongoDB, Couchbase)
  - Column: Stores data in columns rather than rows (Cassandra, HBase)
  - Graph: Stores data in nodes and edges (Neo4j, Amazon Neptune)
- **CAP Theorem** (Consistency, Availability, Partition Tolerance)
  - Consistency: All nodes see the same data at the same time.
  - Availability: Every request gets a response on success/failure.
  - Partition Tolerance: The system continues to operate despite network failures.

---

## **📌 Data Structures & Algorithms (DSA)**

- **Time & Space Complexity (Big-O)**
- **Arrays & Strings** (sorting, searching, two-pointer, sliding window)
- **Linked List** (singly, doubly, fast-slow pointer)
- **Stack & Queue** (monotonic stack, priority queue)
- **Hashing** (hash maps, hash sets, collision handling)
- **Recursion & Backtracking** (combinations, permutations)
- **Binary Trees & BST** (traversals, height, LCA, balancing)
- **Heaps** (min/max heap, heap sort, top-k elements)
- **Graphs** (BFS, DFS, shortest path, connected components)
- **Dynamic Programming** (knapsack, LIS, LCS, memoization/tabulation)

---

## **📌 Spring Framework**

### 🔹 **Spring Core**

- **Spring Beans & Lifecycle**
- **Dependency Injection (Constructor vs Setter)**
- **Bean Scopes & Proxying**
- **ApplicationContext vs BeanFactory**
- **AOP (Aspect-Oriented Programming)**

### 🔹 **Spring Boot**

- **Spring Boot Starter & Auto-Configuration**
- **Spring Boot Profiles & Properties**
- **Spring Boot Actuator**
- **Spring Boot Testing (MockMvc, @SpringBootTest)**

### 🔹 **Spring Data JPA**

- **Core JPA annotations (Entity, Table, Column) & Mapping**

  - `@Entity`, `@Table`, `@Id`, `@GeneratedValue`

    - `@Entity`: Marks a class as an entity that is mapped to a database table.
    - `@Table`: Specifies the table name for the entity.
    - `@Id`: Marks a field as a primary key.
    - `@GeneratedValue`: Provides the generation strategy for the primary key.

  - Field mappings: `@Column`, `@Transient`, `@Enumerated`, `@Lob`
    - `@Column`: Specifies the column name, length, nullable, etc.
    - `@Transient`: Marks a field as not persistent.
    - `@Enumerated`: Maps an enum type to a database column.
    - `@Lob`: Maps a large object to a database CLOB or BLOB.
  - Relationship mappings: `@OneToOne`, `@OneToMany`, `@ManyToOne`, `@ManyToMany`
  - `cascade`, `fetch`, `mappedBy` in relationships

    - `cascade`: Specifies the operations that should be cascaded to the target of the association.
    - `fetch`: Specifies the fetching strategy (lazy or eager).
    - `mappedBy`: Specifies the field that owns the relationship (inverse side).

  - Lazy vs. Eager fetching (`FetchType.LAZY` vs. `FetchType.EAGER`)
    - Lazy fetching: Loads the related entities only when they are accessed. Default for `@ManyToOne` and `@OneToMany`.
    - Eager fetching: Loads the related entities immediately with the parent entity. Default for `@OneToOne` and `@ManyToMany`.

- **Spring Data Repositories & Query Method**

  - `JpaRepository` vs. `CrudRepository`
    - `JpaRepository`: Extends `PagingAndSortingRepository` and provides additional JPA-related methods.
    - `CrudRepository`: Provides CRUD operations (save, findById, findAll, delete, etc.).
  - Custom query methods (`findBy`, `existsBy`, `countBy`)
  - JPQL (`@Query`) vs. Native Queries
    - JPQL: Java Persistence Query Language (object-oriented query language) => used object entity and field name => used for any database
    - Native Queries: SQL queries (database-specific), use @Query(nativeQuery = true) => used for specific database
  - Pagination & Sorting (`Pageable`, `Sort`)
    - `Pageable`: Represents a page request (page number, page size, sort).
    - `Sort`: Represents sorting information (field, direction).

- **Transactions & Lifecycle Events**
  - `@Transactional` annotation and `propagation levels`
    - `@Transactional`: Marks a method as transactional.
    - Propagation levels: Defines the transaction propagation behavior.
      - `REQUIRED`: Use the existing transaction, create a new one if none exists.
      - `REQUIRES_NEW`: Create a new transaction, suspend the existing one if exists.
      - `NESTED`: Create a nested transaction if a current transaction exists.
      - `SUPPORTS`: Use the existing transaction, execute non-transactionally if none exists.
      - `NOT_SUPPORTED`: Execute non-transactionally, suspend the existing transaction if exists.
      - `NEVER`: Execute non-transactionally, throw an exception if a transaction exists.
  - `@PrePersist`, `@PostPersist`, `@PreUpdate`, `@PostUpdate`
    - `@Pre
    - Persist`: Executed before an entity is saved to the database.
    - Update`: Executed before an entity is updated in the database.
    - `@Post
    - Persist`: Executed after an entity is saved to the database.
    - Update`: Executed after an entity is updated in the database.

### 🔹 **Spring Security**

- **Authentication vs Authorization**
- **JWT & OAuth2**
- **Spring Security Filters & Custom Filters**
- **Password Hashing (BCrypt, Argon2)**
- **RBAC (Role-Based Access Control)**

---

## **📌 Microservices**

- **Monolith vs Microservices**
- **Inter-Service Communication (REST, gRPC, Messaging)**
- **Service Discovery (Eureka, Consul)**
- **Load Balancing (Ribbon, Spring Cloud LoadBalancer)**
- **Circuit Breaker (Resilience4J, Hystrix)**
- **API Gateway (Spring Cloud Gateway, Kong, Nginx)**
- **Distributed Tracing (Zipkin, OpenTelemetry)**
- **Event-Driven Architecture (Kafka, RabbitMQ)**

---
