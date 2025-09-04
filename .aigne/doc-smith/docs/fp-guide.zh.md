# 函数式编程指南

`lodash/fp` 模块提供了 Lodash 方法的一个不可变、自动柯里化、迭代函数优先、数据置后的版本。本指南解释了该函数式编程（FP）风格变体的核心原则，以及它与标准 Lodash 构建版本的区别。

要开始使用，只需导入 `fp` 模块：

```js
// 加载 FP 构建版本，以使用不可变、自动柯里化、迭代函数优先、数据置后的方法。
var fp = require('lodash/fp');
```

## 核心原则

FP 模块建立在几个关键的函数式编程原则之上，这些原则有助于创建模块化、可复用且无副作用的代码。

### 1. 不可变性

与许多标准的 Lodash 方法不同，`lodash/fp` 模块中的函数是不可变的。它们不会修改输入数据，而是返回一个新的、经过修改的实例。这适用于那些通常会改变数组或对象的方法。

例如，像 `assign`、`pull` 和 `set` 这样的方法被包装过，在执行操作前会先克隆输入数据，从而确保原始数据结构保持不变。

以下是在 FP 模块中为实现不可变性而包装的标准 Lodash 方法示例：

| 类别 | 实现不可变性的方法 |
| --- | --- |
| **数组** | `fill`, `pull`, `pullAll`, `pullAllBy`, `pullAllWith`, `pullAt`, `remove`, `reverse` |
| **对象** | `assign`, `assignAll`, `assignIn`, `defaults`, `defaultsDeep`, `merge`, `mergeAll` |
| **设置器** | `set`, `setWith`, `unset`, `update`, `updateWith` |

### 2. 自动柯里化

FP 模块中所有参数数量大于 1 的方法都经过自动柯里化。这允许你通过部分应用参数来创建新函数。这一特性是利用简单函数构建复杂操作的核心。

```js
const fp = require('lodash/fp');

// 通过提供迭代函数来创建一个专用函数。
const getNames = fp.map(fp.get('name'));

const users = [{ name: 'Alice' }, { name: 'Bob' }];

// 将数据应用于该专用函数。
getNames(users);
// => ['Alice', 'Bob']
```

你还可以使用占位符 `fp.placeholder`（别名为 `__`）来延迟提供参数。

```js
const g = fp.get(__, { 'a': 1 });

g('a');
// => 1
```

### 3. 数据置后与参数重排

为便于柯里化和函数组合，所有方法都采用数据置后的设计。这意味着被操作的数据结构（如数组或对象）将作为最后一个参数提供。这是通过重新排列原始 Lodash 方法的参数顺序实现的。

常见的重排模式包括：
- **双参数函数**：`(a, b)` 变为 `(b, a)`。
- **三参数函数**：`(a, b, c)` 变为 `(c, a, b)`。

这使得使用像 `fp.flow` 这样的组合函数来创建操作管道变得容易。

**标准 Lodash (数据优先)**
```js
const _ = require('lodash');
_.map(['a', 'b', 'c'], _.toUpper);
// => ['A', 'B', 'C']
```

**Lodash FP (数据置后)**
```js
const fp = require('lodash/fp');
fp.map(fp.toUpper)(['a', 'b', 'c']);
// => ['A', 'B', 'C']
```

### 4. 迭代函数优先

迭代函数（回调函数）始终是第一个参数。这种一致的签名与数据置后相结合，使得函数组合变得简单明了。

```js
const fp = require('lodash/fp');

const getFirstAndDouble = fp.flow(
  fp.map(x => x * 2),
  fp.first
);

getFirstAndDouble([1, 2, 3]);
// => 2
```

## 用于互操作性的别名

为了给来自其他函数式库（如 Ramda）的开发者提供熟悉的体验，`lodash/fp` 包含了一些常用别名。

| 别名 | Lodash FP 方法 | 描述 |
| --- | --- | --- |
| `__` | `placeholder` | 用于部分应用的柯里化占位符。 |
| `pipe` | `flow` | 从左到右的函数组合。 |
| `compose` | `flowRight` | 从右到左的函数组合。 |
| `prop` | `get` | 从对象中检索属性值。 |
| `path` | `get` | 从对象中检索嵌套的属性值。 |
| `equals` | `isEqual` | 执行深层相等性比较。 |
| `always` | `constant` | 创建一个返回常量值的函数。 |
| `T` | `stubTrue` | 一个始终返回 `true` 的函数。 |
| `F` | `stubFalse` | 一个始终返回 `false` 的函数。 |
| `any` | `some` | 检查集合中是否有任何元素通过测试。 |
| `all` | `every` | 检查集合中是否所有元素都通过测试。 |

## 自定义转换

FP 模块是使用一个 `convert` 函数生成的，该函数可用于创建具有特定行为的自定义 Lodash 变体。这是一个高级功能，可以对生成的函数进行精细控制。

每个 FP 方法都附带一个 `.convert()` 方法，该方法接受一个选项对象。

```js
const fp = require('lodash/fp');

// 创建一个可变的、数据优先但仍然柯里化的 set 版本
const mutableCurriedSet = fp.set.convert({
  'immutable': false,
  'rearg': false
});
```

可用的转换选项包括：
- `cap` (boolean): 指定是否限制迭代函数的参数数量。默认为 `true`。
- `curry` (boolean): 指定是否柯里化。默认为 `true`。
- `fixed` (boolean): 指定是否固定参数数量。默认为 `true`。
- `immutable` (boolean): 指定是否为不可变操作。默认为 `true`。
- `rearg` (boolean): 指定是否重排参数。默认为 `true`。

---

要获取可用函数及其签名的完整列表，请参阅 [API 参考](./api.md)。