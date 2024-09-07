# Collections Methods (CRUD)

## Insert Operations
    
### **insertOne()**

The **`insertOne()`** method is used to insert a single document into a collection. This method returns an **`InsertOneResult`** object, that shows the outcome of the operation.

**Syntax:**

```jsx
db.collection.insertOne(   
    <document>,   
    {      
        writeConcern: <document>,      
        ordered: <boolean>,      
        bypassDocumentValidation: <boolean>,      
        comment: <any>   
    }
)
```

**Options:**

- `writeConcern:` An optional document specifying the level of acknowledgment requested from MongoDB for the write operation.
- `ordered:` An optional boolean flag. When set to `true`, MongoDB will return an error if it encounters a duplicate document in the operation. Default is also `true`.
- `bypassDocumentValidation:` Optional boolean flag. To validate or not to validate the document against the collection’s validation rules. Default is `false`.
- `comment:` An optional string or BSON that can be used for descriptive purposes when profiling operations.

**Example:**

```
db.inventory.insertOne({  item: 'book',  qty: 1,});
```

### **insertMany()**

The **`insertMany()`** method is used to insert multiple documents into a collection at once. It returns an **`InsertManyResult`** object, displaying the status of the operation.

**Syntax:**

```
db.collection.insertMany(   [ <document_1>, <document_2>, ... ],   {      writeConcern: <document>,      ordered: <boolean>,      bypassDocumentValidation: <boolean>,      comment: <any>   })
```

**Options:**

- `writeConcern:` Same as mentioned in `insertOne()` method.
- `ordered:` Same as mentioned in `insertOne()` method. When set to `true`, MongoDB will insert the documents in the array’s order. If a fail occurs, it will stop further processing of the documents. Default is `true`.
- `bypassDocumentValidation:` Same as mentioned in `insertOne()` method.
- `comment:` Same as mentioned in `insertOne()` method.

**Example:**

```
db.inventory.insertMany([  { item: 'pen', qty: 5 },  { item: 'pencil', qty: 10 },  { item: 'notebook', qty: 25 },]);
```
    
## Find
the **`find()`** method is an essential aspect of working with collections. It enables you to search for specific documents within a collection by providing query parameters. In this section, we’ll explore various **`find`** methods and how to filter, sort, and limit the search results.

### Basic Find Method

The basic **`find()`** method is used to fetch all documents within a collection. To use it, you’ll simply call the **`find()`** method on a collection.

```
db.collection_name.find();
```

For example, to fetch all documents from a collection named **`users`**:

```
db.users.find();
```

### Query Filters

To search for specific documents, you would need to supply query parameters as a filter within the **`find()`** method. Filters are passed as JSON objects containing key-value pairs that the documents must match.

For example, to fetch documents from the **`users`** collection with the **`age`** field set to **`25`**:

```
db.users.find({ age: 25 });
```

### Logical Operators

MongoDB provides multiple logical operators for more advanced filtering, including **`$and`**, **`$or`**, and **`$not`**. To use logical operators, you pass an array of conditions.

For example, to find users with an age of **`25`** and a first name of **`John`**:

```
db.users.find({ $and: [{ age: 25 }, { first_name: 'John' }] });
```

### Projection

Projection is used to control which fields are returned in the search results. By specifying a projection, you can choose to include or exclude specific fields in the output.

To only include the **`first_name`** and **`age`** fields of the matching documents:

```
db.users.find({ age: 25 }, { first_name: 1, age: 1 });
```

### Sorting

You can also sort the results of the **`find()`** method using the **`sort()`** function. To sort the results by one or multiple fields, pass a JSON object indicating the order.

For example, to sort users by their age in ascending order:

```
db.users.find().sort({ age: 1 });
```

### Limit and Skip

To limit the results of the **`find()`** method, use the **`limit()`** function. For instance, to fetch only the first **`5`** users:

```
db.users.find().limit(5);
```

Additionally, use the **`skip()`** function to start fetching records after a specific number of rows:

```
db.users.find().skip(10);
```

All these **`find`** methods combined provide powerful ways to query your MongoDB collections, allowing you to filter, sort, and retrieve the desired documents.
    
## Update    
`update` methods are used to modify the existing documents of a collection. They allow you to perform updates on specific fields or the entire document, depending on the query criteria provided. Here is a summary of the most commonly used update methods in MongoDB:

- **updateOne()**: This method updates the first document that matches the query criteria provided. The syntax for updateOne is:
    
    ```
    db.collection.updateOne(<filter>, <update>, <options>)
    ```
    
    - `<filter>`: Specifies the criteria for selecting the document to update.
    - `<update>`: Specifies the modifications to apply to the selected document.
    - `<options>`: (Optional) Additional options to configure the behavior of the update operation.
- **updateMany()**: This method updates multiple documents that match the query criteria provided. The syntax for updateMany is:
    
    ```
    db.collection.updateMany(<filter>, <update>, <options>)
    ```
    
    - `<filter>`: Specifies the criteria for selecting the documents to update.
    - `<update>`: Specifies the modifications to apply to the selected documents.
    - `<options>`: (Optional) Additional options to configure the behavior of the update operation.
- **replaceOne()**: This method replaces a document that matches the query criteria with a new document. The syntax for replaceOne is:
    
    ```
    db.collection.replaceOne(<filter>, <replacement>, <options>)
    ```
    
    - `<filter>`: Specifies the criteria for selecting the document to replace.
    - `<replacement>`: The new document that will replace the matched document.
    - `<options>`: (Optional) Additional options to configure the behavior of the replace operation.

### Update Operators

MongoDB provides additional update operators to specify the modifications like **`$set`**, **`$unset`**, **`$inc`**, **`$push`**, **`$pull`**, and more. Here are a few examples:

- Use **`$set`** operator to update the value of a field:
    
    ```
    db.collection.updateOne({ name: 'John Doe' }, { $set: { age: 30 } });
    ```
    
- Use **`$inc`** operator to increment the value of a field:
    
    ```
    db.collection.updateMany({ status: 'new' }, { $inc: { views: 1 } });
    ```
    
- Use **`$push`** operator to add an item to an array field:
    
    ```
    db.collection.updateOne({ name: 'Jane Doe' }, { $push: { tags: 'mongodb' } });
    ```
    

Remember to thoroughly test your update operations to ensure the modifications are done correctly, and always backup your data before making any substantial changes to your documents.
    
## Delete
When working with MongoDB, you will often need to delete documents or even entire collections to manage and maintain your database effectively. MongoDB provides several methods to remove documents from a collection, allowing for flexibility in how you choose to manage your data. In this section, we will explore key delete methods in MongoDB and provide examples for each.

### db.collection.deleteOne()

The **`deleteOne()`** method is used to delete a single document from a collection. It requires specifying a filter that selects the document(s) to be deleted. If multiple documents match the provided filter, only the first one (by natural order) will be deleted.

Syntax: **`db.collection.deleteOne(FILTER)`**

Example:

```
db.users.deleteOne({ firstName: 'John' });
```

This command will delete the first **`users`** document found with a **`firstName`** field equal to **`"John"`**.

### db.collection.deleteMany()

The **`deleteMany()`** method is used to remove multiple documents from a collection. Similar to **`deleteOne()`**, it requires specifying a filter to select the documents to be removed. The difference is that all documents matching the provided filter will be removed.

Syntax: **`db.collection.deleteMany(FILTER)`**

Example:

```
db.users.deleteMany({ country: 'Australia' });
```

This command will delete all **`users`** documents with a **`country`** field equal to **`"Australia"`**.

### db.collection.remove()

The **`remove()`** method can be used to delete documents in a more flexible way, as it takes both a filter and a **`justOne`** option. If **`justOne`** is set to true, only the first document (by natural order) that matches the filter will be removed. Otherwise, if **`justOne`** is set to false, all documents matching the filter will be deleted.

Syntax: **`db.collection.remove(FILTER, JUST_ONE)`**

Example:

```
db.users.remove({ age: { $lt: 18 } }, true);
```

This command would delete a single user document with an **`age`** field value less than 18.

### db.collection.drop()

In cases where you want to remove an entire collection, including the documents and the metadata, you can use the **`drop()`** method. This command does not require a filter, as it removes everything in the specified collection.

Syntax: **`db.collection.drop()`**

Example:

```
db.users.drop();
```

This command would delete the entire **`users`** collection and all related data.

<aside>
💡 It’s important to note that these methods will remove the affected documents permanently from the database, so use caution when executing delete commands. Keep in mind to keep backups or use version control to maintain data integrity throughout the lifecycle of your MongoDB database.

</aside>
    
## BulkWrite
### bulkWrite() and others

Bulk write operations allow you to perform multiple create, update, and delete operations in a single command, which can significantly improve the performance of your application. MongoDB provides two types of bulk write operations:

- **Ordered Bulk Write**: In this type of bulk operation, MongoDB executes the write operations in the order you provide. If a write operation fails, MongoDB returns an error and does not proceed with the remaining operations.
- **Unordered Bulk Write**: In this type of bulk operation, MongoDB can execute the write operations in any order. If a write operation fails, MongoDB will continue to process the remaining write operations.

To perform a bulk write operation, use the **`initializeOrderedBulkOp()`** or **`initializeUnorderedBulkOp()`** methods to create a bulk write object.

#### Example: Ordered Bulk Write

Here’s an example of an ordered bulk write operation:

```jsx
const orderedBulk = db.collection('mycollection').initializeOrderedBulkOp();

orderedBulk.insert({ _id: 1, name: 'John Doe' });
orderedBulk.find({ _id: 2 }).updateOne({ $set: { name: 'Jane Doe' } });
orderedBulk.find({ _id: 3 }).remove();
orderedBulk.execute((err,result) => {  
    // Handle error or result
});
```

#### Example: Unordered Bulk Write

Here’s an example of an unordered bulk write operation:

```jsx
const unorderedBulk = db.collection('mycollection').initializeUnorderedBulkOp();

unorderedBulk.insert({ _id: 1, name: 'John Doe' });
unorderedBulk.find({ _id: 2 }).updateOne({ $set: { name: 'Jane Doe' } });
unorderedBulk.find({ _id: 3 }).remove();

unorderedBulk.execute((err, result) => {
    // Handle error or result
});
```

Remember that using bulk write operations can greatly improve the performance of your MongoDB queries, but make sure to choose the right type (ordered or unordered) based on your application requirements.