# SQLAndMongoQuestions

# SQL:

-> JOINS:
  1.  INNER JOIN: Common between tables
  2.  LEFT JOIN: Common + left
  3.  RIGHT JOIN: Common + right
  4.  OUTER JOIN: All

  Simple join query:
  ```
  SELECT * FROM ORDERS
  INNER JOIN CUSTOMER
  ON ORDER.CUSTOMERID = CUSTOMER.CUSTOMERID;
  ```

-> DELETE, DROP & TRUNCATE:
  1.  DELETE: Delete one or more rows.
  2.  DROP: This will delete the whole table and schema
  3.  TRUNCATE: This will remove all the data from the table only 

-> Second Highest Salary Query: 
  ```
  SELECT * FROM EMPLOYEE ORDER BY SAL DESC LIMIT 2 OFFSET 1;
  LIMIT: Will hold first 2
  OFFSET: Will remove the first
  ```

# MongoDB:

-> Basic Mongo Aggregate Query:

```
db.paymentTransfer.aggregate([
  {
    $match : {"transferReference" : "XYZ"} //find as per match
  },

  {
    $limit : 3 // fetch only 3
  },

  {
    $skip : 2 //skip first 2 records
  },

  {
    $lookup : { // use to join to different collection
      from : "event",
      localField : "transferReference",
      forignField : "serialKeys"
      as : "event"
    }
  },

  {
    $unwind : { // once lookup is done, it will add another attribute of array, and we need to unwind that
      "path" : "$event",
      "preserveNullAndEmptyArrays" : false
    }
  },

  {
    $sort : {"event.createdTime" : -1} // sort the jsons as per attribute [(-1 - Decending, 1 - Ascending)]
  }

])
```
-> Basic Mongo Find Query:

```
db.paymentTransfer.find({"transferReference" : "XYZ"})
```
