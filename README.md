# Express-router


## Routing
Routing refers to the definition of application end points (URIs) and how they respond to client requests. For an introduction to routing, see Basic routing.

The following code is an example of a very basic route.
```
var express = require('express')
var app = express()

// respond with "hello world" when a GET request is made to the homepage
app.get('/', function (req, res) {
  res.send('hello world')
})
```
## Route methods
A route method is derived from one of the HTTP methods, and is attached to an instance of the express class.

The following code is an example of routes that are defined for the GET and the POST methods to the root of the app.
```
// GET method route
app.get('/', function (req, res) {
  res.send('GET request to the homepage')
})

// POST method route
app.post('/', function (req, res) {
  res.send('POST request to the homepage')
})
```

## Route paths
Here are some examples of route paths based on strings.

This route path will match requests to the root route, /.
```
app.get('/', function (req, res) {
  res.send('root')
})
This route path will match requests to /about.

app.get('/about', function (req, res) {
  res.send('about')
})
This route path will match requests to /random.text.

app.get('/random.text', function (req, res) {
  res.send('random.text')
})
```

## Route parameters
Route parameters are named URL segments that are used to capture the values specified at their position in the URL. The captured values are populated in the req.params object, with the name of the route parameter specified in the path as their respective keys.

Route path: /users/:userId/books/:bookId
Request URL: http://localhost:3000/users/34/books/8989
req.params: { "userId": "34", "bookId": "8989" }
To define routes with route parameters, simply specify the route parameters in the path of the route as shown below.
```
app.get('/users/:userId/books/:bookId', function (req, res) {
  res.send(req.params)
})
```
```
The name of route parameters must be made up of “word characters” ([A-Za-z0-9_]).
```
```
Since the hyphen (-) and the dot (.) are interpreted literally, they can be used along with route parameters for useful purposes.
```

```
Route path: /flights/:from-:to
Request URL: http://localhost:3000/flights/LAX-SFO
req.params: { "from": "LAX", "to": "SFO" }
Route path: /plantae/:genus.:species
Request URL: http://localhost:3000/plantae/Prunus.persica
req.params: { "genus": "Prunus", "species": "persica" }
To have more control over the exact string that can be matched by a route parameter, you can append a regular expression in parentheses (()):

Route path: /user/:userId(\d+)
Request URL: http://localhost:3000/user/42
req.params: {"userId": "42"}
```

## express.Router
Use the express.Router class to create modular, mountable route handlers. A Router instance is a complete middleware and routing system; for this reason, it is often referred to as a “mini-app”.

The following example creates a router as a module, loads a middleware function in it, defines some routes, and mounts the router module on a path in the main app.

Create a router file named birds.js in the app directory, with the following content:
```
var express = require('express')
var router = express.Router()

// define the home page route
router.get('/', function (req, res) {
  res.send('Birds home page')
})
// define the about route
router.get('/about', function (req, res) {
  res.send('About birds')
})

module.exports = router

Then, load the router module in the app:

var birds = require('./birds')

// ...
```
```
app.use('/birds', birds)
```
The app will now be able to handle requests to /birds and /birds/about, as well as call the timeLog middleware function that is specific to the route.



Credit: ExpressJS Documentation
