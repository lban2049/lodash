# Seq

A detailed reference for all Lodash functions related to sequential method chaining. Lodash wrappers enable a fluent programming style by allowing you to chain methods together. This process is often lazy, meaning the chain of operations is not executed until the final value is explicitly requested.

This lazy evaluation allows for significant performance optimizations through a technique called "shortcut fusion," which merges iteratee calls to avoid creating intermediate arrays. To resolve the chain and get the final output, you must call the `.value()` method.

## Methods

### _.chain(value)

Creates a `lodash` wrapper instance that wraps `value` with explicit method chain sequences enabled. The result of such sequences must be unwrapped with `_#value()`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to wrap. |

**Returns**

(`Object`): Returns the new `lodash` wrapper instance.

**Example**

```javascript
var users = [
  { 'user': 'barney',  'age': 36 },
  { 'user': 'fred',    'age': 40 },
  { 'user': 'pebbles', 'age': 1 }
];

var youngest = _
  .chain(users)
  .sortBy('age')
  .map(function(o) {
    return o.user + ' is ' + o.age;
  })
  .head()
  .value();
// => 'pebbles is 1'
```

### _.tap(value, interceptor)

This method invokes `interceptor` and returns `value`. The interceptor is invoked with one argument: `(value)`. The purpose of this method is to "tap into" a method chain sequence in order to modify intermediate results without changing the value passed along the chain.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to provide to `interceptor`. |
| `interceptor` | `Function` | The function to invoke. |

**Returns**

(`*`): Returns `value`.

**Example**

```javascript
_([1, 2, 3])
 .tap(function(array) {
   // Mutate input array.
   array.pop();
 })
 .reverse()
 .value();
// => [2, 1]
```

### _.thru(value, interceptor)

This method is like `_.tap` except that it returns the result of `interceptor`. The purpose of this method is to "pass thru" values, replacing intermediate results in a method chain sequence.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to provide to `interceptor`. |
| `interceptor` | `Function` | The function to invoke. |

**Returns**

(`*`): Returns the result of `interceptor`.

**Example**

```javascript
_('  abc  ')
 .chain()
 .trim()
 .thru(function(value) {
   return [value];
 })
 .value();
// => ['abc']
```

## Wrapper Instance Methods

When you create a Lodash wrapper using `_()` or `_.chain()`, the resulting object has several methods to control the chain's execution.

| Method | Description |
|---|---|
| `.value()` | Executes the chain sequence to resolve and return the unwrapped value. Aliased as `.toJSON()` and `.valueOf()`. |
| `.chain()` | Enables explicit chaining on an existing wrapper instance. |
| `.commit()` | Executes the chain sequence and returns a new wrapped result, allowing for further chaining on the computed value. |
| `.plant(value)` | Creates a clone of the chain sequence, planting a new `value` as the wrapped value. |
| `.reverse()` | Reverses the wrapped array. This method mutates the array. |
| `.next()` | Gets the next value in an iteration if the wrapped object is being treated as an iterator. |
| `[Symbol.iterator]()` | Enables the wrapper to be iterable, allowing it to be used in `for...of` loops and with `Array.from()`. |

**Example: Using `.value()`**

```javascript
_([1, 2, 3]).value();
// => [1, 2, 3]
```

**Example: Using `.plant()`**

```javascript
function square(n) {
  return n * n;
}

var wrapped = _([1, 2]).map(square);
var other = wrapped.plant([3, 4]);

other.value();
// => [9, 16]

wrapped.value();
// => [1, 4]
```

---

Method chaining is a powerful feature for creating clean, readable data transformation pipelines. To explore the functions you'll most commonly use within these chains, proceed to the Collection API documentation.

[Next: Collection API](./api-collection.md)
