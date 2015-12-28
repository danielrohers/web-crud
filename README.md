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
        required: true
    },
    last_name: {
        type: String,
        required: true
    },
    full_name: {
        type: String,
        required: true
    },
});

module.exports = mongoose.model('Foo', FooSchema);
```

controller/foo.js
```js
'use strict';

const Model = require('./model/foo');
const Crud = require('web-crud');

Crud.model(Model); // set model mongoose

module.exports = class Foo extends Crud {

    // if you want to override
    static create (req, res) {
        req.body.full_name = `${req.body.name} ${req.body.last_name}`
        super.create(req, res);
    };

};
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

## Technologies
- [Node.js](https://nodejs.org)

## License

[MIT](LICENSE)
