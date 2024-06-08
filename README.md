Blue Button Utility
================

Common utility methods for Amida-Tech repositories

[![NPM](https://nodei.co/npm/@taktikorg/natus-officiis.png)](https://nodei.co/npm/@taktikorg/natus-officiis/)

[![Build Status](https://travis-ci.org/taktikorg/natus-officiis.svg)](https://travis-ci.org/taktikorg/natus-officiis)
[![Coverage Status](https://coveralls.io/repos/taktikorg/natus-officiis/badge.png)](https://coveralls.io/r/taktikorg/natus-officiis)

This library provides common Javascript utilities that are used in other Amida-Tech libraries.

## Quick up and running guide

### Prerequisites

- Node.js (v14.19+) and NPM
- Grunt.js

```
# Install dependencies
npm i

# Install grunt
npm i -g grunt

# Test
grunt

```

## Utilities

You can install using [npm](https://www.npmjs.com) and  `require` to use in [node.js](https://nodejs.org/)
```js
var bbu = require('@taktikorg/natus-officiis');

var ob = bbu.object;         // object library
var obs = bbu.object;        // objectset library
var arrs = bbu.arrayset;     // arrayset library
var dtt = bbu.datetime;      // datetime library
```

The following methods are provided
- [`object.exists`](#object.exists)
- [`objectset.compact`](#objectset.compact)
- [`arrayset.append`](#arrayset.append)
- [`datetime.dateToModel`](#datetime.dateToModel)
- [`datetime.dateTimeToModel`](#datetime.dateTimeToModel)
- [`datetime.modelToDate`](#datetime.modelToDate)
- [`datetime.modelToDateTime`](#datetime.modelToDateTime)

### `object` Library

Provides utility methods for objects.

### `exists(obj)`

Checks if `obj` is not `undefined` or `null`
```js
var r0 = ob.exists(null);
var r1 = ob.exists(undefined);
var r2 = ob.exists('anything else');

console.log(r0); // false
console.log(r1); // false
console.log(r2); // true
```

### `objectset` Library

Provides utility methods that modify an object.

### `objectset.compact(obj)`

Recursively removes all `null` and `undefined` values from `obj`.  No special handling is done for resulting empty objects or arrays
```js
var obj = {
  a: 1,
  b: null,
  c: {
    d: undefined,
    e: 4
  },
  f: {
    g: null
  }
};

obs.compact(obj);
console.log(obj); // {a: 1, c:{e:4}, f:{}}
```
### `arrayset` Library

Provides utility methods that modify an array.

### `append(arr, arrToAppend)`

Appends `arrToAppend` elements to `arr`
```js
var arr = ['a', 'b'];

arrs.append(arr, ['c', 'd']);
console.log(arr); // ['a', 'b', 'c', 'd'];
```

### `datetime` Library

Provides conversion methods to/from [blue-button-model](https://github.com/amida-tech/blue-button-model) datetimes from/to ISO datetimes.

### `datetime.dateToModel(d)`

Converts ISO date `d` to [blue-button-model](https://github.com/amida-tech/blue-button-model) datetime
```js
var r0 = dtt.dateToModel('2014');
var r1 = dtt.dateToModel('2014-02');
var r2 = dtt.dateToModel('2014-02-07');
var r3 = dtt.dateToModel('2014-02-07T12:45:04.000Z');

console.log(r0); // {date: '2014-01-01T00:00:00.000Z', precision: 'year'}
console.log(r1); // {date: '2014-02-01T00:00:00.000Z', precision: 'month'}
console.log(r2); // {date: '2014-02-07T00:00:00.000Z', precision: 'day'}
console.log(r3); // {date: '2014-02-07T00:00:00.000Z', precision: 'day'}
```

### `datetime.dateTimeToModel(dt)`

Converts ISO datetime `d` to [blue-button-model](https://github.com/amida-tech/blue-button-model) datetime
```js
var r0 = dtt.dateTimeToModel('2014');
var r1 = dtt.dateTimeToModel('2014-02');
var r2 = dtt.dateTimeToModel('2014-02-07');
var r3 = dtt.dateTimeToModel('2014-02-07T12:45:04.000Z');

console.log(r0); // {date: '2014-01-01T00:00:00.000Z', precision: 'year'}
console.log(r1); // {date: '2014-02-01T00:00:00.000Z', precision: 'month'}
console.log(r2); // {date: '2014-02-07T00:00:00.000Z', precision: 'day'}
console.log(r3); // {date: '2014-02-07T12:45:04.000Z', precision: 'second'}
```
Millisecond piece is ignored even when it is not zero.

### `datetime.modelToDate(dt)`

Converts [blue-button-model](https://github.com/amida-tech/blue-button-model) datetime `dt` to ISO date
```js
var r0 = dtt.modelToDate({
  date: '2014-01-01T00:00:00.000Z',
  precision: 'year'
});
var r1 = dtt.modelToDate({
  date: '2014-02-01T00:00:00.000Z',
  precision: 'month'
});
var r2 = dtt.modelToDate({
  date: '2014-02-07T00:00:00.000Z',
  precision: 'day'
});
var r3 = dtt.modelToDate({
  date: '2014-02-07T12:45:04.000Z',
  precision: 'second'
});

console.log(r0); // '2014'
console.log(r1); // '2014-02'
console.log(r2); // '2014-02-07'
console.log(r3); // '2014-02-07'
```

### `datetime.modelToDateTime(dt)`

Converts [blue-button-model](https://github.com/amida-tech/blue-button-model) datetime `dt` to ISO datetime
```js
var r0 = dtt.modelToDateTime({
    date: '2014-01-01T00:00:00.000Z',
    precision: 'year'
});
var r1 = dtt.modelToDateTime({
    date: '2014-02-01T00:00:00.000Z',
    precision: 'month'
});
var r2 = dtt.modelToDateTime({
    date: '2014-02-07T00:00:00.000Z',
    precision: 'day'
});
var r3 = dtt.modelToDateTime({
    date: '2014-02-07T12:45:04.000Z',
    precision: 'second'
});
var r4 = dtt.modelToDateTime({
    date: '2014-02-07T12:45:04.010Z',
    precision: 'second'
});


console.log(r0); // '2014'
console.log(r1); // '2014-02'
console.log(r2); // '2014-02-07'
console.log(r3); // '2014-02-07T12:45:04.000Z'
console.log(r4); // '2014-02-07T12:45:04.010Z'
```

## License

Licensed under [Apache 2.0](./LICENSE).
