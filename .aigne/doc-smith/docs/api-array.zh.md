# 数组

本节为所有操作或返回数组的 Lodash 函数提供了详细的参考。这些函数对于创建、分割、组合、修改和过滤数组数据至关重要。其中大部分方法会返回一个新数组，除非明确说明（例如 `_.pull`），否则不会改变输入数组。

对于遍历数组和其他类型集合（如对象）的函数，请参阅 [Collection](./api-collection.md) 文档。

---

## chunk

创建一个元素数组，这些元素被分割成长度为 `size` 的组。如果 `array` 不能被平均分割，那么最后的块将是剩余的元素。

_(自 3.0.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | 要处理的数组。 |
| `[size=1]` | `number` | 每个块的长度。 |

### Returns

(`Array`): 返回新的块数组。

### Example

```javascript
_.chunk(['a', 'b', 'c', 'd'], 2);
// => [['a', 'b'], ['c', 'd']]

_.chunk(['a', 'b', 'c', 'd'], 3);
// => [['a', 'b', 'c'], ['d']]
```

---

## compact

创建一个移除了所有假值 (falsey values) 的数组。`false`、`null`、`0`、`""`、`undefined` 和 `NaN` 均被视为假值。

_(自 0.1.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | 要压缩的数组。 |

### Returns

(`Array`): 返回过滤后的新数组。

### Example

```javascript
_.compact([0, 1, false, 2, '', 3]);
// => [1, 2, 3]
```

---

## concat

创建一个新数组，将 `array` 与任何额外的数组和/或值拼接起来。

_(自 4.0.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | 要拼接的数组。 |
| `[...values]` | `*` | 要拼接的值。 |

### Returns

(`Array`): 返回拼接后的新数组。

### Example

```javascript
var array = [1];
var other = _.concat(array, 2, [3], [[4]]);

console.log(other);
// => [1, 2, 3, [4]]

console.log(array);
// => [1]
```

---

## difference

使用 [`SameValueZero`](http://ecma-international.org/ecma-262/7.0/#sec-samevaluezero) 进行相等性比较，创建一个包含 `array` 中有而其他给定数组中没有的值的数组。结果值的顺序和引用由第一个数组确定。

**注意：** 与 `_.pullAll` 不同，此方法返回一个新数组。

_(自 0.1.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | 要检查的数组。 |
| `[...values]` | `Array` | 要排除的值。 |

### Returns

(`Array`): 返回过滤后的新数组。

### Example

```javascript
_.difference([2, 1], [2, 3]);
// => [1]
```

---

## differenceBy

此方法类似于 `_.difference`，但它接受一个 `iteratee`，该 `iteratee` 会为 `array` 和 `values` 的每个元素调用，以生成用于比较的标准。结果值的顺序和引用由第一个数组确定。该 iteratee 调用时会传入一个参数：(value)。

**注意：** 与 `_.pullAllBy` 不同，此方法返回一个新数组。

_(自 4.0.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | 要检查的数组。 |
| `[...values]` | `Array` | 要排除的值。 |
| `[iteratee=_.identity]` | `Function` | 每个元素调用的 iteratee。 |

### Returns

(`Array`): 返回过滤后的新数组。

### Example

```javascript
_.differenceBy([2.1, 1.2], [2.3, 3.4], Math.floor);
// => [1.2]

// `_.property` iteratee 速记。
_.differenceBy([{ 'x': 2 }, { 'x': 1 }], [{ 'x': 1 }], 'x');
// => [{ 'x': 2 }]
```

---

## differenceWith

此方法类似于 `_.difference`，但它接受一个 `comparator`，该 `comparator` 用于比较 `array` 和 `values` 的元素。结果值的顺序和引用由第一个数组确定。该 comparator 调用时会传入两个参数：(arrVal, othVal)。

**注意：** 与 `_.pullAllWith` 不同，此方法返回一个新数组。

_(自 4.0.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | 要检查的数组。 |
| `[...values]` | `Array` | 要排除的值。 |
| `[comparator]` | `Function` | 每个元素调用的 comparator。 |

### Returns

(`Array`): 返回过滤后的新数组。

### Example

```javascript
var objects = [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }];

_.differenceWith(objects, [{ 'x': 1, 'y': 2 }], _.isEqual);
// => [{ 'x': 2, 'y': 1 }]
```

---

## drop

创建一个 `array` 的切片，从开头移除 `n` 个元素。

_(自 0.5.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | 要查询的数组。 |
| `[n=1]` | `number` | 要移除的元素数量。 |

### Returns

(`Array`): 返回 `array` 的切片。

### Example

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

## dropRight

创建一个 `array` 的切片，从末尾移除 `n` 个元素。

_(自 3.0.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | 要查询的数组。 |
| `[n=1]` | `number` | 要移除的元素数量。 |

### Returns

(`Array`): 返回 `array` 的切片。

### Example

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

## dropRightWhile

创建一个 `array` 的切片，从末尾开始移除元素，直到 `predicate` 返回假值为止。该 predicate 调用时会传入三个参数：(value, index, array)。

_(自 3.0.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | 要查询的数组。 |
| `[predicate=_.identity]` | `Function` | 每次迭代调用的函数。 |

### Returns

(`Array`): 返回 `array` 的切片。

### Example

```javascript
var users = [
  { 'user': 'barney',  'active': true },
  { 'user': 'fred',    'active': false },
  { 'user': 'pebbles', 'active': false }
];

_.dropRightWhile(users, function(o) { return !o.active; });
// => ['barney'] 对应的 objects
```

---

## dropWhile

创建一个 `array` 的切片，从开头开始移除元素，直到 `predicate` 返回假值为止。该 predicate 调用时会传入三个参数：(value, index, array)。

_(自 3.0.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | 要查询的数组。 |
| `[predicate=_.identity]` | `Function` | 每次迭代调用的函数。 |

### Returns

(`Array`): 返回 `array` 的切片。

### Example

```javascript
var users = [
  { 'user': 'barney',  'active': false },
  { 'user': 'fred',    'active': false },
  { 'user': 'pebbles', 'active': true }
];

_.dropWhile(users, function(o) { return !o.active; });
// => ['pebbles'] 对应的 objects
```

---

## fill

使用 `value` 填充 `array` 中的元素，从 `start` 位置开始到 `end` 位置结束（不包括 `end` 位置）。

**注意：** 此方法会改变 `array`。

_(自 3.2.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | 要填充的数组。 |
| `value` | `*` | 用于填充 `array` 的值。 |
| `[start=0]` | `number` | 起始位置。 |
| `[end=array.length]` | `number` | 结束位置。 |

### Returns

(`Array`): 返回 `array`。

### Example

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

---

## findIndex

此方法类似于 `_.find`，但它返回第一个使 `predicate` 返回真值的元素的索引，而不是元素本身。

_(自 1.1.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | 要检查的数组。 |
| `[predicate=_.identity]` | `Function` | 每次迭代调用的函数。 |
| `[fromIndex=0]` | `number` | 开始搜索的索引。 |

### Returns

(`number`): 返回找到的元素的索引，否则返回 `-1`。

### Example

```javascript
var users = [
  { 'user': 'barney',  'active': false },
  { 'user': 'fred',    'active': false },
  { 'user': 'pebbles', 'active': true }
];

_.findIndex(users, function(o) { return o.user == 'barney'; });
// => 0
```

---

## findLastIndex

此方法类似于 `_.findIndex`，但它是从右到左遍历 `collection` 的元素。

_(自 2.0.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | 要检查的数组。 |
| `[predicate=_.identity]` | `Function` | 每次迭代调用的函数。 |
| `[fromIndex=array.length-1]` | `number` | 开始搜索的索引。 |

### Returns

(`number`): 返回找到的元素的索引，否则返回 `-1`。

### Example

```javascript
var users = [
  { 'user': 'barney',  'active': true },
  { 'user': 'fred',    'active': false },
  { 'user': 'pebbles', 'active': false }
];

_.findLastIndex(users, function(o) { return o.user == 'pebbles'; });
// => 2
```

---

## flatten

将 `array` 展平一层。

_(自 0.1.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | 要展平的数组。 |

### Returns

(`Array`): 返回展平后的新数组。

### Example

```javascript
_.flatten([1, [2, [3, [4]], 5]]);
// => [1, 2, [3, [4]], 5]
```

---

## flattenDeep

递归地展平 `array`。

_(自 3.0.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | 要展平的数组。 |

### Returns

(`Array`): 返回展平后的新数组。

### Example

```javascript
_.flattenDeep([1, [2, [3, [4]], 5]]);
// => [1, 2, 3, 4, 5]
```

---

## flattenDepth

递归地将 `array` 展平 `depth` 次。

_(自 4.4.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | 要展平的数组。 |
| `[depth=1]` | `number` | 最大递归深度。 |

### Returns

(`Array`): 返回展平后的新数组。

### Example

```javascript
var array = [1, [2, [3, [4]], 5]];

_.flattenDepth(array, 1);
// => [1, 2, [3, [4]], 5]

_.flattenDepth(array, 2);
// => [1, 2, 3, [4], 5]
```

---

## fromPairs

`_.toPairs` 的反向方法；此方法返回一个由键值对 `pairs` 组成的 object。

_(自 4.0.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `pairs` | `Array` | 键值对。 |

### Returns

(`Object`): 返回新 object。

### Example

```javascript
_.fromPairs([['a', 1], ['b', 2]]);
// => { 'a': 1, 'b': 2 }
```

---

## head

获取 `array` 的第一个元素。

_(自 0.1.0 起)_

_别名：`first`_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | 要查询的数组。 |

### Returns

(`*`): 返回 `array` 的第一个元素。

### Example

```javascript
_.head([1, 2, 3]);
// => 1

_.head([]);
// => undefined
```

---

## indexOf

使用 [`SameValueZero`](http://ecma-international.org/ecma-262/7.0/#sec-samevaluezero) 进行相等性比较，获取 `value` 在 `array` 中首次出现的索引。如果 `fromIndex` 为负数，则将其用作从 `array` 末尾开始的偏移量。

_(自 0.1.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | 要检查的数组。 |
| `value` | `*` | 要搜索的值。 |
| `[fromIndex=0]` | `number` | 开始搜索的索引。 |

### Returns

(`number`): 返回匹配值的索引，否则返回 `-1`。

### Example

```javascript
_.indexOf([1, 2, 1, 2], 2);
// => 1

// 从 fromIndex 开始搜索。
_.indexOf([1, 2, 1, 2], 2, 2);
// => 3
```

---

## initial

获取 `array` 中除最后一个元素外的所有元素。

_(自 0.1.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | 要查询的数组。 |

### Returns

(`Array`): 返回 `array` 的切片。

### Example

```javascript
_.initial([1, 2, 3]);
// => [1, 2]
```

---

## intersection

使用 [`SameValueZero`](http://ecma-international.org/ecma-262/7.0/#sec-samevaluezero) 进行相等性比较，创建一个包含所有给定数组交集的唯一值的数组。结果值的顺序和引用由第一个数组确定。

_(自 0.1.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `[...arrays]` | `Array` | 要检查的数组。 |

### Returns

(`Array`): 返回包含交集值的新数组。

### Example

```javascript
_.intersection([2, 1], [2, 3]);
// => [2]
```

---

## intersectionBy

此方法类似于 `_.intersection`，但它接受一个 `iteratee`，该 `iteratee` 会为每个 `arrays` 中的每个元素调用，以生成用于比较的标准。结果值的顺序和引用由第一个数组确定。该 iteratee 调用时会传入一个参数：(value)。

_(自 4.0.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `[...arrays]` | `Array` | 要检查的数组。 |
| `[iteratee=_.identity]` | `Function` | 每个元素调用的 iteratee。 |

### Returns

(`Array`): 返回包含交集值的新数组。

### Example

```javascript
_.intersectionBy([2.1, 1.2], [2.3, 3.4], Math.floor);
// => [2.1]

// `_.property` iteratee 速记。
_.intersectionBy([{ 'x': 1 }], [{ 'x': 2 }, { 'x': 1 }], 'x');
// => [{ 'x': 1 }]
```

---

## intersectionWith

此方法类似于 `_.intersection`，但它接受一个 `comparator`，该 `comparator` 用于比较 `arrays` 中的元素。结果值的顺序和引用由第一个数组确定。该 comparator 调用时会传入两个参数：(arrVal, othVal)。

_(自 4.0.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `[...arrays]` | `Array` | 要检查的数组。 |
| `[comparator]` | `Function` | 每个元素调用的 comparator。 |

### Returns

(`Array`): 返回包含交集值的新数组。

### Example

```javascript
var objects = [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }];
var others = [{ 'x': 1, 'y': 1 }, { 'x': 1, 'y': 2 }];

_.intersectionWith(objects, others, _.isEqual);
// => [{ 'x': 1, 'y': 2 }]
```

---

## join

将 `array` 中的所有元素转换为一个由 `separator` 分隔的字符串。

_(自 4.0.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | 要转换的数组。 |
| `[separator=',']` | `string` | 元素分隔符。 |

### Returns

(`string`): 返回连接后的字符串。

### Example

```javascript
_.join(['a', 'b', 'c'], '~');
// => 'a~b~c'
```

---

## last

获取 `array` 的最后一个元素。

_(自 0.1.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | 要查询的数组。 |

### Returns

(`*`): 返回 `array` 的最后一个元素。

### Example

```javascript
_.last([1, 2, 3]);
// => 3
```

---

## lastIndexOf

此方法类似于 `_.indexOf`，但它是从右到左遍历 `array` 的元素。

_(自 0.1.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | 要检查的数组。 |
| `value` | `*` | 要搜索的值。 |
| `[fromIndex=array.length-1]` | `number` | 开始搜索的索引。 |

### Returns

(`number`): 返回匹配值的索引，否则返回 `-1`。

### Example

```javascript
_.lastIndexOf([1, 2, 1, 2], 2);
// => 3

// 从 fromIndex 开始搜索。
_.lastIndexOf([1, 2, 1, 2], 2, 2);
// => 1
```

---

## nth

获取 `array` 中索引为 `n` 的元素。如果 `n` 是负数，则返回从末尾开始的第 n 个元素。

_(自 4.11.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | 要查询的数组。 |
| `[n=0]` | `number` | 要返回的元素的索引。 |

### Returns

(`*`): 返回 `array` 的第 n 个元素。

### Example

```javascript
var array = ['a', 'b', 'c', 'd'];

_.nth(array, 1);
// => 'b'

_.nth(array, -2);
// => 'c';
```

---

## pull

使用 [`SameValueZero`](http://ecma-international.org/ecma-262/7.0/#sec-samevaluezero) 进行相等性比较，从 `array` 中移除所有给定的值。

**注意：** 与 `_.without` 不同，此方法会改变 `array`。使用 `_.remove` 可根据 predicate 从数组中移除元素。

_(自 2.0.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | 要修改的数组。 |
| `[...values]` | `*` | 要移除的值。 |

### Returns

(`Array`): 返回 `array`。

### Example

```javascript
var array = ['a', 'b', 'c', 'a', 'b', 'c'];

_.pull(array, 'a', 'c');
console.log(array);
// => ['b', 'b']
```

---

## pullAll

此方法类似于 `_.pull`，但它接受一个要移除的值的数组。

**注意：** 与 `_.difference` 不同，此方法会改变 `array`。

_(自 4.0.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | 要修改的数组。 |
| `values` | `Array` | 要移除的值。 |

### Returns

(`Array`): 返回 `array`。

### Example

```javascript
var array = ['a', 'b', 'c', 'a', 'b', 'c'];

_.pullAll(array, ['a', 'c']);
console.log(array);
// => ['b', 'b']
```

---

## pullAllBy

此方法类似于 `_.pullAll`，但它接受一个 `iteratee`，该 `iteratee` 会为 `array` 和 `values` 的每个元素调用，以生成用于比较的标准。该 iteratee 调用时会传入一个参数：(value)。

**注意：** 与 `_.differenceBy` 不同，此方法会改变 `array`。

_(自 4.0.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | 要修改的数组。 |
| `values` | `Array` | 要移除的值。 |
| `[iteratee=_.identity]` | `Function` | 每个元素调用的 iteratee。 |

### Returns

(`Array`): 返回 `array`。

### Example

```javascript
var array = [{ 'x': 1 }, { 'x': 2 }, { 'x': 3 }, { 'x': 1 }];

_.pullAllBy(array, [{ 'x': 1 }, { 'x': 3 }], 'x');
console.log(array);
// => [{ 'x': 2 }]
```

---

## pullAllWith

此方法类似于 `_.pullAll`，但它接受一个 `comparator`，该 `comparator` 用于比较 `array` 和 `values` 的元素。该 comparator 调用时会传入两个参数：(arrVal, othVal)。

**注意：** 与 `_.differenceWith` 不同，此方法会改变 `array`。

_(自 4.6.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | 要修改的数组。 |
| `values` | `Array` | 要移除的值。 |
| `[comparator]` | `Function` | 每个元素调用的 comparator。 |

### Returns

(`Array`): 返回 `array`。

### Example

```javascript
var array = [{ 'x': 1, 'y': 2 }, { 'x': 3, 'y': 4 }, { 'x': 5, 'y': 6 }];

_.pullAllWith(array, [{ 'x': 3, 'y': 4 }], _.isEqual);
console.log(array);
// => [{ 'x': 1, 'y': 2 }, { 'x': 5, 'y': 6 }]
```

---

## pullAt

根据 `indexes` 从 `array` 中移除元素，并返回被移除元素的数组。

**注意：** 与 `_.at` 不同，此方法会改变 `array`。

_(自 3.0.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | 要修改的数组。 |
| `[...indexes]` | `(number|number[])` | 要移除的元素的索引。 |

### Returns

(`Array`): 返回被移除元素的新数组。

### Example

```javascript
var array = ['a', 'b', 'c', 'd'];
var pulled = _.pullAt(array, [1, 3]);

console.log(array);
// => ['a', 'c']

console.log(pulled);
// => ['b', 'd']
```

---

## remove

从 `array` 中移除所有使 `predicate` 返回真值的元素，并返回被移除元素的数组。该 predicate 调用时会传入三个参数：(value, index, array)。

**注意：** 与 `_.filter` 不同，此方法会改变 `array`。使用 `_.pull` 可按值从数组中移除元素。

_(自 2.0.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | 要修改的数组。 |
| `[predicate=_.identity]` | `Function` | 每次迭代调用的函数。 |

### Returns

(`Array`): 返回被移除元素的新数组。

### Example

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

---

## reverse

反转 `array`，使得第一个元素变为最后一个，第二个元素变为倒数第二个，以此类推。

**注意：** 此方法会改变 `array`，并且基于 [`Array#reverse`](https://mdn.io/Array/reverse)。

_(自 4.0.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | 要修改的数组。 |

### Returns

(`Array`): 返回 `array`。

### Example

```javascript
var array = [1, 2, 3];

_.reverse(array);
// => [3, 2, 1]

console.log(array);
// => [3, 2, 1]
```

---

## slice

创建一个 `array` 的切片，从 `start` 位置开始到 `end` 位置结束（不包括 `end` 位置）。

**注意：** 使用此方法代替 [`Array#slice`](https://mdn.io/Array/slice) 是为了确保返回的是密集数组。

_(自 3.0.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | 要切片的数组。 |
| `[start=0]` | `number` | 起始位置。 |
| `[end=array.length]` | `number` | 结束位置。 |

### Returns

(`Array`): 返回 `array` 的切片。

---

## sortedIndex

使用二分搜索来确定 `value` 应该插入到 `array` 中的最低索引位置，以维持其排序顺序。

_(自 0.1.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | 要检查的已排序数组。 |
| `value` | `*` | 要评估的值。 |

### Returns

(`number`): 返回 `value` 应该插入到 `array` 中的索引。

### Example

```javascript
_.sortedIndex([30, 50], 40);
// => 1
```

---

## sortedIndexBy

此方法类似于 `_.sortedIndex`，但它接受一个 `iteratee`，该 `iteratee` 会为 `value` 和 `array` 中的每个元素调用，以计算它们的排序排名。该 iteratee 调用时会传入一个参数：(value)。

_(自 4.0.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | 要检查的已排序数组。 |
| `value` | `*` | 要评估的值。 |
| `[iteratee=_.identity]` | `Function` | 每个元素调用的 iteratee。 |

### Returns

(`number`): 返回 `value` 应该插入到 `array` 中的索引。

### Example

```javascript
var objects = [{ 'x': 4 }, { 'x': 5 }];

_.sortedIndexBy(objects, { 'x': 4 }, function(o) { return o.x; });
// => 0
```

---

## sortedIndexOf

此方法类似于 `_.indexOf`，但它在已排序的 `array` 上执行二分搜索。

_(自 4.0.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | 要检查的数组。 |
| `value` | `*` | 要搜索的值。 |

### Returns

(`number`): 返回匹配值的索引，否则返回 `-1`。

### Example

```javascript
_.sortedIndexOf([4, 5, 5, 5, 6], 5);
// => 1
```

---

## sortedLastIndex

此方法类似于 `_.sortedIndex`，但它返回 `value` 应该插入到 `array` 中的最高索引位置，以维持其排序顺序。

_(自 3.0.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | 要检查的已排序数组。 |
| `value` | `*` | 要评估的值。 |

### Returns

(`number`): 返回 `value` 应该插入到 `array` 中的索引。

### Example

```javascript
_.sortedLastIndex([4, 5, 5, 5, 6], 5);
// => 4
```

---

## sortedLastIndexBy

此方法类似于 `_.sortedLastIndex`，但它接受一个 `iteratee`，该 `iteratee` 会为 `value` 和 `array` 中的每个元素调用，以计算它们的排序排名。该 iteratee 调用时会传入一个参数：(value)。

_(自 4.0.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | 要检查的已排序数组。 |
| `value` | `*` | 要评估的值。 |
| `[iteratee=_.identity]` | `Function` | 每个元素调用的 iteratee。 |

### Returns

(`number`): 返回 `value` 应该插入到 `array` 中的索引。

### Example

```javascript
var objects = [{ 'x': 4 }, { 'x': 5 }];

_.sortedLastIndexBy(objects, { 'x': 4 }, 'x');
// => 1
```

---

## sortedLastIndexOf

此方法类似于 `_.lastIndexOf`，但它在已排序的 `array` 上执行二分搜索。

_(自 4.0.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | 要检查的数组。 |
| `value` | `*` | 要搜索的值。 |

### Returns

(`number`): 返回匹配值的索引，否则返回 `-1`。

### Example

```javascript
_.sortedLastIndexOf([4, 5, 5, 5, 6], 5);
// => 3
```

---

## sortedUniq

此方法类似于 `_.uniq`，但它是为已排序数组设计和优化的。

_(自 4.0.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | 要检查的数组。 |

### Returns

(`Array`): 返回去重后的新数组。

### Example

```javascript
_.sortedUniq([1, 1, 2]);
// => [1, 2]
```

---

## sortedUniqBy

此方法类似于 `_.uniqBy`，但它是为已排序数组设计和优化的。

_(自 4.0.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | 要检查的数组。 |
| `[iteratee]` | `Function` | 每个元素调用的 iteratee。 |

### Returns

(`Array`): 返回去重后的新数组。

### Example

```javascript
_.sortedUniqBy([1.1, 1.2, 2.3, 2.4], Math.floor);
// => [1.1, 2.3]
```

---

## tail

获取 `array` 中除第一个元素外的所有元素。

_(自 4.0.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | 要查询的数组。 |

### Returns

(`Array`): 返回 `array` 的切片。

### Example

```javascript
_.tail([1, 2, 3]);
// => [2, 3]
```

---

## take

创建一个 `array` 的切片，从开头获取 `n` 个元素。

_(自 0.1.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | 要查询的数组。 |
| `[n=1]` | `number` | 要获取的元素数量。 |

### Returns

(`Array`): 返回 `array` 的切片。

### Example

```javascript
_.take([1, 2, 3]);
// => [1]

_.take([1, 2, 3], 2);
// => [1, 2]

_.take([1, 2, 3], 5);
// => [1, 2, 3]

_.take([1, 2, 3], 0);
// => []
```

---

## takeRight

创建一个 `array` 的切片，从末尾获取 `n` 个元素。

_(自 3.0.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | 要查询的数组。 |
| `[n=1]` | `number` | 要获取的元素数量。 |

### Returns

(`Array`): 返回 `array` 的切片。

### Example

```javascript
_.takeRight([1, 2, 3]);
// => [3]

_.takeRight([1, 2, 3], 2);
// => [2, 3]

_.takeRight([1, 2, 3], 5);
// => [1, 2, 3]

_.takeRight([1, 2, 3], 0);
// => []
```

---

## takeRightWhile

创建一个 `array` 的切片，从末尾开始获取元素，直到 `predicate` 返回假值为止。该 predicate 调用时会传入三个参数：(value, index, array)。

_(自 3.0.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | 要查询的数组。 |
| `[predicate=_.identity]` | `Function` | 每次迭代调用的函数。 |

### Returns

(`Array`): 返回 `array` 的切片。

### Example

```javascript
var users = [
  { 'user': 'barney',  'active': true },
  { 'user': 'fred',    'active': false },
  { 'user': 'pebbles', 'active': false }
];

_.takeRightWhile(users, function(o) { return !o.active; });
// => ['fred', 'pebbles'] 对应的 objects
```

---

## takeWhile

创建一个 `array` 的切片，从开头开始获取元素，直到 `predicate` 返回假值为止。该 predicate 调用时会传入三个参数：(value, index, array)。

_(自 3.0.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | 要查询的数组。 |
| `[predicate=_.identity]` | `Function` | 每次迭代调用的函数。 |

### Returns

(`Array`): 返回 `array` 的切片。

### Example

```javascript
var users = [
  { 'user': 'barney',  'active': false },
  { 'user': 'fred',    'active': false },
  { 'user': 'pebbles', 'active': true }
];

_.takeWhile(users, function(o) { return !o.active; });
// => ['barney', 'fred'] 对应的 objects
```

---

## union

使用 [`SameValueZero`](http://ecma-international.org/ecma-262/7.0/#sec-samevaluezero) 进行相等性比较，创建一个包含所有给定数组并集的唯一值数组，并保持其顺序。

_(自 0.1.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `[...arrays]` | `Array` | 要检查的数组。 |

### Returns

(`Array`): 返回组合值的新数组。

### Example

```javascript
_.union([2], [1, 2]);
// => [2, 1]
```

---

## unionBy

此方法类似于 `_.union`，但它接受一个 `iteratee`，该 `iteratee` 会为每个 `arrays` 中的每个元素调用，以生成用于计算唯一性的标准。结果值从首次出现的数组中选择。该 iteratee 调用时会传入一个参数：(value)。

_(自 4.0.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `[...arrays]` | `Array` | 要检查的数组。 |
| `[iteratee=_.identity]` | `Function` | 每个元素调用的 iteratee。 |

### Returns

(`Array`): 返回组合值的新数组。

### Example

```javascript
_.unionBy([2.1], [1.2, 2.3], Math.floor);
// => [2.1, 1.2]

// `_.property` iteratee 速记。
_.unionBy([{ 'x': 1 }], [{ 'x': 2 }, { 'x': 1 }], 'x');
// => [{ 'x': 1 }, { 'x': 2 }]
```

---

## unionWith

此方法类似于 `_.union`，但它接受一个 `comparator`，该 `comparator` 用于比较 `arrays` 中的元素。结果值从首次出现的数组中选择。该 comparator 调用时会传入两个参数：(arrVal, othVal)。

_(自 4.0.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `[...arrays]` | `Array` | 要检查的数组。 |
| `[comparator]` | `Function` | 每个元素调用的 comparator。 |

### Returns

(`Array`): 返回组合值的新数组。

### Example

```javascript
var objects = [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }];
var others = [{ 'x': 1, 'y': 1 }, { 'x': 1, 'y': 2 }];

_.unionWith(objects, others, _.isEqual);
// => [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }, { 'x': 1, 'y': 1 }]
```

---

## uniq

使用 [`SameValueZero`](http://ecma-international.org/ecma-262/7.0/#sec-samevaluezero) 进行相等性比较，创建一个去重后的数组版本，其中只保留每个元素的首次出现。结果值的顺序由它们在数组中出现的顺序决定。

_(自 0.1.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | 要检查的数组。 |

### Returns

(`Array`): 返回去重后的新数组。

### Example

```javascript
_.uniq([2, 1, 2]);
// => [2, 1]
```

---

## uniqBy

此方法类似于 `_.uniq`，但它接受一个 `iteratee`，该 `iteratee` 会为 `array` 中的每个元素调用，以生成用于计算唯一性的标准。结果值的顺序由它们在数组中出现的顺序决定。该 iteratee 调用时会传入一个参数：(value)。

_(自 4.0.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | 要检查的数组。 |
| `[iteratee=_.identity]` | `Function` | 每个元素调用的 iteratee。 |

### Returns

(`Array`): 返回去重后的新数组。

### Example

```javascript
_.uniqBy([2.1, 1.2, 2.3], Math.floor);
// => [2.1, 1.2]

// `_.property` iteratee 速记。
_.uniqBy([{ 'x': 1 }, { 'x': 2 }, { 'x': 1 }], 'x');
// => [{ 'x': 1 }, { 'x': 2 }]
```

---

## uniqWith

此方法类似于 `_.uniq`，但它接受一个 `comparator`，该 `comparator` 用于比较 `array` 中的元素。结果值的顺序由它们在数组中出现的顺序决定。该 comparator 调用时会传入两个参数：(arrVal, othVal)。

_(自 4.0.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | 要检查的数组。 |
| `[comparator]` | `Function` | 每个元素调用的 comparator。 |

### Returns

(`Array`): 返回去重后的新数组。

### Example

```javascript
var objects = [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }, { 'x': 1, 'y': 2 }];

_.uniqWith(objects, _.isEqual);
// => [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }]
```

---

## unzip

此方法类似于 `_.zip`，但它接受一个分组元素的数组，并创建一个将元素重新组合到其压缩前配置的数组。

_(自 1.2.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | 要处理的分组元素数组。 |

### Returns

(`Array`): 返回重新组合元素的新数组。

### Example

```javascript
var zipped = _.zip(['a', 'b'], [1, 2], [true, false]);
// => [['a', 1, true], ['b', 2, false]]

_.unzip(zipped);
// => [['a', 'b'], [1, 2], [true, false]]
```

---

## unzipWith

此方法类似于 `_.unzip`，但它接受一个 `iteratee` 来指定如何组合重新分组的值。该 iteratee 调用时会传入每个组的元素：(...group)。

_(自 3.8.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | 要处理的分组元素数组。 |
| `[iteratee=_.identity]` | `Function` | 用于组合重新分组值的函数。 |

### Returns

(`Array`): 返回重新组合元素的新数组。

### Example

```javascript
var zipped = _.zip([1, 2], [10, 20], [100, 200]);
// => [[1, 10, 100], [2, 20, 200]]

_.unzipWith(zipped, _.add);
// => [111, 222]
```

---

## without

使用 [`SameValueZero`](http://ecma-international.org/ecma-262/7.0/#sec-samevaluezero) 进行相等性比较，创建一个排除所有给定值的新数组。

**注意：** 与 `_.pull` 不同，此方法返回一个新数组。

_(自 0.1.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | 要检查的数组。 |
| `[...values]` | `*` | 要排除的值。 |

### Returns

(`Array`): 返回过滤后的新数组。

### Example

```javascript
_.without([2, 1, 2, 3], 1, 2);
// => [3]
```

---

## xor

创建一个唯一值的数组，该数组是给定数组的[对称差](https://en.wikipedia.org/wiki/Symmetric_difference)。结果值的顺序由它们在数组中出现的顺序决定。

_(自 2.4.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `[...arrays]` | `Array` | 要检查的数组。 |

### Returns

(`Array`): 返回过滤后的新数组。

### Example

```javascript
_.xor([2, 1], [2, 3]);
// => [1, 3]
```

---

## xorBy

此方法类似于 `_.xor`，但它接受一个 `iteratee`，该 `iteratee` 会为每个 `arrays` 中的每个元素调用，以生成用于比较的标准。结果值的顺序由它们在数组中出现的顺序决定。该 iteratee 调用时会传入一个参数：(value)。

_(自 4.0.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `[...arrays]` | `Array` | 要检查的数组。 |
| `[iteratee=_.identity]` | `Function` | 每个元素调用的 iteratee。 |

### Returns

(`Array`): 返回过滤后的新数组。

### Example

```javascript
_.xorBy([2.1, 1.2], [2.3, 3.4], Math.floor);
// => [1.2, 3.4]

// `_.property` iteratee 速记。
_.xorBy([{ 'x': 1 }], [{ 'x': 2 }, { 'x': 1 }], 'x');
// => [{ 'x': 2 }]
```

---

## xorWith

此方法类似于 `_.xor`，但它接受一个 `comparator`，该 `comparator` 用于比较 `arrays` 中的元素。结果值的顺序由它们在数组中出现的顺序决定。该 comparator 调用时会传入两个参数：(arrVal, othVal)。

_(自 4.0.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `[...arrays]` | `Array` | 要检查的数组。 |
| `[comparator]` | `Function` | 每个元素调用的 comparator。 |

### Returns

(`Array`): 返回过滤后的新数组。

### Example

```javascript
var objects = [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }];
var others = [{ 'x': 1, 'y': 1 }, { 'x': 1, 'y': 2 }];

_.xorWith(objects, others, _.isEqual);
// => [{ 'x': 2, 'y': 1 }, { 'x': 1, 'y': 1 }]
```

---

## zip

创建一个分组元素的数组，其中第一个元素包含给定数组的第一个元素，第二个元素包含给定数组的第二个元素，以此类推。

_(自 0.1.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `[...arrays]` | `Array` | 要处理的数组。 |

### Returns

(`Array`): 返回分组元素的新数组。

### Example

```javascript
_.zip(['a', 'b'], [1, 2], [true, false]);
// => [['a', 1, true], ['b', 2, false]]
```

---

## zipObject

此方法类似于 `_.fromPairs`，但它接受两个数组，一个为属性标识符，另一个为对应的值。

_(自 0.4.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `[props=[]]` | `Array` | 属性标识符。 |
| `[values=[]]` | `Array` | 属性值。 |

### Returns

(`Object`): 返回新 object。

### Example

```javascript
_.zipObject(['a', 'b'], [1, 2]);
// => { 'a': 1, 'b': 2 }
```

---

## zipObjectDeep

此方法类似于 `_.zipObject`，但它支持属性路径。

_(自 4.1.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `[props=[]]` | `Array` | 属性标识符。 |
| `[values=[]]` | `Array` | 属性值。 |

### Returns

(`Object`): 返回新 object。

### Example

```javascript
_.zipObjectDeep(['a.b[0].c', 'a.b[1].d'], [1, 2]);
// => { 'a': { 'b': [{ 'c': 1 }, { 'd': 2 }] } }
```

---

## zipWith

此方法类似于 `_.zip`，但它接受一个 `iteratee` 来指定如何组合分组的值。该 iteratee 调用时会传入每个组的元素：(...group)。

_(自 3.8.0 起)_

### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `[...arrays]` | `Array` | 要处理的数组。 |
| `[iteratee=_.identity]` | `Function` | 用于组合分组值的函数。 |

### Returns

(`Array`): 返回分组元素的新数组。

### Example

```javascript
_.zipWith([1, 2], [10, 20], [100, 200], function(a, b, c) {
  return a + b + c;
});
// => [111, 222]
```