# 集合

集合函数用于遍历数组、对象和字符串等集合。它们为过滤、映射、分组和归约等常见的数据操作任务提供了强大而简洁的方法。

对于特定于单一数据类型的函数，你可能还需要查阅 [Array](./api-array.md) 或 [Object](./api-object.md) 文档。

---

### `_.countBy(collection, [iteratee=_.identity])`

创建一个对象，其键由 `collection` 的每个元素经过 `iteratee` 处理后生成。每个键对应的值是 `iteratee` 返回该键的次数。

**起始版本**
0.5.0

**参数**

| Name | Type | Description |
|---|---|---|
| `collection` | `Array`\|`Object` | 要遍历的集合。 |
| `[iteratee=_.identity]` | `Function` | 每次迭代时调用以生成键的函数。 |

**返回值**

`(Object)`: 返回组合的聚合对象。

**示例**

```javascript
_.countBy([6.1, 4.2, 6.3], Math.floor);
// => { '4': 1, '6': 2 }

// The `_.property` iteratee shorthand.
_.countBy(['one', 'two', 'three'], 'length');
// => { '3': 2, '5': 1 }
```

---

### `_.every(collection, [predicate=_.identity])`

检查 `predicate` 是否对 `collection` 的**所有**元素都返回真值。一旦 `predicate` 返回假值，迭代就会停止。注意：此方法对空集合返回 `true`，因为对于空集合中的元素，任何判断都为真。

**起始版本**
0.1.0

**参数**

| Name | Type | Description |
|---|---|---|
| `collection` | `Array`\|`Object` | 要遍历的集合。 |
| `[predicate=_.identity]` | `Function` | 每次迭代时调用的函数。 |

**返回值**

`(boolean)`: 如果所有元素都通过断言检查，则返回 `true`，否则返回 `false`。

**示例**

```javascript
_.every([true, 1, null, 'yes'], Boolean);
// => false

var users = [
  { 'user': 'barney', 'age': 36, 'active': false },
  { 'user': 'fred',   'age': 40, 'active': false }
];

// The `_.matches` iteratee shorthand.
_.every(users, { 'user': 'barney', 'active': false });
// => false

// The `_.matchesProperty` iteratee shorthand.
_.every(users, ['active', false]);
// => true

// The `_.property` iteratee shorthand.
_.every(users, 'active');
// => false
```

---

### `_.filter(collection, [predicate=_.identity])`

遍历 `collection` 的元素，返回一个包含所有 `predicate` 返回真值的元素的新数组。断言函数调用时会传入三个参数：`(value, index|key, collection)`。

**起始版本**
0.1.0

**参数**

| Name | Type | Description |
|---|---|---|
| `collection` | `Array`\|`Object` | 要遍历的集合。 |
| `[predicate=_.identity]` | `Function` | 每次迭代时调用的函数。 |

**返回值**

`(Array)`: 返回新的已过滤数组。

**示例**

```javascript
var users = [
  { 'user': 'barney', 'age': 36, 'active': true },
  { 'user': 'fred',   'age': 40, 'active': false }
];

_.filter(users, function(o) { return !o.active; });
// => objects for ['fred']

// The `_.matches` iteratee shorthand.
_.filter(users, { 'age': 36, 'active': true });
// => objects for ['barney']
```

---

### `_.find(collection, [predicate=_.identity], [fromIndex=0])`

遍历 `collection` 的元素，返回第一个 `predicate` 返回真值的元素。断言函数调用时会传入三个参数：`(value, index|key, collection)`。

**起始版本**
0.1.0

**参数**

| Name | Type | Description |
|---|---|---|
| `collection` | `Array`\|`Object` | 要检查的集合。 |
| `[predicate=_.identity]` | `Function` | 每次迭代时调用的函数。 |
| `[fromIndex=0]` | `number` | 开始搜索的索引。 |

**返回值**

`(*)`: 返回匹配的元素，否则返回 `undefined`。

**示例**

```javascript
var users = [
  { 'user': 'barney',  'age': 36, 'active': true },
  { 'user': 'fred',    'age': 40, 'active': false },
  { 'user': 'pebbles', 'age': 1,  'active': true }
];

_.find(users, function(o) { return o.age < 40; });
// => object for 'barney'

// The `_.matchesProperty` iteratee shorthand.
_.find(users, ['active', false]);
// => object for 'fred'
```

---

### `_.findLast(collection, [predicate=_.identity], [fromIndex=collection.length-1])`

此方法类似于 `_.find`，只是它从右到左遍历 `collection` 的元素。

**起始版本**
2.0.0

**参数**

| Name | Type | Description |
|---|---|---|
| `collection` | `Array`\|`Object` | 要检查的集合。 |
| `[predicate=_.identity]` | `Function` | 每次迭代时调用的函数。 |
| `[fromIndex=collection.length-1]` | `number` | 开始搜索的索引。 |

**返回值**

`(*)`: 返回匹配的元素，否则返回 `undefined`。

**示例**

```javascript
_.findLast([1, 2, 3, 4], function(n) {
  return n % 2 == 1;
});
// => 3
```

---

### `_.flatMap(collection, [iteratee=_.identity])`

通过对 `collection` 中的每个元素运行 `iteratee` 并将映射结果展平，创建一个展平的值数组。迭代函数调用时会传入三个参数：`(value, index|key, collection)`。

**起始版本**
4.0.0

**参数**

| Name | Type | Description |
|---|---|---|
| `collection` | `Array`\|`Object` | 要遍历的集合。 |
| `[iteratee=_.identity]` | `Function` | 每次迭代时调用的函数。 |

**返回值**

`(Array)`: 返回新的已展平数组。

**示例**

```javascript
function duplicate(n) {
  return [n, n];
}

_.flatMap([1, 2], duplicate);
// => [1, 1, 2, 2]
```

---

### `_.flatMapDeep(collection, [iteratee=_.identity])`

此方法类似于 `_.flatMap`，只是它会递归地展平映射结果。

**起始版本**
4.7.0

**参数**

| Name | Type | Description |
|---|---|---|
| `collection` | `Array`\|`Object` | 要遍历的集合。 |
| `[iteratee=_.identity]` | `Function` | 每次迭代时调用的函数。 |

**返回值**

`(Array)`: 返回新的已展平数组。

**示例**

```javascript
function duplicate(n) {
  return [[[n, n]]];
}

_.flatMapDeep([1, 2], duplicate);
// => [1, 1, 2, 2]
```

---

### `_.flatMapDepth(collection, [iteratee=_.identity], [depth=1])`

此方法类似于 `_.flatMap`，只是它会递归地将映射结果展平最多 `depth` 次。

**起始版本**
4.7.0

**参数**

| Name | Type | Description |
|---|---|---|
| `collection` | `Array`\|`Object` | 要遍历的集合。 |
| `[iteratee=_.identity]` | `Function` | 每次迭代时调用的函数。 |
| `[depth=1]` | `number` | 最大递归深度。 |

**返回值**

`(Array)`: 返回新的已展平数组。

**示例**

```javascript
function duplicate(n) {
  return [[[n, n]]];
}

_.flatMapDepth([1, 2], duplicate, 2);
// => [[1, 1], [2, 2]]
```

---

### `_.forEach(collection, [iteratee=_.identity])`

遍历 `collection` 的元素，并为每个元素调用 `iteratee`。迭代函数调用时会传入三个参数：`(value, index|key, collection)`。迭代函数可以通过显式返回 `false` 来提前退出迭代。

**起始版本**
0.1.0

**参数**

| Name | Type | Description |
|---|---|---|
| `collection` | `Array`\|`Object` | 要遍历的集合。 |
| `[iteratee=_.identity]` | `Function` | 每次迭代时调用的函数。 |

**返回值**

`(Array|Object)`: 返回 `collection`。

**示例**

```javascript
_.forEach([1, 2], function(value) {
  console.log(value);
});
// => Logs `1` then `2`.

_.forEach({ 'a': 1, 'b': 2 }, function(value, key) {
  console.log(key);
});
// => Logs 'a' then 'b' (iteration order is not guaranteed).
```

---

### `_.forEachRight(collection, [iteratee=_.identity])`

此方法类似于 `_.forEach`，只是它从右到左遍历 `collection` 的元素。

**起始版本**
2.0.0

**参数**

| Name | Type | Description |
|---|---|---|
| `collection` | `Array`\|`Object` | 要遍历的集合。 |
| `[iteratee=_.identity]` | `Function` | 每次迭代时调用的函数。 |

**返回值**

`(Array|Object)`: 返回 `collection`。

**示例**

```javascript
_.forEachRight([1, 2], function(value) {
  console.log(value);
});
// => Logs `2` then `1`.
```

---

### `_.groupBy(collection, [iteratee=_.identity])`

创建一个对象，其键由 `collection` 的每个元素经过 `iteratee` 处理后生成。每个键对应的值是一个数组，其中包含生成该键的元素。

**起始版本**
0.1.0

**参数**

| Name | Type | Description |
|---|---|---|
| `collection` | `Array`\|`Object` | 要遍历的集合。 |
| `[iteratee=_.identity]` | `Function` | 用于转换键的迭代函数。 |

**返回值**

`(Object)`: 返回组合的聚合对象。

**示例**

```javascript
_.groupBy([6.1, 4.2, 6.3], Math.floor);
// => { '4': [4.2], '6': [6.1, 6.3] }

// The `_.property` iteratee shorthand.
_.groupBy(['one', 'two', 'three'], 'length');
// => { '3': ['one', 'two'], '5': ['three'] }
```

---

### `_.includes(collection, value, [fromIndex=0])`

检查 `value` 是否在 `collection` 中。如果 `collection` 是一个字符串，则检查它是否包含子字符串 `value`。否则，使用 `SameValueZero` 进行等值比较。如果 `fromIndex` 为负数，则将其用作 `collection` 末尾的偏移量。

**起始版本**
0.1.0

**参数**

| Name | Type | Description |
|---|---|---|
| `collection` | `Array`\|`Object`\|`string` | 要检查的集合。 |
| `value` | `*` | 要搜索的值。 |
| `[fromIndex=0]` | `number` | 开始搜索的索引。 |

**返回值**

`(boolean)`: 如果找到 `value`，则返回 `true`，否则返回 `false`。

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

---

### `_.invokeMap(collection, path, [args])`

调用 `collection` 中每个元素的 `path` 路径上的方法，返回一个包含结果的数组。任何附加参数都将提供给每个被调用的方法。如果 `path` 是一个函数，它将为 `collection` 中的每个元素调用，并将 `this` 绑定到该元素。

**起始版本**
4.0.0

**参数**

| Name | Type | Description |
|---|---|---|
| `collection` | `Array`\|`Object` | 要遍历的集合。 |
| `path` | `Array`\|`Function`\|`string` | 要调用的方法的路径或每次迭代时调用的函数。 |
| `[args]` | `...*` | 调用每个方法时传入的参数。 |

**返回值**

`(Array)`: 返回结果数组。

**示例**

```javascript
_.invokeMap([[5, 1, 7], [3, 2, 1]], 'sort');
// => [[1, 5, 7], [1, 2, 3]]

_.invokeMap([123, 456], String.prototype.split, '');
// => [['1', '2', '3'], ['4', '5', '6']]
```

---

### `_.keyBy(collection, [iteratee=_.identity])`

创建一个对象，其键由 `collection` 的每个元素经过 `iteratee` 处理后生成。每个键对应的值是最后一个生成该键的元素。

**起始版本**
4.0.0

**参数**

| Name | Type | Description |
|---|---|---|
| `collection` | `Array`\|`Object` | 要遍历的集合。 |
| `[iteratee=_.identity]` | `Function` | 用于转换键的迭代函数。 |

**返回值**

`(Object)`: 返回组合的聚合对象。

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

---

### `_.map(collection, [iteratee=_.identity])`

通过对 `collection` 中的每个元素运行 `iteratee` 来创建一个值数组。迭代函数调用时会传入三个参数：`(value, index|key, collection)`。

**起始版本**
0.1.0

**参数**

| Name | Type | Description |
|---|---|---|
| `collection` | `Array`\|`Object` | 要遍历的集合。 |
| `[iteratee=_.identity]` | `Function` | 每次迭代时调用的函数。 |

**返回值**

`(Array)`: 返回新的已映射数组。

**示例**

```javascript
function square(n) {
  return n * n;
}

_.map([4, 8], square);
// => [16, 64]

_.map({ 'a': 4, 'b': 8 }, square);
// => [16, 64] (iteration order is not guaranteed)

var users = [
  { 'user': 'barney' },
  { 'user': 'fred' }
];

// The `_.property` iteratee shorthand.
_.map(users, 'user');
// => ['barney', 'fred']
```

---

### `_.orderBy(collection, [iteratees=[_.identity]], [orders])`

此方法类似于 `_.sortBy`，但它允许指定迭代函数的排序顺序。如果未指定 `orders`，则所有值都按升序排序。否则，为每个迭代函数指定 `'desc'`（降序）或 `'asc'`（升序）的排序顺序。

**起始版本**
4.0.0

**参数**

| Name | Type | Description |
|---|---|---|
| `collection` | `Array`\|`Object` | 要遍历的集合。 |
| `[iteratees=[_.identity]]` | `(Array[]\|Function[]\|Object[]\|string[])` | 用于排序的迭代函数。 |
| `[orders]` | `string[]` | `iteratees` 的排序顺序。 |

**返回值**

`(Array)`: 返回新的已排序数组。

**示例**

```javascript
var users = [
  { 'user': 'fred',   'age': 48 },
  { 'user': 'barney', 'age': 34 },
  { 'user': 'fred',   'age': 40 },
  { 'user': 'barney', 'age': 36 }
];

// Sort by `user` in ascending order and by `age` in descending order.
_.orderBy(users, ['user', 'age'], ['asc', 'desc']);
// => objects for [['barney', 36], ['barney', 34], ['fred', 48], ['fred', 40]]
```

---

### `_.partition(collection, [predicate=_.identity])`

创建一个元素数组，这些元素被分成两组。第一组包含 `predicate` 返回真值的元素，第二组包含 `predicate` 返回假值的元素。

**起始版本**
3.0.0

**参数**

| Name | Type | Description |
|---|---|---|
| `collection` | `Array`\|`Object` | 要遍历的集合。 |
| `[predicate=_.identity]` | `Function` | 每次迭代时调用的函数。 |

**返回值**

`(Array)`: 返回分组后的元素数组。

**示例**

```javascript
var users = [
  { 'user': 'barney',  'age': 36, 'active': false },
  { 'user': 'fred',    'age': 40, 'active': true },
  { 'user': 'pebbles', 'age': 1,  'active': false }
];

_.partition(users, function(o) { return o.active; });
// => objects for [['fred'], ['barney', 'pebbles']]

// The `_.property` iteratee shorthand.
_.partition(users, 'active');
// => objects for [['fred'], ['barney', 'pebbles']]
```

---

### `_.reduce(collection, [iteratee=_.identity], [accumulator])`

将 `collection` 归约为一个值，该值是通过对 `collection` 中的每个元素运行 `iteratee` 的累积结果。每次连续调用都会提供上一次的返回值。如果未提供 `accumulator`，则使用 `collection` 的第一个元素作为初始值。迭代函数调用时会传入四个参数：`(accumulator, value, index|key, collection)`。

**起始版本**
0.1.0

**参数**

| Name | Type | Description |
|---|---|---|
| `collection` | `Array`\|`Object` | 要遍历的集合。 |
| `[iteratee=_.identity]` | `Function` | 每次迭代时调用的函数。 |
| `[accumulator]` | `*` | 初始值。 |

**返回值**

`(*)`: 返回累积的值。

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
// => { '1': ['a', 'c'], '2': ['b'] } (iteration order is not guaranteed)
```

---

### `_.reduceRight(collection, [iteratee=_.identity], [accumulator])`

此方法类似于 `_.reduce`，只是它从右到左遍历 `collection` 的元素。

**起始版本**
0.1.0

**参数**

| Name | Type | Description |
|---|---|---|
| `collection` | `Array`\|`Object` | 要遍历的集合。 |
| `[iteratee=_.identity]` | `Function` | 每次迭代时调用的函数。 |
| `[accumulator]` | `*` | 初始值。 |

**返回值**

`(*)`: 返回累积的值。

**示例**

```javascript
var array = [[0, 1], [2, 3], [4, 5]];

_.reduceRight(array, function(flattened, other) {
  return flattened.concat(other);
}, []);
// => [4, 5, 2, 3, 0, 1]
```

---

### `_.reject(collection, [predicate=_.identity])`

`_.filter` 的反向方法；此方法返回 `predicate` **不**返回真值的 `collection` 元素。

**起始版本**
0.1.0

**参数**

| Name | Type | Description |
|---|---|---|
| `collection` | `Array`\|`Object` | 要遍历的集合。 |
| `[predicate=_.identity]` | `Function` | 每次迭代时调用的函数。 |

**返回值**

`(Array)`: 返回新的已过滤数组。

**示例**

```javascript
var users = [
  { 'user': 'barney', 'age': 36, 'active': false },
  { 'user': 'fred',   'age': 40, 'active': true }
];

_.reject(users, function(o) { return !o.active; });
// => objects for ['fred']

// The `_.property` iteratee shorthand.
_.reject(users, 'active');
// => objects for ['barney']
```

---

### `_.sample(collection)`

从 `collection` 中获取一个随机元素。

**起始版本**
2.0.0

**参数**

| Name | Type | Description |
|---|---|---|
| `collection` | `Array`\|`Object` | 要从中采样的集合。 |

**返回值**

`(*)`: 返回随机元素。

**示例**

```javascript
_.sample([1, 2, 3, 4]);
// => 2
```

---

### `_.sampleSize(collection, [n=1])`

从 `collection` 中获取 `n` 个具有唯一键的随机元素，最多为 `collection` 的大小。

**起始版本**
4.0.0

**参数**

| Name | Type | Description |
|---|---|---|
| `collection` | `Array`\|`Object` | 要从中采样的集合。 |
| `[n=1]` | `number` | 要采样的元素数量。 |

**返回值**

`(Array)`: 返回随机元素。

**示例**

```javascript
_.sampleSize([1, 2, 3], 2);
// => [3, 1]

_.sampleSize([1, 2, 3], 4);
// => [2, 3, 1]
```

---

### `_.shuffle(collection)`

使用 [Fisher-Yates shuffle](https://en.wikipedia.org/wiki/Fisher-Yates_shuffle) 的一个版本创建一个包含已打乱值的数组。

**起始版本**
0.1.0

**参数**

| Name | Type | Description |
|---|---|---|
| `collection` | `Array`\|`Object` | 要打乱的集合。 |

**返回值**

`(Array)`: 返回新的已打乱数组。

**示例**

```javascript
_.shuffle([1, 2, 3, 4]);
// => [4, 1, 3, 2]
```

---

### `_.size(collection)`

获取 `collection` 的大小，对于类数组值，返回其长度；对于对象，返回其自身可枚举的字符串键属性的数量。

**起始版本**
0.1.0

**参数**

| Name | Type | Description |
|---|---|---|
| `collection` | `Array`\|`Object`\|`string` | 要检查的集合。 |

**返回值**

`(number)`: 返回集合大小。

**示例**

```javascript
_.size([1, 2, 3]);
// => 3

_.size({ 'a': 1, 'b': 2 });
// => 2

_.size('pebbles');
// => 7
```

---

### `_.some(collection, [predicate=_.identity])`

检查 `predicate` 是否对 `collection` 的**任何**元素返回真值。一旦 `predicate` 返回真值，迭代就会停止。

**起始版本**
0.1.0

**参数**

| Name | Type | Description |
|---|---|---|
| `collection` | `Array`\|`Object` | 要遍历的集合。 |
| `[predicate=_.identity]` | `Function` | 每次迭代时调用的函数。 |

**返回值**

`(boolean)`: 如果有任何元素通过断言检查，则返回 `true`，否则返回 `false`。

**示例**

```javascript
_.some([null, 0, 'yes', false], Boolean);
// => true

var users = [
  { 'user': 'barney', 'active': true },
  { 'user': 'fred',   'active': false }
];

// The `_.matchesProperty` iteratee shorthand.
_.some(users, ['active', false]);
// => true
```

---

### `_.sortBy(collection, [iteratees=[_.identity]])`

创建一个元素数组，该数组根据对集合中的每个元素运行每个迭代函数的结果进行升序排序。此方法执行稳定排序，这意味着它会保留相等元素的原始排序顺序。

**起始版本**
0.1.0

**参数**

| Name | Type | Description |
|---|---|---|
| `collection` | `Array`\|`Object` | 要遍历的集合。 |
| `[iteratees=[_.identity]]` | `...(Function|Function[])` | 用于排序的迭代函数。 |

**返回值**

`(Array)`: 返回新的已排序数组。

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
