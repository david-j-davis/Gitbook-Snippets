##Mongo Database Basics
* Install mongodb ```brew install mongodb```
* make data directory ```sudo mkdir -p /data/db```
* To get mongo up and running ```sudo mongod```
* close mongodb with ctrl + c twice in stop Database
* Access mongo via shell with ```mongo```
* list database with ```show dbs```
* To create new database with use command ie ```use mongoBasics```
* To insert data do ```db.post.insert. ie db.post.insert({"title": "horray!"})```
* Use ```show dbs``` to see a list of databases. To see collections use ```show collections``` and to see items in collection ```db.post.find()```
