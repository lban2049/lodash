# Collection

Collection functions work on iterable data structures such as arrays, objects, and strings. These functions provide a consistent way to iterate, filter, map, and group elements, regardless of the underlying data type.

These utilities are central to Lodash, enabling data manipulation in a declarative and expressive manner. For operations that specifically target arrays or objects, refer to the documentation in the [Array](./api-array.md) and [Object](./api-object.md) sections, respectively.

## Function List

### `countBy`

Creates an object composed of keys generated from running each element of `collection` thru `iteratee`. The corresponding value of each key is the number of times the key was returned by `iteratee`.

- **Version**: 0.5.0
- **Arguments**:
  - `collection` (Array|Object): The collection to iterate over.
  - `iteratee` (Function): The function invoked per iteration to transform keys.
- **Returns**: (Object): The composed aggregate object.

**Example**

```javascript
_.countBy([6.1, 4.2, 6.3], Math.floor);
// => { '4': 1, '6': 2 }

// The _.property shorthand.
_.countBy(['one', 'two', 'three'], 'length');
// => { '3': 2, '5': 1 }
```

### `every`

Checks if `predicate` returns a truthy value for all elements of `collection`. Iteration is stopped once `predicate` returns a falsy value.

- **Version**: 0.1.0
- **Arguments**:
  - `collection` (Array|Object): The collection to iterate over.
  - `predicate` (Function): The function invoked per iteration.
- **Returns**: (boolean): Returns `true` if all elements pass the truthy test, else `false`.

**Example**

```javascript
_.every([true, 1, null, 'yes'], Boolean);
// => false

var users = [
  { 'user': 'barney', 'age': 36, 'active': false },
  { 'user': 'fred',   'age': 40, 'active': false }
];

// The _.matches shorthand.
_.every(users, { 'user': 'barney', 'active': false });
// => false

// The _.matchesProperty shorthand.
_.every(users, ['active', false]);
// => true

// The _.property shorthand.
_.every(users, 'active');
// => false
```

### `filter`

Iterates over elements of `collection`, returning an array of all elements `predicate` returns truthy for.

- **Version**: 0.1.0
- **Arguments**:
  - `collection` (Array|Object): The collection to iterate over.
  - `predicate` (Function): The function invoked per iteration.
- **Returns**: (Array): The new array of filtered elements.
- **Related**: `reject`

**Example**

```javascript
var users = [
  { 'user': 'barney', 'age': 36, 'active': true },
  { 'user': 'fred',   'age': 40, 'active': false }
];

_.filter(users, function(o) { return !o.active; });
// => objects for ['fred']

// The _.matches shorthand.
_.filter(users, { 'age': 36, 'active': true });
// => objects for ['barney']
```

### `find`

Iterates over elements of `collection`, returning the first element `predicate` returns truthy for. The `predicate` is invoked with three arguments: (value, index|key, collection).

- **Version**: 0.1.0
- **Arguments**:
  - `collection` (Array|Object): The collection to inspect.
  - `predicate` (Function): The function invoked per iteration.
  - `fromIndex` (number): The index to search from, defaults to `0`.
- **Returns**: (*): The matched element, else `undefined`.

**Example**

```javascript
var users = [
  { 'user': 'barney',  'age': 36, 'active': true },
  { 'user': 'fred',    'age': 40, 'active': false },
  { 'user': 'pebbles', 'age': 1,  'active': true }
];

_.find(users, function(o) { return o.age < 40; });
// => object for 'barney'

// The _.matches shorthand.
_.find(users, { 'age': 1, 'active': true });
// => object for 'pebbles'
```

### `findLast`

This method is like `_.find` except that it iterates over elements of `collection` from right to left.

- **Version**: 2.0.0
- **Arguments**:
  - `collection` (Array|Object): The collection to inspect.
  - `predicate` (Function): The function invoked per iteration.
  - `fromIndex` (number): The index to search from, defaults to `collection.length - 1`.
- **Returns**: (*): The matched element, else `undefined`.

**Example**

```javascript
_.findLast([1, 2, 3, 4], function(n) {
  return n % 2 == 1;
});
// => 3
```

### `flatMap`

Creates a flattened array of values by running each element in `collection` thru `iteratee` and flattening the mapped results one level.

- **Version**: 4.0.0
- **Arguments**:
  - `collection` (Array|Object): The collection to iterate over.
  - `iteratee` (Function): The function invoked per iteration.
- **Returns**: (Array): The new flattened array.

**Example**

```javascript
function duplicate(n) {
  return [n, n];
}

_.flatMap([1, 2], duplicate);
// => [1, 1, 2, 2]
```

### `flatMapDeep`

This method is like `_.flatMap` except that it recursively flattens the mapped results.

- **Version**: 4.7.0
- **Arguments**:
  - `collection` (Array|Object): The collection to iterate over.
  - `iteratee` (Function): The function invoked per iteration.
- **Returns**: (Array): The new flattened array.

**Example**

```javascript
function duplicate(n) {
  return [[[n, n]]];
}

_.flatMapDeep([1, 2], duplicate);
// => [1, 1, 2, 2]
```

### `flatMapDepth`

This method is like `_.flatMap` except that it recursively flattens the mapped results up to `depth`.

- **Version**: 4.7.0
- **Arguments**:
  - `collection` (Array|Object): The collection to iterate over.
  - `iteratee` (Function): The function invoked per iteration.
  - `depth` (number): The maximum recursion depth, defaults to `1`.
- **Returns**: (Array): The new flattened array.

**Example**

```javascript
function duplicate(n) {
  return [[[n, n]]];
}

_.flatMapDepth([1, 2], duplicate, 2);
// => [[1, 1], [2, 2]]
```

### `forEach`

Invokes `iteratee` for each element in `collection`. The `iteratee` can exit iteration early by explicitly returning `false`.

- **Version**: 0.1.0
- **Aliases**: `each`
- **Arguments**:
  - `collection` (Array|Object): The collection to iterate over.
  - `iteratee` (Function): The function invoked per iteration.
- **Returns**: (Array|Object): Returns `collection`.

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

### `forEachRight`

This method is like `_.forEach` except that it iterates over elements of `collection` from right to left.

- **Version**: 2.0.0
- **Aliases**: `eachRight`
- **Arguments**:
  - `collection` (Array|Object): The collection to iterate over.
  - `iteratee` (Function): The function invoked per iteration.
- **Returns**: (Array|Object): Returns `collection`.

**Example**

```javascript
_.forEachRight([1, 2], function(value) {
  console.log(value);
});
// => Logs `2` then `1`.
```

### `groupBy`

Creates an object composed of keys generated from running each element of `collection` thru `iteratee`. The value for each key is an array of elements that generated the key.

- **Version**: 0.1.0
- **Arguments**:
  - `collection` (Array|Object): The collection to iterate over.
  - `iteratee` (Function): The function to transform keys.
- **Returns**: (Object): The composed aggregate object.

**Example**

```javascript
_.groupBy([6.1, 4.2, 6.3], Math.floor);
// => { '4': [4.2], '6': [6.1, 6.3] }

// The _.property shorthand.
_.groupBy(['one', 'two', 'three'], 'length');
// => { '3': ['one', 'two'], '5': ['three'] }
```

### `includes`

Checks if `value` is in `collection`. If `collection` is a string, it's checked for a substring of `value`; otherwise, `SameValueZero` is used for equality comparisons. If `fromIndex` is specified, it's used as the index to search from.

- **Version**: 0.1.0
- **Arguments**:
  - `collection` (Array|Object|string): The collection to inspect.
  - `value` (*): The value to search for.
  - `fromIndex` (number): The index to search from, defaults to `0`.
- **Returns**: (boolean): Returns `true` if `value` is found, else `false`.

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

### `invokeMap`

Invokes the method at `path` of each element in `collection`, returning an array of the results of each invocation. Any additional arguments are provided to each invoked method.

- **Version**: 4.0.0
- **Arguments**:
  - `collection` (Array|Object): The collection to iterate over.
  - `path` (Array|Function|string): The path of the method to invoke or the function invoked per iteration.
  - `...args`: The arguments to invoke each method with.
- **Returns**: (Array): The array of results.

**Example**

```javascript
_.invokeMap([[5, 1, 7], [3, 2, 1]], 'sort');
// => [[1, 5, 7], [1, 2, 3]]

_.invokeMap([123, 456], String.prototype.split, '');
// => [['1', '2', '3'], ['4', '5', '6']]
```

### `keyBy`

Creates an object composed of keys generated from running each element of `collection` thru `iteratee`. The corresponding value of each key is the last element responsible for generating the key.

- **Version**: 4.0.0
- **Arguments**:
  - `collection` (Array|Object): The collection to iterate over.
  - `iteratee` (Function): The function to transform keys.
- **Returns**: (Object): The composed aggregate object.

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

### `map`

Creates an array of values by running each element in `collection` thru `iteratee`.

- **Version**: 0.1.0
- **Arguments**:
  - `collection` (Array|Object): The collection to iterate over.
  - `iteratee` (Function): The function invoked per iteration.
- **Returns**: (Array): The new mapped array.

**Example**

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

// The _.property shorthand.
_.map(users, 'user');
// => ['barney', 'fred']
```

### `orderBy`

This method is like `_.sortBy` except that it allows specifying the sort orders of `iteratees`. If `orders` is not specified, all values are sorted in ascending order. Otherwise, specify `desc` for descending or `asc` for ascending order of corresponding values.

- **Version**: 4.0.0
- **Arguments**:
  - `collection` (Array|Object): The collection to iterate over.
  - `iteratees` (Array[]|Function[]|Object[]|string[]): The iteratees to sort by, defaults to `[_.identity]`.
  - `orders` (string[]): The sort orders of `iteratees`.
- **Returns**: (Array): The new sorted array.

**Example**

```javascript
var users = [
  { 'user': 'fred',   'age': 48 },
  { 'user': 'barney', 'age': 34 },
  { 'user': 'fred',   'age': 40 },
  { 'user': 'barney', 'age': 36 }
];

// Sort by 'user' in ascending order and by 'age' in descending order.
_.orderBy(users, ['user', 'age'], ['asc', 'desc']);
// => objects for [['barney', 36], ['barney', 34], ['fred', 48], ['fred', 40]]
```

### `partition`

Creates an array of elements split into two groups, the first of which contains elements `predicate` returns truthy for, the second of which contains elements `predicate` returns falsy for.

- **Version**: 3.0.0
- **Arguments**:
  - `collection` (Array|Object): The collection to iterate over.
  - `predicate` (Function): The function invoked per iteration.
- **Returns**: (Array): The array of grouped elements.

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

### `reduce`

Reduces `collection` to a single value by running each element in `collection` thru `iteratee`. The `iteratee` is invoked with four arguments: (accumulator, value, index|key, collection).

- **Version**: 0.1.0
- **Arguments**:
  - `collection` (Array|Object): The collection to iterate over.
  - `iteratee` (Function): The function invoked per iteration.
  - `accumulator` (*): The initial value.
- **Returns**: (*): The accumulated value.

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

### `reduceRight`

This method is like `_.reduce` except that it iterates over elements of `collection` from right to left.

- **Version**: 0.1.0
- **Arguments**:
  - `collection` (Array|Object): The collection to iterate over.
  - `iteratee` (Function): The function invoked per iteration.
  - `accumulator` (*): The initial value.
- **Returns**: (*): The accumulated value.

**Example**

```javascript
var array = [[0, 1], [2, 3], [4, 5]];

_.reduceRight(array, function(flattened, other) {
  return flattened.concat(other);
}, []);
// => [4, 5, 2, 3, 0, 1]
```

### `reject`

The opposite of `_.filter`; this method returns the elements of `collection` that `predicate` does not return truthy for.

- **Version**: 0.1.0
- **Arguments**:
  - `collection` (Array|Object): The collection to iterate over.
  - `predicate` (Function): The function invoked per iteration.
- **Returns**: (Array): The new filtered array.

**Example**

```javascript
var users = [
  { 'user': 'barney', 'age': 36, 'active': false },
  { 'user': 'fred',   'age': 40, 'active': true }
];

_.reject(users, function(o) { return !o.active; });
// => objects for ['fred']
```

### `sample`

Gets a random element from `collection`.

- **Version**: 2.0.0
- **Arguments**:
  - `collection` (Array|Object): The collection to sample.
- **Returns**: (*): The random element.

**Example**

```javascript
_.sample([1, 2, 3, 4]);
// => 2
```

### `sampleSize`

Gets `n` random and unique elements from `collection`.

- **Version**: 4.0.0
- **Arguments**:
  - `collection` (Array|Object): The collection to sample.
  - `n` (number): The number of elements to sample, defaults to `1`.
- **Returns**: (Array): The array of random elements.

**Example**

```javascript
_.sampleSize([1, 2, 3], 2);
// => [3, 1]

_.sampleSize([1, 2, 3], 4);
// => [2, 3, 1]
```

### `shuffle`

Creates an array of shuffled values, using a version of the Fisher-Yates shuffle algorithm.

- **Version**: 0.1.0
- **Arguments**:
  - `collection` (Array|Object): The collection to shuffle.
- **Returns**: (Array): The new shuffled array.

**Example**

```javascript
_.shuffle([1, 2, 3, 4]);
// => [4, 1, 3, 2]
```

### `size`

Gets the size of `collection` by returning its length for array-like values or the number of own enumerable string keyed properties for objects.

- **Version**: 0.1.0
- **Arguments**:
  - `collection` (Array|Object|string): The collection to inspect.
- **Returns**: (number): The collection size.

**Example**

```javascript
_.size([1, 2, 3]);
// => 3

_.size({ 'a': 1, 'b': 2 });
// => 2

_.size('pebbles');
// => 7
```

### `some`

Checks if `predicate` returns truthy for any element of `collection`. Iteration is stopped once `predicate` returns a truthy value.

- **Version**: 0.1.0
- **Arguments**:
  - `collection` (Array|Object): The collection to iterate over.
  - `predicate` (Function): The function invoked per iteration.
- **Returns**: (boolean): Returns `true` if any element passes the truthy test, else `false`.

**Example**

```javascript
_.some([null, 0, 'yes', false], Boolean);
// => true

var users = [
  { 'user': 'barney', 'active': true },
  { 'user': 'fred',   'active': false }
];

// The _.matches shorthand.
_.some(users, { 'user': 'barney', 'active': false });
// => false
```

### `sortBy`

Creates an array of elements, sorted in ascending order by the results of running each element in a `collection` thru each `iteratee`. This method performs a stable sort.

- **Version**: 0.1.0
- **Arguments**:
  - `collection` (Array|Object): The collection to iterate over.
  - `...iteratees` (Function|Function[]): The iteratees to sort by.
- **Returns**: (Array): The new sorted array.

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

Now that you're familiar with functions for working with collections, continue on to the [Function](./api-function.md) section to learn about manipulating and enhancing functions.