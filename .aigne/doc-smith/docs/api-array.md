# Array

Lodash's array methods offer a comprehensive toolkit for manipulating and querying arrays in JavaScript. These functions provide robust, cross-browser solutions for common tasks like splitting arrays into chunks, removing elements, finding values, and performing complex transformations. By leveraging these utilities, you can write cleaner, more declarative, and more efficient code.

---

### chunk

Creates an array of elements split into groups the length of `size`. If `array` can't be split evenly, the final chunk will be the remaining elements.

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array to process."></x-field>
<x-field data-name="size" data-type="number" data-default="1" data-required="false" data-desc="The length of each chunk."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns the new array of chunks."></x-field>

**Example**

```javascript
_.chunk(['a', 'b', 'c', 'd'], 2);
// => [['a', 'b'], ['c', 'd']]

_.chunk(['a', 'b', 'c', 'd'], 3);
// => [['a', 'b', 'c'], ['d']]
```

### compact

Creates an array with all falsey values removed. The values `false`, `null`, `0`, `""`, `undefined`, and `NaN` are falsey.

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array to compact."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns the new array of filtered values."></x-field>

**Example**

```javascript
_.compact([0, 1, false, 2, '', 3]);
// => [1, 2, 3]
```

### concat

Creates a new array concatenating `array` with any additional arrays and/or values.

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array to concatenate."></x-field>
<x-field data-name="[values]" data-type="...*" data-required="false" data-desc="The values to concatenate."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns the new concatenated array."></x-field>

**Example**

```javascript
var array = [1];
var other = _.concat(array, 2, [3], [[4]]);

console.log(other);
// => [1, 2, 3, [4]]

console.log(array);
// => [1]
```

### difference

Creates an array of `array` values not included in the other given arrays using [`SameValueZero`](http://ecma-international.org/ecma-262/7.0/#sec-samevaluezero) for equality comparisons. The order and references of result values are determined by the first array.

**Note:** Unlike `_.pullAll`, this method returns a new array.

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array to inspect."></x-field>
<x-field data-name="[values]" data-type="...Array" data-required="false" data-desc="The values to exclude."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns the new array of filtered values."></x-field>

**Example**

```javascript
_.difference([2, 1], [2, 3]);
// => [1]
```

### differenceBy

This method is like `_.difference` except that it accepts `iteratee` which is invoked for each element of `array` and `values` to generate the criterion by which they're compared. The order and references of result values are determined by the first array. The iteratee is invoked with one argument: (value).

**Note:** Unlike `_.pullAllBy`, this method returns a new array.

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array to inspect."></x-field>
<x-field data-name="[values]" data-type="...Array" data-required="false" data-desc="The values to exclude."></x-field>
<x-field data-name="[iteratee=_.identity]" data-type="Function" data-required="false" data-desc="The iteratee invoked per element."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns the new array of filtered values."></x-field>

**Example**

```javascript
_.differenceBy([2.1, 1.2], [2.3, 3.4], Math.floor);
// => [1.2]

// The `_.property` iteratee shorthand.
_.differenceBy([{ 'x': 2 }, { 'x': 1 }], [{ 'x': 1 }], 'x');
// => [{ 'x': 2 }]
```

### differenceWith

This method is like `_.difference` except that it accepts `comparator` which is invoked to compare elements of `array` to `values`. The order and references of result values are determined by the first array. The comparator is invoked with two arguments: (arrVal, othVal).

**Note:** Unlike `_.pullAllWith`, this method returns a new array.

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array to inspect."></x-field>
<x-field data-name="[values]" data-type="...Array" data-required="false" data-desc="The values to exclude."></x-field>
<x-field data-name="[comparator]" data-type="Function" data-required="false" data-desc="The comparator invoked per element."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns the new array of filtered values."></x-field>

**Example**

```javascript
var objects = [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }];

_.differenceWith(objects, [{ 'x': 1, 'y': 2 }], _.isEqual);
// => [{ 'x': 2, 'y': 1 }]
```

### drop

Creates a slice of `array` with `n` elements dropped from the beginning.

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array to query."></x-field>
<x-field data-name="[n=1]" data-type="number" data-required="false" data-desc="The number of elements to drop."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns the slice of `array`."></x-field>

**Example**

```javascript
_.drop([1, 2, 3]);
// => [2, 3]

_.drop([1, 2, 3], 2);
// => [3]

_.drop([1, 2, 3], 5);
// => []

_.drop([1, 2, 3], 0);
// => [1, 2, 3]
```

### dropRight

Creates a slice of `array` with `n` elements dropped from the end.

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array to query."></x-field>
<x-field data-name="[n=1]" data-type="number" data-required="false" data-desc="The number of elements to drop."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns the slice of `array`."></x-field>

**Example**

```javascript
_.dropRight([1, 2, 3]);
// => [1, 2]

_.dropRight([1, 2, 3], 2);
// => [1]

_.dropRight([1, 2, 3], 5);
// => []

_.dropRight([1, 2, 3], 0);
// => [1, 2, 3]
```

### dropRightWhile

Creates a slice of `array` excluding elements dropped from the end. Elements are dropped until `predicate` returns falsey. The predicate is invoked with three arguments: (value, index, array).

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array to query."></x-field>
<x-field data-name="[predicate=_.identity]" data-type="Function" data-required="false" data-desc="The function invoked per iteration."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns the slice of `array`."></x-field>

**Example**

```javascript
var users = [
  { 'user': 'barney',  'active': true },
  { 'user': 'fred',    'active': false },
  { 'user': 'pebbles', 'active': false }
];

_.dropRightWhile(users, function(o) { return !o.active; });
// => objects for ['barney']
```

### dropWhile

Creates a slice of `array` excluding elements dropped from the beginning. Elements are dropped until `predicate` returns falsey. The predicate is invoked with three arguments: (value, index, array).

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array to query."></x-field>
<x-field data-name="[predicate=_.identity]" data-type="Function" data-required="false" data-desc="The function invoked per iteration."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns the slice of `array`."></x-field>

**Example**

```javascript
var users = [
  { 'user': 'barney',  'active': false },
  { 'user': 'fred',    'active': false },
  { 'user': 'pebbles', 'active': true }
];

_.dropWhile(users, function(o) { return !o.active; });
// => objects for ['pebbles']
```

### fill

Fills elements of `array` with `value` from `start` up to, but not including, `end`.

**Note:** This method mutates `array`.

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array to fill."></x-field>
<x-field data-name="value" data-type="*" data-required="true" data-desc="The value to fill `array` with."></x-field>
<x-field data-name="[start=0]" data-type="number" data-required="false" data-desc="The start position."></x-field>
<x-field data-name="[end=array.length]" data-type="number" data-required="false" data-desc="The end position."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns `array`."></x-field>

**Example**

```javascript
var array = [1, 2, 3];

_.fill(array, 'a');
console.log(array);
// => ['a', 'a', 'a']

_.fill(Array(3), 2);
// => [2, 2, 2]

_.fill([4, 6, 8, 10], '*', 1, 3);
// => [4, '*', '*', 10]
```

### findIndex

This method is like `_.find` except that it returns the index of the first element `predicate` returns truthy for instead of the element itself.

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array to inspect."></x-field>
<x-field data-name="[predicate=_.identity]" data-type="Function" data-required="false" data-desc="The function invoked per iteration."></x-field>
<x-field data-name="[fromIndex=0]" data-type="number" data-required="false" data-desc="The index to search from."></x-field>

**Returns**

<x-field data-name="" data-type="number" data-desc="Returns the index of the found element, else `-1`."></x-field>

**Example**

```javascript
var users = [
  { 'user': 'barney',  'active': false },
  { 'user': 'fred',    'active': false },
  { 'user': 'pebbles', 'active': true }
];

_.findIndex(users, function(o) { return o.user == 'barney'; });
// => 0
```

### findLastIndex

This method is like `_.findIndex` except that it iterates over elements of `collection` from right to left.

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array to inspect."></x-field>
<x-field data-name="[predicate=_.identity]" data-type="Function" data-required="false" data-desc="The function invoked per iteration."></x-field>
<x-field data-name="[fromIndex=array.length-1]" data-type="number" data-required="false" data-desc="The index to search from."></x-field>

**Returns**

<x-field data-name="" data-type="number" data-desc="Returns the index of the found element, else `-1`."></x-field>

**Example**

```javascript
var users = [
  { 'user': 'barney',  'active': true },
  { 'user': 'fred',    'active': false },
  { 'user': 'pebbles', 'active': false }
];

_.findLastIndex(users, function(o) { return o.user == 'pebbles'; });
// => 2
```

### flatten

Flattens `array` a single level deep.

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array to flatten."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns the new flattened array."></x-field>

**Example**

```javascript
_.flatten([1, [2, [3, [4]], 5]]);
// => [1, 2, [3, [4]], 5]
```

### flattenDeep

Recursively flattens `array`.

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array to flatten."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns the new flattened array."></x-field>

**Example**

```javascript
_.flattenDeep([1, [2, [3, [4]], 5]]);
// => [1, 2, 3, 4, 5]
```

### flattenDepth

Recursively flatten `array` up to `depth` times.

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array to flatten."></x-field>
<x-field data-name="[depth=1]" data-type="number" data-required="false" data-desc="The maximum recursion depth."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns the new flattened array."></x-field>

**Example**

```javascript
var array = [1, [2, [3, [4]], 5]];

_.flattenDepth(array, 1);
// => [1, 2, [3, [4]], 5]

_.flattenDepth(array, 2);
// => [1, 2, 3, [4], 5]
```

### fromPairs

The inverse of `_.toPairs`; this method returns an object composed from key-value `pairs`.

**Parameters**

<x-field data-name="pairs" data-type="Array" data-required="true" data-desc="The key-value pairs."></x-field>

**Returns**

<x-field data-name="" data-type="Object" data-desc="Returns the new object."></x-field>

**Example**

```javascript
_.fromPairs([['a', 1], ['b', 2]]);
// => { 'a': 1, 'b': 2 }
```

### head

Gets the first element of `array`.

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array to query."></x-field>

**Returns**

<x-field data-name="" data-type="*" data-desc="Returns the first element of `array`."></x-field>

**Example**

```javascript
_.head([1, 2, 3]);
// => 1

_.head([]);
// => undefined
```

### indexOf

Gets the index at which the first occurrence of `value` is found in `array` using [`SameValueZero`](http://ecma-international.org/ecma-262/7.0/#sec-samevaluezero) for equality comparisons. If `fromIndex` is negative, it's used as the offset from the end of `array`.

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array to inspect."></x-field>
<x-field data-name="value" data-type="*" data-required="true" data-desc="The value to search for."></x-field>
<x-field data-name="[fromIndex=0]" data-type="number" data-required="false" data-desc="The index to search from."></x-field>

**Returns**

<x-field data-name="" data-type="number" data-desc="Returns the index of the matched value, else `-1`."></x-field>

**Example**

```javascript
_.indexOf([1, 2, 1, 2], 2);
// => 1

// Search from the `fromIndex`.
_.indexOf([1, 2, 1, 2], 2, 2);
// => 3
```

### initial

Gets all but the last element of `array`.

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array to query."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns the slice of `array`."></x-field>

**Example**

```javascript
_.initial([1, 2, 3]);
// => [1, 2]
```

### intersection

Creates an array of unique values that are included in all given arrays using [`SameValueZero`](http://ecma-international.org/ecma-262/7.0/#sec-samevaluezero) for equality comparisons. The order and references of result values are determined by the first array.

**Parameters**

<x-field data-name="[arrays]" data-type="...Array" data-required="true" data-desc="The arrays to inspect."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns the new array of intersecting values."></x-field>

**Example**

```javascript
_.intersection([2, 1], [2, 3]);
// => [2]
```

### join

Converts all elements in `array` into a string separated by `separator`.

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array to convert."></x-field>
<x-field data-name="[separator=',']" data-type="string" data-required="false" data-desc="The element separator."></x-field>

**Returns**

<x-field data-name="" data-type="string" data-desc="Returns the joined string."></x-field>

**Example**

```javascript
_.join(['a', 'b', 'c'], '~');
// => 'a~b~c'
```

### last

Gets the last element of `array`.

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array to query."></x-field>

**Returns**

<x-field data-name="" data-type="*" data-desc="Returns the last element of `array`."></x-field>

**Example**

```javascript
_.last([1, 2, 3]);
// => 3
```

### lastIndexOf

This method is like `_.indexOf` except that it iterates over elements of `array` from right to left.

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array to inspect."></x-field>
<x-field data-name="value" data-type="*" data-required="true" data-desc="The value to search for."></x-field>
<x-field data-name="[fromIndex=array.length-1]" data-type="number" data-required="false" data-desc="The index to search from."></x-field>

**Returns**

<x-field data-name="" data-type="number" data-desc="Returns the index of the matched value, else `-1`."></x-field>

**Example**

```javascript
_.lastIndexOf([1, 2, 1, 2], 2);
// => 3

// Search from the `fromIndex`.
_.lastIndexOf([1, 2, 1, 2], 2, 2);
// => 1
```

### nth

Gets the element at index `n` of `array`. If `n` is negative, the nth element from the end is returned.

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array to query."></x-field>
<x-field data-name="[n=0]" data-type="number" data-required="false" data-desc="The index of the element to return."></x-field>

**Returns**

<x-field data-name="" data-type="*" data-desc="Returns the nth element of `array`."></x-field>

**Example**

```javascript
var array = ['a', 'b', 'c', 'd'];

_.nth(array, 1);
// => 'b'

_.nth(array, -2);
// => 'c';
```

### pull

Removes all given values from `array` using [`SameValueZero`](http://ecma-international.org/ecma-262/7.0/#sec-samevaluezero) for equality comparisons.

**Note:** This method mutates `array`.

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array to modify."></x-field>
<x-field data-name="[values]" data-type="...*" data-required="false" data-desc="The values to remove."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns `array`."></x-field>

**Example**

```javascript
var array = ['a', 'b', 'c', 'a', 'b', 'c'];

_.pull(array, 'a', 'c');
console.log(array);
// => ['b', 'b']
```

### pullAll

This method is like `_.pull` except that it accepts an array of values to remove.

**Note:** This method mutates `array`.

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array to modify."></x-field>
<x-field data-name="values" data-type="Array" data-required="true" data-desc="The values to remove."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns `array`."></x-field>

**Example**

```javascript
var array = ['a', 'b', 'c', 'a', 'b', 'c'];

_.pullAll(array, ['a', 'c']);
console.log(array);
// => ['b', 'b']
```

### pullAllBy

This method is like `_.pullAll` except that it accepts `iteratee` which is invoked for each element of `array` and `values` to generate the criterion by which they're compared. The iteratee is invoked with one argument: (value).

**Note:** This method mutates `array`.

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array to modify."></x-field>
<x-field data-name="values" data-type="Array" data-required="true" data-desc="The values to remove."></x-field>
<x-field data-name="[iteratee=_.identity]" data-type="Function" data-required="false" data-desc="The iteratee invoked per element."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns `array`."></x-field>

**Example**

```javascript
var array = [{ 'x': 1 }, { 'x': 2 }, { 'x': 3 }, { 'x': 1 }];

_.pullAllBy(array, [{ 'x': 1 }, { 'x': 3 }], 'x');
console.log(array);
// => [{ 'x': 2 }]
```

### pullAllWith

This method is like `_.pullAll` except that it accepts `comparator` which is invoked to compare elements of `array` to `values`. The comparator is invoked with two arguments: (arrVal, othVal).

**Note:** This method mutates `array`.

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array to modify."></x-field>
<x-field data-name="values" data-type="Array" data-required="true" data-desc="The values to remove."></x-field>
<x-field data-name="[comparator]" data-type="Function" data-required="false" data-desc="The comparator invoked per element."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns `array`."></x-field>

**Example**

```javascript
var array = [{ 'x': 1, 'y': 2 }, { 'x': 3, 'y': 4 }, { 'x': 5, 'y': 6 }];

_.pullAllWith(array, [{ 'x': 3, 'y': 4 }], _.isEqual);
console.log(array);
// => [{ 'x': 1, 'y': 2 }, { 'x': 5, 'y': 6 }]
```

### pullAt

Removes elements from `array` corresponding to `indexes` and returns an array of removed elements.

**Note:** This method mutates `array`.

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array to modify."></x-field>
<x-field data-name="[indexes]" data-type="...(number|number[])" data-required="false" data-desc="The indexes of elements to remove."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns the new array of removed elements."></x-field>

**Example**

```javascript
var array = ['a', 'b', 'c', 'd'];
var pulled = _.pullAt(array, [1, 3]);

console.log(array);
// => ['a', 'c']

console.log(pulled);
// => ['b', 'd']
```

### remove

Removes all elements from `array` that `predicate` returns truthy for and returns an array of the removed elements. The predicate is invoked with three arguments: (value, index, array).

**Note:** This method mutates `array`.

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array to modify."></x-field>
<x-field data-name="[predicate=_.identity]" data-type="Function" data-required="false" data-desc="The function invoked per iteration."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns the new array of removed elements."></x-field>

**Example**

```javascript
var array = [1, 2, 3, 4];
var evens = _.remove(array, function(n) {
  return n % 2 == 0;
});

console.log(array);
// => [1, 3]

console.log(evens);
// => [2, 4]
```

### reverse

Reverses `array` so that the first element becomes the last, the second element becomes the second to last, and so on.

**Note:** This method mutates `array` and is based on [`Array#reverse`](https://mdn.io/Array/reverse).

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array to modify."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns `array`."></x-field>

**Example**

```javascript
var array = [1, 2, 3];

_.reverse(array);
// => [3, 2, 1]

console.log(array);
// => [3, 2, 1]
```

### slice

Creates a slice of `array` from `start` up to, but not including, `end`.

**Note:** This method is used instead of `Array#slice` to ensure dense arrays are returned.

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array to slice."></x-field>
<x-field data-name="[start=0]" data-type="number" data-required="false" data-desc="The start position."></x-field>
<x-field data-name="[end=array.length]" data-type="number" data-required="false" data-desc="The end position."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns the slice of `array`."></x-field>

### sortedIndex

Uses a binary search to determine the lowest index at which `value` should be inserted into `array` in order to maintain its sort order.

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The sorted array to inspect."></x-field>
<x-field data-name="value" data-type="*" data-required="true" data-desc="The value to evaluate."></x-field>

**Returns**

<x-field data-name="" data-type="number" data-desc="Returns the index at which `value` should be inserted into `array`."></x-field>

**Example**

```javascript
_.sortedIndex([30, 50], 40);
// => 1
```

### sortedIndexBy

This method is like `_.sortedIndex` except that it accepts `iteratee` which is invoked for `value` and each element of `array` to compute their sort ranking. The iteratee is invoked with one argument: (value).

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The sorted array to inspect."></x-field>
<x-field data-name="value" data-type="*" data-required="true" data-desc="The value to evaluate."></x-field>
<x-field data-name="[iteratee=_.identity]" data-type="Function" data-required="false" data-desc="The iteratee invoked per element."></x-field>

**Returns**

<x-field data-name="" data-type="number" data-desc="Returns the index at which `value` should be inserted into `array`."></x-field>

**Example**

```javascript
var objects = [{ 'x': 4 }, { 'x': 5 }];

_.sortedIndexBy(objects, { 'x': 4 }, function(o) { return o.x; });
// => 0
```

### sortedIndexOf

This method is like `_.indexOf` except that it performs a binary search on a sorted `array`.

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array to inspect."></x-field>
<x-field data-name="value" data-type="*" data-required="true" data-desc="The value to search for."></x-field>

**Returns**

<x-field data-name="" data-type="number" data-desc="Returns the index of the matched value, else `-1`."></x-field>

**Example**

```javascript
_.sortedIndexOf([4, 5, 5, 5, 6], 5);
// => 1
```

### sortedLastIndex

This method is like `_.sortedIndex` except that it returns the highest index at which `value` should be inserted into `array` in order to maintain its sort order.

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The sorted array to inspect."></x-field>
<x-field data-name="value" data-type="*" data-required="true" data-desc="The value to evaluate."></x-field>

**Returns**

<x-field data-name="" data-type="number" data-desc="Returns the index at which `value` should be inserted into `array`."></x-field>

**Example**

```javascript
_.sortedLastIndex([4, 5, 5, 5, 6], 5);
// => 4
```

### sortedLastIndexBy

This method is like `_.sortedLastIndex` except that it accepts `iteratee` which is invoked for `value` and each element of `array` to compute their sort ranking. The iteratee is invoked with one argument: (value).

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The sorted array to inspect."></x-field>
<x-field data-name="value" data-type="*" data-required="true" data-desc="The value to evaluate."></x-field>
<x-field data-name="[iteratee=_.identity]" data-type="Function" data-required="false" data-desc="The iteratee invoked per element."></x-field>

**Returns**

<x-field data-name="" data-type="number" data-desc="Returns the index at which `value` should be inserted into `array`."></x-field>

**Example**

```javascript
var objects = [{ 'x': 4 }, { 'x': 5 }];

_.sortedLastIndexBy(objects, { 'x': 4 }, function(o) { return o.x; });
// => 1
```

### sortedLastIndexOf

This method is like `_.lastIndexOf` except that it performs a binary search on a sorted `array`.

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array to inspect."></x-field>
<x-field data-name="value" data-type="*" data-required="true" data-desc="The value to search for."></x-field>

**Returns**

<x-field data-name="" data-type="number" data-desc="Returns the index of the matched value, else `-1`."></x-field>

**Example**

```javascript
_.sortedLastIndexOf([4, 5, 5, 5, 6], 5);
// => 3
```

### sortedUniq

This method is like `_.uniq` except that it's designed and optimized for sorted arrays.

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array to inspect."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns the new duplicate free array."></x-field>

**Example**

```javascript
_.sortedUniq([1, 1, 2]);
// => [1, 2]
```

### sortedUniqBy

This method is like `_.uniqBy` except that it's designed and optimized for sorted arrays.

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array to inspect."></x-field>
<x-field data-name="[iteratee]" data-type="Function" data-required="false" data-desc="The iteratee invoked per element."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns the new duplicate free array."></x-field>

**Example**

```javascript
_.sortedUniqBy([1.1, 1.2, 2.3, 2.4], Math.floor);
// => [1.1, 2.3]
```

### tail

Gets all but the first element of `array`.

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array to query."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns the slice of `array`."></x-field>

**Example**

```javascript
_.tail([1, 2, 3]);
// => [2, 3]
```

### take

Creates a slice of `array` with `n` elements taken from the beginning.

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array to query."></x-field>
<x-field data-name="[n=1]" data-type="number" data-required="false" data-desc="The number of elements to take."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns the slice of `array`."></x-field>

**Example**

```javascript
_.take([1, 2, 3]);
// => [1]

_.take([1, 2, 3], 2);
// => [1, 2]
```

### takeRight

Creates a slice of `array` with `n` elements taken from the end.

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array to query."></x-field>
<x-field data-name="[n=1]" data-type="number" data-required="false" data-desc="The number of elements to take."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns the slice of `array`."></x-field>

**Example**

```javascript
_.takeRight([1, 2, 3]);
// => [3]

_.takeRight([1, 2, 3], 2);
// => [2, 3]
```

### takeRightWhile

Creates a slice of `array` with elements taken from the end. Elements are taken until `predicate` returns falsey.

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array to query."></x-field>
<x-field data-name="[predicate=_.identity]" data-type="Function" data-required="false" data-desc="The function invoked per iteration."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns the slice of `array`."></x-field>

**Example**

```javascript
var users = [
  { 'user': 'barney',  'active': true },
  { 'user': 'fred',    'active': false },
  { 'user': 'pebbles', 'active': false }
];

_.takeRightWhile(users, function(o) { return !o.active; });
// => objects for ['fred', 'pebbles']
```

### takeWhile

Creates a slice of `array` with elements taken from the beginning. Elements are taken until `predicate` returns falsey.

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array to query."></x-field>
<x-field data-name="[predicate=_.identity]" data-type="Function" data-required="false" data-desc="The function invoked per iteration."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns the slice of `array`."></x-field>

**Example**

```javascript
var users = [
  { 'user': 'barney',  'active': false },
  { 'user': 'fred',    'active': false },
  { 'user': 'pebbles', 'active': true }
];

_.takeWhile(users, function(o) { return !o.active; });
// => objects for ['barney', 'fred']
```

### union

Creates an array of unique values, in order, from all given arrays using [`SameValueZero`](http://ecma-international.org/ecma-262/7.0/#sec-samevaluezero) for equality comparisons.

**Parameters**

<x-field data-name="[arrays]" data-type="...Array" data-required="true" data-desc="The arrays to inspect."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns the new array of combined values."></x-field>

**Example**

```javascript
_.union([2], [1, 2]);
// => [2, 1]
```

### unionBy

This method is like `_.union` except that it accepts `iteratee` which is invoked for each element of each `arrays` to generate the criterion by which uniqueness is computed.

**Parameters**

<x-field data-name="[arrays]" data-type="...Array" data-required="true" data-desc="The arrays to inspect."></x-field>
<x-field data-name="[iteratee=_.identity]" data-type="Function" data-required="false" data-desc="The iteratee invoked per element."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns the new array of combined values."></x-field>

**Example**

```javascript
_.unionBy([2.1], [1.2, 2.3], Math.floor);
// => [2.1, 1.2]
```

### unionWith

This method is like `_.union` except that it accepts `comparator` which is invoked to compare elements of `arrays`.

**Parameters**

<x-field data-name="[arrays]" data-type="...Array" data-required="true" data-desc="The arrays to inspect."></x-field>
<x-field data-name="[comparator]" data-type="Function" data-required="false" data-desc="The comparator invoked per element."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns the new array of combined values."></x-field>

**Example**

```javascript
var objects = [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }];
var others = [{ 'x': 1, 'y': 1 }, { 'x': 1, 'y': 2 }];

_.unionWith(objects, others, _.isEqual);
// => [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }, { 'x': 1, 'y': 1 }]
```

### uniq

Creates a duplicate-free version of an array, using [`SameValueZero`](http://ecma-international.org/ecma-262/7.0/#sec-samevaluezero) for equality comparisons, in which only the first occurrence of each element is kept.

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array to inspect."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns the new duplicate free array."></x-field>

**Example**

```javascript
_.uniq([2, 1, 2]);
// => [2, 1]
```

### uniqBy

This method is like `_.uniq` except that it accepts `iteratee` which is invoked for each element in `array` to generate the criterion by which uniqueness is computed.

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array to inspect."></x-field>
<x-field data-name="[iteratee=_.identity]" data-type="Function" data-required="false" data-desc="The iteratee invoked per element."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns the new duplicate free array."></x-field>

**Example**

```javascript
_.uniqBy([2.1, 1.2, 2.3], Math.floor);
// => [2.1, 1.2]
```

### uniqWith

This method is like `_.uniq` except that it accepts `comparator` which is invoked to compare elements of `array`.

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array to inspect."></x-field>
<x-field data-name="[comparator]" data-type="Function" data-required="false" data-desc="The comparator invoked per element."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns the new duplicate free array."></x-field>

**Example**

```javascript
var objects = [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }, { 'x': 1, 'y': 2 }];

_.uniqWith(objects, _.isEqual);
// => [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }]
```

### unzip

This method is like `_.zip` except that it accepts an array of grouped elements and creates an array regrouping the elements to their pre-zip configuration.

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array of grouped elements to process."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns the new array of regrouped elements."></x-field>

**Example**

```javascript
var zipped = _.zip(['a', 'b'], [1, 2], [true, false]);
// => [['a', 1, true], ['b', 2, false]]

_.unzip(zipped);
// => [['a', 'b'], [1, 2], [true, false]]
```

### unzipWith

This method is like `_.unzip` except that it accepts `iteratee` to specify how regrouped values should be combined.

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array of grouped elements to process."></x-field>
<x-field data-name="[iteratee=_.identity]" data-type="Function" data-required="false" data-desc="The function to combine regrouped values."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns the new array of regrouped elements."></x-field>

**Example**

```javascript
var zipped = _.zip([1, 2], [10, 20], [100, 200]);
// => [[1, 10, 100], [2, 20, 200]]

_.unzipWith(zipped, _.add);
// => [3, 30, 300]
```

### without

Creates an array excluding all given values using [`SameValueZero`](http://ecma-international.org/ecma-262/7.0/#sec-samevaluezero) for equality comparisons.

**Note:** Unlike `_.pull`, this method returns a new array.

**Parameters**

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array to inspect."></x-field>
<x-field data-name="[values]" data-type="...*" data-required="false" data-desc="The values to exclude."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns the new array of filtered values."></x-field>

**Example**

```javascript
_.without([2, 1, 2, 3], 1, 2);
// => [3]
```

### xor

Creates an array of unique values that is the [symmetric difference](https://en.wikipedia.org/wiki/Symmetric_difference) of the given arrays.

**Parameters**

<x-field data-name="[arrays]" data-type="...Array" data-required="true" data-desc="The arrays to inspect."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns the new array of filtered values."></x-field>

**Example**

```javascript
_.xor([2, 1], [2, 3]);
// => [1, 3]
```

### xorBy

This method is like `_.xor` except that it accepts `iteratee` which is invoked for each element of each `arrays` to generate the criterion by which they're compared.

**Parameters**

<x-field data-name="[arrays]" data-type="...Array" data-required="true" data-desc="The arrays to inspect."></x-field>
<x-field data-name="[iteratee=_.identity]" data-type="Function" data-required="false" data-desc="The iteratee invoked per element."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns the new array of filtered values."></x-field>

**Example**

```javascript
_.xorBy([2.1, 1.2], [2.3, 3.4], Math.floor);
// => [1.2, 3.4]
```

### xorWith

This method is like `_.xor` except that it accepts `comparator` which is invoked to compare elements of `arrays`.

**Parameters**

<x-field data-name="[arrays]" data-type="...Array" data-required="true" data-desc="The arrays to inspect."></x-field>
<x-field data-name="[comparator]" data-type="Function" data-required="false" data-desc="The comparator invoked per element."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns the new array of filtered values."></x-field>

**Example**

```javascript
var objects = [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }];
var others = [{ 'x': 1, 'y': 1 }, { 'x': 1, 'y': 2 }];

_.xorWith(objects, others, _.isEqual);
// => [{ 'x': 2, 'y': 1 }, { 'x': 1, 'y': 1 }]
```

### zip

Creates an array of grouped elements, the first of which contains the first elements of the given arrays, the second of which contains the second elements of the given arrays, and so on.

**Parameters**

<x-field data-name="[arrays]" data-type="...Array" data-required="true" data-desc="The arrays to process."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns the new array of grouped elements."></x-field>

**Example**

```javascript
_.zip(['a', 'b'], [1, 2], [true, false]);
// => [['a', 1, true], ['b', 2, false]]
```

### zipObject

This method is like `_.fromPairs` except that it accepts two arrays, one of property identifiers and one of corresponding values.

**Parameters**

<x-field data-name="[props=[]]" data-type="Array" data-required="false" data-desc="The property identifiers."></x-field>
<x-field data-name="[values=[]]" data-type="Array" data-required="false" data-desc="The property values."></x-field>

**Returns**

<x-field data-name="" data-type="Object" data-desc="Returns the new object."></x-field>

**Example**

```javascript
_.zipObject(['a', 'b'], [1, 2]);
// => { 'a': 1, 'b': 2 }
```

### zipObjectDeep

This method is like `_.zipObject` except that it supports property paths.

**Parameters**

<x-field data-name="[props=[]]" data-type="Array" data-required="false" data-desc="The property identifiers."></x-field>
<x-field data-name="[values=[]]" data-type="Array" data-required="false" data-desc="The property values."></x-field>

**Returns**

<x-field data-name="" data-type="Object" data-desc="Returns the new object."></x-field>

**Example**

```javascript
_.zipObjectDeep(['a.b[0].c', 'a.b[1].d'], [1, 2]);
// => { 'a': { 'b': [{ 'c': 1 }, { 'd': 2 }] } }
```

### zipWith

This method is like `_.zip` except that it accepts `iteratee` to specify how grouped values should be combined. The iteratee is invoked with the elements of each group: (...group).

**Parameters**

<x-field data-name="[arrays]" data-type="...Array" data-required="true" data-desc="The arrays to process."></x-field>
<x-field data-name="[iteratee=_.identity]" data-type="Function" data-required="false" data-desc="The function to combine grouped values."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns the new array of grouped elements."></x-field>

**Example**

```javascript
_.zipWith([1, 2], [10, 20], [100, 200], function(a, b, c) {
  return a + b + c;
});
// => [111, 222]
```
