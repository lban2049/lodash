# Lang

Lodash's `Lang` category provides a suite of fundamental utility functions that handle language-level operations. These functions are essential for tasks such as type checking, value comparison, cloning, and type casting. They form the bedrock of many complex operations and help ensure code is robust and predictable.

Whether you need to verify if a variable is an array, perform a deep clone of an object, or safely convert a value to a number, the functions in this section offer reliable and optimized solutions. For more specialized object manipulations, see the [Object](./api-object.md) section.

## Type Checking

These functions help you determine the type of a JavaScript value.

### isArguments

Checks if `value` is likely an `arguments` object.

**Parameters**

<x-field data-name="value" data-type="any" data-required="true" data-desc="The value to check."></x-field>

**Returns**

<x-field data-name="" data-type="boolean" data-desc="Returns true if value is an arguments object, else false."></x-field>

**Example**

```javascript
_.isArguments(function() { return arguments; }());
// => true

_.isArguments([1, 2, 3]);
// => false
```

### isArray

Checks if `value` is classified as an `Array` object.

**Parameters**

<x-field data-name="value" data-type="any" data-required="true" data-desc="The value to check."></x-field>

**Returns**

<x-field data-name="" data-type="boolean" data-desc="Returns true if value is an array, else false."></x-field>

**Example**

```javascript
_.isArray([1, 2, 3]);
// => true

_.isArray('abc');
// => false
```

### isArrayBuffer

Checks if `value` is classified as an `ArrayBuffer` object.

**Parameters**

<x-field data-name="value" data-type="any" data-required="true" data-desc="The value to check."></x-field>

**Returns**

<x-field data-name="" data-type="boolean" data-desc="Returns true if value is an ArrayBuffer, else false."></x-field>

**Example**

```javascript
_.isArrayBuffer(new ArrayBuffer(2));
// => true

_.isArrayBuffer(new Array(2));
// => false
```

### isArrayLike

Checks if `value` is array-like. A value is considered array-like if it's not a function and has a `value.length` that's an integer greater than or equal to `0` and less than or equal to `Number.MAX_SAFE_INTEGER`.

**Parameters**

<x-field data-name="value" data-type="any" data-required="true" data-desc="The value to check."></x-field>

**Returns**

<x-field data-name="" data-type="boolean" data-desc="Returns true if value is array-like, else false."></x-field>

**Example**

```javascript
_.isArrayLike([1, 2, 3]);
// => true

_.isArrayLike('abc');
// => true

_.isArrayLike(_.noop);
// => false
```

### isBoolean

Checks if `value` is classified as a boolean primitive or object.

**Parameters**

<x-field data-name="value" data-type="any" data-required="true" data-desc="The value to check."></x-field>

**Returns**

<x-field data-name="" data-type="boolean" data-desc="Returns true if value is a boolean, else false."></x-field>

**Example**

```javascript
_.isBoolean(false);
// => true

_.isBoolean(null);
// => false
```

### isDate

Checks if `value` is classified as a `Date` object.

**Parameters**

<x-field data-name="value" data-type="any" data-required="true" data-desc="The value to check."></x-field>

**Returns**

<x-field data-name="" data-type="boolean" data-desc="Returns true if value is a Date object, else false."></x-field>

**Example**

```javascript
_.isDate(new Date());
// => true

_.isDate('Mon April 23 2012');
// => false
```

### isEmpty

Checks if `value` is an empty object, collection, map, or set.

Objects are considered empty if they have no own enumerable string keyed properties. Array-like values (e.g., `arguments` objects, arrays, strings) are considered empty if they have a `length` of `0`. Maps and sets are considered empty if they have a `size` of `0`.

**Parameters**

<x-field data-name="value" data-type="any" data-required="true" data-desc="The value to check."></x-field>

**Returns**

<x-field data-name="" data-type="boolean" data-desc="Returns true if value is empty, else false."></x-field>

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

### isError

Checks if `value` is an `Error`, `EvalError`, `RangeError`, `ReferenceError`, `SyntaxError`, `TypeError`, or `URIError` object.

**Parameters**

<x-field data-name="value" data-type="any" data-required="true" data-desc="The value to check."></x-field>

**Returns**

<x-field data-name="" data-type="boolean" data-desc="Returns true if value is an error object, else false."></x-field>

**Example**

```javascript
_.isError(new Error());
// => true

_.isError(Error);
// => false
```

### isFunction

Checks if `value` is classified as a `Function` object.

**Parameters**

<x-field data-name="value" data-type="any" data-required="true" data-desc="The value to check."></x-field>

**Returns**

<x-field data-name="" data-type="boolean" data-desc="Returns true if value is a function, else false."></x-field>

**Example**

```javascript
_.isFunction(_);
// => true

_.isFunction(/abc/);
// => false
```

### isNil

Checks if `value` is `null` or `undefined`.

**Parameters**

<x-field data-name="value" data-type="any" data-required="true" data-desc="The value to check."></x-field>

**Returns**

<x-field data-name="" data-type="boolean" data-desc="Returns true if value is nullish, else false."></x-field>

**Example**

```javascript
_.isNil(null);
// => true

_.isNil(void 0);
// => true

_.isNil(NaN);
// => false
```

### isNull

Checks if `value` is `null`.

**Parameters**

<x-field data-name="value" data-type="any" data-required="true" data-desc="The value to check."></x-field>

**Returns**

<x-field data-name="" data-type="boolean" data-desc="Returns true if value is null, else false."></x-field>

**Example**

```javascript
_.isNull(null);
// => true

_.isNull(void 0);
// => false
```

### isNumber

Checks if `value` is classified as a `Number` primitive or object. To exclude `Infinity`, `-Infinity`, and `NaN`, use `_.isFinite`.

**Parameters**

<x-field data-name="value" data-type="any" data-required="true" data-desc="The value to check."></x-field>

**Returns**

<x-field data-name="" data-type="boolean" data-desc="Returns true if value is a number, else false."></x-field>

**Example**

```javascript
_.isNumber(3);
// => true

_.isNumber(Infinity);
// => true

_.isNumber('3');
// => false
```

### isObject

Checks if `value` is the language type of `Object` (e.g., arrays, functions, objects, regexes, `new Number(0)`, and `new String('')`).

**Parameters**

<x-field data-name="value" data-type="any" data-required="true" data-desc="The value to check."></x-field>

**Returns**

<x-field data-name="" data-type="boolean" data-desc="Returns true if value is an object, else false."></x-field>

**Example**

```javascript
_.isObject({});
// => true

_.isObject([1, 2, 3]);
// => true

_.isObject(null);
// => false
```

### isPlainObject

Checks if `value` is a plain object, i.e., an object created by the `Object` constructor or one with a `[[Prototype]]` of `null`.

**Parameters**

<x-field data-name="value" data-type="any" data-required="true" data-desc="The value to check."></x-field>

**Returns**

<x-field data-name="" data-type="boolean" data-desc="Returns true if value is a plain object, else false."></x-field>

**Example**

```javascript
function Foo() {
  this.a = 1;
}

_.isPlainObject(new Foo());
// => false

_.isPlainObject({ 'x': 0, 'y': 0 });
// => true
```

### isString

Checks if `value` is classified as a `String` primitive or object.

**Parameters**

<x-field data-name="value" data-type="any" data-required="true" data-desc="The value to check."></x-field>

**Returns**

<x-field data-name="" data-type="boolean" data-desc="Returns true if value is a string, else false."></x-field>

**Example**

```javascript
_.isString('abc');
// => true

_.isString(1);
// => false
```

### isSymbol

Checks if `value` is classified as a `Symbol` primitive or object.

**Parameters**

<x-field data-name="value" data-type="any" data-required="true" data-desc="The value to check."></x-field>

**Returns**

<x-field data-name="" data-type="boolean" data-desc="Returns true if value is a symbol, else false."></x-field>

**Example**

```javascript
_.isSymbol(Symbol.iterator);
// => true

_.isSymbol('abc');
// => false
```

### isUndefined

Checks if `value` is `undefined`.

**Parameters**

<x-field data-name="value" data-type="any" data-required="true" data-desc="The value to check."></x-field>

**Returns**

<x-field data-name="" data-type="boolean" data-desc="Returns true if value is undefined, else false."></x-field>

**Example**

```javascript
_.isUndefined(void 0);
// => true

_.isUndefined(null);
// => false
```

## Cloning

Create shallow or deep copies of values.

### clone

Creates a shallow clone of `value`. This method supports cloning arrays, booleans, date objects, maps, numbers, `Object` objects, regexes, sets, strings, symbols, and typed arrays.

**Parameters**

<x-field data-name="value" data-type="any" data-required="true" data-desc="The value to clone."></x-field>

**Returns**

<x-field data-name="" data-type="any" data-desc="Returns the cloned value."></x-field>

**Example**

```javascript
var objects = [{ 'a': 1 }, { 'b': 2 }];

var shallow = _.clone(objects);
console.log(shallow[0] === objects[0]);
// => true
```

### cloneDeep

This method is like `_.clone` except that it recursively clones `value`.

**Parameters**

<x-field data-name="value" data-type="any" data-required="true" data-desc="The value to recursively clone."></x-field>

**Returns**

<x-field data-name="" data-type="any" data-desc="Returns the deep cloned value."></x-field>

**Example**

```javascript
var objects = [{ 'a': 1 }, { 'b': 2 }];

var deep = _.cloneDeep(objects);
console.log(deep[0] === objects[0]);
// => false
```

### cloneWith

Like `_.clone`, but accepts a `customizer` function to produce the cloned value. If `customizer` returns `undefined`, cloning is handled by the method.

**Parameters**

<x-field data-name="value" data-type="any" data-required="true" data-desc="The value to clone."></x-field>
<x-field data-name="customizer" data-type="Function" data-required="false" data-desc="The function to customize cloning."></x-field>

**Returns**

<x-field data-name="" data-type="any" data-desc="Returns the cloned value."></x-field>

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
```

### cloneDeepWith

Like `_.cloneWith`, but it recursively clones `value`.

**Parameters**

<x-field data-name="value" data-type="any" data-required="true" data-desc="The value to recursively clone."></x-field>
<x-field data-name="customizer" data-type="Function" data-required="false" data-desc="The function to customize cloning."></x-field>

**Returns**

<x-field data-name="" data-type="any" data-desc="Returns the deep cloned value."></x-field>

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

## Comparison & Conformance

Functions for comparing values and checking object structures.

### eq

Performs a [`SameValueZero`](http://ecma-international.org/ecma-262/7.0/#sec-samevaluezero) comparison between two values to determine if they are equivalent. This means `NaN` is equal to `NaN`.

**Parameters**

<x-field data-name="value" data-type="any" data-required="true" data-desc="The value to compare."></x-field>
<x-field data-name="other" data-type="any" data-required="true" data-desc="The other value to compare."></x-field>

**Returns**

<x-field data-name="" data-type="boolean" data-desc="Returns true if the values are equivalent, else false."></x-field>

**Example**

```javascript
_.eq('a', 'a');
// => true

_.eq('a', Object('a'));
// => false

_.eq(NaN, NaN);
// => true
```

### isEqual

Performs a deep comparison between two values to determine if they are equivalent.

**Parameters**

<x-field data-name="value" data-type="any" data-required="true" data-desc="The value to compare."></x-field>
<x-field data-name="other" data-type="any" data-required="true" data-desc="The other value to compare."></x-field>

**Returns**

<x-field data-name="" data-type="boolean" data-desc="Returns true if the values are equivalent, else false."></x-field>

**Example**

```javascript
var object = { 'a': 1 };
var other = { 'a': 1 };

_.isEqual(object, other);
// => true

object === other;
// => false
```

### gt, gte, lt, lte

These functions perform relational comparisons between two values.

- `gt(value, other)`: Checks if `value` is greater than `other`.
- `gte(value, other)`: Checks if `value` is greater than or equal to `other`.
- `lt(value, other)`: Checks if `value` is less than `other`.
- `lte(value, other)`: Checks if `value` is less than or equal to `other`.

**Example**

```javascript
_.gt(3, 1);
// => true

_.gte(3, 3);
// => true

_.lt(1, 3);
// => true

_.lte(1, 3);
// => true
```

## Type Casting & Conversion

Functions to convert values from one type to another.

### castArray

Casts `value` as an array if it's not one. If `value` is already an array, it's returned as is.

**Parameters**

<x-field data-name="value" data-type="any" data-required="true" data-desc="The value to inspect."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns the cast array."></x-field>

**Example**

```javascript
_.castArray(1);
// => [1]

_.castArray({ 'a': 1 });
// => [{ 'a': 1 }]

var array = [1, 2, 3];
_.castArray(array) === array;
// => true
```

### toArray

Converts `value` to an array. For array-like values or strings, it creates a new array. For objects, it creates an array of the object's values.

**Parameters**

<x-field data-name="value" data-type="any" data-required="true" data-desc="The value to convert."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns the converted array."></x-field>

**Example**

```javascript
_.toArray({ 'a': 1, 'b': 2 });
// => [1, 2]

_.toArray('abc');
// => ['a', 'b', 'c']
```

### toNumber

Converts `value` to a number.

**Parameters**

<x-field data-name="value" data-type="any" data-required="true" data-desc="The value to process."></x-field>

**Returns**

<x-field data-name="" data-type="number" data-desc="Returns the number."></x-field>

**Example**

```javascript
_.toNumber(3.2);
// => 3.2

_.toNumber('3.2');
// => 3.2

_.toNumber(Infinity);
// => Infinity
```

### toString

Converts `value` to a string. An empty string is returned for `null` and `undefined` values. The sign of `-0` is preserved.

**Parameters**

<x-field data-name="value" data-type="any" data-required="true" data-desc="The value to convert."></x-field>

**Returns**

<x-field data-name="" data-type="string" data-desc="Returns the converted string."></x-field>

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

This section covers the core language utilities in Lodash. Mastering these functions will help you write cleaner and more reliable code. To learn about manipulating object properties, continue to the [Object](./api-object.md) documentation.