# Lang

Lodash 的 'Lang' 类别提供了一套丰富的实用函数，用于执行基本的语言级操作。其中包括稳健的类型检查、对象的深浅克隆以及多种类型转换工具。这些函数是编写可预测且安全的 JavaScript 代码的基石。

## 类型检查工具

这些函数可帮助您确定 JavaScript 值的类型。它们对于编写能够妥善处理不同类型输入的稳健代码至关重要。

<x-cards data-columns="3">
  <x-card data-title="isEqual()" data-icon="lucide:git-compare-arrows">对两个值进行深度比较。</x-card>
  <x-card data-title="isArray()" data-icon="lucide:square-brackets">检查一个值是否为 Array 对象。</x-card>
  <x-card data-title="isObject()" data-icon="lucide:braces">检查一个值是否为 Object 语言类型。</x-card>
  <x-card data-title="isString()" data-icon="lucide:type">检查一个值是字符串原始类型还是对象。</x-card>
  <x-card data-title="isNumber()" data-icon="lucide:binary">检查一个值是数字原始类型还是对象。</x-card>
  <x-card data-title="isFunction()" data-icon="lucide:function-square">检查一个值是否为 Function 对象。</x-card>
  <x-card data-title="isBoolean()" data-icon="lucide:toggle-right">检查一个值是布尔原始类型还是对象。</x-card>
  <x-card data-title="isEmpty()" data-icon="lucide:circle-slash">检查一个值是否为空（对象、集合、map 或 set）。</x-card>
  <x-card data-title="isNil()" data-icon="lucide:circle-help">检查一个值是否为 null 或 undefined。</x-card>
</x-cards>

### isEqual

对两个值进行深度比较，以确定它们是否相等。此方法支持比较数组、对象、map、set 等。它比较的是自身拥有的、非继承而来的可枚举属性。

**参数**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要比较的值。 |
| `other` | `*` | 另一个要比较的值。 |

**返回值**

- `(boolean)`: 如果值相等，则返回 `true`，否则返回 `false`。

```javascript isEqual Example icon=logos:javascript
var object = { 'a': 1 };
var other = { 'a': 1 };

_.isEqual(object, other);
// => true

console.log(object === other);
// => false
```

### isEmpty

检查 `value` 是否为空对象、集合、map 或 set。如果对象没有自身拥有的可枚举字符串键属性，则认为该对象为空。如果类数组值的长度为 0，则认为该值为空。

**参数**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要检查的值。 |

**返回值**

- `(boolean)`: 如果 `value` 为空，则返回 `true`，否则返回 `false`。

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

### 其他类型检查函数

| Function | Description |
|---|---|
| `isArguments(value)` | 检查 `value` 是否为 `arguments` 对象。 |
| `isArray(value)` | 检查 `value` 是否为 `Array`。 |
| `isArrayBuffer(value)` | 检查 `value` 是否为 `ArrayBuffer`。 |
| `isArrayLike(value)` | 检查 `value` 是否为类数组（例如，数组、字符串）。 |
| `isArrayLikeObject(value)` | 与 `isArrayLike` 类似，但同时检查 `value` 是否为对象。 |
| `isBoolean(value)` | 检查 `value` 是否为布尔值。 |
| `isBuffer(value)` | 检查 `value` 是否为 Buffer。 |
| `isDate(value)` | 检查 `value` 是否为 `Date` 对象。 |
| `isElement(value)` | 检查 `value` 是否为 DOM 元素。 |
| `isEqualWith(value, other, [customizer])` | 与 `isEqual` 类似，但接受一个 customizer 函数。 |
| `isError(value)` | 检查 `value` 是否为 `Error` 对象。 |
| `isFinite(value)` | 检查 `value` 是否为有限的原始数字。 |
| `isFunction(value)` | 检查 `value` 是否为 `Function`。 |
| `isInteger(value)` | 检查 `value` 是否为整数。 |
| `isLength(value)` | 检查 `value` 是否为有效的类数组长度。 |
| `isMap(value)` | 检查 `value` 是否为 `Map` 对象。 |
| `isMatch(object, source)` | 执行部分深度比较，以确定 `object` 是否包含 `source` 的属性。 |
| `isMatchWith(object, source, [customizer])` | 与 `isMatch` 类似，但接受一个 customizer 函数。 |
| `isNaN(value)` | 检查 `value` 是否为 `NaN`。 |
| `isNative(value)` | 检查 `value` 是否为原生函数。 |
| `isNil(value)` | 检查 `value` 是否为 `null` 或 `undefined`。 |
| `isNull(value)` | 检查 `value` 是否为 `null`。 |
| `isNumber(value)` | 检查 `value` 是否为数字。 |
| `isObject(value)` | 检查 `value` 是否为对象（例如，数组、函数、对象、正则表达式）。 |
| `isObjectLike(value)` | 检查 `value` 是否为类对象（非 `null` 且 `typeof` 为 'object'）。 |
| `isPlainObject(value)` | 检查 `value` 是否为纯对象。 |
| `isRegExp(value)` | 检查 `value` 是否为 `RegExp` 对象。 |
| `isSafeInteger(value)` | 检查 `value` 是否为安全整数。 |
| `isSet(value)` | 检查 `value` 是否为 `Set` 对象。 |
| `isString(value)` | 检查 `value` 是否为字符串。 |
| `isSymbol(value)` | 检查 `value` 是否为 `Symbol`。 |
| `isTypedArray(value)` | 检查 `value` 是否为类型化数组。 |
| `isUndefined(value)` | 检查 `value` 是否为 `undefined`。 |
| `isWeakMap(value)` | 检查 `value` 是否为 `WeakMap` 对象。 |
| `isWeakSet(value)` | 检查 `value` 是否为 `WeakSet` 对象。 |


## 克隆工具

创建值的副本，尤其是复杂对象和数组的副本，是一项常见任务。Lodash 为浅克隆和深克隆提供了强大的工具。

### clone

创建 `value` 的浅克隆。对于对象和数组，顶层结构会被复制，但嵌套的对象和数组在原始值和克隆值之间通过引用共享。

**参数**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要克隆的值。 |

**返回值**

- `(*)`: 返回浅克隆的值。

```javascript clone Example icon=logos:javascript
var objects = [{ 'a': 1 }, { 'b': 2 }];

var shallow = _.clone(objects);

console.log(shallow[0] === objects[0]);
// => true
```

### cloneDeep

此方法与 `_.clone` 类似，但它会递归地克隆 `value`。所有嵌套的对象和数组也都会被复制，从而创建一个完全独立的副本。

**参数**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要递归克隆的值。 |

**返回值**

- `(*)`: 返回深克隆的值。

```javascript cloneDeep Example icon=logos:javascript
var objects = [{ 'a': 1 }, { 'b': 2 }];
 
var deep = _.cloneDeep(objects);
 
console.log(deep[0] === objects[0]);
// => false
```

### cloneWith & cloneDeepWith

这些是 `clone` 和 `cloneDeep` 的高级版本，它们接受一个 `customizer` 函数。此函数被调用以为每个属性生成克隆值。如果 customizer 返回 `undefined`，则由标准的 Lodash 逻辑处理克隆。

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

## 类型转换与转型

这些函数将值从一种类型转换为另一种类型，例如将字符串转换为数字或确保值是一个数组。

### toArray

将 `value` 转换为数组。它适用于类数组值（如 `arguments` 对象）、字符串（拆分为字符数组）和对象（提取其值）。

**参数**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要转换的值。 |

**返回值**

- `(Array)`: 返回转换后的数组。

```javascript toArray Example icon=logos:javascript
_.toArray({ 'a': 1, 'b': 2 });
// => [1, 2]

_.toArray('abc');
// => ['a', 'b', 'c']

_.toArray(null);
// => []
```

### toNumber

将 `value` 转换为数字。它可以处理字符串、符号以及带有 `valueOf` 方法的对象。

**参数**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要处理的值。 |

**返回值**

- `(number)`: 返回该数字。

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

### 其他转换函数

| Function | Description |
|---|---|
| `castArray(value)` | 如果 `value` 不是数组，则将其转换为数组。如果 `value` 已经是数组，则原样返回。 |
| `toFinite(value)` | 将 `value` 转换为一个有限的数值。`Infinity` 会被转换为可表示的最大数值。 |
| `toInteger(value)` | 将 `value` 转换为整数，并截断任何小数部分。 |
| `toLength(value)` | 将 `value` 转换为适合类数组长度的整数（0 到 `MAX_ARRAY_LENGTH`）。 |
| `toPlainObject(value)` | 通过将继承的可枚举属性扁平化为自有属性，将 `value` 转换为纯对象。 |
| `toSafeInteger(value)` | 将 `value` 转换为安全整数（在 `Number.MIN_SAFE_INTEGER` 和 `Number.MAX_SAFE_INTEGER` 之间）。 |
| `toString(value)` | 将 `value` 转换为字符串。`null` 和 `undefined` 会变成空字符串。 |

## 比较工具

在两个值之间执行比较。

| Function | Description |
|---|---|
| `eq(value, other)` | 执行 `SameValueZero` 比较（类似于 `===`，但 `NaN` 等于 `NaN`）。 |
| `gt(value, other)` | 检查 `value` 是否大于 `other`。 |
| `gte(value, other)` | 检查 `value` 是否大于或等于 `other`。 |
| `lt(value, other)` | 检查 `value` 是否小于 `other`。 |
| `lte(value, other)` | 检查 `value` 是否小于或等于 `other`。 |

```javascript Comparison Example icon=logos:javascript
_.gt(3, 1);
// => true

_.lte(3, 3);
// => true

_.eq(NaN, NaN);
// => true
```

---

现在您已熟悉 Lodash 的语言工具，您可能希望探索如何操作数据结构。您可以查看 [Math](./api-math.md) 函数进行数值运算，或深入 [Object](./api-object.md) 部分了解强大的对象操作工具。