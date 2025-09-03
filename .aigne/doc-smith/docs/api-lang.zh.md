# Lang

Lodash 的 'Lang' 类别为核心 JavaScript 语言操作提供了基础的实用函数。其中包括强大的类型检查（例如 `_.isString`、`_.isObjectLike`）、深浅克隆（`_.clone`、`_.cloneDeep`）以及值比较（`_.isEqual`、`_.gt`）。这些函数通过处理 JavaScript 的许多边缘情况和不一致性，帮助创建更可预测、更可靠的代码。

## 类型检查与比较

这些函数帮助你自信地理解和比较数据。

### _.isArguments
检查 `value` 是否可能是一个 `arguments` 对象。

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要检查的值。 |

**Returns**

- `(boolean)`: 如果 `value` 是一个 `arguments` 对象，则返回 `true`，否则返回 `false`。

**Example**

```javascript
_.isArguments(function() { return arguments; }());
// => true

_.isArguments([1, 2, 3]);
// => false
```

### _.isArray
检查 `value` 是否被归类为 `Array` 对象。

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要检查的值。 |

**Returns**

- `(boolean)`: 如果 `value` 是一个数组，则返回 `true`，否则返回 `false`。

**Example**

```javascript
_.isArray([1, 2, 3]);
// => true

_.isArray('abc');
// => false
```

### _.isArrayBuffer
检查 `value` 是否被归类为 `ArrayBuffer` 对象。

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要检查的值。 |

**Returns**

- `(boolean)`: 如果 `value` 是一个数组缓冲区，则返回 `true`，否则返回 `false`。

**Example**

```javascript
_.isArrayBuffer(new ArrayBuffer(2));
// => true

_.isArrayBuffer(new Array(2));
// => false
```

### _.isArrayLike
检查 `value` 是否是类数组。如果一个值不是函数，并且其 `value.length` 是一个大于或等于 `0` 且小于或等于 `Number.MAX_SAFE_INTEGER` 的整数，那么该值被认为是类数组。

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要检查的值。 |

**Returns**

- `(boolean)`: 如果 `value` 是类数组，则返回 `true`，否则返回 `false`。

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
该方法类似于 `_.isArrayLike`，但它还会检查 `value` 是否是一个对象。

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要检查的值。 |

**Returns**

- `(boolean)`: 如果 `value` 是一个类数组对象，则返回 `true`，否则返回 `false`。

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
检查 `value` 是否被归类为布尔原始值或对象。

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要检查的值。 |

**Returns**

- `(boolean)`: 如果 `value` 是一个布尔值，则返回 `true`，否则返回 `false`。

**Example**

```javascript
_.isBoolean(false);
// => true

_.isBoolean(null);
// => false
```

### _.isBuffer
检查 `value` 是否是缓冲区。

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要检查的值。 |

**Returns**

- `(boolean)`: 如果 `value` 是一个缓冲区，则返回 `true`，否则返回 `false`。

**Example**

```javascript
_.isBuffer(new Buffer(2));
// => true

_.isBuffer(new Uint8Array(2));
// => false
```

### _.isDate
检查 `value` 是否被归类为 `Date` 对象。

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要检查的值。 |

**Returns**

- `(boolean)`: 如果 `value` 是一个日期对象，则返回 `true`，否则返回 `false`。

**Example**

```javascript
_.isDate(new Date);
// => true

_.isDate('Mon April 23 2012');
// => false
```

### _.isElement
检查 `value` 是否可能是一个 DOM 元素。

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要检查的值。 |

**Returns**

- `(boolean)`: 如果 `value` 是一个 DOM 元素，则返回 `true`，否则返回 `false`。

**Example**

```javascript
_.isElement(document.body);
// => true

_.isElement('<body>');
// => false
```

### _.isEmpty
检查 `value` 是否是空对象、集合、映射或集。

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要检查的值。 |

**Returns**

- `(boolean)`: 如果 `value` 为空，则返回 `true`，否则返回 `false`。

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
在两个值之间执行深度比较，以确定它们是否相等。

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要比较的值。 |
| `other` | `*` | 要比较的另一个值。 |

**Returns**

- `(boolean)`: 如果值相等，则返回 `true`，否则返回 `false`。

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
该方法类似于 `_.isEqual`，但它接受 `customizer`，`customizer` 会被调用以比较值。如果 `customizer` 返回 `undefined`，则由该方法处理比较。

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要比较的值。 |
| `other` | `*` | 要比较的另一个值。 |
| `customizer` | `Function` | 用于自定义比较的函数。 |

**Returns**

- `(boolean)`: 如果值相等，则返回 `true`，否则返回 `false`。

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
检查 `value` 是否是 `Error`、`EvalError`、`RangeError`、`ReferenceError`、`SyntaxError`、`TypeError` 或 `URIError` 对象。

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要检查的值。 |

**Returns**

- `(boolean)`: 如果 `value` 是一个错误对象，则返回 `true`，否则返回 `false`。

**Example**

```javascript
_.isError(new Error);
// => true

_.isError(Error);
// => false
```

### _.isFinite
检查 `value` 是否是有限的原始数字。

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要检查的值。 |

**Returns**

- `(boolean)`: 如果 `value` 是一个有限数，则返回 `true`，否则返回 `false`。

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
检查 `value` 是否被归类为 `Function` 对象。

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要检查的值。 |

**Returns**

- `(boolean)`: 如果 `value` 是一个函数，则返回 `true`，否则返回 `false`。

**Example**

```javascript
_.isFunction(_);
// => true

_.isFunction(/abc/);
// => false
```

### _.isInteger
检查 `value` 是否是整数。

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要检查的值。 |

**Returns**

- `(boolean)`: 如果 `value` 是一个整数，则返回 `true`，否则返回 `false`。

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
检查 `value` 是否是有效的类数组长度。

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要检查的值。 |

**Returns**

- `(boolean)`: 如果 `value` 是一个有效的长度，则返回 `true`，否则返回 `false`。

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
检查 `value` 是否被归类为 `Map` 对象。

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要检查的值。 |

**Returns**

- `(boolean)`: 如果 `value` 是一个 map，则返回 `true`，否则返回 `false`。

**Example**

```javascript
_.isMap(new Map());
// => true

_.isMap(new WeakMap());
// => false
```

### _.isMatch
在 `object` 和 `source` 之间执行部分深度比较，以确定 `object` 是否包含相等的属性值。

**Parameters**

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | 要检查的对象。 |
| `source` | `Object` | 要匹配的属性值对象。 |

**Returns**

- `(boolean)`: 如果 `object` 匹配，则返回 `true`，否则返回 `false`。

**Example**

```javascript
var object = { 'a': 1, 'b': 2 };

_.isMatch(object, { 'b': 2 });
// => true

_.isMatch(object, { 'b': 1 });
// => false
```

### _.isMatchWith
该方法类似于 `_.isMatch`，但它接受 `customizer`，`customizer` 会被调用以比较值。

**Parameters**

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | 要检查的对象。 |
| `source` | `Object` | 要匹配的属性值对象。 |
| `customizer` | `Function` | 用于自定义比较的函数。 |

**Returns**

- `(boolean)`: 如果 `object` 匹配，则返回 `true`，否则返回 `false`。

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
检查 `value` 是否是 `NaN`。

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要检查的值。 |

**Returns**

- `(boolean)`: 如果 `value` 是 `NaN`，则返回 `true`，否则返回 `false`。

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
检查 `value` 是否是原始的本地函数。

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要检查的值。 |

**Returns**

- `(boolean)`: 如果 `value` 是一个本地函数，则返回 `true`，否则返回 `false`。

**Example**

```javascript
_.isNative(Array.prototype.push);
// => true

_.isNative(_);
// => false
```

### _.isNil
检查 `value` 是否是 `null` 或 `undefined`。

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要检查的值。 |

**Returns**

- `(boolean)`: 如果 `value` 是 `null` 或 `undefined`，则返回 `true`，否则返回 `false`。

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
检查 `value` 是否是 `null`。

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要检查的值。 |

**Returns**

- `(boolean)`: 如果 `value` 是 `null`，则返回 `true`，否则返回 `false`。

**Example**

```javascript
_.isNull(null);
// => true

_.isNull(void 0);
// => false
```

### _.isNumber
检查 `value` 是否被归类为 `Number` 原始值或对象。

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要检查的值。 |

**Returns**

- `(boolean)`: 如果 `value` 是一个数字，则返回 `true`，否则返回 `false`。

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
检查 `value` 是否是 `Object` 语言类型（例如，数组、函数、对象、正则表达式、`new Number(0)` 和 `new String('')`）。

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要检查的值。 |

**Returns**

- `(boolean)`: 如果 `value` 是一个对象，则返回 `true`，否则返回 `false`。

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
检查 `value` 是否是类对象。如果一个值不是 `null` 且其 `typeof` 结果为 "object"，则该值是类对象。

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要检查的值。 |

**Returns**

- `(boolean)`: 如果 `value` 是类对象，则返回 `true`，否则返回 `false`。

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
检查 `value` 是否是普通对象，即由 `Object` 构造函数创建的对象或 `[[Prototype]]` 为 `null` 的对象。

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要检查的值。 |

**Returns**

- `(boolean)`: 如果 `value` 是一个普通对象，则返回 `true`，否则返回 `false`。

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
检查 `value` 是否被归类为 `RegExp` 对象。

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要检查的值。 |

**Returns**

- `(boolean)`: 如果 `value` 是一个正则表达式，则返回 `true`，否则返回 `false`。

**Example**

```javascript
_.isRegExp(/abc/);
// => true

_.isRegExp('/abc/');
// => false
```

### _.isSafeInteger
检查 `value` 是否是安全整数。

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要检查的值。 |

**Returns**

- `(boolean)`: 如果 `value` 是一个安全整数，则返回 `true`，否则返回 `false`。

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
检查 `value` 是否被归类为 `Set` 对象。

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要检查的值。 |

**Returns**

- `(boolean)`: 如果 `value` 是一个 set，则返回 `true`，否则返回 `false`。

**Example**

```javascript
_.isSet(new Set());
// => true

_.isSet(new WeakSet());
// => false
```

### _.isString
检查 `value` 是否被归类为 `String` 原始值或对象。

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要检查的值。 |

**Returns**

- `(boolean)`: 如果 `value` 是一个字符串，则返回 `true`，否则返回 `false`。

**Example**

```javascript
_.isString('abc');
// => true

_.isString(1);
// => false
```

### _.isSymbol
检查 `value` 是否被归类为 `Symbol` 原始值或对象。

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要检查的值。 |

**Returns**

- `(boolean)`: 如果 `value` 是一个 symbol，则返回 `true`，否则返回 `false`。

**Example**

```javascript
_.isSymbol(Symbol.iterator);
// => true

_.isSymbol('abc');
// => false
```

### _.isTypedArray
检查 `value` 是否被归类为类型化数组。

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要检查的值。 |

**Returns**

- `(boolean)`: 如果 `value` 是一个类型化数组，则返回 `true`，否则返回 `false`。

**Example**

```javascript
_.isTypedArray(new Uint8Array());
// => true

_.isTypedArray([]);
// => false
```

### _.isUndefined
检查 `value` 是否是 `undefined`。

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要检查的值。 |

**Returns**

- `(boolean)`: 如果 `value` 是 `undefined`，则返回 `true`，否则返回 `false`。

**Example**

```javascript
_.isUndefined(void 0);
// => true

_.isUndefined(null);
// => false
```

### _.isWeakMap
检查 `value` 是否被归类为 `WeakMap` 对象。

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要检查的值。 |

**Returns**

- `(boolean)`: 如果 `value` 是一个弱映射，则返回 `true`，否则返回 `false`。

**Example**

```javascript
_.isWeakMap(new WeakMap());
// => true

_.isWeakMap(new Map());
// => false
```

### _.isWeakSet
检查 `value` 是否被归类为 `WeakSet` 对象。

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要检查的值。 |

**Returns**

- `(boolean)`: 如果 `value` 是一个弱集，则返回 `true`，否则返回 `false`。

**Example**

```javascript
_.isWeakSet(new WeakSet());
// => true

_.isWeakSet(new Set());
// => false
```

### _.lt
检查 `value` 是否小于 `other`。

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要比较的值。 |
| `other` | `*` | 要比较的另一个值。 |

**Returns**

- `(boolean)`: 如果 `value` 小于 `other`，则返回 `true`，否则返回 `false`。

**Example**

```javascript
_.lt(1, 3);
// => true

_.lt(3, 3);
// => false
```

### _.lte
检查 `value` 是否小于或等于 `other`。

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要比较的值。 |
| `other` | `*` | 要比较的另一个值。 |

**Returns**

- `(boolean)`: 如果 `value` 小于或等于 `other`，则返回 `true`，否则返回 `false`。

**Example**

```javascript
_.lte(1, 3);
// => true

_.lte(3, 3);
// => true
```

## 克隆

创建值的浅拷贝或深拷贝。

### _.clone
创建 `value` 的浅克隆。

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要克隆的值。 |

**Returns**

- `(*)`: 返回克隆后的值。

**Example**

```javascript
var objects = [{ 'a': 1 }, { 'b': 2 }];

var shallow = _.clone(objects);
console.log(shallow[0] === objects[0]);
// => true
```

### _.cloneWith
该方法类似于 `_.clone`，但它接受 `customizer`，`customizer` 会被调用以生成克隆值。

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要克隆的值。 |
| `customizer` | `Function` | 用于自定义克隆的函数。 |

**Returns**

- `(*)`: 返回克隆后的值。

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
该方法类似于 `_.clone`，但它会递归地克隆 `value`。

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要递归克隆的值。 |

**Returns**

- `(*)`: 返回深克隆后的值。

**Example**

```javascript
var objects = [{ 'a': 1 }, { 'b': 2 }];

var deep = _.cloneDeep(objects);
console.log(deep[0] === objects[0]);
// => false
```

### _.cloneDeepWith
该方法类似于 `_.cloneWith`，但它会递归地克隆 `value`。

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要递归克隆的值。 |
| `customizer` | `Function` | 用于自定义克隆的函数。 |

**Returns**

- `(*)`: 返回深克隆后的值。

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

## 类型转换

将值从一种类型转换为另一种类型。

### _.castArray
如果 `value` 不是数组，则将其转换为数组。

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要检查的值。 |

**Returns**

- `(Array)`: 返回转换后的数组。

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
将 `value` 转换为数组。

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要转换的值。 |

**Returns**

- `(Array)`: 返回转换后的数组。

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
将 `value` 转换为有限数。

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要转换的值。 |

**Returns**

- `(number)`: 返回转换后的数字。

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
将 `value` 转换为整数。

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要转换的值。 |

**Returns**

- `(number)`: 返回转换后的整数。

**Example**

```javascript
_.toInteger(3.2);
// => 3

_.toInteger('3.2');
// => 3
```

### _.toLength
将 `value` 转换为适合用作类数组对象长度的整数。

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要转换的值。 |

**Returns**

- `(number)`: 返回转换后的整数。

**Example**

```javascript
_.toLength(3.2);
// => 3

_.toLength(Infinity);
// => 4294967295
```

### _.toNumber
将 `value` 转换为数字。

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要处理的值。 |

**Returns**

- `(number)`: 返回数字。

**Example**

```javascript
_.toNumber(3.2);
// => 3.2

_.toNumber('3.2');
// => 3.2
```

### _.toPlainObject
将 `value` 转换为普通对象，将 `value` 的可继承、可枚举的字符串键控属性展平为普通对象的自身属性。

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要转换的值。 |

**Returns**

- `(Object)`: 返回转换后的普通对象。

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
将 `value` 转换为安全整数。

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要转换的值。 |

**Returns**

- `(number)`: 返回转换后的整数。

**Example**

```javascript
_.toSafeInteger(3.2);
// => 3

_.toSafeInteger(Infinity);
// => 9007199254740991
```

### _.toString
将 `value` 转换为字符串。对于 `null` 和 `undefined` 值，返回空字符串。

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要转换的值。 |

**Returns**

- `(string)`: 返回转换后的字符串。

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

掌握了这些语言实用工具后，你可能想探索用于处理特定数据类型的函数，例如 [Math](./api-math.md) 或 [String](./api-string.md)。