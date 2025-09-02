# Seq

Lodash 提供了强大的方法链式调用能力，允许你将多个操作串联起来，以一种清晰、可读的方式处理数据。这种方式的核心是 Lodash 包装器对象，它封装了你的数据，并允许在其上调用 Lodash 方法。

链式调用支持**惰性求值 (Lazy Evaluation)**。这意味着在显式或隐式地调用 `_#value()` 之前，中间操作不会被执行。这种机制通过“快捷融合”优化了性能，避免了创建中间数组，从而大大减少了迭代次数，尤其是在处理大型数据集时。

### 链式调用流程

下面的图表演示了一个典型的数据处理链：

```d2
direction: right

A: "原始数组\n[1, 2, 3, 4]"
B: "_.map(n => n * n)\n[1, 4, 9, 16]"
C: "_.filter(n => n > 5)\n[9, 16]"
D: "_.take(1)\n[9]"
E: "_.value()\n获取最终结果"
F: "最终结果\n[9]"

A -> B: "映射" { style.animated: true }
B -> C: "过滤" { style.animated: true }
C -> D: "截取" { style.animated: true }
D -> E: "求值" { style.animated: true }
E -> F
```

## 核心函数

以下是与序列化方法链相关的核心函数。

### _.chain(value)

创建一个启用了显式方法链的 Lodash 包装器实例。通过 `_.chain` 开始的序列必须使用 `_#value()` 方法来获取最终结果。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `value` | `*` | 要包装的值。 |

**返回**

- `(Object)`: 返回新的 Lodash 包装器实例。

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

此方法调用 `interceptor` 并返回 `value`。`interceptor` 接收 `value` 作为其唯一参数。这个方法的主要目的是“接入”一个方法链，以便在不改变链中值的情况下执行某些操作，例如记录日志或修改外部变量。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `value` | `*` | 提供给 `interceptor` 的值。 |
| `interceptor` | `Function` | 要调用的函数。 |

**返回**

- `(*)`: 返回 `value`。

**示例**

```javascript
_([1, 2, 3])
 .tap(function(array) {
   // 在此处可以对数组进行操作，例如记录日志
   console.log(array); // 输出 [1, 2, 3]
   array.pop();
 })
 .reverse()
 .value();
// => [2, 1]
```

### _.thru(value, interceptor)

此方法与 `_.tap` 类似，但它返回 `interceptor` 的执行结果。这使得你可以在方法链中传递和替换中间结果。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `value` | `*` | 提供给 `interceptor` 的值。 |
| `interceptor` | `Function` | 要调用的函数。 |

**返回**

- `(*)`: 返回 `interceptor` 的结果。

**示例**

```javascript
_('  abc  ')
 .chain()
 .trim()
 .thru(function(value) {
   return [value, value.length];
 })
 .value();
// => ['abc', 3]
```

## 包装器方法

### _#value()

执行链式调用序列以获取最终被包装的值。这是显式链式调用的终点。

**别名**: `_#toJSON`, `_#valueOf`

**返回**

- `(*)`: 返回解析后的未包装值。

**示例**

```javascript
_([1, 2, 3]).value();
// => [1, 2, 3]

_('  abc  ').chain().trim().value();
// => 'abc'
```

### _#at(...paths)

`_.at` 的包装器版本。根据指定的属性路径选择值。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `...paths` | `(string|string[])` | 要选择的属性路径。 |

**返回**

- `(Object)`: 返回新的 Lodash 包装器实例。

**示例**

```javascript
var object = { 'a': [{ 'b': { 'c': 3 } }, 4] };
 
_(object).at(['a[0].b.c', 'a[1]']).value();
// => [3, 4]
```

### _#chain()

在现有的包装器实例上启用显式链式调用。

**返回**

- `(Object)`: 返回新的 Lodash 包装器实例。

**示例**

```javascript
var users = [
  { 'user': 'barney', 'age': 36 },
  { 'user': 'fred',   'age': 40 }
];

// 没有显式链
_(users).head();
// => { 'user': 'barney', 'age': 36 }

// 带有显式链
_(users)
  .chain()
  .head()
  .pick('user')
  .value();
// => { 'user': 'barney' }
```

### _#commit()

执行当前的链式序列并返回一个包含结果的新 Lodash 包装器实例。这允许你在一个链中“提交”部分结果，然后继续链接其他方法。

**返回**

- `(Object)`: 返回新的 Lodash 包装器实例。

**示例**

```javascript
var array = [1, 2];
var wrapped = _(array).push(3);

console.log(array);
// => [1, 2]

wrapped = wrapped.commit();
console.log(array);
// => [1, 2, 3]

wrapped.last();
// => 3
```

### _#plant(value)

创建一个链式序列的克隆，并将 `value` 作为新的被包装值。这对于在保持相同操作序列的同时，对不同的数据集应用这些操作非常有用。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `value` | `*` | 要植入的值。 |

**返回**

- `(Object)`: 返回新的 Lodash 包装器实例。

**示例**

```javascript
function square(n) {
  return n * n;
}

var wrapped = _([1, 2]).map(square);
var other = wrapped.plant([3, 4]);

console.log(other.value());
// => [9, 16]

console.log(wrapped.value());
// => [1, 4]
```

### _#reverse()

`_.reverse` 的包装器版本。反转包装的数组。这是一个原地操作，会改变原始数组。

**返回**

- `(Object)`: 返回新的 Lodash 包装器实例。

**示例**

```javascript
var array = [1, 2, 3];

_(array).reverse().value();
// => [3, 2, 1]

console.log(array);
// => [3, 2, 1]
```

---

掌握了 Lodash 的链式调用方法，你可以构建出更具表现力和可读性的数据处理流水线。接下来，可以深入了解 [Collection](./api-collection.md) 或 [Array](./api-array.md) 方法，探索可以在链式调用中使用的强大函数。