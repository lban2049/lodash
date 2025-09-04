# Lang

Lodash 的 'Lang' 类别提供了一套基础的语言工具函数。这些函数处理类型检查、值比较、克隆和类型转换等任务，构成了更复杂操作的基础。它们对于编写健壮且可预测的 JavaScript 代码至关重要。

## 函数参考

| Function | Description |
|---|---|
| `_.castArray(value)` | 如果 `value` 不是数组，则将其转换为数组。 |
| `_.clone(value)` | 创建 `value` 的浅克隆。 |
| `_.cloneWith(value, [customizer])` | 与 `_.clone` 类似，但接受 `customizer` 函数。 |
| `_.cloneDeep(value)` | 递归地克隆 `value`。 |
| `_.cloneDeepWith(value, [customizer])` | 与 `_.cloneDeep` 类似，但接受 `customizer` 函数。 |
| `_.conformsTo(object, source)` | 通过调用 `source` 的谓词属性来检查 `object` 是否符合 `source`。 |
| `_.eq(value, other)` | 在两个值之间执行 `SameValueZero` 比较。 |
| `_.gt(value, other)` | 检查 `value` 是否大于 `other`。 |
| `_.gte(value, other)` | 检查 `value` 是否大于或等于 `other`。 |
| `_.isArguments(value)` | 检查 `value` 是否可能是一个 `arguments` 对象。 |
| `_.isArray(value)` | 检查 `value` 是否被归类为 `Array` 对象。 |
| `_.isArrayBuffer(value)` | 检查 `value` 是否被归类为 `ArrayBuffer` 对象。 |
| `_.isArrayLike(value)` | 检查 `value` 是否为类数组。 |
| `_.isArrayLikeObject(value)` | 与 `_.isArrayLike` 类似，但还会检查 `value` 是否为对象。 |
| `_.isBoolean(value)` | 检查 `value` 是布尔原始值还是布尔对象。 |
| `_.isBuffer(value)` | 检查 `value` 是否为缓冲区。 |
| `_.isDate(value)` | 检查 `value` 是否被归类为 `Date` 对象。 |
| `_.isElement(value)` | 检查 `value` 是否可能是一个 DOM 元素。 |
| `_.isEmpty(value)` | 检查 `value` 是否为空对象、集合、映射或集。 |
| `_.isEqual(value, other)` | 在两个值之间执行深度比较。 |
| `_.isEqualWith(value, other, [customizer])` | 与 `_.isEqual` 类似，但接受 `customizer` 函数。 |
| `_.isError(value)` | 检查 `value` 是否为 `Error` 对象。 |
| `_.isFinite(value)` | 检查 `value` 是否为有限的原始数字。 |
| `_.isFunction(value)` | 检查 `value` 是否被归类为 `Function` 对象。 |
| `_.isInteger(value)` | 检查 `value` 是否为整数。 |
| `_.isLength(value)` | 检查 `value` 是否为有效的类数组长度。 |
| `_.isMap(value)` | 检查 `value` 是否被归类为 `Map` 对象。 |
| `_.isMatch(object, source)` | 在 `object` 和 `source` 之间执行部分深度比较。 |
| `_.isMatchWith(object, source, [customizer])` | 与 `_.isMatch` 类似，但接受 `customizer` 函数。 |
| `_.isNaN(value)` | 检查 `value` 是否为 `NaN`。 |
| `_.isNative(value)` | 检查 `value` 是否为原始的本地函数。 |
| `_.isNil(value)` | 检查 `value` 是否为 `null` 或 `undefined`。 |
| `_.isNull(value)` | 检查 `value` 是否为 `null`。 |
| `_.isNumber(value)` | 检查 `value` 是 `Number` 原始值还是对象。 |
| `_.isObject(value)` | 检查 `value` 是否为 `Object` 的语言类型。 |
| `_.isObjectLike(value)` | 检查 `value` 是否为类对象。 |
| `_.isPlainObject(value)` | 检查 `value` 是否为纯对象。 |
| `_.isRegExp(value)` | 检查 `value` 是否为 `RegExp` 对象。 |
| `_.isSafeInteger(value)` | 检查 `value` 是否为安全整数。 |
| `_.isSet(value)` | 检查 `value` 是否为 `Set` 对象。 |
| `_.isString(value)` | 检查 `value` 是 `String` 原始值还是对象。 |
| `_.isSymbol(value)` | 检查 `value` 是 `Symbol` 原始值还是对象。 |
| `_.isTypedArray(value)` | 检查 `value` 是否为类型化数组。 |
| `_.isUndefined(value)` | 检查 `value` 是否为 `undefined`。 |
| `_.isWeakMap(value)` | 检查 `value` 是否为 `WeakMap` 对象。 |
| `_.isWeakSet(value)` | 检查 `value` 是否为 `WeakSet` 对象。 |
| `_.lt(value, other)` | 检查 `value` 是否小于 `other`。 |
| `_.lte(value, other)` | 检查 `value` 是否小于或等于 `other`。 |
| `_.toArray(value)` | 将 `value` 转换为数组。 |
| `_.toFinite(value)` | 将 `value` 转换为有限数。 |
| `_.toInteger(value)` | 将 `value` 转换为整数。 |
| `_.toLength(value)` | 将 `value` 转换为适合用作长度的整数。 |
| `_.toNumber(value)` | 将 `value` 转换为数字。 |
| `_.toPlainObject(value)` | 将 `value` 转换为纯对象。 |
| `_.toSafeInteger(value)` | 将 `value` 转换为安全整数。 |
| `_.toString(value)` | 将 `value` 转换为字符串。 |

---

### _.castArray(value)

如果 `value` 不是数组，则将其转换为数组。

#### 自
4.4.0

#### 参数

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要检查的值。 |

#### 返回

`(Array)`: 返回转换后的数组。

#### 示例

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

创建 `value` 的浅克隆。注意：此方法大致基于[结构化克隆算法](https://mdn.io/Structured_clone_algorithm)，支持克隆数组、数组缓冲区、布尔值、日期对象、映射、数字、`Object` 对象、正则表达式、集合、字符串、符号和类型化数组。`arguments` 对象自身的可枚举属性被克隆为普通对象。对于不可克隆的值，如错误对象、函数、DOM 节点和 WeakMap，将返回一个空对象。

#### 自
0.1.0

#### 参数

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要克隆的值。 |

#### 返回

`(*)`: 返回克隆后的值。

#### 示例

```javascript
var objects = [{ 'a': 1 }, { 'b': 2 }];

var shallow = _.clone(objects);
console.log(shallow[0] === objects[0]);
// => true
```

---

### _.cloneWith(value, [customizer])

此方法与 `_.clone` 类似，不同之处在于它接受 `customizer`，该函数被调用以生成克隆值。如果 `customizer` 返回 `undefined`，则由该方法处理克隆。`customizer` 被调用时最多可传入四个参数：(value [, index|key, object, stack])。

#### 自
4.0.0

#### 参数

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要克隆的值。 |
| `[customizer]` | `Function` | 用于自定义克隆的函数。 |

#### 返回

`(*)`: 返回克隆后的值。

#### 示例

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

此方法与 `_.clone` 类似，不同之处在于它会递归地克隆 `value`。

#### 自
1.0.0

#### 参数

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要递归克隆的值。 |

#### 返回

`(*)`: 返回深克隆后的值。

#### 示例

```javascript
var objects = [{ 'a': 1 }, { 'b': 2 }];

var deep = _.cloneDeep(objects);
console.log(deep[0] === objects[0]);
// => false
```

---

### _.cloneDeepWith(value, [customizer])

此方法与 `_.cloneWith` 类似，不同之处在于它会递归地克隆 `value`。

#### 自
4.0.0

#### 参数

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要递归克隆的值。 |
| `[customizer]` | `Function` | 用于自定义克隆的函数。 |

#### 返回

`(*)`: 返回深克隆后的值。

#### 示例

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

通过使用 `object` 的相应属性值调用 `source` 的谓词属性，检查 `object` 是否符合 `source`。

#### 自
4.14.0

#### 参数

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | 要检查的对象。 |
| `source` | `Object` | 要符合的属性谓词对象。 |

#### 返回

`(boolean)`: 如果 `object` 符合，则返回 `true`，否则返回 `false`。

#### 示例

```javascript
var object = { 'a': 1, 'b': 2 };

_.conformsTo(object, { 'b': function(n) { return n > 1; } });
// => true

_.conformsTo(object, { 'b': function(n) { return n > 2; } });
// => false
```

---

### _.eq(value, other)

在两个值之间执行 [`SameValueZero`](http://ecma-international.org/ecma-262/7.0/#sec-samevaluezero) 比较，以确定它们是否相等。

#### 自
4.0.0

#### 参数

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要比较的值。 |
| `other` | `*` | 要比较的另一个值。 |

#### 返回

`(boolean)`: 如果值相等，则返回 `true`，否则返回 `false`。

#### 示例

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

检查 `value` 是否可能是一个 `arguments` 对象。

#### 自
0.1.0

#### 参数

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要检查的值。 |

#### 返回

`(boolean)`: 如果 `value` 是一个 `arguments` 对象，则返回 `true`，否则返回 `false`。

#### 示例

```javascript
_.isArguments(function() { return arguments; }());
// => true

_.isArguments([1, 2, 3]);
// => false
```

---

### _.isArray(value)

检查 `value` 是否被归类为 `Array` 对象。

#### 自
0.1.0

#### 参数

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要检查的值。 |

#### 返回

`(boolean)`: 如果 `value` 是一个数组，则返回 `true`，否则返回 `false`。

#### 示例

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

检查 `value` 是否为空对象、集合、映射或集。如果对象没有自身的可枚举字符串键属性，则认为该对象为空。如果类数组值的 `length` 为 `0`，则认为该值为空。

#### 自
0.1.0

#### 参数

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要检查的值。 |

#### 返回

`(boolean)`: 如果 `value` 为空，则返回 `true`，否则返回 `false`。

#### 示例

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

在两个值之间执行深度比较，以确定它们是否相等。

#### 自
0.1.0

#### 参数

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要比较的值。 |
| `other` | `*` | 要比较的另一个值。 |

#### 返回

`(boolean)`: 如果值相等，则返回 `true`，否则返回 `false`。

#### 示例

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

检查 `value` 是否为 `Error`、`EvalError`、`RangeError`、`ReferenceError`、`SyntaxError`、`TypeError` 或 `URIError` 对象。

#### 自
3.0.0

#### 参数

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要检查的值。 |

#### 返回

`(boolean)`: 如果 `value` 是一个错误对象，则返回 `true`，否则返回 `false`。

#### 示例

```javascript
_.isError(new Error);
// => true

_.isError(Error);
// => false
```

---

### _.isNil(value)

检查 `value` 是否为 `null` 或 `undefined`。

#### 自
4.0.0

#### 参数

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要检查的值。 |

#### 返回

`(boolean)`: 如果 `value` 为 nullish，则返回 `true`，否则返回 `false`。

#### 示例

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

将 `value` 转换为有限数。

#### 自
4.12.0

#### 参数

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要转换的值。 |

#### 返回

`(number)`: 返回转换后的数字。

#### 示例

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

将 `value` 转换为字符串。对于 `null` 和 `undefined` 值，返回空字符串。`-0` 的符号会被保留。

#### 自
4.0.0

#### 参数

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要转换的值。 |

#### 返回

`(string)`: 返回转换后的字符串。

#### 示例

```javascript
_.toString(null);
// => ''

_.toString(-0);
// => '-0'

_.toString([1, 2, 3]);
// => '1,2,3'
```

以上是 Lodash 语言工具的参考文档。有关数学运算，请参阅 [Math API 参考](./api-math.md)。
