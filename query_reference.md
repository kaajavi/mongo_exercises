# Query REFERENCE

## Select All Documents in a Collection
db.films.find( {} )

## Specify Equality Condition

To specify equality conditions, use <field>:<value> expressions in the query filter document:
 > `{ <field1>: <value1>, ... }`

#### Specify Conditions Using Query Operators
 > `{ <field1>: { <operator1>: <value1> }, ... }`

#### Specify AND Conditions
A compound query can specify conditions for more than one field in the collection’s documents. Implicitly, a logical AND conjunction connects the clauses of a compound query so that the query selects the documents in the collection that match all the conditions.

 >`db.customers.find({'First Name':'MARY', 'Last Name':'SMITH'})`

#### Specify OR Conditions
Using the **$or** operator, you can specify a compound query that joins each clause with a logical OR conjunction so that the query selects the documents in the collection that match at least one condition.

 > `db.films.find( { $or: [ { Category: "Documentary" }, { Rating: { $lt: 30 } } ] } )`

#### Specify AND as well as OR Conditions
In the following example, the compound query document selects all documents in the collection where the film Category is Documentary and Length is equals 86 Or  Rating is less than 30.

 > `db.films.find( {Category: "Documentary", $or: [ { Length:'86' }, { Rating: { $lt: 30 } } ] } ) `

### Filter equal
* Example for comparations where  (equals)
 > `db.films.find({Length:86})`

* Example for comparations where  (less than...)
 > `db.films.find({Length: {$lt:86  }})`
* Example for comparations where  (less than or equals ...)
 > `db.films.find({Length: {$lte:86  }})`

* Example for comparations where  (grater than...)
 > `db.films.find({Length: {$gt:86  }})`
* Example for comparations where  (grater than or equals ...)
 > `db.films.find({Length: {$gte:86  }})`


### Filter likes

* Example for where like = 'MARY'  
 >`db.customers.find({'First Name':'MARY'})`

* With where like = "MAR%"  
>`db.customers.find({'First Name':/^MAR/})`

* With where like = "%ARY"    
>`db.customers.find({'First Name':/ARY$/})`

* With where like = "%AR%"  
>`db.customers.find({'First Name':/AR/})`

### In clause

> `db.films.find({Rating: {$in:["G","PG"]}})`

## Return the Specified Fields and the _id Field Only
A projection can explicitly include several fields by setting the <field> to 1 in the projection document. The following operation returns all documents that match the query. In the result set, only the title and, by default, the _id fields return in the matching documents.

 > `db.films.find({Rating: {$in:["G","PG"]}} , {Title:1} )`

If you need remove _id field, setting **_id** to 0:

 > `db.films.find({Rating: {$in:["G","PG"]}} , {Title:1, _id:0} )`


## AGREGATIONS
When you need write an aggregation in mongo db, you need make an query called "pipeline".  

###Pipeline Concept

In UNIX command, shell pipeline means the possibility to execute an operation on some input and use the output as the input for the next command and so on. MongoDB also supports same concept in aggregation framework. There is a set of possible stages and each of those is taken as a set of documents as an input and produces a resulting set of documents (or the final resulting JSON document at the end of the pipeline). This can then in turn be used for the next stage and so on.

Following are the possible stages in aggregation framework −

* __$project__ − Used to select some specific fields from a collection.

* __$match__ − This is a filtering operation and thus this can reduce the amount of documents that are given as input to the next stage.

* __$group__ − This does the actual aggregation as discussed above.

* __$sort__ − Sorts the documents.

* __$skip__ − With this, it is possible to skip forward in the list of documents for a given amount of documents.

* __$limit__ − This limits the amount of documents to look at, by the given number starting from the current positions.

* __$unwind__ − This is used to unwind document that are using arrays. When using an array, the data is kind of pre-joined and this operation will be undone with this to have individual documents again. Thus with this stage we will increase the amount of documents for the next stage.

### Example

