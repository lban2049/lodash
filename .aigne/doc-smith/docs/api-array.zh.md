# Array

Lodash 提供了一套功能强大的数组处理函数，能够简化和增强原生 JavaScript 数组的操作。这些函数覆盖了数组的创建、分割、过滤、合并、查找、排序等多种常见场景。许多函数都支持深度操作和自定义比较器，为复杂的数据处理提供了极大的便利。

本章节详细介绍了所有专门用于操作或返回数组的 Lodash 函数。对于同时适用于数组和对象的迭代函数，请参阅 [/api/collection](./api-collection.md) 部分。

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

### _.dropRightWhile(array, [predicate=_.identity])

创建一个 `array` 的切片，从结尾开始去除元素，直到 `predicate` 返回假值。`predicate` 会接收三个参数： (value, index, array)。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `array` | `Array` | 要查询的数组。 |
| `[predicate=_.identity]` | `Function` | 每次迭代调用的函数。 |

**返回**

| 类型 | 描述 |
|---|---|
| `Array` | 返回 `array` 的切片。 |

**示例**

```javascript
var users = [
  { 'user': 'barney',  'active': true },
  { 'user': 'fred',    'active': false },
  { 'user': 'pebbles', 'active': false }
];

_.dropRightWhile(users, function(o) { return !o.active; });
// => objects for ['barney']
```

### _.dropWhile(array, [predicate=_.identity])

创建一个 `array` 的切片，从开头开始去除元素，直到 `predicate` 返回假值。`predicate` 会接收三个参数： (value, index, array)。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `array` | `Array` | 要查询的数组。 |
| `[predicate=_.identity]` | `Function` | 每次迭代调用的函数。 |

**返回**

| 类型 | 描述 |
|---|---|
| `Array` | 返回 `array` 的切片。 |

**示例**

```javascript
var users = [
  { 'user': 'barney',  'active': false },
  { 'user': 'fred',    'active': false },
  { 'user': 'pebbles', 'active': true }
];

_.dropWhile(users, function(o) { return !o.active; });
// => objects for ['pebbles']
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

### _.intersectionBy(...[arrays], [iteratee=_.identity])

这个方法类似 `_.intersection`，但它接受一个 `iteratee`，这个 `iteratee` 会为每个 `arrays` 的每个元素调用以生成比较的标准。结果值的顺序和引用由第一个数组确定。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `...[arrays]` | `Array` | 要检查的数组。 |
| `[iteratee=_.identity]` | `Function` | 每个元素调用的迭代函数。 |

**返回**

| 类型 | 描述 |
|---|---|
| `Array` | 返回一个包含所有传入数组交集元素的新数组。 |

**示例**

```javascript
_.intersectionBy([2.1, 1.2], [2.3, 3.4], Math.floor);
// => [2.1]
```

### _.intersectionWith(...[arrays], [comparator])

这个方法类似 `_.intersection`，但它接受一个 `comparator`，用于比较 `arrays` 中的元素。结果值的顺序和引用由第一个数组确定。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `...[arrays]` | `Array` | 要检查的数组。 |
| `[comparator]` | `Function` | 每个元素调用的比较器。 |

**返回**

| 类型 | 描述 |
|---|---|
| `Array` | 返回一个包含所有传入数组交集元素的新数组。 |

**示例**

```javascript
var objects = [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }];
var others = [{ 'x': 1, 'y': 1 }, { 'x': 1, 'y': 2 }];

_.intersectionWith(objects, others, _.isEqual);
// => [{ 'x': 1, 'y': 2 }]
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

### _.nth(array, [n=0])

获取 `array` 中索引为 `n` 的元素。如果 `n` 为负数，则返回从结尾开始的第 n 个元素。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `array` | `Array` | 要查询的数组。 |
| `[n=0]` | `number` | 要返回的元素的索引。 |

**返回**

| 类型 | 描述 |
|---|---|
| `*` | 返回 `array` 的第 n 个元素。 |

**示例**

```javascript
var array = ['a', 'b', 'c', 'd'];

_.nth(array, 1);
// => 'b'

_.nth(array, -2);
// => 'c';
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

### _.pullAllBy(array, values, [iteratee=_.identity])

这个方法类似 `_.pullAll`，但它接受一个 `iteratee`，这个 `iteratee` 会为 `array` 和 `values` 的每个元素调用以生成比较的标准。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `array` | `Array` | 要修改的数组。 |
| `values` | `Array` | 要移除的值的数组。 |
| `[iteratee=_.identity]` | `Function` | 每个元素调用的迭代函数。 |

**返回**

| 类型 | 描述 |
|---|---|
| `Array` | 返回 `array`。 |

**示例**

```javascript
var array = [{ 'x': 1 }, { 'x': 2 }, { 'x': 3 }, { 'x': 1 }];

_.pullAllBy(array, [{ 'x': 1 }, { 'x': 3 }], 'x');
console.log(array);
// => [{ 'x': 2 }]
```

### _.pullAllWith(array, values, [comparator])

这个方法类似 `_.pullAll`，但它接受一个 `comparator`，用于比较 `array` 和 `values` 中的元素。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `array` | `Array` | 要修改的数组。 |
| `values` | `Array` | 要移除的值的数组。 |
| `[comparator]` | `Function` | 每个元素调用的比较器。 |

**返回**

| 类型 | 描述 |
|---|---|
| `Array` | 返回 `array`。 |

**示例**

```javascript
var array = [{ 'x': 1, 'y': 2 }, { 'x': 3, 'y': 4 }, { 'x': 5, 'y': 6 }];

_.pullAllWith(array, [{ 'x': 3, 'y': 4 }], _.isEqual);
console.log(array);
// => [{ 'x': 1, 'y': 2 }, { 'x': 5, 'y': 6 }]
```

### _.pullAt(array, ...[indexes])

根据索引 `indexes` 移除 `array` 中的元素，并返回被移除元素的数组。

**注意:** 这个方法会改变 `array`。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `array` | `Array` | 要修改的数组。 |
| `...[indexes]` | `(number|number[])` | 要移除的元素的索引。 |

**返回**

| 类型 | 描述 |
|---|---|
| `Array` | 返回被移除元素的数组。 |

**示例**

```javascript
var array = ['a', 'b', 'c', 'd'];
var pulled = _.pullAt(array, [1, 3]);

console.log(array);
// => ['a', 'c']

console.log(pulled);
// => ['b', 'd']
```

### _.remove(array, [predicate=_.identity])

移除 `array` 中 `predicate` 返回真值的所有元素，并返回被移除元素的数组。`predicate` 会接收三个参数：(value, index, array)。

**注意:** 这个方法会改变 `array`。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `array` | `Array` | 要修改的数组。 |
| `[predicate=_.identity]` | `Function` | 每次迭代调用的函数。 |

**返回**

| 类型 | 描述 |
|---|---|
| `Array` | 返回被移除元素的数组。 |

**示例**

```javascript
var array = [1, 2, 3, 4];
var evens = _.remove(array, function(n) {
  return n % 2 == 0;
});

console.log(array);
// => [1, 3]

console.log(evens);
// => [2, 4]
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

### _.sortedIndex(array, value)

使用二进制搜索来确定 `value` 应该插入到 `array` 中的最低索引位置，以维持其排序顺序。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `array` | `Array` | 要检查的已排序数组。 |
| `value` | `*` | 要评估的值。 |

**返回**

| 类型 | 描述 |
|---|---|
| `number` | 返回 `value` 应该插入到 `array` 的索引。 |

**示例**

```javascript
_.sortedIndex([30, 50], 40);
// => 1
```

### _.sortedIndexBy(array, value, [iteratee=_.identity])

这个方法类似 `_.sortedIndex`，但它接受一个 `iteratee`，用于为 `value` 和 `array` 的每个元素计算排序标准。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `array` | `Array` | 要检查的已排序数组。 |
| `value` | `*` | 要评估的值。 |
| `[iteratee=_.identity]` | `Function` | 每个元素调用的迭代函数。 |

**返回**

| 类型 | 描述 |
|---|---|
| `number` | 返回 `value` 应该插入到 `array` 的索引。 |

**示例**

```javascript
var objects = [{ 'x': 4 }, { 'x': 5 }];

_.sortedIndexBy(objects, { 'x': 4 }, function(o) { return o.x; });
// => 0
```

### _.sortedIndexOf(array, value)

这个方法类似 `_.indexOf`，但它对一个已排序的 `array` 执行二进制搜索。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `array` | `Array` | 要检查的数组。 |
| `value` | `*` | 要搜索的值。 |

**返回**

| 类型 | 描述 |
|---|---|
| `number` | 返回匹配值的索引，否则返回 `-1`。 |

**示例**

```javascript
_.sortedIndexOf([4, 5, 5, 5, 6], 5);
// => 1
```

### _.sortedLastIndex(array, value)

这个方法类似 `_.sortedIndex`，但它返回 `value` 应该插入到 `array` 中的最高索引位置，以维持其排序顺序。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `array` | `Array` | 要检查的已排序数组。 |
| `value` | `*` | 要评估的值。 |

**返回**

| 类型 | 描述 |
|---|---|
| `number` | 返回 `value` 应该插入到 `array` 的索引。 |

**示例**

```javascript
_.sortedLastIndex([4, 5, 5, 5, 6], 5);
// => 4
```

### _.sortedLastIndexBy(array, value, [iteratee=_.identity])

这个方法类似 `_.sortedLastIndex`，但它接受一个 `iteratee`，用于为 `value` 和 `array` 的每个元素计算排序标准。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `array` | `Array` | 要检查的已排序数组。 |
| `value` | `*` | 要评估的值。 |
| `[iteratee=_.identity]` | `Function` | 每个元素调用的迭代函数。 |

**返回**

| 类型 | 描述 |
|---|---|
| `number` | 返回 `value` 应该插入到 `array` 的索引。 |

**示例**

```javascript
var objects = [{ 'x': 4 }, { 'x': 5 }];

_.sortedLastIndexBy(objects, { 'x': 4 }, 'x');
// => 1
```

### _.sortedLastIndexOf(array, value)

这个方法类似 `_.lastIndexOf`，但它对一个已排序的 `array` 执行二进制搜索。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `array` | `Array` | 要检查的数组。 |
| `value` | `*` | 要搜索的值。 |

**返回**

| 类型 | 描述 |
|---|---|
| `number` | 返回匹配值的索引，否则返回 `-1`。 |

**示例**

```javascript
_.sortedLastIndexOf([4, 5, 5, 5, 6], 5);
// => 3
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

### _.sortedUniqBy(array, [iteratee])

这个方法类似 `_.uniqBy`，但它专门为已排序的数组作了优化。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `array` | `Array` | 要检查的数组。 |
| `[iteratee]` | `Function` | 每个元素调用的迭代函数。 |

**返回**

| 类型 | 描述 |
|---|---|
| `Array` | 返回不含重复元素的新数组。 |

**示例**

```javascript
_.sortedUniqBy([1.1, 1.2, 2.3, 2.4], Math.floor);
// => [1.1, 2.3]
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

### _.takeRight(array, [n=1])

创建一个 `array` 的切片，从结尾取 `n` 个元素。

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
_.takeRight([1, 2, 3]);
// => [3]
```

### _.takeRightWhile(array, [predicate=_.identity])

创建一个 `array` 的切片，从结尾开始获取元素，直到 `predicate` 返回假值。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `array` | `Array` | 要查询的数组。 |
| `[predicate=_.identity]` | `Function` | 每次迭代调用的函数。 |

**返回**

| 类型 | 描述 |
|---|---|
| `Array` | 返回 `array` 的切片。 |

**示例**

```javascript
var users = [
  { 'user': 'barney',  'active': true },
  { 'user': 'fred',    'active': false },
  { 'user': 'pebbles', 'active': false }
];

_.takeRightWhile(users, function(o) { return !o.active; });
// => objects for ['fred', 'pebbles']
```

### _.takeWhile(array, [predicate=_.identity])

创建一个 `array` 的切片，从开头开始获取元素，直到 `predicate` 返回假值。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `array` | `Array` | 要查询的数组。 |
| `[predicate=_.identity]` | `Function` | 每次迭代调用的函数。 |

**返回**

| 类型 | 描述 |
|---|---|
| `Array` | 返回 `array` 的切片。 |

**示例**

```javascript
var users = [
  { 'user': 'barney',  'active': false },
  { 'user': 'fred',    'active': false },
  { 'user': 'pebbles', 'active': true }
];

_.takeWhile(users, function(o) { return !o.active; });
// => objects for ['barney', 'fred']
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

### _.unionBy(...[arrays], [iteratee=_.identity])

这个方法类似 `_.union`，但它接受一个 `iteratee`，用于为每个 `arrays` 的每个元素调用以生成唯一性比较的标准。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `...[arrays]` | `Array` | 要检查的数组。 |
| `[iteratee=_.identity]` | `Function` | 每个元素调用的迭代函数。 |

**返回**

| 类型 | 描述 |
|---|---|
| `Array` | 返回合并后的新数组。 |

**示例**

```javascript
_.unionBy([2.1], [1.2, 2.3], Math.floor);
// => [2.1, 1.2]
```

### _.unionWith(...[arrays], [comparator])

这个方法类似 `_.union`，但它接受一个 `comparator`，用于比较 `arrays` 中的元素。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `...[arrays]` | `Array` | 要检查的数组。 |
| `[comparator]` | `Function` | 每个元素调用的比较器。 |

**返回**

| 类型 | 描述 |
|---|---|
| `Array` | 返回合并后的新数组。 |

**示例**

```javascript
var objects = [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }];
var others = [{ 'x': 1, 'y': 1 }, { 'x': 1, 'y': 2 }];

_.unionWith(objects, others, _.isEqual);
// => [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }, { 'x': 1, 'y': 1 }]
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

### _.uniqBy(array, [iteratee=_.identity])

这个方法类似 `_.uniq`，但它接受一个 `iteratee`，用于为 `array` 的每个元素调用以生成唯一性比较的标准。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `array` | `Array` | 要检查的数组。 |
| `[iteratee=_.identity]` | `Function` | 每个元素调用的迭代函数。 |

**返回**

| 类型 | 描述 |
|---|---|
| `Array` | 返回不含重复元素的新数组。 |

**示例**

```javascript
_.uniqBy([2.1, 1.2, 2.3], Math.floor);
// => [2.1, 1.2]
```

### _.uniqWith(array, [comparator])

这个方法类似 `_.uniq`，但它接受一个 `comparator`，用于比较 `array` 中的元素。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `array` | `Array` | 要检查的数组。 |
| `[comparator]` | `Function` | 每个元素调用的比较器。 |

**返回**

| 类型 | 描述 |
|---|---|
| `Array` | 返回不含重复元素的新数组。 |

**示例**

```javascript
var objects = [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }, { 'x': 1, 'y': 2 }];

_.uniqWith(objects, _.isEqual);
// => [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }]
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

### _.unzipWith(array, [iteratee=_.identity])

这个方法类似 `_.unzip`，但它接受一个 `iteratee` 来指定如何组合重组后的值。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `array` | `Array` | 要处理的已分组元素的数组。 |
| `[iteratee=_.identity]` | `Function` | 组合重组值的函数。 |

**返回**

| 类型 | 描述 |
|---|---|
| `Array` | 返回重组后的元素数组。 |

**示例**

```javascript
var zipped = _.zip([1, 2], [10, 20], [100, 200]);
// => [[1, 10, 100], [2, 20, 200]]

_.unzipWith(zipped, _.add);
// => [3, 30, 300]
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

### _.xorBy(...[arrays], [iteratee=_.identity])

这个方法类似 `_.xor`，但它接受一个 `iteratee`，用于为每个 `arrays` 的每个元素调用以生成比较的标准。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `...[arrays]` | `Array` | 要检查的数组。 |
| `[iteratee=_.identity]` | `Function` | 每个元素调用的迭代函数。 |

**返回**

| 类型 | 描述 |
|---|---|
| `Array` | 返回一个包含所有数组对称差集元素的新数组。 |

**示例**

```javascript
_.xorBy([2.1, 1.2], [2.3, 3.4], Math.floor);
// => [1.2, 3.4]
```

### _.xorWith(...[arrays], [comparator])

这个方法类似 `_.xor`，但它接受一个 `comparator`，用于比较 `arrays` 中的元素。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `...[arrays]` | `Array` | 要检查的数组。 |
| `[comparator]` | `Function` | 每个元素调用的比较器。 |

**返回**

| 类型 | 描述 |
|---|---|
| `Array` | 返回一个包含所有数组对称差集元素的新数组。 |

**示例**

```javascript
var objects = [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }];
var others = [{ 'x': 1, 'y': 1 }, { 'x': 1, 'y': 2 }];

_.xorWith(objects, others, _.isEqual);
// => [{ 'x': 2, 'y': 1 }, { 'x': 1, 'y': 1 }]
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

### _.zipObject([props=[]], [values=[]])

这个方法类似 `_.fromPairs`，但它接受两个数组，一个作为属性标识符（键），另一个作为相应的值。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `[props=[]]` | `Array` | 属性标识符。 |
| `[values=[]]` | `Array` | 属性值。 |

**返回**

| 类型 | 描述 |
|---|---|
| `Object` | 返回新对象。 |

**示例**

```javascript
_.zipObject(['a', 'b'], [1, 2]);
// => { 'a': 1, 'b': 2 }
```

### _.zipObjectDeep([props=[]], [values=[]])

这个方法类似 `_.zipObject`，但它支持属性路径。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `[props=[]]` | `Array` | 属性标识符。 |
| `[values=[]]` | `Array` | 属性值。 |

**返回**

| 类型 | 描述 |
|---|---|
| `Object` | 返回新对象。 |

**示例**

```javascript
_.zipObjectDeep(['a.b[0].c', 'a.b[1].d'], [1, 2]);
// => { 'a': { 'b': [{ 'c': 1 }, { 'd': 2 }] } }
```

### _.zipWith(...[arrays], [iteratee=_.identity])

这个方法类似 `_.zip`，但它接受一个 `iteratee` 来指定如何组合分组后的值。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `...[arrays]` | `Array` | 要处理的数组。 |
| `[iteratee=_.identity]` | `Function` | 组合重组值的函数。 |

**返回**

| 类型 | 描述 |
|---|---|
| `Array` | 返回分组元素的新数组。 |

**示例**

```javascript
_.zipWith([1, 2], [10, 20], [100, 200], function(a, b, c) {
  return a + b + c;
});
// => [111, 222]
```

---

本节涵盖了 Lodash 中核心的数组操作函数。许多处理数组的函数也适用于其他可迭代的数据结构。要了解更多信息，请继续阅读 [/api/collection](./api-collection.md) 部分的文档。