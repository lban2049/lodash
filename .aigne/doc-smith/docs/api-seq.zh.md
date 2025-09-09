# Seq

关于所有与顺序方法链相关的 Lodash 函数的详细参考。Lodash 包装器允许你将方法链接在一起，从而实现流畅的编程风格。这个过程通常是惰性的，意味着在显式请求最终值之前，操作链不会被执行。

这种惰性求值通过一种名为“快捷融合”的技术实现了显著的性能优化，该技术通过合并迭代器调用来避免创建中间数组。要解析该链并获取最终输出，你必须调用 `.value()` 方法。

## 方法

### _.chain(value)

创建一个 `lodash` 包装器实例，该实例包装 `value` 并启用显式方法链序列。此类序列的结果必须使用 `_#value()` 进行解包。

**参数**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要包装的值。 |

**返回**

(`Object`): 返回新的 `lodash` 包装器实例。

**示例**

```javascript
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

### _.tap(value, interceptor)

此方法调用 `interceptor` 并返回 `value`。拦截器调用时会传入一个参数：`(value)`。此方法的目的是“接入”方法链序列，以便在不改变沿链传递值的情况下修改中间结果。

**参数**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 提供给 `interceptor` 的值。 |
| `interceptor` | `Function` | 要调用的函数。 |

**返回**

(`*`): 返回 `value`。

**示例**

```javascript
_([1, 2, 3])
 .tap(function(array) {
   // Mutate input array.
   array.pop();
 })
 .reverse()
 .value();
// => [2, 1]
```

### _.thru(value, interceptor)

此方法与 `_.tap` 类似，但它返回 `interceptor` 的结果。此方法的目的是“传递”值，替换方法链序列中的中间结果。

**参数**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 提供给 `interceptor` 的值。 |
| `interceptor` | `Function` | 要调用的函数。 |

**返回**

(`*`): 返回 `interceptor` 的结果。

**示例**

```javascript
_('  abc  ')
 .chain()
 .trim()
 .thru(function(value) {
   return [value];
 })
 .value();
// => ['abc']
```

## 包装器实例方法

当你使用 `_()` 或 `_.chain()` 创建 Lodash 包装器时，生成的对象有几个方法可以控制链的执行。

| Method | Description |
|---|---|
| `.value()` | 执行链序列以解析并返回解包后的值。别名为 `.toJSON()` 和 `.valueOf()`。 |
| `.chain()` | 在现有的包装器实例上启用显式链式调用。 |
| `.commit()` | 执行链序列并返回一个新的包装结果，允许对计算出的值进行进一步的链式调用。 |
| `.plant(value)` | 创建链序列的克隆，并将新的 `value` 作为包装值。 |
| `.reverse()` | 反转包装的数组。此方法会改变原数组。 |
| `.next()` | 如果包装的对象被视为迭代器，则获取迭代中的下一个值。 |
| `[Symbol.iterator]()` | 使包装器可迭代，从而可以在 `for...of` 循环和 `Array.from()` 中使用。 |

**示例：使用 `.value()`**

```javascript
_([1, 2, 3]).value();
// => [1, 2, 3]
```

**示例：使用 `.plant()`**

```javascript
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

方法链是创建清晰、可读的数据转换管道的强大功能。要了解在这些链中最常用的函数，请继续阅读集合 API 文档。

[下一步：集合 API](./api-collection.md)
