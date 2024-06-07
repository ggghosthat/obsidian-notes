## Brief theory

NoSQL is a concept in database design that enables the storage and querying of data outside the traditional structures found in relational databases. 

Instead of the typical structure of a relational database, NoSQL databases, house data within one data structure, such as JSON document. Since this non-relational database design does not require a schema, it offers rapid scalability to manage large and typically unstructured data sets.

NoSQL is also type of distributed database, which means that information is copied and stored on various servers, which can be remote or local. This ensure availability and reliability of data. If some of data goes offline, the rest of the database can continue to run.

Main purpose of SQL is a retrieving  specific data from a database. In old day database management systems (DBMS) enabled users to organize large quantities of data. However, they were too much complex, often proprietary to particular app, and limited in the ways in which they could uncover within the data. These limitation led to the development of relational database management systems, which arrange data in tables. SQL provided an interface to interact with relation data, allowing analysts to connect tables by merging on common fields.

## Types of NoSQL databases

A NoSQL database manages information using any of these primary data models:

#### ==Key-value store==
The most simplest type of data organization in NoSQL databases is Key-Value pair. Where key like in relational databases store Id of instance and value value column store rest of instance's fields. For example, in Key column we can store cart Id, while the value is an array of data, like each individual item in that user's shopping cart. Commonly used for caching and storing user session information, such as shopping carts, but not ideal to put multiple records at a time.
**Redis** and **Memcached** are examples of an open source key-value database.
#### ==Document store==
Document databases are inherently subclass of NoSQL databases. Difference lies in the way of data is processed in key-value store, the data is considered as inherently opaque to the database, whereas a document database engine uses for further optimization.  Document databases have a contrast with the traditional relation databases. Relational databases store data in separate tables, which are defined by the programmer, and single object may be spread across several tables. Document database store all of a given information in a single instance of the database.  
Documents might be represented in JSON, BSON (MongoDB) or XML formats. It is gain more flexibilities than simple key-store databases, since data schemas do no need to match across document (e.g. `name` vs `first_name`). However 
#### ==Wide-column store==
This database type stores information in columns, enabling users to access only the specific columns they need without allocating additional memory on irrelevant data. This database tries to solve for the shortcomings of key-value and document stores, but since it can be more complex system to manage, it is not recommended for use for newer teams and projects. `Apache Cassandra` and `HBase` are examples of open-source, wide-column databases.
#### ==Graph store==
This type of database typically houses data from a knowledge of graph theorem. Data elements are stored as nodes, edges and properties. Any object, place or person can be a node. An edge defines the relationship between the nodes. For example, a node could be a client, like `John` , and agency like `Shopify`. An edge would be categorize the relationship as a customer relationship between `Shopify` and `John`. 
Graph databases are used for storing and managing a network of connections between elements within the graph. As an example of graph database there is `Neo4j`.

#### ==In-memory store==
This type of database resides data in main memory rather than on disk, increasing speed of data accession.

