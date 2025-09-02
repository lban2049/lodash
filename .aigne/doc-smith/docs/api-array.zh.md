# Array

Lodash 提供了一套功能强大的数组处理函数，能够简化和增强原生 JavaScript 数组的操作。这些函数覆盖了数组的创建、分割、过滤、合并、查找、排序等多种常见场景。许多函数都支持深度操作和自定义比较器，为复杂的数据处理提供了极大的便利。

本章节详细介绍了所有专门用于操作或返回数组的 Lodash 函数。对于同时适用于数组和对象的迭代函数，请参阅 [Collection](./api-collection.md) 部分。

## 函数参考

为了方便查阅，所有数组函数均按字母顺序列出。

### _.chunk(array, [size=1])

将数组（`array`）拆分成多个 `size` 长度的区块，并将这些区块组成一个新数组。 如果 `array` 无法被分割成全部等长的区块，那么最后剩余的元素将组成一个区块。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `array` | `Array` | 需要处理的数组。 |
| `[size=1]` | `number` | 每个数组区块的长度。 |

**返回**

| 类型 | 描述 |
|---|---|
| `Array` | 返回一个包含拆分区块的新数组。 |

**示例**

```javascript
_.chunk(['a', 'b', 'c', 'd'], 2);
// => [['a', 'b'], ['c', 'd']]
 
_.chunk(['a', 'b', 'c', 'd'], 3);
// => [['a', 'b', 'c'], ['d']]
```

### _.compact(array)

创建一个新数组，包含原数组中所有的非假值元素。例如 `false`、`null`、`0`、`""`、`undefined` 和 `NaN` 都是被认为是“假值”。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `array` | `Array` | 待处理的数组。 |

**返回**

| 类型 | 描述 |
|---|---|
| `Array` | 返回过滤掉假值的新数组。 |

**示例**

```javascript
_.compact([0, 1, false, 2, '', 3]);
// => [1, 2, 3]
```

### _.concat(array, ...[values])

创建一个新数组，将 `array` 与任何额外的数组或值连接起来。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `array` | `Array` | 被连接的数组。 |
| `...[values]`| `*` | 连接的值。 |

**返回**

| 类型 | 描述 |
|---|---|
| `Array` | 返回连接后的新数组。 |

**示例**

```javascript
var array = [1];
var other = _.concat(array, 2, [3], [[4]]);
 
console.log(other);
// => [1, 2, 3, [4]]
 
console.log(array);
// => [1]
```

### _.difference(array, ...[values])

创建一个新数组，这个数组中的值，是 `array` 中没有在其它 `values` 数组中出现的值。结果值的顺序和引用由第一个数组确定。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `array` | `Array` | 要检查的数组。 |
| `...[values]`| `Array` | 要排除的值的数组。 |

**返回**

| 类型 | 描述 |
|---|---|
| `Array` | 返回一个过滤值后的新数组。 |

**示例**

```javascript
_.difference([2, 1], [2, 3]);
// => [1]
```

### _.differenceBy(array, ...[values], [iteratee=_.identity])

这个方法类似 `_.difference`，但它接受一个 `iteratee`（迭代函数），这个 `iteratee` 会为 `array` 和 `values` 中的每个元素调用，并生成一个值用于比较。结果值的顺序和引用由第一个数组确定。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `array` | `Array` | 要检查的数组。 |
| `...[values]`| `Array` | 要排除的值的数组。 |
| `[iteratee=_.identity]`| `Function` | 每个元素调用的迭代函数。 |

**返回**

| 类型 | 描述 |
|---|---|
| `Array` | 返回一个过滤值后的新数组。 |

**示例**

```javascript
_.differenceBy([2.1, 1.2], [2.3, 3.4], Math.floor);
// => [1.2]
 
// The `_.property` iteratee shorthand.
_.differenceBy([{ 'x': 2 }, { 'x': 1 }], [{ 'x': 1 }], 'x');
// => [{ 'x': 2 }]
```

### _.differenceWith(array, ...[values], [comparator])

这个方法类似 `_.difference`，但它接受一个 `comparator`（比较器），用于比较 `array` 和 `values` 中的元素。结果值的顺序和引用由第一个数组确定。比较器会传入两个参数：`(arrVal, othVal)`。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `array` | `Array` | 要检查的数组。 |
| `...[values]`| `Array` | 要排除的值的数组。 |
| `[comparator]`| `Function` | 每个元素调用的比较器。 |

**返回**

| 类型 | 描述 |
|---|---|
| `Array` | 返回一个过滤值后的新数组。 |

**示例**

```javascript
var objects = [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }];
 
_.differenceWith(objects, [{ 'x': 1, 'y': 2 }], _.isEqual);
// => [{ 'x': 2, 'y': 1 }]
```

### _.drop(array, [n=1])

创建一个切片，去除 `array` 中从起点开始的 `n` 个元素。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `array` | `Array` | 要查询的数组。 |
| `[n=1]` | `number` | 要去除的元素个数。 |

**返回**

| 类型 | 描述 |
|---|---|
| `Array` | 返回 `array` 的切片。 |

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

### _.dropRight(array, [n=1])

创建一个切片，去除 `array` 中从结尾开始的 `n` 个元素。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `array` | `Array` | 要查询的数组。 |
| `[n=1]` | `number` | 要去除的元素个数。 |

**返回**

| 类型 | 描述 |
|---|---|
| `Array` | 返回 `array` 的切片。 |

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

### _.fill(array, value, [start=0], [end=array.length])

使用 `value` 值填充 `array`，从 `start` 位置开始，到 `end` 位置结束（不包含 `end` 位置）。

**注意:** 这个方法会改变 `array`。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `array` | `Array` | 要填充的数组。 |
| `value` | `*` | 填充 `array` 的值。 |
| `[start=0]` | `number` | 开始位置。 |
| `[end=array.length]` | `number` | 结束位置。 |

**返回**

| 类型 | 描述 |
|---|---|
| `Array` | 返回 `array`。 |

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

### _.findIndex(array, [predicate=_.identity], [fromIndex=0])

该方法类似 `_.find`，但它返回第一个通过 `predicate` 真值检测的元素的索引，而不是元素本身。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `array` | `Array` | 要检查的数组。 |
| `[predicate=_.identity]` | `Function` | 每次迭代调用的函数。 |
| `[fromIndex=0]` | `number` | 开始搜索的索引。 |

**返回**

| 类型 | 描述 |
|---|---|
| `number` | 返回找到的元素的索引，否则返回 `-1`。 |

**示例**

```javascript
var users = [
  { 'user': 'barney',  'active': false },
  { 'user': 'fred',    'active': false },
  { 'user': 'pebbles', 'active': true }
];
 
_.findIndex(users, function(o) { return o.user == 'barney'; });
// => 0
```

### _.findLastIndex(array, [predicate=_.identity], [fromIndex=array.length-1])

这个方法类似 `_.findIndex`，但它从右到左遍历 `collection` 的元素。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `array` | `Array` | 要检查的数组。 |
| `[predicate=_.identity]` | `Function` | 每次迭代调用的函数。 |
| `[fromIndex=array.length-1]` | `number` | 开始搜索的索引。 |

**返回**

| 类型 | 描述 |
|---|---|
| `number` | 返回找到的元素的索引，否则返回 `-1`。 |

**示例**

```javascript
var users = [
  { 'user': 'barney',  'active': true },
  { 'user': 'fred',    'active': false },
  { 'user': 'pebbles', 'active': false }
];
 
_.findLastIndex(users, function(o) { return o.user == 'pebbles'; });
// => 2
```

### _.flatten(array)

减少一级 `array` 嵌套深度。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `array` | `Array` | 需要减少嵌套层级的数组。 |

**返回**

| 类型 | 描述 |
|---|---|
| `Array` | 返回减少嵌套层级后的新数组。 |

**示例**

```javascript
_.flatten([1, [2, [3, [4]], 5]]);
// => [1, 2, [3, [4]], 5]
```

### _.flattenDeep(array)

将 `array` 递归为一维数组。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `array` | `Array` | 需要处理的数组。 |

**返回**

| 类型 | 描述 |
|---|---|
| `Array` | 返回处理后的新数组。 |

**示例**

```javascript
_.flattenDeep([1, [2, [3, [4]], 5]]);
// => [1, 2, 3, 4, 5]
```

### _.flattenDepth(array, [depth=1])

根据 `depth` 递归减少 `array` 的嵌套层级。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `array` | `Array` | 需要减少嵌套层级的数组。 |
| `[depth=1]` | `number` | 最大递归深度。 |

**返回**

| 类型 | 描述 |
|---|---|
| `Array` | 返回减少嵌套层级后的新数组。 |

**示例**

```javascript
var array = [1, [2, [3, [4]], 5]];
 
_.flattenDepth(array, 1);
// => [1, 2, [3, [4]], 5]
 
_.flattenDepth(array, 2);
// => [1, 2, 3, [4], 5]
```

### _.fromPairs(pairs)

与 `_.toPairs` 相反；这个方法返回一个由键值对 `pairs` 组成的的对象。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `pairs` | `Array` | 键值对数组。 |

**返回**

| 类型 | 描述 |
|---|---|
| `Object` | 返回一个新对象。 |

**示例**

```javascript
_.fromPairs([['a', 1], ['b', 2]]);
// => { 'a': 1, 'b': 2 }
```

### _.head(array)

获取数组 `array` 的第一个元素。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `array` | `Array` | 要查询的数组。 |

**返回**

| 类型 | 描述 |
|---|---|
| `*` | 返回数组的第一个元素。 |

**示例**

```javascript
_.head([1, 2, 3]);
// => 1
 
_.head([]);
// => undefined
```

### _.indexOf(array, value, [fromIndex=0])

使用 `SameValueZero` 等值比较，返回 `value` 在 `array` 中首次出现的索引值。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `array` | `Array` | 需要搜索的数组。 |
| `value` | `*` | 需要搜索的值。 |
| `[fromIndex=0]` | `number` | 开始搜索的索引位置。 |

**返回**

| 类型 | 描述 |
|---|---|
| `number` | 返回 `value` 的索引值，如果未找到则返回 `-1`。 |

**示例**

```javascript
_.indexOf([1, 2, 1, 2], 2);
// => 1
 
// Search from the `fromIndex`.
_.indexOf([1, 2, 1, 2], 2, 2);
// => 3
```

### _.initial(array)

获取数组 `array` 中除了最后一个元素之外的所有元素。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `array` | `Array` | 要查询的数组。 |

**返回**

| 类型 | 描述 |
|---|---|
| `Array` | 返回 `array` 的切片。 |

**示例**

```javascript
_.initial([1, 2, 3]);
// => [1, 2]
```

### _.intersection(...[arrays])

创建唯一值的数组，这个数组是所有给定数组的交集。结果值的顺序和引用由第一个数组确定。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `...[arrays]` | `Array` | 要检查的数组。 |

**返回**

| 类型 | 描述 |
|---|---|
| `Array` | 返回一个包含所有传入数组交集元素的新数组。 |

**示例**

```javascript
_.intersection([2, 1], [2, 3]);
// => [2]
```

### _.join(array, [separator=','])

将 `array` 中的所有元素转换为由 `separator` 分隔的字符串。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `array` | `Array` | 要转换的数组。 |
| `[separator=',']` | `string` | 分隔元素。 |

**返回**

| 类型 | 描述 |
|---|---|
| `string` | 返回连接后的字符串。 |

**示例**

```javascript
_.join(['a', 'b', 'c'], '~');
// => 'a~b~c'
```

### _.last(array)

获取 `array` 中的最后一个元素。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `array` | `Array` | 要查询的数组。 |

**返回**

| 类型 | 描述 |
|---|---|
| `*` | 返回 `array` 的最后一个元素。 |

**示例**

```javascript
_.last([1, 2, 3]);
// => 3
```

### _.lastIndexOf(array, value, [fromIndex=array.length-1])

这个方法类似 `_.indexOf`，但它从右到左遍历 `array` 的元素。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `array` | `Array` | 要检查的数组。 |
| `value` | `*` | 要搜索的值。 |
| `[fromIndex=array.length-1]` | `number` | 开始搜索的索引。 |

**返回**

| 类型 | 描述 |
|---|---|
| `number` | 返回匹配值的索引，否则返回 `-1`。 |

**示例**

```javascript
_.lastIndexOf([1, 2, 1, 2], 2);
// => 3
```

### _.pull(array, ...[values])

移除数组 `array` 中所有和 `values` 相等的元素。

**注意:** 这个方法会改变 `array`。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `array` | `Array` | 要修改的数组。 |
| `...[values]` | `*` | 要移除的值。 |

**返回**

| 类型 | 描述 |
|---|---|
| `Array` | 返回 `array`。 |

**示例**

```javascript
var array = ['a', 'b', 'c', 'a', 'b', 'c'];
 
_.pull(array, 'a', 'c');
console.log(array);
// => ['b', 'b']
```

### _.pullAll(array, values)

这个方法类似 `_.pull`，但它接受一个要移除值的数组。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `array` | `Array` | 要修改的数组。 |
| `values` | `Array` | 要移除的值的数组。 |

**返回**

| 类型 | 描述 |
|---|---|
| `Array` | 返回 `array`。 |

**示例**

```javascript
var array = ['a', 'b', 'c', 'a', 'b', 'c'];
 
_.pullAll(array, ['a', 'c']);
console.log(array);
// => ['b', 'b']
```

### _.reverse(array)

反转 `array`，使得第一个元素变为最后一个元素，第二个元素变为倒数第二个元素，以此类推。

**注意:** 这个方法会改变 `array`。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `array` | `Array` | 要修改的数组。 |

**返回**

| 类型 | 描述 |
|---|---|
| `Array` | 返回 `array`。 |

**示例**

```javascript
var array = [1, 2, 3];
 
_.reverse(array);
// => [3, 2, 1]
 
console.log(array);
// => [3, 2, 1]
```

### _.slice(array, [start=0], [end=array.length])

裁剪 `array`，从 `start` 位置开始，到 `end` 位置结束（不包含 `end` 位置）。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `array` | `Array` | 要裁剪的数组。 |
| `[start=0]` | `number` | 开始位置。 |
| `[end=array.length]` | `number` | 结束位置。 |

**返回**

| 类型 | 描述 |
|---|---|
| `Array` | 返回 `array` 的切片。 |

**示例**

```javascript
var array = [1, 2, 3, 4];
_.slice(array, 1, 3);
// => [2, 3]
```

### _.sortedUniq(array)

这个方法类似 `_.uniq`，但它专门为已排序的数组作了优化。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `array` | `Array` | 要检查的数组。 |

**返回**

| 类型 | 描述 |
|---|---|
| `Array` | 返回不含重复元素的新数组。 |

**示例**

```javascript
_.sortedUniq([1, 1, 2]);
// => [1, 2]
```

### _.tail(array)

获取 `array` 中除了第一个元素外的所有元素。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `array` | `Array` | 要查询的数组。 |

**返回**

| 类型 | 描述 |
|---|---|
| `Array` | 返回 `array` 的切片。 |

**示例**

```javascript
_.tail([1, 2, 3]);
// => [2, 3]
```

### _.take(array, [n=1])

创建一个 `array` 的切片，从开头取 `n` 个元素。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `array` | `Array` | 要查询的数组。 |
| `[n=1]` | `number` | 要获取的元素数量。 |

**返回**

| 类型 | 描述 |
|---|---|
| `Array` | 返回 `array` 的切片。 |

**示例**

```javascript
_.take([1, 2, 3]);
// => [1]
```

### _.union(...[arrays])

创建一个按顺序排列的唯一值组成的数组，所有给定数组的元素都使用 `SameValueZero` 进行等值比较。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `...[arrays]` | `Array` | 要检查的数组。 |

**返回**

| 类型 | 描述 |
|---|---|
| `Array` | 返回合并后的新数组。 |

**示例**

```javascript
_.union([2], [1, 2]);
// => [2, 1]
```

### _.uniq(array)

创建一个去重后的 `array` 数组副本。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `array` | `Array` | 要检查的数组。 |

**返回**

| 类型 | 描述 |
|---|---|
| `Array` | 返回不含重复元素的新数组。 |

**示例**

```javascript
_.uniq([2, 1, 2]);
// => [2, 1]
```

### _.unzip(array)

这个方法是 `_.zip` 的逆操作。给定一个已经分组的 `array`，这个方法返回一个重组后的数组。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `array` | `Array` | 要处理的已分组元素的数组。 |

**返回**

| 类型 | 描述 |
|---|---|
| `Array` | 返回重组后的元素数组。 |

**示例**

```javascript
var zipped = _.zip(['a', 'b'], [1, 2], [true, false]);
// => [['a', 1, true], ['b', 2, false]]
 
_.unzip(zipped);
// => [['a', 'b'], [1, 2], [true, false]]
```

### _.without(array, ...[values])

创建一个剔除所有给定值的 `array` 副本。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `array` | `Array` | 要检查的数组。 |
| `...[values]` | `*` | 要移除的值。 |

**返回**

| 类型 | 描述 |
|---|---|
| `Array` | 返回过滤值后的新数组。 |

**示例**

```javascript
_.without([2, 1, 2, 3], 1, 2);
// => [3]
```

### _.xor(...[arrays])

创建一个唯一值的数组，这个数组是给定所有数组的对称差集。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `...[arrays]` | `Array` | 要检查的数组。 |

**返回**

| 类型 | 描述 |
|---|---|
| `Array` | 返回一个包含所有数组对称差集元素的新数组。 |

**示例**

```javascript
_.xor([2, 1], [2, 3]);
// => [1, 3]
```

### _.zip(...[arrays])

创建一个分组元素的数组，数组的第一个元素包含所有给定数组的第一个元素，数组的第二个元素包含所有给定数组的第二个元素，以此类推。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `...[arrays]` | `Array` | 要处理的数组。 |

**返回**

| 类型 | 描述 |
|---|---|
| `Array` | 返回分组元素的新数组。 |

**示例**

```javascript
_.zip(['a', 'b'], [1, 2], [true, false]);
// => [['a', 1, true], ['b', 2, false]]
```

---

本节涵盖了 Lodash 中核心的数组操作函数。许多处理数组的函数也适用于其他可迭代的数据结构。要了解更多信息，请继续阅读 [Collection](./api-collection.md) 部分的文档。