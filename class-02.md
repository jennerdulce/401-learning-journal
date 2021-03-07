## Key Ideas

### exporting
- you first have to create a module.js file
- must have a `module.exports = {} at the end of the file`
```javascript

// filename person.js
module.exports = {
  name: jenner,
  age: 28,
  isCool: true
}
```
### importing
- you first need to import the file
  - `const person = require('./server.js')`
- person now has a value of the the `module.exports` object that was imported
- has access to its properties
```javascript

// you need to import the file
const person = require('./server.js')

console.log(person.jenner)
console.log(person.age)
console.log(person.isCool)
```

### middleware
- middleware can be app/global or route level
  - app/global middleware are touched by every call to routes that are made
    - `app.use(logger)`
  - route level middleware are only invoked when the route they are inserted to are called
    - `app.get('/person', validator, (req, res) => {`

### receiving data from routes
- /:parameters
  - `app.get('/api/:name',...)` = `req.params.name`
- Query Strings
  - `http://server/route?name=jenner` = `req.query.name`

### setup for testing
1. Install `jest` and `superagent` so that you can run your tests
  - `npm install jest superagent express`
2. Create a `__test__` folder
3. Within the `__test__` folder, create a test file
  - this test file should match the name of the js file that you want to test.
  - `server.js` -> `server.test.js`
4. Add the proper testing scrips to your `package.json` file
  ```
    // package.json
   "scripts": {
     "test": "jest --coverage",
   }
   ```
5. Run tests on demand by `npm test`

### server testing
- withing the `server.test.js` file
```javascript
const supertest = require('supertest');
const server = require('server.js');
const request = supertest(server.app);
describe('test-suite', () => {
  test('what youre actually testing', async () => {
    await request.get('/data')
      .then( response => {
        expect(response.body).toBeDefined();
      })
  })
})
```

### misc
- `.get()`, `.post()`, `.put()`, `.delete()` are also known as method
