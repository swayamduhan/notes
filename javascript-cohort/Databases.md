## Installing MongoDb and Postgres

Get a cloud instance of mongo from the web
create a database and add password authentication 
add ip address 0.0.0.0/0 so that it is accessible from everywhere. if you set it to your own ip address then only your computer will be able to access it
Click on connect then Compass. install compass locally for GUI interface of your database

For postgres, simply go to neon.tech and create a database and keep the connection string handy


## Why databases
In Memory databases are not cool, we lose them as soon as the server goes down. also, its difficult to keep them in sync when we have multiple backend servers
User hits backend then backend hits database

### Types of databases
1. Graph DBs
2. Vector DBs
3. Non SQL DBs (MongoDB is this)
4. SQL DBs

## MongoDB
lets you create multiple databases
each database has tables (collections)
we can dumb json data in these tables
it is schemaless (json data doesnt have any structure) and it scales well (good choice for decent applications but most of the open source real world full stack applications use SQL DBs)


## Using mongoose.js
this lib is used to store data in database
we can do CRUD => create, read, update, delete

eg : 
```
const mongoose = require('mongoose');
mongoose.connect(`mongodb+srv://admin:<pass>@cluster0.aioqxmc.mongodb.net/${database-name}`)

const User = mongoose.model('<table_name>', {
  name : String,
  age : Number,
  email : String
})

const user = new User({name : "swayam", age : 18, email : "oqibz@example.com"})

user.save()
.then(()=>console.log("done"))
```
we can also do `await User.create({json})` instead of new User and then saving

there are various methods present in docs to simply search for a certain object instance in database
we usually use this to see if the user already exists in the db
```
const userExists = await User.findOne({email : "adjada@gmail.com"}) 
```