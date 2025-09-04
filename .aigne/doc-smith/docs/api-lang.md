# Lang

Lodash's 'Lang' category provides a suite of fundamental language utility functions. These functions handle tasks like type checking, value comparison, cloning, and type casting, forming the building blocks for more complex operations. They are essential for writing robust and predictable JavaScript code.

## Function Reference

| Function | Description |
|---|---|
| `_.castArray(value)` | Casts `value` as an array if it's not one. |
| `_.clone(value)` | Creates a shallow clone of `value`. |
| `_.cloneWith(value, [customizer])` | Like `_.clone` but accepts a `customizer` function. |
| `_.cloneDeep(value)` | Recursively clones `value`. |
| `_.cloneDeepWith(value, [customizer])` | Like `_.cloneDeep` but accepts a `customizer` function. |
| `_.conformsTo(object, source)` | Checks if `object` conforms to `source` by invoking the predicate properties of `source`. |
| `_.eq(value, other)` | Performs a `SameValueZero` comparison between two values. |
| `_.gt(value, other)` | Checks if `value` is greater than `other`. |
| `_.gte(value, other)` | Checks if `value` is greater than or equal to `other`. |
| `_.isArguments(value)` | Checks if `value` is likely an `arguments` object. |
| `_.isArray(value)` | Checks if `value` is classified as an `Array` object. |
| `_.isArrayBuffer(value)` | Checks if `value` is classified as an `ArrayBuffer` object. |
| `_.isArrayLike(value)` | Checks if `value` is array-like. |
| `_.isArrayLikeObject(value)` | Like `_.isArrayLike` but also checks if `value` is an object. |
| `_.isBoolean(value)` | Checks if `value` is a boolean primitive or object. |
| `_.isBuffer(value)` | Checks if `value` is a buffer. |
| `_.isDate(value)` | Checks if `value` is classified as a `Date` object. |
| `_.isElement(value)` | Checks if `value` is likely a DOM element. |
| `_.isEmpty(value)` | Checks if `value` is an empty object, collection, map, or set. |
| `_.isEqual(value, other)` | Performs a deep comparison between two values. |
| `_.isEqualWith(value, other, [customizer])` | Like `_.isEqual` but accepts a `customizer` function. |
| `_.isError(value)` | Checks if `value` is an `Error` object. |
| `_.isFinite(value)` | Checks if `value` is a finite primitive number. |
| `_.isFunction(value)` | Checks if `value` is classified as a `Function` object. |
| `_.isInteger(value)` | Checks if `value` is an integer. |
| `_.isLength(value)` | Checks if `value` is a valid array-like length. |
| `_.isMap(value)` | Checks if `value` is classified as a `Map` object. |
| `_.isMatch(object, source)` | Performs a partial deep comparison between `object` and `source`. |
| `_.isMatchWith(object, source, [customizer])` | Like `_.isMatch` but accepts a `customizer` function. |
| `_.isNaN(value)` | Checks if `value` is `NaN`. |
| `_.isNative(value)` | Checks if `value` is a pristine native function. |
| `_.isNil(value)` | Checks if `value` is `null` or `undefined`. |
| `_.isNull(value)` | Checks if `value` is `null`. |
| `_.isNumber(value)` | Checks if `value` is a `Number` primitive or object. |
| `_.isObject(value)` | Checks if `value` is the language type of `Object`. |
| `_.isObjectLike(value)` | Checks if `value` is object-like. |
| `_.isPlainObject(value)` | Checks if `value` is a plain object. |
| `_.isRegExp(value)` | Checks if `value` is a `RegExp` object. |
| `_.isSafeInteger(value)` | Checks if `value` is a safe integer. |
| `_.isSet(value)` | Checks if `value` is a `Set` object. |
| `_.isString(value)` | Checks if `value` is a `String` primitive or object. |
| `_.isSymbol(value)` | Checks if `value` is a `Symbol` primitive or object. |
| `_.isTypedArray(value)` | Checks if `value` is a typed array. |
| `_.isUndefined(value)` | Checks if `value` is `undefined`. |
| `_.isWeakMap(value)` | Checks if `value` is a `WeakMap` object. |
| `_.isWeakSet(value)` | Checks if `value` is a `WeakSet` object. |
| `_.lt(value, other)` | Checks if `value` is less than `other`. |
| `_.lte(value, other)` | Checks if `value` is less than or equal to `other`. |
| `_.toArray(value)` | Converts `value` to an array. |
| `_.toFinite(value)` | Converts `value` to a finite number. |
| `_.toInteger(value)` | Converts `value` to an integer. |
| `_.toLength(value)` | Converts `value` to an integer suitable for use as a length. |
| `_.toNumber(value)` | Converts `value` to a number. |
| `_.toPlainObject(value)` | Converts `value` to a plain object. |
| `_.toSafeInteger(value)` | Converts `value` to a safe integer. |
| `_.toString(value)` | Converts `value` to a string. |

---

### _.castArray(value)

Casts `value` as an array if it's not one.

#### Since
4.4.0

#### Parameters

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to inspect. |

#### Returns

`(Array)`: Returns the cast array.

#### Example

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

---

### _.clone(value)

Creates a shallow clone of `value`. Note: This method is loosely based on the [structured clone algorithm](https://mdn.io/Structured_clone_algorithm) and supports cloning arrays, array buffers, booleans, date objects, maps, numbers, `Object` objects, regexes, sets, strings, symbols, and typed arrays. The own enumerable properties of `arguments` objects are cloned as plain objects. An empty object is returned for uncloneable values such as error objects, functions, DOM nodes, and WeakMaps.

#### Since
0.1.0

#### Parameters

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to clone. |

#### Returns

`(*)`: Returns the cloned value.

#### Example

```javascript
var objects = [{ 'a': 1 }, { 'b': 2 }];

var shallow = _.clone(objects);
console.log(shallow[0] === objects[0]);
// => true
```

---

### _.cloneWith(value, [customizer])

This method is like `_.clone` except that it accepts `customizer` which is invoked to produce the cloned value. If `customizer` returns `undefined`, cloning is handled by the method instead. The `customizer` is invoked with up to four arguments; (value [, index|key, object, stack]).

#### Since
4.0.0

#### Parameters

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to clone. |
| `[customizer]` | `Function` | The function to customize cloning. |

#### Returns

`(*)`: Returns the cloned value.

#### Example

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

---

### _.cloneDeep(value)

This method is like `_.clone` except that it recursively clones `value`.

#### Since
1.0.0

#### Parameters

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to recursively clone. |

#### Returns

`(*)`: Returns the deep cloned value.

#### Example

```javascript
var objects = [{ 'a': 1 }, { 'b': 2 }];

var deep = _.cloneDeep(objects);
console.log(deep[0] === objects[0]);
// => false
```

---

### _.cloneDeepWith(value, [customizer])

This method is like `_.cloneWith` except that it recursively clones `value`.

#### Since
4.0.0

#### Parameters

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to recursively clone. |
| `[customizer]` | `Function` | The function to customize cloning. |

#### Returns

`(*)`: Returns the deep cloned value.

#### Example

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
// => 20 (or your page's body child node count)
```

---

### _.conformsTo(object, source)

Checks if `object` conforms to `source` by invoking the predicate properties of `source` with the corresponding property values of `object`.

#### Since
4.14.0

#### Parameters

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | The object to inspect. |
| `source` | `Object` | The object of property predicates to conform to. |

#### Returns

`(boolean)`: Returns `true` if `object` conforms, else `false`.

#### Example

```javascript
var object = { 'a': 1, 'b': 2 };

_.conformsTo(object, { 'b': function(n) { return n > 1; } });
// => true

_.conformsTo(object, { 'b': function(n) { return n > 2; } });
// => false
```

---

### _.eq(value, other)

Performs a [`SameValueZero`](http://ecma-international.org/ecma-262/7.0/#sec-samevaluezero) comparison between two values to determine if they are equivalent.

#### Since
4.0.0

#### Parameters

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to compare. |
| `other` | `*` | The other value to compare. |

#### Returns

`(boolean)`: Returns `true` if the values are equivalent, else `false`.

#### Example

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

---

### _.isArguments(value)

Checks if `value` is likely an `arguments` object.

#### Since
0.1.0

#### Parameters

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to check. |

#### Returns

`(boolean)`: Returns `true` if `value` is an `arguments` object, else `false`.

#### Example

```javascript
_.isArguments(function() { return arguments; }());
// => true

_.isArguments([1, 2, 3]);
// => false
```

---

### _.isArray(value)

Checks if `value` is classified as an `Array` object.

#### Since
0.1.0

#### Parameters

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to check. |

#### Returns

`(boolean)`: Returns `true` if `value` is an array, else `false`.

#### Example

```javascript
_.isArray([1, 2, 3]);
// => true

_.isArray(document.body.children);
// => false

_.isArray('abc');
// => false
```

---

### _.isEmpty(value)

Checks if `value` is an empty object, collection, map, or set. Objects are considered empty if they have no own enumerable string keyed properties. Array-like values are considered empty if they have a `length` of `0`.

#### Since
0.1.0

#### Parameters

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to check. |

#### Returns

`(boolean)`: Returns `true` if `value` is empty, else `false`.

#### Example

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

---

### _.isEqual(value, other)

Performs a deep comparison between two values to determine if they are equivalent.

#### Since
0.1.0

#### Parameters

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to compare. |
| `other` | `*` | The other value to compare. |

#### Returns

`(boolean)`: Returns `true` if the values are equivalent, else `false`.

#### Example

```javascript
var object = { 'a': 1 };
var other = { 'a': 1 };

_.isEqual(object, other);
// => true

object === other;
// => false
```

---

### _.isError(value)

Checks if `value` is an `Error`, `EvalError`, `RangeError`, `ReferenceError`, `SyntaxError`, `TypeError`, or `URIError` object.

#### Since
3.0.0

#### Parameters

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to check. |

#### Returns

`(boolean)`: Returns `true` if `value` is an error object, else `false`.

#### Example

```javascript
_.isError(new Error);
// => true

_.isError(Error);
// => false
```

---

### _.isNil(value)

Checks if `value` is `null` or `undefined`.

#### Since
4.0.0

#### Parameters

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to check. |

#### Returns

`(boolean)`: Returns `true` if `value` is nullish, else `false`.

#### Example

```javascript
_.isNil(null);
// => true

_.isNil(void 0);
// => true

_.isNil(NaN);
// => false
```

---

### _.toFinite(value)

Converts `value` to a finite number.

#### Since
4.12.0

#### Parameters

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to convert. |

#### Returns

`(number)`: Returns the converted number.

#### Example

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

---

### _.toString(value)

Converts `value` to a string. An empty string is returned for `null` and `undefined` values. The sign of `-0` is preserved.

#### Since
4.0.0

#### Parameters

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to convert. |

#### Returns

`(string)`: Returns the converted string.

#### Example

```javascript
_.toString(null);
// => ''

_.toString(-0);
// => '-0'

_.toString([1, 2, 3]);
// => '1,2,3'
```

This concludes the reference for Lodash's language utilities. For mathematical operations, see the [Math API reference](./api-math.md).
