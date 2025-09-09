# 数组

Lodash 提供了一套丰富的函数，用于操作数组。这些实用工具可帮助处理常见的任务，如拆分、筛选、转换和查询数组数据。许多函数遵循函数式编程原则，会返回新的数组，而另一些函数为了性能会直接修改原数组，这一点将在其描述中注明。对于遍历数组和其他可迭代类型的函数，请参阅 [集合](./api-collection.md) 部分。

### `_.chunk(array, [size=1])`

创建一个元素数组，这些元素被分成长度为 `size` 的组。如果 `array` 不能被均匀分割，最后一个块将是剩余的元素。

**参数**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | 要处理的数组。 |
| `[size=1]` | `number` | 每个块的长度。 |

**返回**

- `(Array)`: 返回包含块的新数组。

**示例**

```javascript
_.chunk(['a', 'b', 'c', 'd'], 2);
// => [['a', 'b'], ['c', 'd']]

_.chunk(['a', 'b', 'c', 'd'], 3);
// => [['a', 'b', 'c'], ['d']]
```

### `_.compact(array)`

创建一个移除了所有假值的数组。值 `false`、`null`、`0`、`""`、`undefined` 和 `NaN` 都是假值。

**参数**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | 要进行紧凑处理的数组。 |

**返回**

- `(Array)`: 返回筛选值后的新数组。

**示例**

```javascript
_.compact([0, 1, false, 2, '', 3]);
// => [1, 2, 3]
```

### `_.concat(array, ...[values])`

创建一个新数组，将 `array` 与任何其他数组和/或值连接起来。

**参数**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | 要连接的数组。 |
| `...[values]` | `*` | 要连接的值。 |

**返回**

- `(Array)`: 返回连接后的新数组。

**示例**

```javascript
var array = [1];
var other = _.concat(array, 2, [3], [[4]]);

console.log(other);
// => [1, 2, 3, [4]]

console.log(array);
// => [1]
```

### `_.difference(array, ...[values])`

创建一个包含 `array` 中有但其他给定数组中没有的值的数组，使用 [`SameValueZero`](http://ecma-international.org/ecma-262/7.0/#sec-samevaluezero) 进行等值比较。结果值的顺序和引用由第一个数组决定。

**注意：**与 `_.pullAll` 不同，此方法返回一个新数组。

**参数**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | 要检查的数组。 |
| `...[values]` | `Array` | 要排除的值。 |

**返回**

- `(Array)`: 返回筛选值后的新数组。

**示例**

```javascript
_.difference([2, 1], [2, 3]);
// => [1]
```

### `_.differenceBy(array, ...[values], [iteratee=_.identity])`

此方法类似于 `_.difference`，但它接受一个 `iteratee`，该函数会为 `array` 和 `values` 的每个元素调用，以生成用于比较的标准。结果值的顺序和引用由第一个数组决定。iteratee 调用时带有一个参数：(value)。

**注意：**与 `_.pullAllBy` 不同，此方法返回一个新数组。

**参数**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | 要检查的数组。 |
| `...[values]` | `Array` | 要排除的值。 |
| `[iteratee=_.identity]` | `Function` | 为每个元素调用的 iteratee。 |

**返回**

- `(Array)`: 返回筛选值后的新数组。

**示例**

```javascript
_.differenceBy([2.1, 1.2], [2.3, 3.4], Math.floor);
// => [1.2]

// `_.property` iteratee 的简写形式。
_.differenceBy([{ 'x': 2 }, { 'x': 1 }], [{ 'x': 1 }], 'x');
// => [{ 'x': 2 }]
```

### `_.differenceWith(array, ...[values], [comparator])`

此方法类似于 `_.difference`，但它接受一个 `comparator`，该函数用于比较 `array` 和 `values` 的元素。结果值的顺序和引用由第一个数组决定。comparator 调用时带有两个参数：(arrVal, othVal)。

**注意：**与 `_.pullAllWith` 不同，此方法返回一个新数组。

**参数**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | 要检查的数组。 |
| `...[values]` | `Array` | 要排除的值。 |
| `[comparator]` | `Function` | 为每个元素调用的比较器。 |

**返回**

- `(Array)`: 返回筛选值后的新数组。

**示例**

```javascript
var objects = [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }];

_.differenceWith(objects, [{ 'x': 1, 'y': 2 }], _.isEqual);
// => [{ 'x': 2, 'y': 1 }]
```

### `_.drop(array, [n=1])`

创建一个 `array` 的切片，从开头移除 `n` 个元素。

**参数**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | 要查询的数组。 |
| `[n=1]` | `number` | 要移除的元素数量。 |

**返回**

- `(Array)`: 返回 `array` 的切片。

**示例**

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

### `_.dropRight(array, [n=1])`

创建一个 `array` 的切片，从末尾移除 `n` 个元素。

**参数**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | 要查询的数组。 |
| `[n=1]` | `number` | 要移除的元素数量。 |

**返回**

- `(Array)`: 返回 `array` 的切片。

**示例**

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

### `_.fill(array, value, [start=0], [end=array.length])`

使用 `value` 填充 `array` 的元素，从 `start` 位置开始，到 `end` 位置（不包括 `end`）结束。

**注意：**此方法会修改 `array`。

**参数**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | 要填充的数组。 |
| `value` | `*` | 用于填充 `array` 的值。 |
| `[start=0]` | `number` | 起始位置。 |
| `[end=array.length]` | `number` | 结束位置。 |

**返回**

- `(Array)`: 返回 `array`。

**示例**

```javascript
var array = [1, 2, 3];

_.fill(array, 'a');
console.log(array);
// => ['a', 'a', 'a']

_.fill(Array(3), 2);
// => [2, 2, 2]

_.fill([4, 6, 8, 10], '*', 1, 3);
// => [4, '*', '*', 10]
```

### `_.flatten(array)`

将 `array` 展平一层。

**参数**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | 要展平的数组。 |

**返回**

- `(Array)`: 返回展平后的新数组。

**示例**

```javascript
_.flatten([1, [2, [3, [4]], 5]]);
// => [1, 2, [3, [4]], 5]
```

### `_.flattenDeep(array)`

递归地展平 `array`。

**参数**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | 要展平的数组。 |

**返回**

- `(Array)`: 返回展平后的新数组。

**示例**

```javascript
_.flattenDeep([1, [2, [3, [4]], 5]]);
// => [1, 2, 3, 4, 5]
```

### `_.flattenDepth(array, [depth=1])`

递归地将 `array` 展平最多 `depth` 次。

**参数**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | 要展平的数组。 |
| `[depth=1]` | `number` | 最大递归深度。 |

**返回**

- `(Array)`: 返回展平后的新数组。

**示例**

```javascript
var array = [1, [2, [3, [4]], 5]];

_.flattenDepth(array, 1);
// => [1, 2, [3, [4]], 5]

_.flattenDepth(array, 2);
// => [1, 2, 3, [4], 5]
```

### `_.fromPairs(pairs)`

`_.toPairs` 的逆方法；此方法返回一个由键值对 `pairs` 组成的对象。

**参数**

| Name | Type | Description |
|---|---|---|
| `pairs` | `Array` | 键值对。 |

**返回**

- `(Object)`: 返回新对象。

**示例**

```javascript
_.fromPairs([['a', 1], ['b', 2]]);
// => { 'a': 1, 'b': 2 }
```

### `_.head(array)`

获取 `array` 的第一个元素。别名：`_.first`。

**参数**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | 要查询的数组。 |

**返回**

- `(*)`: 返回 `array` 的第一个元素。

**示例**

```javascript
_.head([1, 2, 3]);
// => 1

_.head([]);
// => undefined
```

### `_.indexOf(array, value, [fromIndex=0])`

使用 [`SameValueZero`](http://ecma-international.org/ecma-262/7.0/#sec-samevaluezero) 进行等值比较，获取 `value` 在 `array` 中首次出现的索引。如果 `fromIndex` 是负数，则将其用作从 `array` 末尾开始的偏移量。

**参数**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | 要检查的数组。 |
| `value` | `*` | 要搜索的值。 |
| `[fromIndex=0]` | `number` | 搜索的起始索引。 |

**返回**

- `(number)`: 返回匹配值的索引，否则返回 `-1`。

**示例**

```javascript
_.indexOf([1, 2, 1, 2], 2);
// => 1

// 从 `fromIndex` 开始搜索。
_.indexOf([1, 2, 1, 2], 2, 2);
// => 3
```

### `_.initial(array)`

获取 `array` 中除最后一个元素外的所有元素。

**参数**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | 要查询的数组。 |

**返回**

- `(Array)`: 返回 `array` 的切片。

**示例**

```javascript
_.initial([1, 2, 3]);
// => [1, 2]
```

### `_.intersection(...[arrays])`

创建一个包含所有给定数组中都存在的唯一值的数组，使用 [`SameValueZero`](http://ecma-international.org/ecma-262/7.0/#sec-samevaluezero) 进行等值比较。结果值的顺序和引用由第一个数组决定。

**参数**

| Name | Type | Description |
|---|---|---|
| `...[arrays]` | `Array` | 要检查的数组。 |

**返回**

- `(Array)`: 返回包含交集值的新数组。

**示例**

```javascript
_.intersection([2, 1], [2, 3]);
// => [2]
```

### `_.join(array, [separator=','])`

将 `array` 中的所有元素转换为一个由 `separator` 分隔的字符串。

**参数**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | 要转换的数组。 |
| `[separator=',']` | `string` | 元素分隔符。 |

**返回**

- `(string)`: 返回连接后的字符串。

**示例**

```javascript
_.join(['a', 'b', 'c'], '~');
// => 'a~b~c'
```

### `_.last(array)`

获取 `array` 的最后一个元素。

**参数**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | 要查询的数组。 |

**返回**

- `(*)`: 返回 `array` 的最后一个元素。

**示例**

```javascript
_.last([1, 2, 3]);
// => 3
```

### `_.lastIndexOf(array, value, [fromIndex=array.length-1])`

此方法类似于 `_.indexOf`，但它是从右到左遍历 `array` 的元素。

**参数**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | 要检查的数组。 |
| `value` | `*` | 要搜索的值。 |
| `[fromIndex=array.length-1]` | `number` | 搜索的起始索引。 |

**返回**

- `(number)`: 返回匹配值的索引，否则返回 `-1`。

**示例**

```javascript
_.lastIndexOf([1, 2, 1, 2], 2);
// => 3

// 从 `fromIndex` 开始搜索。
_.lastIndexOf([1, 2, 1, 2], 2, 2);
// => 1
```

### `_.pull(array, ...[values])`

从 `array` 中移除所有给定的值，使用 [`SameValueZero`](http://ecma-international.org/ecma-262/7.0/#sec-samevaluezero) 进行等值比较。

**注意：**此方法会修改 `array`。

**参数**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | 要修改的数组。 |
| `...[values]` | `*` | 要移除的值。 |

**返回**

- `(Array)`: 返回 `array`。

**示例**

```javascript
var array = ['a', 'b', 'c', 'a', 'b', 'c'];

_.pull(array, 'a', 'c');
console.log(array);
// => ['b', 'b']
```

### `_.reverse(array)`

反转 `array`，使得第一个元素变为最后一个，第二个元素变为倒数第二个，以此类推。

**注意：**此方法会修改 `array`，并且基于 [`Array#reverse`](https://mdn.io/Array/reverse)。

**参数**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | 要修改的数组。 |

**返回**

- `(Array)`: 返回 `array`。

**示例**

```javascript
var array = [1, 2, 3];

_.reverse(array);
// => [3, 2, 1]

console.log(array);
// => [3, 2, 1]
```

### `_.sortedUniq(array)`

此方法类似于 `_.uniq`，但它是为已排序的数组设计和优化的。

**参数**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | 要检查的数组。 |

**返回**

- `(Array)`: 返回去重后的新数组。

**示例**

```javascript
_.sortedUniq([1, 1, 2]);
// => [1, 2]
```

### `_.union(...[arrays])`

创建一个按顺序包含所有给定数组中唯一值的数组，使用 [`SameValueZero`](http://ecma-international.org/ecma-262/7.0/#sec-samevaluezero) 进行等值比较。

**参数**

| Name | Type | Description |
|---|---|---|
| `...[arrays]` | `Array` | 要检查的数组。 |

**返回**

- `(Array)`: 返回包含组合值的新数组。

**示例**

```javascript
_.union([2], [1, 2]);
// => [2, 1]
```

### `_.uniq(array)`

创建一个去重后的数组版本，使用 [`SameValueZero`](http://ecma-international.org/ecma-262/7.0/#sec-samevaluezero) 进行等值比较，其中只保留每个元素的第一次出现。结果值的顺序由它们在数组中出现的顺序决定。

**参数**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | 要检查的数组。 |

**返回**

- `(Array)`: 返回去重后的新数组。

**示例**

```javascript
_.uniq([2, 1, 2]);
// => [2, 1]
```

### `_.without(array, ...[values])`

创建一个排除所有给定值的数组，使用 [`SameValueZero`](http://ecma-international.org/ecma-262/7.0/#sec-samevaluezero) 进行等值比较。

**注意：**与 `_.pull` 不同，此方法返回一个新数组。

**参数**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | 要检查的数组。 |
| `...[values]` | `*` | 要排除的值。 |

**返回**

- `(Array)`: 返回筛选值后的新数组。

**示例**

```javascript
_.without([2, 1, 2, 3], 1, 2);
// => [3]
```

### `_.zip(...[arrays])`

创建一个分组元素的数组，第一个分组包含所有给定数组的第一个元素，第二个分组包含所有给定数组的第二个元素，以此类推。

**参数**

| Name | Type | Description |
|---|---|---|
| `...[arrays]` | `Array` | 要处理的数组。 |

**返回**

- `(Array)`: 返回包含分组元素的新数组。

**示例**

```javascript
_.zip(['a', 'b'], [1, 2], [true, false]);
// => [['a', 1, true], ['b', 2, false]]
```

---

现在您已经了解了 Lodash 的数组操作功能。要继续学习，您可以深入研究适用于数组和对象的 [集合](./api-collection.md) 函数，或探索用于文本操作的 [字符串](./api-string.md) 实用工具。
