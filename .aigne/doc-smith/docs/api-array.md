# Array

Lodash provides a rich set of functions for creating, manipulating, querying, and transforming arrays. These utilities simplify common array operations, offering powerful and performant alternatives to native JavaScript methods, especially when dealing with complex data structures.

Many of these methods return new arrays and can be chained together for expressive data processing. For functions that iterate over arrays and other iterable types, also see the [Collection](./api-collection.md) documentation.

---

### `_.chunk(array, [size=1])`

Creates an array of elements split into groups the length of `size`. If `array` can't be split evenly, the final chunk will be the remaining elements.

**Since**
3.0.0

**Arguments**

| Param | Type | Description |
|---|---|---|
| `array` | `Array` | The array to process. |
| `[size=1]` | `number` | The length of each chunk. |

**Returns**

(`Array`): Returns the new array of chunks.

**Example**

```javascript
_.chunk(['a', 'b', 'c', 'd'], 2);
// => [['a', 'b'], ['c', 'd']]

_.chunk(['a', 'b', 'c', 'd'], 3);
// => [['a', 'b', 'c'], ['d']]
```

---

### `_.compact(array)`

Creates an array with all falsey values removed. The values `false`, `null`, `0`, `""`, `undefined`, and `NaN` are falsey.

**Since**
0.1.0

**Arguments**

| Param | Type | Description |
|---|---|---|
| `array` | `Array` | The array to compact. |

**Returns**

(`Array`): Returns the new array of filtered values.

**Example**

```javascript
_.compact([0, 1, false, 2, '', 3]);
// => [1, 2, 3]
```

---

### `_.concat(array, ...[values])`

Creates a new array concatenating `array` with any additional arrays and/or values.

**Since**
4.0.0

**Arguments**

| Param | Type | Description |
|---|---|---|
| `array` | `Array` | The array to concatenate. |
| `...[values]` | `*` | The values to concatenate. |

**Returns**

(`Array`): Returns the new concatenated array.

**Example**

```javascript
var array = [1];
var other = _.concat(array, 2, [3], [[4]]);

console.log(other);
// => [1, 2, 3, [4]]

console.log(array);
// => [1]
```

---

### `_.difference(array, ...[values])`

Creates an array of `array` values not included in the other given arrays using `SameValueZero` for equality comparisons. The order and references of result values are determined by the first array.

**Since**
0.1.0

**Arguments**

| Param | Type | Description |
|---|---|---|
| `array` | `Array` | The array to inspect. |
| `...[values]` | `Array` | The values to exclude. |

**Returns**

(`Array`): Returns the new array of filtered values.

**Example**

```javascript
_.difference([2, 1], [2, 3]);
// => [1]
```

---

### `_.differenceBy(array, ...[values], [iteratee=_.identity])`

This method is like `_.difference` except that it accepts `iteratee` which is invoked for each element of `array` and `values` to generate the criterion by which they're compared. The order and references of result values are determined by the first array. The iteratee is invoked with one argument: (value).

**Since**
4.0.0

**Arguments**

| Param | Type | Description |
|---|---|---|
| `array` | `Array` | The array to inspect. |
| `...[values]` | `Array` | The values to exclude. |
| `[iteratee=_.identity]` | `Function` | The iteratee invoked per element. |

**Returns**

(`Array`): Returns the new array of filtered values.

**Example**

```javascript
_.differenceBy([2.1, 1.2], [2.3, 3.4], Math.floor);
// => [1.2]

// The `_.property` iteratee shorthand.
_.differenceBy([{ 'x': 2 }, { 'x': 1 }], [{ 'x': 1 }], 'x');
// => [{ 'x': 2 }]
```

---

### `_.differenceWith(array, ...[values], [comparator])`

This method is like `_.difference` except that it accepts `comparator` which is invoked to compare elements of `array` to `values`. The order and references of result values are determined by the first array. The comparator is invoked with two arguments: (arrVal, othVal).

**Since**
4.0.0

**Arguments**

| Param | Type | Description |
|---|---|---|
| `array` | `Array` | The array to inspect. |
| `...[values]` | `Array` | The values to exclude. |
| `[comparator]` | `Function` | The comparator invoked per element. |

**Returns**

(`Array`): Returns the new array of filtered values.

**Example**

```javascript
var objects = [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }];

_.differenceWith(objects, [{ 'x': 1, 'y': 2 }], _.isEqual);
// => [{ 'x': 2, 'y': 1 }]
```

---

### `_.drop(array, [n=1])`

Creates a slice of `array` with `n` elements dropped from the beginning.

**Since**
0.5.0

**Arguments**

| Param | Type | Description |
|---|---|---|
| `array` | `Array` | The array to query. |
| `[n=1]` | `number` | The number of elements to drop. |

**Returns**

(`Array`): Returns the slice of `array`.

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

---

### `_.dropRight(array, [n=1])`

Creates a slice of `array` with `n` elements dropped from the end.

**Since**
3.0.0

**Arguments**

| Param | Type | Description |
|---|---|---|
| `array` | `Array` | The array to query. |
| `[n=1]` | `number` | The number of elements to drop. |

**Returns**

(`Array`): Returns the slice of `array`.

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

---

### `_.findIndex(array, [predicate=_.identity], [fromIndex=0])`

This method is like `_.find` except that it returns the index of the first element `predicate` returns truthy for instead of the element itself.

**Since**
1.1.0

**Arguments**

| Param | Type | Description |
|---|---|---|
| `array` | `Array` | The array to inspect. |
| `[predicate=_.identity]` | `Function` | The function invoked per iteration. |
| `[fromIndex=0]` | `number` | The index to search from. |

**Returns**

(`number`): Returns the index of the found element, else `-1`.

**Example**

```javascript
var users = [
  { 'user': 'barney',  'active': false },
  { 'user': 'fred',    'active': false },
  { 'user': 'pebbles', 'active': true }
];

_.findIndex(users, function(o) { return o.user == 'barney'; });
// => 0

// The `_.matches` iteratee shorthand.
_.findIndex(users, { 'user': 'fred', 'active': false });
// => 1
```

---

### `_.flatten(array)`

Flattens `array` a single level deep.

**Since**
0.1.0

**Arguments**

| Param | Type | Description |
|---|---|---|
| `array` | `Array` | The array to flatten. |

**Returns**

(`Array`): Returns the new flattened array.

**Example**

```javascript
_.flatten([1, [2, [3, [4]], 5]]);
// => [1, 2, [3, [4]], 5]
```

---

### `_.fromPairs(pairs)`

The inverse of `_.toPairs`; this method returns an object composed from key-value `pairs`.

**Since**
4.0.0

**Arguments**

| Param | Type | Description |
|---|---|---|
| `pairs` | `Array` | The key-value pairs. |

**Returns**

(`Object`): Returns the new object.

**Example**

```javascript
_.fromPairs([['a', 1], ['b', 2]]);
// => { 'a': 1, 'b': 2 }
```

---

### `_.head(array)`

Gets the first element of `array`.

**Since**
0.1.0

**Arguments**

| Param | Type | Description |
|---|---|---|
| `array` | `Array` | The array to query. |

**Returns**

(`*`): Returns the first element of `array`.

**Example**

```javascript
_.head([1, 2, 3]);
// => 1

_.head([]);
// => undefined
```

---

### `_.indexOf(array, value, [fromIndex=0])`

Gets the index at which the first occurrence of `value` is found in `array` using `SameValueZero` for equality comparisons. If `fromIndex` is negative, it's used as the offset from the end of `array`.

**Since**
0.1.0

**Arguments**

| Param | Type | Description |
|---|---|---|
| `array` | `Array` | The array to inspect. |
| `value` | `*` | The value to search for. |
| `[fromIndex=0]` | `number` | The index to search from. |

**Returns**

(`number`): Returns the index of the matched value, else `-1`.

**Example**

```javascript
_.indexOf([1, 2, 1, 2], 2);
// => 1

// Search from the `fromIndex`.
_.indexOf([1, 2, 1, 2], 2, 2);
// => 3
```

---

### `_.join(array, [separator=','])`

Converts all elements in `array` into a string separated by `separator`.

**Since**
4.0.0

**Arguments**

| Param | Type | Description |
|---|---|---|
| `array` | `Array` | The array to convert. |
| `[separator=',']` | `string` | The element separator. |

**Returns**

(`string`): Returns the joined string.

**Example**

```javascript
_.join(['a', 'b', 'c'], '~');
// => 'a~b~c'
```

---

### `_.pull(array, ...[values])`

Removes all given values from `array` using `SameValueZero` for equality comparisons. This method mutates `array`.

**Since**
2.0.0

**Arguments**

| Param | Type | Description |
|---|---|---|
| `array` | `Array` | The array to modify. |
| `...[values]` | `*` | The values to remove. |

**Returns**

(`Array`): Returns `array`.

**Example**

```javascript
var array = ['a', 'b', 'c', 'a', 'b', 'c'];

_.pull(array, 'a', 'c');
console.log(array);
// => ['b', 'b']
```

---

### `_.reverse(array)`

Reverses `array` so that the first element becomes the last, the second element becomes the second to last, and so on. This method mutates `array`.

**Since**
4.0.0

**Arguments**

| Param | Type | Description |
|---|---|---|
| `array` | `Array` | The array to modify. |

**Returns**

(`Array`): Returns `array`.

**Example**

```javascript
var array = [1, 2, 3];

_.reverse(array);
// => [3, 2, 1]

console.log(array);
// => [3, 2, 1]
```

---

### `_.union(...[arrays])`

Creates an array of unique values, in order, from all given arrays using `SameValueZero` for equality comparisons.

**Since**
0.1.0

**Arguments**

| Param | Type | Description |
|---|---|---|
| `...[arrays]` | `Array` | The arrays to inspect. |

**Returns**

(`Array`): Returns the new array of combined values.

**Example**

```javascript
_.union([2], [1, 2]);
// => [2, 1]
```

---

This is a selection of the most commonly used Array functions. For a complete list and further details, please explore the API reference. For functions that handle iteration over both arrays and objects, please see the [Collection](./api-collection.md) documentation.