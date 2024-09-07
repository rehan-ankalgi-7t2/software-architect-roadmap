# **What is MongoDB**

> MongoDB is an open-source, document-based, and cross-platform NoSQL database that offers high performance, high availability, and easy scalability. It differs from traditional relational databases by utilizing a flexible, schema-less data model built on top of BSON (Binary JSON), allowing for non-structured data to be easily stored and queried.
>

## **Key Features of MongoDB**

- **Document-oriented**: MongoDB stores data in JSON-like documents (BSON format), meaning that the data model is very flexible and can adapt to real-world object representations easily.
- **Scalability**: MongoDB offers automatic scaling, as it can be scaled horizontally by sharding (partitioning data across multiple servers) and vertically by adding storage capacity.
- **Indexing**: To enhance query performance, MongoDB supports indexing on any attribute within a document.
- **Replication**: MongoDB provides high availability through replica sets, which are primary and secondary nodes that maintain copies of the data.
- **Aggregation**: MongoDB features a powerful aggregation framework to perform complex data operations, such as transformations, filtering, and sorting.
- **Support for ad hoc queries**: MongoDB supports searching by field, range, and regular expression queries.

## **When to use MongoDB**

MongoDB is a suitable choice for various applications, including:

- **Big Data**: MongoDB’s flexible data model and horizontal scalability make it a great fit for managing large volumes of unstructured or semi-structured data.
- **Real-time analytics**: MongoDB’s aggregation framework and indexing capabilities help analyze and process data in real-time.
- **Content management**: With its dynamic schema, MongoDB can handle diverse content types, making it a suitable choice for content management systems.
- **Internet of Things (IoT) applications**: MongoDB can capture and store data from a large number of devices and sensors, proving beneficial in IoT scenarios.
- **Mobile applications**: MongoDB provides a flexible data model, which is an essential requirement for the dynamic nature and varying data types of mobile applications.

## Mongo DB basics

MongoDB is a popular NoSQL database system that stores data in Flexible JSON-like documents, making it suitable for working with large scale and unstructured data.

- **Database**: Stores all your collections within a MongoDB instance.
- **Collection**: A group of related documents, similar to a table in a relational database.
- **Document**: A single record within a collection, which is stored as BSON (Binary JSON) format.
- **Field**: A key-value pair within a document.
- **_id**: A unique identifier automatically generated for each document within a collection.

### **Basic Operations**

- **Insert**: To insert a single document, use `db.collection.insertOne()`. For inserting multiple documents, use `db.collection.insertMany()`.
- **Find**: Fetch documents from a collection using `db.collection.find()`, and filter the results with query criteria like `{field: value}`. To fetch only one document, use `db.collection.findOne()`.
- **Update**: Update fields or entire documents by using update operators like `$set` and `$unset` with `db.collection.updateOne()` or `db.collection.updateMany()`.
- **Delete**: Remove documents from a collection using `db.collection.deleteOne()` or `db.collection.deleteMany()` with query criteria.
- **Drop**: Permanently delete a collection or a database using `db.collection.drop()` and `db.dropDatabase()`.

### **Indexes and Aggregations**

- **Indexes**: Improve the performance of searches by creating indexes on fields within a collection using `db.collection.createIndex()` or build compound indexes for querying multiple fields.
- **Aggregations**: Perform complex data processing tasks like filtering, grouping, transforming, and sorting using aggregation operations like `$match`, `$group`, `$project`, and `$sort`.

### **Data Modeling**
boiler plate code for data model using nodejs and mongoose

```javascript
import mongoose from 'mongoose';

const orderSchema = mongoose.Schema({}, { timestamps: true });

export const Order = mongoose.model('Order', orderSchema);
```

data modelling practice code repo:

MongoDB’s flexible schema allows for various data modeling techniques, including:

- **Embedded Documents**: Store related data together in a single document, which is suitable for one-to-one or one-to-few relationships.
- **Normalization**: Store related data in separate documents with references between them, suitable for one-to-many or many-to-many relationships.
- **Hybrid Approach**: Combine embedded documents and normalization to balance performance and storage needs.

In conclusion, MongoDB’s flexible and feature-rich design makes it a powerful choice for modern applications dealing with large scale and unstructured data. Understanding the basics of MongoDB can help you effectively use it as your data storage solution.

## Mongo DB Terminology
| Term | Defination / Description |
| --- | --- |
| Database | A MongoDB database is used to store and manage a set of collections. It consists of various collections, indexes, and other essential data structures required to store the data efficiently. |
| collection | A collection in MongoDB is a group of documents. The name of a collection must be unique within its database. Collections can be viewed as the table equivalencies in a relational database. |
| Document | A document is a record in a MongoDB collection. It is comprised of a set of fields, similar to a row in a relational database. However, unlike tables in a relational database, no schema or specific structure is enforced on the documents within a collection. |
| Field | A field in MongoDB is a key-value pair inside a document. It can store various types of data, including strings, numbers, arrays, and other documents. Fields in MongoDB can be seen as columns in a relational database. |
| Index | Indexes in MongoDB are data structures that improve the speed of common search operations. They store a small portion of the dataset in a well-organized structure. This structure allows MongoDB to search and sort documents faster by reducing the number of documents it has to scan. |
| query | A query in MongoDB is used to retrieve data from the database. It retrieves specific documents or subsets of documents from a collection based on a given condition. |
| Cursor | A cursor is a pointer to the result set of a query. It allows developers to process individual documents from the result set in an efficient manner. |
| Aggregation | Aggregation in MongoDB is the process of summarizing and transforming the data stored in collections. It is used to run complex analytical operations on the dataset or create summary reports. |
| Replica Set | A replica set in MongoDB is a group of mongodb instances that maintain the same data set. It provides redundancy, high availability, and automatic failover in case the primary node becomes unreachable. |
| Sharding | • Sharding is a method of distributing data across multiple machines. It is used in MongoDB to horizontally scale the database by partitioning the dataset into smaller, more manageable chunks called shards. |

## Data Types

- String
- Array
- Object
- Binary data
- ObjectId
- Undefined
- boolean
- Date
- null
- Regular expression
- Javascript
- Symbol
- Int 32 / Int
- Int 64 / long
- Timestamp
- Decimal 128
- Min Key
- Max Key

