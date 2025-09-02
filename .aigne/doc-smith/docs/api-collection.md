# Collection

Collection functions are suitable for iterable data structures, such as arrays, objects, and strings. These functions provide a consistent way to iterate, filter, map, and group elements, simplifying operations on complex data structures. They handle data in a declarative and efficient manner, regardless of the underlying data type.

For operations specifically targeting arrays or objects, please refer to the documentation in the [Array](./api-array.md) and [Object](./api-object.md) sections, respectively.

## Function List

### countBy

Creates an object composed of keys generated from the results of running each element of `collection` thru `iteratee`. The corresponding value of each key is the number of times the key was returned by `iteratee`.

- **Version**: 0.5.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `collection` | `Array`\|`Object` | The collection to iterate over. |
| `iteratee` | `Function` | The function invoked per iteration to transform keys. |

**Returns**

| Type | Description |
| --- | --- |
| `Object` | Returns the composed aggregate object. |

**Example**

```javascript
_.countBy([6.1, 4.2, 6.3], Math.floor);
// => { '4': 1, '6': 2 }

// Using the _.property shorthand
_.countBy(['one', 'two', 'three'], 'length');
// => { '3': 2, '5': 1 }
```

### every

Checks if the `predicate` function returns a truthy value for all elements of the `collection`. Iteration stops once `predicate` returns a falsy value.

- **Version**: 0.1.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `collection` | `Array`\|`Object` | The collection to iterate over. |
| `predicate` | `Function` | The function invoked per iteration. |

**Returns**

| Type | Description |
| --- | --- |
| `boolean` | Returns `true` if all elements pass the truth test, else `false`. |

**Example**

```javascript
_.every([true, 1, null, 'yes'], Boolean);
// => false

var users = [
  { 'user': 'barney', 'age': 36, 'active': false },
  { 'user': 'fred',   'age': 40, 'active': false }
];

// Using the _.matches shorthand
_.every(users, { 'user': 'barney', 'active': false });
// => false

// Using the _.matchesProperty shorthand
_.every(users, ['active', false]);
// => true
```

### filter

Iterates over elements of `collection`, returning a new array of all elements for which the `predicate` function returns a truthy value.

- **Version**: 0.1.0
- **Related**: `reject`

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `collection` | `Array`\|`Object` | The collection to iterate over. |
| `predicate` | `Function` | The function invoked per iteration. |

**Returns**

| Type | Description |
| --- | --- |
| `Array` | Returns the new array of filtered elements. |

**Example**

```javascript
var users = [
  { 'user': 'barney', 'age': 36, 'active': true },
  { 'user': 'fred',   'age': 40, 'active': false }
];

_.filter(users, function(o) { return !o.active; });
// => objects for ['fred']

// Using the _.matches shorthand
_.filter(users, { 'age': 36, 'active': true });
// => objects for ['barney']
```

### find

Iterates over elements of `collection`, returning the first element for which the `predicate` function returns a truthy value. The `predicate` is invoked with three arguments: (value, index|key, collection).

- **Version**: 0.1.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `collection` | `Array`\|`Object` | The collection to inspect. |
| `predicate` | `Function` | The function invoked per iteration. |
| `fromIndex` | `number` | The index to search from, defaults to `0`. |

**Returns**

| Type | Description |
| --- | --- |
| `*` | Returns the matched element, else `undefined`. |

**Example**

```javascript
var users = [
  { 'user': 'barney',  'age': 36, 'active': true },
  { 'user': 'fred',    'age': 40, 'active': false },
  { 'user': 'pebbles', 'age': 1,  'active': true }
];

_.find(users, function(o) { return o.age < 40; });
// => object for 'barney'

// Using the _.matches shorthand
_.find(users, { 'age': 1, 'active': true });
// => object for 'pebbles'
```

### findLast

This method is like `_.find` except that it iterates over elements of `collection` from right to left.

- **Version**: 2.0.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `collection` | `Array`\|`Object` | The collection to inspect. |
| `predicate` | `Function` | The function invoked per iteration. |
| `fromIndex` | `number` | The index to search from, defaults to `collection.length - 1`. |

**Returns**

| Type | Description |
| --- | --- |
| `*` | Returns the matched element, else `undefined`. |

**Example**

```javascript
_.findLast([1, 2, 3, 4], function(n) {
  return n % 2 == 1;
});
// => 3
```

### flatMap

Creates a new flattened array by running each element in `collection` through the `iteratee` function and flattening the mapped results by one level.

- **Version**: 4.0.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `collection` | `Array`\|`Object` | The collection to iterate over. |
| `iteratee` | `Function` | The function invoked per iteration. |

**Returns**

| Type | Description |
| --- | --- |
| `Array` | Returns the new flattened array. |

**Example**

```javascript
function duplicate(n) {
  return [n, n];
}

_.flatMap([1, 2], duplicate);
// => [1, 1, 2, 2]
```

### flatMapDeep

This method is like `_.flatMap` except that it recursively flattens the mapped results.

- **Version**: 4.7.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `collection` | `Array`\|`Object` | The collection to iterate over. |
| `iteratee` | `Function` | The function invoked per iteration. |

**Returns**

| Type | Description |
| --- | --- |
| `Array` | Returns the new flattened array. |

**Example**

```javascript
function duplicate(n) {
  return [[[n, n]]];
}

_.flatMapDeep([1, 2], duplicate);
// => [1, 1, 2, 2]
```

### flatMapDepth

This method is like `_.flatMap` except that it recursively flattens the mapped results up to a specified `depth`.

- **Version**: 4.7.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `collection` | `Array`\|`Object` | The collection to iterate over. |
| `iteratee` | `Function` | The function invoked per iteration. |
| `depth` | `number` | The maximum recursion depth for flattening, defaults to `1`. |

**Returns**

| Type | Description |
| --- | --- |
| `Array` | Returns the new flattened array. |

**Example**

```javascript
function duplicate(n) {
  return [[[n, n]]];
}

_.flatMapDepth([1, 2], duplicate, 2);
// => [[1, 1], [2, 2]]
```

### forEach

Invokes the `iteratee` function for each element in `collection`. The `iteratee` function can exit iteration early by explicitly returning `false`.

- **Version**: 0.1.0
- **Alias**: `each`
- **Related**: `forEachRight`

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `collection` | `Array`\|`Object` | The collection to iterate over. |
| `iteratee` | `Function` | The function invoked per iteration. |

**Returns**

| Type | Description |
| --- | --- |
| `Array`\|`Object` | Returns `collection`. |

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

### forEachRight

This method is like `_.forEach` except that it iterates over elements of `collection` from right to left.

- **Version**: 2.0.0
- **Alias**: `eachRight`
- **Related**: `forEach`

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `collection` | `Array`\|`Object` | The collection to iterate over. |
| `iteratee` | `Function` | The function invoked per iteration. |

**Returns**

| Type | Description |
| --- | --- |
| `Array`\|`Object` | Returns `collection`. |

**Example**

```javascript
_.forEachRight([1, 2], function(value) {
  console.log(value);
});
// => Logs `2` then `1`.
```

### groupBy

Creates an object with keys generated by running each element of `collection` through the `iteratee` function. The value for each key is an array of elements that produced that key.

- **Version**: 0.1.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `collection` | `Array`\|`Object` | The collection to iterate over. |
| `iteratee` | `Function` | The function to transform keys. |

**Returns**

| Type | Description |
| --- | --- |
| `Object` | Returns the composed aggregate object. |

**Example**

```javascript
_.groupBy([6.1, 4.2, 6.3], Math.floor);
// => { '4': [4.2], '6': [6.1, 6.3] }

// Using the _.property shorthand
_.groupBy(['one', 'two', 'three'], 'length');
// => { '3': ['one', 'two'], '5': ['three'] }
```

### includes

Checks if `value` is in `collection`. If `collection` is a string, it checks if `value` is a substring; otherwise, it uses `SameValueZero` for equality comparisons. If `fromIndex` is specified, it starts searching from that index.

- **Version**: 0.1.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `collection` | `Array`\|`Object`\|`string` | The collection to inspect. |
| `value` | `*` | The value to search for. |
| `fromIndex` | `number` | The index to search from, defaults to `0`. |

**Returns**

| Type | Description |
| --- | --- |
| `boolean` | Returns `true` if `value` is found, else `false`. |

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

### invokeMap

Invokes the method at `path` on each element in `collection`, returning an array of the results of each invocation. Any additional arguments are passed to each invoked method.

- **Version**: 4.0.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `collection` | `Array`\|`Object` | The collection to iterate over. |
| `path` | `Array`\|`Function`\|`string` | The path of the method to invoke or the function to invoke per iteration. |
| `...args` | `*` | The arguments to pass to each method. |

**Returns**

| Type | Description |
| --- | --- |
| `Array` | Returns the array of results. |

**Example**

```javascript
_.invokeMap([[5, 1, 7], [3, 2, 1]], 'sort');
// => [[1, 5, 7], [1, 2, 3]]

_.invokeMap([123, 456], String.prototype.split, '');
// => [['1', '2', '3'], ['4', '5', '6']]
```

### keyBy

Creates an object with keys generated by running each element of `collection` through the `iteratee` function. The value for each key is the last element that produced that key.

- **Version**: 4.0.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `collection` | `Array`\|`Object` | The collection to iterate over. |
| `iteratee` | `Function` | The function to transform keys. |

**Returns**

| Type | Description |
| --- | --- |
| `Object` | Returns the composed aggregate object. |

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

### map

Creates a new array of values by running each element in `collection` through the `iteratee` function.

- **Version**: 0.1.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `collection` | `Array`\|`Object` | The collection to iterate over. |
| `iteratee` | `Function` | The function invoked per iteration. |

**Returns**

| Type | Description |
| --- | --- |
| `Array` | Returns the new mapped array. |

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

// Using the _.property shorthand
_.map(users, 'user');
// => ['barney', 'fred']
```

### orderBy

This method is like `_.sortBy`, except that it allows specifying the sort orders for each iteratee. If `orders` are not specified, all values are sorted in ascending order. Otherwise, specify `desc` for descending or `asc` for ascending order for the corresponding values.

- **Version**: 4.0.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `collection` | `Array`\|`Object` | The collection to iterate over. |
| `iteratees` | `Array[]`\|`Function[]`\|`Object[]`\|`string[]` | The iteratees to sort by, defaults to `[_.identity]`. |
| `orders` | `string[]` | The sort orders for `iteratees`. |

**Returns**

| Type | Description |
| --- | --- |
| `Array` | Returns the new sorted array. |

**Example**

```javascript
var users = [
  { 'user': 'fred',   'age': 48 },
  { 'user': 'barney', 'age': 34 },
  { 'user': 'fred',   'age': 40 },
  { 'user': 'barney', 'age': 36 }
];

// Sort by 'user' in ascending order and 'age' in descending order
_.orderBy(users, ['user', 'age'], ['asc', 'desc']);
// => objects for [['barney', 36], ['barney', 34], ['fred', 48], ['fred', 40]]
```

### partition

Creates an array of elements split into two groups. The first group contains elements for which the `predicate` returns a truthy value, and the second group contains elements for which the `predicate` returns a falsy value.

- **Version**: 3.0.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `collection` | `Array`\|`Object` | The collection to iterate over. |
| `predicate` | `Function` | The function invoked per iteration. |

**Returns**

| Type | Description |
| --- | --- |
| `Array` | Returns the array of grouped elements. |

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

### reduce

Reduces `collection` to a single value by running each element through an `iteratee` function. The `iteratee` is invoked with four arguments: (accumulator, value, index|key, collection).

- **Version**: 0.1.0
- **Related**: `reduceRight`

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `collection` | `Array`\|`Object` | The collection to iterate over. |
| `iteratee` | `Function` | The function invoked per iteration. |
| `accumulator` | `*` | The initial value. |

**Returns**

| Type | Description |
| --- | --- |
| `*` | Returns the accumulated value. |

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

### reduceRight

This method is like `_.reduce` except that it iterates over elements of `collection` from right to left.

- **Version**: 0.1.0
- **Related**: `reduce`

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `collection` | `Array`\|`Object` | The collection to iterate over. |
| `iteratee` | `Function` | The function invoked per iteration. |
| `accumulator` | `*` | The initial value. |

**Returns**

| Type | Description |
| --- | --- |
| `*` | Returns the accumulated value. |

**Example**

```javascript
var array = [[0, 1], [2, 3], [4, 5]];

_.reduceRight(array, function(flattened, other) {
  return flattened.concat(other);
}, []);
// => [4, 5, 2, 3, 0, 1]
```

### reject

The opposite of `_.filter`; this method returns the elements of `collection` that the `predicate` function does not return a truthy value for.

- **Version**: 0.1.0
- **Related**: `filter`

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `collection` | `Array`\|`Object` | The collection to iterate over. |
| `predicate` | `Function` | The function invoked per iteration. |

**Returns**

| Type | Description |
| --- | --- |
| `Array` | Returns the new filtered array. |

**Example**

```javascript
var users = [
  { 'user': 'barney', 'age': 36, 'active': false },
  { 'user': 'fred',   'age': 40, 'active': true }
];

_.reject(users, function(o) { return !o.active; });
// => objects for ['fred']
```

### sample

Gets a random element from `collection`.

- **Version**: 2.0.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `collection` | `Array`\|`Object` | The collection to sample from. |

**Returns**

| Type | Description |
| --- | --- |
| `*` | Returns the random element. |

**Example**

```javascript
_.sample([1, 2, 3, 4]);
// => 2
```

### sampleSize

Gets `n` random, unique elements from `collection`.

- **Version**: 4.0.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `collection` | `Array`\|`Object` | The collection to sample from. |
| `n` | `number` | The number of elements to sample, defaults to `1`. |

**Returns**

| Type | Description |
| --- | --- |
| `Array` | Returns an array of random elements. |

**Example**

```javascript
_.sampleSize([1, 2, 3], 2);
// => [3, 1]

_.sampleSize([1, 2, 3], 4);
// => [2, 3, 1]
```

### shuffle

Creates an array of shuffled values, using a version of the Fisher-Yates shuffle algorithm.

- **Version**: 0.1.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `collection` | `Array`\|`Object` | The collection to shuffle. |

**Returns**

| Type | Description |
| --- | --- |
| `Array` | Returns the new shuffled array. |

**Example**

```javascript
_.shuffle([1, 2, 3, 4]);
// => [4, 1, 3, 2]
```

### size

Gets the size of `collection`. For array-like values, it returns their length; for objects, it returns the number of their own enumerable string-keyed properties.

- **Version**: 0.1.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `collection` | `Array`\|`Object`\|`string` | The collection to inspect. |

**Returns**

| Type | Description |
| --- | --- |
| `number` | Returns the collection size. |

**Example**

```javascript
_.size([1, 2, 3]);
// => 3

_.size({ 'a': 1, 'b': 2 });
// => 2

_.size('pebbles');
// => 7
```

### some

Checks if any element in `collection` passes the truth test of the `predicate` function. Iteration stops as soon as `predicate` returns a truthy value.

- **Version**: 0.1.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `collection` | `Array`\|`Object` | The collection to iterate over. |
| `predicate` | `Function` | The function invoked per iteration. |

**Returns**

| Type | Description |
| --- | --- |
| `boolean` | Returns `true` if any element passes the truth test, else `false`. |

**Example**

```javascript
_.some([null, 0, 'yes', false], Boolean);
// => true

var users = [
  { 'user': 'barney', 'active': true },
  { 'user': 'fred',   'active': false }
];

// Using the _.matches shorthand
_.some(users, { 'user': 'barney', 'active': false });
// => false
```

### sortBy

Creates an array of elements, sorted in ascending order by the results of running each element in the `collection` through each `iteratee` function. This method performs a stable sort.

- **Version**: 0.1.0

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `collection` | `Array`\|`Object` | The collection to iterate over. |
| `...iteratees` | `Function`\|`Function[]` | The iteratees to sort by. |

**Returns**

| Type | Description |
| --- | --- |
| `Array` | Returns the new sorted array. |

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

Now that you are familiar with functions for handling collections, you can proceed to explore the [Date](./api-date.md) section to learn how to work with date objects.
