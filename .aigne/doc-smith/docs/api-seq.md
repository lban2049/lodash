# Seq

Lodash provides powerful tools for creating sequences of operations through method chaining. This allows you to build elegant, readable data-processing pipelines. A `lodash` object wraps a value, enabling you to call Lodash methods on it in a chain.

Methods that operate on and return arrays, collections, or functions can be chained together. Methods that retrieve a single value or a primitive will automatically end the chain and return the unwrapped value. For all other cases, the value must be explicitly unwrapped using `.value()`.

One of the key features of chaining is **lazy evaluation**. The execution of chained methods is deferred until `.value()` is called. This allows Lodash to perform optimizations like **shortcut fusion**, which merges iteratee calls to avoid creating intermediate arrays, significantly improving performance.

For a deeper dive into related concepts, see our [Functional Programming Guide](./fp-guide.md).

## Creating Chains

There are two ways to create a chain:

*   **Implicit Chaining**: Simply wrap your data with `_()`. Most methods will return a wrapped value, but some (like `_.add` or `_.find`) will return a primitive, ending the chain.
*   **Explicit Chaining**: Use `_.chain()` to start a chain where every method call returns a wrapped instance, which must be unwrapped with `.value()`.

---

## API Methods

### chain

Creates a `lodash` wrapper instance that wraps `value` with explicit method chain sequences enabled. The result of such sequences must always be unwrapped with `_#value`.

**Parameters**

<x-field data-name="value" data-type="any" data-desc="The value to wrap."></x-field>

**Returns**

<x-field data-name="wrapper" data-type="Object" data-desc="Returns the new `lodash` wrapper instance."></x-field>

**Example**

```javascript icon=logos:javascript
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

### tap

This method invokes `interceptor` and returns `value`. The interceptor is invoked with one argument: `(value)`. The purpose of this method is to "tap into" a method chain sequence in order to modify intermediate results or perform side effects like logging.

**Parameters**

<x-field data-name="value" data-type="any" data-desc="The value to provide to the interceptor."></x-field>
<x-field data-name="interceptor" data-type="Function" data-desc="The function to invoke."></x-field>

**Returns**

<x-field data-name="value" data-type="any" data-desc="Returns the original `value`."></x-field>

**Example**

```javascript icon=logos:javascript
_([1, 2, 3])
 .tap(function(array) {
   // Mutate the input array.
   array.pop();
 })
 .reverse()
 .value();
// => [2, 1]
```

### thru

This method is like `_.tap` except that it returns the result of `interceptor`. The purpose of this method is to "pass thru" values, replacing intermediate results in a method chain sequence.

**Parameters**

<x-field data-name="value" data-type="any" data-desc="The value to provide to the interceptor."></x-field>
<x-field data-name="interceptor" data-type="Function" data-desc="The function to invoke."></x-field>

**Returns**

<x-field data-name="result" data-type="any" data-desc="Returns the result of `interceptor`."></x-field>

**Example**

```javascript icon=logos:javascript
_('  abc  ')
 .chain()
 .trim()
 .thru(function(value) {
   return [value];
 })
 .value();
// => ['abc']
```

## Wrapper Prototype Methods

These methods are available on a Lodash wrapper instance, such as one created by `_()` or `_.chain()`.

| Method | Description |
|---|---|
| `at(...paths)` | The wrapper version of `_.at`. Picks values from the wrapped object at the given paths. |
| `chain()` | Enables explicit chaining from an existing wrapper. |
| `commit()` | Executes the chain sequence and returns the wrapped result. |
| `plant(value)` | Creates a clone of the chain sequence, planting a new `value` as the wrapped value. |
| `reverse()` | The wrapper version of `_.reverse`. Note: this mutates the wrapped array. |
| `value()` | Executes the chain sequence to resolve and return the unwrapped value. Aliased as `toJSON` and `valueOf`. |
| `next()` | Gets the next value on a wrapped object, following the iterator protocol. |
| `[Symbol.iterator]()` | Enables the wrapper to be iterable (e.g., in `for...of` loops). |

**Example: Using `.plant()`**

```javascript icon=logos:javascript
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

Now that you understand how to create and manage sequences, explore the methods you can use within them in the [Collection](./api-collection.md) and [Array](./api-array.md) API sections.