# Collection

Lodash provides a rich set of functions for working with collections, which can be either arrays or objects. These functions allow you to iterate, filter, group, sort, and transform data in a consistent and powerful way. For methods specific to arrays or objects, see the [Array](./api-array.md) and [Object](./api-object.md) sections.

---

### countBy

Creates an object composed of keys generated from the results of running each element of `collection` through `iteratee`. The corresponding value of each key is the number of times the key was returned by `iteratee`. The iteratee is invoked with one argument: `(value)`.

**Syntax**
```typescript
_.countBy(collection, [iteratee=_.identity])
```

**Arguments**
| Name | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | The collection to iterate over. |
| `[iteratee=_.identity]` | `Function` | The iteratee to transform keys. |

**Returns**
- `(Object)`: Returns the composed aggregate object.

**Example**
```javascript
_.countBy([6.1, 4.2, 6.3], Math.floor);
// => { '4': 1, '6': 2 }

// The `_.property` iteratee shorthand.
_.countBy(['one', 'two', 'three'], 'length');
// => { '3': 2, '5': 1 }
```

---

### every

Checks if `predicate` returns truthy for **all** elements of `collection`. Iteration is stopped once `predicate` returns falsey. The predicate is invoked with three arguments: `(value, index|key, collection)`.

**Note:** This method returns `true` for [empty collections](https://en.wikipedia.org/wiki/Empty_set) because [everything is true](https://en.wikipedia.org/wiki/Vacuous_truth) of elements of empty collections.

**Syntax**
```typescript
_.every(collection, [predicate=_.identity])
```

**Arguments**
| Name | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | The collection to iterate over. |
| `[predicate=_.identity]` | `Function` | The function invoked per iteration. |

**Returns**
- `(boolean)`: Returns `true` if all elements pass the predicate check, else `false`.

**Example**
```javascript
_.every([true, 1, null, 'yes'], Boolean);
// => false

var users = [
  { 'user': 'barney', 'age': 36, 'active': false },
  { 'user': 'fred',   'age': 40, 'active': false }
];

// The `_.matchesProperty` iteratee shorthand.
_.every(users, ['active', false]);
// => true
```

---

### filter

Iterates over elements of `collection`, returning an array of all elements `predicate` returns truthy for. The predicate is invoked with three arguments: `(value, index|key, collection)`.

**Syntax**
```typescript
_.filter(collection, [predicate=_.identity])
```

**Arguments**
| Name | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | The collection to iterate over. |
| `[predicate=_.identity]` | `Function` | The function invoked per iteration. |

**Returns**
- `(Array)`: Returns the new filtered array.

**Example**
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

### find

Iterates over elements of `collection`, returning the first element `predicate` returns truthy for. The predicate is invoked with three arguments: `(value, index|key, collection)`.

**Syntax**
```typescript
_.find(collection, [predicate=_.identity], [fromIndex=0])
```

**Arguments**
| Name | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | The collection to inspect. |
| `[predicate=_.identity]` | `Function` | The function invoked per iteration. |
| `[fromIndex=0]` | `number` | The index to search from. |

**Returns**
- `(*)`: Returns the matched element, else `undefined`.

**Example**
```javascript
var users = [
  { 'user': 'barney',  'age': 36, 'active': true },
  { 'user': 'fred',    'age': 40, 'active': false },
  { 'user': 'pebbles', 'age': 1,  'active': true }
];

_.find(users, function(o) { return o.age < 40; });
// => object for 'barney'

// The `_.property` iteratee shorthand.
_.find(users, 'active');
// => object for 'barney'
```

---

### findLast

This method is like `_.find` except that it iterates over elements of `collection` from right to left.

**Syntax**
```typescript
_.findLast(collection, [predicate=_.identity], [fromIndex=collection.length-1])
```

**Arguments**
| Name | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | The collection to inspect. |
| `[predicate=_.identity]` | `Function` | The function invoked per iteration. |
| `[fromIndex=collection.length-1]` | `number` | The index to search from. |

**Returns**
- `(*)`: Returns the matched element, else `undefined`.

**Example**
```javascript
_.findLast([1, 2, 3, 4], function(n) {
  return n % 2 == 1;
});
// => 3
```

---

### flatMap

Creates a flattened array of values by running each element in `collection` through `iteratee` and flattening the mapped results. The iteratee is invoked with three arguments: `(value, index|key, collection)`.

**Syntax**
```typescript
_.flatMap(collection, [iteratee=_.identity])
```

**Arguments**
| Name | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | The collection to iterate over. |
| `[iteratee=_.identity]` | `Function` | The function invoked per iteration. |

**Returns**
- `(Array)`: Returns the new flattened array.

**Example**
```javascript
function duplicate(n) {
  return [n, n];
}

_.flatMap([1, 2], duplicate);
// => [1, 1, 2, 2]
```

---

### flatMapDeep

This method is like `_.flatMap` except that it recursively flattens the mapped results.

**Syntax**
```typescript
_.flatMapDeep(collection, [iteratee=_.identity])
```

**Arguments**
| Name | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | The collection to iterate over. |
| `[iteratee=_.identity]` | `Function` | The function invoked per iteration. |

**Returns**
- `(Array)`: Returns the new flattened array.

**Example**
```javascript
function duplicate(n) {
  return [[[n, n]]];
}

_.flatMapDeep([1, 2], duplicate);
// => [1, 1, 2, 2]
```

---

### flatMapDepth

This method is like `_.flatMap` except that it recursively flattens the mapped results up to `depth` times.

**Syntax**
```typescript
_.flatMapDepth(collection, [iteratee=_.identity], [depth=1])
```

**Arguments**
| Name | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | The collection to iterate over. |
| `[iteratee=_.identity]` | `Function` | The function invoked per iteration. |
| `[depth=1]` | `number` | The maximum recursion depth. |

**Returns**
- `(Array)`: Returns the new flattened array.

**Example**
```javascript
function duplicate(n) {
  return [[[n, n]]];
}

_.flatMapDepth([1, 2], duplicate, 2);
// => [[1, 1], [2, 2]]
```

---

### forEach (each)

Iterates over elements of `collection` and invokes `iteratee` for each element. The iteratee is invoked with three arguments: `(value, index|key, collection)`. Iteratee functions may exit iteration early by explicitly returning `false`.

**Syntax**
```typescript
_.forEach(collection, [iteratee=_.identity])
```

**Arguments**
| Name | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | The collection to iterate over. |
| `[iteratee=_.identity]` | `Function` | The function invoked per iteration. |

**Returns**
- `(Array|Object)`: Returns `collection`.

**Example**
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

This method is like `_.forEach` except that it iterates over elements of `collection` from right to left.

**Syntax**
```typescript
_.forEachRight(collection, [iteratee=_.identity])
```

**Arguments**
| Name | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | The collection to iterate over. |
| `[iteratee=_.identity]` | `Function` | The function invoked per iteration. |

**Returns**
- `(Array|Object)`: Returns `collection`.

**Example**
```javascript
_.forEachRight([1, 2], function(value) {
  console.log(value);
});
// => Logs `2` then `1`.
```

---

### groupBy

Creates an object composed of keys generated from the results of running each element of `collection` through `iteratee`. The order of grouped values is determined by the order they occur in `collection`. The corresponding value of each key is an array of elements responsible for generating the key.

**Syntax**
```typescript
_.groupBy(collection, [iteratee=_.identity])
```

**Arguments**
| Name | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | The collection to iterate over. |
| `[iteratee=_.identity]` | `Function` | The iteratee to transform keys. |

**Returns**
- `(Object)`: Returns the composed aggregate object.

**Example**
```javascript
_.groupBy([6.1, 4.2, 6.3], Math.floor);
// => { '4': [4.2], '6': [6.1, 6.3] }

// The `_.property` iteratee shorthand.
_.groupBy(['one', 'two', 'three'], 'length');
// => { '3': ['one', 'two'], '5': ['three'] }
```

---

### includes

Checks if `value` is in `collection`. If `collection` is a string, it's checked for a substring of `value`, otherwise [`SameValueZero`](http://ecma-international.org/ecma-262/7.0/#sec-samevaluezero) is used for equality comparisons. If `fromIndex` is negative, it's used as the offset from the end of `collection`.

**Syntax**
```typescript
_.includes(collection, value, [fromIndex=0])
```

**Arguments**
| Name | Type | Description |
|---|---|---|
| `collection` | `Array`, `Object`, or `string` | The collection to inspect. |
| `value` | `*` | The value to search for. |
| `[fromIndex=0]` | `number` | The index to search from. |

**Returns**
- `(boolean)`: Returns `true` if `value` is found, else `false`.

**Example**
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

Invokes the method at `path` of each element in `collection`, returning an array of the results of each invoked method. Any additional arguments are provided to each invoked method. If `path` is a function, it's invoked for, and `this` bound to, each element in `collection`.

**Syntax**
```typescript
_.invokeMap(collection, path, [args])
```

**Arguments**
| Name | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | The collection to iterate over. |
| `path` | `Array`, `Function`, or `string` | The path of the method to invoke or the function invoked per iteration. |
| `[args]` | `...*` | The arguments to invoke each method with. |

**Returns**
- `(Array)`: Returns the array of results.

**Example**
```javascript
_.invokeMap([[5, 1, 7], [3, 2, 1]], 'sort');
// => [[1, 5, 7], [1, 2, 3]]

_.invokeMap([123, 456], String.prototype.split, '');
// => [['1', '2', '3'], ['4', '5', '6']]
```

---

### keyBy

Creates an object composed of keys generated from the results of running each element of `collection` through `iteratee`. The corresponding value of each key is the last element responsible for generating the key.

**Syntax**
```typescript
_.keyBy(collection, [iteratee=_.identity])
```

**Arguments**
| Name | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | The collection to iterate over. |
| `[iteratee=_.identity]` | `Function` | The iteratee to transform keys. |

**Returns**
- `(Object)`: Returns the composed aggregate object.

**Example**
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

Creates an array of values by running each element in `collection` through `iteratee`. The iteratee is invoked with three arguments: `(value, index|key, collection)`.

**Syntax**
```typescript
_.map(collection, [iteratee=_.identity])
```

**Arguments**
| Name | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | The collection to iterate over. |
| `[iteratee=_.identity]` | `Function` | The function invoked per iteration. |

**Returns**
- `(Array)`: Returns the new mapped array.

**Example**
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

This method is like `_.sortBy` except that it allows specifying the sort orders of the iteratees to sort by. If `orders` is unspecified, all values are sorted in ascending order. Otherwise, specify an order of `'desc'` for descending or `'asc'` for ascending sort order of corresponding values.

**Syntax**
```typescript
_.orderBy(collection, [iteratees=[_.identity]], [orders])
```

**Arguments**
| Name | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | The collection to iterate over. |
| `[iteratees=[_.identity]]` | `(Array[]|Function[]|Object[]|string[])` | The iteratees to sort by. |
| `[orders]` | `string[]` | The sort orders of `iteratees`. |

**Returns**
- `(Array)`: Returns the new sorted array.

**Example**
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

Creates an array of elements split into two groups, the first of which contains elements `predicate` returns truthy for, the second of which contains elements `predicate` returns falsey for. The predicate is invoked with one argument: `(value)`.

**Syntax**
```typescript
_.partition(collection, [predicate=_.identity])
```

**Arguments**
| Name | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | The collection to iterate over. |
| `[predicate=_.identity]` | `Function` | The function invoked per iteration. |

**Returns**
- `(Array)`: Returns the array of grouped elements.

**Example**
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

Reduces `collection` to a value which is the accumulated result of running each element in `collection` through `iteratee`, where each successive invocation is supplied the return value of the previous. If `accumulator` is not given, the first element of `collection` is used as the initial value. The iteratee is invoked with four arguments: `(accumulator, value, index|key, collection)`.

**Syntax**
```typescript
_.reduce(collection, [iteratee=_.identity], [accumulator])
```

**Arguments**
| Name | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | The collection to iterate over. |
| `[iteratee=_.identity]` | `Function` | The function invoked per iteration. |
| `[accumulator]` | `*` | The initial value. |

**Returns**
- `(*)`: Returns the accumulated value.

**Example**
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

This method is like `_.reduce` except that it iterates over elements of `collection` from right to left.

**Syntax**
```typescript
_.reduceRight(collection, [iteratee=_.identity], [accumulator])
```

**Arguments**
| Name | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | The collection to iterate over. |
| `[iteratee=_.identity]` | `Function` | The function invoked per iteration. |
| `[accumulator]` | `*` | The initial value. |

**Returns**
- `(*)`: Returns the accumulated value.

**Example**
```javascript
var array = [[0, 1], [2, 3], [4, 5]];

_.reduceRight(array, function(flattened, other) {
  return flattened.concat(other);
}, []);
// => [4, 5, 2, 3, 0, 1]
```

---

### reject

The opposite of `_.filter`; this method returns the elements of `collection` that `predicate` does **not** return truthy for.

**Syntax**
```typescript
_.reject(collection, [predicate=_.identity])
```

**Arguments**
| Name | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | The collection to iterate over. |
| `[predicate=_.identity]` | `Function` | The function invoked per iteration. |

**Returns**
- `(Array)`: Returns the new filtered array.

**Example**
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

Gets a random element from `collection`.

**Syntax**
```typescript
_.sample(collection)
```

**Arguments**
| Name | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | The collection to sample. |

**Returns**
- `(*)`: Returns the random element.

**Example**
```javascript
_.sample([1, 2, 3, 4]);
// => 2
```

---

### sampleSize

Gets `n` random elements at unique keys from `collection` up to the size of `collection`.

**Syntax**
```typescript
_.sampleSize(collection, [n=1])
```

**Arguments**
| Name | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | The collection to sample. |
| `[n=1]` | `number` | The number of elements to sample. |

**Returns**
- `(Array)`: Returns the random elements.

**Example**
```javascript
_.sampleSize([1, 2, 3], 2);
// => [3, 1]

_.sampleSize([1, 2, 3], 4);
// => [2, 3, 1]
```

---

### shuffle

Creates an array of shuffled values, using a version of the [Fisher-Yates shuffle](https://en.wikipedia.org/wiki/Fisher-Yates_shuffle).

**Syntax**
```typescript
_.shuffle(collection)
```

**Arguments**
| Name | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | The collection to shuffle. |

**Returns**
- `(Array)`: Returns the new shuffled array.

**Example**
```javascript
_.shuffle([1, 2, 3, 4]);
// => [4, 1, 3, 2]
```

---

### size

Gets the size of `collection` by returning its length for array-like values or the number of own enumerable string keyed properties for objects.

**Syntax**
```typescript
_.size(collection)
```

**Arguments**
| Name | Type | Description |
|---|---|---|
| `collection` | `Array`, `Object`, or `string` | The collection to inspect. |

**Returns**
- `(number)`: Returns the collection size.

**Example**
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

Checks if `predicate` returns truthy for **any** element of `collection`. Iteration is stopped once `predicate` returns truthy.

**Syntax**
```typescript
_.some(collection, [predicate=_.identity])
```

**Arguments**
| Name | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | The collection to iterate over. |
| `[predicate=_.identity]` | `Function` | The function invoked per iteration. |

**Returns**
- `(boolean)`: Returns `true` if any element passes the predicate check, else `false`.

**Example**
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

### sortBy

Creates an array of elements, sorted in ascending order by the results of running each element in a collection through each iteratee. This method performs a stable sort, meaning it preserves the original sort order of equal elements.

**Syntax**
```typescript
_.sortBy(collection, [iteratees=[_.identity]])
```

**Arguments**
| Name | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | The collection to iterate over. |
| `[iteratees=[_.identity]]` | `...(Function|Function[])` | The iteratees to sort by. |

**Returns**
- `(Array)`: Returns the new sorted array.

**Example**
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
