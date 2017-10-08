## Module Merge Objects

Deep merge everyting using powerful merging strategy.

## Statistics

[![Github All Releases](https://img.shields.io/github/downloads/brickifyjs/module-merge/total.svg?style=flat-square)](https://github.com/brickifyjs/module-merge)

## Social
[![GitHub forks](https://img.shields.io/github/forks/brickifyjs/module-merge.svg?style=social&label=Fork&style=flat-square)](https://github.com/brickifyjs/module-merge)
[![GitHub stars](https://img.shields.io/github/stars/brickifyjs/module-merge.svg?style=social&label=Stars&style=flat-square)](https://github.com/brickifyjs/module-merge)
[![GitHub watchers](https://img.shields.io/github/watchers/brickifyjs/module-merge.svg?style=social&label=Watch&style=flat-square)](https://github.com/brickifyjs/module-merge)

## Project Health

[![Travis branch](https://img.shields.io/travis/brickifyjs/module-merge/master.svg?style=flat-square)](https://travis-ci.org/brickifyjs/module-merge)
[![Coveralls branch](https://img.shields.io/coveralls/brickifyjs/module-merge/master.svg?style=flat-square)](https://coveralls.io/github/brickifyjs/module-merge)
[![bitHound](https://img.shields.io/bithound/dependencies/github/brickifyjs/module-merge.svg?style=flat-square)](https://www.bithound.io/github/brickifyjs/module-merge/master/dependencies/npm)
[![bitHound](https://img.shields.io/bithound/devDependencies/github/brickifyjs/module-merge.svg?style=flat-square)](https://www.bithound.io/github/brickifyjs/module-merge/master/dependencies/npm)

## Install

```bash
$ npm install @brickify/m-merge
```

## Options

*Merging strategy*

```js
{
  immutable: false, // Returns new Object
  keepExistingValues: true, // Older properties are kept even if they didn't exist in the new object
  eraseMethods: true,  // Override methods or keep previous method
  eraseValues: true, // Override string || boolean || undefined || null
  eraseNotSameType: true, // Override not same types without diff
  eraseArray: false, // Direct Override Arrays
  eraseObject: false // Direct Override Objects
}
```

## Usage

```js
var merge = require('@bricksjs/m-merge');


// Merge not same type
var a = 1;
var b = null;
console.log(merge(a, b));
// -> null


// Merge object not immutable
var a = {foo: 'foo'};
var b = {bar: 'bar'};
console.log(merge(a, b));
// ->  {foo: 'foo'}


// Merge object immutable
var a = {foo: 'foo'};
var b = {bar: 'bar'};
console.log(merge(a, b, {immutable: true}));
// ->  {foo: 'foo'}


// Merge objects erasing existing objects
var a = {foo: 'foo'};
var b = {bar: 'bar'};
console.log(merge(a, b, {eraseObject: true}));
// -> {bar: 'bar'};


// Merge objects without keeping existing values
var a = {foo: 'foo'};
var b = {bar: 'bar2'};
console.log(merge(a, b, {keepExistingValues: false}));
// -> {bar: 'bar2'}


// Merge objects keeping existing values
var a = {foo: 'foo'};
var b = {bar: 'bar'};
console.log(merge(a, b));
// -> {foo: 'foo', bar: 'bar'}

// Merge objects
var a = {foo: 'foo'};
var b = {foo: 'foo2', bar: 'bar'};
console.log(merge(a, b));
// -> {foo: 'foo2', bar: 'bar'};


// Merge objects and not erase existing values
var a = {foo: 'foo'};
var b = {foo: 'foo2', bar: 'bar'};
console.log(merge(a, b, {eraseValues: false}));
// -> {foo: 'foo', bar: 'bar'}


// Merge array < length
var a = [0];
var b = [0, 1];
console.log(merge(a, b));
// -> [0]


// Merge array > length
var a = [0, 1];
var b = [0];
console.log(merge(a, b));
// -> [0, 1]

// Merge array < length and not keepExistingValues
var a = [0];
var b = [0, 1];
console.log(merge(a, b, {keepExistingValues: false}));
// -> [0]

// Merge array > length and not keepExistingValues
var a = [0, 1];
var b = [0];
console.log(merge(a, b, {keepExistingValues: false}));
// -> [0, 1]


// Merge array not immutable
var a = [0];
var b = [0];
console.log(merge(a, b));
// -> [0]


// Merge array immutable
var a = [0, 1, 2];
var b = [0, 1, 2, 3];
var c = merge(a, b, {immutable: true});
console.log(c);
// -> [0, 1, 2, 3]


// Merge methods
var a = function () {
};
a.foo = true;
var b = function () {
    
};
console.log(merge(a, b));
// -> b && b.foo

// eraseArray
var a = [0, 1, 2];
var b = [0, 1, 2, 3];
console.log(merge(a, b, {eraseArray: true}));
// -> [0, 1, 2, 3]

// eraseArray immutable
var a = [0, 1, 2];
var b = [0, 1, 2, 3];
var c = merge(a, b, {eraseArray: true, immutable: true});
console.log(c);
// -> [0, 1, 2, 3]


// eraseObject
var a = {foo: 'foo'};
var b = {bar: 'bar'};
console.log(merge(a, b, {eraseObject: true}));
// -> {bar: 'bar'}

// eraseObject immutable
var a = {foo: 'foo'};
var b = {bar: 'bar'};
var c = merge(a, b, {eraseObject: true, immutable: true});
console.log(c);
// -> {bar: 'bar'}

```

## Input

```js
merge(ObjectA, ObjectB ,{...options});
```
