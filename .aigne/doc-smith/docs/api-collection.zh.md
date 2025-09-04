# 集合

集合函数旨在迭代和操作数据集合，在 Lodash 中，集合可以是数组或对象。这些方法提供了强大的工具，用于过滤、映射、分组和归约数据，而无需考虑其底层结构。有关特定于数组或对象的函数，请参阅 [Array](./api-array.md) 和 [Object](./api-object.md) 部分。

## 方法

| 方法 | 描述 |
|---|---|
| [`_.countBy`](#_countbycollection-iteratee__identity) | 创建一个由键组成的对象，这些键是通过对集合中的每个元素运行迭代器生成的。每个键对应的值是该键被返回的次数。 |
| [`_.every`](#_everycollection-predicate__identity) | 检查谓词是否对集合的所有元素都返回真值。 |
| [`_.filter`](#_filtercollection-predicate__identity) | 迭代集合的元素，返回一个由谓词返回真值的所有元素组成的数组。 |
| [`_.find`](#_findcollection-predicate__identity-fromindex0) | 迭代集合的元素，返回谓词为其返回真值的第一个元素。 |
| [`_.findLast`](#_findlastcollection-predicate__identity-fromindexcollectionlength-1) | 此方法类似于 `_.find`，只是它从右到左迭代集合的元素。 |
| [`_.flatMap`](#_flatmapcollection-iteratee__identity) | 通过对集合中的每个元素运行迭代器并展平映射结果来创建一个扁平化的值数组。 |
| [`_.flatMapDeep`](#_flatmapdeepcollection-iteratee__identity) | 此方法类似于 `_.flatMap`，只是它会递归地展平映射结果。 |
| [`_.flatMapDepth`](#_flatmapdepthcollection-iteratee__identity-depth1) | 此方法类似于 `_.flatMap`，只是它会递归地将映射结果展平到指定深度。 |
| [`_.forEach`](#_foreachcollection-iteratee__identity) | 迭代集合的元素，并为每个元素调用迭代器。别名：`_.each`。 |
| [`_.forEachRight`](#_foreachrightcollection-iteratee__identity) | 此方法类似于 `_.forEach`，只是它从右到左迭代集合的元素。别名：`_.eachRight`。 |
| [`_.groupBy`](#_groupbycollection-iteratee__identity) | 创建一个由键组成的对象，这些键是通过对集合中的每个元素运行迭代器生成的。分组值的顺序由它们在集合中出现的顺序决定。 |
| [`_.includes`](#_includescollection-value-fromindex0) | 检查一个值是否在集合中。 |
| [`_.invokeMap`](#_invokemapcollection-path-args) | 为集合中的每个元素调用指定路径上的方法。 |
| [`_.keyBy`](#_keybycollection-iteratee__identity) | 创建一个由键组成的对象，这些键是通过对集合中的每个元素运行迭代器生成的。每个键对应的值是最后一个负责生成该键的元素。 |
| [`_.map`](#_mapcollection-iteratee__identity) | 通过对集合中的每个元素运行迭代器来创建一个值数组。 |
| [`_.orderBy`](#_orderbycollection-iteratees_identity-orders) | 此方法类似于 `_.sortBy`，只是它允许指定用于排序的迭代器的排序顺序。 |
| [`_.partition`](#_partitioncollection-predicate__identity) | 创建一个元素数组，分为两组，第一组包含谓词返回真值的元素，第二组包含谓词返回假值的元素。 |
| [`_.reduce`](#_reducecollection-iteratee__identity-accumulator) | 通过对集合中的每个元素运行迭代器，将集合归约为一个值。 |
| [`_.reduceRight`](#_reducerightcollection-iteratee__identity-accumulator) | 此方法类似于 `_.reduce`，只是它从右到左迭代集合的元素。 |
| [`_.reject`](#_rejectcollection-predicate__identity) | `_.filter` 的反向方法；此方法返回集合中谓词不返回真值的元素。 |
| [`_.sample`](#_samplecollection) | 从集合中获取一个随机元素。 |
| [`_.sampleSize`](#_samplesizecollection-n1) | 从集合中获取 `n` 个具有唯一键的随机元素，数量不超过集合的大小。 |
| [`_.shuffle`](#_shufflecollection) | 创建一个打乱值的数组，使用 Fisher-Yates shuffle 的一个版本。 |
| [`_.size`](#_sizecollection) | 获取集合的大小，对于类数组值，返回其长度，对于对象，返回其自身可枚举字符串键属性的数量。 |
| [`_.some`](#_somecollection-predicate__identity) | 检查谓词是否对集合的任何元素返回真值。 |
| [`_.sortBy`](#_sortbycollection-iteratees_identity) | 创建一个元素数组，根据对集合中每个元素运行每个迭代器的结果按升序排序。 |

---

### _.countBy(collection, [iteratee=_.identity])

创建一个由键组成的对象，这些键是通过对 `collection` 中的每个元素运行 `iteratee` 生成的。每个键的值是产生该键的元素的数量。

**参数**

| 参数 | 类型 | 描述 |
|---|---|---|
| `collection` | `Array` or `Object` | 要迭代的集合。 |
| `[iteratee=_.identity]` | `Function` | 每次迭代时调用以生成键的函数。 |

**返回值**

(`Object`): 返回组合的聚合对象。

**示例**

```javascript
_.countBy([6.1, 4.2, 6.3], Math.floor);
// => { '4': 1, '6': 2 }

// 使用 _.property 迭代器简写。
_.countBy(['one', 'two', 'three'], 'length');
// => { '3': 2, '5': 1 }
```

### _.every(collection, [predicate=_.identity])

检查 `predicate` 是否对 `collection` 的**所有**元素都返回真值。一旦 `predicate` 返回假值，迭代就会停止。

**参数**

| 参数 | 类型 | 描述 |
|---|---|---|
| `collection` | `Array` or `Object` | 要迭代的集合。 |
| `[predicate=_.identity]` | `Function` | 每次迭代时调用的函数。 |

**返回值**

(`boolean`): 如果所有元素都通过谓词检查，则返回 `true`，否则返回 `false`。

**示例**

```javascript
_.every([true, 1, null, 'yes'], Boolean);
// => false

var users = [
  { 'user': 'barney', 'age': 36, 'active': false },
  { 'user': 'fred',   'age': 40, 'active': false }
];

// `_.matchesProperty` 迭代器简写。
_.every(users, ['active', false]);
// => true
```

### _.filter(collection, [predicate=_.identity])

迭代 `collection` 的元素，返回一个由 `predicate` 返回真值的所有元素组成的数组。

**参数**

| 参数 | 类型 | 描述 |
|---|---|---|
| `collection` | `Array` or `Object` | 要迭代的集合。 |
| `[predicate=_.identity]` | `Function` | 每次迭代时调用的函数。 |

**返回值**

(`Array`): 返回新的已过滤数组。

**示例**

```javascript
var users = [
  { 'user': 'barney', 'age': 36, 'active': true },
  { 'user': 'fred',   'age': 40, 'active': false }
];

_.filter(users, function(o) { return !o.active; });
// => objects for ['fred']

// `_.matches` 迭代器简写。
_.filter(users, { 'age': 36, 'active': true });
// => objects for ['barney']
```

### _.find(collection, [predicate=_.identity], [fromIndex=0])

迭代 `collection` 的元素，返回 `predicate` 为其返回真值的第一个元素。

**参数**

| 参数 | 类型 | 描述 |
|---|---|---|
| `collection` | `Array` or `Object` | 要检查的集合。 |
| `[predicate=_.identity]` | `Function` | 每次迭代时调用的函数。 |
| `[fromIndex=0]` | `number` | 开始搜索的索引。 |

**返回值**

(`*`): 返回匹配的元素，否则返回 `undefined`。

**示例**

```javascript
var users = [
  { 'user': 'barney',  'age': 36, 'active': true },
  { 'user': 'fred',    'age': 40, 'active': false },
  { 'user': 'pebbles', 'age': 1,  'active': true }
];

_.find(users, function(o) { return o.age < 40; });
// => object for 'barney'

// `_.property` 迭代器简写。
_.find(users, 'active');
// => object for 'barney'
```

### _.findLast(collection, [predicate=_.identity], [fromIndex=collection.length-1])

此方法类似于 `_.find`，只是它从右到左迭代 `collection` 的元素。

**参数**

| 参数 | 类型 | 描述 |
|---|---|---|
| `collection` | `Array` or `Object` | 要检查的集合。 |
| `[predicate=_.identity]` | `Function` | 每次迭代时调用的函数。 |
| `[fromIndex=collection.length-1]` | `number` | 开始搜索的索引。 |

**返回值**

(`*`): 返回匹配的元素，否则返回 `undefined`。

**示例**

```javascript
_.findLast([1, 2, 3, 4], function(n) {
  return n % 2 == 1;
});
// => 3
```

### _.flatMap(collection, [iteratee=_.identity])

通过对 `collection` 中的每个元素运行 `iteratee` 并将映射结果展平一级来创建一个扁平化的值数组。

**参数**

| 参数 | 类型 | 描述 |
|---|---|---|
| `collection` | `Array` or `Object` | 要迭代的集合。 |
| `[iteratee=_.identity]` | `Function` | 每次迭代时调用的函数。 |

**返回值**

(`Array`): 返回新的扁平化数组。

**示例**

```javascript
function duplicate(n) {
  return [n, n];
}

_.flatMap([1, 2], duplicate);
// => [1, 1, 2, 2]
```

### _.flatMapDeep(collection, [iteratee=_.identity])

此方法类似于 `_.flatMap`，只是它会递归地展平映射结果。

**参数**

| 参数 | 类型 | 描述 |
|---|---|---|
| `collection` | `Array` or `Object` | 要迭代的集合。 |
| `[iteratee=_.identity]` | `Function` | 每次迭代时调用的函数。 |

**返回值**

(`Array`): 返回新的扁平化数组。

**示例**

```javascript
function duplicate(n) {
  return [[[n, n]]];
}

_.flatMapDeep([1, 2], duplicate);
// => [1, 1, 2, 2]
```

### _.flatMapDepth(collection, [iteratee=_.identity], [depth=1])

此方法类似于 `_.flatMap`，只是它会递归地将映射结果展平最多 `depth` 次。

**参数**

| 参数 | 类型 | 描述 |
|---|---|---|
| `collection` | `Array` or `Object` | 要迭代的集合。 |
| `[iteratee=_.identity]` | `Function` | 每次迭代时调用的函数。 |
| `[depth=1]` | `number` | 最大递归深度。 |

**返回值**

(`Array`): 返回新的扁平化数组。

**示例**

```javascript
function duplicate(n) {
  return [[[n, n]]];
}

_.flatMapDepth([1, 2], duplicate, 2);
// => [[1, 1], [2, 2]]
```

### _.forEach(collection, [iteratee=_.identity])

迭代 `collection` 的元素，并为每个元素调用 `iteratee`。迭代器可以通过显式返回 `false` 来提前退出迭代。别名：`_.each`。

**参数**

| 参数 | 类型 | 描述 |
|---|---|---|
| `collection` | `Array` or `Object` | 要迭代的集合。 |
| `[iteratee=_.identity]` | `Function` | 每次迭代时调用的函数。 |

**返回值**

(`Array` or `Object`): 返回 `collection`。

**示例**

```javascript
_.forEach([1, 2], function(value) {
  console.log(value);
});
// => 输出 `1` 然后是 `2`。

_.forEach({ 'a': 1, 'b': 2 }, function(value, key) {
  console.log(key);
});
// => 输出 'a' 然后是 'b'（不保证迭代顺序）。
```

### _.forEachRight(collection, [iteratee=_.identity])

此方法类似于 `_.forEach`，只是它从右到左迭代 `collection` 的元素。别名：`_.eachRight`。

**参数**

| 参数 | 类型 | 描述 |
|---|---|---|
| `collection` | `Array` or `Object` | 要迭代的集合。 |
| `[iteratee=_.identity]` | `Function` | 每次迭代时调用的函数。 |

**返回值**

(`Array` or `Object`): 返回 `collection`。

**示例**

```javascript
_.forEachRight([1, 2], function(value) {
  console.log(value);
});
// => 输出 `2` 然后是 `1`。
```

### _.groupBy(collection, [iteratee=_.identity])

创建一个由键组成的对象，这些键是通过对 `collection` 中的每个元素运行 `iteratee` 的结果生成的。每个键的值是负责生成该键的元素数组。

**参数**

| 参数 | 类型 | 描述 |
|---|---|---|
| `collection` | `Array` or `Object` | 要迭代的集合。 |
| `[iteratee=_.identity]` | `Function` | 用于转换键的迭代器。 |

**返回值**

(`Object`): 返回组合的聚合对象。

**示例**

```javascript
_.groupBy([6.1, 4.2, 6.3], Math.floor);
// => { '4': [4.2], '6': [6.1, 6.3] }

// `_.property` 迭代器简写。
_.groupBy(['one', 'two', 'three'], 'length');
// => { '3': ['one', 'two'], '5': ['three'] }
```

### _.includes(collection, value, [fromIndex=0])

检查 `value` 是否在 `collection` 中。如果 `collection` 是字符串，则检查 `value` 是否为其子字符串。如果 `fromIndex` 为负数，则用作从 `collection` 末尾开始的偏移量。

**参数**

| 参数 | 类型 | 描述 |
|---|---|---|
| `collection` | `Array`, `Object`, or `string` | 要检查的集合。 |
| `value` | `*` | 要搜索的值。 |
| `[fromIndex=0]` | `number` | 开始搜索的索引。 |

**返回值**

(`boolean`): 如果找到 `value`，则返回 `true`，否则返回 `false`。

**示例**

```javascript
_.includes([1, 2, 3], 1);
// => true

_.includes([1, 2, 3], 1, 2);
// => false

_.includes({ 'a': 1, 'b': 2 }, 1);
// => true

_.includes('abcd', 'bc');
// => true
```

### _.invokeMap(collection, path, [args])

调用 `collection` 中每个元素的 `path` 处​​的方法，返回一个包含结果的数组。附加参数会提供给每个被调用的方法。

**参数**

| 参数 | 类型 | 描述 |
|---|---|---|
| `collection` | `Array` or `Object` | 要迭代的集合。 |
| `path` | `Array`, `Function`, or `string` | 要调用的方法的路径或每次迭代调用的函数。 |
| `[args]` | `...*` | 调用每个方法时使用的参数。 |

**返回值**

(`Array`): 返回结果数组。

**示例**

```javascript
_.invokeMap([[5, 1, 7], [3, 2, 1]], 'sort');
// => [[1, 5, 7], [1, 2, 3]]

_.invokeMap([123, 456], String.prototype.split, '');
// => [['1', '2', '3'], ['4', '5', '6']]
```

### _.keyBy(collection, [iteratee=_.identity])

创建一个由键组成的对象，这些键是通过对 `collection` 中的每个元素运行 `iteratee` 生成的。每个键对应的值是最后一个负责生成该键的元素。

**参数**

| 参数 | 类型 | 描述 |
|---|---|---|
| `collection` | `Array` or `Object` | 要迭代的集合。 |
| `[iteratee=_.identity]` | `Function` | 用于转换键的迭代器。 |

**返回值**

(`Object`): 返回组合的聚合对象。

**示例**

```javascript
var array = [
  { 'dir': 'left', 'code': 97 },
  { 'dir': 'right', 'code': 100 }
];

_.keyBy(array, function(o) {
  return String.fromCharCode(o.code);
});
// => { 'a': { 'dir': 'left', 'code': 97 }, 'd': { 'dir': 'right', 'code': 100 } }

_.keyBy(array, 'dir');
// => { 'left': { 'dir': 'left', 'code': 97 }, 'right': { 'dir': 'right', 'code': 100 } }
```

### _.map(collection, [iteratee=_.identity])

通过对 `collection` 中的每个元素运行 `iteratee` 来创建一个值数组。

**参数**

| 参数 | 类型 | 描述 |
|---|---|---|
| `collection` | `Array` or `Object` | 要迭代的集合。 |
| `[iteratee=_.identity]` | `Function` | 每次迭代时调用的函数。 |

**返回值**

(`Array`): 返回新的映射后数组。

**示例**

```javascript
function square(n) {
  return n * n;
}

_.map([4, 8], square);
// => [16, 64]

_.map({ 'a': 4, 'b': 8 }, square);
// => [16, 64] (不保证迭代顺序)
```

### _.orderBy(collection, [iteratees=[_.identity]], [orders])

此方法类似于 `_.sortBy`，只是它允许为迭代器指定排序顺序。如果未指定 `orders`，则所有值都按升序排序。否则，指定 `'desc'` 为降序或 `'asc'` 为升序。

**参数**

| 参数 | 类型 | 描述 |
|---|---|---|
| `collection` | `Array` or `Object` | 要迭代的集合。 |
| `[iteratees=[_.identity]]` | `Array[]`, `Function[]`, `Object[]`, or `string[]` | 用于排序的迭代器。 |
| `[orders]` | `string[]` | `iteratees` 的排序顺序。 |

**返回值**

(`Array`): 返回新的已排序数组。

**示例**

```javascript
var users = [
  { 'user': 'fred',   'age': 48 },
  { 'user': 'barney', 'age': 34 },
  { 'user': 'fred',   'age': 40 },
  { 'user': 'barney', 'age': 36 }
];

// 按 `user` 升序排序，按 `age` 降序排序。
_.orderBy(users, ['user', 'age'], ['asc', 'desc']);
// => objects for [['barney', 36], ['barney', 34], ['fred', 48], ['fred', 40]]
```

### _.partition(collection, [predicate=_.identity])

创建一个元素数组，分为两组。第一组包含 `predicate` 返回 true 的元素，第二组包含 `predicate` 返回 false 的元素。

**参数**

| 参数 | 类型 | 描述 |
|---|---|---|
| `collection` | `Array` or `Object` | 要迭代的集合。 |
| `[predicate=_.identity]` | `Function` | 每次迭代时调用的函数。 |

**返回值**

(`Array`): 返回分组后的元素数组。

**示例**

```javascript
var users = [
  { 'user': 'barney',  'age': 36, 'active': false },
  { 'user': 'fred',    'age': 40, 'active': true },
  { 'user': 'pebbles', 'age': 1,  'active': false }
];

_.partition(users, function(o) { return o.active; });
// => objects for [['fred'], ['barney', 'pebbles']]
```

### _.reduce(collection, [iteratee=_.identity], [accumulator])

通过对每个元素运行 `iteratee` 将 `collection` 归约为一个值。迭代器的返回值是下一次迭代的累积值。如果未提供 `accumulator`，则使用 `collection` 的第一个元素作为初始值。

**参数**

| 参数 | 类型 | 描述 |
|---|---|---|
| `collection` | `Array` or `Object` | 要迭代的集合。 |
| `[iteratee=_.identity]` | `Function` | 每次迭代时调用的函数。 |
| `[accumulator]` | `*` | 初始值。 |

**返回值**

(`*`): 返回累积值。

**示例**

```javascript
_.reduce([1, 2], function(sum, n) {
  return sum + n;
}, 0);
// => 3

_.reduce({ 'a': 1, 'b': 2, 'c': 1 }, function(result, value, key) {
  (result[value] || (result[value] = [])).push(key);
  return result;
}, {});
// => { '1': ['a', 'c'], '2': ['b'] } (不保证迭代顺序)
```

### _.reduceRight(collection, [iteratee=_.identity], [accumulator])

此方法类似于 `_.reduce`，只是它从右到左迭代 `collection` 的元素。

**参数**

| 参数 | 类型 | 描述 |
|---|---|---|
| `collection` | `Array` or `Object` | 要迭代的集合。 |
| `[iteratee=_.identity]` | `Function` | 每次迭代时调用的函数。 |
| `[accumulator]` | `*` | 初始值。 |

**返回值**

(`*`): 返回累积值。

**示例**

```javascript
var array = [[0, 1], [2, 3], [4, 5]];

_.reduceRight(array, function(flattened, other) {
  return flattened.concat(other);
}, []);
// => [4, 5, 2, 3, 0, 1]
```

### _.reject(collection, [predicate=_.identity])

`_.filter` 的反向方法；此方法返回 `collection` 中 `predicate` **不**返回真值的元素。

**参数**

| 参数 | 类型 | 描述 |
|---|---|---|
| `collection` | `Array` or `Object` | 要迭代的集合。 |
| `[predicate=_.identity]` | `Function` | 每次迭代时调用的函数。 |

**返回值**

(`Array`): 返回新的已过滤数组。

**示例**

```javascript
var users = [
  { 'user': 'barney', 'age': 36, 'active': false },
  { 'user': 'fred',   'age': 40, 'active': true }
];

_.reject(users, function(o) { return !o.active; });
// => objects for ['fred']
```

### _.sample(collection)

从 `collection` 中获取一个随机元素。

**参数**

| 参数 | 类型 | 描述 |
|---|---|---|
| `collection` | `Array` or `Object` | 要采样的集合。 |

**返回值**

(`*`): 返回随机元素。

**示例**

```javascript
_.sample([1, 2, 3, 4]);
// => 2
```

### _.sampleSize(collection, [n=1])

从 `collection` 中获取 `n` 个随机元素。

**参数**

| 参数 | 类型 | 描述 |
|---|---|---|
| `collection` | `Array` or `Object` | 要采样的集合。 |
| `[n=1]` | `number` | 要采样的元素数量。 |

**返回值**

(`Array`): 返回随机元素。

**示例**

```javascript
_.sampleSize([1, 2, 3], 2);
// => [3, 1]

_.sampleSize([1, 2, 3], 4);
// => [2, 3, 1]
```

### _.shuffle(collection)

创建一个打乱值的数组，使用 [Fisher-Yates shuffle](https://en.wikipedia.org/wiki/Fisher-Yates_shuffle) 的一个版本。

**参数**

| 参数 | 类型 | 描述 |
|---|---|---|
| `collection` | `Array` or `Object` | 要打乱的集合。 |

**返回值**

(`Array`): 返回新的已打乱数组。

**示例**

```javascript
_.shuffle([1, 2, 3, 4]);
// => [4, 1, 3, 2]
```

### _.size(collection)

获取 `collection` 的大小，对于类数组值，返回其长度，对于对象，返回其自身可枚举字符串键属性的数量。

**参数**

| 参数 | 类型 | 描述 |
|---|---|---|
| `collection` | `Array`, `Object`, or `string` | 要检查的集合。 |

**返回值**

(`number`): 返回集合大小。

**示例**

```javascript
_.size([1, 2, 3]);
// => 3

_.size({ 'a': 1, 'b': 2 });
// => 2

_.size('pebbles');
// => 7
```

### _.some(collection, [predicate=_.identity])

检查 `predicate` 是否对 `collection` 的**任何**元素返回真值。一旦 `predicate` 返回真值，迭代就会停止。

**参数**

| 参数 | 类型 | 描述 |
|---|---|---|
| `collection` | `Array` or `Object` | 要迭代的集合。 |
| `[predicate=_.identity]` | `Function` | 每次迭代时调用的函数。 |

**返回值**

(`boolean`): 如果有任何元素通过谓词检查，则返回 `true`，否则返回 `false`。

**示例**

```javascript
_.some([null, 0, 'yes', false], Boolean);
// => true

var users = [
  { 'user': 'barney', 'active': true },
  { 'user': 'fred',   'active': false }
];

// `_.property` 迭代器简写。
_.some(users, 'active');
// => true
```

### _.sortBy(collection, [iteratees=[_.identity]])

创建一个元素数组，根据对集合中每个元素运行每个迭代器的结果按升序排序。此方法执行稳定排序。

**参数**

| 参数 | 类型 | 描述 |
|---|---|---|
| `collection` | `Array` or `Object` | 要迭代的集合。 |
| `[iteratees=[_.identity]]` | `...(Function|Function[])` | 用于排序的迭代器。 |

**返回值**

(`Array`): 返回新的已排序数组。

**示例**

```javascript
var users = [
  { 'user': 'fred',   'age': 48 },
  { 'user': 'barney', 'age': 36 },
  { 'user': 'fred',   'age': 30 },
  { 'user': 'barney', 'age': 34 }
];

_.sortBy(users, [function(o) { return o.user; }]);
// => objects for [['barney', 36], ['barney', 34], ['fred', 48], ['fred', 30]]

_.sortBy(users, ['user', 'age']);
// => objects for [['barney', 34], ['barney', 36], ['fred', 30], ['fred', 48]]
```

---

本节介绍了处理集合的基本函数。有关更专门的操作，您可能需要浏览 [Array](./api-array.md) 或 [Object](./api-object.md) API 部分。