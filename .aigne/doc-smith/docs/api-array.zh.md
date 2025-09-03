# 数组

Lodash 提供了一套丰富的函数，用于创建、操作、查询和转换数组。这些实用工具简化了常见的数组操作，为原生 JavaScript 方法提供了强大且高性能的替代方案，尤其是在处理复杂数据结构时。

许多这类方法会返回新数组，并且可以链式调用以实现富有表现力的数据处理。对于遍历数组和其他可迭代类型的函数，另请参阅 [集合](./api-collection.md) 文档。

---

### `_.chunk(array, [size=1])`

创建一个元素数组，这些元素被分成长度为 `size` 的组。如果 `array` 不能被均匀拆分，最后的块将是剩余的元素。

**Since**
3.0.0

**Arguments**

| Param | Type | Description |
|---|---|---|
| `array` | `Array` | 要处理的数组。 |
| `[size=1]` | `number` | 每个块的长度。 |

**Returns**

(`Array`): 返回一个包含块的新数组。

**Example**

```javascript
_.chunk(['a', 'b', 'c', 'd'], 2);
// => [['a', 'b'], ['c', 'd']]

_.chunk(['a', 'b', 'c', 'd'], 3);
// => [['a', 'b', 'c'], ['d']]
```

---

### `_.compact(array)`

创建一个移除了所有假值（falsey values）的数组。`false`、`null`、`0`、`""`、`undefined` 和 `NaN` 都被视为假值。

**Since**
0.1.0

**Arguments**

| Param | Type | Description |
|---|---|---|
| `array` | `Array` | 要压缩的数组。 |

**Returns**

(`Array`): 返回过滤掉假值后的新数组。

**Example**

```javascript
_.compact([0, 1, false, 2, '', 3]);
// => [1, 2, 3]
```

---

### `_.concat(array, ...[values])`

创建一个新数组，将 `array` 与任何其他数组或值连接起来。

**Since**
4.0.0

**Arguments**

| Param | Type | Description |
|---|---|---|
| `array` | `Array` | 要连接的数组。 |
| `...[values]` | `*` | 要连接的值。 |

**Returns**

(`Array`): 返回连接后的新数组。

**Example**

```javascript
var array = [1];
var other = _.concat(array, 2, [3], [[4]]);

console.log(other);
// => [1, 2, 3, [4]]

console.log(array);
// => [1]
```

---

### `_.difference(array, ...[values])`

创建一个包含 `array` 中有但其他给定数组中没有的值的数组，使用 `SameValueZero` 进行相等性比较。结果值的顺序和引用由第一个数组决定。

**Since**
0.1.0

**Arguments**

| Param | Type | Description |
|---|---|---|
| `array` | `Array` | 要检查的数组。 |
| `...[values]` | `Array` | 要排除的值。 |

**Returns**

(`Array`): 返回过滤后的新数组。

**Example**

```javascript
_.difference([2, 1], [2, 3]);
// => [1]
```

---

### `_.differenceBy(array, ...[values], [iteratee=_.identity])`

此方法类似于 `_.difference`，但它接受一个 `iteratee`（迭代器）。这个 `iteratee` 会对 `array` 和 `values` 中的每个元素调用，以生成用于比较的基准。结果值的顺序和引用由第一个数组决定。迭代器调用时会传入一个参数：(value)。

**Since**
4.0.0

**Arguments**

| Param | Type | Description |
|---|---|---|
| `array` | `Array` | 要检查的数组。 |
| `...[values]` | `Array` | 要排除的值。 |
| `[iteratee=_.identity]` | `Function` | 对每个元素调用的迭代器。 |

**Returns**

(`Array`): 返回过滤后的新数组。

**Example**

```javascript
_.differenceBy([2.1, 1.2], [2.3, 3.4], Math.floor);
// => [1.2]

// The `_.property` iteratee shorthand.
_.differenceBy([{ 'x': 2 }, { 'x': 1 }], [{ 'x': 1 }], 'x');
// => [{ 'x': 2 }]
```

---

### `_.differenceWith(array, ...[values], [comparator])`

此方法类似于 `_.difference`，但它接受一个 `comparator`（比较器）。这个 `comparator` 会被调用来比较 `array` 和 `values` 中的元素。结果值的顺序和引用由第一个数组决定。比较器调用时会传入两个参数：(arrVal, othVal)。

**Since**
4.0.0

**Arguments**

| Param | Type | Description |
|---|---|---|
| `array` | `Array` | 要检查的数组。 |
| `...[values]` | `Array` | 要排除的值。 |
| `[comparator]` | `Function` | 对每个元素调用的比较器。 |

**Returns**

(`Array`): 返回过滤后的新数组。

**Example**

```javascript
var objects = [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }];

_.differenceWith(objects, [{ 'x': 1, 'y': 2 }], _.isEqual);
// => [{ 'x': 2, 'y': 1 }]
```

---

### `_.drop(array, [n=1])`

创建一个 `array` 的切片，从开头移除 `n` 个元素。

**Since**
0.5.0

**Arguments**

| Param | Type | Description |
|---|---|---|
| `array` | `Array` | 要查询的数组。 |
| `[n=1]` | `number` | 要移除的元素数量。 |

**Returns**

(`Array`): 返回 `array` 的切片。

**Example**

```javascript
_.drop([1, 2, 3]);
// => [2, 3]

_.drop([1, 2, 3], 2);
// => [3]

_.drop([1, 2, 3], 5);
// => []

_.drop([1, 2, 3], 0);
// => [1, 2, 3]
```

---

### `_.dropRight(array, [n=1])`

创建一个 `array` 的切片，从末尾移除 `n` 个元素。

**Since**
3.0.0

**Arguments**

| Param | Type | Description |
|---|---|---|
| `array` | `Array` | 要查询的数组。 |
| `[n=1]` | `number` | 要移除的元素数量。 |

**Returns**

(`Array`): 返回 `array` 的切片。

**Example**

```javascript
_.dropRight([1, 2, 3]);
// => [1, 2]

_.dropRight([1, 2, 3], 2);
// => [1]

_.dropRight([1, 2, 3], 5);
// => []

_.dropRight([1, 2, 3], 0);
// => [1, 2, 3]
```

---

### `_.findIndex(array, [predicate=_.identity], [fromIndex=0])`

此方法类似于 `_.find`，但它返回第一个通过 `predicate` 真值检查的元素的索引，而不是元素本身。

**Since**
1.1.0

**Arguments**

| Param | Type | Description |
|---|---|---|
| `array` | `Array` | 要检查的数组。 |
| `[predicate=_.identity]` | `Function` | 每次迭代调用的函数。 |
| `[fromIndex=0]` | `number` | 开始搜索的索引。 |

**Returns**

(`number`): 返回找到元素的索引，否则返回 `-1`。

**Example**

```javascript
var users = [
  { 'user': 'barney',  'active': false },
  { 'user': 'fred',    'active': false },
  { 'user': 'pebbles', 'active': true }
];

_.findIndex(users, function(o) { return o.user == 'barney'; });
// => 0

// The `_.matches` iteratee shorthand.
_.findIndex(users, { 'user': 'fred', 'active': false });
// => 1
```

---

### `_.flatten(array)`

将 `array` 展开一层。

**Since**
0.1.0

**Arguments**

| Param | Type | Description |
|---|---|---|
| `array` | `Array` | 要展开的数组。 |

**Returns**

(`Array`): 返回展开后的新数组。

**Example**

```javascript
_.flatten([1, [2, [3, [4]], 5]]);
// => [1, 2, [3, [4]], 5]
```

---

### `_.fromPairs(pairs)`

`_.toPairs` 的反向操作；此方法返回一个由键值对 `pairs` 组成的对象。

**Since**
4.0.0

**Arguments**

| Param | Type | Description |
|---|---|---|
| `pairs` | `Array` | 键值对。 |

**Returns**

(`Object`): 返回新对象。

**Example**

```javascript
_.fromPairs([['a', 1], ['b', 2]]);
// => { 'a': 1, 'b': 2 }
```

---

### `_.head(array)`

获取 `array` 的第一个元素。

**Since**
0.1.0

**Arguments**

| Param | Type | Description |
|---|---|---|
| `array` | `Array` | 要查询的数组。 |

**Returns**

(`*`): 返回 `array` 的第一个元素。

**Example**

```javascript
_.head([1, 2, 3]);
// => 1

_.head([]);
// => undefined
```

---

### `_.indexOf(array, value, [fromIndex=0])`

使用 `SameValueZero` 进行相等性比较，获取 `value` 在 `array` 中首次出现的索引。如果 `fromIndex` 为负数，则将其用作从 `array` 末尾开始的偏移量。

**Since**
0.1.0

**Arguments**

| Param | Type | Description |
|---|---|---|
| `array` | `Array` | 要检查的数组。 |
| `value` | `*` | 要搜索的值。 |
| `[fromIndex=0]` | `number` | 开始搜索的索引。 |

**Returns**

(`number`): 返回匹配值的索引，否则返回 `-1`。

**Example**

```javascript
_.indexOf([1, 2, 1, 2], 2);
// => 1

// Search from the `fromIndex`.
_.indexOf([1, 2, 1, 2], 2, 2);
// => 3
```

---

### `_.join(array, [separator=','])`

将 `array` 中的所有元素转换为一个由 `separator` 分隔的字符串。

**Since**
4.0.0

**Arguments**

| Param | Type | Description |
|---|---|---|
| `array` | `Array` | 要转换的数组。 |
| `[separator=',']` | `string` | 元素分隔符。 |

**Returns**

(`string`): 返回连接后的字符串。

**Example**

```javascript
_.join(['a', 'b', 'c'], '~');
// => 'a~b~c'
```

---

### `_.pull(array, ...[values])`

使用 `SameValueZero` 进行相等性比较，从 `array` 中移除所有给定的值。此方法会改变 `array`。

**Since**
2.0.0

**Arguments**

| Param | Type | Description |
|---|---|---|
| `array` | `Array` | 要修改的数组。 |
| `...[values]` | `*` | 要移除的值。 |

**Returns**

(`Array`): 返回 `array`。

**Example**

```javascript
var array = ['a', 'b', 'c', 'a', 'b', 'c'];

_.pull(array, 'a', 'c');
console.log(array);
// => ['b', 'b']
```

---

### `_.reverse(array)`

反转 `array`，使得第一个元素变为最后一个，第二个元素变为倒数第二个，以此类推。此方法会改变 `array`。

**Since**
4.0.0

**Arguments**

| Param | Type | Description |
|---|---|---|
| `array` | `Array` | 要修改的数组。 |

**Returns**

(`Array`): 返回 `array`。

**Example**

```javascript
var array = [1, 2, 3];

_.reverse(array);
// => [3, 2, 1]

console.log(array);
// => [3, 2, 1]
```

---

### `_.union(...[arrays])`

使用 `SameValueZero` 进行相等性比较，从所有给定的数组中创建一个按顺序排列的唯一值数组。

**Since**
0.1.0

**Arguments**

| Param | Type | Description |
|---|---|---|
| `...[arrays]` | `Array` | 要检查的数组。 |

**Returns**

(`Array`): 返回组合值的新数组。

**Example**

```javascript
_.union([2], [1, 2]);
// => [2, 1]
```

---

以上是一些最常用的数组函数。如需查看完整列表和更多详细信息，请浏览 API 参考文档。对于处理数组和对象迭代的函数，请参阅 [集合](./api-collection.md) 文档。