<h1> MongoDB Cheet Sheet</h1>

<h2> CRUD operations</h2>

| Query            | Details| Reference |
| :---------------- | :------: | ----: |

<h2> Associate Developer Exam Study Notes </h2>

<h4> Reference </h4>

* [Curriculum](https://learn.mongodb.com/learn/course/mongodb-associate-developer-exam-study-guide/main/associate-dba-exam-study-guide?client=customer)

<h4> MONGODB OVERVIEW AND THE DOCUMENT MODEL </h4>

| Nr             | Topic| Notes | Reference |
| :------| :------ |:---- | :----------------|
| 1 | Identify the set of value types MongoDB BSON supports | | [BSON Types](https://www.mongodb.com/docs/manual/reference/bson-types/)|
| 2 | Given three documents that are of different shape, identify which can co-exist in the same collection | **Technical constraints** </br> - Documents Exceeding Size Limits (16 MB) </br>- Non-Unique `_id` Values </br>- Schema Validation Rules (if defined) </br>- Documents with Circular References </br>- Invalid Field Names ($, .) </br>- Field Values of Unsupported BSON Types (i.e functions) </br>- Documents with Reserved Field Names in System Collections
|
