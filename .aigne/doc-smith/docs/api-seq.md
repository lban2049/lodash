# Seq

Lodash's sequence (or "Seq") methods are the foundation of its powerful chaining capabilities. When you wrap a value with `_()`, you create a Lodash wrapper instance that can be used to chain multiple operations together in a readable, sequential manner. This approach supports both implicit and explicit chaining and leverages lazy evaluation for performance optimization.

## Chaining Concepts

Method chaining allows you to combine multiple Lodash methods. Instead of nesting function calls, you can call them one after another. The execution of chained methods is lazy, meaning it's deferred until `_.value()` is called. This allows Lodash to perform optimizations like "shortcut fusion" to merge iteratee calls and reduce the number of intermediate arrays created.

```d2
direction: right

"Data\n[1, 2, 3, 4]": {
  shape: document
}

"Wrapper-Object": {
  label: "Wrapper Object"
  shape: package
  
  "Operations": {
    shape: rectangle
    label: ".filter(isEven)\n.map(square)\n.take(1)"
  }
}

"Result\n[4]": {
  shape: document
}

Data -> "Wrapper-Object": "_()"
"Wrapper-Object" -> Result: ".value()"
```

### _.chain(value)

Creates a `lodash` wrapper instance that wraps `value` with explicit method chain sequences enabled. The result of such sequences must be unwrapped with `_#value`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to wrap. |

**Returns**

- `Object`: Returns the new `lodash` wrapper instance.

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

### .commit()

Executes the chain sequence and returns the wrapped result.

**Returns**

- `Object`: Returns the new `lodash` wrapper instance.

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

console.log(array);
// => [1, 2, 3]
```

### .plant(value)

Creates a clone of the chain sequence planting `value` as the wrapped value.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to plant. |

**Returns**

- `Object`: Returns the new `lodash` wrapper instance.

**Example**

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

### .tap(interceptor)

This method invokes `interceptor` and returns `value`. The interceptor is invoked with one argument: `(value)`. The purpose of this method is to "tap into" a method chain sequence in order to modify intermediate results.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `interceptor` | `Function` | The function to invoke. |

**Returns**

- `*`: Returns `value`.

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

### .thru(interceptor)

This method is like `.tap` except that it returns the result of `interceptor`. The purpose of this method is to "pass thru" values, replacing intermediate results in a method chain sequence.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `interceptor` | `Function` | The function to invoke. |

**Returns**

- `*`: Returns the result of `interceptor`.

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

### .value()

Executes the chain sequence to resolve the unwrapped value.

**Aliases**: `toJSON`, `valueOf`

**Returns**

- `*`: Returns the resolved unwrapped value.

**Example**

```javascript
_([1, 2, 3]).value();
// => [1, 2, 3]
```

---

With a solid understanding of Lodash's sequential chaining, you can write more expressive and maintainable data transformations. For other utility functions, check out the [Util API reference](./api-util.md).