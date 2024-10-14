<h1> MongoDB Cheet Sheet</h1>

<img width="1000" alt="Screenshot 2024-10-14 at 22 40 40" src="https://github.com/user-attachments/assets/b8cece98-84f9-4a10-9554-7cf8ca731f1d">

<h2> Associate Developer Exam Study Notes </h2>

<h4> Reference </h4>

* [Curriculum](https://learn.mongodb.com/learn/course/mongodb-associate-developer-exam-study-guide/main/associate-dba-exam-study-guide?client=customer)

<h4> 1. MONGODB OVERVIEW AND THE DOCUMENT MODEL </h4>

| Nr             | Topic| Notes &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  | Reference |
| :------| :------ |:---- | :----------------|
| 1 | Identify the set of value types MongoDB BSON supports | - Extension of JSON </br> - Optimized for storage, retrieval, and transmission across the wire </br> -  More secure than plaintext JSON </br> - Supports more data types than JSON </br> **Example** </br> - String </br> - `int32, int64`</br> | [BSON Types](https://www.mongodb.com/docs/manual/reference/bson-types/)|
| 2 | Given three documents that are of different shape, identify which can co-exist in the same collection | **Technical constraints** </br> - Documents Exceeding Size Limits (16 MB) </br>- Non-Unique `_id` Values </br>- Schema Validation Rules (if defined) </br>- Documents with Circular References </br>- Invalid Field Names ($, .) </br>- Field Values of Unsupported BSON Types (i.e functions) </br>- Documents with Reserved Field Names in System Collections


<h4> 2. CRUD </h4>

| Nr             | Topic| Notes &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  | Reference |
| :------| :------ |:---- | :----------------|
2.1 |Given a scenario with a type of structured document that needs to be inserted into a database, identify properly and improperly formed insert commands. ||- [Insert One](https://www.mongodb.com/docs/manual/reference/method/db.collection.insertOne) /</br> - [Insert Many](https://www.mongodb.com/docs/manual/reference/method/db.collection.insertMany/)|
2.2 |Given an update scenario where an entire updated document (no update operators used) is provided, identify the output and how the database changed state.
2.3 |Given an update scenario where $set is used, identify the output and how the database changed state. |- `$set` adds or modifies fields in the pipeline </br> - `db.col.updateOne({<filter>}, {<update>}, {options})` </br> -`{ $set: { <field1>: <value1>, ... } }` </br> - `db.products.updateOne({ _id: 100 }, { $set: { "details.make": "Kustom Kidz" }  })` </br> - updates the value second element (array index of 1) in the tags field `"tags.1"` </br> - the rating field in the first element (array index of 0) of the ratings array `"ratings.0.rating"` | - [$set](https://www.mongodb.com/docs/manual/reference/operator/update/set/?_ga=2.56665699.810066485.1665291537-836515500.1666025886) </br> -[updateMany](https://www.mongodb.com/docs/manual/reference/method/db.collection.updateMany/) </br> - [Update operator expressions](https://www.mongodb.com/docs/manual/reference/method/db.collection.updateOne/#std-label-updateOne-behavior-update-expressions)| 
2.4 |Given a scenario about updating a document and information about where it should be inserted if it does not exist, identify the upsert command that should be used.
2.5 |Given a scenario where multiple documents need to be updated, identify the correct update expression.
2.6 |Given a findAndModify scenario where another operation is run concurrently, identify the output and how the database changed state.|Updates and returns a single document </br> `db.collection.findAndModify({ </br>query: <document>, sort: <document>,remove: <boolean>, update: <document or aggregation pipeline>});`|- [findAndModify](https://www.mongodb.com/docs/manual/reference/method/db.collection.findAndModify/?_ga=2.123127490.810066485.1665291537-836515500.1666025886)|
2.7 |Given a scenario where a document should be deleted from the database, identify the delete expression that should be used. |`db.collection.deleteOne(<filter>)` </br> `db.collection.deleteMany(<filter>)` |- [deleteOne](https://www.mongodb.com/docs/v5.3/reference/method/db.collection.deleteOne/) </br> - [deleteMany](https://www.mongodb.com/docs/v5.3/reference/method/db.collection.deleteMany/?_ga=2.23103219.810066485.1665291537-836515500.1666025886)|
2.8 |Given a scenario where a single document should be looked up by a simple equality constraint (eg {x: 3}), identify the expression that should be used. |`db.col.find(<query>, <projection>)`|
2.9 | Identify documents matched by a query with an equality constraint on an array field. |`$match` </br> -Filters for data that matches criteria </br> - Place as early as possible in the pipeline so it can use indexes|
2.10 | Identify documents matched by an expression with relational operators in it.
2.11 | Identify documents matched by an expression with $in. |`db.col.find({  <field>: {$in: [val1, val2, ...]} })` </br> - select all documents that have a field value equal to any of the values specified in the arrav.|
2.12 | Identify documents matched by an $elemMatch expression. |`db.sales.find({ items: { $elemMatch: { name: "laptop", price: { $gt: 800 }, quantity: { $gte: 1 } }, }, })`|find all documents that contain the specified subdocument </br> - [Example](https://learn.mongodb.com/learn/course/mongodb-crud-operations-insert-and-find-documents/lesson-4-querying-on-array-elements-in-mongodb/learn?client=customer&page=2)|
2.13 | Identify documents matched by an expression that has several logical operators. |`db.col.find({ $or: [{<opt1>},{<opt2>}] })` </br>|
2.14 | Given a query with a sort and limit, identify the correct output. |Limits the number of documents that are passed on to the next aggregation stage </br> - Sorts all input documents and passes them through pipeline in sorted order |
2.15  | Identify the incorrect projection among a set of expressions. |Determines output shape </br> - Inclusion & exclusion statements can't be combined in projections </br> - `_id` field is an exception |
2.16  | Identify how to get all results from a cursor. |- **cursor:** pointer to the result set of a query|
2.17  | Identify the expressions used to count the number of documents matching a query. |`db.col.countDocuments({query})`|
2.18  | Given an indexing scenario, identify the correct command for defining a search index.
2.19  | Given a scenario, identify the correct search query.
2.20  | Given an aggregation expression using `$match`, `$group`, identify the correct output. |`{$group:`</br>`{ _id: <expression>, // Group key` </br> `<field1>: { <accumulator1> : <expression1> },`</br> `} }`|- [Group](https://www.mongodb.com/docs/manual/reference/operator/aggregation/group/)|
2.21  | Given an aggregation expression using `$lookup`, identify the correct output.
2.22  | Given an aggregation expression using `$out`, identify the correct output. | Writes the documents that are returned by an aggregation pipeline into a collection - If collection exists, `Sout` replaces the existing collection with new data </br> - Creates a new collection if it does not already exist </br> `$out: { db: "<db>", coll: "<new_collecgtion>" }`|

<h4> 3. Indexes </h4> 

| Nr             | Topic| Notes &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  | Reference |
| :------| :------ |:---- | :----------------|
3.1  | Given a query that is performing a collection scan, identify which index would improve the performance of this query. |- there is one devault index per collection: `_id` </br> - Follow this order: Equality, Sort, Range|
3.2  | Given a query that is performing a collection scan on an equality match on an array field, identify which index would improve the performance of this query. |`db.col.createIndex({fieldname: 1})`</br> `db.col.createIndex({fieldname1: 1}, {unique: true})`|
3.3  | Given a query with no constraint and a sort of two fields that is doing collection scan, identify which index would improve the performance of this query. | **Most common index types** </br> - single field </br> - compound </br> - Multikey indexes operate on an array field |
3.4  | Given a collection, identify how many indexes exist for that collection.|`db.coll.getIndexes()`|
3.5  | Identify the trade-offs of using indexes and the ramifications of deleting indexes support queries |`db.coll.hideIndex('active_1_birthdate_-1_name_1')` </br>`db.coll.hideIndex({active: 1, birthdate: -1, name:1 })`</br>`db.coll.dropIndex('active_1_birthdate_-1_name_1')` </br> **Improve performance**</br> - speed up queries </br> - reduce disk I/O </br> - Reduce resources required </br> - Support equality matches and range-based operations and return sorted results </br> **Without Index** </br> - MongoDB reads all documents (collection scan) </br> - Sorts results in memory </br> **Problems with indexes** </br> - insert or update document: need to update index </br> - Indexes have a write cost.|
3.6  | Identify the explain plan outputs that signify a potential performance issue, specifically whether an index is present or not for the given query.

<h4> 4: DATA MODELING </h4>

| Nr             | Topic| Notes &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  | Reference |
| :------| :------ |:---- | :----------------|
4.1 | Given a scenario with three collections (a parent and two children) and the user, identify the embedded relationships and which should be linked.|  | 
4.2 | Identify data model examples that are considered an anti-pattern | - Massive arrays </br> - Massive number of collections </br> -  Unnecessary indexes  </br> -  Queries without indexes  </br> - Data that's accessed together, but stored in different collections | 



<h4> 6. DRIVERS </h4> 

| Nr             | Topic| Notes &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  | Reference |
| :------| :------ |:---- | :----------------|
| 6.1| Define what the XX driver is?| MongoDB drivers connect our application to our database by using a connection string. | - [Mongo Drivers](https://www.mongodb.com/docs/drivers/)| 
| 6.2  |Define how the XX application connects/uses the XXX driver?| **Python**</br>`mongodb://<db_username>:<db_password>@<hostname>:<port>` </br>**SRV Connection Format** </br> `mongodb+srv://[username:password@]host[/[defaultauthdb][?options]]` </br> - `+srv` indicates to the client that the hostname that follows corresponds to a DNS SRV record. </br>  - The driver or mongosh will then query the DNS for the record to determine which hosts are running the mongod or mongos instances| - [PyMongo reference](https://www.mongodb.com/docs/languages/python/pymongo-driver/current/) </br> - [PyMongo connect](https://www.mongodb.com/docs/languages/python/pymongo-driver/current/connect/#std-label-pymongo-connect) </br> -[Connection String](https://www.mongodb.com/docs/manual/reference/connection-string/#std-label-connections-dns-seedlist)|
| 6.3 |Define the components of the URI string used by MongoClient to connect the driver to the database. |
| 6.4 |Identify what connection pooling is in terms of the driver and what advantages it offers.| - a technique used by the MongoDB driver to manage multiple connections to the database efficiently. Instead of opening and closing a new connection every time a client interacts with the database, the driver maintains a pool of open, reusable connections </br> **Advantages of Connection Pooling** </br> - Reduced Overhead </br> - Efficient Resource Utilization </br> - Increased Throughput: Concurrent Operations </br> - Increased Throughput: Minimizing Blocking  </br> -  Scalability: Handling Multiple Requests </br> -  Scalability: Maximizing Database Resources </br> - Reduced Latency: Faster Query Execution </br> -  Configurable </br> `client = MongoClient("mongodb://localhost:27017", maxPoolSize=50, minPoolSize=10 )`|
|6.5 |Identify the correct syntax for the XX driver to insert one document and to insert many documents.| `db.test.insert_one(document, bypass_document_validation=False, session=None, comment=None)` </br> `db.test.insert_one({'x': 1})` </br> `insert_many(documents, ordered=True, ...)` </br> `db.test.insert_many([{'x': i} for i in range(2)])`| - [Insert](https://www.mongodb.com/docs/languages/python/pymongo-driver/current/write/insert/)|
|6.6 |Identify the correct syntax for the XX driver to update one document and to update many documents. | `db.collection.update_one(<filter>, <update>)` </br> `db.collection.update_many(<filter>, <update>)`| - [Write](https://www.mongodb.com/docs/languages/python/pymongo-driver/current/write-operations/#std-label-pymongo-write)|
|6.7 |Identify the correct syntax for the XX driver to delete one document and to delete many documents. | - `delete_one(<query_filter>)` - delete the first document that matches the search criteria </br> - `delete_many(<query_filter>)` - deletes all documents that match the search criteria | - [Delete](https://www.mongodb.com/docs/languages/python/pymongo-driver/current/write/delete/)|
|6.8 |Identify the correct syntax for the XX driver to find many documents and to find one document.| `xx.find_one({ "<field name>" : "<value>" })`</br> `xx.find()`| - [Find](https://www.mongodb.com/docs/languages/python/pymongo-driver/current/read/#std-label-pymongo-read)| 
|6.9 |Identify the correct syntax for the XX driver to create an aggregation pipeline.| `pipeline = [<stage 1>, <stage 2>]; db.collection.aggregate(pipeline)`|
|6.10| Identify the different syntax for the XX driver when using the MongoDB Query Language (MQL) and when using the Aggregation Framework.|

<h2> Miscellaneous Use Cases </h2>

| Query            | Details| Reference |
| :---------------- | :------ | ----: |
| `db.help()` | get help on general MongoDB commands ||
|`{ <field>: { $regex: /pattern/, $options: '<options>' } }` </br> | Regex expression search| [RegEx](https://www.mongodb.com/docs/manual/reference/operator/query/regex/)|
|**Python** </br> `client = MongoClient(<uri>);`</br>`db = client['my_database'];`</br>`collections = db.list_collection_names()`|List collections in database||

