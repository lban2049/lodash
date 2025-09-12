# Collection

Collection functions are essential for iterating over and manipulating groups of data, including both arrays and objects. These methods provide powerful and concise ways to perform common operations like filtering, mapping, and reducing.

**Note:** When iterating over objects, Lodash treats any object with a `length` property as an array-like collection. For iterating over the properties of plain objects, it is recommended to use functions from the [Object](./api-object.md) category, such as `_.forOwn` or `_.forIn`.

---

## _.countBy

Creates an object composed of keys generated from the results of running each element of `collection` through `iteratee`. The corresponding value of each key is the number of times the key was returned by `iteratee`.

### Parameters

<x-field data-name="collection" data-type="Array|Object" data-required="true" data-desc="The collection to iterate over."></x-field>
<x-field data-name="iteratee" data-type="Function" data-default="_.identity" data-required="false" data-desc="The iteratee to transform keys. Invoked with one argument: (value)."></x-field>

### Returns

<x-field data-name="" data-type="Object" data-desc="Returns the composed aggregate object."></x-field>

### Example

```javascript
_.countBy([6.1, 4.2, 6.3], Math.floor);
// => { '4': 1, '6': 2 }

// The `_.property` iteratee shorthand.
_.countBy(['one', 'two', 'three'], 'length');
// => { '3': 2, '5': 1 }
```

---

## _.every

Checks if `predicate` returns truthy for **all** elements of `collection`. Iteration is stopped once `predicate` returns falsey.

**Note:** This method returns `true` for [empty collections](https://en.wikipedia.org/wiki/Empty_set) because [everything is true](https://en.wikipedia.org/wiki/Vacuous_truth) of elements of empty collections.

### Parameters

<x-field data-name="collection" data-type="Array|Object" data-required="true" data-desc="The collection to iterate over."></x-field>
<x-field data-name="predicate" data-type="Function" data-default="_.identity" data-required="false" data-desc="The function invoked per iteration. It receives three arguments: (value, index|key, collection)."></x-field>

### Returns

<x-field data-name="" data-type="boolean" data-desc="Returns `true` if all elements pass the predicate check, else `false`."></x-field>

### Example

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

## _.filter

Iterates over elements of `collection`, returning an array of all elements `predicate` returns truthy for.

### Parameters

<x-field data-name="collection" data-type="Array|Object" data-required="true" data-desc="The collection to iterate over."></x-field>
<x-field data-name="predicate" data-type="Function" data-default="_.identity" data-required="false" data-desc="The function invoked per iteration. It receives three arguments: (value, index|key, collection)."></x-field>

### Returns

<x-field data-name="" data-type="Array" data-desc="Returns the new filtered array."></x-field>

### Example

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

// The `_.matchesProperty` iteratee shorthand.
_.filter(users, ['active', false]);
// => objects for ['fred']

// The `_.property` iteratee shorthand.
_.filter(users, 'active');
// => objects for ['barney']
```

---

## _.find

Iterates over elements of `collection`, returning the first element `predicate` returns truthy for.

### Parameters

<x-field data-name="collection" data-type="Array|Object" data-required="true" data-desc="The collection to inspect."></x-field>
<x-field data-name="predicate" data-type="Function" data-default="_.identity" data-required="false" data-desc="The function invoked per iteration. It receives three arguments: (value, index|key, collection)."></x-field>
<x-field data-name="fromIndex" data-type="number" data-default="0" data-required="false" data-desc="The index to search from."></x-field>

### Returns

<x-field data-name="" data-type="*" data-desc="Returns the matched element, else `undefined`."></x-field>

### Example

```javascript
var users = [
  { 'user': 'barney',  'age': 36, 'active': true },
  { 'user': 'fred',    'age': 40, 'active': false },
  { 'user': 'pebbles', 'age': 1,  'active': true }
];

_.find(users, function(o) { return o.age < 40; });
// => object for 'barney'

// The `_.matches` iteratee shorthand.
_.find(users, { 'age': 1, 'active': true });
// => object for 'pebbles'

// The `_.matchesProperty` iteratee shorthand.
_.find(users, ['active', false]);
// => object for 'fred'

// The `_.property` iteratee shorthand.
_.find(users, 'active');
// => object for 'barney'
```

---

## _.findLast

This method is like `_.find` except that it iterates over elements of `collection` from right to left.

### Parameters

<x-field data-name="collection" data-type="Array|Object" data-required="true" data-desc="The collection to inspect."></x-field>
<x-field data-name="predicate" data-type="Function" data-default="_.identity" data-required="false" data-desc="The function invoked per iteration."></x-field>
<x-field data-name="fromIndex" data-type="number" data-default="collection.length-1" data-required="false" data-desc="The index to search from."></x-field>

### Returns

<x-field data-name="" data-type="*" data-desc="Returns the matched element, else `undefined`."></x-field>

### Example

```javascript
_.findLast([1, 2, 3, 4], function(n) {
  return n % 2 == 1;
});
// => 3
```

---

## _.flatMap

Creates a flattened array of values by running each element in `collection` through `iteratee` and flattening the mapped results.

### Parameters

<x-field data-name="collection" data-type="Array|Object" data-required="true" data-desc="The collection to iterate over."></x-field>
<x-field data-name="iteratee" data-type="Function" data-default="_.identity" data-required="false" data-desc="The function invoked per iteration. It receives three arguments: (value, index|key, collection)."></x-field>

### Returns

<x-field data-name="" data-type="Array" data-desc="Returns the new flattened array."></x-field>

### Example

```javascript
function duplicate(n) {
  return [n, n];
}

_.flatMap([1, 2], duplicate);
// => [1, 1, 2, 2]
```

---

## _.flatMapDeep

This method is like `_.flatMap` except that it recursively flattens the mapped results.

### Parameters

<x-field data-name="collection" data-type="Array|Object" data-required="true" data-desc="The collection to iterate over."></x-field>
<x-field data-name="iteratee" data-type="Function" data-default="_.identity" data-required="false" data-desc="The function invoked per iteration."></x-field>

### Returns

<x-field data-name="" data-type="Array" data-desc="Returns the new flattened array."></x-field>

### Example

```javascript
function duplicate(n) {
  return [[[n, n]]];
}

_.flatMapDeep([1, 2], duplicate);
// => [1, 1, 2, 2]
```

---

## _.flatMapDepth

This method is like `_.flatMap` except that it recursively flattens the mapped results up to `depth` times.

### Parameters

<x-field data-name="collection" data-type="Array|Object" data-required="true" data-desc="The collection to iterate over."></x-field>
<x-field data-name="iteratee" data-type="Function" data-default="_.identity" data-required="false" data-desc="The function invoked per iteration."></x-field>
<x-field data-name="depth" data-type="number" data-default="1" data-required="false" data-desc="The maximum recursion depth."></x-field>

### Returns

<x-field data-name="" data-type="Array" data-desc="Returns the new flattened array."></x-field>

### Example

```javascript
function duplicate(n) {
  return [[[n, n]]];
}

_.flatMapDepth([1, 2], duplicate, 2);
// => [[1, 1], [2, 2]]
```

---

## _.forEach

Iterates over elements of `collection` and invokes `iteratee` for each element. Iteratee functions may exit iteration early by explicitly returning `false`.

### Parameters

<x-field data-name="collection" data-type="Array|Object" data-required="true" data-desc="The collection to iterate over."></x-field>
<x-field data-name="iteratee" data-type="Function" data-default="_.identity" data-required="false" data-desc="The function invoked per iteration. It receives three arguments: (value, index|key, collection)."></x-field>

### Returns

<x-field data-name="" data-type="Array|Object" data-desc="Returns `collection`."></x-field>

### Example

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

## _.forEachRight

This method is like `_.forEach` except that it iterates over elements of `collection` from right to left.

### Parameters

<x-field data-name="collection" data-type="Array|Object" data-required="true" data-desc="The collection to iterate over."></x-field>
<x-field data-name="iteratee" data-type="Function" data-default="_.identity" data-required="false" data-desc="The function invoked per iteration."></x-field>

### Returns

<x-field data-name="" data-type="Array|Object" data-desc="Returns `collection`."></x-field>

### Example

```javascript
_.forEachRight([1, 2], function(value) {
  console.log(value);
});
// => Logs `2` then `1`.
```

---

## _.groupBy

Creates an object composed of keys generated from the results of running each element of `collection` through `iteratee`. The order of grouped values is determined by the order they occur in `collection`. The corresponding value of each key is an array of elements responsible for generating the key.

### Parameters

<x-field data-name="collection" data-type="Array|Object" data-required="true" data-desc="The collection to iterate over."></x-field>
<x-field data-name="iteratee" data-type="Function" data-default="_.identity" data-required="false" data-desc="The iteratee to transform keys."></x-field>

### Returns

<x-field data-name="" data-type="Object" data-desc="Returns the composed aggregate object."></x-field>

### Example

```javascript
_.groupBy([6.1, 4.2, 6.3], Math.floor);
// => { '4': [4.2], '6': [6.1, 6.3] }

// The `_.property` iteratee shorthand.
_.groupBy(['one', 'two', 'three'], 'length');
// => { '3': ['one', 'two'], '5': ['three'] }
```

---

## _.includes

Checks if `value` is in `collection`. If `collection` is a string, it's checked for a substring of `value`. Otherwise, `SameValueZero` is used for equality comparisons. If `fromIndex` is negative, it's used as the offset from the end of `collection`.

### Parameters

<x-field data-name="collection" data-type="Array|Object|string" data-required="true" data-desc="The collection to inspect."></x-field>
<x-field data-name="value" data-type="*" data-required="true" data-desc="The value to search for."></x-field>
<x-field data-name="fromIndex" data-type="number" data-default="0" data-required="false" data-desc="The index to search from."></x-field>

### Returns

<x-field data-name="" data-type="boolean" data-desc="Returns `true` if `value` is found, else `false`."></x-field>

### Example

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

Invokes the method at `path` of each element in `collection`, returning an array of the results. Any additional arguments are provided to each invoked method. If `path` is a function, it's invoked for, and `this` bound to, each element in `collection`.

### Parameters

<x-field data-name="collection" data-type="Array|Object" data-required="true" data-desc="The collection to iterate over."></x-field>
<x-field data-name="path" data-type="Array|Function|string" data-required="true" data-desc="The path of the method to invoke or the function invoked per iteration."></x-field>
<x-field data-name="args" data-type="...*" data-required="false" data-desc="The arguments to invoke each method with."></x-field>

### Returns

<x-field data-name="" data-type="Array" data-desc="Returns the array of results."></x-field>

### Example

```javascript
_.invokeMap([[5, 1, 7], [3, 2, 1]], 'sort');
// => [[1, 5, 7], [1, 2, 3]]

_.invokeMap([123, 456], String.prototype.split, '');
// => [['1', '2', '3'], ['4', '5', '6']]
```

---

## _.keyBy

Creates an object composed of keys generated from the results of running each element of `collection` through `iteratee`. The corresponding value of each key is the last element responsible for generating the key.

### Parameters

<x-field data-name="collection" data-type="Array|Object" data-required="true" data-desc="The collection to iterate over."></x-field>
<x-field data-name="iteratee" data-type="Function" data-default="_.identity" data-required="false" data-desc="The iteratee to transform keys."></x-field>

### Returns

<x-field data-name="" data-type="Object" data-desc="Returns the composed aggregate object."></x-field>

### Example

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

Creates an array of values by running each element in `collection` through `iteratee`. The iteratee is invoked with three arguments: `(value, index|key, collection)`.

### Parameters

<x-field data-name="collection" data-type="Array|Object" data-required="true" data-desc="The collection to iterate over."></x-field>
<x-field data-name="iteratee" data-type="Function" data-default="_.identity" data-required="false" data-desc="The function invoked per iteration."></x-field>

### Returns

<x-field data-name="" data-type="Array" data-desc="Returns the new mapped array."></x-field>

### Example

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

## _.orderBy

This method is like `_.sortBy` except that it allows specifying the sort orders of the iteratees to sort by. If `orders` is unspecified, all values are sorted in ascending order. Otherwise, specify an order of `"desc"` for descending or `"asc"` for ascending sort order of corresponding values.

### Parameters

<x-field data-name="collection" data-type="Array|Object" data-required="true" data-desc="The collection to iterate over."></x-field>
<x-field data-name="iteratees" data-type="Array[]|Function[]|Object[]|string[]" data-default="[_.identity]" data-required="false" data-desc="The iteratees to sort by."></x-field>
<x-field data-name="orders" data-type="string[]" data-required="false" data-desc="The sort orders of `iteratees`."></x-field>

### Returns

<x-field data-name="" data-type="Array" data-desc="Returns the new sorted array."></x-field>

### Example

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

## _.partition

Creates an array of elements split into two groups. The first group contains elements for which `predicate` returns truthy, and the second group contains elements for which it returns falsey.

### Parameters

<x-field data-name="collection" data-type="Array|Object" data-required="true" data-desc="The collection to iterate over."></x-field>
<x-field data-name="predicate" data-type="Function" data-default="_.identity" data-required="false" data-desc="The function invoked per iteration."></x-field>

### Returns

<x-field data-name="" data-type="Array" data-desc="Returns the array of grouped elements, e.g. `[[truthy_elements], [falsey_elements]]`."></x-field>

### Example

```javascript
var users = [
  { 'user': 'barney',  'age': 36, 'active': false },
  { 'user': 'fred',    'age': 40, 'active': true },
  { 'user': 'pebbles', 'age': 1,  'active': false }
];

_.partition(users, function(o) { return o.active; });
// => objects for [['fred'], ['barney', 'pebbles']]

// The `_.matches` iteratee shorthand.
_.partition(users, { 'age': 1, 'active': false });
// => objects for [['pebbles'], ['barney', 'fred']]
```

---

## _.reduce

Reduces `collection` to a value which is the accumulated result of running each element in `collection` through `iteratee`. If `accumulator` is not given, the first element of `collection` is used as the initial value. The iteratee is invoked with four arguments: `(accumulator, value, index|key, collection)`.

### Parameters

<x-field data-name="collection" data-type="Array|Object" data-required="true" data-desc="The collection to iterate over."></x-field>
<x-field data-name="iteratee" data-type="Function" data-default="_.identity" data-required="false" data-desc="The function invoked per iteration."></x-field>
<x-field data-name="accumulator" data-type="*" data-required="false" data-desc="The initial value."></x-field>

### Returns

<x-field data-name="" data-type="*" data-desc="Returns the accumulated value."></x-field>

### Example

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

## _.reduceRight

This method is like `_.reduce` except that it iterates over elements of `collection` from right to left.

### Parameters

<x-field data-name="collection" data-type="Array|Object" data-required="true" data-desc="The collection to iterate over."></x-field>
<x-field data-name="iteratee" data-type="Function" data-default="_.identity" data-required="false" data-desc="The function invoked per iteration."></x-field>
<x-field data-name="accumulator" data-type="*" data-required="false" data-desc="The initial value."></x-field>

### Returns

<x-field data-name="" data-type="*" data-desc="Returns the accumulated value."></x-field>

### Example

```javascript
var array = [[0, 1], [2, 3], [4, 5]];

_.reduceRight(array, function(flattened, other) {
  return flattened.concat(other);
}, []);
// => [4, 5, 2, 3, 0, 1]
```

---

## _.reject

The opposite of `_.filter`; this method returns the elements of `collection` that `predicate` does **not** return truthy for.

### Parameters

<x-field data-name="collection" data-type="Array|Object" data-required="true" data-desc="The collection to iterate over."></x-field>
<x-field data-name="predicate" data-type="Function" data-default="_.identity" data-required="false" data-desc="The function invoked per iteration."></x-field>

### Returns

<x-field data-name="" data-type="Array" data-desc="Returns the new filtered array."></x-field>

### Example

```javascript
var users = [
  { 'user': 'barney', 'age': 36, 'active': false },
  { 'user': 'fred',   'age': 40, 'active': true }
];

_.reject(users, function(o) { return !o.active; });
// => objects for ['fred']

// The `_.matches` iteratee shorthand.
_.reject(users, { 'age': 40, 'active': true });
// => objects for ['barney']
```

---

## _.sample

Gets a random element from `collection`.

### Parameters

<x-field data-name="collection" data-type="Array|Object" data-required="true" data-desc="The collection to sample."></x-field>

### Returns

<x-field data-name="" data-type="*" data-desc="Returns the random element."></x-field>

### Example

```javascript
_.sample([1, 2, 3, 4]);
// => 2
```

---

## _.sampleSize

Gets `n` random elements at unique keys from `collection` up to the size of `collection`.

### Parameters

<x-field data-name="collection" data-type="Array|Object" data-required="true" data-desc="The collection to sample."></x-field>
<x-field data-name="n" data-type="number" data-default="1" data-required="false" data-desc="The number of elements to sample."></x-field>

### Returns

<x-field data-name="" data-type="Array" data-desc="Returns the random elements."></x-field>

### Example

```javascript
_.sampleSize([1, 2, 3], 2);
// => [3, 1]

_.sampleSize([1, 2, 3], 4);
// => [2, 3, 1]
```

---

## _.shuffle

Creates an array of shuffled values, using a version of the [Fisher-Yates shuffle](https://en.wikipedia.org/wiki/Fisher-Yates_shuffle).

### Parameters

<x-field data-name="collection" data-type="Array|Object" data-required="true" data-desc="The collection to shuffle."></x-field>

### Returns

<x-field data-name="" data-type="Array" data-desc="Returns the new shuffled array."></x-field>

### Example

```javascript
_.shuffle([1, 2, 3, 4]);
// => [4, 1, 3, 2]
```

---

## _.size

Gets the size of `collection` by returning its length for array-like values or the number of own enumerable string keyed properties for objects.

### Parameters

<x-field data-name="collection" data-type="Array|Object|string" data-required="true" data-desc="The collection to inspect."></x-field>

### Returns

<x-field data-name="" data-type="number" data-desc="Returns the collection size."></x-field>

### Example

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

Checks if `predicate` returns truthy for **any** element of `collection`. Iteration is stopped once `predicate` returns truthy.

### Parameters

<x-field data-name="collection" data-type="Array|Object" data-required="true" data-desc="The collection to iterate over."></x-field>
<x-field data-name="predicate" data-type="Function" data-default="_.identity" data-required="false" data-desc="The function invoked per iteration."></x-field>

### Returns

<x-field data-name="" data-type="boolean" data-desc="Returns `true` if any element passes the predicate check, else `false`."></x-field>

### Example

```javascript
_.some([null, 0, 'yes', false], Boolean);
// => true

var users = [
  { 'user': 'barney', 'active': true },
  { 'user': 'fred',   'active': false }
];

// The `_.matches` iteratee shorthand.
_.some(users, { 'user': 'barney', 'active': false });
// => false

// The `_.matchesProperty` iteratee shorthand.
_.some(users, ['active', false]);
// => true
```

---

## _.sortBy

Creates an array of elements, sorted in ascending order by the results of running each element in a collection through each iteratee. This method performs a stable sort, meaning it preserves the original sort order of equal elements.

### Parameters

<x-field data-name="collection" data-type="Array|Object" data-required="true" data-desc="The collection to iterate over."></x-field>
<x-field data-name="iteratees" data-type="...(Function|Function[])" data-default="[_.identity]" data-required="false" data-desc="The iteratees to sort by."></x-field>

### Returns

<x-field data-name="" data-type="Array" data-desc="Returns the new sorted array."></x-field>

### Example

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