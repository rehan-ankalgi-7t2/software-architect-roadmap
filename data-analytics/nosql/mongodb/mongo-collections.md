# Collections and Methods

> **collections** are used to organize documents. A collection can be thought of as a container or group used to store documents of similar structure, like a table in relational databases. However, unlike tables, collections don’t enforce a strict schema, offering more flexibility in managing your data.
>

## **Key Features**

- **Flexible Schema**: A collection can contain multiple documents with different structures or fields, allowing you to store unstructured or semi-structured data.
- **Dynamic**: Collections can be created implicitly or explicitly, and documents can be added or removed easily without affecting others in the collection.


### Creating Collections
To create a collection in MongoDB, you can choose from two methods:

- **Implicit Creation**: When you insert a document without specifying an existing collection, MongoDB automatically creates the collection for you.
    
    ```jsx
    db.createCollection('users');
    ```
    
- **Explicit Creation**: Use the **`db.createCollection(name, options)`** method to create a collection with specific options:
    
    ```jsx
    db.createCollection('users', { capped: true, size: 100000, max: 5000 });
    ```
    
### Managing Collections
- **Insert Documents**: To insert a document into a collection, use the **`insertOne()`** or **`insertMany()`** methods.
    
    ```jsx
    db.users.insertOne({ name: 'John Doe', age: 30, email: 'john@example.com' });
    db.users.insertMany([  
        { name: 'Jane Doe', age: 28, email: 'jane@example.com' },
        { name: 'Mary Jane', age: 32, email: 'mary@example.com' },
    ]);
    ```
    
- **Find Documents**: Use the **`find()`** method to query documents in a collection.
    
    ```jsx
    db.users.find({ age: { $gt: 30 } });
    ```
    
- **Update Documents**: Use the **`updateOne()`**, **`updateMany()`**, or **`replaceOne()`** methods to modify documents in a collection.
    
    ```jsx
    db.users.updateOne({ name: 'John Doe' }, { $set: { age: 31 } });
    db.users.updateMany({ age: { $gt: 30 } }, { $inc: { age: 1 } });
    ```
    
- **Delete Documents**: Use the **`deleteOne()`** or **`deleteMany()`** methods to remove documents from a collection.
    
    ```jsx
    db.users.deleteOne({ name: 'John Doe' });
    db.users.deleteMany({ age: { $lt: 30 } });
    ```
    
- **Drop Collection**: To delete the entire collection, use the **`drop()`** method.
    
    ```jsx
    db.users.drop();
    ```

## Counting Documents
When working with MongoDB, you might often need to know the number of documents present in a collection. MongoDB provides a few methods to efficiently count documents in a collection. In this section, we will discuss the following methods:

- `countDocuments()`
- `estimatedDocumentCount()`

## **countDocuments()**

The **`countDocuments()`** method is used to count the number of documents in a collection based on a specified filter. It provides an accurate count that may involve reading all documents in the collection.

**Syntax:**

```jsx
collection.countDocuments(filter, options);
```

- `filter`: (Optional) A query that will filter the documents before the count is applied.
- `options`: (Optional) Additional options for the count operation such as `skip`, `limit`, and `collation`.

**Example:**

```jsx
db.collection('orders').countDocuments(  { status: 'completed' },  (err,count) => {    console.log('Number of completed orders: ', count);  });
```

In the example above, we count the number of documents in the **`orders`** collection that have a**`status`** field equal to **`'completed'`**.

## **estimatedDocumentCount()**

The **`estimatedDocumentCount()`** method provides an approximate count of documents in the collection, without applying any filters. This method uses the collection’s metadata to determine the count and is generally faster than **`countDocuments()`**.

**Syntax:**

```jsx
collection.estimatedDocumentCount(options);
```

- `options`: (Optional) Additional options for the count operation such as `maxTimeMS`.

**Example:**

```jsx
db.collection('orders').estimatedDocumentCount((err,count) => {  console.log('Estimated number of orders: ', count);});
```

In the example above, we get the estimated number of documents in the **`orders`** collection.

Keep in mind that you should use the **`countDocuments()`** method when you need to apply filters to count documents, while **`estimatedDocumentCount()`** should be used when an approximate count is sufficient and you don’t need to apply any filters.

## validate()

The **`validate`** command is used to examine a MongoDB collection to verify and report on the correctness of its internal structures, such as indexes, namespace details, or documents. This command can also return statistics about the storage and distribution of data within a collection.

## **Usage**

The basic syntax of the **`validate`** command is as follows:

```jsx
db.runCommand({validate: "<collection_name>", options...})
```

**`<collection_name>`** is the name of the collection to be validated.

## **Options**

- **`full`**: (default: false) When set to true, the **`validate`** command conducts a more thorough inspection of the collection, looking through all its extents, which are contiguous sections of the collection’s data on disk. This option should be used with caution as it may impact read and write performance.
- **`background`**: (default: false) When set to true, the **`validate`** command runs in the background, allowing other read and write operations on the collection to proceed concurrently. This option is beneficial for large collections, as it minimizes the impact on system performance.

## **Example**

Validate a collection named “products”:

```jsx
db.runCommand({ validate: 'products' });
```

Validate the collection and perform a background and full check:

```jsx
db.runCommand({ validate: 'products', background: true, full: true });
```

## **Output**

The **`validate`** command returns an object that contains information about the validation process and its results.

```jsx
{    
    "ns": <string>, // Namespace of the validated collection    
    "nIndexes": <number>, // Number of indexes in the collection    
    "keysPerIndex": {        
        <index_name>: <number> // Number of keys per index    
    },    
    "valid": <boolean>, // If true, the collection is valid    
    "errors": [<string>, ...], // Array of error messages, if any    
    "warnings": [<string>, ...], // Array of warning messages, if any    
    "ok": <number> // If 1, the validation command executed successfully
}
```

Keep in mind that the **`validate`** command should be used mainly for diagnostics and troubleshooting purposes, as it can impact system performance when validating large collections or when using the **`full`** flag. Use it when you suspect that there might be corruption or discrepancies within the collection’s data or internal structures.