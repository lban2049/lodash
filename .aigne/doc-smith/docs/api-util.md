# Util

A detailed reference for miscellaneous Lodash utility functions.

The Util category provides a collection of versatile helper functions that don't fit into more specific categories like Array or Object. These functions are powerful building blocks for creating complex logic, handling callbacks, generating data, and controlling function execution flow.

For a complete list of all available functions, please see the main [API Reference](./api.md).

## Functions

### `_.attempt(func, ...args)`

Attempts to invoke `func`, returning either the result or the caught error object. Any additional arguments are provided to `func` when it's invoked.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `func` | `Function` | The function to attempt. |
| `...args` | `...*` | The arguments to invoke `func` with. |

**Returns**

- `(*)`: Returns the `func` result or error object.

**Example**

```javascript
// Avoid throwing errors for invalid selectors.
var elements = _.attempt(function(selector) {
  return document.querySelectorAll(selector);
}, '>_>');

if (_.isError(elements)) {
  elements = [];
}
// => elements is now an empty array instead of an error being thrown.
```

---

### `_.bindAll(object, ...methodNames)`

Binds methods of an object to the object itself, overwriting the existing methods. This is useful for ensuring that methods have the correct `this` context when used as callbacks.

**Note:** This method doesn't set the "length" property of bound functions.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | The object to bind and assign the bound methods to. |
| `methodNames` | `...(string|string[])` | The object method names to bind. |

**Returns**

- `(Object)`: Returns `object`.

**Example**

```javascript
var view = {
  'label': 'docs',
  'click': function() {
    console.log('clicked ' + this.label);
  }
};

_.bindAll(view, ['click']);
// Now, if view.click is used as a callback, 'this' will correctly refer to view.
// For example, in a browser context:
// element.addEventListener('click', view.click);
// When the element is clicked, it will log 'clicked docs'.
```

---

### `_.constant(value)`

Creates a function that returns the given `value`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to return from the new function. |

**Returns**

- `(Function)`: Returns the new constant function.

**Example**

```javascript
var objects = _.times(2, _.constant({ 'a': 1 }));

console.log(objects);
// => [{ 'a': 1 }, { 'a': 1 }]

console.log(objects[0] === objects[1]);
// => true, because it returns a reference to the same object.
```

---

### `_.identity(value)`

This method returns the first argument it receives. It is often used as a default iteratee.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | Any value. |

**Returns**

- `(*)`: Returns `value`.

**Example**

```javascript
var object = { 'a': 1 };

_.identity(object) === object;
// => true

// Useful as a default iteratee in functions like filter or map.
_.filter([0, 1, false, 2, '', 3], _.identity);
// => [1, 2, 3]
```

---

### `_.iteratee([func=_.identity])`

Creates a function that can be used as an iteratee for many Lodash methods. It's a powerful way to create flexible callbacks from different value types.

- If `func` is a function, it's returned as is.
- If `func` is an object, a function is returned that performs a partial deep comparison (like `_.matches`).
- If `func` is an array, a function is returned that performs a partial deep comparison for a property path (like `_.matchesProperty`).
- If `func` is a string, a function is returned that gets the property value at that path (like `_.property`).

**Parameters**

| Name | Type | Description |
|---|---|---|
| `func` | `*` | The value to convert to a callback. Defaults to `_.identity`. |

**Returns**

- `(Function)`: Returns the callback.

**Example**

```javascript
var users = [
  { 'user': 'barney', 'age': 36, 'active': true },
  { 'user': 'fred',   'age': 40, 'active': false }
];

// The _.matches shorthand
_.filter(users, _.iteratee({ 'user': 'barney', 'active': true }));
// => [{ 'user': 'barney', 'age': 36, 'active': true }]

// The _.matchesProperty shorthand
_.filter(users, _.iteratee(['user', 'fred']));
// => [{ 'user': 'fred', 'age': 40, 'active': false }]

// The _.property shorthand
_.map(users, _.iteratee('user'));
// => ['barney', 'fred']
```

---

### `_.noop()`

This method returns `undefined`. It is useful as a default callback when you need a function that does nothing.

**Example**

```javascript
_.times(2, _.noop);
// => [undefined, undefined]

// Can be used as a default for optional callbacks
function process(data, callback) {
  const cb = callback || _.noop;
  // ... process data
  cb();
}
```

---

### `_.property(path)`

Creates a function that returns the value at `path` of a given object.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `path` | `Array|string` | The path of the property to get. |

**Returns**

- `(Function)`: Returns the new accessor function.

**Example**

```javascript
var objects = [
  { 'a': { 'b': 2 } },
  { 'a': { 'b': 1 } }
];

_.map(objects, _.property('a.b'));
// => [2, 1]

_.map(_.sortBy(objects, _.property(['a', 'b'])), 'a.b');
// => [1, 2]
```

---

### `_.range(start, end, step)`

Creates an array of numbers (positive and/or negative) progressing from `start` up to, but not including, `end`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `start` | `number` | The start of the range. Defaults to `0` if `end` is not specified. |
| `end` | `number` | The end of the range. |
| `step` | `number` | The value to increment or decrement by. Defaults to `1` or `-1`. |

**Returns**

- `(Array)`: Returns the range of numbers.

**Example**

```javascript
_.range(4);
// => [0, 1, 2, 3]

_.range(-4);
// => [0, -1, -2, -3]

_.range(1, 5);
// => [1, 2, 3, 4]

_.range(0, 20, 5);
// => [0, 5, 10, 15]
```

---

### `_.times(n, [iteratee=_.identity])`

Invokes the iteratee `n` times, returning an array of the results of each invocation. The iteratee is invoked with one argument: `(index)`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `n` | `number` | The number of times to invoke `iteratee`. |
| `iteratee` | `Function` | The function invoked per iteration. Defaults to `_.identity`. |

**Returns**

- `(Array)`: Returns the array of results.

**Example**

```javascript
_.times(3, String);
// => ['0', '1', '2']

_.times(4, _.constant(0));
// => [0, 0, 0, 0]
```

---

### `_.uniqueId([prefix=''])`

Generates a unique ID. If `prefix` is given, the ID is appended to it.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `prefix` | `string` | The value to prefix the ID with. Defaults to an empty string. |

**Returns**

- `(string)`: Returns the unique ID.

**Example**

```javascript
_.uniqueId('contact_');
// => 'contact_1'

_.uniqueId('contact_');
// => 'contact_2'

_.uniqueId();
// => '3'
```

---

This section has provided an overview of the miscellaneous utility functions in Lodash. These tools are fundamental for writing concise and expressive code.

For more specialized tasks, consider exploring the [Function](./api-function.md) or [Lang](./api-lang.md) API sections.