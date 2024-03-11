# start with backend
- connect to database and make your schemas/models
- start creating routes using express-Router
- make the signup and signin page and return a jwt token for authentication, store the jwt in cookies
- make middlewares for further stuff like updating profile, sending some req etc. ( you can set something you may require later in consequent functions in your req body in this way `req.userId = user._id` )
- use zod whenever accepting a body in requests
- whenever storing passwords in your db, you must hash them using some lib to keep them safe
  moreover, same words return same hash so anyone can guess that 2 passwords are same when they see the hash, to prevent this you must add some SALT, salt means to add some shit in the word of your own to make the passwords unguessable
  one cool library for doing this is **BCRYPT.js**
- mongoDB isn't used much in real world applications, use some other db when you learn it. PostGres is a popular one
- if creating a payment application, store amounts in the form of integers not decimals because of approximation issues, so instead of storing 88.88 you will store 8888 and specify in your code that decimals are 2, something similar to how it is done in ERC20 Tokens

# frontend
- when connecting your backend, you can send http requests to an HTTP DUMP on the web  to test your call out (search it on google)
- first of all setup your routes to different pages in the main app using react-router-dom
- your job in frontend is to break down your app into small components for simpler implementation