# Util

A detailed reference for miscellaneous Lodash utility functions. These functions provide a wide range of helpers, from creating new functions and controlling invocation to generating unique IDs and managing function context.

---

## _.attempt(func, [...args])

Attempts to invoke `func`, returning either the result or the caught error object. Any additional arguments are provided to `func` when it's invoked.

**Since**: 3.0.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
| `func` | `Function` | The function to attempt. |
| `[...args]` | `...*` | The arguments to invoke `func` with. |

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

## _.bindAll(object, methodNames)

Binds methods of an object to the object itself, overwriting the existing method.

**Note**: This method doesn't set the "length" property of bound functions.

**Since**: 0.1.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
| `object` | `Object` | The object to bind and assign the bound methods to. |
| `methodNames` | `...(string|string[])` | The object method names to bind. |

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

## _.cond(pairs)

Creates a function that iterates over `pairs` and invokes the corresponding function of the first predicate to return truthy. The predicate-function pairs are invoked with the `this` binding and arguments of the created function.

**Since**: 4.0.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
| `pairs` | `Array` | The predicate-function pairs. |

**Returns**

`(Function)`: Returns the new composite function.

**Example**

```javascript
var func = _.cond([
  [_.matches({ 'a': 1 }),           _.constant('matches A')],
  [_.conforms({ 'b': _.isNumber }), _.constant('matches B')],
  [_.stubTrue,                      _.constant('no match')]
]);

func({ 'a': 1, 'b': 2 });
// => 'matches A'

func({ 'a': 0, 'b': 1 });
// => 'matches B'

func({ 'a': '1', 'b': '2' });
// => 'no match'
```

---

## _.conforms(source)

Creates a function that invokes the predicate properties of `source` with the corresponding property values of a given object, returning `true` if all predicates return truthy, else `false`.

**Note**: The created function is equivalent to `_.conformsTo` with `source` partially applied.

**Since**: 4.0.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
| `source` | `Object` | The object of property predicates to conform to. |

**Returns**

`(Function)`: Returns the new spec function.

**Example**

```javascript
var objects = [
  { 'a': 2, 'b': 1 },
  { 'a': 1, 'b': 2 }
];

_.filter(objects, _.conforms({ 'b': function(n) { return n > 1; } }));
// => [{ 'a': 1, 'b': 2 }]
```

---

## _.constant(value)

Creates a function that returns `value`.

**Since**: 2.4.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
| `value` | `*` | The value to return from the new function. |

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

## _.defaultTo(value, defaultValue)

Checks `value` to determine whether a default value should be returned in its place. The `defaultValue` is returned if `value` is `NaN`, `null`, or `undefined`.

**Since**: 4.14.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
| `value` | `*` | The value to check. |
| `defaultValue` | `*` | The default value. |

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

## _.flow([...funcs])

Creates a function that returns the result of invoking the given functions from left to right. Each successive invocation is supplied the return value of the previous.

**Since**: 3.0.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
| `[...funcs]` | `...(Function|Function[])` | The functions to invoke. |

**Returns**

`(Function)`: Returns the new composite function.

**See Also**: `_.flowRight`

**Example**

```javascript
function square(n) {
  return n * n;
}

var addSquare = _.flow([_.add, square]);
addSquare(1, 2);
// => 9
```

---

## _.flowRight([...funcs])

This method is like `_.flow` except that it creates a function that invokes the given functions from right to left.

**Since**: 3.0.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
| `[...funcs]` | `...(Function|Function[])` | The functions to invoke. |

**Returns**

`(Function)`: Returns the new composite function.

**See Also**: `_.flow`

**Example**

```javascript
function square(n) {
  return n * n;
}

var addSquare = _.flowRight([square, _.add]);
addSquare(1, 2);
// => 9
```

---

## _.identity(value)

This method returns the first argument it receives.

**Since**: 0.1.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
| `value` | `*` | Any value. |

**Returns**

`(*)`: Returns `value`.

**Example**

```javascript
var object = { 'a': 1 };

console.log(_.identity(object) === object);
// => true
```

---

## _.iteratee([func=_.identity])

Creates a function that invokes `func` with the arguments of the created function. If `func` is a property name, the created function returns the property value for a given element. If `func` is an array or object, the created function returns `true` for elements that contain the equivalent source properties, otherwise it returns `false`.

**Since**: 4.0.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
| `[func=_.identity]` | `*` | The value to convert to a callback. |

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

## _.matches(source)

Creates a function that performs a partial deep comparison between a given object and `source`, returning `true` if the given object has equivalent property values, else `false`.

**Since**: 3.0.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
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

## _.matchesProperty(path, srcValue)

Creates a function that performs a partial deep comparison between the value at `path` of a given object to `srcValue`, returning `true` if the object value is equivalent, else `false`.

**Since**: 3.2.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
| `path` | `Array|string` | The path of the property to get. |
| `srcValue` | `*` | The value to match. |

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

## _.method(path, [...args])

Creates a function that invokes the method at `path` of a given object. Any additional arguments are provided to the invoked method.

**Since**: 3.7.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
| `path` | `Array|string` | The path of the method to invoke. |
| `[...args]` | `...*` | The arguments to invoke the method with. |

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

## _.methodOf(object, [...args])

The opposite of `_.method`; this method creates a function that invokes the method at a given path of `object`. Any additional arguments are provided to the invoked method.

**Since**: 3.7.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
| `object` | `Object` | The object to query. |
| `[...args]` | `...*` | The arguments to invoke the method with. |

**Returns**

`(Function)`: Returns the new invoker function.

**Example**

```javascript
var array = _.times(3, _.constant),
    object = { 'a': array, 'b': array, 'c': array };

_.map(['a[2]', 'c[0]'], _.methodOf(object));
// => [2, 0]

_.map([['a', '2'], ['c', '0']], _.methodOf(object));
// => [2, 0]
```

---

## _.mixin([object=lodash], source, [options={}])

Adds all own enumerable string keyed function properties of a source object to the destination object. If `object` is a function, then methods are added to its prototype as well.

**Since**: 0.1.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
| `[object=lodash]` | `Function|Object` | The destination object. |
| `source` | `Object` | The object of functions to add. |
| `[options={}]` | `Object` | The options object. |
| `[options.chain=true]` | `boolean` | Specify whether mixins are chainable. |

**Returns**

`(Function|Object)`: Returns `object`.

**Example**

```javascript
function vowels(string) {
  return _.filter(string, function(v) {
    return /[aeiou]/i.test(v);
  });
}

_.mixin({ 'vowels': vowels });
_.vowels('fred');
// => ['e']

_('fred').vowels().value();
// => ['e']
```

---

## _.noConflict()

Reverts the `_` variable to its previous value and returns a reference to the `lodash` function.

**Since**: 0.1.0

**Returns**

`(Function)`: Returns the `lodash` function.

**Example**

```javascript
var lodash = _.noConflict();
```

---

## _.noop()

This method returns `undefined`.

**Since**: 2.3.0

**Example**

```javascript
_.times(2, _.noop);
// => [undefined, undefined]
```

---

## _.nthArg([n=0])

Creates a function that gets the argument at index `n`. If `n` is negative, the nth argument from the end is returned.

**Since**: 4.0.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
| `[n=0]` | `number` | The index of the argument to return. |

**Returns**

`(Function)`: Returns the new pass-thru function.

**Example**

```javascript
var func = _.nthArg(1);
func('a', 'b', 'c', 'd');
// => 'b'

var func = _.nthArg(-2);
func('a', 'b', 'c', 'd');
// => 'c'
```

---

## _.over([...iteratees=[_.identity]])

Creates a function that invokes `iteratees` with the arguments it receives and returns their results.

**Since**: 4.0.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
| `[...iteratees=[_.identity]]` | `...(Function|Function[])` | The iteratees to invoke. |

**Returns**

`(Function)`: Returns the new function.

**Example**

```javascript
var func = _.over([Math.max, Math.min]);

func(1, 2, 3, 4);
// => [4, 1]
```

---

## _.overEvery([...predicates=[_.identity]])

Creates a function that checks if **all** of the `predicates` return truthy when invoked with the arguments it receives.

**Since**: 4.0.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
| `[...predicates=[_.identity]]` | `...(Function|Function[])` | The predicates to check. |

**Returns**

`(Function)`: Returns the new function.

**Example**

```javascript
var func = _.overEvery([Boolean, isFinite]);

func('1');
// => true

func(null);
// => false

func(NaN);
// => false
```

---

## _.overSome([...predicates=[_.identity]])

Creates a function that checks if **any** of the `predicates` return truthy when invoked with the arguments it receives.

**Since**: 4.0.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
| `[...predicates=[_.identity]]` | `...(Function|Function[])` | The predicates to check. |

**Returns**

`(Function)`: Returns the new function.

**Example**

```javascript
var func = _.overSome([Boolean, isFinite]);

func('1');
// => true

func(null);
// => true

func(NaN);
// => false
```

---

## _.property(path)

Creates a function that returns the value at `path` of a given object.

**Since**: 2.4.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
| `path` | `Array|string` | The path of the property to get. |

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

## _.propertyOf(object)

The opposite of `_.property`; this method creates a function that returns the value at a given path of `object`.

**Since**: 3.0.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
| `object` | `Object` | The object to query. |

**Returns**

`(Function)`: Returns the new accessor function.

**Example**

```javascript
var array = [0, 1, 2],
    object = { 'a': array, 'b': array, 'c': array };

_.map(['a[2]', 'c[0]'], _.propertyOf(object));
// => [2, 0]

_.map([['a', '2'], ['c', '0']], _.propertyOf(object));
// => [2, 0]
```

---

## _.range([start=0], end, [step=1])

Creates an array of numbers progressing from `start` up to, but not including, `end`.

**Since**: 0.1.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
| `[start=0]` | `number` | The start of the range. |
| `end` | `number` | The end of the range. |
| `[step=1]` | `number` | The value to increment or decrement by. |

**Returns**

`(Array)`: Returns the range of numbers.

**See Also**: `_.rangeRight`

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

## _.rangeRight([start=0], end, [step=1])

This method is like `_.range` except that it populates values in descending order.

**Since**: 4.0.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
| `[start=0]` | `number` | The start of the range. |
| `end` | `number` | The end of the range. |
| `[step=1]` | `number` | The value to increment or decrement by. |

**Returns**

`(Array)`: Returns the range of numbers.

**See Also**: `_.range`

**Example**

```javascript
_.rangeRight(4);
// => [3, 2, 1, 0]

_.rangeRight(1, 5);
// => [4, 3, 2, 1]
```

---

## _.runInContext([context=root])

Create a new pristine `lodash` function using the `context` object.

**Since**: 1.1.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
| `[context=root]` | `Object` | The context object. |

**Returns**

`(Function)`: Returns a new `lodash` function.

**Example**

```javascript
_.mixin({ 'foo': _.constant('foo') });

var lodash = _.runInContext();
lodash.mixin({ 'bar': lodash.constant('bar') });

_.isFunction(_.bar);
// => false

lodash.isFunction(lodash.bar);
// => true
```

---

## Stub Functions

These functions return a constant value and are useful as default iteratees.

| Function | Return Value | Since |
| --- | --- | --- |
| `_.stubArray()` | `[]` (a new empty array) | 4.13.0 |
| `_.stubFalse()` | `false` | 4.13.0 |
| `_.stubObject()` | `{}` (a new empty object) | 4.13.0 |
| `_.stubString()` | `''` (an empty string) | 4.13.0 |
| `_.stubTrue()` | `true` | 4.13.0 |

**Example**

```javascript
var objects = _.times(2, _.stubObject);

console.log(objects);
// => [{}, {}]

console.log(objects[0] === objects[1]);
// => false
```

---

## _.times(n, [iteratee=_.identity])

Invokes the iteratee `n` times, returning an array of the results of each invocation. The iteratee is invoked with one argument: (index).

**Since**: 0.1.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
| `n` | `number` | The number of times to invoke `iteratee`. |
| `[iteratee=_.identity]` | `Function` | The function invoked per iteration. |

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

## _.toPath(value)

Converts `value` to a property path array.

**Since**: 4.0.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
| `value` | `*` | The value to convert. |

**Returns**

`(Array)`: Returns the new property path array.

**Example**

```javascript
_.toPath('a.b.c');
// => ['a', 'b', 'c']

_.toPath('a[0].b.c');
// => ['a', '0', 'b', 'c']
```

---

## _.uniqueId([prefix=''])

Generates a unique ID. If `prefix` is given, the ID is appended to it.

**Since**: 0.1.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
| `[prefix='']` | `string` | The value to prefix the ID with. |

**Returns**

`(string)`: Returns the unique ID.

**Example**

```javascript
_.uniqueId('contact_');
// => 'contact_104'

_.uniqueId();
// => '105'
```
