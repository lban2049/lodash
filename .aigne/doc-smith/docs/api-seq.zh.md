# 序列

Lodash 提供了强大的工具，通过方法链来创建操作序列。这使你可以构建优雅、可读的数据处理管道。一个 `lodash` 对象包装一个值，使你能够在其上以链式方式调用 Lodash 方法。

对数组、集合或函数进行操作并返回这些类型的方法可以被链式调用。检索单个值或原始值的方法将自动结束链式调用并返回未包装的值。对于所有其他情况，必须使用 `.value()` 显式地解开包装。

链式调用的一个关键特性是**延迟求值**。链式方法的执行会延迟到 `.value()` 被调用时。这使得 Lodash 能够执行诸如**快捷融合**之类的优化，它会合并迭代器调用以避免创建中间数组，从而显著提高性能。

要深入了解相关概念，请参阅我们的[函数式编程指南](./fp-guide.md)。

## 创建链式调用

有两种方法可以创建链式调用：

*   **隐式链式调用**：只需用 `_()` 包装你的数据。大多数方法将返回一个包装后的值，但某些方法（如 `_.add` 或 `_.find`）将返回一个原始值，从而结束链式调用。
*   **显式链式调用**：使用 `_.chain()` 开始一个链式调用，其中每个方法调用都返回一个包装后的实例，该实例必须用 `.value()` 解开包装。

---

## API 方法

### chain

创建一个 `lodash` 包装器实例，该实例包装 `value` 并启用显式方法链序列。此类序列的结果必须始终使用 `_#value` 解开包装。

**参数**

<x-field data-name="value" data-type="any" data-desc="要包装的值。"></x-field>

**返回**

<x-field data-name="wrapper" data-type="Object" data-desc="返回新的 `lodash` 包装器实例。"></x-field>

**示例**

```javascript icon=logos:javascript
var users = [
  { 'user': 'barney',  'age': 36 },
  { 'user': 'fred',    'age': 40 },
  { 'user': 'pebbles', 'age': 1 }
];

var youngest = _
  .chain(users)
  .sortBy('age')
  .map(function(o) {
    return o.user + ' is ' + o.age;
  })
  .head()
  .value();
// => 'pebbles is 1'
```

### tap

此方法调用 `interceptor` 并返回 `value`。拦截器调用时带有一个参数：`(value)`。此方法的目的是“接入”方法链序列，以修改中间结果或执行诸如日志记录之类的副作用。

**参数**

<x-field data-name="value" data-type="any" data-desc="提供给拦截器的值。"></x-field>
<x-field data-name="interceptor" data-type="Function" data-desc="要调用的函数。"></x-field>

**返回**

<x-field data-name="value" data-type="any" data-desc="返回原始的 `value`。"></x-field>

**示例**

```javascript icon=logos:javascript
_([1, 2, 3])
 .tap(function(array) {
   // Mutate the input array.
   array.pop();
 })
 .reverse()
 .value();
// => [2, 1]
```

### thru

此方法类似于 `_.tap`，但它返回 `interceptor` 的结果。此方法的目的是“传递”值，替换方法链序列中的中间结果。

**参数**

<x-field data-name="value" data-type="any" data-desc="提供给拦截器的值。"></x-field>
<x-field data-name="interceptor" data-type="Function" data-desc="要调用的函数。"></x-field>

**返回**

<x-field data-name="result" data-type="any" data-desc="返回 `interceptor` 的结果。"></x-field>

**示例**

```javascript icon=logos:javascript
_('  abc  ')
 .chain()
 .trim()
 .thru(function(value) {
   return [value];
 })
 .value();
// => ['abc']
```

## 包装器原型方法

这些方法在 Lodash 包装器实例上可用，例如由 `_()` 或 `_.chain()` 创建的实例。

| 方法 | 描述 |
|---|---|
| `at(...paths)` | `_.at` 的包装器版本。从包装的对象中根据给定的路径选择值。 |
| `chain()` | 从现有包装器启用显式链式调用。 |
| `commit()` | 执行链式序列并返回包装后的结果。 |
| `plant(value)` | 创建链式序列的克隆，并将新的 `value` 作为包装值植入。 |
| `reverse()` | `_.reverse` 的包装器版本。注意：这将改变包装的数组。 |
| `value()` | 执行链式序列以解析并返回未包装的值。别名为 `toJSON` 和 `valueOf`。 |
| `next()` | 根据迭代器协议，获取包装对象上的下一个值。 |
| `[Symbol.iterator]()` | 使包装器可迭代（例如，在 `for...of` 循环中）。 |

**示例：使用 .plant()**

```javascript icon=logos:javascript
function square(n) {
  return n * n;
}

var wrapped = _([1, 2]).map(square);
var other = wrapped.plant([3, 4]);

other.value();
// => [9, 16]

wrapped.value();
// => [1, 4]
```

---

现在你已经了解了如何创建和管理序列，可以在 [Collection](./api-collection.md) 和 [Array](./api-array.md) API 部分探索可以在序列中使用的方法。