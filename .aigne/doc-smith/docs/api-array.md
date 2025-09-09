# Array

Lodash provides a rich set of functions for manipulating arrays. These utilities help with common tasks like splitting, filtering, transforming, and querying array data. Many of these functions return new arrays, adhering to functional programming principles, while others mutate arrays in place for performance, which will be noted in their descriptions. For functions that iterate over arrays and other iterable types, see the [Collection](./api-collection.md) section.

### `_.chunk(array, [size=1])`

Creates an array of elements split into groups the length of `size`. If `array` can't be split evenly, the final chunk will be the remaining elements.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to process. |
| `[size=1]` | `number` | The length of each chunk. |

**Returns**

- `(Array)`: Returns the new array of chunks.

**Example**

```javascript
_.chunk(['a', 'b', 'c', 'd'], 2);
// => [['a', 'b'], ['c', 'd']]

_.chunk(['a', 'b', 'c', 'd'], 3);
// => [['a', 'b', 'c'], ['d']]
```

### `_.compact(array)`

Creates an array with all falsey values removed. The values `false`, `null`, `0`, `""`, `undefined`, and `NaN` are falsey.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to compact. |

**Returns**

- `(Array)`: Returns the new array of filtered values.

**Example**

```javascript
_.compact([0, 1, false, 2, '', 3]);
// => [1, 2, 3]
```

### `_.concat(array, ...[values])`

Creates a new array concatenating `array` with any additional arrays and/or values.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to concatenate. |
| `...[values]` | `*` | The values to concatenate. |

**Returns**

- `(Array)`: Returns the new concatenated array.

**Example**

```javascript
var array = [1];
var other = _.concat(array, 2, [3], [[4]]);

console.log(other);
// => [1, 2, 3, [4]]

console.log(array);
// => [1]
```

### `_.difference(array, ...[values])`

Creates an array of `array` values not included in the other given arrays using [`SameValueZero`](http://ecma-international.org/ecma-262/7.0/#sec-samevaluezero) for equality comparisons. The order and references of result values are determined by the first array.

**Note:** Unlike `_.pullAll`, this method returns a new array.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to inspect. |
| `...[values]` | `Array` | The values to exclude. |

**Returns**

- `(Array)`: Returns the new array of filtered values.

**Example**

```javascript
_.difference([2, 1], [2, 3]);
// => [1]
```

### `_.differenceBy(array, ...[values], [iteratee=_.identity])`

This method is like `_.difference` except that it accepts `iteratee` which is invoked for each element of `array` and `values` to generate the criterion by which they're compared. The order and references of result values are determined by the first array. The iteratee is invoked with one argument: (value).

**Note:** Unlike `_.pullAllBy`, this method returns a new array.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to inspect. |
| `...[values]` | `Array` | The values to exclude. |
| `[iteratee=_.identity]` | `Function` | The iteratee invoked per element. |

**Returns**

- `(Array)`: Returns the new array of filtered values.

**Example**

```javascript
_.differenceBy([2.1, 1.2], [2.3, 3.4], Math.floor);
// => [1.2]

// The `_.property` iteratee shorthand.
_.differenceBy([{ 'x': 2 }, { 'x': 1 }], [{ 'x': 1 }], 'x');
// => [{ 'x': 2 }]
```

### `_.differenceWith(array, ...[values], [comparator])`

This method is like `_.difference` except that it accepts `comparator` which is invoked to compare elements of `array` to `values`. The order and references of result values are determined by the first array. The comparator is invoked with two arguments: (arrVal, othVal).

**Note:** Unlike `_.pullAllWith`, this method returns a new array.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to inspect. |
| `...[values]` | `Array` | The values to exclude. |
| `[comparator]` | `Function` | The comparator invoked per element. |

**Returns**

- `(Array)`: Returns the new array of filtered values.

**Example**

```javascript
var objects = [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }];

_.differenceWith(objects, [{ 'x': 1, 'y': 2 }], _.isEqual);
// => [{ 'x': 2, 'y': 1 }]
```

### `_.drop(array, [n=1])`

Creates a slice of `array` with `n` elements dropped from the beginning.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to query. |
| `[n=1]` | `number` | The number of elements to drop. |

**Returns**

- `(Array)`: Returns the slice of `array`.

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

### `_.dropRight(array, [n=1])`

Creates a slice of `array` with `n` elements dropped from the end.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to query. |
| `[n=1]` | `number` | The number of elements to drop. |

**Returns**

- `(Array)`: Returns the slice of `array`.

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

### `_.fill(array, value, [start=0], [end=array.length])`

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

- `(Array)`: Returns `array`.

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

### `_.flatten(array)`

Flattens `array` a single level deep.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to flatten. |

**Returns**

- `(Array)`: Returns the new flattened array.

**Example**

```javascript
_.flatten([1, [2, [3, [4]], 5]]);
// => [1, 2, [3, [4]], 5]
```

### `_.flattenDeep(array)`

Recursively flattens `array`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to flatten. |

**Returns**

- `(Array)`: Returns the new flattened array.

**Example**

```javascript
_.flattenDeep([1, [2, [3, [4]], 5]]);
// => [1, 2, 3, 4, 5]
```

### `_.flattenDepth(array, [depth=1])`

Recursively flatten `array` up to `depth` times.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to flatten. |
| `[depth=1]` | `number` | The maximum recursion depth. |

**Returns**

- `(Array)`: Returns the new flattened array.

**Example**

```javascript
var array = [1, [2, [3, [4]], 5]];

_.flattenDepth(array, 1);
// => [1, 2, [3, [4]], 5]

_.flattenDepth(array, 2);
// => [1, 2, 3, [4], 5]
```

### `_.fromPairs(pairs)`

The inverse of `_.toPairs`; this method returns an object composed from key-value `pairs`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `pairs` | `Array` | The key-value pairs. |

**Returns**

- `(Object)`: Returns the new object.

**Example**

```javascript
_.fromPairs([['a', 1], ['b', 2]]);
// => { 'a': 1, 'b': 2 }
```

### `_.head(array)`

Gets the first element of `array`. Alias: `_.first`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to query. |

**Returns**

- `(*)`: Returns the first element of `array`.

**Example**

```javascript
_.head([1, 2, 3]);
// => 1

_.head([]);
// => undefined
```

### `_.indexOf(array, value, [fromIndex=0])`

Gets the index at which the first occurrence of `value` is found in `array` using [`SameValueZero`](http://ecma-international.org/ecma-262/7.0/#sec-samevaluezero) for equality comparisons. If `fromIndex` is negative, it's used as the offset from the end of `array`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to inspect. |
| `value` | `*` | The value to search for. |
| `[fromIndex=0]` | `number` | The index to search from. |

**Returns**

- `(number)`: Returns the index of the matched value, else `-1`.

**Example**

```javascript
_.indexOf([1, 2, 1, 2], 2);
// => 1

// Search from the `fromIndex`.
_.indexOf([1, 2, 1, 2], 2, 2);
// => 3
```

### `_.initial(array)`

Gets all but the last element of `array`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to query. |

**Returns**

- `(Array)`: Returns the slice of `array`.

**Example**

```javascript
_.initial([1, 2, 3]);
// => [1, 2]
```

### `_.intersection(...[arrays])`

Creates an array of unique values that are included in all given arrays using [`SameValueZero`](http://ecma-international.org/ecma-262/7.0/#sec-samevaluezero) for equality comparisons. The order and references of result values are determined by the first array.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `...[arrays]` | `Array` | The arrays to inspect. |

**Returns**

- `(Array)`: Returns the new array of intersecting values.

**Example**

```javascript
_.intersection([2, 1], [2, 3]);
// => [2]
```

### `_.join(array, [separator=','])`

Converts all elements in `array` into a string separated by `separator`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to convert. |
| `[separator=',']` | `string` | The element separator. |

**Returns**

- `(string)`: Returns the joined string.

**Example**

```javascript
_.join(['a', 'b', 'c'], '~');
// => 'a~b~c'
```

### `_.last(array)`

Gets the last element of `array`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to query. |

**Returns**

- `(*)`: Returns the last element of `array`.

**Example**

```javascript
_.last([1, 2, 3]);
// => 3
```

### `_.lastIndexOf(array, value, [fromIndex=array.length-1])`

This method is like `_.indexOf` except that it iterates over elements of `array` from right to left.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to inspect. |
| `value` | `*` | The value to search for. |
| `[fromIndex=array.length-1]` | `number` | The index to search from. |

**Returns**

- `(number)`: Returns the index of the matched value, else `-1`.

**Example**

```javascript
_.lastIndexOf([1, 2, 1, 2], 2);
// => 3

// Search from the `fromIndex`.
_.lastIndexOf([1, 2, 1, 2], 2, 2);
// => 1
```

### `_.pull(array, ...[values])`

Removes all given values from `array` using [`SameValueZero`](http://ecma-international.org/ecma-262/7.0/#sec-samevaluezero) for equality comparisons.

**Note:** This method mutates `array`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to modify. |
| `...[values]` | `*` | The values to remove. |

**Returns**

- `(Array)`: Returns `array`.

**Example**

```javascript
var array = ['a', 'b', 'c', 'a', 'b', 'c'];

_.pull(array, 'a', 'c');
console.log(array);
// => ['b', 'b']
```

### `_.reverse(array)`

Reverses `array` so that the first element becomes the last, the second element becomes the second to last, and so on.

**Note:** This method mutates `array` and is based on [`Array#reverse`](https://mdn.io/Array/reverse).

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to modify. |

**Returns**

- `(Array)`: Returns `array`.

**Example**

```javascript
var array = [1, 2, 3];

_.reverse(array);
// => [3, 2, 1]

console.log(array);
// => [3, 2, 1]
```

### `_.sortedUniq(array)`

This method is like `_.uniq` except that it's designed and optimized for sorted arrays.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to inspect. |

**Returns**

- `(Array)`: Returns the new duplicate free array.

**Example**

```javascript
_.sortedUniq([1, 1, 2]);
// => [1, 2]
```

### `_.union(...[arrays])`

Creates an array of unique values, in order, from all given arrays using [`SameValueZero`](http://ecma-international.org/ecma-262/7.0/#sec-samevaluezero) for equality comparisons.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `...[arrays]` | `Array` | The arrays to inspect. |

**Returns**

- `(Array)`: Returns the new array of combined values.

**Example**

```javascript
_.union([2], [1, 2]);
// => [2, 1]
```

### `_.uniq(array)`

Creates a duplicate-free version of an array, using [`SameValueZero`](http://ecma-international.org/ecma-262/7.0/#sec-samevaluezero) for equality comparisons, in which only the first occurrence of each element is kept. The order of result values is determined by the order they occur in the array.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to inspect. |

**Returns**

- `(Array)`: Returns the new duplicate free array.

**Example**

```javascript
_.uniq([2, 1, 2]);
// => [2, 1]
```

### `_.without(array, ...[values])`

Creates an array excluding all given values using [`SameValueZero`](http://ecma-international.org/ecma-262/7.0/#sec-samevaluezero) for equality comparisons.

**Note:** Unlike `_.pull`, this method returns a new array.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to inspect. |
| `...[values]` | `*` | The values to exclude. |

**Returns**

- `(Array)`: Returns the new array of filtered values.

**Example**

```javascript
_.without([2, 1, 2, 3], 1, 2);
// => [3]
```

### `_.zip(...[arrays])`

Creates an array of grouped elements, the first of which contains the first elements of the given arrays, the second of which contains the second elements of the given arrays, and so on.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `...[arrays]` | `Array` | The arrays to process. |

**Returns**

- `(Array)`: Returns the new array of grouped elements.

**Example**

```javascript
_.zip(['a', 'b'], [1, 2], [true, false]);
// => [['a', 1, true], ['b', 2, false]]
```

---

You've now explored the array manipulation capabilities of Lodash. To continue, you might want to delve into [Collection](./api-collection.md) functions, which work on both arrays and objects, or explore the [String](./api-string.md) utilities for text manipulation.
