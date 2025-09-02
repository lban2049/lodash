# Seq

Lodash provides powerful method chaining capabilities, allowing you to string multiple operations together to process data in a clear and readable manner. The core of this approach is the Lodash wrapper object, which encapsulates your data and allows Lodash methods to be called on it.

Chaining supports **Lazy Evaluation**. This means that intermediate operations are not executed until `_#value()` is called, either explicitly or implicitly. This mechanism optimizes performance through "shortcut fusion" by avoiding the creation of intermediate arrays, which significantly reduces the number of iterations, especially when processing large datasets.

### Chaining Flow

The following diagram illustrates a typical data processing chain:

```d2
direction: right

A: "Original Array\n[1, 2, 3, 4]"
B: "_.map(n => n * n)\n[1, 4, 9, 16]"
C: "_.filter(n => n > 5)\n[9, 16]"
D: "_.take(1)\n[9]"
E: "_.value()\nGet the final result"
F: "Final Result\n[9]"

A -> B: "Map" { style.animated: true }
B -> C: "Filter" { style.animated: true }
C -> D: "Take" { style.animated: true }
D -> E: "Evaluate" { style.animated: true }
E -> F
```

## Core Functions

The following are the core functions related to sequence method chaining.

### _.chain(value)

Creates a Lodash wrapper instance with explicit method chaining enabled. Sequences started with `_.chain` must use the `_#value()` method to get the final result.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to wrap. |

**Returns**

- `(Object)`: Returns the new Lodash wrapper instance.

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

This method invokes `interceptor` and returns `value`. The `interceptor` is invoked with one argument: `value`. The main purpose of this method is to "tap into" a method chain to perform actions without changing the value in the chain, such as logging or modifying external variables.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to provide to the `interceptor`. |
| `interceptor` | `Function` | The function to invoke. |

**Returns**

- `(*)`: Returns `value`.

**Example**

```javascript
_([1, 2, 3])
 .tap(function(array) {
   // You can operate on the array here, e.g., for logging
   console.log(array); // Outputs [1, 2, 3]
   array.pop();
 })
 .reverse()
 .value();
// => [2, 1]
```

### _.thru(value, interceptor)

This method is like `_.tap` except that it returns the result of `interceptor`. This allows you to pass and replace intermediate results within a method chain.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to provide to the `interceptor`. |
| `interceptor` | `Function` | The function to invoke. |

**Returns**

- `(*)`: Returns the result of `interceptor`.

**Example**

```javascript
_('  abc  ')
 .chain()
 .trim()
 .thru(function(value) {
   return [value, value.length];
 })
 .value();
// => ['abc', 3]
```

## Wrapper Methods

### _#value()

Executes the chained sequence to extract the wrapped value. This is the endpoint for explicit chaining.

**Aliases**: `_#toJSON`, `_#valueOf`

**Returns**

- `(*)`: Returns the resolved unwrapped value.

**Example**

```javascript
_([1, 2, 3]).value();
// => [1, 2, 3]

_('  abc  ').chain().trim().value();
// => 'abc'
```

### _#at(...paths)

The wrapper version of `_.at`. Selects values based on specified property paths.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `...paths` | `(string|string[])` | The property paths to pick. |

**Returns**

- `(Object)`: Returns the new Lodash wrapper instance.

**Example**

```javascript
var object = { 'a': [{ 'b': { 'c': 3 } }, 4] };
 
_(object).at(['a[0].b.c', 'a[1]']).value();
// => [3, 4]
```

### _#chain()

Enables explicit chaining on an existing wrapper instance.

**Returns**

- `(Object)`: Returns the new Lodash wrapper instance.

**Example**

```javascript
var users = [
  { 'user': 'barney', 'age': 36 },
  { 'user': 'fred',   'age': 40 }
];

// Without explicit chaining
_(users).head();
// => { 'user': 'barney', 'age': 36 }

// With explicit chaining
_(users)
  .chain()
  .head()
  .pick('user')
  .value();
// => { 'user': 'barney' }
```

### _#commit()

Executes the current chained sequence and returns a new Lodash wrapper instance with the result. This allows you to "commit" partial results in a chain and then continue chaining other methods.

**Returns**

- `(Object)`: Returns the new Lodash wrapper instance.

**Example**

```javascript
var array = [1, 2];
var wrapped = _(array).push(3);

console.log(array);
// => [1, 2]

wrapped = wrapped.commit();
console.log(array);
// => [1, 2, 3]

wrapped.last();
// => 3
```

### _#plant(value)

Creates a clone of the chained sequence and sets `value` as the new wrapped value. This is useful for applying the same sequence of operations to different datasets while preserving the original sequence.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to plant. |

**Returns**

- `(Object)`: Returns the new Lodash wrapper instance.

**Example**

```javascript
function square(n) {
  return n * n;
}

var wrapped = _([1, 2]).map(square);
var other = wrapped.plant([3, 4]);

console.log(other.value());
// => [9, 16]

console.log(wrapped.value());
// => [1, 4]
```

### _#reverse()

The wrapper version of `_.reverse`. Reverses the wrapped array. This is an in-place operation that mutates the original array.

**Returns**

- `(Object)`: Returns the new Lodash wrapper instance.

**Example**

```javascript
var array = [1, 2, 3];

_(array).reverse().value();
// => [3, 2, 1]

console.log(array);
// => [3, 2, 1]
```

---

By mastering Lodash's chaining methods, you can build more expressive and readable data processing pipelines. Next, you can delve into the [Collection](./api-collection.md) or [Array](./api-array.md) methods to explore the powerful functions available for use in chained calls.