# Seq

Lodash 的序列（或“Seq”）方法是其强大链式调用功能的基础。当你使用 `_()` 包装一个值时，会创建一个 Lodash 包装器实例，可用于以可读的、顺序的方式将多个操作链接在一起。这种方法支持隐式和显式链式调用，并利用延迟求值进行性能优化。

## 链式调用概念

方法链式调用允许你组合多个 Lodash 方法。你可以一个接一个地调用它们，而不是嵌套函数调用。链式方法的执行是延迟的，这意味着它会推迟到 `_.value()` 被调用时才执行。这使得 Lodash 能够执行“快捷融合”等优化，以合并迭代函数调用并减少创建的中间数组数量。

```d2
direction: right

"Data\n[1, 2, 3, 4]": {
  shape: document
}

"Wrapper-Object": {
  label: "Wrapper Object"
  shape: package
  
  "Operations": {
    shape: rectangle
    label: ".filter(isEven)\n.map(square)\n.take(1)"
  }
}

"Result\n[4]": {
  shape: document
}

Data -> "Wrapper-Object": "_()"
"Wrapper-Object" -> Result: ".value()"
```

### _.chain(value)

创建一个 `lodash` 包装器实例，该实例包装 `value` 并启用显式方法链序列。此类序列的结果必须使用 `_#value` 解开包装。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `value` | `*` | 要包装的值。 |

**返回**

- `Object`：返回新的 `lodash` 包装器实例。

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

### .commit()

执行链序列并返回包装后的结果。

**返回**

- `Object`：返回新的 `lodash` 包装器实例。

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

console.log(array);
// => [1, 2, 3]
```

### .plant(value)

创建链序列的克隆，并将 `value` 作为其包装值。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `value` | `*` | 要植入的值。 |

**返回**

- `Object`：返回新的 `lodash` 包装器实例。

**示例**

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

### .tap(interceptor)

此方法调用 `interceptor` 并返回 `value`。拦截器调用时带有一个参数：`(value)`。此方法的目的是“接入”方法链序列以修改中间结果。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `interceptor` | `Function` | 要调用的函数。 |

**返回**

- `*`：返回 `value`。

**示例**

```javascript
_([1, 2, 3])
 .tap(function(array) {
   // 修改输入数组。
   array.pop();
 })
 .reverse()
 .value();
// => [2, 1]
```

### .thru(interceptor)

此方法类似于 `.tap`，但它返回 `interceptor` 的结果。此方法的目的是“传递”值，在方法链序列中替换中间结果。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `interceptor` | `Function` | 要调用的函数。 |

**返回**

- `*`：返回 `interceptor` 的结果。

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

### .value()

执行链序列以解析未包装的值。

**别名**：`toJSON`、`valueOf`

**返回**

- `*`：返回解析后的未包装值。

**示例**

```javascript
_([1, 2, 3]).value();
// => [1, 2, 3]
```

---

深入了解 Lodash 的序列链式调用后，你可以编写更具表现力且更易于维护的数据转换。有关其他实用工具函数，请查看 [Util API 参考](./api-util.md)。