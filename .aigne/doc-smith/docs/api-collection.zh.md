# 集合

Lodash 提供了一套丰富的函数，用于处理集合（可以是数组或对象）。这些函数使你能够以一致且强大的方式对数据进行迭代、筛选、分组、排序和转换。有关专门用于数组或对象的方法，请参阅 [Array](./api-array.md) 和 [Object](./api-object.md) 部分。

---

### countBy

通过 `iteratee` 处理 `collection` 中的每个元素，创建一个由生成的结果作为键的对象。每个键对应的值是 `iteratee` 返回该键的次数。iteratee 调用时会传入一个参数：`(value)`。

**语法**
```typescript
_.countBy(collection, [iteratee=_.identity])
```

**参数**
| Name | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | 要迭代的集合。 |
| `[iteratee=_.identity]` | `Function` | 用于转换键的迭代函数。 |

**返回值**
- `(Object)`: 返回组合的聚合对象。

**示例**
```javascript
_.countBy([6.1, 4.2, 6.3], Math.floor);
// => { '4': 1, '6': 2 }

// `_.property` iteratee 的简写形式。
_.countBy(['one', 'two', 'three'], 'length');
// => { '3': 2, '5': 1 }
```

---

### every

检查 `predicate` 是否对 `collection` 的**所有**元素都返回真值。一旦 `predicate` 返回假值，迭代就会停止。predicate 调用时会传入三个参数：`(value, index|key, collection)`。

**注意：** 此方法对[空集合](https://en.wikipedia.org/wiki/Empty_set)返回 `true`，因为[空集合中的所有元素都为真](https://en.wikipedia.org/wiki/Vacuous_truth)。

**语法**
```typescript
_.every(collection, [predicate=_.identity])
```

**参数**
| Name | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | 要迭代的集合。 |
| `[predicate=_.identity]` | `Function` | 每次迭代调用的函数。 |

**返回值**
- `(boolean)`: 如果所有元素都通过谓词检查，则返回 `true`，否则返回 `false`。

**示例**
```javascript
_.every([true, 1, null, 'yes'], Boolean);
// => false

var users = [
  { 'user': 'barney', 'age': 36, 'active': false },
  { 'user': 'fred',   'age': 40, 'active': false }
];

// `_.matchesProperty` iteratee 的简写形式。
_.every(users, ['active', false]);
// => true
```

---

### filter

遍历 `collection` 的元素，返回一个数组，包含所有 `predicate` 返回真值的元素。predicate 调用时会传入三个参数：`(value, index|key, collection)`。

**语法**
```typescript
_.filter(collection, [predicate=_.identity])
```

**参数**
| Name | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | 要迭代的集合。 |
| `[predicate=_.identity]` | `Function` | 每次迭代调用的函数。 |

**返回值**
- `(Array)`: 返回新的已筛选数组。

**示例**
```javascript
var users = [
  { 'user': 'barney', 'age': 36, 'active': true },
  { 'user': 'fred',   'age': 40, 'active': false }
];

_.filter(users, function(o) { return !o.active; });
// => objects for ['fred']

// `_.matches` iteratee 的简写形式。
_.filter(users, { 'age': 36, 'active': true });
// => objects for ['barney']
```

---

### find

遍历 `collection` 的元素，返回 `predicate` 返回真值的第一个元素。predicate 调用时会传入三个参数：`(value, index|key, collection)`。

**语法**
```typescript
_.find(collection, [predicate=_.identity], [fromIndex=0])
```

**参数**
| Name | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | 要检查的集合。 |
| `[predicate=_.identity]` | `Function` | 每次迭代调用的函数。 |
| `[fromIndex=0]` | `number` | 开始搜索的索引。 |

**返回值**
- `(*)`: 返回匹配的元素，否则返回 `undefined`。

**示例**
```javascript
var users = [
  { 'user': 'barney',  'age': 36, 'active': true },
  { 'user': 'fred',    'age': 40, 'active': false },
  { 'user': 'pebbles', 'age': 1,  'active': true }
];

_.find(users, function(o) { return o.age < 40; });
// => object for 'barney'

// `_.property` iteratee 的简写形式。
_.find(users, 'active');
// => object for 'barney'
```

---

### findLast

此方法类似于 `_.find`，区别在于它从右到左遍历 `collection` 的元素。

**语法**
```typescript
_.findLast(collection, [predicate=_.identity], [fromIndex=collection.length-1])
```

**参数**
| Name | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | 要检查的集合。 |
| `[predicate=_.identity]` | `Function` | 每次迭代调用的函数。 |
| `[fromIndex=collection.length-1]` | `number` | 开始搜索的索引。 |

**返回值**
- `(*)`: 返回匹配的元素，否则返回 `undefined`。

**示例**
```javascript
_.findLast([1, 2, 3, 4], function(n) {
  return n % 2 == 1;
});
// => 3
```

---

### flatMap

通过 `iteratee` 运行 `collection` 中的每个元素并展平映射结果，从而创建一个新的扁平化数组。iteratee 调用时会传入三个参数：`(value, index|key, collection)`。

**语法**
```typescript
_.flatMap(collection, [iteratee=_.identity])
```

**参数**
| Name | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | 要迭代的集合。 |
| `[iteratee=_.identity]` | `Function` | 每次迭代调用的函数。 |

**返回值**
- `(Array)`: 返回新的扁平化数组。

**示例**
```javascript
function duplicate(n) {
  return [n, n];
}

_.flatMap([1, 2], duplicate);
// => [1, 1, 2, 2]
```

---

### flatMapDeep

此方法类似于 `_.flatMap`，区别在于它会递归地展平映射结果。

**语法**
```typescript
_.flatMapDeep(collection, [iteratee=_.identity])
```

**参数**
| Name | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | 要迭代的集合。 |
| `[iteratee=_.identity]` | `Function` | 每次迭代调用的函数。 |

**返回值**
- `(Array)`: 返回新的扁平化数组。

**示例**
```javascript
function duplicate(n) {
  return [[[n, n]]];
}

_.flatMapDeep([1, 2], duplicate);
// => [1, 1, 2, 2]
```

---

### flatMapDepth

此方法类似于 `_.flatMap`，区别在于它会根据 `depth` 的深度递归地展平映射结果。

**语法**
```typescript
_.flatMapDepth(collection, [iteratee=_.identity], [depth=1])
```

**参数**
| Name | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | 要迭代的集合。 |
| `[iteratee=_.identity]` | `Function` | 每次迭代调用的函数。 |
| `[depth=1]` | `number` | 最大递归深度。 |

**返回值**
- `(Array)`: 返回新的扁平化数组。

**示例**
```javascript
function duplicate(n) {
  return [[[n, n]]];
}

_.flatMapDepth([1, 2], duplicate, 2);
// => [[1, 1], [2, 2]]
```

---

### forEach (each)

遍历 `collection` 的元素，并为每个元素调用 `iteratee`。iteratee 调用时会传入三个参数：`(value, index|key, collection)`。Iteratee 函数可以通过显式返回 `false` 来提前退出迭代。

**语法**
```typescript
_.forEach(collection, [iteratee=_.identity])
```

**参数**
| Name | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | 要迭代的集合。 |
| `[iteratee=_.identity]` | `Function` | 每次迭代调用的函数。 |

**返回值**
- `(Array|Object)`: 返回 `collection`。

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

### forEachRight (eachRight)

此方法类似于 `_.forEach`，区别在于它从右到左遍历 `collection` 的元素。

**语法**
```typescript
_.forEachRight(collection, [iteratee=_.identity])
```

**参数**
| Name | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | 要迭代的集合。 |
| `[iteratee=_.identity]` | `Function` | 每次迭代调用的函数。 |

**返回值**
- `(Array|Object)`: 返回 `collection`。

**示例**
```javascript
_.forEachRight([1, 2], function(value) {
  console.log(value);
});
// => Logs `2` then `1`.
```

---

### groupBy

通过 `iteratee` 处理 `collection` 中的每个元素，创建一个由生成的结果作为键的对象。分组值的顺序由它们在 `collection` 中出现的顺序决定。每个键对应的值是一个数组，其中包含所有生成该键的元素。

**语法**
```typescript
_.groupBy(collection, [iteratee=_.identity])
```

**参数**
| Name | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | 要迭代的集合。 |
| `[iteratee=_.identity]` | `Function` | 用于转换键的迭代函数。 |

**返回值**
- `(Object)`: 返回组合的聚合对象。

**示例**
```javascript
_.groupBy([6.1, 4.2, 6.3], Math.floor);
// => { '4': [4.2], '6': [6.1, 6.3] }

// `_.property` iteratee 的简写形式。
_.groupBy(['one', 'two', 'three'], 'length');
// => { '3': ['one', 'two'], '5': ['three'] }
```

---

### includes

检查 `value` 是否在 `collection` 中。如果 `collection` 是一个字符串，则检查其是否包含 `value` 子字符串，否则使用 [`SameValueZero`](http://ecma-international.org/ecma-262/7.0/#sec-samevaluezero) 进行等值比较。如果 `fromIndex` 为负数，则将其用作从 `collection` 末尾开始的偏移量。

**语法**
```typescript
_.includes(collection, value, [fromIndex=0])
```

**参数**
| Name | Type | Description |
|---|---|---|
| `collection` | `Array`, `Object`, or `string` | 要检查的集合。 |
| `value` | `*` | 要搜索的值。 |
| `[fromIndex=0]` | `number` | 开始搜索的索引。 |

**返回值**
- `(boolean)`: 如果找到 `value`，则返回 `true`，否则返回 `false`。

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

### invokeMap

调用 `collection` 中每个元素的 `path` 路径上的方法，返回一个包含每次调用结果的数组。任何附加参数都会提供给每个被调用的方法。如果 `path` 是一个函数，它将被调用并绑定 `this` 到 `collection` 中的每个元素。

**语法**
```typescript
_.invokeMap(collection, path, [args])
```

**参数**
| Name | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | 要迭代的集合。 |
| `path` | `Array`, `Function`, or `string` | 要调用的方法的路径，或每次迭代调用的函数。 |
| `[args]` | `...*` | 调用每个方法时传入的参数。 |

**返回值**
- `(Array)`: 返回结果数组。

**示例**
```javascript
_.invokeMap([[5, 1, 7], [3, 2, 1]], 'sort');
// => [[1, 5, 7], [1, 2, 3]]

_.invokeMap([123, 456], String.prototype.split, '');
// => [['1', '2', '3'], ['4', '5', '6']]
```

---

### keyBy

通过 `iteratee` 处理 `collection` 中的每个元素，创建一个由生成的结果作为键的对象。每个键对应的值是最后一个生成该键的元素。

**语法**
```typescript
_.keyBy(collection, [iteratee=_.identity])
```

**参数**
| Name | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | 要迭代的集合。 |
| `[iteratee=_.identity]` | `Function` | 用于转换键的迭代函数。 |

**返回值**
- `(Object)`: 返回组合的聚合对象。

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

### map

通过 `iteratee` 运行 `collection` 中的每个元素，创建一个新数组。iteratee 调用时会传入三个参数：`(value, index|key, collection)`。

**语法**
```typescript
_.map(collection, [iteratee=_.identity])
```

**参数**
| Name | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | 要迭代的集合。 |
| `[iteratee=_.identity]` | `Function` | 每次迭代调用的函数。 |

**返回值**
- `(Array)`: 返回新的映射后数组。

**示例**
```javascript
function square(n) {
  return n * n;
}

_.map([4, 8], square);
// => [16, 64]

_.map({ 'a': 4, 'b': 8 }, square);
// => [16, 64] (iteration order is not guaranteed)
```

---

### orderBy

此方法类似于 `_.sortBy`，区别在于它允许指定用于排序的 iteratees 的排序顺序。如果未指定 `orders`，则所有值都按升序排序。否则，为相应的值指定 `'desc'`（降序）或 `'asc'`（升序）的排序顺序。

**语法**
```typescript
_.orderBy(collection, [iteratees=[_.identity]], [orders])
```

**参数**
| Name | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | 要迭代的集合。 |
| `[iteratees=[_.identity]]` | `(Array[]|Function[]|Object[]|string[])` | 用于排序的迭代函数。 |
| `[orders]` | `string[]` | `iteratees` 的排序顺序。 |

**返回值**
- `(Array)`: 返回新的已排序数组。

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

### partition

创建一个元素数组，分为两组：第一组包含 `predicate` 返回真值的元素，第二组包含 `predicate` 返回假值的元素。predicate 调用时会传入一个参数：`(value)`。

**语法**
```typescript
_.partition(collection, [predicate=_.identity])
```

**参数**
| Name | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | 要迭代的集合。 |
| `[predicate=_.identity]` | `Function` | 每次迭代调用的函数。 |

**返回值**
- `(Array)`: 返回分组后的元素数组。

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

---

### reduce

将 `collection` 归约为一个值，该值是通过 `iteratee` 遍历 `collection` 中每个元素并累积计算的结果，每次连续的调用都会提供上一次的返回值。如果未提供 `accumulator`，则使用 `collection` 的第一个元素作为初始值。iteratee 调用时会传入四个参数：`(accumulator, value, index|key, collection)`。

**语法**
```typescript
_.reduce(collection, [iteratee=_.identity], [accumulator])
```

**参数**
| Name | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | 要迭代的集合。 |
| `[iteratee=_.identity]` | `Function` | 每次迭代调用的函数。 |
| `[accumulator]` | `*` | 初始值。 |

**返回值**
- `(*)`: 返回累积值。

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

### reduceRight

此方法类似于 `_.reduce`，区别在于它从右到左遍历 `collection` 的元素。

**语法**
```typescript
_.reduceRight(collection, [iteratee=_.identity], [accumulator])
```

**参数**
| Name | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | 要迭代的集合。 |
| `[iteratee=_.identity]` | `Function` | 每次迭代调用的函数。 |
| `[accumulator]` | `*` | 初始值。 |

**返回值**
- `(*)`: 返回累积值。

**示例**
```javascript
var array = [[0, 1], [2, 3], [4, 5]];

_.reduceRight(array, function(flattened, other) {
  return flattened.concat(other);
}, []);
// => [4, 5, 2, 3, 0, 1]
```

---

### reject

与 `_.filter` 相反；此方法返回 `collection` 中 `predicate` **不**返回真值的元素。

**语法**
```typescript
_.reject(collection, [predicate=_.identity])
```

**参数**
| Name | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | 要迭代的集合。 |
| `[predicate=_.identity]` | `Function` | 每次迭代调用的函数。 |

**返回值**
- `(Array)`: 返回新的已筛选数组。

**示例**
```javascript
var users = [
  { 'user': 'barney', 'age': 36, 'active': false },
  { 'user': 'fred',   'age': 40, 'active': true }
];

_.reject(users, function(o) { return !o.active; });
// => objects for ['fred']
```

---

### sample

从 `collection` 中获取一个随机元素。

**语法**
```typescript
_.sample(collection)
```

**参数**
| Name | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | 要采样的集合。 |

**返回值**
- `(*)`: 返回随机元素。

**示例**
```javascript
_.sample([1, 2, 3, 4]);
// => 2
```

---

### sampleSize

从 `collection` 中获取 `n` 个随机元素，最多不超过 `collection` 的大小。

**语法**
```typescript
_.sampleSize(collection, [n=1])
```

**参数**
| Name | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | 要采样的集合。 |
| `[n=1]` | `number` | 要采样的元素数量。 |

**返回值**
- `(Array)`: 返回随机元素。

**示例**
```javascript
_.sampleSize([1, 2, 3], 2);
// => [3, 1]

_.sampleSize([1, 2, 3], 4);
// => [2, 3, 1]
```

---

### shuffle

创建一个打乱值的数组，使用 [Fisher-Yates shuffle](https://en.wikipedia.org/wiki/Fisher-Yates_shuffle) 算法的一个版本。

**语法**
```typescript
_.shuffle(collection)
```

**参数**
| Name | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | 要打乱的集合。 |

**返回值**
- `(Array)`: 返回新的已打乱数组。

**示例**
```javascript
_.shuffle([1, 2, 3, 4]);
// => [4, 1, 3, 2]
```

---

### size

获取 `collection` 的大小，对于类数组值，返回其 `length` 属性，对于对象，返回其自身可枚举的字符串键属性的数量。

**语法**
```typescript
_.size(collection)
```

**参数**
| Name | Type | Description |
|---|---|---|
| `collection` | `Array`, `Object`, or `string` | 要检查的集合。 |

**返回值**
- `(number)`: 返回集合的大小。

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

### some

检查 `predicate` 是否对 `collection` 的**任何**元素返回真值。一旦 `predicate` 返回真值，迭代就会停止。

**语法**
```typescript
_.some(collection, [predicate=_.identity])
```

**参数**
| Name | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | 要迭代的集合。 |
| `[predicate=_.identity]` | `Function` | 每次迭代调用的函数。 |

**返回值**
- `(boolean)`: 如果有任何元素通过谓词检查，则返回 `true`，否则返回 `false`。

**示例**
```javascript
_.some([null, 0, 'yes', false], Boolean);
// => true

var users = [
  { 'user': 'barney', 'active': true },
  { 'user': 'fred',   'active': false }
];

// `_.matchesProperty` iteratee 的简写形式。
_.some(users, ['active', false]);
// => true
```

---

### sortBy

创建一个元素数组，根据通过每个 iteratee 运行集合中每个元素的结果进行升序排序。此方法执行稳定排序，这意味着它会保留相等元素的原始排序顺序。

**语法**
```typescript
_.sortBy(collection, [iteratees=[_.identity]])
```

**参数**
| Name | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | 要迭代的集合。 |
| `[iteratees=[_.identity]]` | `...(Function|Function[])` | 用于排序的迭代函数。 |

**返回值**
- `(Array)`: 返回新的已排序数组。

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
