# Collection

集合（Collection）函数适用于可迭代的数据结构，如数组、对象和字符串。这些函数提供了一致的方法来遍历、筛选、映射和分组元素，无论底层的数据类型是什么。

这些工具是 Lodash 的核心，能够以声明式和富有表现力的方式处理数据。对于专门针对数组或对象的操作，请分别参阅 [Array](./api-array.md) 和 [Object](./api-object.md) 部分的文档。

## 函数列表

### `countBy`

创建一个由键生成的对象，这些键是通过对 `collection` 中的每个元素运行 `iteratee` 函数得出的。每个键对应的值是 `iteratee` 返回该键的次数。

- **版本**: 0.5.0
- **参数**:
  - `collection` (Array|Object): 要迭代的集合。
  - `iteratee` (Function): 用于转换键的函数，每次迭代时调用。
- **返回**: (Object): 聚合后的对象。

**示例**

```javascript
_.countBy([6.1, 4.2, 6.3], Math.floor);
// => { '4': 1, '6': 2 }

// 使用 _.property 速记法
_.countBy(['one', 'two', 'three'], 'length');
// => { '3': 2, '5': 1 }
```

### `every`

检查 `collection` 中的所有元素是否都通过 `predicate` 函数的真值测试。一旦 `predicate` 返回假值，迭代就会停止。

- **版本**: 0.1.0
- **参数**:
  - `collection` (Array|Object): 要迭代的集合。
  - `predicate` (Function): 每次迭代时调用的函数。
- **返回**: (boolean): 如果所有元素都通过了真值测试，则返回 `true`，否则返回 `false`。

**示例**

```javascript
_.every([true, 1, null, 'yes'], Boolean);
// => false

var users = [
  { 'user': 'barney', 'age': 36, 'active': false },
  { 'user': 'fred',   'age': 40, 'active': false }
];

// 使用 _.matches 速记法
_.every(users, { 'user': 'barney', 'active': false });
// => false

// 使用 _.matchesProperty 速记法
_.every(users, ['active', false]);
// => true

// 使用 _.property 速记法
_.every(users, 'active');
// => false
```

### `filter`

遍历 `collection` 的元素，返回一个包含所有 `predicate` 函数返回真值的元素的新数组。

- **版本**: 0.1.0
- **参数**:
  - `collection` (Array|Object): 要迭代的集合。
  - `predicate` (Function): 每次迭代时调用的函数。
- **返回**: (Array): 包含通过筛选的元素的新数组。
- **相关**: `reject`

**示例**

```javascript
var users = [
  { 'user': 'barney', 'age': 36, 'active': true },
  { 'user': 'fred',   'age': 40, 'active': false }
];

_.filter(users, function(o) { return !o.active; });
// => objects for ['fred']

// 使用 _.matches 速记法
_.filter(users, { 'age': 36, 'active': true });
// => objects for ['barney']
```

### `find`

遍历 `collection` 的元素，返回第一个 `predicate` 函数返回真值的元素。`predicate` 被调用时会传入三个参数：(value, index|key, collection)。

- **版本**: 0.1.0
- **参数**:
  - `collection` (Array|Object): 要检查的集合。
  - `predicate` (Function): 每次迭代时调用的函数。
  - `fromIndex` (number): 开始搜索的索引，默认为 `0`。
- **返回**: (*): 匹配的元素，如果未找到则返回 `undefined`。

**示例**

```javascript
var users = [
  { 'user': 'barney',  'age': 36, 'active': true },
  { 'user': 'fred',    'age': 40, 'active': false },
  { 'user': 'pebbles', 'age': 1,  'active': true }
];

_.find(users, function(o) { return o.age < 40; });
// => object for 'barney'

// 使用 _.matches 速记法
_.find(users, { 'age': 1, 'active': true });
// => object for 'pebbles'
```

### `findLast`

此方法类似于 `_.find`，但它是从右到左遍历 `collection` 的元素。

- **版本**: 2.0.0
- **参数**:
  - `collection` (Array|Object): 要检查的集合。
  - `predicate` (Function): 每次迭代时调用的函数。
  - `fromIndex` (number): 开始搜索的索引，默认为 `collection.length - 1`。
- **返回**: (*): 匹配的元素，如果未找到则返回 `undefined`。

**示例**

```javascript
_.findLast([1, 2, 3, 4], function(n) {
  return n % 2 == 1;
});
// => 3
```

### `flatMap`

通过对 `collection` 中的每个元素运行 `iteratee` 函数，并将映射结果展平一级，来创建一个展平后的数组。

- **版本**: 4.0.0
- **参数**:
  - `collection` (Array|Object): 要迭代的集合。
  - `iteratee` (Function): 每次迭代时调用的函数。
- **返回**: (Array): 新的展平后的数组。

**示例**

```javascript
function duplicate(n) {
  return [n, n];
}

_.flatMap([1, 2], duplicate);
// => [1, 1, 2, 2]
```

### `flatMapDeep`

此方法类似于 `_.flatMap`，不同之处在于它会递归地展平映射结果。

- **版本**: 4.7.0
- **参数**:
  - `collection` (Array|Object): 要迭代的集合。
  - `iteratee` (Function): 每次迭代时调用的函数。
- **返回**: (Array): 新的展平后的数组。

**示例**

```javascript
function duplicate(n) {
  return [[[n, n]]];
}

_.flatMapDeep([1, 2], duplicate);
// => [1, 1, 2, 2]
```

### `flatMapDepth`

此方法类似于 `_.flatMap`，不同之处在于它会根据指定的 `depth` 递归地展平映射结果。

- **版本**: 4.7.0
- **参数**:
  - `collection` (Array|Object): 要迭代的集合。
  - `iteratee` (Function): 每次迭代时调用的函数。
  - `depth` (number): 递归展平的最大深度，默认为 `1`。
- **返回**: (Array): 新的展平后的数组。

**示例**

```javascript
function duplicate(n) {
  return [[[n, n]]];
}

_.flatMapDepth([1, 2], duplicate, 2);
// => [[1, 1], [2, 2]]
```

### `forEach`

为 `collection` 中的每个元素调用 `iteratee` 函数。`iteratee` 函数可以通过显式返回 `false` 来提前退出迭代。

- **版本**: 0.1.0
- **别名**: `each`
- **参数**:
  - `collection` (Array|Object): 要迭代的集合。
  - `iteratee` (Function): 每次迭代时调用的函数。
- **返回**: (Array|Object): 返回 `collection`。

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

### `forEachRight`

此方法类似于 `_.forEach`，但它是从右到左遍历 `collection` 的元素。

- **版本**: 2.0.0
- **别名**: `eachRight`
- **参数**:
  - `collection` (Array|Object): 要迭代的集合。
  - `iteratee` (Function): 每次迭代时调用的函数。
- **返回**: (Array|Object): 返回 `collection`。

**示例**

```javascript
_.forEachRight([1, 2], function(value) {
  console.log(value);
});
// => Logs `2` then `1`.
```

### `groupBy`

创建一个由键生成的对象，这些键是通过对 `collection` 中的每个元素运行 `iteratee` 函数得出的。每个键对应的值是一个数组，包含生成该键的元素。

- **版本**: 0.1.0
- **参数**:
  - `collection` (Array|Object): 要迭代的集合。
  - `iteratee` (Function): 用于转换键的函数。
- **返回**: (Object): 聚合后的对象。

**示例**

```javascript
_.groupBy([6.1, 4.2, 6.3], Math.floor);
// => { '4': [4.2], '6': [6.1, 6.3] }

// 使用 _.property 速记法
_.groupBy(['one', 'two', 'three'], 'length');
// => { '3': ['one', 'two'], '5': ['three'] }
```

### `includes`

检查 `value` 是否在 `collection` 中。如果 `collection` 是字符串，则检查 `value` 是否为其子字符串；否则，使用 `SameValueZero` 进行相等性比较。如果指定了 `fromIndex`，则从该索引开始搜索。

- **版本**: 0.1.0
- **参数**:
  - `collection` (Array|Object|string): 要检查的集合。
  - `value` (*): 要搜索的值。
  - `fromIndex` (number): 开始搜索的索引，默认为 `0`。
- **返回**: (boolean): 如果找到 `value`，则返回 `true`，否则返回 `false`。

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

### `invokeMap`

对 `collection` 中的每个元素调用 `path` 指定的方法，并返回每次调用结果组成的数组。任何附加参数都会传递给每次调用的方法。

- **版本**: 4.0.0
- **参数**:
  - `collection` (Array|Object): 要迭代的集合。
  - `path` (Array|Function|string): 要调用的方法路径或每次迭代调用的函数。
  - `...args`: 传递给每个方法的参数。
- **返回**: (Array): 结果数组。

**示例**

```javascript
_.invokeMap([[5, 1, 7], [3, 2, 1]], 'sort');
// => [[1, 5, 7], [1, 2, 3]]

_.invokeMap([123, 456], String.prototype.split, '');
// => [['1', '2', '3'], ['4', '5', '6']]
```

### `keyBy`

创建一个由键生成的对象，这些键是通过对 `collection` 中的每个元素运行 `iteratee` 函数得出的。每个键对应的值是最后一次生成该键的元素。

- **版本**: 4.0.0
- **参数**:
  - `collection` (Array|Object): 要迭代的集合。
  - `iteratee` (Function): 用于转换键的函数。
- **返回**: (Object): 聚合后的对象。

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

### `map`

通过对 `collection` 中的每个元素运行 `iteratee` 函数，创建一个新数组。

- **版本**: 0.1.0
- **参数**:
  - `collection` (Array|Object): 要迭代的集合。
  - `iteratee` (Function): 每次迭代时调用的函数。
- **返回**: (Array): 新的映射后的数组。

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

// 使用 _.property 速记法
_.map(users, 'user');
// => ['barney', 'fred']
```

### `orderBy`

此方法类似于 `_.sortBy`，但允许指定 `iteratees` 的排序顺序。如果未指定 `orders`，则所有值都按升序排序。否则，为相应的值指定 `desc` 表示降序，`asc` 表示升序。

- **版本**: 4.0.0
- **参数**:
  - `collection` (Array|Object): 要迭代的集合。
  - `iteratees` (Array[]|Function[]|Object[]|string[]): 用于排序的迭代器，默认为 `[_.identity]`。
  - `orders` (string[]): `iteratees` 的排序顺序。
- **返回**: (Array): 新的排序后的数组。

**示例**

```javascript
var users = [
  { 'user': 'fred',   'age': 48 },
  { 'user': 'barney', 'age': 34 },
  { 'user': 'fred',   'age': 40 },
  { 'user': 'barney', 'age': 36 }
];

// 按 'user' 升序，'age' 降序排序
_.orderBy(users, ['user', 'age'], ['asc', 'desc']);
// => objects for [['barney', 36], ['barney', 34], ['fred', 48], ['fred', 40]]
```

### `partition`

创建一个元素数组，分为两组。第一组包含 `predicate` 返回真值的元素，第二组包含 `predicate` 返回假值的元素。

- **版本**: 3.0.0
- **参数**:
  - `collection` (Array|Object): 要迭代的集合。
  - `predicate` (Function): 每次迭代时调用的函数。
- **返回**: (Array): 分组后的元素数组。

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

### `reduce`

将 `collection` 归约为一个值，该值是运行 `collection` 中每个元素通过 `iteratee` 函数的累积结果。`iteratee` 会传入四个参数：(accumulator, value, index|key, collection)。

- **版本**: 0.1.0
- **参数**:
  - `collection` (Array|Object): 要迭代的集合。
  - `iteratee` (Function): 每次迭代时调用的函数。
  - `accumulator` (*): 初始值。
- **返回**: (*): 累积后的值。

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

### `reduceRight`

此方法类似于 `_.reduce`，但它是从右到左遍历 `collection` 的元素。

- **版本**: 0.1.0
- **参数**:
  - `collection` (Array|Object): 要迭代的集合。
  - `iteratee` (Function): 每次迭代时调用的函数。
  - `accumulator` (*): 初始值。
- **返回**: (*): 累积后的值。

**示例**

```javascript
var array = [[0, 1], [2, 3], [4, 5]];

_.reduceRight(array, function(flattened, other) {
  return flattened.concat(other);
}, []);
// => [4, 5, 2, 3, 0, 1]
```

### `reject`

`_.filter` 的反向方法；此方法返回 `predicate` 函数不返回真值的 `collection` 元素。

- **版本**: 0.1.0
- **参数**:
  - `collection` (Array|Object): 要迭代的集合。
  - `predicate` (Function): 每次迭代时调用的函数。
- **返回**: (Array): 新的筛选后的数组。

**示例**

```javascript
var users = [
  { 'user': 'barney', 'age': 36, 'active': false },
  { 'user': 'fred',   'age': 40, 'active': true }
];

_.reject(users, function(o) { return !o.active; });
// => objects for ['fred']
```

### `sample`

从 `collection` 中获取一个随机元素。

- **版本**: 2.0.0
- **参数**:
  - `collection` (Array|Object): 要采样的集合。
- **返回**: (*): 随机元素。

**示例**

```javascript
_.sample([1, 2, 3, 4]);
// => 2
```

### `sampleSize`

从 `collection` 中获取 `n` 个随机的唯一元素。

- **版本**: 4.0.0
- **参数**:
  - `collection` (Array|Object): 要采样的集合。
  - `n` (number): 要采样的元素数量，默认为 `1`。
- **返回**: (Array): 随机元素组成的数组。

**示例**

```javascript
_.sampleSize([1, 2, 3], 2);
// => [3, 1]

_.sampleSize([1, 2, 3], 4);
// => [2, 3, 1]
```

### `shuffle`

创建一个使用 Fisher-Yates shuffle 算法打乱值的数组。

- **版本**: 0.1.0
- **参数**:
  - `collection` (Array|Object): 要打乱的集合。
- **返回**: (Array): 新的打乱后的数组。

**示例**

```javascript
_.shuffle([1, 2, 3, 4]);
// => [4, 1, 3, 2]
```

### `size`

获取 `collection` 的大小。对于类数组值，返回其长度；对于对象，返回其自身可枚举的字符串键属性的数量。

- **版本**: 0.1.0
- **参数**:
  - `collection` (Array|Object|string): 要检查的集合。
- **返回**: (number): 集合的大小。

**示例**

```javascript
_.size([1, 2, 3]);
// => 3

_.size({ 'a': 1, 'b': 2 });
// => 2

_.size('pebbles');
// => 7
```

### `some`

检查 `collection` 中是否有任何元素通过 `predicate` 函数的真值测试。一旦 `predicate` 返回真值，迭代就会停止。

- **版本**: 0.1.0
- **参数**:
  - `collection` (Array|Object): 要迭代的集合。
  - `predicate` (Function): 每次迭代时调用的函数。
- **返回**: (boolean): 如果有任何元素通过了真值测试，则返回 `true`，否则返回 `false`。

**示例**

```javascript
_.some([null, 0, 'yes', false], Boolean);
// => true

var users = [
  { 'user': 'barney', 'active': true },
  { 'user': 'fred',   'active': false }
];

// 使用 _.matches 速记法
_.some(users, { 'user': 'barney', 'active': false });
// => false
```

### `sortBy`

创建一个元素数组，按升序排序，排序依据是对 `collection` 中的每个元素运行每个 `iteratee` 函数的结果。此方法执行稳定排序。

- **版本**: 0.1.0
- **参数**:
  - `collection` (Array|Object): 要迭代的集合。
  - `...iteratees` (Function|Function[]): 用于排序的迭代器。
- **返回**: (Array): 新的排序后的数组。

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

现在您已经熟悉了处理集合的函数，可以继续探索 [Function](./api-function.md) 部分，学习如何操作和增强函数。