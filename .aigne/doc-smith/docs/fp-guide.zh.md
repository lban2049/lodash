# 函数式编程指南

`lodash/fp` 模块提供了 Lodash 方法的不可变、自动柯里化、迭代函数优先、数据置后的版本，从而实现了一种更函数式的编程方法。本指南将解释其核心概念及使用方法。

要开始使用，只需从 `lodash/fp` 导入即可：

```js
// 加载 FP 版本，用于不可变、自动柯里化、迭代函数优先、数据置后的方法。
var fp = require('lodash/fp');
```

## 核心原则

Lodash 的函数式编程版本建立在四个主要原则之上，这些原则能够实现一种不同的、更具声明性的编码风格，尤其适用于数据操作。

### 1. 不可变性

标准的 Lodash 方法有时会改变输入的数组或对象（例如 `_.pull`、`_.assign`）。在 FP 版本中，这些方法被包装为以不可变的方式操作。它们不会修改原始数据结构，而是始终返回一个新的、更新后的数据结构。

例如，像 `fill`、`pull`、`pullAll` 和 `reverse` 这样会改变数组的方法将返回一个新数组。同样，像 `assign`、`defaults` 和 `merge` 这样的对象方法将返回一个新对象。

```js
const data = { 'a': 1, 'b': 2 };

// 标准 Lodash (会改变 'data')
// _.assign(data, { 'c': 3 });
// console.log(data); // => { 'a': 1, 'b': 2, 'c': 3 }

// Lodash FP (返回一个新对象)
const result = fp.assign({ 'c': 3 }, data);
console.log(result); // => { 'a': 1, 'b': 2, 'c': 3 }
console.log(data);   // => { 'a': 1, 'b': 2 } (原对象未改变)
```

### 2. 数据置后的方法签名

大多数 Lodash 方法的签名是 `(data, ...args)`。FP 版本将这些参数重新排列为数据置后：`(...args, data)`。这是一个关键的改动，有助于函数组合和柯里化。

| 标准 Lodash | Lodash FP |
|---|---|
| `_.map(collection, iteratee)` | `fp.map(iteratee, collection)` |
| `_.filter(collection, predicate)` | `fp.filter(predicate, collection)` |
| `_.get(object, path, defaultValue)` | `fp.get(path, object)` or `fp.getOr(defaultValue, path, object)` |

这种约定允许你通过预先填充参数来创建专用函数，而数据则可以稍后提供。

### 3. 自动柯里化

`lodash/fp` 中的所有方法都是自动柯里化的。这意味着你可以用比预期少的参数来调用一个函数，它将返回一个等待剩余参数的新函数。这与数据置后的方法无缝协作。

```js
const users = [{ 'name': 'Alice', 'active': true }, { 'name': 'Bob', 'active': false }];

// 通过首先提供迭代函数参数来创建一个专用函数。
const getNames = fp.map(fp.get('name'));

// 现在，将此函数应用于你的数据。
const names = getNames(users);
// => ['Alice', 'Bob']
```

你也可以使用占位符 `fp.__` 来不按顺序提供参数。

```js
// 创建一个将任何数字除以 2 的函数
const divideBy2 = fp.divide(fp.__, 2);

divideBy2(10); // => 5
```

### 4. 限制迭代函数参数

默认情况下，传递给 `map` 和 `filter` 等方法的迭代函数只接收一个参数：`(value)`。这可以防止常见错误，例如 `parseInt` 接收到 `index` 参数并产生意外结果。

## 函数组合

这些原则的主要好处是实现强大且可读性强的函数组合。你可以使用 `fp.flow`（从左到右）或 `fp.flowRight`（从右到左）将简单的函数链接在一起，构建复杂的数据转换。

```js
const users = [
  { 'name': 'ALICE', 'age': 30 },
  { 'name': 'bob', 'age': 25 },
  { 'name': 'CHARLIE', 'age': 35 }
];

const processUsers = fp.flow(
  fp.filter(user => user.age > 28),
  fp.map(fp.get('name')),
  fp.map(fp.lowerCase),
  fp.map(fp.capitalize)
);

const result = processUsers(users);
// => ['Alice', 'Charlie']
```

## 别名与重映射

为了提供更一致的 FP 体验并与其他库（如 Ramda）的约定保持一致，`lodash/fp` 包含了一些别名和重映射的方法。

| Lodash FP 别名 | 真实的 Lodash 方法 |
|---|---|
| `pipe` | `flow` |
| `compose` | `flowRight` |
| `prop` | `get` |
| `propEq` | `matchesProperty` |
| `assoc` | `set` |
| `dissoc` | `unset` |
| `any` | `some` |
| `all` | `every` |
| `__` | `placeholder` |
| `equals` | `isEqual` |
| `T` | `stubTrue` |
| `F` | `stubFalse` |

## 自定义转换

你可以使用 `fp.convert` 创建自己的 FP 风格函数或转换整个库。这是一个高级功能，可以让你控制转换过程。

```js
const myLib = {
  add: (a, b) => a + b
};

const fpLib = fp.convert(myLib, {
  'curry': true,
  'rearg': true
});

const add5 = fpLib.add(5);
add5(10); // => 15
```

`convert` 函数接受一个选项对象来控制其行为：

| 选项 | 默认值 | 描述 |
|---|---|---|
| `cap` | `true` | 指定是否限制迭代函数的参数。 |
| `curry` | `true` | 指定是否进行柯里化。 |
| `fixed` | `true` | 指定固定的参数数量。 |
| `immutable` | `true` | 指定是否进行不可变操作。 |
| `rearg` | `true` | 指定是否将参数重新排列为数据置后。 |

---

通过遵循这些函数式原则，`lodash/fp` 实现了一种声明式、功能强大且高度可复用的数据操作方式。有关函数的完整列表，请参阅 [API 参考](./api.md)。