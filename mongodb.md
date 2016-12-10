##Mongo Database Basics. As of Mongo version 3.4.1
* Install mongodb ```brew install mongodb```
* make data directory ```sudo mkdir -p /data/db```
* To get mongo dameon up and running ```sudo mongod```
* Access mongo shell with ```mongo```
* close mongodb with ctrl + c twice in stop Database
* list database with ```show dbs```
* To create new database with use command ie ```use mongoBasics```
* Create user for database:
      db.createUser(
         {
           user: "admin",
           pwd: "somepassword",
           roles: [ "readWrite", "dbAdmin" ]
         }
      );
* To update user use ```db.updateUser()```
* Login as user: ```db.auth('user','password');```
* Get mongodb version ```db.version()```

###Working with Mongo
* See contents of current directory ```ls()```
* Load file in directory with ```load('./seed.js')```
* the following is the same as running `use mongoBasics` from the ```db.getSiblingDB('mongoBasics');```
* Find length of collection with ```db.collectionname.count()```
* Query collection with ```db.collectionname.find()``` or at specific document with ```db.collectionname.find()[1]```
* Limit number of posts with ``` db.collectionname.find().limit(2)```
* Assign collections to variables easily with ```var data = db.collectionname.find()``` and access with ```data.item```
* Only return certain data from a collection with bolleans ```db.collectionname.find({}, {body: false, description: false})``` or instead of ommiting fields get one field back with ```db.collectionname.find({}, {title:true})``` and to turn id off do ```db.collectionname.find({}, {title:true, id:false})```
* To query for a certain value do ```db.collectionname.find({title: "some title"},{})```
* For more query operators visit [https://docs.mongodb.org/v3.0/reference/operator/query/](https://docs.mongodb.org/v3.0/reference/operator/query/)
* To insert data do ```db.post.insert. ie db.post.insert({"title": "horray!"})```
* Use ```show dbs``` to see a list of databases. To see collections use ```show collections``` and to see items in collection ```db.post.find()```
* To update posts do ```db.posts.update({"author": ObjectId("584c605def2992d45926dd74")},{$set:{tags: ['foo', 'bar', 'interesting']}})```
* See what keys are in a field collection ```Object.keys(db.posts.find()[0])```
* To sort asccending/decending use sort ```db.posts.find({}, {title:true}).sort({title: 1})``` and decending ```db.posts.find({}, {title:true}).sort({title: -1})```
* For pagination results use limit and skip methods ```db.posts.find({}, {title:true}).limit(2).skip(2)```
 * Pagination formula: limit = number of records on each page, skip = number of records on each page * page number - 1

  * So, with 5 results per page:
  * page 1: limit = 5, skip = 0
  * page 2: limit = 5, skip = 5
  * page 3: limit = 5, skip = 10
  * etc...

###Mongo drivers
* for node.js there is a core MongoDB driver or the popular Mongoose driver
* For PHP there is PHPLIB+ driver
* more here [https://docs.mongodb.com/ecosystem/drivers](https://docs.mongodb.com/ecosystem/drivers)

###Mongo extras
* For shell syntax highlighting install ```npm install -g mongo-hacker```
* Mongo is more powerful compared to relational databases because of sharding [https://docs.mongodb.org/manual/sharding/](https://docs.mongodb.org/manual/sharding/)
