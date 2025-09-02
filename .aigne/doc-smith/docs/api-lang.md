# Lang

Functions in the Lang category provide a series of core JavaScript language utilities, primarily for type checking (e.g., `_.isNumber`, `_.isArray`), value comparison (e.g., `_.isEqual`, `_.gt`), and object cloning (e.g., `_.clone`, `_.cloneDeep`). These fundamental functions are the building blocks for more complex logic.

## castArray

Casts `value` as an array if it's not one.

**Since**
4.4.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `value` | `*` | The value to check. |

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

_.castArray(null);
// => [null]

_.castArray(undefined);
// => [undefined]

_.castArray();
// => []

var array = [1, 2, 3];
console.log(_.castArray(array) === array);
// => true
```

## clone

Creates a shallow clone of `value`. Supported values are arrays, array buffers, booleans, date objects, maps, numbers, `Object` objects, regexes, sets, strings, symbols, and typed arrays. The enumerable properties of `arguments` objects are cloned as plain objects. Unclonable values, such as error objects, functions, DOM nodes, and WeakMaps, are returned as empty objects.

**Since**
0.1.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
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

## cloneDeep

This method is like `_.clone` except that it recursively clones `value`.

**Since**
1.0.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
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

## cloneDeepWith

This method is like `_.cloneWith` except that it recursively clones `value`.

**Since**
4.0.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `value` | `*` | The value to recursively clone. |
| `customizer` | `Function` | (Optional) The function to customize cloning. |

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
console.log(el.nodeName);
// => 'BODY'
console.log(el.childNodes.length);
// => 20
```

## cloneWith

This method is like `_.clone` except that it accepts `customizer` which is invoked to produce the cloned value. If `customizer` returns `undefined`, cloning is handled by the method. The `customizer` is invoked with up to four arguments: (value [, index|key, object, stack]).

**Since**
4.0.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `value` | `*` | The value to clone. |
| `customizer` | `Function` | (Optional) The function to customize cloning. |

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
console.log(el.nodeName);
// => 'BODY'
console.log(el.childNodes.length);
// => 0
```

## conformsTo

Checks if `object` conforms to `source` by invoking the predicate properties of `source` with the corresponding property values of `object`.

**Since**
4.14.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `object` | `Object` | The object to inspect. |
| `source` | `Object` | The object of property predicates to conform to. |

**Returns**

- `(boolean)`: Returns `true` if `object` conforms, else `false`.

**Example**

```javascript
var object = { 'a': 1, 'b': 2 };

_.conformsTo(object, { 'b': function(n) { return n > 1; } });
// => true

_.conformsTo(object, { 'b': function(n) { return n > 2; } });
// => false
```

## eq

Performs a `SameValueZero` comparison between two values to determine if they are equivalent.

**Since**
4.0.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `value` | `*` | The value to compare. |
| `other` | `*` | The other value to compare. |

**Returns**

- `(boolean)`: Returns `true` if the values are equivalent, else `false`.

**Example**

```javascript
var object = { 'a': 1 };
var other = { 'a': 1 };

_.eq(object, object);
// => true

_.eq(object, other);
// => false

_.eq('a', 'a');
// => true

_.eq('a', Object('a'));
// => false

_.eq(NaN, NaN);
// => true
```

## gt

Checks if `value` is greater than `other`.

**Since**
3.9.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `value` | `*` | The value to compare. |
| `other` | `*` | The other value to compare. |

**Returns**

- `(boolean)`: Returns `true` if `value` is greater than `other`, else `false`.

**Example**

```javascript
_.gt(3, 1);
// => true

_.gt(3, 3);
// => false

_.gt(1, 3);
// => false
```

## gte

Checks if `value` is greater than or equal to `other`.

**Since**
3.9.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `value` | `*` | The value to compare. |
| `other` | `*` | The other value to compare. |

**Returns**

- `(boolean)`: Returns `true` if `value` is greater than or equal to `other`, else `false`.

**Example**

```javascript
_.gte(3, 1);
// => true

_.gte(3, 3);
// => true

_.gte(1, 3);
// => false
```

## isArguments

Checks if `value` is likely an `arguments` object.

**Since**
0.1.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
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

## isArray

Checks if `value` is classified as an `Array` object.

**Since**
0.1.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `value` | `*` | The value to check. |

**Returns**

- `(boolean)`: Returns `true` if `value` is an array, else `false`.

**Example**

```javascript
_.isArray([1, 2, 3]);
// => true

_.isArray(document.body.children);
// => false

_.isArray('abc');
// => false

_.isArray(_.noop);
// => false
```

## isArrayBuffer

Checks if `value` is classified as an `ArrayBuffer` object.

**Since**
4.3.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
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

## isArrayLike

Checks if `value` is array-like. A value is considered array-like if it's not a function and has a `value.length` that's an integer greater than or equal to `0` and less than or equal to `Number.MAX_SAFE_INTEGER`.

**Since**
4.0.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `value` | `*` | The value to check. |

**Returns**

- `(boolean)`: Returns `true` if `value` is array-like, else `false`.

**Example**

```javascript
_.isArrayLike([1, 2, 3]);
// => true

_.isArrayLike(document.body.children);
// => true

_.isArrayLike('abc');
// => true

_.isArrayLike(_.noop);
// => false
```

## isArrayLikeObject

This method is like `_.isArrayLike` except that it also checks if `value` is an object.

**Since**
4.0.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `value` | `*` | The value to check. |

**Returns**

- `(boolean)`: Returns `true` if `value` is an array-like object, else `false`.

**Example**

```javascript
_.isArrayLikeObject([1, 2, 3]);
// => true

_.isArrayLikeObject(document.body.children);
// => true

_.isArrayLikeObject('abc');
// => false

_.isArrayLikeObject(_.noop);
// => false
```

## isBoolean

Checks if `value` is classified as a boolean primitive or object.

**Since**
0.1.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
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

## isBuffer

Checks if `value` is a buffer.

**Since**
4.3.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
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

## isDate

Checks if `value` is classified as a `Date` object.

**Since**
0.1.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
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

## isElement

Checks if `value` is likely a DOM element.

**Since**
0.1.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
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

## isEmpty

Checks if `value` is an empty object, collection, map, or set. Objects are considered empty if they have no own enumerable string keyed properties. Array-like values such as `arguments` objects, arrays, buffers, strings, or jQuery-like collections are considered empty if they have a `length` of `0`. Similarly, maps and sets are considered empty if they have a `size` of `0`.

**Since**
0.1.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
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

## isEqual

Performs a deep comparison between two values to determine if they are equivalent. Supported values are arrays, array buffers, booleans, date objects, error objects, maps, numbers, `Object` objects, regexes, sets, strings, symbols, and typed arrays. `Object` objects are compared by their own, not inherited, enumerable properties. Functions and DOM nodes are compared by strict equality (`===`).

**Since**
0.1.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
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

## isEqualWith

This method is like `_.isEqual` except that it accepts `customizer` which is invoked to compare values. If `customizer` returns `undefined`, comparisons are handled by the method. The `customizer` is invoked with up to six arguments: (objValue, othValue [, index|key, object, other, stack]).

**Since**
4.0.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `value` | `*` | The value to compare. |
| `other` | `*` | The other value to compare. |
| `customizer` | `Function` | (Optional) The function to customize comparisons. |

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

## isError

Checks if `value` is an `Error`, `EvalError`, `RangeError`, `ReferenceError`, `SyntaxError`, `TypeError`, or `URIError` object.

**Since**
3.0.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
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

## isFinite

Checks if `value` is a finite primitive number.

**Since**
0.1.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
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

## isFunction

Checks if `value` is classified as a `Function` object.

**Since**
0.1.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
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

## isInteger

Checks if `value` is an integer.

**Since**
4.0.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
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

## isLength

Checks if `value` is a valid array-like length.

**Since**
4.0.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
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

## isMap

Checks if `value` is classified as a `Map` object.

**Since**
4.3.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `value` | `*` | The value to check. |

**Returns**

- `(boolean)`: Returns `true` if `value` is a map, else `false`.

**Example**

```javascript
_.isMap(new Map);
// => true

_.isMap(new WeakMap);
// => false
```

## isMatch

Performs a partial deep comparison between `object` and `source` to determine if `object` contains equivalent property values.

**Since**
3.0.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
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

## isMatchWith

This method is like `_.isMatch` except that it accepts `customizer` which is invoked to compare values. If `customizer` returns `undefined`, comparisons are handled by the method. The `customizer` is invoked with up to five arguments: (objValue, srcValue, index|key, object, source).

**Since**
4.0.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `object` | `Object` | The object to inspect. |
| `source` | `Object` | The object of property values to match. |
| `customizer` | `Function` | (Optional) The function to customize comparisons. |

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

## isNaN

Checks if `value` is `NaN`. Note: This method is not the same as the global `isNaN` which returns `true` for `undefined` and other non-number values.

**Since**
0.1.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
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

## isNative

Checks if `value` is a pristine native function.

**Since**
3.0.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
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

## isNil

Checks if `value` is `null` or `undefined`.

**Since**
4.0.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
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

## isNull

Checks if `value` is `null`.

**Since**
0.1.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
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

## isNumber

Checks if `value` is classified as a `Number` primitive or object. To exclude `Infinity`, `-Infinity`, and `NaN`, use the `_.isFinite` method.

**Since**
0.1.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `value` | `*` | The value to check. |

**Returns**

- `(boolean)`: Returns `true` if `value` is a number, else `false`.

**Example**

```javascript
_.isNumber(3);
// => true

_.isNumber(Number.MIN_VALUE);
// => true

_.isNumber(Infinity);
// => true

_.isNumber('3');
// => false
```

## isObject

Checks if `value` is the language type of `Object` (e.g., arrays, functions, objects, regexes, `new Number(0)`, and `new String('')`).

**Since**
0.1.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `value` | `*` | The value to check. |

**Returns**

- `(boolean)`: Returns `true` if `value` is an object, else `false`.

**Example**

```javascript
_.isObject({});
// => true

_.isObject([1, 2, 3]);
// => true

_.isObject(_.noop);
// => true

_.isObject(null);
// => false
```

## isObjectLike

Checks if `value` is object-like. A value is object-like if it's not `null` and has a `typeof` result of `"object"`.

**Since**
4.0.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
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

## isPlainObject

Checks if `value` is a plain object, that is, an object created by the `Object` constructor or one with a `[[Prototype]]` of `null`.

**Since**
0.8.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `value` | `*` | The value to check. |

**Returns**

- `(boolean)`: Returns `true` if `value` is a plain object, else `false`.

**Example**

```javascript
function Foo() {
  this.a = 1;
}

_.isPlainObject(new Foo);
// => false

_.isPlainObject([1, 2, 3]);
// => false

_.isPlainObject({ 'x': 0, 'y': 0 });
// => true

_.isPlainObject(Object.create(null));
// => true
```

## isRegExp

Checks if `value` is classified as a `RegExp` object.

**Since**
0.1.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `value` | `*` | The value to check. |

**Returns**

- `(boolean)`: Returns `true` if `value` is a regular expression, else `false`.

**Example**

```javascript
_.isRegExp(/abc/);
// => true

_.isRegExp('/abc/');
// => false
```

## isSafeInteger

Checks if `value` is a safe integer. An integer is safe if it's an IEEE-754 double precision number which isn't the result of an unsafe rounding.

**Since**
4.0.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
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

## isSet

Checks if `value` is classified as a `Set` object.

**Since**
4.3.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `value` | `*` | The value to check. |

**Returns**

- `(boolean)`: Returns `true` if `value` is a set, else `false`.

**Example**

```javascript
_.isSet(new Set);
// => true

_.isSet(new WeakSet);
// => false
```

## isString

Checks if `value` is classified as a `String` primitive or object.

**Since**
0.1.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
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

## isSymbol

Checks if `value` is classified as a `Symbol` primitive or object.

**Since**
4.0.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
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

## isTypedArray

Checks if `value` is classified as a typed array.

**Since**
3.0.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `value` | `*` | The value to check. |

**Returns**

- `(boolean)`: Returns `true` if `value` is a typed array, else `false`.

**Example**

```javascript
_.isTypedArray(new Uint8Array);
// => true

_.isTypedArray([]);
// => false
```

## isUndefined

Checks if `value` is `undefined`.

**Since**
0.1.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
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

## isWeakMap

Checks if `value` is classified as a `WeakMap` object.

**Since**
4.3.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `value` | `*` | The value to check. |

**Returns**

- `(boolean)`: Returns `true` if `value` is a weak map, else `false`.

**Example**

```javascript
_.isWeakMap(new WeakMap);
// => true

_.isWeakMap(new Map);
// => false
```

## isWeakSet

Checks if `value` is classified as a `WeakSet` object.

**Since**
4.3.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `value` | `*` | The value to check. |

**Returns**

- `(boolean)`: Returns `true` if `value` is a weak set, else `false`.

**Example**

```javascript
_.isWeakSet(new WeakSet);
// => true

_.isWeakSet(new Set);
// => false
```

## lt

Checks if `value` is less than `other`.

**Since**
3.9.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
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

_.lt(3, 1);
// => false
```

## lte

Checks if `value` is less than or equal to `other`.

**Since**
3.9.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
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

_.lte(3, 1);
// => false
```

## toArray

Converts `value` to an array.

**Since**
0.1.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
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

_.toArray(null);
// => []
```

## toFinite

Converts `value` to a finite number.

**Since**
4.12.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `value` | `*` | The value to convert. |

**Returns**

- `(number)`: Returns the converted number.

**Example**

```javascript
_.toFinite(3.2);
// => 3.2

_.toFinite(Number.MIN_VALUE);
// => 5e-324

_.toFinite(Infinity);
// => 1.7976931348623157e+308

_.toFinite('3.2');
// => 3.2
```

## toInteger

Converts `value` to an integer.

**Since**
4.0.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `value` | `*` | The value to convert. |

**Returns**

- `(number)`: Returns the converted integer.

**Example**

```javascript
_.toInteger(3.2);
// => 3

_.toInteger(Number.MIN_VALUE);
// => 0

_.toInteger(Infinity);
// => 1.7976931348623157e+308

_.toInteger('3.2');
// => 3
```

## toLength

Converts `value` to an integer suitable for use as the length of an array-like object.

**Since**
4.0.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `value` | `*` | The value to convert. |

**Returns**

- `(number)`: Returns the converted integer.

**Example**

```javascript
_.toLength(3.2);
// => 3

_.toLength(Number.MIN_VALUE);
// => 0

_.toLength(Infinity);
// => 4294967295

_.toLength('3.2');
// => 3
```

## toNumber

Converts `value` to a number.

**Since**
4.0.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `value` | `*` | The value to process. |

**Returns**

- `(number)`: Returns the number.

**Example**

```javascript
_.toNumber(3.2);
// => 3.2

_.toNumber(Number.MIN_VALUE);
// => 5e-324

_.toNumber(Infinity);
// => Infinity

_.toNumber('3.2');
// => 3.2
```

## toPlainObject

Converts `value` to a plain object by flattening its inherited enumerable string keyed properties into own properties of the plain object.

**Since**
3.0.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `value` | `*` | The value to convert. |

**Returns**

- `(Object)`: Returns the converted plain object.

**Example**

```javascript
function Foo() {
  this.b = 2;
}

Foo.prototype.c = 3;

_.assign({ 'a': 1 }, new Foo);
// => { 'a': 1, 'b': 2 }

_.assign({ 'a': 1 }, _.toPlainObject(new Foo));
// => { 'a': 1, 'b': 2, 'c': 3 }
```

## toSafeInteger

Converts `value` to a safe integer. A safe integer can be compared and represented correctly.

**Since**
4.0.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `value` | `*` | The value to convert. |

**Returns**

- `(number)`: Returns the converted integer.

**Example**

```javascript
_.toSafeInteger(3.2);
// => 3

_.toSafeInteger(Number.MIN_VALUE);
// => 0

_.toSafeInteger(Infinity);
// => 9007199254740991

_.toSafeInteger('3.2');
// => 3
```

## toString

Converts `value` to a string. An empty string is returned for `null` and `undefined` values. The sign of `-0` is preserved.

**Since**
4.0.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
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

This section introduced Lodash's core language utility functions. To learn more about functions for numerical computations, see the [Math API](./api-math.md) section.
