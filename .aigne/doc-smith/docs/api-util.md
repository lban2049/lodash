# Util

The Util category provides a collection of miscellaneous utility functions that offer powerful, reusable logic for common programming tasks. These functions range from creating callbacks and composite functions to generating unique IDs and handling default values. They are essential tools for writing cleaner, more declarative code.

---

### _.attempt(func, ...args)

Attempts to invoke `func`, returning either the result or the caught error object. Any additional arguments are provided to `func` when it's invoked.

**Since**
3.0.0

**Arguments**

| Param    | Type     | Description                    |
| :------- | :------- | :----------------------------- |
| `func`   | `Function` | The function to attempt.       |
| `[args]` | `...*`   | The arguments to invoke `func` with. |

**Returns**

`(*)`: Returns the `func` result or error object.

**Example**

```javascript
// Avoid throwing errors for invalid selectors.
var elements = _.attempt(function(selector) {
  return document.querySelectorAll(selector);
}, '>_>');

if (_.isError(elements)) {
  elements = [];
}
```

---

### _.bindAll(object, methodNames)

Binds methods of an object to the object itself, overwriting the existing method.

**Note:** This method doesn't set the "length" property of bound functions.

**Since**
0.1.0

**Arguments**

| Param         | Type                | Description                           |
| :------------ | :------------------ | :------------------------------------ |
| `object`      | `Object`            | The object to bind methods to.        |
| `methodNames` | `...(string|string[])` | The object method names to bind.      |

**Returns**

`(Object)`: Returns `object`.

**Example**

```javascript
var view = {
  'label': 'docs',
  'click': function() {
    console.log('clicked ' + this.label);
  }
};

_.bindAll(view, ['click']);
jQuery(element).on('click', view.click);
// => Logs 'clicked docs' when clicked.
```

---

### _.constant(value)

Creates a function that returns `value`.

**Since**
2.4.0

**Arguments**

| Param   | Type | Description                            |
| :------ | :--- | :------------------------------------- |
| `value` | `*`  | The value to return from the new function. |

**Returns**

`(Function)`: Returns the new constant function.

**Example**

```javascript
var objects = _.times(2, _.constant({ 'a': 1 }));

console.log(objects);
// => [{ 'a': 1 }, { 'a': 1 }]

console.log(objects[0] === objects[1]);
// => true
```

---

### _.defaultTo(value, defaultValue)

Checks `value` to determine whether a default value should be returned in its place. The `defaultValue` is returned if `value` is `NaN`, `null`, or `undefined`.

**Since**
4.14.0

**Arguments**

| Param          | Type | Description           |
| :------------- | :--- | :-------------------- |
| `value`        | `*`  | The value to check.   |
| `defaultValue` | `*`  | The default value.    |

**Returns**

`(*)`: Returns the resolved value.

**Example**

```javascript
_.defaultTo(1, 10);
// => 1

_.defaultTo(undefined, 10);
// => 10
```

---

### _.identity(value)

This method returns the first argument it receives.

**Since**
0.1.0

**Arguments**

| Param   | Type | Description |
| :------ | :--- | :---------- |
| `value` | `*`  | Any value.  |

**Returns**

`(*)`: Returns `value`.

**Example**

```javascript
var object = { 'a': 1 };

console.log(_.identity(object) === object);
// => true
```

---

### _.iteratee([func=_.identity])

Creates a function that invokes `func` with the arguments of the created function. If `func` is a property name, the created function returns the property value for a given element. If `func` is an array or object, the created function returns `true` for elements that contain the equivalent source properties, otherwise it returns `false`.

**Since**
4.0.0

**Arguments**

| Param  | Type | Description                      |
| :----- | :--- | :------------------------------- |
| `func` | `*`  | The value to convert to a callback. |

**Returns**

`(Function)`: Returns the callback.

**Example**

```javascript
var users = [
  { 'user': 'barney', 'age': 36, 'active': true },
  { 'user': 'fred',   'age': 40, 'active': false }
];

// The `_.matches` iteratee shorthand.
_.filter(users, _.iteratee({ 'user': 'barney', 'active': true }));
// => [{ 'user': 'barney', 'age': 36, 'active': true }]

// The `_.matchesProperty` iteratee shorthand.
_.filter(users, _.iteratee(['user', 'fred']));
// => [{ 'user': 'fred', 'age': 40 }]

// The `_.property` iteratee shorthand.
_.map(users, _.iteratee('user'));
// => ['barney', 'fred']
```

---

### _.matches(source)

Creates a function that performs a partial deep comparison between a given object and `source`, returning `true` if the given object has equivalent property values, else `false`.

**Since**
3.0.0

**Arguments**

| Param    | Type   | Description                         |
| :------- | :----- | :---------------------------------- |
| `source` | `Object` | The object of property values to match. |

**Returns**

`(Function)`: Returns the new spec function.

**Example**

```javascript
var objects = [
  { 'a': 1, 'b': 2, 'c': 3 },
  { 'a': 4, 'b': 5, 'c': 6 }
];

_.filter(objects, _.matches({ 'a': 4, 'c': 6 }));
// => [{ 'a': 4, 'b': 5, 'c': 6 }]
```

---

### _.matchesProperty(path, srcValue)

Creates a function that performs a partial deep comparison between the value at `path` of a given object to `srcValue`, returning `true` if the object value is equivalent, else `false`.

**Since**
3.2.0

**Arguments**

| Param      | Type          | Description                   |
| :--------- | :------------ | :---------------------------- |
| `path`     | `Array|string`  | The path of the property to get. |
| `srcValue` | `*`           | The value to match.           |

**Returns**

`(Function)`: Returns the new spec function.

**Example**

```javascript
var objects = [
  { 'a': 1, 'b': 2, 'c': 3 },
  { 'a': 4, 'b': 5, 'c': 6 }
];

_.find(objects, _.matchesProperty('a', 4));
// => { 'a': 4, 'b': 5, 'c': 6 }
```

---

### _.method(path, ...args)

Creates a function that invokes the method at `path` of a given object. Any additional arguments are provided to the invoked method.

**Since**
3.7.0

**Arguments**

| Param    | Type          | Description                         |
| :------- | :------------ | :---------------------------------- |
| `path`   | `Array|string`  | The path of the method to invoke.   |
| `[args]` | `...*`        | The arguments to invoke the method with. |

**Returns**

`(Function)`: Returns the new invoker function.

**Example**

```javascript
var objects = [
  { 'a': { 'b': _.constant(2) } },
  { 'a': { 'b': _.constant(1) } }
];

_.map(objects, _.method('a.b'));
// => [2, 1]

_.map(objects, _.method(['a', 'b']));
// => [2, 1]
```

---

### _.noop()

This method returns `undefined`.

**Since**
2.3.0

**Example**

```javascript
_.times(2, _.noop);
// => [undefined, undefined]
```

---

### _.property(path)

Creates a function that returns the value at `path` of a given object.

**Since**
2.4.0

**Arguments**

| Param  | Type          | Description                   |
| :----- | :------------ | :---------------------------- |
| `path` | `Array|string`  | The path of the property to get. |

**Returns**

`(Function)`: Returns the new accessor function.

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

### _.range([start=0], end, [step=1])

Creates an array of numbers (positive and/or negative) progressing from `start` up to, but not including, `end`.

**Since**
0.1.0

**Arguments**

| Param   | Type   | Description                         |
| :------ | :----- | :---------------------------------- |
| `start` | `number` | The start of the range.             |
| `end`   | `number` | The end of the range.               |
| `step`  | `number` | The value to increment or decrement by. |

**Returns**

`(Array)`: Returns the range of numbers.

**Example**

```javascript
_.range(4);
// => [0, 1, 2, 3]

_.range(-4);
// => [0, -1, -2, -3]

_.range(1, 5);
// => [1, 2, 3, 4]
```

---

### _.times(n, [iteratee=_.identity])

Invokes the iteratee `n` times, returning an array of the results of each invocation. The iteratee is invoked with one argument: (index).

**Since**
0.1.0

**Arguments**

| Param      | Type     | Description                      |
| :--------- | :------- | :------------------------------- |
| `n`        | `number` | The number of times to invoke `iteratee`. |
| `iteratee` | `Function` | The function invoked per iteration. |

**Returns**

`(Array)`: Returns the array of results.

**Example**

```javascript
_.times(3, String);
// => ['0', '1', '2']

_.times(4, _.constant(0));
// => [0, 0, 0, 0]
```

---

### _.uniqueId([prefix=''])

Generates a unique ID. If `prefix` is given, the ID is appended to it.

**Since**
0.1.0

**Arguments**

| Param    | Type   | Description                   |
| :------- | :----- | :---------------------------- |
| `prefix` | `string` | The value to prefix the ID with. |

**Returns**

`(string)`: Returns the unique ID.

**Example**

```javascript
_.uniqueId('contact_');
// => 'contact_104'

_.uniqueId();
// => '105'
```

---

This concludes the reference for Lodash's miscellaneous utility functions. To explore other categories, you can return to the main [API Reference](./api.md).