# arguguard

> Strict argument validation with testable errors

## Install

Install with [npm](https://www.npmjs.com/)

```sh
$ npm i arguguard --save-dev
```

## Usage

arguguard takes three arguments.

`arguguard(label, [description1, description2, ...], arguments)``

1. A string label such as `myFunction()` that will be used in error reporting
2. An array of descriptions. Each description can either be a string (like `number` or `boolean`) or a class function (like `Array` or `MyClass`).
If the description is a string a `typeof` check will be used. If its a class function, an `instanceof` check will be used.
3. The arguments to test.

```js
var arguguard = require('arguguard')

function myFunction(myNumber, myClass, arrayofMyClass) {
  arguguard('myFunction()', ['number', MyClass, [MyClass]], arguments)
}

myFunction()
>> Arguguard:User:ArgumentsLengthError: myFunction() arguments.length should be "3", received "0"

myFunction(1, myClass, [myClass, myClass], callback)
>> Arguguard:User:ArgumentsLengthError: myFunction() arguments.length should be "3", received "4"

myFunction('1', myClass, [myClass, myClass])
>> Arguguard:User:ArgumentTypeError: myFunction() arguments[0] type should be "number", received "string"

myFunction(1, {}, [myClass, myClass])
>> Arguguard:User:ArgumentInstanceError: myFunction() arguments[1] constructor should be "MyClass", received "Object"

myFunction(1, myClass, myClass)
>> Arguguard:User:ArgumentInstanceError: myFunction() arguments[2] constructor should be "Array", received "MyClass"

myFunction(1, myClass, [myClass, MyClass])
>> Arguguard:User:ArgumentInstanceError: myFunction() arguments[2][1] constructor should be "MyClass", received "Function"

myFunction(1, new MyClass())
>> ✓
```

### Api Errors

The `arguguard` api is defensively programmed and will throw errors if called with the wrong arguments

```js
arguguard(['number', MyClass, [MyClass]], arguments)
>> Arguguard:Api:ArgumentsLengthError: arguguard() arguments.length should be "3", received "2"

arguguard('myFunction()', ['number', MyClass, [MyClass]], arguments)
>> ✓
```

## Running tests

Install dev dependencies:

```sh
$ npm i -d && npm test
```

## Contributing

Pull requests and stars are always welcome. For bugs and feature requests, [please create an issue](https://github.com/SafeMarket/arguguard/issues)

## Author

***

* [github/---](https://github.com/---)
* [twitter/---](http://twitter.com/---)

## License

Copyright © 2017 []()
Licensed under the MIT license.

***

_This file was generated by [readme-generator](https://github.com/jonschlinkert/readme-generator) on January 21, 2017._
