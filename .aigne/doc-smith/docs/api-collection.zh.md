# 集合

集合函数对于遍历和操作数据组（包括数组和对象）至关重要。这些方法提供了强大而简洁的方式来执行过滤、映射和归约等常见操作。

**注意：** 在遍历对象时，Lodash 会将任何带有 `length` 属性的对象视作类数组集合。对于遍历普通对象的属性，建议使用 [Object](./api-object.md) 分类中的函数，例如 `_.forOwn` 或 `_.forIn`。

---

## _.countBy

创建一个由键组成的对象，这些键是通过对 `collection` 的每个元素运行 `iteratee` 的结果生成的。每个键对应的值是 `iteratee` 返回该键的次数。

### 参数

<x-field data-name="collection" data-type="Array|Object" data-required="true" data-desc="要遍历的集合。"></x-field>
<x-field data-name="iteratee" data-type="Function" data-default="_.identity" data-required="false" data-desc="用于转换键的迭代函数。调用时带有一个参数：(value)。"></x-field>

### 返回值

<x-field data-name="" data-type="Object" data-desc="返回组合后的聚合对象。"></x-field>

### 示例

```javascript
_.countBy([6.1, 4.2, 6.3], Math.floor);
// => { '4': 1, '6': 2 }

// `_.property` 迭代器的简写形式。
_.countBy(['one', 'two', 'three'], 'length');
// => { '3': 2, '5': 1 }
```

---

## _.every

检查 `predicate` 是否对 `collection` 的 **所有** 元素都返回真值。一旦 `predicate` 返回假值，遍历就会停止。

**注意：** 此方法对[空集合](https://en.wikipedia.org/wiki/Empty_set)返回 `true`，因为空集合的所有元素都[被认为是真](https://en.wikipedia.org/wiki/Vacuous_truth)。

### 参数

<x-field data-name="collection" data-type="Array|Object" data-required="true" data-desc="要遍历的集合。"></x-field>
<x-field data-name="predicate" data-type="Function" data-default="_.identity" data-required="false" data-desc="每次遍历时调用的函数。它接收三个参数：(value, index|key, collection)。"></x-field>

### 返回值

<x-field data-name="" data-type="boolean" data-desc="如果所有元素都通过谓词检查，则返回 `true`，否则返回 `false`。"></x-field>

### 示例

```javascript
_.every([true, 1, null, 'yes'], Boolean);
// => false

var users = [
  { 'user': 'barney', 'age': 36, 'active': false },
  { 'user': 'fred',   'age': 40, 'active': false }
];

// `_.matches` 迭代器的简写形式。
_.every(users, { 'user': 'barney', 'active': false });
// => false

// `_.matchesProperty` 迭代器的简写形式。
_.every(users, ['active', false]);
// => true

// `_.property` 迭代器的简写形式。
_.every(users, 'active');
// => false
```

---

## _.filter

遍历 `collection` 的元素，返回一个由所有 `predicate` 返回真值的元素组成的新数组。

### 参数

<x-field data-name="collection" data-type="Array|Object" data-required="true" data-desc="要遍历的集合。"></x-field>
<x-field data-name="predicate" data-type="Function" data-default="_.identity" data-required="false" data-desc="每次遍历时调用的函数。它接收三个参数：(value, index|key, collection)。"></x-field>

### 返回值

<x-field data-name="" data-type="Array" data-desc="返回新的已过滤数组。"></x-field>

### 示例

```javascript
var users = [
  { 'user': 'barney', 'age': 36, 'active': true },
  { 'user': 'fred',   'age': 40, 'active': false }
];

_.filter(users, function(o) { return !o.active; });
// => ['fred'] 的对象

// `_.matches` 迭代器的简写形式。
_.filter(users, { 'age': 36, 'active': true });
// => ['barney'] 的对象

// `_.matchesProperty` 迭代器的简写形式。
_.filter(users, ['active', false]);
// => ['fred'] 的对象

// `_.property` 迭代器的简写形式。
_.filter(users, 'active');
// => ['barney'] 的对象
```

---

## _.find

遍历 `collection` 的元素，返回第一个 `predicate` 返回真值的元素。

### 参数

<x-field data-name="collection" data-type="Array|Object" data-required="true" data-desc="要检查的集合。"></x-field>
<x-field data-name="predicate" data-type="Function" data-default="_.identity" data-required="false" data-desc="每次遍历时调用的函数。它接收三个参数：(value, index|key, collection)。"></x-field>
<x-field data-name="fromIndex" data-type="number" data-default="0" data-required="false" data-desc="开始搜索的索引。"></x-field>

### 返回值

<x-field data-name="" data-type="*" data-desc="返回匹配的元素，否则返回 `undefined`。"></x-field>

### 示例

```javascript
var users = [
  { 'user': 'barney',  'age': 36, 'active': true },
  { 'user': 'fred',    'age': 40, 'active': false },
  { 'user': 'pebbles', 'age': 1,  'active': true }
];

_.find(users, function(o) { return o.age < 40; });
// => 'barney' 的对象

// `_.matches` 迭代器的简写形式。
_.find(users, { 'age': 1, 'active': true });
// => 'pebbles' 的对象

// `_.matchesProperty` 迭代器的简写形式。
_.find(users, ['active', false]);
// => 'fred' 的对象

// `_.property` 迭代器的简写形式。
_.find(users, 'active');
// => 'barney' 的对象
```

---

## _.findLast

此方法类似于 `_.find`，只是它从右到左遍历 `collection` 的元素。

### 参数

<x-field data-name="collection" data-type="Array|Object" data-required="true" data-desc="要检查的集合。"></x-field>
<x-field data-name="predicate" data-type="Function" data-default="_.identity" data-required="false" data-desc="每次遍历时调用的函数。"></x-field>
<x-field data-name="fromIndex" data-type="number" data-default="collection.length-1" data-required="false" data-desc="开始搜索的索引。"></x-field>

### 返回值

<x-field data-name="" data-type="*" data-desc="返回匹配的元素，否则返回 `undefined`。"></x-field>

### 示例

```javascript
_.findLast([1, 2, 3, 4], function(n) {
  return n % 2 == 1;
});
// => 3
```

---

## _.flatMap

通过对 `collection` 中的每个元素运行 `iteratee` 并展平映射结果，创建一个已展平的数组。

### 参数

<x-field data-name="collection" data-type="Array|Object" data-required="true" data-desc="要遍历的集合。"></x-field>
<x-field data-name="iteratee" data-type="Function" data-default="_.identity" data-required="false" data-desc="每次遍历时调用的函数。它接收三个参数：(value, index|key, collection)。"></x-field>

### 返回值

<x-field data-name="" data-type="Array" data-desc="返回新的已展平数组。"></x-field>

### 示例

```javascript
function duplicate(n) {
  return [n, n];
}

_.flatMap([1, 2], duplicate);
// => [1, 1, 2, 2]
```

---

## _.flatMapDeep

此方法类似于 `_.flatMap`，只是它会递归地展平映射结果。

### 参数

<x-field data-name="collection" data-type="Array|Object" data-required="true" data-desc="要遍历的集合。"></x-field>
<x-field data-name="iteratee" data-type="Function" data-default="_.identity" data-required="false" data-desc="每次遍历时调用的函数。"></x-field>

### 返回值

<x-field data-name="" data-type="Array" data-desc="返回新的已展平数组。"></x-field>

### 示例

```javascript
function duplicate(n) {
  return [[[n, n]]];
}

_.flatMapDeep([1, 2], duplicate);
// => [1, 1, 2, 2]
```

---

## _.flatMapDepth

此方法类似于 `_.flatMap`，只是它会递归地展平映射结果，最多 `depth` 次。

### 参数

<x-field data-name="collection" data-type="Array|Object" data-required="true" data-desc="要遍历的集合。"></x-field>
<x-field data-name="iteratee" data-type="Function" data-default="_.identity" data-required="false" data-desc="每次遍历时调用的函数。"></x-field>
<x-field data-name="depth" data-type="number" data-default="1" data-required="false" data-desc="最大递归深度。"></x-field>

### 返回值

<x-field data-name="" data-type="Array" data-desc="返回新的已展平数组。"></x-field>

### 示例

```javascript
function duplicate(n) {
  return [[[n, n]]];
}

_.flatMapDepth([1, 2], duplicate, 2);
// => [[1, 1], [2, 2]]
```

---

## _.forEach

遍历 `collection` 的元素，并为每个元素调用 `iteratee`。迭代函数可以通过显式返回 `false` 来提前退出遍历。

### 参数

<x-field data-name="collection" data-type="Array|Object" data-required="true" data-desc="要遍历的集合。"></x-field>
<x-field data-name="iteratee" data-type="Function" data-default="_.identity" data-required="false" data-desc="每次遍历时调用的函数。它接收三个参数：(value, index|key, collection)。"></x-field>

### 返回值

<x-field data-name="" data-type="Array|Object" data-desc="返回 `collection`。"></x-field>

### 示例

```javascript
_.forEach([1, 2], function(value) {
  console.log(value);
});
// => 依次输出 `1` 和 `2`。

_.forEach({ 'a': 1, 'b': 2 }, function(value, key) {
  console.log(key);
});
// => 依次输出 'a' 和 'b'（不保证遍历顺序）。
```

---

## _.forEachRight

此方法类似于 `_.forEach`，只是它从右到左遍历 `collection` 的元素。

### 参数

<x-field data-name="collection" data-type="Array|Object" data-required="true" data-desc="要遍历的集合。"></x-field>
<x-field data-name="iteratee" data-type="Function" data-default="_.identity" data-required="false" data-desc="每次遍历时调用的函数。"></x-field>

### 返回值

<x-field data-name="" data-type="Array|Object" data-desc="返回 `collection`。"></x-field>

### 示例

```javascript
_.forEachRight([1, 2], function(value) {
  console.log(value);
});
// => 依次输出 `2` 和 `1`。
```

---

## _.groupBy

创建一个由键组成的对象，这些键是通过对 `collection` 的每个元素运行 `iteratee` 的结果生成的。分组值的顺序由它们在 `collection` 中出现的顺序决定。每个键对应的值是一个由生成该键的元素组成的数组。

### 参数

<x-field data-name="collection" data-type="Array|Object" data-required="true" data-desc="要遍历的集合。"></x-field>
<x-field data-name="iteratee" data-type="Function" data-default="_.identity" data-required="false" data-desc="用于转换键的迭代函数。"></x-field>

### 返回值

<x-field data-name="" data-type="Object" data-desc="返回组合后的聚合对象。"></x-field>

### 示例

```javascript
_.groupBy([6.1, 4.2, 6.3], Math.floor);
// => { '4': [4.2], '6': [6.1, 6.3] }

// `_.property` 迭代器的简写形式。
_.groupBy(['one', 'two', 'three'], 'length');
// => { '3': ['one', 'two'], '5': ['three'] }
```

---

## _.includes

检查 `value` 是否在 `collection` 中。如果 `collection` 是一个字符串，则检查它是否包含 `value` 子字符串。否则，使用 `SameValueZero` 进行相等性比较。如果 `fromIndex` 为负数，则用作 `collection` 末尾的偏移量。

### 参数

<x-field data-name="collection" data-type="Array|Object|string" data-required="true" data-desc="要检查的集合。"></x-field>
<x-field data-name="value" data-type="*" data-required="true" data-desc="要搜索的值。"></x-field>
<x-field data-name="fromIndex" data-type="number" data-default="0" data-required="false" data-desc="开始搜索的索引。"></x-field>

### 返回值

<x-field data-name="" data-type="boolean" data-desc="如果找到 `value`，则返回 `true`，否则返回 `false`。"></x-field>

### 示例

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

## _.invokeMap

调用 `collection` 中每个元素在 `path` 上的方法，返回一个包含结果的数组。任何额外的参数都会提供给每个被调用的方法。如果 `path` 是一个函数，它会为 `collection` 中的每个元素调用，并将 `this` 绑定到该元素。

### 参数

<x-field data-name="collection" data-type="Array|Object" data-required="true" data-desc="要遍历的集合。"></x-field>
<x-field data-name="path" data-type="Array|Function|string" data-required="true" data-desc="要调用的方法的路径或每次遍历时调用的函数。"></x-field>
<x-field data-name="args" data-type="...*" data-required="false" data-desc="调用每个方法时使用的参数。"></x-field>

### 返回值

<x-field data-name="" data-type="Array" data-desc="返回结果数组。"></x-field>

### 示例

```javascript
_.invokeMap([[5, 1, 7], [3, 2, 1]], 'sort');
// => [[1, 5, 7], [1, 2, 3]]

_.invokeMap([123, 456], String.prototype.split, '');
// => [['1', '2', '3'], ['4', '5', '6']]
```

---

## _.keyBy

创建一个由键组成的对象，这些键是通过对 `collection` 的每个元素运行 `iteratee` 的结果生成的。每个键对应的值是最后一个负责生成该键的元素。

### 参数

<x-field data-name="collection" data-type="Array|Object" data-required="true" data-desc="要遍历的集合。"></x-field>
<x-field data-name="iteratee" data-type="Function" data-default="_.identity" data-required="false" data-desc="用于转换键的迭代函数。"></x-field>

### 返回值

<x-field data-name="" data-type="Object" data-desc="返回组合后的聚合对象。"></x-field>

### 示例

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

## _.map

通过对 `collection` 中的每个元素运行 `iteratee`，创建一个包含值的数组。迭代函数被调用时带有三个参数：`(value, index|key, collection)`。

### 参数

<x-field data-name="collection" data-type="Array|Object" data-required="true" data-desc="要遍历的集合。"></x-field>
<x-field data-name="iteratee" data-type="Function" data-default="_.identity" data-required="false" data-desc="每次遍历时调用的函数。"></x-field>

### 返回值

<x-field data-name="" data-type="Array" data-desc="返回新的映射后数组。"></x-field>

### 示例

```javascript
function square(n) {
  return n * n;
}

_.map([4, 8], square);
// => [16, 64]

_.map({ 'a': 4, 'b': 8 }, square);
// => [16, 64] (不保证遍历顺序)

var users = [
  { 'user': 'barney' },
  { 'user': 'fred' }
];

// `_.property` 迭代器的简写形式。
_.map(users, 'user');
// => ['barney', 'fred']
```

---

## _.orderBy

此方法类似于 `_.sortBy`，只是它允许指定要排序的迭代器的排序顺序。如果未指定 `orders`，则所有值都按升序排序。否则，为相应的值指定 `"desc"` 表示降序，或 `"asc"` 表示升序。

### 参数

<x-field data-name="collection" data-type="Array|Object" data-required="true" data-desc="要遍历的集合。"></x-field>
<x-field data-name="iteratees" data-type="Array[]|Function[]|Object[]|string[]" data-default="[_.identity]" data-required="false" data-desc="用于排序的迭代器。"></x-field>
<x-field data-name="orders" data-type="string[]" data-required="false" data-desc="`iteratees` 的排序顺序。"></x-field>

### 返回值

<x-field data-name="" data-type="Array" data-desc="返回新的已排序数组。"></x-field>

### 示例

```javascript
var users = [
  { 'user': 'fred',   'age': 48 },
  { 'user': 'barney', 'age': 34 },
  { 'user': 'fred',   'age': 40 },
  { 'user': 'barney', 'age': 36 }
];

// 按 `user` 升序排序，按 `age` 降序排序。
_.orderBy(users, ['user', 'age'], ['asc', 'desc']);
// => [['barney', 36], ['barney', 34], ['fred', 48], ['fred', 40]] 的对象
```

---

## _.partition

创建一个元素数组，这些元素被分成两组。第一组包含 `predicate` 返回真值的元素，第二组包含其返回假值的元素。

### 参数

<x-field data-name="collection" data-type="Array|Object" data-required="true" data-desc="要遍历的集合。"></x-field>
<x-field data-name="predicate" data-type="Function" data-default="_.identity" data-required="false" data-desc="每次遍历时调用的函数。"></x-field>

### 返回值

<x-field data-name="" data-type="Array" data-desc="返回分组元素的数组，例如 `[[truthy_elements], [falsey_elements]]`。"></x-field>

### 示例

```javascript
var users = [
  { 'user': 'barney',  'age': 36, 'active': false },
  { 'user': 'fred',    'age': 40, 'active': true },
  { 'user': 'pebbles', 'age': 1,  'active': false }
];

_.partition(users, function(o) { return o.active; });
// => [['fred'], ['barney', 'pebbles']] 的对象

// `_.matches` 迭代器的简写形式。
_.partition(users, { 'age': 1, 'active': false });
// => [['pebbles'], ['barney', 'fred']] 的对象
```

---

## _.reduce

将 `collection` 归约为一个值，该值是通过对 `collection` 中的每个元素运行 `iteratee` 的累积结果。如果未提供 `accumulator`，则使用 `collection` 的第一个元素作为初始值。迭代函数被调用时带有四个参数：`(accumulator, value, index|key, collection)`。

### 参数

<x-field data-name="collection" data-type="Array|Object" data-required="true" data-desc="要遍历的集合。"></x-field>
<x-field data-name="iteratee" data-type="Function" data-default="_.identity" data-required="false" data-desc="每次遍历时调用的函数。"></x-field>
<x-field data-name="accumulator" data-type="*" data-required="false" data-desc="初始值。"></x-field>

### 返回值

<x-field data-name="" data-type="*" data-desc="返回累积的值。"></x-field>

### 示例

```javascript
_.reduce([1, 2], function(sum, n) {
  return sum + n;
}, 0);
// => 3

_.reduce({ 'a': 1, 'b': 2, 'c': 1 }, function(result, value, key) {
  (result[value] || (result[value] = [])).push(key);
  return result;
}, {});
// => { '1': ['a', 'c'], '2': ['b'] } (不保证遍历顺序)
```

---

## _.reduceRight

此方法类似于 `_.reduce`，只是它从右到左遍历 `collection` 的元素。

### 参数

<x-field data-name="collection" data-type="Array|Object" data-required="true" data-desc="要遍历的集合。"></x-field>
<x-field data-name="iteratee" data-type="Function" data-default="_.identity" data-required="false" data-desc="每次遍历时调用的函数。"></x-field>
<x-field data-name="accumulator" data-type="*" data-required="false" data-desc="初始值。"></x-field>

### 返回值

<x-field data-name="" data-type="*" data-desc="返回累积的值。"></x-field>

### 示例

```javascript
var array = [[0, 1], [2, 3], [4, 5]];

_.reduceRight(array, function(flattened, other) {
  return flattened.concat(other);
}, []);
// => [4, 5, 2, 3, 0, 1]
```

---

## _.reject

`_.filter` 的反向操作；此方法返回 `collection` 中 `predicate` **不** 返回真值的元素。

### 参数

<x-field data-name="collection" data-type="Array|Object" data-required="true" data-desc="要遍历的集合。"></x-field>
<x-field data-name="predicate" data-type="Function" data-default="_.identity" data-required="false" data-desc="每次遍历时调用的函数。"></x-field>

### 返回值

<x-field data-name="" data-type="Array" data-desc="返回新的已过滤数组。"></x-field>

### 示例

```javascript
var users = [
  { 'user': 'barney', 'age': 36, 'active': false },
  { 'user': 'fred',   'age': 40, 'active': true }
];

_.reject(users, function(o) { return !o.active; });
// => ['fred'] 的对象

// `_.matches` 迭代器的简写形式。
_.reject(users, { 'age': 40, 'active': true });
// => ['barney'] 的对象
```

---

## _.sample

从 `collection` 中获取一个随机元素。

### 参数

<x-field data-name="collection" data-type="Array|Object" data-required="true" data-desc="要采样的集合。"></x-field>

### 返回值

<x-field data-name="" data-type="*" data-desc="返回随机元素。"></x-field>

### 示例

```javascript
_.sample([1, 2, 3, 4]);
// => 2
```

---

## _.sampleSize

从 `collection` 中获取 `n` 个唯一键上的随机元素，最多为 `collection` 的大小。

### 参数

<x-field data-name="collection" data-type="Array|Object" data-required="true" data-desc="要采样的集合。"></x-field>
<x-field data-name="n" data-type="number" data-default="1" data-required="false" data-desc="要采样的元素数量。"></x-field>

### 返回值

<x-field data-name="" data-type="Array" data-desc="返回随机元素。"></x-field>

### 示例

```javascript
_.sampleSize([1, 2, 3], 2);
// => [3, 1]

_.sampleSize([1, 2, 3], 4);
// => [2, 3, 1]
```

---

## _.shuffle

创建一个经过洗牌的值的数组，使用 [Fisher-Yates 洗牌算法](https://en.wikipedia.org/wiki/Fisher-Yates_shuffle)的一个版本。

### 参数

<x-field data-name="collection" data-type="Array|Object" data-required="true" data-desc="要洗牌的集合。"></x-field>

### 返回值

<x-field data-name="" data-type="Array" data-desc="返回新的已洗牌数组。"></x-field>

### 示例

```javascript
_.shuffle([1, 2, 3, 4]);
// => [4, 1, 3, 2]
```

---

## _.size

获取 `collection` 的大小，对于类数组值返回其长度，对于对象返回其自身可枚举字符串键属性的数量。

### 参数

<x-field data-name="collection" data-type="Array|Object|string" data-required="true" data-desc="要检查的集合。"></x-field>

### 返回值

<x-field data-name="" data-type="number" data-desc="返回集合大小。"></x-field>

### 示例

```javascript
_.size([1, 2, 3]);
// => 3

_.size({ 'a': 1, 'b': 2 });
// => 2

_.size('pebbles');
// => 7
```

---

## _.some

检查 `predicate` 是否对 `collection` 的 **任何** 元素返回真值。一旦 `predicate` 返回真值，遍历就会停止。

### 参数

<x-field data-name="collection" data-type="Array|Object" data-required="true" data-desc="要遍历的集合。"></x-field>
<x-field data-name="predicate" data-type="Function" data-default="_.identity" data-required="false" data-desc="每次遍历时调用的函数。"></x-field>

### 返回值

<x-field data-name="" data-type="boolean" data-desc="如果任何元素通过谓词检查，则返回 `true`，否则返回 `false`。"></x-field>

### 示例

```javascript
_.some([null, 0, 'yes', false], Boolean);
// => true

var users = [
  { 'user': 'barney', 'active': true },
  { 'user': 'fred',   'active': false }
];

// `_.matches` 迭代器的简写形式。
_.some(users, { 'user': 'barney', 'active': false });
// => false

// `_.matchesProperty` 迭代器的简写形式。
_.some(users, ['active', false]);
// => true
```

---

## _.sortBy

创建一个元素数组，按升序排序，排序依据是对集合中的每个元素通过每个迭代器运行的结果。此方法执行稳定排序，这意味着它保留了相等元素的原始排序顺序。

### 参数

<x-field data-name="collection" data-type="Array|Object" data-required="true" data-desc="要遍历的集合。"></x-field>
<x-field data-name="iteratees" data-type="...(Function|Function[])" data-default="[_.identity]" data-required="false" data-desc="用于排序的迭代器。"></x-field>

### 返回值

<x-field data-name="" data-type="Array" data-desc="返回新的已排序数组。"></x-field>

### 示例

```javascript
var users = [
  { 'user': 'fred',   'age': 48 },
  { 'user': 'barney', 'age': 36 },
  { 'user': 'fred',   'age': 30 },
  { 'user': 'barney', 'age': 34 }
];

_.sortBy(users, [function(o) { return o.user; }]);
// => [['barney', 36], ['barney', 34], ['fred', 48], ['fred', 30]] 的对象

_.sortBy(users, ['user', 'age']);
// => [['barney', 34], ['barney', 36], ['fred', 30], ['fred', 48]] 的对象
```