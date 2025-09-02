# Array

Lodash provides a powerful set of array manipulation functions that simplify and enhance native JavaScript array operations. These functions cover various common scenarios such as creating, splitting, filtering, merging, finding, and sorting arrays. Many functions support deep operations and custom comparators, providing great convenience for complex data processing.

This chapter details all Lodash functions that are specifically for manipulating or returning arrays. For iteration functions that apply to both arrays and objects, please refer to the [Collection](./api-collection.md) section.

## Function Reference

For easy reference, all array functions are listed in alphabetical order.

### _.chunk(array, [size=1])

Splits an `array` into chunks of `size` length and groups them into a new array. If the `array` cannot be split evenly, the final chunk will contain the remaining elements.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to process. |
| `[size=1]` | `number` | The length of each chunk. |

**Returns**

| Type | Description |
|---|---|
| `Array` | Returns the new array of chunks. |

**Example**

```javascript
_.chunk(['a', 'b', 'c', 'd'], 2);
// => [['a', 'b'], ['c', 'd']]
 
_.chunk(['a', 'b', 'c', 'd'], 3);
// => [['a', 'b', 'c'], ['d']]
```

### _.compact(array)

Creates a new array with all falsy values removed. For example, `false`, `null`, `0`, `""`, `undefined`, and `NaN` are considered "falsy" values.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to process. |

**Returns**

| Type | Description |
|---|---|
| `Array` | Returns the new array of filtered values. |

**Example**

```javascript
_.compact([0, 1, false, 2, '', 3]);
// => [1, 2, 3]
```

### _.concat(array, ...[values])

Creates a new array by concatenating `array` with any additional arrays or values.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to concatenate. |
| `...[values]`| `*` | The values to concatenate. |

**Returns**

| Type | Description |
|---|---|
| `Array` | Returns the new concatenated array. |

**Example**

```javascript
var array = [1];
var other = _.concat(array, 2, [3], [[4]]);
 
console.log(other);
// => [1, 2, 3, [4]]
 
console.log(array);
// => [1]
```

### _.difference(array, ...[values])

Creates an array of `array` values not included in the other given `values` arrays. The order and references of result values are determined by the first array.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to inspect. |
| `...[values]`| `Array` | The arrays of values to exclude. |

**Returns**

| Type | Description |
|---|---|
| `Array` | Returns the new array of filtered values. |

**Example**

```javascript
_.difference([2, 1], [2, 3]);
// => [1]
```

### _.differenceBy(array, ...[values], [iteratee=_.identity])

This method is like `_.difference` except that it accepts an `iteratee` which is invoked for each element of `array` and `values` to generate the criterion by which they're compared. The order and references of result values are determined by the first array.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to inspect. |
| `...[values]`| `Array` | The arrays of values to exclude. |
| `[iteratee=_.identity]`| `Function` | The iteratee invoked per element. |

**Returns**

| Type | Description |
|---|---|
| `Array` | Returns the new array of filtered values. |

**Example**

```javascript
_.differenceBy([2.1, 1.2], [2.3, 3.4], Math.floor);
// => [1.2]
 
// The `_.property` iteratee shorthand.
_.differenceBy([{ 'x': 2 }, { 'x': 1 }], [{ 'x': 1 }], 'x');
// => [{ 'x': 2 }]
```

### _.differenceWith(array, ...[values], [comparator])

This method is like `_.difference` except that it accepts a `comparator` which is invoked to compare elements of `array` to `values`. The order and references of result values are determined by the first array. The comparator is invoked with two arguments: `(arrVal, othVal)`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to inspect. |
| `...[values]`| `Array` | The arrays of values to exclude. |
| `[comparator]`| `Function` | The comparator invoked per element. |

**Returns**

| Type | Description |
|---|---|
| `Array` | Returns the new array of filtered values. |

**Example**

```javascript
var objects = [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }];
 
_.differenceWith(objects, [{ 'x': 1, 'y': 2 }], _.isEqual);
// => [{ 'x': 2, 'y': 1 }]
```

### _.drop(array, [n=1])

Creates a slice of `array` with `n` elements dropped from the beginning.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to query. |
| `[n=1]` | `number` | The number of elements to drop. |

**Returns**

| Type | Description |
|---|---|
| `Array` | Returns the slice of `array`. |

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

### _.dropRight(array, [n=1])

Creates a slice of `array` with `n` elements dropped from the end.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to query. |
| `[n=1]` | `number` | The number of elements to drop. |

**Returns**

| Type | Description |
|---|---|
| `Array` | Returns the slice of `array`. |

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

### _.fill(array, value, [start=0], [end=array.length])

Fills elements of `array` with `value` from `start` up to, but not including, `end`.

**Note:** This method mutates `array`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to fill. |
| `value` | `*` | The value to fill `array` with. |
| `[start=0]` | `number` | The start position. |
| `[end=array.length]` | `number` | The end position. |

**Returns**

| Type | Description |
|---|---|
| `Array` | Returns `array`. |

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

### _.findIndex(array, [predicate=_.identity], [fromIndex=0])

This method is like `_.find` except that it returns the index of the first element `predicate` returns truthy for instead of the element itself.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to inspect. |
| `[predicate=_.identity]` | `Function` | The function invoked per iteration. |
| `[fromIndex=0]` | `number` | The index to search from. |

**Returns**

| Type | Description |
|---|---|
| `number` | Returns the index of the found element, else `-1`. |

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

### _.findLastIndex(array, [predicate=_.identity], [fromIndex=array.length-1])

This method is like `_.findIndex` except that it iterates over elements of `collection` from right to left.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to inspect. |
| `[predicate=_.identity]` | `Function` | The function invoked per iteration. |
| `[fromIndex=array.length-1]` | `number` | The index to search from. |

**Returns**

| Type | Description |
|---|---|
| `number` | Returns the index of the found element, else `-1`. |

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

### _.flatten(array)

Flattens `array` a single level deep.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to flatten. |

**Returns**

| Type | Description |
|---|---|
| `Array` | Returns the new flattened array. |

**Example**

```javascript
_.flatten([1, [2, [3, [4]], 5]]);
// => [1, 2, [3, [4]], 5]
```

### _.flattenDeep(array)

Recursively flattens `array`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to flatten. |

**Returns**

| Type | Description |
|---|---|
| `Array` | Returns the new flattened array. |

**Example**

```javascript
_.flattenDeep([1, [2, [3, [4]], 5]]);
// => [1, 2, 3, 4, 5]
```

### _.flattenDepth(array, [depth=1])

Recursively flattens `array` up to `depth` times.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to flatten. |
| `[depth=1]` | `number` | The maximum recursion depth. |

**Returns**

| Type | Description |
|---|---|
| `Array` | Returns the new flattened array. |

**Example**

```javascript
var array = [1, [2, [3, [4]], 5]];
 
_.flattenDepth(array, 1);
// => [1, 2, [3, [4]], 5]
 
_.flattenDepth(array, 2);
// => [1, 2, 3, [4], 5]
```

### _.fromPairs(pairs)

The inverse of `_.toPairs`; this method returns an object composed from key-value `pairs`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `pairs` | `Array` | The key-value pairs. |

**Returns**

| Type | Description |
|---|---|
| `Object` | Returns the new object. |

**Example**

```javascript
_.fromPairs([['a', 1], ['b', 2]]);
// => { 'a': 1, 'b': 2 }
```

### _.head(array)

Gets the first element of `array`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to query. |

**Returns**

| Type | Description |
|---|---|
| `*` | Returns the first element of the array. |

**Example**

```javascript
_.head([1, 2, 3]);
// => 1
 
_.head([]);
// => undefined
```

### _.indexOf(array, value, [fromIndex=0])

Gets the index at which the first occurrence of `value` is found in `array` using `SameValueZero` for equality comparisons.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to inspect. |
| `value` | `*` | The value to search for. |
| `[fromIndex=0]` | `number` | The index to search from. |

**Returns**

| Type | Description |
|---|---|
| `number` | Returns the index of the matched value, else `-1`. |

**Example**

```javascript
_.indexOf([1, 2, 1, 2], 2);
// => 1
 
// Search from the `fromIndex`.
_.indexOf([1, 2, 1, 2], 2, 2);
// => 3
```

### _.initial(array)

Gets all but the last element of `array`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to query. |

**Returns**

| Type | Description |
|---|---|
| `Array` | Returns the slice of `array`. |

**Example**

```javascript
_.initial([1, 2, 3]);
// => [1, 2]
```

### _.intersection(...[arrays])

Creates an array of unique values that are included in all given arrays. The order and references of result values are determined by the first array.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `...[arrays]` | `Array` | The arrays to inspect. |

**Returns**

| Type | Description |
|---|---|
| `Array` | Returns the new array of intersecting values. |

**Example**

```javascript
_.intersection([2, 1], [2, 3]);
// => [2]
```

### _.join(array, [separator=','])

Converts all elements in `array` into a string separated by `separator`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to convert. |
| `[separator=',']` | `string` | The element separator. |

**Returns**

| Type | Description |
|---|---|
| `string` | Returns the joined string. |

**Example**

```javascript
_.join(['a', 'b', 'c'], '~');
// => 'a~b~c'
```

### _.last(array)

Gets the last element of `array`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to query. |

**Returns**

| Type | Description |
|---|---|
| `*` | Returns the last element of `array`. |

**Example**

```javascript
_.last([1, 2, 3]);
// => 3
```

### _.lastIndexOf(array, value, [fromIndex=array.length-1])

This method is like `_.indexOf` except that it iterates over elements of `array` from right to left.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to inspect. |
| `value` | `*` | The value to search for. |
| `[fromIndex=array.length-1]` | `number` | The index to search from. |

**Returns**

| Type | Description |
|---|---|
| `number` | Returns the index of the matched value, else `-1`. |

**Example**

```javascript
_.lastIndexOf([1, 2, 1, 2], 2);
// => 3
```

### _.pull(array, ...[values])

Removes all given values from `array`.

**Note:** This method mutates `array`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to modify. |
| `...[values]` | `*` | The values to remove. |

**Returns**

| Type | Description |
|---|---|
| `Array` | Returns `array`. |

**Example**

```javascript
var array = ['a', 'b', 'c', 'a', 'b', 'c'];
 
_.pull(array, 'a', 'c');
console.log(array);
// => ['b', 'b']
```

### _.pullAll(array, values)

This method is like `_.pull` except that it accepts an array of values to remove.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to modify. |
| `values` | `Array` | The array of values to remove. |

**Returns**

| Type | Description |
|---|---|
| `Array` | Returns `array`. |

**Example**

```javascript
var array = ['a', 'b', 'c', 'a', 'b', 'c'];
 
_.pullAll(array, ['a', 'c']);
console.log(array);
// => ['b', 'b']
```

### _.reverse(array)

Reverses `array` so that the first element becomes the last, the second element becomes the second to last, and so on.

**Note:** This method mutates `array`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to modify. |

**Returns**

| Type | Description |
|---|---|
| `Array` | Returns `array`. |

**Example**

```javascript
var array = [1, 2, 3];
 
_.reverse(array);
// => [3, 2, 1]
 
console.log(array);
// => [3, 2, 1]
```

### _.slice(array, [start=0], [end=array.length])

Creates a slice of `array` from `start` up to, but not including, `end`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to slice. |
| `[start=0]` | `number` | The start position. |
| `[end=array.length]` | `number` | The end position. |

**Returns**

| Type | Description |
|---|---|
| `Array` | Returns the slice of `array`. |

**Example**

```javascript
var array = [1, 2, 3, 4];
_.slice(array, 1, 3);
// => [2, 3]
```

### _.sortedUniq(array)

This method is like `_.uniq` except that it's designed and optimized for sorted arrays.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to inspect. |

**Returns**

| Type | Description |
|---|---|
| `Array` | Returns the new duplicate free array. |

**Example**

```javascript
_.sortedUniq([1, 1, 2]);
// => [1, 2]
```

### _.tail(array)

Gets all but the first element of `array`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to query. |

**Returns**

| Type | Description |
|---|---|
| `Array` | Returns the slice of `array`. |

**Example**

```javascript
_.tail([1, 2, 3]);
// => [2, 3]
```

### _.take(array, [n=1])

Creates a slice of `array` with `n` elements taken from the beginning.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to query. |
| `[n=1]` | `number` | The number of elements to take. |

**Returns**

| Type | Description |
|---|---|
| `Array` | Returns the slice of `array`. |

**Example**

```javascript
_.take([1, 2, 3]);
// => [1]
```

### _.union(...[arrays])

Creates an array of unique values, in order, from all given arrays using `SameValueZero` for equality comparisons.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `...[arrays]` | `Array` | The arrays to inspect. |

**Returns**

| Type | Description |
|---|---|
| `Array` | Returns the new array of combined values. |

**Example**

```javascript
_.union([2], [1, 2]);
// => [2, 1]
```

### _.uniq(array)

Creates a duplicate-free version of an `array`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to inspect. |

**Returns**

| Type | Description |
|---|---|
| `Array` | Returns the new duplicate free array. |

**Example**

```javascript
_.uniq([2, 1, 2]);
// => [2, 1]
```

### _.unzip(array)

This method is like `_.zip` except that it accepts an array of grouped elements and creates an array regrouping the elements to their pre-zip configuration.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array of grouped elements to process. |

**Returns**

| Type | Description |
|---|---|
| `Array` | Returns the new array of regrouped elements. |

**Example**

```javascript
var zipped = _.zip(['a', 'b'], [1, 2], [true, false]);
// => [['a', 1, true], ['b', 2, false]]
 
_.unzip(zipped);
// => [['a', 'b'], [1, 2], [true, false]]
```

### _.without(array, ...[values])

Creates an array excluding all given values.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to inspect. |
| `...[values]` | `*` | The values to exclude. |

**Returns**

| Type | Description |
|---|---|
| `Array` | Returns the new array of filtered values. |

**Example**

```javascript
_.without([2, 1, 2, 3], 1, 2);
// => [3]
```

### _.xor(...[arrays])

Creates an array of unique values that is the symmetric difference of the given arrays.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `...[arrays]` | `Array` | The arrays to inspect. |

**Returns**

| Type | Description |
|---|---|
| `Array` | Returns the new array of filtered values. |

**Example**

```javascript
_.xor([2, 1], [2, 3]);
// => [1, 3]
```

### _.zip(...[arrays])

Creates an array of grouped elements, the first of which contains the first elements of the given arrays, the second of which contains the second elements of the given arrays, and so on.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `...[arrays]` | `Array` | The arrays to process. |

**Returns**

| Type | Description |
|---|---|
| `Array` | Returns the new array of grouped elements. |

**Example**

```javascript
_.zip(['a', 'b'], [1, 2], [true, false]);
// => [['a', 1, true], ['b', 2, false]]
```

---

This section covers the core array manipulation functions in Lodash. Many functions that handle arrays also work with other iterable data structures. To learn more, continue reading the documentation for the [Collection](./api-collection.md) section.
