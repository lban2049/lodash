# Lang

Lodash 的 `Lang` 类别提供了一套处理语言级别操作的基础工具函数。这些函数对于类型检查、值比较、克隆和类型转换等任务至关重要。它们构成了许多复杂操作的基石，有助于确保代码的健壮性和可预测性。

无论你需要验证一个变量是否为数组、对一个对象执行深克隆，还是安全地将一个值转换为数字，本节中的函数都能提供可靠且经过优化的解决方案。如需了解更专门的对象操作，请参阅 [Object](./api-object.md) 部分。

## 类型检查

这些函数可帮助你确定 JavaScript 值的类型。

### isArguments

检查 `value` 是否可能是一个 `arguments` 对象。

**参数**

<x-field data-name="value" data-type="any" data-required="true" data-desc="要检查的值。"></x-field>

**返回值**

<x-field data-name="" data-type="boolean" data-desc="如果 value 是一个 arguments 对象，则返回 true，否则返回 false。"></x-field>

**示例**

```javascript
_.isArguments(function() { return arguments; }());
// => true

_.isArguments([1, 2, 3]);
// => false
```

### isArray

检查 `value` 是否归类为 `Array` 对象。

**参数**

<x-field data-name="value" data-type="any" data-required="true" data-desc="要检查的值。"></x-field>

**返回值**

<x-field data-name="" data-type="boolean" data-desc="如果 value 是一个数组，则返回 true，否则返回 false。"></x-field>

**示例**

```javascript
_.isArray([1, 2, 3]);
// => true

_.isArray('abc');
// => false
```

### isArrayBuffer

检查 `value` 是否归类为 `ArrayBuffer` 对象。

**参数**

<x-field data-name="value" data-type="any" data-required="true" data-desc="要检查的值。"></x-field>

**返回值**

<x-field data-name="" data-type="boolean" data-desc="如果 value 是一个 ArrayBuffer，则返回 true，否则返回 false。"></x-field>

**示例**

```javascript
_.isArrayBuffer(new ArrayBuffer(2));
// => true

_.isArrayBuffer(new Array(2));
// => false
```

### isArrayLike

检查 `value` 是否是类数组。如果一个值不是函数，并且其 `value.length` 是一个大于或等于 `0` 且小于或等于 `Number.MAX_SAFE_INTEGER` 的整数，那么它就被认为是类数组。

**参数**

<x-field data-name="value" data-type="any" data-required="true" data-desc="要检查的值。"></x-field>

**返回值**

<x-field data-name="" data-type="boolean" data-desc="如果 value 是类数组，则返回 true，否则返回 false。"></x-field>

**示例**

```javascript
_.isArrayLike([1, 2, 3]);
// => true

_.isArrayLike('abc');
// => true

_.isArrayLike(_.noop);
// => false
```

### isBoolean

检查 `value` 是否归类为布尔基元或对象。

**参数**

<x-field data-name="value" data-type="any" data-required="true" data-desc="要检查的值。"></x-field>

**返回值**

<x-field data-name="" data-type="boolean" data-desc="如果 value 是一个布尔值，则返回 true，否则返回 false。"></x-field>

**示例**

```javascript
_.isBoolean(false);
// => true

_.isBoolean(null);
// => false
```

### isDate

检查 `value` 是否归类为 `Date` 对象。

**参数**

<x-field data-name="value" data-type="any" data-required="true" data-desc="要检查的值。"></x-field>

**返回值**

<x-field data-name="" data-type="boolean" data-desc="如果 value 是一个 Date 对象，则返回 true，否则返回 false。"></x-field>

**示例**

```javascript
_.isDate(new Date());
// => true

_.isDate('Mon April 23 2012');
// => false
```

### isEmpty

检查 `value` 是否为空对象、集合、Map 或 Set。

如果对象自身没有可枚举的字符串键属性，则该对象被认为是空的。类数组值（如 `arguments` 对象、数组、字符串）的 `length` 为 `0` 时被认为是空的。Map 和 Set 的 `size` 为 `0` 时被认为是空的。

**参数**

<x-field data-name="value" data-type="any" data-required="true" data-desc="要检查的值。"></x-field>

**返回值**

<x-field data-name="" data-type="boolean" data-desc="如果 value 为空，则返回 true，否则返回 false。"></x-field>

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

### isError

检查 `value` 是否是 `Error`、`EvalError`、`RangeError`、`ReferenceError`、`SyntaxError`、`TypeError` 或 `URIError` 对象。

**参数**

<x-field data-name="value" data-type="any" data-required="true" data-desc="要检查的值。"></x-field>

**返回值**

<x-field data-name="" data-type="boolean" data-desc="如果 value 是一个错误对象，则返回 true，否则返回 false。"></x-field>

**示例**

```javascript
_.isError(new Error());
// => true

_.isError(Error);
// => false
```

### isFunction

检查 `value` 是否归类为 `Function` 对象。

**参数**

<x-field data-name="value" data-type="any" data-required="true" data-desc="要检查的值。"></x-field>

**返回值**

<x-field data-name="" data-type="boolean" data-desc="如果 value 是一个函数，则返回 true，否则返回 false。"></x-field>

**示例**

```javascript
_.isFunction(_);
// => true

_.isFunction(/abc/);
// => false
```

### isNil

检查 `value` 是否为 `null` 或 `undefined`。

**参数**

<x-field data-name="value" data-type="any" data-required="true" data-desc="要检查的值。"></x-field>

**返回值**

<x-field data-name="" data-type="boolean" data-desc="如果 value 是 nullish，则返回 true，否则返回 false。"></x-field>

**示例**

```javascript
_.isNil(null);
// => true

_.isNil(void 0);
// => true

_.isNil(NaN);
// => false
```

### isNull

检查 `value` 是否为 `null`。

**参数**

<x-field data-name="value" data-type="any" data-required="true" data-desc="要检查的值。"></x-field>

**返回值**

<x-field data-name="" data-type="boolean" data-desc="如果 value 是 null，则返回 true，否则返回 false。"></x-field>

**示例**

```javascript
_.isNull(null);
// => true

_.isNull(void 0);
// => false
```

### isNumber

检查 `value` 是否归类为 `Number` 基元或对象。要排除 `Infinity`、`-Infinity` 和 `NaN`，请使用 `_.isFinite`。

**参数**

<x-field data-name="value" data-type="any" data-required="true" data-desc="要检查的值。"></x-field>

**返回值**

<x-field data-name="" data-type="boolean" data-desc="如果 value 是一个数字，则返回 true，否则返回 false。"></x-field>

**示例**

```javascript
_.isNumber(3);
// => true

_.isNumber(Infinity);
// => true

_.isNumber('3');
// => false
```

### isObject

检查 `value` 是否是 `Object` 语言类型（例如，数组、函数、对象、正则表达式、`new Number(0)` 和 `new String('')`）。

**参数**

<x-field data-name="value" data-type="any" data-required="true" data-desc="要检查的值。"></x-field>

**返回值**

<x-field data-name="" data-type="boolean" data-desc="如果 value 是一个对象，则返回 true，否则返回 false。"></x-field>

**示例**

```javascript
_.isObject({});
// => true

_.isObject([1, 2, 3]);
// => true

_.isObject(null);
// => false
```

### isPlainObject

检查 `value` 是否是纯粹的对象，即由 `Object` 构造函数创建的对象或 `[[Prototype]]` 为 `null` 的对象。

**参数**

<x-field data-name="value" data-type="any" data-required="true" data-desc="要检查的值。"></x-field>

**返回值**

<x-field data-name="" data-type="boolean" data-desc="如果 value 是一个纯粹的对象，则返回 true，否则返回 false。"></x-field>

**示例**

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

检查 `value` 是否归类为 `String` 基元或对象。

**参数**

<x-field data-name="value" data-type="any" data-required="true" data-desc="要检查的值。"></x-field>

**返回值**

<x-field data-name="" data-type="boolean" data-desc="如果 value 是一个字符串，则返回 true，否则返回 false。"></x-field>

**示例**

```javascript
_.isString('abc');
// => true

_.isString(1);
// => false
```

### isSymbol

检查 `value` 是否归类为 `Symbol` 基元或对象。

**参数**

<x-field data-name="value" data-type="any" data-required="true" data-desc="要检查的值。"></x-field>

**返回值**

<x-field data-name="" data-type="boolean" data-desc="如果 value 是一个 symbol，则返回 true，否则返回 false。"></x-field>

**示例**

```javascript
_.isSymbol(Symbol.iterator);
// => true

_.isSymbol('abc');
// => false
```

### isUndefined

检查 `value` 是否为 `undefined`。

**参数**

<x-field data-name="value" data-type="any" data-required="true" data-desc="要检查的值。"></x-field>

**返回值**

<x-field data-name="" data-type="boolean" data-desc="如果 value 是 undefined，则返回 true，否则返回 false。"></x-field>

**示例**

```javascript
_.isUndefined(void 0);
// => true

_.isUndefined(null);
// => false
```

## 克隆

创建值的浅拷贝或深拷贝。

### clone

创建 `value` 的浅克隆。此方法支持克隆数组、布尔值、日期对象、Map、数字、`Object` 对象、正则表达式、Set、字符串、Symbol 和类型化数组。

**参数**

<x-field data-name="value" data-type="any" data-required="true" data-desc="要克隆的值。"></x-field>

**返回值**

<x-field data-name="" data-type="any" data-desc="返回克隆后的值。"></x-field>

**示例**

```javascript
var objects = [{ 'a': 1 }, { 'b': 2 }];

var shallow = _.clone(objects);
console.log(shallow[0] === objects[0]);
// => true
```

### cloneDeep

此方法类似于 `_.clone`，但它会递归地克隆 `value`。

**参数**

<x-field data-name="value" data-type="any" data-required="true" data-desc="要递归克隆的值。"></x-field>

**返回值**

<x-field data-name="" data-type="any" data-desc="返回深度克隆后的值。"></x-field>

**示例**

```javascript
var objects = [{ 'a': 1 }, { 'b': 2 }];

var deep = _.cloneDeep(objects);
console.log(deep[0] === objects[0]);
// => false
```

### cloneWith

与 `_.clone` 类似，但接受一个 `customizer` 函数来生成克隆值。如果 `customizer` 返回 `undefined`，则由该方法处理克隆。

**参数**

<x-field data-name="value" data-type="any" data-required="true" data-desc="要克隆的值。"></x-field>
<x-field data-name="customizer" data-type="Function" data-required="false" data-desc="用于自定义克隆的函数。"></x-field>

**返回值**

<x-field data-name="" data-type="any" data-desc="返回克隆后的值。"></x-field>

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
```

### cloneDeepWith

与 `_.cloneWith` 类似，但它会递归地克隆 `value`。

**参数**

<x-field data-name="value" data-type="any" data-required="true" data-desc="要递归克隆的值。"></x-field>
<x-field data-name="customizer" data-type="Function" data-required="false" data-desc="用于自定义克隆的函数。"></x-field>

**返回值**

<x-field data-name="" data-type="any" data-desc="返回深度克隆后的值。"></x-field>

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
```

## 比较与一致性

用于比较值和检查对象结构的函数。

### eq

在两个值之间执行 [`SameValueZero`](http://ecma-international.org/ecma-262/7.0/#sec-samevaluezero) 比较，以确定它们是否相等。这意味着 `NaN` 等于 `NaN`。

**参数**

<x-field data-name="value" data-type="any" data-required="true" data-desc="要比较的值。"></x-field>
<x-field data-name="other" data-type="any" data-required="true" data-desc="要比较的另一个值。"></x-field>

**返回值**

<x-field data-name="" data-type="boolean" data-desc="如果值相等，则返回 true，否则返回 false。"></x-field>

**示例**

```javascript
_.eq('a', 'a');
// => true

_.eq('a', Object('a'));
// => false

_.eq(NaN, NaN);
// => true
```

### isEqual

在两个值之间执行深度比较，以确定它们是否相等。

**参数**

<x-field data-name="value" data-type="any" data-required="true" data-desc="要比较的值。"></x-field>
<x-field data-name="other" data-type="any" data-required="true" data-desc="要比较的另一个值。"></x-field>

**返回值**

<x-field data-name="" data-type="boolean" data-desc="如果值相等，则返回 true，否则返回 false。"></x-field>

**示例**

```javascript
var object = { 'a': 1 };
var other = { 'a': 1 };

_.isEqual(object, other);
// => true

object === other;
// => false
```

### gt, gte, lt, lte

这些函数在两个值之间执行关系比较。

- `gt(value, other)`: 检查 `value` 是否大于 `other`。
- `gte(value, other)`: 检查 `value` 是否大于或等于 `other`。
- `lt(value, other)`: 检查 `value` 是否小于 `other`。
- `lte(value, other)`: 检查 `value` 是否小于或等于 `other`。

**示例**

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

## 类型转换与转换

用于将值从一种类型转换为另一种类型的函数。

### castArray

如果 `value` 不是数组，则将其转换为数组。如果 `value` 已经是数组，则原样返回。

**参数**

<x-field data-name="value" data-type="any" data-required="true" data-desc="要检查的值。"></x-field>

**返回值**

<x-field data-name="" data-type="Array" data-desc="返回转换后的数组。"></x-field>

**示例**

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

将 `value` 转换为数组。对于类数组值或字符串，它会创建一个新数组。对于对象，它会创建一个包含对象值的数组。

**参数**

<x-field data-name="value" data-type="any" data-required="true" data-desc="要转换的值。"></x-field>

**返回值**

<x-field data-name="" data-type="Array" data-desc="返回转换后的数组。"></x-field>

**示例**

```javascript
_.toArray({ 'a': 1, 'b': 2 });
// => [1, 2]

_.toArray('abc');
// => ['a', 'b', 'c']
```

### toNumber

将 `value` 转换为数字。

**参数**

<x-field data-name="value" data-type="any" data-required="true" data-desc="要处理的值。"></x-field>

**返回值**

<x-field data-name="" data-type="number" data-desc="返回数字。"></x-field>

**示例**

```javascript
_.toNumber(3.2);
// => 3.2

_.toNumber('3.2');
// => 3.2

_.toNumber(Infinity);
// => Infinity
```

### toString

将 `value` 转换为字符串。对于 `null` 和 `undefined` 值，返回空字符串。`-0` 的符号会被保留。

**参数**

<x-field data-name="value" data-type="any" data-required="true" data-desc="要转换的值。"></x-field>

**返回值**

<x-field data-name="" data-type="string" data-desc="返回转换后的字符串。"></x-field>

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

本节介绍了 Lodash 中的核心语言工具。掌握这些函数将帮助你编写更清晰、更可靠的代码。要了解有关操作对象属性的信息，请继续阅读 [Object](./api-object.md) 文档。