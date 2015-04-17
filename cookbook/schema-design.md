Schema Design  
====================================

The bad news is that  schema design totally depends on the kind of application you're going to build, so it totally varies.

Furthermore, because Mongo is denormalized, we're not going to go through [database normalization](http://en.wikipedia.org/wiki/Database_normalization), meaning there aren't any formal schemas like [First Normal Form (1NF)](http://en.wikipedia.org/wiki/First_normal_form) or [Second Normal Form (2NF)](http://en.wikipedia.org/wiki/Second_normal_form). So, toss everything you know about 1NF and 2NF and keeping data DRY out the window.  

However, the good news is that we **do** have a whole bunch of tools from the field of [cladistics](http://en.wikipedia.org/wiki/Cladistics) at our disposal for analyzing tree structures (which JSON records are structured as), such as [variety.js](https://github.com/variety/variety) and [schema.js](http://skratchdot.com/projects/mongodb-schema/).  If you've never studied cladistics...  well, lets just say that there is a *lot* of math behind the branching of trees, and they're very well known algorithms.  It's an entire area of study from the field of biology.  So plenty of things to learn!


#### Reference Materials
For more details, I highly recommend the following article on NoSQL data modeling techniques:  
[NoSQL Data Modeling Techniques](http://highlyscalable.wordpress.com/2012/03/01/nosql-data-modeling-techniques/)   
[MongoDB Applied Design Patterns](http://www.amazon.com/MongoDB-Applied-Design-Patterns-Copeland/dp/1449340040/ref=sr_1_3?s=books&ie=UTF8&qid=1409761891&sr=1-3&keywords=mongodb)  


####General Design Considerations  
Instead of relying on formal schemas, I'm just going to share some experience on how I go about designing *my* collection schemas, having worked with document oriented database for some 10 odd years.  So, here are few guidelines I use nowdays when designing data storage collections:

1.  Don't do data modeling in the collection schemas.  
2.  Do a careful analysis of the most commonly used queries in your application instead.   
3.  Collection schemas should be designed for optimizing server/client communications.  
4.  Therefore, collections should reflect the types of queries the application is going to perform.  
5.  If its not worth storing a billion records, odds are that it doesn't actually need to be a collection.  
6.  Collections with records containing only 2 or 3 fields are suspicious in the Mongo world.  
7.  As are collections with only a dozen records.  
8.  The exception are collections that contain unique configuration information.
9.  If a table is so small it can be converted into an enum, do so.    
10.  Consolidate and merge tables when possible.  
11.  Think in terms of document schemas, rather than table schemas.  
12.  Collections schemas should be about performance.  
13.  Document schemas are where you want to do your data modeling.  

####Antipatterns
1.  Importing normalized SQL schemas directly into Mongo.
2.  Appending to arrays ad infinitum.

####MongoDB 6 Rules of Thumb
[6 Rules of Thumb for MongoDB Schema Design: Part 1](http://blog.mongodb.org/post/87200945828/6-rules-of-thumb-for-mongodb-schema-design-part-1)  
[6 Rules of Thumb for MongoDB Schema Design: Part 2](http://blog.mongodb.org/post/87892923503/6-rules-of-thumb-for-mongodb-schema-design-part-2)  
[6 Rules of Thumb for MongoDB Schema Design: Part 3](http://blog.mongodb.org/post/88473035333/6-rules-of-thumb-for-mongodb-schema-design-part-3)  

####Naming Conventions  
And here are a few rules of thumb for database field naming conventions.  

1.  Use camelCase or snake_case.  
2.  Don't use dot notation in your field names!  
3.  SmallTalk style type suffixes can be quite useful.  
4.  But don't go overboard with Hungarian notation prefixes.

````js
  // this naming convention works well
  user_id  
  user_key  
  user_tag
  
  // as does this
  userId  
  userKey  
  userTag
  userName
````

snake_case is better if you're new to Meteor, and want a clear distinction between the database layer and application layer.  cameCase is better if you're a little more experienced, and want to be clever with dynamically generating templates and object attributes.  


