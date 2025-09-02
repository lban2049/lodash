# 函数式编程指南

Lodash FP 模块 (`lodash/fp`) 提供了一个函数式编程风格的 Lodash 版本。它遵循不可变性、自动柯里化、迭代器优先和数据置后的核心原则，这使得函数组合和代码复用变得更加简洁和强大。

与标准的 Lodash 方法不同，FP 版本的方法经过精心设计，以支持一种更具声明性的编程范式。你可以在 [FP Guide](https://github.com/lodash/lodash/wiki/FP-Guide) Wiki 页面找到更多信息。

## 核心原则

Lodash FP 的设计基于四个核心原则，这些原则共同作用，为 JavaScript 提供了强大的函数式编程能力。

<x-cards data-columns="2">
  <x-card data-title="数据置后 (Data-Last)" data-icon="lucide:align-end-vertical">
    集合或数据对象始终作为最后一个参数传递。这使得你可以轻松地创建新函数，等待数据传入后执行。
  </x-card>
  <x-card data-title="自动柯里化 (Auto-Curried)" data-icon="lucide:git-fork">
    所有方法都是自动柯里化的，这意味着你可以传递部分参数并返回一个等待其余参数的新函数。
  </x-card>
  <x-card data-title="不可变性 (Immutability)" data-icon="lucide:shield-check">
    FP 方法不会修改输入数据。任何会产生副作用的操作（如 `fill` 或 `assign`）都会返回一个新的实例，而原始数据保持不变。
  </x-card>
  <x-card data-title="迭代器优先 (Iteratee-First)" data-icon="lucide:list-filter">
    处理集合的函数（迭代器）作为第一个参数传递。这与数据置后原则相辅相成，便于函数的创建和组合。
  </x-card>
</x-cards>

### 数据流对比

为了更直观地理解标准 Lodash 和 Lodash FP 之间的差异，下面的图表演示了 `map` 函数在两种模式下的数据流。

```d2
direction: down

"Standard Lodash Data Flow": {
  direction: right
  data: "Collection\n[1, 2, 3]"
  iteratee: "Iteratee\nn => n * 2"
  map_func: "_.map(collection, iteratee)"
  result: "Result\n[2, 4, 6]"
  
  data -> map_func
  iteratee -> map_func
  map_func -> result
}

"Lodash FP Data Flow (Point-free style)": {
  direction: right
  iteratee_fp: "Iteratee\nn => n * 2"
  curried_func: "fp.map(iteratee)"
  data_fp: "Collection\n[1, 2, 3]"
  apply_data: "curriedMapFn([1, 2, 3])"
  result_fp: "Result\n[2, 4, 6]"

  iteratee_fp -> curried_func: "返回一个新函数 `curriedMapFn`"
  curried_func -> apply_data
  data_fp -> apply_data
  apply_data -> result_fp
}
```

## 方法转换

为了实现函数式风格，FP 模块对标准 Lodash 方法进行了转换。主要包括参数重排和提供别名。

### 参数顺序

大多数接受集合或对象作为参数的方法都已重新排列，以将数据参数放在最后。这对于柯里化和函数组合至关重要。

| 标准 Lodash | Lodash FP | 参数重排说明 |
|---|---|---|
| `_.filter(collection, predicate)` | `fp.filter(predicate)(collection)` | `predicate` 优先，`collection` 置后。 |
| `_.get(object, path, defaultValue)` | `fp.get(path)(object)` 或 `fp.getOr(defaultValue, path)(object)` | `path` 优先，`object` 置后。`getOr` 是一个独立的变体。 |
| `_.isMatchWith(object, source, customizer)` | `fp.isMatchWith(customizer, source)(object)` | `customizer` 和 `source` 优先，`object` 置后。 |
| `_.reduce(collection, iteratee, accumulator)` | `fp.reduce(iteratee, accumulator)(collection)` | `iteratee` 和 `accumulator` 优先，`collection` 置后。 |
| `_.set(object, path, value)` | `fp.set(path, value)(object)` | `path` 和 `value` 优先，`object` 置后。 |

### 方法别名

为了给熟悉 Ramda 等其他函数式库的开发者提供便利，`lodash/fp` 提供了许多常见方法的别名。

| Lodash FP 别名 | 原始 Lodash 方法 | 描述 |
|---|---|---|
| `pipe` | `flow` | 从左到右组合函数。 |
| `compose` | `flowRight` | 从右到左组合函数。 |
| `prop` | `get` | 获取对象的属性值。 |
| `assoc` | `set` | 设置对象的属性值（不可变）。 |
| `contains` | `includes` | 检查集合是否包含某个值。 |
| `all` | `every` | 检查集合中的所有元素是否都满足断言。 |
| `any` | `some` | 检查集合中是否有任何元素满足断言。 |
| `__` | `placeholder` | 用于部分应用的占位符。 |
| `T` | `stubTrue` | 返回 `true` 的函数。 |
| `F` | `stubFalse` | 返回 `false` 的函数。 |

## 使用占位符进行部分应用

当你需要在一个非首位的参数位置上预先填充数据时，可以使用占位符 `fp.placeholder`（或其别名 `__`）。这在创建需要特定参数顺序的函数时非常有用。

例如，`fp.subtract` 的签名是 `fp.subtract(subtrahend)(minuend)`，它计算 `minuend - subtrahend`。

```javascript
const fp = require('lodash/fp');

// 创建一个函数，从 10 中减去一个数
// 相当于创建一个函数 x => 10 - x
const subtractFrom10 = fp.subtract(fp.__, 10);

const result = subtractFrom10(4);
console.log(result);
// => 6
```

在这个例子中，占位符 `__` 占据了第一个参数（`subtrahend`）的位置，允许我们先提供第二个参数 `10`（`minuend`）。

## 高级定制：`convert` 函数

如果你需要对 FP 模块的行为进行更精细的控制，可以使用 `convert` 函数。它允许你创建一个自定义的 Lodash FP 实例，并可以配置其行为，例如禁用自动柯里化或不可变性。

```javascript
const _ = require('lodash');
const fp = require('lodash/fp');

// 创建一个禁用了自动柯里化功能的 Lodash FP 版本
const nonCurriedFp = fp.convert({ 'curry': false });

const iteratee = x => x * 2;
const collection = [1, 2, 3];

// 由于禁用了柯里化，下面的调用方式会抛出错误
// nonCurriedFp.map(iteratee)(collection);

// 你必须像调用标准 Lodash 函数一样一次性提供所有参数
const result = nonCurriedFp.map(iteratee, collection);
console.log(result);
// => [2, 4, 6]
```

`convert` 函数接受一个配置对象，你可以通过它来开启或关闭以下特性：

| 配置项 | 默认值 | 描述 |
|---|---|---|
| `cap` | `true` | 是否限制迭代器的参数数量。 |
| `curry` | `true` | 是否启用自动柯里化。 |
| `fixed` | `true` | 是否固定函数参数个数，以支持柯里化。 |
| `immutable` | `true` | 是否强制不可变性，对有副作用的方法进行包装。 |
| `rearg` | `true` | 是否重排参数顺序以实现数据置后。 |

通过本指南，你应该对 Lodash FP 的核心概念和用法有了深入的了解。要查看所有可用的函数，请继续浏览 [API 参考](./api.md)。