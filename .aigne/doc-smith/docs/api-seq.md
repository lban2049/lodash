# Seq

Lodash's sequence (Seq) functions are the foundation of its powerful method chaining capabilities. When you wrap a value (like an array or object) with `_()`, you create a Lodash wrapper instance. This allows you to call a series of Lodash methods on the data, where the output of one method becomes the input for the next. This approach promotes writing clean, readable, and declarative code.

Key concepts in Lodash's chaining are implicit vs. explicit chaining and lazy evaluation.

- **Implicit Chaining**: Created by `_(value)`. Methods that return arrays, collections, or functions will return a new wrapper instance, allowing you to continue the chain. Methods that return a single value (e.g., `_.head` or `_.reduce`) will automatically end the chain and return the unwrapped value.
- **Explicit Chaining**: Created by `_.chain(value)`. All methods in an explicit chain will return a wrapper instance, even those that would normally unwrap. You must explicitly call `.value()` to get the final result.
- **Lazy Evaluation**: Chained method calls are not executed immediately. Instead, they are deferred until `.value()` is called. This allows Lodash to perform optimizations like *shortcut fusion*, where it merges multiple iteratee calls into a single pass, significantly improving performance by avoiding the creation of intermediate arrays.

## Chaining Flow Diagram

The following diagram illustrates how data flows through a typical Lodash chain, highlighting the concept of lazy evaluation.

```d2
direction: right

"Initial Array" { 
  shape: document
  label: "[1, 2, 3, 4]"
}

"Wrapped" {
  shape: package
  label: "_([1, 2, 3, 4])"
}

"map(n => n * 2)" {
  shape: package
  label: "Intermediate Wrapper"
}

"filter(n => n > 4)" {
  shape: package
  label: "Intermediate Wrapper"
}

"Result" {
  shape: document
  label: "[6, 8]"
}

"Initial Array" -> "Wrapped": "1. Wrap Value"
"Wrapped" -> "map(n => n * 2)": "2. Chain method (Lazy)"
"map(n => n * 2)" -> "filter(n => n > 4)": "3. Chain method (Lazy)"
"filter(n => n > 4)" -> "Result": "4. .value() (Execute)"

```

## Methods

### `_.chain(value)`

Creates a Lodash wrapper instance that enables explicit method chaining. With explicit chaining, every method call returns a wrapper, and you must call `.value()` at the end to retrieve the final result.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to wrap. |

**Returns**

- `(Object)`: Returns the new `lodash` wrapper instance.

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

### `_.tap(value, interceptor)`

This method invokes an `interceptor` function and then returns the original `value`. It's useful for "tapping into" a method chain to perform side effects, such as logging intermediate results, without altering the value being passed through the chain.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to provide to the `interceptor`. |
| `interceptor` | `Function` | The function to invoke. It receives `value` as its only argument. |

**Returns**

- `(*)`: Returns the original `value`.

**Example**

```javascript
_([1, 2, 3])
 .tap(function(array) {
   // Mutate the array as a side effect.
   console.log('Before pop:', array);
   array.pop();
   console.log('After pop:', array);
 })
 .reverse()
 .value();
// Logs: Before pop: [1, 2, 3]
// Logs: After pop: [1, 2]
// => [2, 1]
```

### `_.thru(value, interceptor)`

This method is similar to `_.tap`, but instead of returning the original `value`, it returns the result of the `interceptor` function. This allows you to replace the value in the chain with a new one.

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
   // The interceptor's return value continues the chain.
   return [value, value.length];
 })
 .value();
// => ['abc', 3]
```

### `_(...).[method]`

Many methods in Lodash are available on the wrapper prototype and can be chained together. When a method returns a new array or collection, it typically returns a new wrapper instance, allowing the chain to continue.

**Wrapper Methods**

| Method | Description |
|---|---|
| `at(...paths)` | Wrapper version of `_.at`. Picks values from the wrapped object at given paths. |
| `commit()` | Executes the chain sequence and returns a new wrapper with the result. |
| `plant(value)` | Creates a clone of the chain sequence, planting a new `value` as the wrapped value. |
| `reverse()` | Wrapper version of `_.reverse`. Mutates the wrapped array. |
| `value()` | Executes the chain sequence to resolve and return the unwrapped value. Aliases: `toJSON`, `valueOf`. |

**Example: Using Wrapper Methods**

```javascript
var object = { 'a': [{ 'b': { 'c': 3 } }, 4] };
 
// Using .at() in a chain
var result = _(object).at(['a[0].b.c', 'a[1]']).value();
// => [3, 4]

// Using .commit() and .plant()
var array = [1, 2];
var wrapped = _(array).push(3); // Lazy push

console.log(array); // => [1, 2]

var committed = wrapped.commit(); // Executes push
console.log(array); // => [1, 2, 3]

var planted = committed.plant(['a', 'b']); // Replaces the value
console.log(planted.value()); // => ['a', 'b']
```

---

Understanding sequential chaining is key to writing expressive and efficient data transformations with Lodash. Many of the methods you'll use in chains come from the [Array](./api-array.md) and [Collection](./api-collection.md) categories.