#Exercises
We will use the "mflix" dataset to solve the exercises.  
[This is a user manual of mflix.](https://docs.atlas.mongodb.com/sample-data/sample-mflix/)

(On command line)
```bash
use mflix
```

##Find

### Examples
_Find all movies of type = movie_
```js
db.movies.find({type:'movie'})
```
_Find all movies of array directors contains item with Auguste Lumière _
```js
db.movies.find({directors:"Auguste Lumière"})
```

1. _Find all movies of array directors contains item with Auguste Lumière and Louis Lumière_

1. _Find all teathers on "Bloomington" city_ 

1. _Find all teathers on "Bloomington" city. Returns id and theaterId_

1. _Find all comments of movie called "Pauvre Pierrot"._

1. _Look for movies from the first half of the 19th century_

1. _Find the oldest movie_

##Count
¬¬  
_Find all movies of type = movie_
```js
db.movies.find({type:'movie'}).count()
```
_Find all movies of array directors contains item with Auguste Lumière _
```js
db.movies.find({directors:"Auguste Lumière"}).count()
```

1. _Find number of teathers on "Bloomington" city_ 

1. _Find number of comments of movie called "Pauvre Pierrot". _


##Aggregation
Example
* _Find repeated movies (titles) on list and return from max number of concurrence to min._
 
```js

[
{"$group" : {_id:"$title", 'counter':{$sum:1}}},
{'$match':{'counter':{"$gte":2}}},
{'$sort':{'counter':-1}}
]

```

1. _Find counts of comments by movies. Returns only with movie has more than 5 comments_

1. _Find number of teathers in minessota (MN)._

1. _Find the name of the person who make more comments._

1. _Find the number of movies from the second half of the 19th century_

1. _Find all comments of movie called "The Story of the Kelly Gang".
Returns only the name of user_




