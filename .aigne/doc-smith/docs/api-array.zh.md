# 数组

Lodash 的数组方法提供了一套用于在 JavaScript 中操作和查询数组的综合工具集。这些函数为拆分数组、移除元素、查找值和执行复杂转换等常见任务提供了稳健、跨浏览器的解决方案。利用这些工具，您可以编写出更简洁、更具声明性且更高效的代码。

---

### chunk

创建一个将元素按 `size` 长度分组的数组。如果 `array` 不能被平均分割，最后的块将是剩余的元素。

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要处理的数组。"></x-field>
<x-field data-name="size" data-type="number" data-default="1" data-required="false" data-desc="每个块的长度。"></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="返回新的块数组。"></x-field>

**Example**

```javascript
_.chunk(['a', 'b', 'c', 'd'], 2);
// => [['a', 'b'], ['c', 'd']]

_.chunk(['a', 'b', 'c', 'd'], 3);
// => [['a', 'b', 'c'], ['d']]
```

### compact

创建一个移除了所有假值（falsey values）的数组。`false`、`null`、`0`、`""`、`undefined` 和 `NaN` 都被视作假值。

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要压缩的数组。"></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="返回过滤值后的新数组。"></x-field>

**Example**

```javascript
_.compact([0, 1, false, 2, '', 3]);
// => [1, 2, 3]
```

### concat

创建一个新数组，将 `array` 与任何附加的数组和/或值连接起来。

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要连接的数组。"></x-field>
<x-field data-name="[values]" data-type="...*" data-required="false" data-desc="要连接的值。"></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="返回连接后的新数组。"></x-field>

**Example**

```javascript
var array = [1];
var other = _.concat(array, 2, [3], [[4]]);

console.log(other);
// => [1, 2, 3, [4]]

console.log(array);
// => [1]
```

### difference

创建一个由 `array` 中不包含在其他给定数组中的值组成的数组。使用 [`SameValueZero`](http://ecma-international.org/ecma-262/7.0/#sec-samevaluezero) 进行相等性比较。结果值的顺序和引用由第一个数组决定。

**Note:** 与 `_.pullAll` 不同，此方法返回一个新数组。

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要检查的数组。"></x-field>
<x-field data-name="[values]" data-type="...Array" data-required="false" data-desc="要排除的值。"></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="返回过滤值后的新数组。"></x-field>

**Example**

```javascript
_.difference([2, 1], [2, 3]);
// => [1]
```

### differenceBy

此方法类似于 `_.difference`，但它接受一个 `iteratee`（迭代器），该迭代器会为 `array` 和 `values` 的每个元素调用，以生成用于比较的标准。结果值的顺序和引用由第一个数组决定。调用迭代器时会传入一个参数：(value)。

**Note:** 与 `_.pullAllBy` 不同，此方法返回一个新数组。

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要检查的数组。"></x-field>
<x-field data-name="[values]" data-type="...Array" data-required="false" data-desc="要排除的值。"></x-field>
<x-field data-name="[iteratee=_.identity]" data-type="Function" data-required="false" data-desc="为每个元素调用的迭代器。"></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="返回过滤值后的新数组。"></x-field>

**Example**

```javascript
_.differenceBy([2.1, 1.2], [2.3, 3.4], Math.floor);
// => [1.2]

// The `_.property` iteratee shorthand.
_.differenceBy([{ 'x': 2 }, { 'x': 1 }], [{ 'x': 1 }], 'x');
// => [{ 'x': 2 }]
```

### differenceWith

此方法类似于 `_.difference`，但它接受一个 `comparator`（比较器），该比较器用于比较 `array` 和 `values` 的元素。结果值的顺序和引用由第一个数组决定。调用比较器时会传入两个参数：(arrVal, othVal)。

**Note:** 与 `_.pullAllWith` 不同，此方法返回一个新数组。

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要检查的数组。"></x-field>
<x-field data-name="[values]" data-type="...Array" data-required="false" data-desc="要排除的值。"></x-field>
<x-field data-name="[comparator]" data-type="Function" data-required="false" data-desc="为每个元素调用的比较器。"></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="返回过滤值后的新数组。"></x-field>

**Example**

```javascript
var objects = [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }];

_.differenceWith(objects, [{ 'x': 1, 'y': 2 }], _.isEqual);
// => [{ 'x': 2, 'y': 1 }]
```

### drop

创建一个从 `array` 开头移除 `n` 个元素后的切片。

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要查询的数组。"></x-field>
<x-field data-name="[n=1]" data-type="number" data-required="false" data-desc="要移除的元素数量。"></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="返回 `array` 的切片。"></x-field>

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

### dropRight

创建一个从 `array` 尾部移除 `n` 个元素后的切片。

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要查询的数组。"></x-field>
<x-field data-name="[n=1]" data-type="number" data-required="false" data-desc="要移除的元素数量。"></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="返回 `array` 的切片。"></x-field>

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

### dropRightWhile

创建一个从 `array` 尾部移除元素的切片。元素会一直被移除，直到 `predicate` 返回假值。调用断言函数时会传入三个参数：(value, index, array)。

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要查询的数组。"></x-field>
<x-field data-name="[predicate=_.identity]" data-type="Function" data-required="false" data-desc="每次迭代调用的函数。"></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="返回 `array` 的切片。"></x-field>

**Example**

```javascript
var users = [
  { 'user': 'barney',  'active': true },
  { 'user': 'fred',    'active': false },
  { 'user': 'pebbles', 'active': false }
];

_.dropRightWhile(users, function(o) { return !o.active; });
// => objects for ['barney']
```

### dropWhile

创建一个从 `array` 开头移除元素的切片。元素会一直被移除，直到 `predicate` 返回假值。调用断言函数时会传入三个参数：(value, index, array)。

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要查询的数组。"></x-field>
<x-field data-name="[predicate=_.identity]" data-type="Function" data-required="false" data-desc="每次迭代调用的函数。"></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="返回 `array` 的切片。"></x-field>

**Example**

```javascript
var users = [
  { 'user': 'barney',  'active': false },
  { 'user': 'fred',    'active': false },
  { 'user': 'pebbles', 'active': true }
];

_.dropWhile(users, function(o) { return !o.active; });
// => objects for ['pebbles']
```

### fill

使用 `value` 填充 `array` 中的元素，从 `start` 位置开始，到 `end` 位置结束（不包括 `end`）。

**Note:** 此方法会修改 `array`。

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要填充的数组。"></x-field>
<x-field data-name="value" data-type="*" data-required="true" data-desc="用于填充 `array` 的值。"></x-field>
<x-field data-name="[start=0]" data-type="number" data-required="false" data-desc="起始位置。"></x-field>
<x-field data-name="[end=array.length]" data-type="number" data-required="false" data-desc="结束位置。"></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="返回 `array`。"></x-field>

**Example**

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

### findIndex

此方法类似于 `_.find`，但它返回第一个使 `predicate` 返回真值的元素的索引，而不是元素本身。

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要检查的数组。"></x-field>
<x-field data-name="[predicate=_.identity]" data-type="Function" data-required="false" data-desc="每次迭代调用的函数。"></x-field>
<x-field data-name="[fromIndex=0]" data-type="number" data-required="false" data-desc="开始搜索的索引。"></x-field>

**Returns**

<x-field data-name="" data-type="number" data-desc="返回找到元素的索引，否则返回 `-1`。"></x-field>

**Example**

```javascript
var users = [
  { 'user': 'barney',  'active': false },
  { 'user': 'fred',    'active': false },
  { 'user': 'pebbles', 'active': true }
];

_.findIndex(users, function(o) { return o.user == 'barney'; });
// => 0
```

### findLastIndex

此方法类似于 `_.findIndex`，但它是从右到左遍历 `collection` 的元素。

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要检查的数组。"></x-field>
<x-field data-name="[predicate=_.identity]" data-type="Function" data-required="false" data-desc="每次迭代调用的函数。"></x-field>
<x-field data-name="[fromIndex=array.length-1]" data-type="number" data-required="false" data-desc="开始搜索的索引。"></x-field>

**Returns**

<x-field data-name="" data-type="number" data-desc="返回找到元素的索引，否则返回 `-1`。"></x-field>

**Example**

```javascript
var users = [
  { 'user': 'barney',  'active': true },
  { 'user': 'fred',    'active': false },
  { 'user': 'pebbles', 'active': false }
];

_.findLastIndex(users, function(o) { return o.user == 'pebbles'; });
// => 2
```

### flatten

将 `array` 展平一层。

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要展平的数组。"></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="返回展平后的新数组。"></x-field>

**Example**

```javascript
_.flatten([1, [2, [3, [4]], 5]]);
// => [1, 2, [3, [4]], 5]
```

### flattenDeep

递归地展平 `array`。

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要展平的数组。"></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="返回展平后的新数组。"></x-field>

**Example**

```javascript
_.flattenDeep([1, [2, [3, [4]], 5]]);
// => [1, 2, 3, 4, 5]
```

### flattenDepth

递归地展平 `array` 最多 `depth` 次。

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要展平的数组。"></x-field>
<x-field data-name="[depth=1]" data-type="number" data-required="false" data-desc="最大递归深度。"></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="返回展平后的新数组。"></x-field>

**Example**

```javascript
var array = [1, [2, [3, [4]], 5]];

_.flattenDepth(array, 1);
// => [1, 2, [3, [4]], 5]

_.flattenDepth(array, 2);
// => [1, 2, 3, [4], 5]
```

### fromPairs

`_.toPairs` 的反向操作；此方法返回一个由键值对 `pairs` 组成的对象。

**Parameters**

<x-field data-name="pairs" data-type="Array" data-required="true" data-desc="键值对。"></x-field>

**Returns**

<x-field data-name="" data-type="Object" data-desc="返回新对象。"></x-field>

**Example**

```javascript
_.fromPairs([['a', 1], ['b', 2]]);
// => { 'a': 1, 'b': 2 }
```

### head

获取 `array` 的第一个元素。

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要查询的数组。"></x-field>

**Returns**

<x-field data-name="" data-type="*" data-desc="返回 `array` 的第一个元素。"></x-field>

**Example**

```javascript
_.head([1, 2, 3]);
// => 1

_.head([]);
// => undefined
```

### indexOf

获取 `value` 在 `array` 中首次出现的索引，使用 [`SameValueZero`](http://ecma-international.org/ecma-262/7.0/#sec-samevaluezero) 进行相等性比较。如果 `fromIndex` 是负数，则将其用作从 `array` 末尾开始的偏移量。

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要检查的数组。"></x-field>
<x-field data-name="value" data-type="*" data-required="true" data-desc="要搜索的值。"></x-field>
<x-field data-name="[fromIndex=0]" data-type="number" data-required="false" data-desc="开始搜索的索引。"></x-field>

**Returns**

<x-field data-name="" data-type="number" data-desc="返回匹配值的索引，否则返回 `-1`。"></x-field>

**Example**

```javascript
_.indexOf([1, 2, 1, 2], 2);
// => 1

// Search from the `fromIndex`.
_.indexOf([1, 2, 1, 2], 2, 2);
// => 3
```

### initial

获取 `array` 中除最后一个元素外的所有元素。

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要查询的数组。"></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="返回 `array` 的切片。"></x-field>

**Example**

```javascript
_.initial([1, 2, 3]);
// => [1, 2]
```

### intersection

创建一个包含所有给定数组中共有值的唯一值数组。使用 [`SameValueZero`](http://ecma-international.org/ecma-262/7.0/#sec-samevaluezero) 进行相等性比较。结果值的顺序和引用由第一个数组决定。

**Parameters**

<x-field data-name="[arrays]" data-type="...Array" data-required="true" data-desc="要检查的数组。"></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="返回相交值的新数组。"></x-field>

**Example**

```javascript
_.intersection([2, 1], [2, 3]);
// => [2]
```

### join

将 `array` 中的所有元素转换为一个由 `separator` 分隔的字符串。

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要转换的数组。"></x-field>
<x-field data-name="[separator=',']" data-type="string" data-required="false" data-desc="元素分隔符。"></x-field>

**Returns**

<x-field data-name="" data-type="string" data-desc="返回连接后的字符串。"></x-field>

**Example**

```javascript
_.join(['a', 'b', 'c'], '~');
// => 'a~b~c'
```

### last

获取 `array` 的最后一个元素。

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要查询的数组。"></x-field>

**Returns**

<x-field data-name="" data-type="*" data-desc="返回 `array` 的最后一个元素。"></x-field>

**Example**

```javascript
_.last([1, 2, 3]);
// => 3
```

### lastIndexOf

此方法类似于 `_.indexOf`，但它是从右到左遍历 `array` 的元素。

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要检查的数组。"></x-field>
<x-field data-name="value" data-type="*" data-required="true" data-desc="要搜索的值。"></x-field>
<x-field data-name="[fromIndex=array.length-1]" data-type="number" data-required="false" data-desc="开始搜索的索引。"></x-field>

**Returns**

<x-field data-name="" data-type="number" data-desc="返回匹配值的索引，否则返回 `-1`。"></x-field>

**Example**

```javascript
_.lastIndexOf([1, 2, 1, 2], 2);
// => 3

// Search from the `fromIndex`.
_.lastIndexOf([1, 2, 1, 2], 2, 2);
// => 1
```

### nth

获取 `array` 中索引为 `n` 的元素。如果 `n` 是负数，则返回从末尾算起的第 n 个元素。

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要查询的数组。"></x-field>
<x-field data-name="[n=0]" data-type="number" data-required="false" data-desc="要返回的元素的索引。"></x-field>

**Returns**

<x-field data-name="" data-type="*" data-desc="返回 `array` 的第 n 个元素。"></x-field>

**Example**

```javascript
var array = ['a', 'b', 'c', 'd'];

_.nth(array, 1);
// => 'b'

_.nth(array, -2);
// => 'c';
```

### pull

从 `array` 中移除所有给定的值。使用 [`SameValueZero`](http://ecma-international.org/ecma-262/7.0/#sec-samevaluezero) 进行相等性比较。

**Note:** 此方法会修改 `array`。

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要修改的数组。"></x-field>
<x-field data-name="[values]" data-type="...*" data-required="false" data-desc="要移除的值。"></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="返回 `array`。"></x-field>

**Example**

```javascript
var array = ['a', 'b', 'c', 'a', 'b', 'c'];

_.pull(array, 'a', 'c');
console.log(array);
// => ['b', 'b']
```

### pullAll

此方法类似于 `_.pull`，但它接受一个要移除的值的数组。

**Note:** 此方法会修改 `array`。

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要修改的数组。"></x-field>
<x-field data-name="values" data-type="Array" data-required="true" data-desc="要移除的值。"></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="返回 `array`。"></x-field>

**Example**

```javascript
var array = ['a', 'b', 'c', 'a', 'b', 'c'];

_.pullAll(array, ['a', 'c']);
console.log(array);
// => ['b', 'b']
```

### pullAllBy

此方法类似于 `_.pullAll`，但它接受一个 `iteratee`（迭代器），该迭代器会为 `array` 和 `values` 的每个元素调用，以生成用于比较的标准。调用迭代器时会传入一个参数：(value)。

**Note:** 此方法会修改 `array`。

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要修改的数组。"></x-field>
<x-field data-name="values" data-type="Array" data-required="true" data-desc="要移除的值。"></x-field>
<x-field data-name="[iteratee=_.identity]" data-type="Function" data-required="false" data-desc="为每个元素调用的迭代器。"></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="返回 `array`。"></x-field>

**Example**

```javascript
var array = [{ 'x': 1 }, { 'x': 2 }, { 'x': 3 }, { 'x': 1 }];

_.pullAllBy(array, [{ 'x': 1 }, { 'x': 3 }], 'x');
console.log(array);
// => [{ 'x': 2 }]
```

### pullAllWith

此方法类似于 `_.pullAll`，但它接受一个 `comparator`（比较器），该比较器用于比较 `array` 和 `values` 的元素。调用比较器时会传入两个参数：(arrVal, othVal)。

**Note:** 此方法会修改 `array`。

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要修改的数组。"></x-field>
<x-field data-name="values" data-type="Array" data-required="true" data-desc="要移除的值。"></x-field>
<x-field data-name="[comparator]" data-type="Function" data-required="false" data-desc="为每个元素调用的比较器。"></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="返回 `array`。"></x-field>

**Example**

```javascript
var array = [{ 'x': 1, 'y': 2 }, { 'x': 3, 'y': 4 }, { 'x': 5, 'y': 6 }];

_.pullAllWith(array, [{ 'x': 3, 'y': 4 }], _.isEqual);
console.log(array);
// => [{ 'x': 1, 'y': 2 }, { 'x': 5, 'y': 6 }]
```

### pullAt

移除 `array` 中与 `indexes` 对应的元素，并返回一个包含被移除元素的数组。

**Note:** 此方法会修改 `array`。

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要修改的数组。"></x-field>
<x-field data-name="[indexes]" data-type="...(number|number[])" data-required="false" data-desc="要移除的元素的索引。"></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="返回包含被移除元素的新数组。"></x-field>

**Example**

```javascript
var array = ['a', 'b', 'c', 'd'];
var pulled = _.pullAt(array, [1, 3]);

console.log(array);
// => ['a', 'c']

console.log(pulled);
// => ['b', 'd']
```

### remove

从 `array` 中移除所有使 `predicate` 返回真值的元素，并返回一个包含被移除元素的数组。调用断言函数时会传入三个参数：(value, index, array)。

**Note:** 此方法会修改 `array`。

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要修改的数组。"></x-field>
<x-field data-name="[predicate=_.identity]" data-type="Function" data-required="false" data-desc="每次迭代调用的函数。"></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="返回包含被移除元素的新数组。"></x-field>

**Example**

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

### reverse

反转 `array`，使得第一个元素变为最后一个，第二个元素变为倒数第二个，以此类推。

**Note:** 此方法会修改 `array`，它基于 [`Array#reverse`](https://mdn.io/Array/reverse)。

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要修改的数组。"></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="返回 `array`。"></x-field>

**Example**

```javascript
var array = [1, 2, 3];

_.reverse(array);
// => [3, 2, 1]

console.log(array);
// => [3, 2, 1]
```

### slice

创建一个 `array` 的切片，从 `start` 开始，到 `end` 结束（不包括 `end`）。

**Note:** 使用此方法代替 `Array#slice` 可确保返回密集数组。

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要切片的数组。"></x-field>
<x-field data-name="[start=0]" data-type="number" data-required="false" data-desc="起始位置。"></x-field>
<x-field data-name="[end=array.length]" data-type="number" data-required="false" data-desc="结束位置。"></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="返回 `array` 的切片。"></x-field>

### sortedIndex

使用二分搜索来确定 `value` 应该插入到 `array` 中的最低索引位置，以保持其排序顺序。

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要检查的已排序数组。"></x-field>
<x-field data-name="value" data-type="*" data-required="true" data-desc="要评估的值。"></x-field>

**Returns**

<x-field data-name="" data-type="number" data-desc="返回 `value` 应该插入到 `array` 中的索引。"></x-field>

**Example**

```javascript
_.sortedIndex([30, 50], 40);
// => 1
```

### sortedIndexBy

此方法类似于 `_.sortedIndex`，但它接受一个 `iteratee`（迭代器），该迭代器会为 `value` 和 `array` 的每个元素调用，以计算它们的排序排名。调用迭代器时会传入一个参数：(value)。

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要检查的已排序数组。"></x-field>
<x-field data-name="value" data-type="*" data-required="true" data-desc="要评估的值。"></x-field>
<x-field data-name="[iteratee=_.identity]" data-type="Function" data-required="false" data-desc="为每个元素调用的迭代器。"></x-field>

**Returns**

<x-field data-name="" data-type="number" data-desc="返回 `value` 应该插入到 `array` 中的索引。"></x-field>

**Example**

```javascript
var objects = [{ 'x': 4 }, { 'x': 5 }];

_.sortedIndexBy(objects, { 'x': 4 }, function(o) { return o.x; });
// => 0
```

### sortedIndexOf

此方法类似于 `_.indexOf`，但它在已排序的 `array` 上执行二分搜索。

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要检查的数组。"></x-field>
<x-field data-name="value" data-type="*" data-required="true" data-desc="要搜索的值。"></x-field>

**Returns**

<x-field data-name="" data-type="number" data-desc="返回匹配值的索引，否则返回 `-1`。"></x-field>

**Example**

```javascript
_.sortedIndexOf([4, 5, 5, 5, 6], 5);
// => 1
```

### sortedLastIndex

此方法类似于 `_.sortedIndex`，但它返回 `value` 应该插入到 `array` 中以保持其排序顺序的最高索引。

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要检查的已排序数组。"></x-field>
<x-field data-name="value" data-type="*" data-required="true" data-desc="要评估的值。"></x-field>

**Returns**

<x-field data-name="" data-type="number" data-desc="返回 `value` 应该插入到 `array` 中的索引。"></x-field>

**Example**

```javascript
_.sortedLastIndex([4, 5, 5, 5, 6], 5);
// => 4
```

### sortedLastIndexBy

此方法类似于 `_.sortedLastIndex`，但它接受一个 `iteratee`（迭代器），该迭代器会为 `value` 和 `array` 的每个元素调用，以计算它们的排序排名。调用迭代器时会传入一个参数：(value)。

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要检查的已排序数组。"></x-field>
<x-field data-name="value" data-type="*" data-required="true" data-desc="要评估的值。"></x-field>
<x-field data-name="[iteratee=_.identity]" data-type="Function" data-required="false" data-desc="为每个元素调用的迭代器。"></x-field>

**Returns**

<x-field data-name="" data-type="number" data-desc="返回 `value` 应该插入到 `array` 中的索引。"></x-field>

**Example**

```javascript
var objects = [{ 'x': 4 }, { 'x': 5 }];

_.sortedLastIndexBy(objects, { 'x': 4 }, function(o) { return o.x; });
// => 1
```

### sortedLastIndexOf

此方法类似于 `_.lastIndexOf`，但它在已排序的 `array` 上执行二分搜索。

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要检查的数组。"></x-field>
<x-field data-name="value" data-type="*" data-required="true" data-desc="要搜索的值。"></x-field>

**Returns**

<x-field data-name="" data-type="number" data-desc="返回匹配值的索引，否则返回 `-1`。"></x-field>

**Example**

```javascript
_.sortedLastIndexOf([4, 5, 5, 5, 6], 5);
// => 3
```

### sortedUniq

此方法类似于 `_.uniq`，但它是为已排序数组设计和优化的。

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要检查的数组。"></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="返回去重后的新数组。"></x-field>

**Example**

```javascript
_.sortedUniq([1, 1, 2]);
// => [1, 2]
```

### sortedUniqBy

此方法类似于 `_.uniqBy`，但它是为已排序数组设计和优化的。

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要检查的数组。"></x-field>
<x-field data-name="[iteratee]" data-type="Function" data-required="false" data-desc="为每个元素调用的迭代器。"></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="返回去重后的新数组。"></x-field>

**Example**

```javascript
_.sortedUniqBy([1.1, 1.2, 2.3, 2.4], Math.floor);
// => [1.1, 2.3]
```

### tail

获取 `array` 中除第一个元素外的所有元素。

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要查询的数组。"></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="返回 `array` 的切片。"></x-field>

**Example**

```javascript
_.tail([1, 2, 3]);
// => [2, 3]
```

### take

创建一个包含从 `array` 开头取出的 `n` 个元素的切片。

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要查询的数组。"></x-field>
<x-field data-name="[n=1]" data-type="number" data-required="false" data-desc="要取出的元素数量。"></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="返回 `array` 的切片。"></x-field>

**Example**

```javascript
_.take([1, 2, 3]);
// => [1]

_.take([1, 2, 3], 2);
// => [1, 2]
```

### takeRight

创建一个包含从 `array` 尾部取出的 `n` 个元素的切片。

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要查询的数组。"></x-field>
<x-field data-name="[n=1]" data-type="number" data-required="false" data-desc="要取出的元素数量。"></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="返回 `array` 的切片。"></x-field>

**Example**

```javascript
_.takeRight([1, 2, 3]);
// => [3]

_.takeRight([1, 2, 3], 2);
// => [2, 3]
```

### takeRightWhile

创建一个包含从 `array` 尾部取出的元素的切片。元素会一直被取出，直到 `predicate` 返回假值。

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要查询的数组。"></x-field>
<x-field data-name="[predicate=_.identity]" data-type="Function" data-required="false" data-desc="每次迭代调用的函数。"></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="返回 `array` 的切片。"></x-field>

**Example**

```javascript
var users = [
  { 'user': 'barney',  'active': true },
  { 'user': 'fred',    'active': false },
  { 'user': 'pebbles', 'active': false }
];

_.takeRightWhile(users, function(o) { return !o.active; });
// => objects for ['fred', 'pebbles']
```

### takeWhile

创建一个包含从 `array` 开头取出的元素的切片。元素会一直被取出，直到 `predicate` 返回假值。

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要查询的数组。"></x-field>
<x-field data-name="[predicate=_.identity]" data-type="Function" data-required="false" data-desc="每次迭代调用的函数。"></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="返回 `array` 的切片。"></x-field>

**Example**

```javascript
var users = [
  { 'user': 'barney',  'active': false },
  { 'user': 'fred',    'active': false },
  { 'user': 'pebbles', 'active': true }
];

_.takeWhile(users, function(o) { return !o.active; });
// => objects for ['barney', 'fred']
```

### union

创建一个由所有给定数组中的唯一值组成的数组，并保持其顺序。使用 [`SameValueZero`](http://ecma-international.org/ecma-262/7.0/#sec-samevaluezero) 进行相等性比较。

**Parameters**

<x-field data-name="[arrays]" data-type="...Array" data-required="true" data-desc="要检查的数组。"></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="返回组合值的新数组。"></x-field>

**Example**

```javascript
_.union([2], [1, 2]);
// => [2, 1]
```

### unionBy

此方法类似于 `_.union`，但它接受一个 `iteratee`（迭代器），该迭代器会为每个 `arrays` 的每个元素调用，以生成用于计算唯一性的标准。

**Parameters**

<x-field data-name="[arrays]" data-type="...Array" data-required="true" data-desc="要检查的数组。"></x-field>
<x-field data-name="[iteratee=_.identity]" data-type="Function" data-required="false" data-desc="为每个元素调用的迭代器。"></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="返回组合值的新数组。"></x-field>

**Example**

```javascript
_.unionBy([2.1], [1.2, 2.3], Math.floor);
// => [2.1, 1.2]
```

### unionWith

此方法类似于 `_.union`，但它接受一个 `comparator`（比较器），该比较器用于比较 `arrays` 的元素。

**Parameters**

<x-field data-name="[arrays]" data-type="...Array" data-required="true" data-desc="要检查的数组。"></x-field>
<x-field data-name="[comparator]" data-type="Function" data-required="false" data-desc="为每个元素调用的比较器。"></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="返回组合值的新数组。"></x-field>

**Example**

```javascript
var objects = [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }];
var others = [{ 'x': 1, 'y': 1 }, { 'x': 1, 'y': 2 }];

_.unionWith(objects, others, _.isEqual);
// => [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }, { 'x': 1, 'y': 1 }]
```

### uniq

创建一个去重后的数组版本，使用 [`SameValueZero`](http://ecma-international.org/ecma-262/7.0/#sec-samevaluezero) 进行相等性比较，其中只保留每个元素的首次出现。

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要检查的数组。"></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="返回去重后的新数组。"></x-field>

**Example**

```javascript
_.uniq([2, 1, 2]);
// => [2, 1]
```

### uniqBy

此方法类似于 `_.uniq`，但它接受一个 `iteratee`（迭代器），该迭代器会为 `array` 中的每个元素调用，以生成用于计算唯一性的标准。

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要检查的数组。"></x-field>
<x-field data-name="[iteratee=_.identity]" data-type="Function" data-required="false" data-desc="为每个元素调用的迭代器。"></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="返回去重后的新数组。"></x-field>

**Example**

```javascript
_.uniqBy([2.1, 1.2, 2.3], Math.floor);
// => [2.1, 1.2]
```

### uniqWith

此方法类似于 `_.uniq`，但它接受一个 `comparator`（比较器），该比较器用于比较 `array` 的元素。

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要检查的数组。"></x-field>
<x-field data-name="[comparator]" data-type="Function" data-required="false" data-desc="为每个元素调用的比较器。"></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="返回去重后的新数组。"></x-field>

**Example**

```javascript
var objects = [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }, { 'x': 1, 'y': 2 }];

_.uniqWith(objects, _.isEqual);
// => [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }]
```

### unzip

此方法类似于 `_.zip`，但它接受一个分组后的元素数组，并创建一个将元素重新组合到其压缩前配置的数组。

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要处理的分组元素数组。"></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="返回重新组合元素的新数组。"></x-field>

**Example**

```javascript
var zipped = _.zip(['a', 'b'], [1, 2], [true, false]);
// => [['a', 1, true], ['b', 2, false]]

_.unzip(zipped);
// => [['a', 'b'], [1, 2], [true, false]]
```

### unzipWith

此方法类似于 `_.unzip`，但它接受一个 `iteratee`（迭代器）来指定如何组合重新分组的值。

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要处理的分组元素数组。"></x-field>
<x-field data-name="[iteratee=_.identity]" data-type="Function" data-required="false" data-desc="用于组合重新分组值的函数。"></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="返回重新组合元素的新数组。"></x-field>

**Example**

```javascript
var zipped = _.zip([1, 2], [10, 20], [100, 200]);
// => [[1, 10, 100], [2, 20, 200]]

_.unzipWith(zipped, _.add);
// => [3, 30, 300]
```

### without

创建一个排除了所有给定值的数组。使用 [`SameValueZero`](http://ecma-international.org/ecma-262/7.0/#sec-samevaluezero) 进行相等性比较。

**Note:** 与 `_.pull` 不同，此方法返回一个新数组。

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要检查的数组。"></x-field>
<x-field data-name="[values]" data-type="...*" data-required="false" data-desc="要排除的值。"></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="返回过滤值后的新数组。"></x-field>

**Example**

```javascript
_.without([2, 1, 2, 3], 1, 2);
// => [3]
```

### xor

创建一个唯一值数组，该数组是给定数组的[对称差](https://en.wikipedia.org/wiki/Symmetric_difference)。

**Parameters**

<x-field data-name="[arrays]" data-type="...Array" data-required="true" data-desc="要检查的数组。"></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="返回过滤值后的新数组。"></x-field>

**Example**

```javascript
_.xor([2, 1], [2, 3]);
// => [1, 3]
```

### xorBy

此方法类似于 `_.xor`，但它接受一个 `iteratee`（迭代器），该迭代器会为每个 `arrays` 的每个元素调用，以生成用于比较的标准。

**Parameters**

<x-field data-name="[arrays]" data-type="...Array" data-required="true" data-desc="要检查的数组。"></x-field>
<x-field data-name="[iteratee=_.identity]" data-type="Function" data-required="false" data-desc="为每个元素调用的迭代器。"></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="返回过滤值后的新数组。"></x-field>

**Example**

```javascript
_.xorBy([2.1, 1.2], [2.3, 3.4], Math.floor);
// => [1.2, 3.4]
```

### xorWith

此方法类似于 `_.xor`，但它接受一个 `comparator`（比较器），该比较器用于比较 `arrays` 的元素。

**Parameters**

<x-field data-name="[arrays]" data-type="...Array" data-required="true" data-desc="要检查的数组。"></x-field>
<x-field data-name="[comparator]" data-type="Function" data-required="false" data-desc="为每个元素调用的比较器。"></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="返回过滤值后的新数组。"></x-field>

**Example**

```javascript
var objects = [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }];
var others = [{ 'x': 1, 'y': 1 }, { 'x': 1, 'y': 2 }];

_.xorWith(objects, others, _.isEqual);
// => [{ 'x': 2, 'y': 1 }, { 'x': 1, 'y': 1 }]
```

### zip

创建一个分组元素的数组，其中第一个元素包含给定数组的第一个元素，第二个元素包含给定数组的第二个元素，以此类推。

**Parameters**

<x-field data-name="[arrays]" data-type="...Array" data-required="true" data-desc="要处理的数组。"></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="返回分组元素的新数组。"></x-field>

**Example**

```javascript
_.zip(['a', 'b'], [1, 2], [true, false]);
// => [['a', 1, true], ['b', 2, false]]
```

### zipObject

此方法类似于 `_.fromPairs`，但它接受两个数组，一个用于属性标识符，另一个用于相应的值。

**Parameters**

<x-field data-name="[props=[]]" data-type="Array" data-required="false" data-desc="属性标识符。"></x-field>
<x-field data-name="[values=[]]" data-type="Array" data-required="false" data-desc="属性值。"></x-field>

**Returns**

<x-field data-name="" data-type="Object" data-desc="返回新对象。"></x-field>

**Example**

```javascript
_.zipObject(['a', 'b'], [1, 2]);
// => { 'a': 1, 'b': 2 }
```

### zipObjectDeep

此方法类似于 `_.zipObject`，但它支持属性路径。

**Parameters**

<x-field data-name="[props=[]]" data-type="Array" data-required="false" data-desc="属性标识符。"></x-field>
<x-field data-name="[values=[]]" data-type="Array" data-required="false" data-desc="属性值。"></x-field>

**Returns**

<x-field data-name="" data-type="Object" data-desc="返回新对象。"></x-field>

**Example**

```javascript
_.zipObjectDeep(['a.b[0].c', 'a.b[1].d'], [1, 2]);
// => { 'a': { 'b': [{ 'c': 1 }, { 'd': 2 }] } }
```

### zipWith

此方法类似于 `_.zip`，但它接受一个 `iteratee`（迭代器）来指定如何组合分组的值。调用迭代器时会传入每个组的元素：(...group)。

**Parameters**

<x-field data-name="[arrays]" data-type="...Array" data-required="true" data-desc="要处理的数组。"></x-field>
<x-field data-name="[iteratee=_.identity]" data-type="Function" data-required="false" data-desc="用于组合分组值的函数。"></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="返回分组元素的新数组。"></x-field>

**Example**

```javascript
_.zipWith([1, 2], [10, 20], [100, 200], function(a, b, c) {
  return a + b + c;
});
// => [111, 222]
```
