Overview
==============
The FieldVal-JS library allows you to easily validate objects and provide readable and structured error reports.

FieldVal modules:

* FieldVal-JS (This repository)

   The core of FieldVal - provides basic validation functionality such as getting keys from an object and allows chaining of operators.
   
* FieldVal-BasicVal-JS

   Basic operators and errors for required fields, type checking, length and numeric rules.
   
* FieldVal-UI

   A companion library that creates customizable forms that parse and display FieldVal error structures.
   

How to use in NodeJS
=============
The FieldVal library works both as a node package and via the browser. To install the node packages, run:
```bash
npm install fieldval
npm install fieldval-basicval
```

Basic Usage
=============
```javascript

//Import FieldVal
var Validator = require('fieldval');

//Import FieldVal-BasicVal - some simple validators
var bval = require('fieldval-basicval');

//Have some data to validate
var data = {
    my_number: "clearly not a number"
}

//Create a Validator instance using the data
var validator = new Validator(data);

//Get values using validator.get(field_name, field_type, required)
var my_number = validator.get("my_number", bval.integer(true));

//Create an error for the validation (null if no errors)
var error = validator.end();
```

The ```error``` in this instance will be:
```json
{
  "invalid": {
    "my_number": {
      "error_message": "Incorrect field type. Expected integer.",
      "error": 2,
      "expected": "integer",
      "received": "string"
    }
  },
  "error_message": "One or more errors.",
  "error": 0
}
```

How to use in the browser
=============
To use in the browser, download and include the ```fieldval.js``` file from this repository and ```fieldval-basicval.js``` from [https://github.com/FieldVal/fieldval-basicval-js/](https://github.com/FieldVal/fieldval-basicval-js/).

Development
=============

This project uses [gulp.js](http://gulpjs.com/) to build and [mocha](http://visionmedia.github.io/mocha/) to test.

```bash
npm install
gulp js
mocha test/test
```