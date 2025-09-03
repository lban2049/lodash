# Seq

Lodash 的序列 (Seq) 函数是其强大的方法链式调用功能的基础。当你使用 `_()` 包装一个值（例如数组或对象）时，会创建一个 Lodash 包装器实例。这允许你对数据调用一系列 Lodash 方法，其中一个方法的输出将成为下一个方法的输入。这种方法有助于编写简洁、可读性强且声明式的代码。

Lodash 链式调用中的关键概念是隐式链式调用与显式链式调用以及惰性求值。

- **隐式链式调用**：通过 `_(value)` 创建。返回数组、集合或函数的方法将返回一个新的包装器实例，从而可以继续链式调用。返回单个值（例如 `_.head` 或 `_.reduce`）的方法会自动结束链式调用并返回未包装的值。
- **显式链式调用**：通过 `_.chain(value)` 创建。显式链中的所有方法都会返回一个包装器实例，即使是那些通常会返回未包装值的方法也不例外。你必须显式调用 `.value()` 才能获取最终结果。
- **惰性求值**：链式方法调用不会立即执行，而是会延迟到 `.value()` 被调用时才执行。这使得 Lodash 能够执行*快捷融合*等优化，将多个迭代器调用合并为单次处理，通过避免创建中间数组来显著提升性能。

## 链式调用流程图

下图展示了数据如何流经一个典型的 Lodash 链，并重点说明了惰性求值的概念。

```d2
direction: right

"初始数组" { 
  shape: document
  label: "[1, 2, 3, 4]"
}

"已包装" {
  shape: package
  label: "_([1, 2, 3, 4])"
}

"map(n => n * 2)" {
  shape: package
  label: "中间包装器"
}

"filter(n => n > 4)" {
  shape: package
  label: "中间包装器"
}

"结果" {
  shape: document
  label: "[6, 8]"
}

"初始数组" -> "已包装": "1. 包装值"
"已包装" -> "map(n => n * 2)": "2. 链式方法 (惰性)"
"map(n => n * 2)" -> "filter(n => n > 4)": "3. 链式方法 (惰性)"
"filter(n => n > 4)" -> "结果": "4. .value() (执行)"

```

## 方法

### `_.chain(value)`

创建一个支持显式方法链式调用的 Lodash 包装器实例。在显式链式调用中，每个方法调用都会返回一个包装器，你必须在最后调用 `.value()` 来获取最终结果。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `value` | `*` | 要包装的值。 |

**返回值**

- `(Object)`: 返回新的 `lodash` 包装器实例。

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

### `_.tap(value, interceptor)`

此方法会调用一个 `interceptor` 函数，然后返回原始的 `value`。这对于“接入”方法链以执行副作用（例如，记录中间结果）非常有用，且不会改变在链中传递的值。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `value` | `*` | 提供给 `interceptor` 的值。 |
| `interceptor` | `Function` | 要调用的函数。它接收 `value` 作为其唯一参数。 |

**返回值**

- `(*)`: 返回原始的 `value`。

**示例**

```javascript
_([1, 2, 3])
 .tap(function(array) {
   // 作为副作用改变数组。
   console.log('pop 前：', array);
   array.pop();
   console.log('pop 后：', array);
 })
 .reverse()
 .value();
// 输出：pop 前: [1, 2, 3]
// 输出：pop 后: [1, 2]
// => [2, 1]
```

### `_.thru(value, interceptor)`

此方法与 `_.tap` 类似，但它返回的是 `interceptor` 函数的结果，而不是原始的 `value`。这允许你将链中的值替换为一个新值。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `value` | `*` | 提供给 `interceptor` 的值。 |
| `interceptor` | `Function` | 要调用的函数。 |

**返回值**

- `(*)`: 返回 `interceptor` 的结果。

**示例**

```javascript
_('  abc  ')
 .chain()
 .trim()
 .thru(function(value) {
   // 拦截器（interceptor）的返回值会继续链式调用。
   return [value, value.length];
 })
 .value();
// => ['abc', 3]
```

### `_(...).[method]`

Lodash 中的许多方法都可以在包装器原型上使用，并且可以链接在一起。当一个方法返回新的数组或集合时，它通常会返回一个新的包装器实例，从而使链式调用得以继续。

**包装器方法**

| 方法 | 描述 |
|---|---|
| `at(...paths)` | `_.at` 的包装器版本。从包装的对象中根据给定的路径选择值。 |
| `commit()` | 执行链式序列并返回一个包含结果的新包装器。 |
| `plant(value)` | 创建链式序列的克隆，并将新 `value` 作为包装值。 |
| `reverse()` | `_.reverse` 的包装器版本。会改变被包装的数组。 |
| `value()` | 执行链式序列以解析并返回未包装的值。别名：`toJSON`、`valueOf`。 |

**示例：使用包装器方法**

```javascript
var object = { 'a': [{ 'b': { 'c': 3 } }, 4] };
 
// 在链式调用中使用 .at()
var result = _(object).at(['a[0].b.c', 'a[1]']).value();
// => [3, 4]

// 使用 .commit() 和 .plant()
var array = [1, 2];
var wrapped = _(array).push(3); // 惰性 push

console.log(array); // => [1, 2]

var committed = wrapped.commit(); // 执行 push
console.log(array); // => [1, 2, 3]

var planted = committed.plant(['a', 'b']); // 替换值
console.log(planted.value()); // => ['a', 'b']
```

---

理解序列链式调用是使用 Lodash 编写富有表现力且高效的数据转换的关键。链式调用中使用的许多方法都来自 [Array](./api-array.md) 和 [Collection](./api-collection.md) 类别。