# 函数式编程指南

The `lodash/fp` 模块为 Lodash 提供了一种函数式编程方法，提供了不可变、自动柯里化、迭代函数优先和数据置后的方法。这种风格提倡创建可复用和可组合的函数，这可以使代码更清晰、更可预测。

要开始使用，只需从 `lodash/fp` 导入方法：

```javascript Getting Started with lodash/fp icon=logos:javascript
// 加载 FP 版本，以使用不可变、自动柯里化、迭代函数优先、数据置后的方法。
import fp from 'lodash/fp';

// 按需挑选方法以减小打包体积。
import map from 'lodash/fp/map';
import curryN from 'lodash/fp/curryN';
```

## 核心原则

Lodash 的函数式编程版本建立在几个关键原则之上，这些原则使其与标准的 Lodash 库有所不同。

### 1. 不可变性

FP 方法不会改变你传递给它们的数据。任何通常会更改输入数据的方法，例如 `_.set` 或 `_.pull`，会返回一个新的、被修改过的对象或数组，而原始数据保持不变。

这是通过包装那些已知会引起数据变更的方法来实现的。例如，像 `fill`、`pull` 和 `reverse` 这样的数组方法，以及像 `assign`、`defaults` 和 `merge` 这样的对象方法，都被转换成了它们的不可变版本。

```javascript Immutability Example icon=logos:javascript
import { set } from 'lodash/fp';

const originalObject = { 'a': [{ 'b': { 'c': 3 } }] };

// 'set' 返回一个新对象，而不是修改原始对象。
const newObject = set('a[0].b.c', 4, originalObject);

console.log(originalObject.a[0].b.c); // => 3
console.log(newObject.a[0].b.c);      // => 4
```

### 2. 自动柯里化

`lodash/fp` 中的所有方法都是自动柯里化的。这意味着你可以用比预期少的参数来调用一个函数，它将返回一个等待剩余参数的新函数。这对于创建专用函数非常强大。

```javascript Auto-Currying Example icon=logos:javascript
import { map, add } from 'lodash/fp';

// 通过部分应用 'add' 创建一个专用的 'addOne' 函数。
const addOne = add(1);

// 通过使用 'addOne' 部分应用 'map' 创建一个专用的 'incrementAll' 函数。
const incrementAll = map(addOne);

const numbers = [1, 2, 3];
console.log(incrementAll(numbers)); // => [2, 3, 4]
```

### 3. 迭代函数优先，数据置后（参数重排）

为了方便柯里化和函数组合，大多数 Lodash 方法的参数都经过了重新排列。数据（如数组或对象）通常是最后一个参数，而要应用的函数（迭代函数）是第一个。

这种数据置后的方法使得构建操作管道变得容易。

- **标准 Lodash：** `_.map(collection, iteratee)`
- **FP Lodash：** `fp.map(iteratee)(collection)`

这种重排是一致应用的。对于像 `_.get(object, path, defaultValue)` 这样的函数，其 FP 等效函数是 `fp.get(path, object)`，或者在有默认值的情况下是 `fp.getOr(defaultValue, path, object)`。

### 4. 用于柯里化的占位符

Lodash FP 提供了一个特殊的占位符值 `_`（可通过 `fp.placeholder` 访问），允许在柯里化时以非顺序方式提供参数。当数据参数不是你想要提供的最后一个参数时，这尤其有用。

```javascript Placeholder Example icon=logos:javascript
import fp from 'lodash/fp';

const numbers = [10, 20, 30, 40, 50];

// 创建一个函数，用 100 减去数组中的每个数字。
// 占位符 `_` 允许我们先指定 subtract 的第二个参数。
const subtractFrom100 = fp.subtract(100);
const result = fp.map(subtractFrom100, numbers);
console.log(result); // => [90, 80, 70, 60, 50]

// 或者，直接在 map 中使用占位符：
const subtractAllFrom100 = fp.map(fp.subtract(_, 100));
const invertedResult = subtractAllFrom100(numbers);
console.log(invertedResult); // => [-90, -80, -70, -60, -50]
```

## 方法别名与兼容性

为了给来自其他函数式库（如 Ramda）的开发人员提供熟悉的体验，`lodash/fp` 包含了众多别名。这减少了使用上的阻力，并使库更加直观。

关键别名包括：

| Lodash FP 名称 | 别名 |
| :--- | :--- |
| `forEach` | `each` |
| `forEachRight` | `eachRight` |
| `toPairs` | `entries` |
| `head` | `first` |
| `flowRight` | `compose` |
| `includes` | `contains` |
| `isEqual` | `equals` |
| `get` | `prop`, `path`, `property` |
| `set` | `assoc`, `assocPath` |
| `placeholder` | `__` |
| `stubFalse` | `F` |
| `stubTrue` | `T` |
| `every` | `all` |
| `some` | `any` |

## 自定义转换

整个 `lodash/fp` 模块是通过使用一个强大的 `convert` 函数转换标准 Lodash 库生成的。该函数允许通过一个选项对象对转换过程进行细粒度控制。你可以用它来创建自己的定制化 FP 版本。

主要的转换选项有：

- **`cap`** (boolean)：切换是否限制迭代函数的参数数量。默认为 `true`，以防止像 `parseInt` 这样的函数接收到额外参数而引发问题。
- **`curry`** (boolean)：切换是否自动柯里化。默认为 `true`。
- **`fixed`** (boolean)：切换是否固定函数参数个数。默认为 `true`。
- **`immutable`** (boolean)：切换是否为不可变操作。默认为 `true`。
- **`rearg`** (boolean)：切换是否重排参数（数据置后）。默认为 `true`。