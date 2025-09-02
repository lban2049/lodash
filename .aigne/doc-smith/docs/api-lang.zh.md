# Lang

Lang 类别下的函数提供了一系列核心的 JavaScript 语言工具，主要用于类型检查（例如 `_.isNumber`, `_.isArray`），值的比较（例如 `_.isEqual`, `_.gt`），以及对象的克隆（例如 `_.clone`, `_.cloneDeep`）。这些基础函数是构建更复杂逻辑的基石。

## castArray

如果 `value` 不是数组，则将其转换为数组。

**Since**
4.4.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要检查的值。 |

**返回**

- `(Array)`: 返回转换后的数组。

**示例**

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

创建一个 `value` 的浅拷贝。支持克隆数组、数组缓冲区、布尔值、日期对象、map、数字、`Object` 对象、正则表达式、set、字符串、符号和类型化数组。`arguments` 对象的可枚举属性被克隆为普通对象。对于不可克隆的值（如错误对象、函数、DOM 节点和 WeakMaps），返回一个空对象。

**Since**
0.1.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要克隆的值。 |

**返回**

- `(*)`: 返回克隆后的值。

**示例**

```javascript
var objects = [{ 'a': 1 }, { 'b': 2 }];

var shallow = _.clone(objects);
console.log(shallow[0] === objects[0]);
// => true
```

## cloneDeep

此方法类似于 `_.clone`，但它会递归地克隆 `value`。

**Since**
1.0.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要递归克隆的值。 |

**返回**

- `(*)`: 返回深度克隆后的值。

**示例**

```javascript
var objects = [{ 'a': 1 }, { 'b': 2 }];

var deep = _.cloneDeep(objects);
console.log(deep[0] === objects[0]);
// => false
```

## cloneDeepWith

此方法类似于 `_.cloneWith`，但它会递归地克隆 `value`。

**Since**
4.0.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要递归克隆的值。 |
| `customizer` | `Function` | （可选）自定义克隆的函数。 |

**返回**

- `(*)`: 返回深度克隆后的值。

**示例**

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

此方法类似于 `_.clone`，但它接受 `customizer`，该函数被调用以产生克隆的值。如果 `customizer` 返回 `undefined`，则由该方法处理克隆。`customizer` 最多可被调用四个参数：(value [, index|key, object, stack])。

**Since**
4.0.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要克隆的值。 |
| `customizer` | `Function` | （可选）自定义克隆的函数。 |

**返回**

- `(*)`: 返回克隆后的值。

**示例**

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

通过调用 `source` 的谓词属性与 `object` 的相应属性值来检查 `object` 是否符合 `source`。

**Since**
4.14.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `object` | `Object` | 要检查的对象。 |
| `source` | `Object` | 属性谓词的对象。 |

**返回**

- `(boolean)`: 如果 `object` 符合，则返回 `true`，否则返回 `false`。

**示例**

```javascript
var object = { 'a': 1, 'b': 2 };

_.conformsTo(object, { 'b': function(n) { return n > 1; } });
// => true

_.conformsTo(object, { 'b': function(n) { return n > 2; } });
// => false
```

## eq

在两个值之间执行 `SameValueZero` 比较以确定它们是否相等。

**Since**
4.0.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要比较的值。 |
| `other` | `*` | 另一个要比较的值。 |

**返回**

- `(boolean)`: 如果值相等则返回 `true`，否则返回 `false`。

**示例**

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

检查 `value` 是否大于 `other`。

**Since**
3.9.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要比较的值。 |
| `other` | `*` | 另一个要比较的值。 |

**返回**

- `(boolean)`: 如果 `value` 大于 `other`，则返回 `true`，否则返回 `false`。

**示例**

```javascript
_.gt(3, 1);
// => true

_.gt(3, 3);
// => false

_.gt(1, 3);
// => false
```

## gte

检查 `value` 是否大于或等于 `other`。

**Since**
3.9.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要比较的值。 |
| `other` | `*` | 另一个要比较的值。 |

**返回**

- `(boolean)`: 如果 `value` 大于或等于 `other`，则返回 `true`，否则返回 `false`。

**示例**

```javascript
_.gte(3, 1);
// => true

_.gte(3, 3);
// => true

_.gte(1, 3);
// => false
```

## isArguments

检查 `value` 是否可能是一个 `arguments` 对象。

**Since**
0.1.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要检查的值。 |

**返回**

- `(boolean)`: 如果 `value` 是一个 `arguments` 对象，则返回 `true`，否则返回 `false`。

**示例**

```javascript
_.isArguments(function() { return arguments; }());
// => true

_.isArguments([1, 2, 3]);
// => false
```

## isArray

检查 `value` 是否被归类为 `Array` 对象。

**Since**
0.1.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要检查的值。 |

**返回**

- `(boolean)`: 如果 `value` 是一个数组，则返回 `true`，否则返回 `false`。

**示例**

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

检查 `value` 是否被归类为 `ArrayBuffer` 对象。

**Since**
4.3.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要检查的值。 |

**返回**

- `(boolean)`: 如果 `value` 是一个数组缓冲区，则返回 `true`，否则返回 `false`。

**示例**

```javascript
_.isArrayBuffer(new ArrayBuffer(2));
// => true

_.isArrayBuffer(new Array(2));
// => false
```

## isArrayLike

检查 `value` 是否是类数组。如果一个值不是函数并且具有一个大于或等于 `0` 且小于或等于 `Number.MAX_SAFE_INTEGER` 的整数 `value.length`，则该值被认为是类数组。

**Since**
4.0.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要检查的值。 |

**返回**

- `(boolean)`: 如果 `value` 是类数组，则返回 `true`，否则返回 `false`。

**示例**

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

此方法类似于 `_.isArrayLike`，但它还会检查 `value` 是否为对象。

**Since**
4.0.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要检查的值。 |

**返回**

- `(boolean)`: 如果 `value` 是一个类数组对象，则返回 `true`，否则返回 `false`。

**示例**

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

检查 `value` 是否被归类为布尔基元或对象。

**Since**
0.1.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要检查的值。 |

**返回**

- `(boolean)`: 如果 `value` 是一个布尔值，则返回 `true`，否则返回 `false`。

**示例**

```javascript
_.isBoolean(false);
// => true

_.isBoolean(null);
// => false
```

## isBuffer

检查 `value` 是否是一个 buffer。

**Since**
4.3.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要检查的值。 |

**返回**

- `(boolean)`: 如果 `value` 是一个 buffer，则返回 `true`，否则返回 `false`。

**示例**

```javascript
_.isBuffer(new Buffer(2));
// => true

_.isBuffer(new Uint8Array(2));
// => false
```

## isDate

检查 `value` 是否被归类为 `Date` 对象。

**Since**
0.1.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要检查的值。 |

**返回**

- `(boolean)`: 如果 `value` 是一个日期对象，则返回 `true`，否则返回 `false`。

**示例**

```javascript
_.isDate(new Date);
// => true

_.isDate('Mon April 23 2012');
// => false
```

## isElement

检查 `value` 是否可能是一个 DOM 元素。

**Since**
0.1.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要检查的值。 |

**返回**

- `(boolean)`: 如果 `value` 是一个 DOM 元素，则返回 `true`，否则返回 `false`。

**示例**

```javascript
_.isElement(document.body);
// => true

_.isElement('<body>');
// => false
```

## isEmpty

检查 `value` 是否为空对象、集合、map 或 set。如果对象没有自己的可枚举字符串键属性，则认为对象为空。类数组值（如 `arguments` 对象、数组、缓冲区、字符串或类 jQuery 集合）如果 `length` 为 `0`，则认为为空。同样，如果 map 和 set 的 `size` 为 `0`，则认为为空。

**Since**
0.1.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要检查的值。 |

**返回**

- `(boolean)`: 如果 `value` 为空，则返回 `true`，否则返回 `false`。

**示例**

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

执行两个值之间的深度比较以确定它们是否相等。支持比较数组、数组缓冲区、布尔值、日期对象、错误对象、map、数字、`Object` 对象、正则表达式、set、字符串、符号和类型化数组。`Object` 对象通过其自身的（而非继承的）可枚举属性进行比较。函数和 DOM 节点通过严格相等（`===`）进行比较。

**Since**
0.1.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要比较的值。 |
| `other` | `*` | 另一个要比较的值。 |

**返回**

- `(boolean)`: 如果值相等，则返回 `true`，否则返回 `false`。

**示例**

```javascript
var object = { 'a': 1 };
var other = { 'a': 1 };

_.isEqual(object, other);
// => true

object === other;
// => false
```

## isEqualWith

此方法类似于 `_.isEqual`，但它接受 `customizer`，该函数被调用以比较值。如果 `customizer` 返回 `undefined`，则由该方法处理比较。`customizer` 最多可被调用六个参数：(objValue, othValue [, index|key, object, other, stack])。

**Since**
4.0.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要比较的值。 |
| `other` | `*` | 另一个要比较的值。 |
| `customizer` | `Function` | （可选）自定义比较的函数。 |

**返回**

- `(boolean)`: 如果值相等，则返回 `true`，否则返回 `false`。

**示例**

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

检查 `value` 是否为 `Error`、`EvalError`、`RangeError`、`ReferenceError`、`SyntaxError`、`TypeError` 或 `URIError` 对象。

**Since**
3.0.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要检查的值。 |

**返回**

- `(boolean)`: 如果 `value` 是一个错误对象，则返回 `true`，否则返回 `false`。

**示例**

```javascript
_.isError(new Error);
// => true

_.isError(Error);
// => false
```

## isFinite

检查 `value` 是否为有限的原始数字。

**Since**
0.1.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要检查的值。 |

**返回**

- `(boolean)`: 如果 `value` 是一个有限数字，则返回 `true`，否则返回 `false`。

**示例**

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

检查 `value` 是否被归类为 `Function` 对象。

**Since**
0.1.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要检查的值。 |

**返回**

- `(boolean)`: 如果 `value` 是一个函数，则返回 `true`，否则返回 `false`。

**示例**

```javascript
_.isFunction(_);
// => true

_.isFunction(/abc/);
// => false
```

## isInteger

检查 `value` 是否为整数。

**Since**
4.0.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要检查的值。 |

**返回**

- `(boolean)`: 如果 `value` 是一个整数，则返回 `true`，否则返回 `false`。

**示例**

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

检查 `value` 是否为有效的类数组长度。

**Since**
4.0.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要检查的值。 |

**返回**

- `(boolean)`: 如果 `value` 是一个有效的长度，则返回 `true`，否则返回 `false`。

**示例**

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

检查 `value` 是否被归类为 `Map` 对象。

**Since**
4.3.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要检查的值。 |

**返回**

- `(boolean)`: 如果 `value` 是一个 map，则返回 `true`，否则返回 `false`。

**示例**

```javascript
_.isMap(new Map);
// => true

_.isMap(new WeakMap);
// => false
```

## isMatch

执行 `object` 和 `source` 之间的部分深度比较，以确定 `object` 是否包含相等的属性值。

**Since**
3.0.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `object` | `Object` | 要检查的对象。 |
| `source` | `Object` | 要匹配的属性值的对象。 |

**返回**

- `(boolean)`: 如果 `object` 匹配，则返回 `true`，否则返回 `false`。

**示例**

```javascript
var object = { 'a': 1, 'b': 2 };

_.isMatch(object, { 'b': 2 });
// => true

_.isMatch(object, { 'b': 1 });
// => false
```

## isMatchWith

此方法类似于 `_.isMatch`，但它接受 `customizer`，该函数被调用以比较值。如果 `customizer` 返回 `undefined`，则由该方法处理比较。`customizer` 最多可被调用五个参数：(objValue, srcValue, index|key, object, source)。

**Since**
4.0.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `object` | `Object` | 要检查的对象。 |
| `source` | `Object` | 要匹配的属性值的对象。 |
| `customizer` | `Function` | （可选）自定义比较的函数。 |

**返回**

- `(boolean)`: 如果 `object` 匹配，则返回 `true`，否则返回 `false`。

**示例**

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

检查 `value` 是否为 `NaN`。注意：此方法与全局 `isNaN` 不同，全局 `isNaN` 对 `undefined` 和其他非数字值返回 `true`。

**Since**
0.1.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要检查的值。 |

**返回**

- `(boolean)`: 如果 `value` 是 `NaN`，则返回 `true`，否则返回 `false`。

**示例**

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

检查 `value` 是否为原始的本地函数。

**Since**
3.0.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要检查的值。 |

**返回**

- `(boolean)`: 如果 `value` 是一个本地函数，则返回 `true`，否则返回 `false`。

**示例**

```javascript
_.isNative(Array.prototype.push);
// => true

_.isNative(_);
// => false
```

## isNil

检查 `value` 是否为 `null` 或 `undefined`。

**Since**
4.0.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要检查的值。 |

**返回**

- `(boolean)`: 如果 `value` 是 nullish，则返回 `true`，否则返回 `false`。

**示例**

```javascript
_.isNil(null);
// => true

_.isNil(void 0);
// => true

_.isNil(NaN);
// => false
```

## isNull

检查 `value` 是否为 `null`。

**Since**
0.1.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要检查的值。 |

**返回**

- `(boolean)`: 如果 `value` 是 `null`，则返回 `true`，否则返回 `false`。

**示例**

```javascript
_.isNull(null);
// => true

_.isNull(void 0);
// => false
```

## isNumber

检查 `value` 是否被归类为 `Number` 基元或对象。要排除 `Infinity`、`-Infinity` 和 `NaN`，请使用 `_.isFinite` 方法。

**Since**
0.1.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要检查的值。 |

**返回**

- `(boolean)`: 如果 `value` 是一个数字，则返回 `true`，否则返回 `false`。

**示例**

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

检查 `value` 是否为 `Object` 的语言类型（例如数组、函数、对象、正则表达式、`new Number(0)` 和 `new String('')`）。

**Since**
0.1.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要检查的值。 |

**返回**

- `(boolean)`: 如果 `value` 是一个对象，则返回 `true`，否则返回 `false`。

**示例**

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

检查 `value` 是否是类对象。如果一个值不是 `null` 且 `typeof` 结果为 `"object"`，则该值是类对象的。

**Since**
4.0.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要检查的值。 |

**返回**

- `(boolean)`: 如果 `value` 是类对象，则返回 `true`，否则返回 `false`。

**示例**

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

检查 `value` 是否为普通对象，即由 `Object` 构造函数创建或具有 `[[Prototype]]` 为 `null` 的对象。

**Since**
0.8.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要检查的值。 |

**返回**

- `(boolean)`: 如果 `value` 是一个普通对象，则返回 `true`，否则返回 `false`。

**示例**

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

检查 `value` 是否被归类为 `RegExp` 对象。

**Since**
0.1.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要检查的值。 |

**返回**

- `(boolean)`: 如果 `value` 是一个正则表达式，则返回 `true`，否则返回 `false`。

**示例**

```javascript
_.isRegExp(/abc/);
// => true

_.isRegExp('/abc/');
// => false
```

## isSafeInteger

检查 `value` 是否为安全整数。如果一个整数是 IEEE-754 双精度数且不是舍入不安全整数的结果，则该整数是安全的。

**Since**
4.0.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要检查的值。 |

**返回**

- `(boolean)`: 如果 `value` 是一个安全整数，则返回 `true`，否则返回 `false`。

**示例**

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

检查 `value` 是否被归类为 `Set` 对象。

**Since**
4.3.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要检查的值。 |

**返回**

- `(boolean)`: 如果 `value` 是一个 set，则返回 `true`，否则返回 `false`。

**示例**

```javascript
_.isSet(new Set);
// => true

_.isSet(new WeakSet);
// => false
```

## isString

检查 `value` 是否被归类为 `String` 基元或对象。

**Since**
0.1.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要检查的值。 |

**返回**

- `(boolean)`: 如果 `value` 是一个字符串，则返回 `true`，否则返回 `false`。

**示例**

```javascript
_.isString('abc');
// => true

_.isString(1);
// => false
```

## isSymbol

检查 `value` 是否被归类为 `Symbol` 基元或对象。

**Since**
4.0.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要检查的值。 |

**返回**

- `(boolean)`: 如果 `value` 是一个符号，则返回 `true`，否则返回 `false`。

**示例**

```javascript
_.isSymbol(Symbol.iterator);
// => true

_.isSymbol('abc');
// => false
```

## isTypedArray

检查 `value` 是否被归类为类型化数组。

**Since**
3.0.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要检查的值。 |

**返回**

- `(boolean)`: 如果 `value` 是一个类型化数组，则返回 `true`，否则返回 `false`。

**示例**

```javascript
_.isTypedArray(new Uint8Array);
// => true

_.isTypedArray([]);
// => false
```

## isUndefined

检查 `value` 是否为 `undefined`。

**Since**
0.1.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要检查的值。 |

**返回**

- `(boolean)`: 如果 `value` 是 `undefined`，则返回 `true`，否则返回 `false`。

**示例**

```javascript
_.isUndefined(void 0);
// => true

_.isUndefined(null);
// => false
```

## isWeakMap

检查 `value` 是否被归类为 `WeakMap` 对象。

**Since**
4.3.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要检查的值。 |

**返回**

- `(boolean)`: 如果 `value` 是一个弱映射，则返回 `true`，否则返回 `false`。

**示例**

```javascript
_.isWeakMap(new WeakMap);
// => true

_.isWeakMap(new Map);
// => false
```

## isWeakSet

检查 `value` 是否被归类为 `WeakSet` 对象。

**Since**
4.3.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要检查的值。 |

**返回**

- `(boolean)`: 如果 `value` 是一个弱集合，则返回 `true`，否则返回 `false`。

**示例**

```javascript
_.isWeakSet(new WeakSet);
// => true

_.isWeakSet(new Set);
// => false
```

## lt

检查 `value` 是否小于 `other`。

**Since**
3.9.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要比较的值。 |
| `other` | `*` | 另一个要比较的值。 |

**返回**

- `(boolean)`: 如果 `value` 小于 `other`，则返回 `true`，否则返回 `false`。

**示例**

```javascript
_.lt(1, 3);
// => true

_.lt(3, 3);
// => false

_.lt(3, 1);
// => false
```

## lte

检查 `value` 是否小于或等于 `other`。

**Since**
3.9.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要比较的值。 |
| `other` | `*` | 另一个要比较的值。 |

**返回**

- `(boolean)`: 如果 `value` 小于或等于 `other`，则返回 `true`，否则返回 `false`。

**示例**

```javascript
_.lte(1, 3);
// => true

_.lte(3, 3);
// => true

_.lte(3, 1);
// => false
```

## toArray

将 `value` 转换为数组。

**Since**
0.1.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要转换的值。 |

**返回**

- `(Array)`: 返回转换后的数组。

**示例**

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

将 `value` 转换为一个有限数。

**Since**
4.12.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要转换的值。 |

**返回**

- `(number)`: 返回转换后的数字。

**示例**

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

将 `value` 转换为一个整数。

**Since**
4.0.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要转换的值。 |

**返回**

- `(number)`: 返回转换后的整数。

**示例**

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

将 `value` 转换为一个适合用作类数组对象长度的整数。

**Since**
4.0.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要转换的值。 |

**返回**

- `(number)`: 返回转换后的整数。

**示例**

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

将 `value` 转换为一个数字。

**Since**
4.0.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要处理的值。 |

**返回**

- `(number)`: 返回数字。

**示例**

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

将 `value` 转换为一个普通对象，将 `value` 的继承的可枚举字符串键属性扁平化为普通对象的自身属性。

**Since**
3.0.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要转换的值。 |

**返回**

- `(Object)`: 返回转换后的普通对象。

**示例**

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

将 `value` 转换为一个安全整数。安全整数可以被正确比较和表示。

**Since**
4.0.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要转换的值。 |

**返回**

- `(number)`: 返回转换后的整数。

**示例**

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

将 `value` 转换为一个字符串。对于 `null` 和 `undefined` 值返回一个空字符串。`-0` 的符号会被保留。

**Since**
4.0.0

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要转换的值。 |

**返回**

- `(string)`: 返回转换后的字符串。

**示例**

```javascript
_.toString(null);
// => ''

_.toString(-0);
// => '-0'

_.toString([1, 2, 3]);
// => '1,2,3'
```

---

本节介绍了 Lodash 的核心语言工具函数。要了解更多关于数值计算的函数，请参阅 [Math API](./api-math.md) 部分。
