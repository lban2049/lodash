# Collection

Collection functions are designed to iterate over and manipulate collections of data, which in Lodash can be either arrays or objects. These methods provide powerful tools for filtering, mapping, grouping, and reducing data, regardless of its underlying structure. For functions specific to arrays or objects, see the [Array](./api-array.md) and [Object](./api-object.md) sections.

## Methods

| Method | Description |
|---|---|
| [`_.countBy`](#_countbycollection-iteratee__identity) | Creates an object composed of keys generated from running each element of a collection through an iteratee. The corresponding value of each key is the number of times the key was returned. |
| [`_.every`](#_everycollection-predicate__identity) | Checks if the predicate returns truthy for all elements of the collection. |
| [`_.filter`](#_filtercollection-predicate__identity) | Iterates over elements of a collection, returning an array of all elements the predicate returns truthy for. |
| [`_.find`](#_findcollection-predicate__identity-fromindex0) | Iterates over elements of a collection, returning the first element the predicate returns truthy for. |
| [`_.findLast`](#_findlastcollection-predicate__identity-fromindexcollectionlength-1) | This method is like `_.find` except that it iterates over elements of a collection from right to left. |
| [`_.flatMap`](#_flatmapcollection-iteratee__identity) | Creates a flattened array of values by running each element in the collection through an iteratee and flattening the mapped results. |
| [`_.flatMapDeep`](#_flatmapdeepcollection-iteratee__identity) | This method is like `_.flatMap` except that it recursively flattens the mapped results. |
| [`_.flatMapDepth`](#_flatmapdepthcollection-iteratee__identity-depth1) | This method is like `_.flatMap` except that it recursively flattens the mapped results up to a specified depth. |
| [`_.forEach`](#_foreachcollection-iteratee__identity) | Iterates over elements of a collection and invokes the iteratee for each element. Alias: `_.each`. |
| [`_.forEachRight`](#_foreachrightcollection-iteratee__identity) | This method is like `_.forEach` except that it iterates over elements of a collection from right to left. Alias: `_.eachRight`. |
| [`_.groupBy`](#_groupbycollection-iteratee__identity) | Creates an object composed of keys generated from running each element of a collection through an iteratee. The order of grouped values is determined by the order they occur in the collection. |
| [`_.includes`](#_includescollection-value-fromindex0) | Checks if a value is in a collection. |
| [`_.invokeMap`](#_invokemapcollection-path-args) | Invokes the method at a specified path for each element in the collection. |
| [`_.keyBy`](#_keybycollection-iteratee__identity) | Creates an object composed of keys generated from running each element of a collection through an iteratee. The corresponding value of each key is the last element responsible for generating the key. |
| [`_.map`](#_mapcollection-iteratee__identity) | Creates an array of values by running each element in the collection through an iteratee. |
| [`_.orderBy`](#_orderbycollection-iteratees_identity-orders) | This method is like `_.sortBy` except that it allows specifying the sort orders of the iteratees to sort by. |
| [`_.partition`](#_partitioncollection-predicate__identity) | Creates an array of elements split into two groups, the first of which contains elements the predicate returns truthy for, the second of which contains elements the predicate returns falsey for. |
| [`_.reduce`](#_reducecollection-iteratee__identity-accumulator) | Reduces a collection to a value which is the accumulated result of running each element in the collection through an iteratee. |
| [`_.reduceRight`](#_reducerightcollection-iteratee__identity-accumulator) | This method is like `_.reduce` except that it iterates over elements of a collection from right to left. |
| [`_.reject`](#_rejectcollection-predicate__identity) | The opposite of `_.filter`; this method returns the elements of a collection that the predicate does not return truthy for. |
| [`_.sample`](#_samplecollection) | Gets a random element from a collection. |
| [`_.sampleSize`](#_samplesizecollection-n1) | Gets `n` random elements at unique keys from a collection up to the size of the collection. |
| [`_.shuffle`](#_shufflecollection) | Creates an array of shuffled values, using a version of the Fisher-Yates shuffle. |
| [`_.size`](#_sizecollection) | Gets the size of a collection by returning its length for array-like values or the number of own enumerable string keyed properties for objects. |
| [`_.some`](#_somecollection-predicate__identity) | Checks if the predicate returns truthy for any element of the collection. |
| [`_.sortBy`](#_sortbycollection-iteratees_identity) | Creates an array of elements, sorted in ascending order by the results of running each element in a collection through each iteratee. |

---

### _.countBy(collection, [iteratee=_.identity])

Creates an object composed of keys generated from running each element of `collection` through an `iteratee`. The value for each key is the count of elements that produced that key.

**Arguments**

| Argument | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | The collection to iterate over. |
| `[iteratee=_.identity]` | `Function` | The function invoked per iteration to generate the key. |

**Returns**

(`Object`): Returns the composed aggregate object.

**Example**

```javascript
_.countBy([6.1, 4.2, 6.3], Math.floor);
// => { '4': 1, '6': 2 }

// Using the _.property iteratee shorthand.
_.countBy(['one', 'two', 'three'], 'length');
// => { '3': 2, '5': 1 }
```

### _.every(collection, [predicate=_.identity])

Checks if `predicate` returns truthy for **all** elements of `collection`. Iteration is stopped once `predicate` returns a falsey value.

**Arguments**

| Argument | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | The collection to iterate over. |
| `[predicate=_.identity]` | `Function` | The function invoked per iteration. |

**Returns**

(`boolean`): Returns `true` if all elements pass the predicate check, else `false`.

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

### _.filter(collection, [predicate=_.identity])

Iterates over elements of `collection`, returning an array of all elements `predicate` returns truthy for. 

**Arguments**

| Argument | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | The collection to iterate over. |
| `[predicate=_.identity]` | `Function` | The function invoked per iteration. |

**Returns**

(`Array`): Returns the new filtered array.

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

### _.find(collection, [predicate=_.identity], [fromIndex=0])

Iterates over elements of `collection`, returning the first element `predicate` returns truthy for.

**Arguments**

| Argument | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | The collection to inspect. |
| `[predicate=_.identity]` | `Function` | The function invoked per iteration. |
| `[fromIndex=0]` | `number` | The index to search from. |

**Returns**

(`*`): Returns the matched element, else `undefined`.

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

### _.findLast(collection, [predicate=_.identity], [fromIndex=collection.length-1])

This method is like `_.find` except that it iterates over elements of `collection` from right to left.

**Arguments**

| Argument | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | The collection to inspect. |
| `[predicate=_.identity]` | `Function` | The function invoked per iteration. |
| `[fromIndex=collection.length-1]` | `number` | The index to search from. |

**Returns**

(`*`): Returns the matched element, else `undefined`.

**Example**

```javascript
_.findLast([1, 2, 3, 4], function(n) {
  return n % 2 == 1;
});
// => 3
```

### _.flatMap(collection, [iteratee=_.identity])

Creates a flattened array of values by running each element in `collection` through `iteratee` and flattening the mapped results a single level deep.

**Arguments**

| Argument | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | The collection to iterate over. |
| `[iteratee=_.identity]` | `Function` | The function invoked per iteration. |

**Returns**

(`Array`): Returns the new flattened array.

**Example**

```javascript
function duplicate(n) {
  return [n, n];
}

_.flatMap([1, 2], duplicate);
// => [1, 1, 2, 2]
```

### _.flatMapDeep(collection, [iteratee=_.identity])

This method is like `_.flatMap` except that it recursively flattens the mapped results.

**Arguments**

| Argument | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | The collection to iterate over. |
| `[iteratee=_.identity]` | `Function` | The function invoked per iteration. |

**Returns**

(`Array`): Returns the new flattened array.

**Example**

```javascript
function duplicate(n) {
  return [[[n, n]]];
}

_.flatMapDeep([1, 2], duplicate);
// => [1, 1, 2, 2]
```

### _.flatMapDepth(collection, [iteratee=_.identity], [depth=1])

This method is like `_.flatMap` except that it recursively flattens the mapped results up to `depth` times.

**Arguments**

| Argument | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | The collection to iterate over. |
| `[iteratee=_.identity]` | `Function` | The function invoked per iteration. |
| `[depth=1]` | `number` | The maximum recursion depth. |

**Returns**

(`Array`): Returns the new flattened array.

**Example**

```javascript
function duplicate(n) {
  return [[[n, n]]];
}

_.flatMapDepth([1, 2], duplicate, 2);
// => [[1, 1], [2, 2]]
```

### _.forEach(collection, [iteratee=_.identity])

Iterates over elements of `collection` and invokes `iteratee` for each element. The iteratee may exit iteration early by explicitly returning `false`. Alias: `_.each`.

**Arguments**

| Argument | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | The collection to iterate over. |
| `[iteratee=_.identity]` | `Function` | The function invoked per iteration. |

**Returns**

(`Array` or `Object`): Returns `collection`.

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

### _.forEachRight(collection, [iteratee=_.identity])

This method is like `_.forEach` except that it iterates over elements of `collection` from right to left. Alias: `_.eachRight`.

**Arguments**

| Argument | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | The collection to iterate over. |
| `[iteratee=_.identity]` | `Function` | The function invoked per iteration. |

**Returns**

(`Array` or `Object`): Returns `collection`.

**Example**

```javascript
_.forEachRight([1, 2], function(value) {
  console.log(value);
});
// => Logs `2` then `1`.
```

### _.groupBy(collection, [iteratee=_.identity])

Creates an object composed of keys generated from the results of running each element of `collection` through `iteratee`. The value of each key is an array of elements responsible for generating the key.

**Arguments**

| Argument | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | The collection to iterate over. |
| `[iteratee=_.identity]` | `Function` | The iteratee to transform keys. |

**Returns**

(`Object`): Returns the composed aggregate object.

**Example**

```javascript
_.groupBy([6.1, 4.2, 6.3], Math.floor);
// => { '4': [4.2], '6': [6.1, 6.3] }

// The `_.property` iteratee shorthand.
_.groupBy(['one', 'two', 'three'], 'length');
// => { '3': ['one', 'two'], '5': ['three'] }
```

### _.includes(collection, value, [fromIndex=0])

Checks if `value` is in `collection`. If `collection` is a string, it's checked for a substring of `value`. If `fromIndex` is negative, it's used as the offset from the end of `collection`.

**Arguments**

| Argument | Type | Description |
|---|---|---|
| `collection` | `Array`, `Object`, or `string` | The collection to inspect. |
| `value` | `*` | The value to search for. |
| `[fromIndex=0]` | `number` | The index to search from. |

**Returns**

(`boolean`): Returns `true` if `value` is found, else `false`.

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

### _.invokeMap(collection, path, [args])

Invokes the method at `path` of each element in `collection`, returning an array of the results. Additional arguments are provided to each invoked method.

**Arguments**

| Argument | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | The collection to iterate over. |
| `path` | `Array`, `Function`, or `string` | The path of the method to invoke or the function invoked per iteration. |
| `[args]` | `...*` | The arguments to invoke each method with. |

**Returns**

(`Array`): Returns the array of results.

**Example**

```javascript
_.invokeMap([[5, 1, 7], [3, 2, 1]], 'sort');
// => [[1, 5, 7], [1, 2, 3]]

_.invokeMap([123, 456], String.prototype.split, '');
// => [['1', '2', '3'], ['4', '5', '6']]
```

### _.keyBy(collection, [iteratee=_.identity])

Creates an object composed of keys generated from running each element of `collection` through `iteratee`. The corresponding value of each key is the last element responsible for generating the key.

**Arguments**

| Argument | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | The collection to iterate over. |
| `[iteratee=_.identity]` | `Function` | The iteratee to transform keys. |

**Returns**

(`Object`): Returns the composed aggregate object.

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

### _.map(collection, [iteratee=_.identity])

Creates an array of values by running each element in `collection` through `iteratee`.

**Arguments**

| Argument | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | The collection to iterate over. |
| `[iteratee=_.identity]` | `Function` | The function invoked per iteration. |

**Returns**

(`Array`): Returns the new mapped array.

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

### _.orderBy(collection, [iteratees=[_.identity]], [orders])

This method is like `_.sortBy` except that it allows specifying the sort orders for the iteratees. If `orders` is unspecified, all values are sorted in ascending order. Otherwise, specify an order of `'desc'` for descending or `'asc'` for ascending.

**Arguments**

| Argument | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | The collection to iterate over. |
| `[iteratees=[_.identity]]` | `Array[]`, `Function[]`, `Object[]`, or `string[]` | The iteratees to sort by. |
| `[orders]` | `string[]` | The sort orders of `iteratees`. |

**Returns**

(`Array`): Returns the new sorted array.

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

### _.partition(collection, [predicate=_.identity])

Creates an array of elements split into two groups. The first group contains elements for which `predicate` returns true, the second group contains elements for which it returns false.

**Arguments**

| Argument | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | The collection to iterate over. |
| `[predicate=_.identity]` | `Function` | The function invoked per iteration. |

**Returns**

(`Array`): Returns the array of grouped elements.

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

### _.reduce(collection, [iteratee=_.identity], [accumulator])

Reduces `collection` to a value by running each element through `iteratee`. The iteratee's return value is the accumulated value for the next iteration. If `accumulator` is not given, the first element of `collection` is used as the initial value.

**Arguments**

| Argument | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | The collection to iterate over. |
| `[iteratee=_.identity]` | `Function` | The function invoked per iteration. |
| `[accumulator]` | `*` | The initial value. |

**Returns**

(`*`): Returns the accumulated value.

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

### _.reduceRight(collection, [iteratee=_.identity], [accumulator])

This method is like `_.reduce` except that it iterates over elements of `collection` from right to left.

**Arguments**

| Argument | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | The collection to iterate over. |
| `[iteratee=_.identity]` | `Function` | The function invoked per iteration. |
| `[accumulator]` | `*` | The initial value. |

**Returns**

(`*`): Returns the accumulated value.

**Example**

```javascript
var array = [[0, 1], [2, 3], [4, 5]];

_.reduceRight(array, function(flattened, other) {
  return flattened.concat(other);
}, []);
// => [4, 5, 2, 3, 0, 1]
```

### _.reject(collection, [predicate=_.identity])

The opposite of `_.filter`; this method returns the elements of `collection` that `predicate` does **not** return truthy for.

**Arguments**

| Argument | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | The collection to iterate over. |
| `[predicate=_.identity]` | `Function` | The function invoked per iteration. |

**Returns**

(`Array`): Returns the new filtered array.

**Example**

```javascript
var users = [
  { 'user': 'barney', 'age': 36, 'active': false },
  { 'user': 'fred',   'age': 40, 'active': true }
];

_.reject(users, function(o) { return !o.active; });
// => objects for ['fred']
```

### _.sample(collection)

Gets a random element from `collection`.

**Arguments**

| Argument | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | The collection to sample. |

**Returns**

(`*`): Returns the random element.

**Example**

```javascript
_.sample([1, 2, 3, 4]);
// => 2
```

### _.sampleSize(collection, [n=1])

Gets `n` random elements from `collection`.

**Arguments**

| Argument | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | The collection to sample. |
| `[n=1]` | `number` | The number of elements to sample. |

**Returns**

(`Array`): Returns the random elements.

**Example**

```javascript
_.sampleSize([1, 2, 3], 2);
// => [3, 1]

_.sampleSize([1, 2, 3], 4);
// => [2, 3, 1]
```

### _.shuffle(collection)

Creates an array of shuffled values, using a version of the [Fisher-Yates shuffle](https://en.wikipedia.org/wiki/Fisher-Yates_shuffle).

**Arguments**

| Argument | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | The collection to shuffle. |

**Returns**

(`Array`): Returns the new shuffled array.

**Example**

```javascript
_.shuffle([1, 2, 3, 4]);
// => [4, 1, 3, 2]
```

### _.size(collection)

Gets the size of `collection` by returning its length for array-like values or the number of own enumerable string keyed properties for objects.

**Arguments**

| Argument | Type | Description |
|---|---|---|
| `collection` | `Array`, `Object`, or `string` | The collection to inspect. |

**Returns**

(`number`): Returns the collection size.

**Example**

```javascript
_.size([1, 2, 3]);
// => 3

_.size({ 'a': 1, 'b': 2 });
// => 2

_.size('pebbles');
// => 7
```

### _.some(collection, [predicate=_.identity])

Checks if `predicate` returns truthy for **any** element of `collection`. Iteration is stopped once `predicate` returns a truthy value.

**Arguments**

| Argument | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | The collection to iterate over. |
| `[predicate=_.identity]` | `Function` | The function invoked per iteration. |

**Returns**

(`boolean`): Returns `true` if any element passes the predicate check, else `false`.

**Example**

```javascript
_.some([null, 0, 'yes', false], Boolean);
// => true

var users = [
  { 'user': 'barney', 'active': true },
  { 'user': 'fred',   'active': false }
];

// The `_.property` iteratee shorthand.
_.some(users, 'active');
// => true
```

### _.sortBy(collection, [iteratees=[_.identity]])

Creates an array of elements, sorted in ascending order by the results of running each element in a collection through each iteratee. This method performs a stable sort.

**Arguments**

| Argument | Type | Description |
|---|---|---|
| `collection` | `Array` or `Object` | The collection to iterate over. |
| `[iteratees=[_.identity]]` | `...(Function|Function[])` | The iteratees to sort by. |

**Returns**

(`Array`): Returns the new sorted array.

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

---

This section covers the essential functions for working with collections. For more specialized operations, you may want to explore the [Array](./api-array.md) or [Object](./api-object.md) API sections.