# Lang

Lodash's 'Lang' category provides a rich set of utility functions for fundamental language-level operations. These include robust type checking, deep and shallow cloning of objects, and various type conversion utilities. These functions form the bedrock for writing predictable and safe JavaScript code.

## Type Checking Utilities

These functions help you determine the type of a JavaScript value. They are essential for writing robust code that can handle different kinds of input gracefully.

<x-cards data-columns="3">
  <x-card data-title="isEqual()" data-icon="lucide:git-compare-arrows">Performs a deep comparison between two values.</x-card>
  <x-card data-title="isArray()" data-icon="lucide:square-brackets">Checks if a value is classified as an Array object.</x-card>
  <x-card data-title="isObject()" data-icon="lucide:braces">Checks if a value is the language type of Object.</x-card>
  <x-card data-title="isString()" data-icon="lucide:type">Checks if a value is a string primitive or object.</x-card>
  <x-card data-title="isNumber()" data-icon="lucide:binary">Checks if a value is a number primitive or object.</x-card>
  <x-card data-title="isFunction()" data-icon="lucide:function-square">Checks if a value is classified as a Function object.</x-card>
  <x-card data-title="isBoolean()" data-icon="lucide:toggle-right">Checks if a value is a boolean primitive or object.</x-card>
  <x-card data-title="isEmpty()" data-icon="lucide:circle-slash">Checks if a value is empty (object, collection, map, or set).</x-card>
  <x-card data-title="isNil()" data-icon="lucide:circle-help">Checks if a value is null or undefined.</x-card>
</x-cards>

### isEqual

Performs a deep comparison between two values to determine if they are equivalent. This method supports comparing arrays, objects, maps, sets, and more. It compares own, not inherited, enumerable properties.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to compare. |
| `other` | `*` | The other value to compare. |

**Returns**

- `(boolean)`: Returns `true` if the values are equivalent, else `false`.

```javascript isEqual Example icon=logos:javascript
var object = { 'a': 1 };
var other = { 'a': 1 };

_.isEqual(object, other);
// => true

console.log(object === other);
// => false
```

### isEmpty

Checks if `value` is an empty object, collection, map, or set. Objects are considered empty if they have no own enumerable string-keyed properties. Array-like values are considered empty if they have a length of 0.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to check. |

**Returns**

- `(boolean)`: Returns `true` if `value` is empty, else `false`.

```javascript isEmpty Example icon=logos:javascript
_.isEmpty(null);
// => true

_.isEmpty({});
// => true

_.isEmpty('');
// => true

_.isEmpty([1, 2, 3]);
// => false

_.isEmpty({ 'a': 1 });
// => false
```

### Other Type Checking Functions

| Function | Description |
|---|---|
| `isArguments(value)` | Checks if `value` is an `arguments` object. |
| `isArray(value)` | Checks if `value` is an `Array`. |
| `isArrayBuffer(value)` | Checks if `value` is an `ArrayBuffer`. |
| `isArrayLike(value)` | Checks if `value` is array-like (e.g., arrays, strings). |
| `isArrayLikeObject(value)` | Like `isArrayLike` but also checks if `value` is an object. |
| `isBoolean(value)` | Checks if `value` is a boolean. |
| `isBuffer(value)` | Checks if `value` is a Buffer. |
| `isDate(value)` | Checks if `value` is a `Date` object. |
| `isElement(value)` | Checks if `value` is a DOM element. |
| `isEqualWith(value, other, [customizer])` | Like `isEqual` but accepts a customizer function. |
| `isError(value)` | Checks if `value` is an `Error` object. |
| `isFinite(value)` | Checks if `value` is a finite primitive number. |
| `isFunction(value)` | Checks if `value` is a `Function`. |
| `isInteger(value)` | Checks if `value` is an integer. |
| `isLength(value)` | Checks if `value` is a valid array-like length. |
| `isMap(value)` | Checks if `value` is a `Map` object. |
| `isMatch(object, source)` | Performs a partial deep comparison to see if `object` contains `source`'s properties. |
| `isMatchWith(object, source, [customizer])` | Like `isMatch` but accepts a customizer function. |
| `isNaN(value)` | Checks if `value` is `NaN`. |
| `isNative(value)` | Checks if `value` is a native function. |
| `isNil(value)` | Checks if `value` is `null` or `undefined`. |
| `isNull(value)` | Checks if `value` is `null`. |
| `isNumber(value)` | Checks if `value` is a number. |
| `isObject(value)` | Checks if `value` is an object (e.g., arrays, functions, objects, regexes). |
| `isObjectLike(value)` | Checks if `value` is object-like (not `null` and `typeof` is 'object'). |
| `isPlainObject(value)` | Checks if `value` is a plain object. |
| `isRegExp(value)` | Checks if `value` is a `RegExp` object. |
| `isSafeInteger(value)` | Checks if `value` is a safe integer. |
| `isSet(value)` | Checks if `value` is a `Set` object. |
| `isString(value)` | Checks if `value` is a string. |
| `isSymbol(value)` | Checks if `value` is a `Symbol`. |
| `isTypedArray(value)` | Checks if `value` is a typed array. |
| `isUndefined(value)` | Checks if `value` is `undefined`. |
| `isWeakMap(value)` | Checks if `value` is a `WeakMap` object. |
| `isWeakSet(value)` | Checks if `value` is a `WeakSet` object. |


## Cloning Utilities

Creating copies of values, especially complex objects and arrays, is a common task. Lodash provides powerful utilities for both shallow and deep cloning.

### clone

Creates a shallow clone of `value`. For objects and arrays, the top-level structure is duplicated, but nested objects and arrays are shared by reference between the original and the clone.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to clone. |

**Returns**

- `(*)`: Returns the shallow cloned value.

```javascript clone Example icon=logos:javascript
var objects = [{ 'a': 1 }, { 'b': 2 }];

var shallow = _.clone(objects);

console.log(shallow[0] === objects[0]);
// => true
```

### cloneDeep

This method is like `_.clone` except that it recursively clones `value`. All nested objects and arrays are also duplicated, creating a completely independent copy.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to recursively clone. |

**Returns**

- `(*)`: Returns the deep cloned value.

```javascript cloneDeep Example icon=logos:javascript
var objects = [{ 'a': 1 }, { 'b': 2 }];
 
var deep = _.cloneDeep(objects);
 
console.log(deep[0] === objects[0]);
// => false
```

### cloneWith & cloneDeepWith

These are advanced versions of `clone` and `cloneDeep` that accept a `customizer` function. This function is invoked to produce the cloned value for each property. If the customizer returns `undefined`, cloning is handled by the standard Lodash logic.

```javascript cloneWith Example icon=logos:javascript
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

## Type Conversion & Casting

These functions convert values from one type to another, such as converting a string to a number or ensuring a value is an array.

### toArray

Converts `value` to an array. It works on array-like values (like `arguments` objects), strings (splits into characters), and objects (extracts values).

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to convert. |

**Returns**

- `(Array)`: Returns the converted array.

```javascript toArray Example icon=logos:javascript
_.toArray({ 'a': 1, 'b': 2 });
// => [1, 2]

_.toArray('abc');
// => ['a', 'b', 'c']

_.toArray(null);
// => []
```

### toNumber

Converts `value` to a number. It can handle strings, symbols, and objects with a `valueOf` method.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to process. |

**Returns**

- `(number)`: Returns the number.

```javascript toNumber Example icon=logos:javascript
_.toNumber(3.2);
// => 3.2

_.toNumber('3.2');
// => 3.2

_.toNumber(Infinity);
// => Infinity

_.toNumber(Symbol.iterator);
// => NaN
```

### Other Conversion Functions

| Function | Description |
|---|---|
| `castArray(value)` | Casts `value` as an array if it's not one. If it's already an array, it's returned as is. |
| `toFinite(value)` | Converts `value` to a finite number. `Infinity` is converted to the largest representable number. |
| `toInteger(value)` | Converts `value` to an integer, truncating any decimal part. |
| `toLength(value)` | Converts `value` to an integer suitable for an array-like length (0 to `MAX_ARRAY_LENGTH`). |
| `toPlainObject(value)` | Converts `value` to a plain object by flattening inherited enumerable properties to own properties. |
| `toSafeInteger(value)` | Converts `value` to a safe integer (within `Number.MIN_SAFE_INTEGER` and `Number.MAX_SAFE_INTEGER`). |
| `toString(value)` | Converts `value` to a string. `null` and `undefined` become empty strings. |

## Comparison Utilities

Perform comparisons between two values.

| Function | Description |
|---|---|
| `eq(value, other)` | Performs a `SameValueZero` comparison (like `===` but `NaN` equals `NaN`). |
| `gt(value, other)` | Checks if `value` is greater than `other`. |
| `gte(value, other)` | Checks if `value` is greater than or equal to `other`. |
| `lt(value, other)` | Checks if `value` is less than `other`. |
| `lte(value, other)` | Checks if `value` is less than or equal to `other`. |

```javascript Comparison Example icon=logos:javascript
_.gt(3, 1);
// => true

_.lte(3, 3);
// => true

_.eq(NaN, NaN);
// => true
```

---

Now that you're familiar with Lodash's language utilities, you may want to explore how to manipulate data structures. Check out the [Math](./api-math.md) functions for numerical operations or dive into the [Object](./api-object.md) section for powerful object manipulation tools.