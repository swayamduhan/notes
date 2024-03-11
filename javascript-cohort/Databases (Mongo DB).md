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
we can dump json data in these tables
it is schemaless (json data doesnt have any structure) and it scales well (good choice for decent applications but most of the open source real world full stack applications use SQL DBs)


## Using mongoose.js
this lib is used to store data in database
we can do CRUD => create, read, update, delete

eg : 
```js
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

or 

```js
const mongoose = require("mongoose")
mongoose.connect("mongodb+srv://admin:Jc6sD0hiR6morjrU@cluster0.aioqxmc.mongodb.net/user-data")
  
const schema = new mongoose.Schema({
    name : String,
    password : String
})
  
const User = mongoose.model("user data", schema)
  
const user1 = new User({name : "swayamdawn", password : "hell0x123"})
user1.save().then(() => console.log("User Saved"))
     .catch(err => console.log(err))
  
// find a user by its name
User.findOne({name : "swayamdawn"}).then((user)=>{
    if(!user){
        return console.log("No user found")
    }
    // show the user info
    console.log(`User Name : ${user.name}`)
    console.log(`Password : ${user.password}`)
})
```
we can also do `await User.create({json})` instead of new User and then saving

there are various methods present in docs to simply search for a certain object instance in database
we usually use this to see if the user already exists in the db
```js
const userExists = await User.findOne({email : "adjada@gmail.com"}) 
```

## Creating References
- a user purchases courses and these courses are available in another table
- how can you create a relationship between this purchasedCourses field and the table
- we can use the `ref` property to do this

example : 
```js
const mongoose = require('mongoose');
const Schema = mongoose.Schema;

// Define Author schema
const authorSchema = new Schema({
    name: String,
    age: Number
});

// Define Book schema
const bookSchema = new Schema({
    title: String,
    author: {
        type: Schema.Types.ObjectId,
        ref: 'Author'  // This refers to the 'Author' model
    },
    pages: Number
});

// Create models from the schemas
const Author = mongoose.model('Author', authorSchema);
const Book = mongoose.model('Book', bookSchema);

// Example usage
(async () => {
    await mongoose.connect('mongodb://localhost:27017/mydb', { useNewUrlParser: true, useUnifiedTopology: true });

    // Create a new author
    const author = await Author.create({ name: 'John Doe', age: 40 });

    // Create a new book referencing the author
    const book = await Book.create({ title: 'Sample Book', author: author._id, pages: 200 });

    // Now you can populate the author field of the book
    const populatedBook = await Book.findById(book._id).populate('author');
    console.log(populatedBook);

    // Close connection
    await mongoose.connection.close();
})();

```

## CRUD 
1. Create
	`.create` to create new entry in table
2. Read
	`.findById`, `.findOne` to find one entry with the specified data
	`find` to multiple entries, `.find({})` to get all entries (similar for update)
3. Update
	`updateOne`, `updateMany`, `update`
```js
await Author.updateOne({name : "John Doe"}, {$push : {bookIds : 800}})
```
this will push a new book id to the bookIds array in the entry of author with name John Doe

4. Delete
	`.deleteOne` and `deleteMany`

## NOTE
CLUSTER? - eg an AWS machine to store all databases
DATABASES? - every application has its own database and it contains further tables
TABLES? - they contain the data for sum' specific shit



## Querying / Filtering
example : returning all the users containing "swa" in either first name or last name
we use `$or, $regex` to handle this filtering.
we also have `$and` for more cases

```js
const users = await User.find({
    $or: [
      {
        firstName: {
          $regex: filter,
          $options : 'i'
        },
      },
      {
        lastName: {
          $regex: filter,  // to handle if beech wale letters
          $options : 'i'  // for case insensitivity
        },
      },
    ],
  });
  
  return res.json({
    user: users.map((user) => {
      return {
        username: user.username,
        firstName: user.firstName,
        lastName: user.lastName,
        _id : user._id
      };
    }),
  });
```

- in SQL Databases, we have `LIKE` querying



## Atomic Transactions

-------------- Read Here --------------
[[BACKEND DEVELOPMENT#Atomic Transaction?]]



## Creating Txs in MongoDB
what happens in a tx?
either everything happens or nothing happens in the code that is mentioned, this is for safety in especially cases where money transfers are involved, if the backend goes down inbetween we want the money to be reverted
you can [read here](https://mongoosejs.com/docs/transactions.html)

- everything between `startTransaction` and `commitTransaction` is in the tx
- you need to start a session at the starting
- everytime you do a find,update (any db operation) : do a `.session(session)`

here is the code : 
```js
router.post("/transfer", authMiddleware, async (req, res) => {
  const { success } = transferSchema.safeParse(req.body);
  if (!success) {
    return res.json({
      message: "invalid inputs",
    });
  }
  
  const session = await mongoose.startSession();
  session.startTransaction();
  const { amount, to } = req.body;
  const fromAccount = await Account.findOne({ userId: req.userId }).session(
    session
  );
  
  if (!fromAccount || fromAccount.balance < amount) {
    await session.abortTransaction();
    return res.status(400).json({
      message: "insufficient balance",
    });
  }
  
  const toAccount = await Account.findOne({ userId: to });
  if (!toAccount) {
    await session.abortTransaction();
    return res.status(400).json({
      message: "invalid account",
    });
  }
  
  await Account.updateOne(
    { userId: req.userId },
    { $inc: { balance: -amount } }
  ).session(session);
  
  await Account.updateOne(
    { userId: to },
    { $inc: { balance: amount } }
  ).session(session);
  
  await session.commitTransaction();
  res.status(200).json({
    message: "transaction completed",
  });
});
```

**COOL SHIT ACHIEVED :**
1. if user tries to exploit payment app by sending 2 tx at once and doing exploitation in balance, it will be solved because user wont be able to send 2 tx at once
   what happens is if lets suppose the current tx that is running, another tx starts running which wants to read/write to the same stuff that the first tx is running then that would make a conflict and wont happen 
1. if backend kharab hojata beech mein or if tx fails to go through, then whole tx will be reverted

