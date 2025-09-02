# API 参考

本节全面介绍了所有 Lodash 方法，并根据其主要数据类型或实用功能进行分类。每个方法条目都提供了其语法、详细参数、预期返回值和实用示例，以助您进行开发。

如需了解 Lodash 的架构和设计原则的基础知识，请参阅[核心概念](./core-concepts.md)部分。如果您对使用 Lodash 进行函数式编程感兴趣，请查阅[函数式编程 (FP)](./functional-programming.md)指南。

## 数组方法

### chunk

创建一个数组，其中的元素按 `size` 的长度分成组。如果 `array` 无法被平均分割，最后一个块将包含剩余的元素。

**参数**

| 名称 | 类型 | 描述 |
|---:|:---:|:---|
| `array` | `Array` | 要处理的数组。 |
| `size` | `number` | 每个块的长度（默认值：1）。 |
| `guard` | `Object` | 允许作为 `_.map` 等方法的迭代器使用。 |

**返回值**

| 名称 | 类型 | 描述 |
|---:|:---:|:---|
| `Array` | `Array` | 返回新的块数组。 |

**示例**

```javascript
_.chunk(['a', 'b', 'c', 'd'], 2);
// => [['a', 'b'], ['c', 'd']]

_.chunk(['a', 'b', 'c', 'd'], 3);
// => [['a', 'b', 'c'], ['d']]
```

此示例演示了 `_.chunk` 如何将数组分割成指定大小的子数组。

### compact

创建一个移除了所有假值的数组。`false`、`null`、`0`、`""`、`undefined` 和 `NaN` 都是假值。

**参数**

| 名称 | 类型 | 描述 |
|---:|:---:|:---|
| `array` | `Array` | 要压缩的数组。 |

**返回值**

| 名称 | 类型 | 描述 |
|---:|:---:|:---|
| `Array` | `Array` | 返回新的过滤值数组。 |

**示例**

```javascript
_.compact([0, 1, false, 2, '', 3]);
// => [1, 2, 3]
```

此示例展示了 `_.compact` 如何从数组中移除所有假值，只保留真值元素。

### head

获取 `array` 的第一个元素。

**参数**

| 名称 | 类型 | 描述 |
|---:|:---:|:---|
| `array` | `Array` | 要查询的数组。 |

**返回值**

| 名称 | 类型 | 描述 |
|---:|:---:|:---|
| `*` | `*` | 返回 `array` 的第一个元素。 |

**示例**

```javascript
_.head([1, 2, 3]);
// => 1

_.head([]);
// => undefined
```

此示例使用 `_.head` 从数组中检索第一个元素。

### tail

获取 `array` 中除第一个元素外的所有元素。

**参数**

| 名称 | 类型 | 描述 |
|---:|:---:|:---|
| `array` | `Array` | 要查询的数组。 |

**返回值**

| 名称 | 类型 | 描述 |
|---:|:---:|:---|
| `Array` | `Array` | 返回 `array` 的切片。 |

**示例**

```javascript
_.tail([1, 2, 3]);
// => [2, 3]
```

此示例演示了 `_.tail` 如何返回数组中除第一个元素外的所有元素。

### union

使用 `SameValueZero` 进行相等比较，从所有给定数组中按顺序创建一个包含唯一值的数组。

**参数**

| 名称 | 类型 | 描述 |
|---:|:---:|:---|
| `arrays` | `Array` | 要检查的数组。 |

**返回值**

| 名称 | 类型 | 描述 |
|---:|:---:|:---|
| `Array` | `Array` | 返回合并后的新数组。 |

**示例**

```javascript
_.union([2], [1, 2]);
// => [2, 1]
```

此示例将两个数组合并成一个只包含唯一值的数组。

## 集合方法

### forEach

遍历 `collection` 的元素，并为每个元素调用 `iteratee`。迭代器使用三个参数调用：(值, 索引|键, 集合)。迭代器函数可以通过显式返回 `false` 来提前退出迭代。

**参数**

| 名称 | 类型 | 描述 |
|---:|:---:|:---|
| `collection` | `Array` \| `Object` | 要迭代的集合。 |
| `iteratee` | `Function` | 每次迭代调用的函数（默认值：`_.identity`）。 |

**返回值**

| 名称 | 类型 | 描述 |
|---:|:---:|:---|
| `collection` | `Array` \| `Object` | 返回 `collection`。 |

**示例**

```javascript
_.forEach([1, 2], function(value) {
  console.log(value);
});
// => Logs `1` then `2`.

_.forEach({ 'a': 1, 'b': 2 }, function(value, key) {
  console.log(key);
});
// => Logs 'a' then 'b' (iteration order is not guaranteed).
```

此示例演示了如何使用 `_.forEach` 遍历数组和对象，并分别记录值或键。

### map

通过对 `collection` 中的每个元素运行 `iteratee` 来创建一个值数组。迭代器使用三个参数调用：(值, 索引|键, 集合)。

**参数**

| 名称 | 类型 | 描述 |
|---:|:---:|:---|
| `collection` | `Array` \| `Object` | 要迭代的集合。 |
| `iteratee` | `Function` | 每次迭代调用的函数（默认值：`_.identity`）。 |

**返回值**

| 名称 | 类型 | 描述 |
|---:|:---:|:---|
| `Array` | `Array` | 返回新的映射数组。 |

**示例**

```javascript
function square(n) {
  return n * n;
}

_.map([4, 8], square);
// => [16, 64]

_.map({ 'a': 4, 'b': 8 }, square);
// => [16, 64] (iteration order is not guaranteed)

var users = [
  { 'user': 'barney' },
  { 'user': 'fred' }
];

// The `_.property` iteratee shorthand.
_.map(users, 'user');
// => ['barney', 'fred']
```

此示例使用 `_.map` 转换数组和对象的元素，应用 `square` 函数或提取属性。

### filter

遍历 `collection` 的元素，返回 `predicate` 返回真值的所有元素的数组。谓词使用三个参数调用：(值, 索引|键, 集合)。

**参数**

| 名称 | 类型 | 描述 |
|---:|:---:|:---|
| `collection` | `Array` \| `Object` | 要迭代的集合。 |
| `predicate` | `Function` | 每次迭代调用的函数（默认值：`_.identity`）。 |

**返回值**

| 名称 | 类型 | 描述 |
|---:|:---:|:---|
| `Array` | `Array` | 返回新的过滤数组。 |

**示例**

```javascript
var users = [
  { 'user': 'barney', 'age': 36, 'active': true },
  { 'user': 'fred',   'age': 40, 'active': false }
];

_.filter(users, function(o) { return !o.active; });
// => objects for ['fred']

// The `_.matches` iteratee shorthand.
_.filter(users, { 'age': 36, 'active': true });
// => objects for ['barney']

// The `_.matchesProperty` iteratee shorthand.
_.filter(users, ['active', false]);
// => objects for ['fred']

// The `_.property` iteratee shorthand.
_.filter(users, 'active');
// => objects for ['barney']
```

此示例演示了如何根据不同的谓词过滤用户对象集合，包括函数、对象匹配、属性匹配和属性存在性。

### reduce

将 `collection` 归约为一个值，该值是通过对 `collection` 中的每个元素运行 `iteratee` 累积的结果，其中每次后续调用都提供前一次的返回值。如果未给出 `accumulator`，则 `collection` 的第一个元素用作初始值。迭代器使用四个参数调用：(累加器, 值, 索引|键, 集合)。

**参数**

| 名称 | 类型 | 描述 |
|---:|:---:|:---|
| `collection` | `Array` \| `Object` | 要迭代的集合。 |
| `iteratee` | `Function` | 每次迭代调用的函数（默认值：`_.identity`）。 |
| `accumulator` | `*` | 初始值。 |

**返回值**

| 名称 | 类型 | 描述 |
|---:|:---:|:---|
| `*` | `*` | 返回累积值。 |

**示例**

```javascript
_.reduce([1, 2], function(sum, n) {
  return sum + n;
}, 0);
// => 3

_.reduce({ 'a': 1, 'b': 2, 'c': 1 }, function(result, value, key) {
  (result[value] || (result[value] = [])).push(key);
  return result;
}, {});
// => { '1': ['a', 'c'], '2': ['b'] } (iteration order is not guaranteed)
```

此示例展示了 `_.reduce` 如何对数组中的数字求和，以及在对象中按值对键进行分组。

## 函数方法

### debounce

创建一个防抖函数，该函数会延迟调用 `func`，直到自上次调用防抖函数后经过 `wait` 毫秒。防抖函数带有 `cancel` 方法以取消延迟的 `func` 调用，以及 `flush` 方法以立即调用它们。

**参数**

| 名称 | 类型 | 描述 |
|---:|:---:|:---|
| `func` | `Function` | 要防抖的函数。 |
| `wait` | `number` | 延迟的毫秒数（默认值：0）。 |
| `options` | `Object` | 选项对象。 |
| `options.leading` | `boolean` | 指定在超时前沿调用（默认值：`false`）。 |
| `options.maxWait` | `number` | `func` 允许延迟的最大时间，在此之后它将被调用。 |
| `options.trailing` | `boolean` | 指定在超时后沿调用（默认值：`true`）。 |

**返回值**

| 名称 | 类型 | 描述 |
|---:|:---:|:---|
| `Function` | `Function` | 返回新的防抖函数。 |

**示例**

```javascript
// Avoid costly calculations while the window size is in flux.
// jQuery(window).on('resize', _.debounce(calculateLayout, 150));

// Invoke `sendMail` when clicked, debouncing subsequent calls.
// jQuery(element).on('click', _.debounce(sendMail, 300, {
//   'leading': true,
//   'trailing': false
// }));

// Ensure `batchLog` is invoked once after 1 second of debounced calls.
// var debounced = _.debounce(batchLog, 250, { 'maxWait': 1000 });
// var source = new EventSource('/stream');
// jQuery(source).on('message', debounced);

// Cancel the trailing debounced invocation.
// jQuery(window).on('popstate', debounced.cancel);
```

此示例（因通常依赖 jQuery 等外部库而被注释掉）说明了 `_.debounce` 如何防止函数被过于频繁地调用，例如在窗口大小调整事件或快速点击时。

### throttle

创建一个节流函数，该函数每 `wait` 毫秒最多只调用 `func` 一次。节流函数带有 `cancel` 方法以取消延迟的 `func` 调用，以及 `flush` 方法以立即调用它们。

**参数**

| 名称 | 类型 | 描述 |
|---:|:---:|:---|
| `func` | `Function` | 要节流的函数。 |
| `wait` | `number` | 节流调用的毫秒数（默认值：0）。 |
| `options` | `Object` | 选项对象。 |
| `options.leading` | `boolean` | 指定在超时前沿调用（默认值：`true`）。 |
| `options.trailing` | `boolean` | 指定在超时后沿调用（默认值：`true`）。 |

**返回值**

| 名称 | 类型 | 描述 |
|---:|:---:|:---|
| `Function` | `Function` | 返回新的节流函数。 |

**示例**

```javascript
// Avoid excessively updating the position while scrolling.
// jQuery(window).on('scroll', _.throttle(updatePosition, 100));

// Invoke `renewToken` when the click event is fired, but not more than once every 5 minutes.
// var throttled = _.throttle(renewToken, 300000, { 'trailing': false });
// jQuery(element).on('click', throttled);

// Cancel the trailing throttled invocation.
// jQuery(window).on('popstate', throttled.cancel);
```

与 `debounce` 类似，此示例（已注释掉）展示了 `_.throttle` 如何限制函数被调用的频率，这对于滚动事件或不应过于频繁的 API 调用非常有用。

### memoize

创建一个函数，该函数会记忆 `func` 的结果。如果提供了 `resolver`，它将根据传递给记忆函数的参数来确定存储结果的缓存键。默认情况下，传递给记忆函数的第一个参数用作映射缓存键。

**参数**

| 名称 | 类型 | 描述 |
|---:|:---:|:---|
| `func` | `Function` | 要对其输出进行记忆的函数。 |
| `resolver` | `Function` | 用于解析缓存键的函数。 |

**返回值**

| 名称 | 类型 | 描述 |
|---:|:---:|:---|
| `Function` | `Function` | 返回新的记忆化函数。 |

**示例**

```javascript
var object = { 'a': 1, 'b': 2 };
var other = { 'c': 3, 'd': 4 };

var values = _.memoize(_.values);
values(object);
// => [1, 2]

values(other);
// => [3, 4]

object.a = 2;
values(object);
// => [1, 2]

// Modify the result cache.
values.cache.set(object, ['a', 'b']);
values(object);
// => ['a', 'b']

// Replace `_.memoize.Cache`.
// _.memoize.Cache = WeakMap;
```

此示例说明了 `_.memoize` 如何缓存 `_.values` 对对象的结果，展示了对同一对象的后续调用如何返回缓存结果，直到缓存被手动修改或替换。

## 语言方法

### isObject

检查 `value` 是否为 `Object` 的语言类型。（例如数组、函数、对象、正则表达式、`new Number(0)` 和 `new String('')`）

**参数**

| 名称 | 类型 | 描述 |
|---:|:---:|:---|
| `value` | `*` | 要检查的值。 |

**返回值**

| 名称 | 类型 | 描述 |
|---:|:---:|:---|
| `boolean` | `boolean` | 如果 `value` 是一个对象，则返回 `true`，否则返回 `false`。 |

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

此示例演示了 `_.isObject` 如何识别各种 JavaScript 对象类型。

### isEqual

对两个值执行 `SameValueZero` 比较以确定它们是否相等。此方法支持比较数组、ArrayBuffer、布尔值、日期对象、错误对象、映射、数字、`Object` 对象、正则表达式、集合、字符串、符号和类型化数组。`Object` 对象通过其自身的（而非继承的）可枚举属性进行比较。函数和 DOM 节点通过严格相等（即 `===`）进行比较。

**参数**

| 名称 | 类型 | 描述 |
|---:|:---:|:---|
| `value` | `*` | 要比较的值。 |
| `other` | `*` | 要比较的另一个值。 |

**返回值**

| 名称 | 类型 | 描述 |
|---:|:---:|:---|
| `boolean` | `boolean` | 如果值相等，则返回 `true`，否则返回 `false`。 |

**示例**

```javascript
var object = { 'a': 1 };
var other = { 'a': 1 };

_.isEqual(object, other);
// => true

object === other;
// => false
```

此示例展示了 `_.isEqual` 执行深度比较，对于结构上相等但不严格相等的对象返回 `true`。

### cloneDeep

递归克隆 `value`。

**参数**

| 名称 | 类型 | 描述 |
|---:|:---:|:---|
| `value` | `*` | 要递归克隆的值。 |

**返回值**

| 名称 | 类型 | 描述 |
|---:|:---:|:---|
| `*` | `*` | 返回深克隆的值。 |

**示例**

```javascript
var objects = [{ 'a': 1 }, { 'b': 2 }];

var deep = _.cloneDeep(objects);
console.log(deep[0] === objects[0]);
// => false
```

此示例演示了 `_.cloneDeep` 如何创建一个新数组并在其中创建新对象，确保与原始对象没有共享引用。

## 对象方法

### get

获取 `object` 中 `path` 处的值。如果解析后的值为 `undefined`，则返回 `defaultValue`。

**参数**

| 名称 | 类型 | 描述 |
|---:|:---:|:---|
| `object` | `Object` | 要查询的对象。 |
| `path` | `Array` \| `string` | 要获取属性的路径。 |
| `defaultValue` | `*` | 对于解析为 `undefined` 的值返回的值。 |

**返回值**

| 名称 | 类型 | 描述 |
|---:|:---:|:---|
| `*` | `*` | 返回解析后的值。 |

**示例**

```javascript
var object = { 'a': [{ 'b': { 'c': 3 } }] };

_.get(object, 'a[0].b.c');
// => 3

_.get(object, ['a', '0', 'b', 'c']);
// => 3

_.get(object, 'a.b.c', 'default');
// => 'default'
```

此示例展示了如何使用 `_.get` 安全地访问对象中的嵌套属性，支持数组索引和缺失路径的默认值。

### set

设置 `object` 中 `path` 处的值。如果 `path` 的一部分不存在，则会创建它。对于缺失的索引属性会创建数组，而对于所有其他缺失的属性会创建对象。

**参数**

| 名称 | 类型 | 描述 |
|---:|:---:|:---|
| `object` | `Object` | 要修改的对象。 |
| `path` | `Array` \| `string` | 要设置属性的路径。 |
| `value` | `*` | 要设置的值。 |

**返回值**

| 名称 | 类型 | 描述 |
|---:|:---:|:---|
| `Object` | `Object` | 返回 `object`。 |

**示例**

```javascript
var object = { 'a': [{ 'b': { 'c': 3 } }] };

_.set(object, 'a[0].b.c', 4);
console.log(object.a[0].b.c);
// => 4

_.set(object, ['x', '0', 'y', 'z'], 5);
console.log(object.x[0].y.z);
// => 5
```

此示例说明了 `_.set` 创建嵌套路径并在对象中设置值的能力。

### merge

将源对象的自身和继承的可枚举字符串键属性递归合并到目标对象中。如果目标值存在，解析为 `undefined` 的源属性将被跳过。数组和普通对象属性将递归合并。其他对象和值类型将通过赋值覆盖。

**参数**

| 名称 | 类型 | 描述 |
|---:|:---:|:---|
| `object` | `Object` | 目标对象。 |
| `sources` | `Object` | 源对象。 |

**返回值**

| 名称 | 类型 | 描述 |
|---:|:---:|:---|
| `Object` | `Object` | 返回 `object`。 |

**示例**

```javascript
var object = {
  'a': [{ 'b': 2 }, { 'd': 4 }]
};

var other = {
  'a': [{ 'c': 3 }, { 'e': 5 }]
};

_.merge(object, other);
// => { 'a': [{ 'b': 2, 'c': 3 }, { 'd': 4, 'e': 5 }] }
```

此示例演示了 `_.merge` 如何递归合并对象和数组。

## 字符串方法

### camelCase

将 `string` 转换为[驼峰式](https://en.wikipedia.org/wiki/CamelCase)。

**参数**

| 名称 | 类型 | 描述 |
|---:|:---:|:---|
| `string` | `string` | 要转换的字符串（默认值：`''`）。 |

**返回值**

| 名称 | 类型 | 描述 |
|---:|:---:|:---|
| `string` | `string` | 返回驼峰式字符串。 |

**示例**

```javascript
_.camelCase('Foo Bar');
// => 'fooBar'

_.camelCase('--foo-bar--');
// => 'fooBar'

_.camelCase('__FOO_BAR__');
// => 'fooBar'
```

此示例展示了 `_.camelCase` 如何将各种字符串格式转换为驼峰式。

### trim

移除 `string` 中开头和结尾的空格或指定字符。

**参数**

| 名称 | 类型 | 描述 |
|---:|:---:|:---|
| `string` | `string` | 要修剪的字符串（默认值：`''`）。 |
| `chars` | `string` | 要修剪的字符（默认值：空格）。 |
| `guard` | `Object` | 允许作为 `_.map` 等方法的迭代器使用。 |

**返回值**

| 名称 | 类型 | 描述 |
|---:|:---:|:---|
| `string` | `string` | 返回修剪后的字符串。 |

**示例**

```javascript
_.trim('  abc  ');
// => 'abc'

_.trim('-_-abc-_-', '_-');
// => 'abc'

_.map(['  foo  ', '  bar  '], _.trim);
// => ['foo', 'bar']
```

此示例演示了 `_.trim` 如何从字符串中移除开头/结尾的空格或自定义字符。

### words

将 `string` 分割成其单词数组。

**参数**

| 名称 | 类型 | 描述 |
|---:|:---:|:---|
| `string` | `string` | 要检查的字符串（默认值：`''`）。 |
| `pattern` | `RegExp` \| `string` | 匹配单词的模式。 |
| `guard` | `Object` | 允许作为 `_.map` 等方法的迭代器使用。 |

**返回值**

| 名称 | 类型 | 描述 |
|---:|:---:|:---|
| `Array` | `Array` | 返回 `string` 的单词。 |

**示例**

```javascript
_.words('fred, barney, & pebbles');
// => ['fred', 'barney', 'pebbles']

_.words('fred, barney, & pebbles', /[^, ]+/g);
// => ['fred', 'barney', '&', 'pebbles']
```

此示例展示了 `_.words` 如何从字符串中提取单词，并支持可选的模式匹配。

## 数字方法

### add

将两个数字相加。

**参数**

| 名称 | 类型 | 描述 |
|---:|:---:|:---|
| `augend` | `number` | 加法中的第一个数字。 |
| `addend` | `number` | 加法中的第二个数字。 |

**返回值**

| 名称 | 类型 | 描述 |
|---:|:---:|:---|
| `number` | `number` | 返回总和。 |

**示例**

```javascript
_.add(6, 4);
// => 10
```

此示例使用 `_.add` 执行简单的加法运算。

### random

生成一个介于包含 `lower` 和 `upper` 界限之间的随机数。如果只提供一个参数，则返回一个介于 `0` 和给定数字之间的数。如果 `floating` 为 `true`，或者 `lower` 或 `upper` 之一是浮点数，则返回浮点数而不是整数。

**参数**

| 名称 | 类型 | 描述 |
|---:|:---:|:---|
| `lower` | `number` | 下限（默认值：0）。 |
| `upper` | `number` | 上限（默认值：1）。 |
| `floating` | `boolean` | 指定返回浮点数。 |

**返回值**

| 名称 | 类型 | 描述 |
|---:|:---:|:---|
| `number` | `number` | 返回随机数。 |

**示例**

```javascript
_.random(0, 5);
// => an integer between 0 and 5

_.random(5);
// => also an integer between 0 and 5

_.random(5, true);
// => a floating-point number between 0 and 5

_.random(1.2, 5.2);
// => a floating-point number between 1.2 and 5.2
```

此示例在指定范围内生成随机数，包括浮点数。

## 实用方法

### identity

此方法返回其接收到的第一个参数。

**参数**

| 名称 | 类型 | 描述 |
|---:|:---:|:---|
| `value` | `*` | 任何值。 |

**返回值**

| 名称 | 类型 | 描述 |
|---:|:---:|:---|
| `*` | `*` | 返回 `value`。 |

**示例**

```javascript
var object = { 'a': 1 };

console.log(_.identity(object) === object);
// => true
```

此示例展示了 `_.identity` 如何返回其接收到的确切值。

### uniqueId

生成一个唯一 ID。如果提供了 `prefix`，则 ID 将附加到其后。

**参数**

| 名称 | 类型 | 描述 |
|---:|:---:|:---|
| `prefix` | `string` | 要用作 ID 前缀的值（默认值：`''`）。 |

**返回值**

| 名称 | 类型 | 描述 |
|---:|:---:|:---|
| `string` | `string` | 返回唯一 ID。 |

**示例**

```javascript
_.uniqueId('contact_');
// => 'contact_104'

_.uniqueId();
// => '105'
```

此示例生成唯一 ID，可带或不带自定义前缀。

---

本 API 参考详细介绍了 Lodash 在各个类别中最常用的一些方法。通过理解这些方法，您可以编写更简洁、更具可读性且性能更高的 JavaScript 代码。继续您的探索，在[贡献](./contributing.md)部分了解如何为 Lodash 项目做出贡献。
