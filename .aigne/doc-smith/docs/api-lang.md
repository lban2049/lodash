# Lang

Lodash's 'Lang' category provides fundamental utility functions for core JavaScript language operations. These include robust type checking (e.g., `_.isString`, `_.isObjectLike`), deep and shallow cloning (`_.clone`, `_.cloneDeep`), and value comparison (`_.isEqual`, `_.gt`). These functions help create more predictable and reliable code by handling many of JavaScript's edge cases and inconsistencies.

## Type Checking & Comparison

These functions help you understand and compare your data with confidence.

### _.isArguments
Checks if `value` is likely an `arguments` object.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to check. |

**Returns**

- `(boolean)`: Returns `true` if `value` is an `arguments` object, else `false`.

**Example**

```javascript
_.isArguments(function() { return arguments; }());
// => true

_.isArguments([1, 2, 3]);
// => false
```

### _.isArray
Checks if `value` is classified as an `Array` object.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to check. |

**Returns**

- `(boolean)`: Returns `true` if `value` is an array, else `false`.

**Example**

```javascript
_.isArray([1, 2, 3]);
// => true

_.isArray('abc');
// => false
```

### _.isArrayBuffer
Checks if `value` is classified as an `ArrayBuffer` object.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to check. |

**Returns**

- `(boolean)`: Returns `true` if `value` is an array buffer, else `false`.

**Example**

```javascript
_.isArrayBuffer(new ArrayBuffer(2));
// => true

_.isArrayBuffer(new Array(2));
// => false
```

### _.isArrayLike
Checks if `value` is array-like. A value is considered array-like if it's not a function and has a `value.length` that's an integer greater than or equal to `0` and less than or equal to `Number.MAX_SAFE_INTEGER`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to check. |

**Returns**

- `(boolean)`: Returns `true` if `value` is array-like, else `false`.

**Example**

```javascript
_.isArrayLike([1, 2, 3]);
// => true

_.isArrayLike('abc');
// => true

_.isArrayLike(_.noop);
// => false
```

### _.isArrayLikeObject
This method is like `_.isArrayLike` except that it also checks if `value` is an object.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to check. |

**Returns**

- `(boolean)`: Returns `true` if `value` is an array-like object, else `false`.

**Example**

```javascript
_.isArrayLikeObject([1, 2, 3]);
// => true

_.isArrayLikeObject('abc');
// => false

_.isArrayLikeObject(_.noop);
// => false
```

### _.isBoolean
Checks if `value` is classified as a boolean primitive or object.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to check. |

**Returns**

- `(boolean)`: Returns `true` if `value` is a boolean, else `false`.

**Example**

```javascript
_.isBoolean(false);
// => true

_.isBoolean(null);
// => false
```

### _.isBuffer
Checks if `value` is a buffer.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to check. |

**Returns**

- `(boolean)`: Returns `true` if `value` is a buffer, else `false`.

**Example**

```javascript
_.isBuffer(new Buffer(2));
// => true

_.isBuffer(new Uint8Array(2));
// => false
```

### _.isDate
Checks if `value` is classified as a `Date` object.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to check. |

**Returns**

- `(boolean)`: Returns `true` if `value` is a date object, else `false`.

**Example**

```javascript
_.isDate(new Date);
// => true

_.isDate('Mon April 23 2012');
// => false
```

### _.isElement
Checks if `value` is likely a DOM element.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to check. |

**Returns**

- `(boolean)`: Returns `true` if `value` is a DOM element, else `false`.

**Example**

```javascript
_.isElement(document.body);
// => true

_.isElement('<body>');
// => false
```

### _.isEmpty
Checks if `value` is an empty object, collection, map, or set.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to check. |

**Returns**

- `(boolean)`: Returns `true` if `value` is empty, else `false`.

**Example**

```javascript
_.isEmpty(null);
// => true

_.isEmpty(true);
// => true

_.isEmpty(1);
// => true

_.isEmpty([1, 2, 3]);
// => false

_.isEmpty({ 'a': 1 });
// => false
```

### _.isEqual
Performs a deep comparison between two values to determine if they are equivalent.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to compare. |
| `other` | `*` | The other value to compare. |

**Returns**

- `(boolean)`: Returns `true` if the values are equivalent, else `false`.

**Example**

```javascript
var object = { 'a': 1 };
var other = { 'a': 1 };

_.isEqual(object, other);
// => true

object === other;
// => false
```

### _.isEqualWith
This method is like `_.isEqual` except that it accepts `customizer` which is invoked to compare values. If `customizer` returns `undefined`, comparisons are handled by the method instead.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to compare. |
| `other` | `*` | The other value to compare. |
| `customizer` | `Function` | The function to customize comparisons. |

**Returns**

- `(boolean)`: Returns `true` if the values are equivalent, else `false`.

**Example**

```javascript
function isGreeting(value) {
  return /^h(?:i|ello)$/.test(value);
}

function customizer(objValue, othValue) {
  if (isGreeting(objValue) && isGreeting(othValue)) {
    return true;
  }
}

var array = ['hello', 'goodbye'];
var other = ['hi', 'goodbye'];

_.isEqualWith(array, other, customizer);
// => true
```

### _.isError
Checks if `value` is an `Error`, `EvalError`, `RangeError`, `ReferenceError`, `SyntaxError`, `TypeError`, or `URIError` object.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to check. |

**Returns**

- `(boolean)`: Returns `true` if `value` is an error object, else `false`.

**Example**

```javascript
_.isError(new Error);
// => true

_.isError(Error);
// => false
```

### _.isFinite
Checks if `value` is a finite primitive number.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to check. |

**Returns**

- `(boolean)`: Returns `true` if `value` is a finite number, else `false`.

**Example**

```javascript
_.isFinite(3);
// => true

_.isFinite(Number.MIN_VALUE);
// => true

_.isFinite(Infinity);
// => false

_.isFinite('3');
// => false
```

### _.isFunction
Checks if `value` is classified as a `Function` object.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to check. |

**Returns**

- `(boolean)`: Returns `true` if `value` is a function, else `false`.

**Example**

```javascript
_.isFunction(_);
// => true

_.isFunction(/abc/);
// => false
```

### _.isInteger
Checks if `value` is an integer.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to check. |

**Returns**

- `(boolean)`: Returns `true` if `value` is an integer, else `false`.

**Example**

```javascript
_.isInteger(3);
// => true

_.isInteger(Number.MIN_VALUE);
// => false

_.isInteger(Infinity);
// => false

_.isInteger('3');
// => false
```

### _.isLength
Checks if `value` is a valid array-like length.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to check. |

**Returns**

- `(boolean)`: Returns `true` if `value` is a valid length, else `false`.

**Example**

```javascript
_.isLength(3);
// => true

_.isLength(Number.MIN_VALUE);
// => false

_.isLength(Infinity);
// => false

_.isLength('3');
// => false
```

### _.isMap
Checks if `value` is classified as a `Map` object.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to check. |

**Returns**

- `(boolean)`: Returns `true` if `value` is a map, else `false`.

**Example**

```javascript
_.isMap(new Map());
// => true

_.isMap(new WeakMap());
// => false
```

### _.isMatch
Performs a partial deep comparison between `object` and `source` to determine if `object` contains equivalent property values.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | The object to inspect. |
| `source` | `Object` | The object of property values to match. |

**Returns**

- `(boolean)`: Returns `true` if `object` is a match, else `false`.

**Example**

```javascript
var object = { 'a': 1, 'b': 2 };

_.isMatch(object, { 'b': 2 });
// => true

_.isMatch(object, { 'b': 1 });
// => false
```

### _.isMatchWith
This method is like `_.isMatch` except that it accepts `customizer` which is invoked to compare values.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | The object to inspect. |
| `source` | `Object` | The object of property values to match. |
| `customizer` | `Function` | The function to customize comparisons. |

**Returns**

- `(boolean)`: Returns `true` if `object` is a match, else `false`.

**Example**

```javascript
function isGreeting(value) {
  return /^h(?:i|ello)$/.test(value);
}

function customizer(objValue, srcValue) {
  if (isGreeting(objValue) && isGreeting(srcValue)) {
    return true;
  }
}

var object = { 'greeting': 'hello' };
var source = { 'greeting': 'hi' };

_.isMatchWith(object, source, customizer);
// => true
```

### _.isNaN
Checks if `value` is `NaN`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to check. |

**Returns**

- `(boolean)`: Returns `true` if `value` is `NaN`, else `false`.

**Example**

```javascript
_.isNaN(NaN);
// => true

_.isNaN(new Number(NaN));
// => true

isNaN(undefined);
// => true

_.isNaN(undefined);
// => false
```

### _.isNative
Checks if `value` is a pristine native function.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to check. |

**Returns**

- `(boolean)`: Returns `true` if `value` is a native function, else `false`.

**Example**

```javascript
_.isNative(Array.prototype.push);
// => true

_.isNative(_);
// => false
```

### _.isNil
Checks if `value` is `null` or `undefined`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to check. |

**Returns**

- `(boolean)`: Returns `true` if `value` is nullish, else `false`.

**Example**

```javascript
_.isNil(null);
// => true

_.isNil(void 0);
// => true

_.isNil(NaN);
// => false
```

### _.isNull
Checks if `value` is `null`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to check. |

**Returns**

- `(boolean)`: Returns `true` if `value` is `null`, else `false`.

**Example**

```javascript
_.isNull(null);
// => true

_.isNull(void 0);
// => false
```

### _.isNumber
Checks if `value` is classified as a `Number` primitive or object.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to check. |

**Returns**

- `(boolean)`: Returns `true` if `value` is a number, else `false`.

**Example**

```javascript
_.isNumber(3);
// => true

_.isNumber(Infinity);
// => true

_.isNumber('3');
// => false
```

### _.isObject
Checks if `value` is the language type of `Object` (e.g. arrays, functions, objects, regexes, `new Number(0)`, and `new String('')`).

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to check. |

**Returns**

- `(boolean)`: Returns `true` if `value` is an object, else `false`.

**Example**

```javascript
_.isObject({});
// => true

_.isObject([1, 2, 3]);
// => true

_.isObject(null);
// => false
```

### _.isObjectLike
Checks if `value` is object-like. A value is object-like if it's not `null` and has a `typeof` result of "object".

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to check. |

**Returns**

- `(boolean)`: Returns `true` if `value` is object-like, else `false`.

**Example**

```javascript
_.isObjectLike({});
// => true

_.isObjectLike([1, 2, 3]);
// => true

_.isObjectLike(_.noop);
// => false

_.isObjectLike(null);
// => false
```

### _.isPlainObject
Checks if `value` is a plain object, that is, an object created by the `Object` constructor or one with a `[[Prototype]]` of `null`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to check. |

**Returns**

- `(boolean)`: Returns `true` if `value` is a plain object, else `false`.

**Example**

```javascript
function Foo() {
  this.a = 1;
}

_.isPlainObject(new Foo());
// => false

_.isPlainObject([1, 2, 3]);
// => false

_.isPlainObject({ 'x': 0, 'y': 0 });
// => true

_.isPlainObject(Object.create(null));
// => true
```

### _.isRegExp
Checks if `value` is classified as a `RegExp` object.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to check. |

**Returns**

- `(boolean)`: Returns `true` if `value` is a regexp, else `false`.

**Example**

```javascript
_.isRegExp(/abc/);
// => true

_.isRegExp('/abc/');
// => false
```

### _.isSafeInteger
Checks if `value` is a safe integer.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to check. |

**Returns**

- `(boolean)`: Returns `true` if `value` is a safe integer, else `false`.

**Example**

```javascript
_.isSafeInteger(3);
// => true

_.isSafeInteger(Number.MIN_VALUE);
// => false

_.isSafeInteger(Infinity);
// => false

_.isSafeInteger('3');
// => false
```

### _.isSet
Checks if `value` is classified as a `Set` object.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to check. |

**Returns**

- `(boolean)`: Returns `true` if `value` is a set, else `false`.

**Example**

```javascript
_.isSet(new Set());
// => true

_.isSet(new WeakSet());
// => false
```

### _.isString
Checks if `value` is classified as a `String` primitive or object.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to check. |

**Returns**

- `(boolean)`: Returns `true` if `value` is a string, else `false`.

**Example**

```javascript
_.isString('abc');
// => true

_.isString(1);
// => false
```

### _.isSymbol
Checks if `value` is classified as a `Symbol` primitive or object.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to check. |

**Returns**

- `(boolean)`: Returns `true` if `value` is a symbol, else `false`.

**Example**

```javascript
_.isSymbol(Symbol.iterator);
// => true

_.isSymbol('abc');
// => false
```

### _.isTypedArray
Checks if `value` is classified as a typed array.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to check. |

**Returns**

- `(boolean)`: Returns `true` if `value` is a typed array, else `false`.

**Example**

```javascript
_.isTypedArray(new Uint8Array());
// => true

_.isTypedArray([]);
// => false
```

### _.isUndefined
Checks if `value` is `undefined`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to check. |

**Returns**

- `(boolean)`: Returns `true` if `value` is `undefined`, else `false`.

**Example**

```javascript
_.isUndefined(void 0);
// => true

_.isUndefined(null);
// => false
```

### _.isWeakMap
Checks if `value` is classified as a `WeakMap` object.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to check. |

**Returns**

- `(boolean)`: Returns `true` if `value` is a weak map, else `false`.

**Example**

```javascript
_.isWeakMap(new WeakMap());
// => true

_.isWeakMap(new Map());
// => false
```

### _.isWeakSet
Checks if `value` is classified as a `WeakSet` object.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to check. |

**Returns**

- `(boolean)`: Returns `true` if `value` is a weak set, else `false`.

**Example**

```javascript
_.isWeakSet(new WeakSet());
// => true

_.isWeakSet(new Set());
// => false
```

### _.lt
Checks if `value` is less than `other`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to compare. |
| `other` | `*` | The other value to compare. |

**Returns**

- `(boolean)`: Returns `true` if `value` is less than `other`, else `false`.

**Example**

```javascript
_.lt(1, 3);
// => true

_.lt(3, 3);
// => false
```

### _.lte
Checks if `value` is less than or equal to `other`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to compare. |
| `other` | `*` | The other value to compare. |

**Returns**

- `(boolean)`: Returns `true` if `value` is less than or equal to `other`, else `false`.

**Example**

```javascript
_.lte(1, 3);
// => true

_.lte(3, 3);
// => true
```

## Cloning

Create shallow or deep copies of values.

### _.clone
Creates a shallow clone of `value`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to clone. |

**Returns**

- `(*)`: Returns the cloned value.

**Example**

```javascript
var objects = [{ 'a': 1 }, { 'b': 2 }];

var shallow = _.clone(objects);
console.log(shallow[0] === objects[0]);
// => true
```

### _.cloneWith
This method is like `_.clone` except that it accepts `customizer` which is invoked to produce the cloned value.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to clone. |
| `customizer` | `Function` | The function to customize cloning. |

**Returns**

- `(*)`: Returns the cloned value.

**Example**

```javascript
function customizer(value) {
  if (_.isElement(value)) {
    return value.cloneNode(false);
  }
}

var el = _.cloneWith(document.body, customizer);

console.log(el === document.body);
// => false
```

### _.cloneDeep
This method is like `_.clone` except that it recursively clones `value`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to recursively clone. |

**Returns**

- `(*)`: Returns the deep cloned value.

**Example**

```javascript
var objects = [{ 'a': 1 }, { 'b': 2 }];

var deep = _.cloneDeep(objects);
console.log(deep[0] === objects[0]);
// => false
```

### _.cloneDeepWith
This method is like `_.cloneWith` except that it recursively clones `value`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to recursively clone. |
| `customizer` | `Function` | The function to customize cloning. |

**Returns**

- `(*)`: Returns the deep cloned value.

**Example**

```javascript
function customizer(value) {
  if (_.isElement(value)) {
    return value.cloneNode(true);
  }
}

var el = _.cloneDeepWith(document.body, customizer);

console.log(el === document.body);
// => false
```

## Type Conversion

Convert values from one type to another.

### _.castArray
Casts `value` as an array if it's not one.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to inspect. |

**Returns**

- `(Array)`: Returns the cast array.

**Example**

```javascript
_.castArray(1);
// => [1]

_.castArray({ 'a': 1 });
// => [{ 'a': 1 }]

_.castArray('abc');
// => ['abc']
```

### _.toArray
Converts `value` to an array.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to convert. |

**Returns**

- `(Array)`: Returns the converted array.

**Example**

```javascript
_.toArray({ 'a': 1, 'b': 2 });
// => [1, 2]

_.toArray('abc');
// => ['a', 'b', 'c']

_.toArray(1);
// => []
```

### _.toFinite
Converts `value` to a finite number.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to convert. |

**Returns**

- `(number)`: Returns the converted number.

**Example**

```javascript
_.toFinite(3.2);
// => 3.2

_.toFinite(Infinity);
// => 1.7976931348623157e+308

_.toFinite('3.2');
// => 3.2
```

### _.toInteger
Converts `value` to an integer.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to convert. |

**Returns**

- `(number)`: Returns the converted integer.

**Example**

```javascript
_.toInteger(3.2);
// => 3

_.toInteger('3.2');
// => 3
```

### _.toLength
Converts `value` to an integer suitable for use as the length of an array-like object.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to convert. |

**Returns**

- `(number)`: Returns the converted integer.

**Example**

```javascript
_.toLength(3.2);
// => 3

_.toLength(Infinity);
// => 4294967295
```

### _.toNumber
Converts `value` to a number.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to process. |

**Returns**

- `(number)`: Returns the number.

**Example**

```javascript
_.toNumber(3.2);
// => 3.2

_.toNumber('3.2');
// => 3.2
```

### _.toPlainObject
Converts `value` to a plain object flattening inherited enumerable string keyed properties of `value` to own properties of the plain object.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to convert. |

**Returns**

- `(Object)`: Returns the converted plain object.

**Example**

```javascript
function Foo() {
  this.b = 2;
}

Foo.prototype.c = 3;

_.assign({ 'a': 1 }, new Foo());
// => { 'a': 1, 'b': 2 }

_.assign({ 'a': 1 }, _.toPlainObject(new Foo()));
// => { 'a': 1, 'b': 2, 'c': 3 }
```

### _.toSafeInteger
Converts `value` to a safe integer.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to convert. |

**Returns**

- `(number)`: Returns the converted integer.

**Example**

```javascript
_.toSafeInteger(3.2);
// => 3

_.toSafeInteger(Infinity);
// => 9007199254740991
```

### _.toString
Converts `value` to a string. An empty string is returned for `null` and `undefined` values.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to convert. |

**Returns**

- `(string)`: Returns the converted string.

**Example**

```javascript
_.toString(null);
// => ''

_.toString(-0);
// => '-0'

_.toString([1, 2, 3]);
// => '1,2,3'
```

---

After mastering these language utilities, you may want to explore functions for working with specific data types, such as [Math](./api-math.md) or [String](./api-string.md).