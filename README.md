# num-parser

Parse numbers in ExpressJS requests.

[![npm](https://img.shields.io/npm/v/num-parser.svg)](https://www.npmjs.com/package/num-parser)

## Installation

    npm i num-parser --save


## Usage

The module will parse all numbers in `req.query`, `req.params`, and `req.body`.

Also works with floating points.

To work with `req.body` you need to add after [body-parser](https://github.com/expressjs/body-parser):

```javascript
const bodyParser = require('body-parser')
const numParser = require('num-parser')

app.use(bodyParser.json())
app.use(numParser)

// ?a=1&b[c]=tw0&b[d]=3.5
app.use('/', (req, res) => {
  console.log(req.query)
  // => { a: 1, b: { c: 'tw0', d: 3.5 } }
})
```

NOTE: I've had problems having it as a global middleware to work with `req.params`. If it's not working for you, try putting the middleware in for each route:

```javascript
// ?a=1&b[c]=tw0&b[d]=3.5
app.use('/', numParser, (req, res) => {
  console.log(req.query)
  // => { a: 1, b: { c: 'tw0', d: 3.5 } }
})
```
