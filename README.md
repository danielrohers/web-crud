# web-crud

Web application CRUD Node and Mongoose
- list
- create
- findById
- update
- delete


[![npm version](https://badge.fury.io/js/web-crud.svg)](https://badge.fury.io/js/web-crud)
[![npm](https://img.shields.io/npm/dt/web-crud.svg)](https://www.npmjs.com/package/web-crud)

## Installation

```sh
$ npm install web-crud --save
```

### Example

model/foo.js
```js
'use strict';

const mongoose = require('mongoose');
const Schema = mongoose.Schema;

const FooSchema = new Schema({
    name: {
        type: String,
        default: ''
    }
});

module.exports = mongoose.model('Foo', FooSchema);
```

controller/foo.js
```js
'use strict';

const Model = require('./model/foo');
const Crud = require('web-crud');

Crud.model(Model); // set model mongoose

module.exports = class Foo extends Crud {};
```

route/foo.js
```js
'use strict';

const express = require('express');
const router = express.Router();
const controller = require('./controller/foo');

router
    .route('/')
    .get(controller.list)
    .post(controller.create)

router
    .route('/:id')
    .get(controller.findById)
    .put(controller.update)
    .delete(controller.delete)

module.exports = router;
```

List method accepts common query parameters. To prevent column name confusion, some of those parameter are prefixed with underscore.

* Find
```js
/myapiurl/list?my_object_propertie=SomeValue
```
According to: http://mongoosejs.com/docs/api.html#query_Query-find

* Limit
```js
/myapiurl/list?_limit=10
```
According to: http://mongoosejs.com/docs/api.html#query_Query-limit

* Skip
```js
/myapiurl/list?_skip=5
```
According to: http://mongoosejs.com/docs/api.html#query_Query-skip

* Sort
```js
/myapiurl/list?_sort=property_name
/myapiurl/list?_sort=-property_name
```
According to: http://mongoosejs.com/docs/api.html#query_Query-sort

* Count
```js
/myapiurl/list?_count=true
```
According to: http://mongoosejs.com/docs/api.html#query_Query-count

## Technologies
- [Node.js](https://nodejs.org)

## License

[MIT](LICENSE)
