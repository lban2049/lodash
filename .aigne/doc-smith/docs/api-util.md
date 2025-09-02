# Util

This section provides a detailed reference for the various utility functions in Lodash, which offer foundational capabilities for creating functions, handling function arguments, and performing other meta-programming tasks.

## Function List

| Function | Description |
| --- | --- |
| [_.attempt](#_attemptfunc-args) | Attempts to invoke a function, returning its result or the caught error object. |
| [_.bindAll](#_bindallobject-methodnames) | Binds methods of an object to the object itself, overwriting existing methods. |
| [_.cond](#_condpairs) | Creates a function that iterates through a series of predicate-function pairs and executes the function corresponding to the first predicate that returns a truthy value. |
| [_.conforms](#_conformssource) | Creates a function that checks if a given object conforms to the structure of `source` by invoking the predicate properties of `source`. |
| [_.constant](#_constantvalue) | Creates a function that returns the given value. |
| [_.defaultTo](#_defaulttovalue-defaultvalue) | Checks a value and returns a default value if it is `NaN`, `null`, or `undefined`. |
| [_.flow](#_flowfuncs) | Creates a function that returns the result of invoking a sequence of given functions, where the return value of each function is passed as an argument to the next. |
| [_.flowRight](#_flowrightfuncs) | Similar to `_.flow`, but invokes functions from right to left. |
| [_.identity](#_identityvalue) | Returns the first argument it receives. |
| [_.iteratee](#_iterateefunc) | Converts a value into an iteratee function that can be used in Lodash. |
| [_.matches](#_matchessource) | Creates a function that performs a partial deep comparison to determine if a given object contains equivalent property values. |
| [_.matchesProperty](#_matchespropertypath-srcvalue) | Creates a function that performs a partial deep comparison between the value at `path` of a given object and `srcValue`. |
| [_.method](#_methodpath-args) | Creates a function that invokes the method at `path` of a given object. |
| [_.methodOf](#_methodofobject-args) | The inverse of `_.method`; creates a function that invokes the method on `object` at a given path. |
| [_.mixin](#_mixinobject-source-options) | Adds all enumerable function properties of a source object to a destination object. |
| [_.noConflict](#_noconflict) | Reverts the `_` variable to its previous value and returns a reference to the `lodash` function. |
| [_.noop](#_noop) | A function that does nothing and returns `undefined`. |
| [_.nthArg](#_nthargn) | Creates a function that returns the nth argument. |
| [_.over](#_overiteratees) | Creates a function that invokes each iteratee with the received arguments and returns an array of the results. |
| [_.overEvery](#_overeverypredicates) | Creates a function that checks if all predicates return truthy when invoked. |
| [_.overSome](#_oversomepredicates) | Creates a function that checks if any predicate returns truthy when invoked. |
| [_.property](#_propertypath) | Creates a function that returns the value at `path` of a given object. |
| [_.propertyOf](#_propertyofobject) | The inverse of `_.property`; creates a function that returns the value at a given path of `object`. |
| [_.range](#_rangestart-end-step) | Creates an array of numbers in a range. |
| [_.rangeRight](#_rangerightstart-end-step) | Similar to `_.range`, but populates values in descending order. |
| [_.runInContext](#_runincontextcontext) | Creates a new, pristine `lodash` function using a `context` object. |
| [_.stubArray](#_stubarray) | Returns a new empty array. |
| [_.stubFalse](#_stubfalse) | Returns `false`. |
| [_.stubObject](#_stubobject) | Returns a new empty object. |
| [_.stubString](#_stubstring) | Returns an empty string. |
| [_.stubTrue](#_stubtrue) | Returns `true`. |
| [_.times](#_timesn-iteratee) | Invokes an iteratee n times, returning an array of the results from each invocation. |
| [_.toPath](#_topathvalue) | Converts a value to a property path array. |
| [_.uniqueId](#_uniqueidprefix) | Generates a unique ID. |

---

### _.attempt(func, [...args])

Attempts to invoke `func`, returning the result or the caught error object. Any additional arguments are provided to `func` when it's invoked.

**Since `3.0.0`**

**Arguments**

| Argument | Type | Description |
| --- | --- | --- |
| `func` | `Function` | The function to attempt. |
| `[...args]` | `*` | The arguments to invoke `func` with. |

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

### _.bindAll(object, methodNames)

Binds methods of an object to the object itself, overwriting existing methods.

**Note:** This method doesn't set the "length" property of bound functions.

**Since `0.1.0`**

**Arguments**

| Argument | Type | Description |
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
// => Logs 'clicked docs' on click.
```

### _.cond(pairs)

Creates a function that iterates through `pairs` (predicate-function pairs) and invokes the corresponding function of the first predicate to return a truthy value. The predicate-function pairs are invoked with the `this` binding and arguments of the created function.

**Since `4.0.0`**

**Arguments**

| Argument | Type | Description |
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

### _.conforms(source)

Creates a function that invokes the predicate properties of `source` with the corresponding property values of a given object. Returns `true` if all predicates return truthy, else `false`.

**Since `4.0.0`**

**Arguments**

| Argument | Type | Description |
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

### _.constant(value)

Creates a function that returns `value`.

**Since `2.4.0`**

**Arguments**

| Argument | Type | Description |
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

### _.defaultTo(value, defaultValue)

Checks `value` to determine if a default value should be returned. If `value` is `NaN`, `null`, or `undefined`, `defaultValue` is returned.

**Since `4.14.0`**

**Arguments**

| Argument | Type | Description |
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

### _.flow([...funcs])

Creates a function that returns the result of invoking the given functions in sequence, where each successive invocation is supplied the return value of the previous.

**Since `3.0.0`**

**Arguments**

| Argument | Type | Description |
| --- | --- | --- |
| `[...funcs]` | `...(Function|Function[])` | The functions to invoke. |

**Returns**

`(Function)`: Returns the new composite function.

**Example**

```javascript
function square(n) {
  return n * n;
}

var addSquare = _.flow([_.add, square]);
addSquare(1, 2);
// => 9
```

### _.flowRight([...funcs])

This method is like `_.flow` except that it creates a function that invokes the given functions from right to left.

**Since `3.0.0`**

**Arguments**

| Argument | Type | Description |
| --- | --- | --- |
| `[...funcs]` | `...(Function|Function[])` | The functions to invoke. |

**Returns**

`(Function)`: Returns the new composite function.

**Example**

```javascript
function square(n) {
  return n * n;
}

var addSquare = _.flowRight([square, _.add]);
addSquare(1, 2);
// => 9
```

### _.identity(value)

This method returns the first argument it receives.

**Since `0.1.0`**

**Arguments**

| Argument | Type | Description |
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

### _.iteratee([func=_.identity])

Creates a function that invokes `func` with the arguments of the created function. If `func` is a property name, the created function returns the property value of a given element. If `func` is an array or object, the created function returns `true` for elements that have equivalent source properties, otherwise it returns `false`.

**Since `4.0.0`**

**Arguments**

| Argument | Type | Description |
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
```

### _.matches(source)

Creates a function that performs a partial deep comparison between a given object and `source`, returning `true` if the given object has equivalent property values, else `false`.

**Since `3.0.0`**

**Arguments**

| Argument | Type | Description |
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

### _.matchesProperty(path, srcValue)

Creates a function that performs a partial deep comparison between the value at `path` of a given object and `srcValue`, returning `true` if the object value is equivalent, else `false`.

**Since `3.2.0`**

**Arguments**

| Argument | Type | Description |
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

### _.method(path, [...args])

Creates a function that invokes the method at `path` of a given object. Any additional arguments are provided to the invoked method.

**Since `3.7.0`**

**Arguments**

| Argument | Type | Description |
| --- | --- | --- |
| `path` | `Array|string` | The path of the method to invoke. |
| `[...args]` | `*` | The arguments to invoke the method with. |

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
```

### _.methodOf(object, [...args])

The inverse of `_.method`; this method creates a function that invokes the method at a given path on `object`. Any additional arguments are provided to the invoked method.

**Since `3.7.0`**

**Arguments**

| Argument | Type | Description |
| --- | --- | --- |
| `object` | `Object` | The object to query. |
| `[...args]` | `*` | The arguments to invoke the method with. |

**Returns**

`(Function)`: Returns the new invoker function.

**Example**

```javascript
var array = _.times(3, _.constant),
    object = { 'a': array, 'b': array, 'c': array };

_.map(['a[2]', 'c[0]'], _.methodOf(object));
// => [2, 0]
```

### _.mixin([object=lodash], source, [options={}])

Adds all own enumerable string keyed function properties of a source object to the destination object. If `object` is a function, methods are added to its prototype as well.

**Since `0.1.0`**

**Arguments**

| Argument | Type | Description |
| --- | --- | --- |
| `[object=lodash]` | `Function|Object` | The destination object. |
| `source` | `Object` | The object of functions to add. |
| `[options={}]` | `Object` | The options object. |
| `[options.chain=true]` | `boolean` | Specify whether the mixins are chainable. |

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
```

### _.noConflict()

Reverts the `_` variable to its previous value and returns a reference to the `lodash` function.

**Since `0.1.0`**

**Returns**

`(Function)`: Returns the `lodash` function.

**Example**

```javascript
var lodash = _.noConflict();
```

### _.noop()

This method returns `undefined`.

**Since `2.3.0`**

**Example**

```javascript
_.times(2, _.noop);
// => [undefined, undefined]
```

### _.nthArg([n=0])

Creates a function that gets the `n`th argument. If `n` is negative, the nth argument from the end is returned.

**Since `4.0.0`**

**Arguments**

| Argument | Type | Description |
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

### _.over([...iteratees=[_.identity]])

Creates a function that invokes `iteratees` with the arguments it receives and returns their results.

**Since `4.o.0`**

**Arguments**

| Argument | Type | Description |
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

### _.overEvery([...predicates=[_.identity]])

Creates a function that checks if all `predicates` return truthy when invoked with the arguments it receives.

**Since `4.0.0`**

**Arguments**

| Argument | Type | Description |
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
```

### _.overSome([...predicates=[_.identity]])

Creates a function that checks if any of the `predicates` return truthy when invoked with the arguments it receives.

**Since `4.0.0`**

**Arguments**

| Argument | Type | Description |
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
```

### _.property(path)

Creates a function that returns the value at `path` of a given object.

**Since `2.4.0`**

**Arguments**

| Argument | Type | Description |
| --- | --- | --- |
| `path` | `Array|string` | The path of the property to retrieve. |

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
```

### _.propertyOf(object)

The inverse of `_.property`; this method creates a function that returns the value at a given path of `object`.

**Since `3.0.0`**

**Arguments**

| Argument | Type | Description |
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
```

### _.range([start=0], end, [step=1])

Creates an array of numbers from `start` up to, but not including, `end`. If `start` is negative and `end` or `step` is not specified, `step` is `-1`. If `end` is not specified, it's set to `start` with `start` then set to `0`.

**Since `0.1.0`**

**Arguments**

| Argument | Type | Description |
| --- | --- | --- |
| `[start=0]` | `number` | The start of the range. |
| `end` | `number` | The end of the range. |
| `[step=1]` | `number` | The value to increment or decrement by. |

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

### _.rangeRight([start=0], end, [step=1])

This method is like `_.range` except that it populates values in descending order.

**Since `4.0.0`**

**Arguments**

| Argument | Type | Description |
| --- | --- | --- |
| `[start=0]` | `number` | The start of the range. |
| `end` | `number` | The end of the range. |
| `[step=1]` | `number` | The value to increment or decrement by. |

**Returns**

`(Array)`: Returns the range of numbers.

**Example**

```javascript
_.rangeRight(4);
// => [3, 2, 1, 0]

_.rangeRight(1, 5);
// => [4, 3, 2, 1]
```

### _.runInContext([context=root])

Creates a new, pristine `lodash` function using the `context` object.

**Since `1.1.0`**

**Arguments**

| Argument | Type | Description |
| --- | --- | --- |
| `[context=root]` | `Object` | The context object. |

**Returns**

`(Function)`: Returns a new `lodash` function.

**Example**

```javascript
_.mixin({ 'foo': _.constant('foo') });

var lodash = _.runInContext();
lodash.mixin({ 'bar': lodash.constant('bar') });

_.isFunction(_.foo);
// => true
_.isFunction(_.bar);
// => false

lodash.isFunction(lodash.foo);
// => false
lodash.isFunction(lodash.bar);
// => true

// Create a suped-up `defer` in Node.js.
var defer = _.runInContext({ 'setTimeout': setImmediate }).defer;
```

### _.stubArray()

This method returns a new empty array.

**Since `4.13.0`**

**Returns**

`(Array)`: Returns the new empty array.

**Example**

```javascript
var arrays = _.times(2, _.stubArray);

console.log(arrays);
// => [[], []]
```

### _.stubFalse()

This method returns `false`.

**Since `4.13.0`**

**Returns**

`(boolean)`: Returns `false`.

**Example**

```javascript
_.times(2, _.stubFalse);
// => [false, false]
```

### _.stubObject()

This method returns a new empty object.

**Since `4.13.0`**

**Returns**

`(Object)`: Returns the new empty object.

**Example**

```javascript
var objects = _.times(2, _.stubObject);

console.log(objects);
// => [{}, {}]
```

### _.stubString()

This method returns an empty string.

**Since `4.13.0`**

**Returns**

`(string)`: Returns the empty string.

**Example**

```javascript
_.times(2, _.stubString);
// => ['', '']
```

### _.stubTrue()

This method returns `true`.

**Since `4.13.0`**

**Returns**

`(boolean)`: Returns `true`.

**Example**

```javascript
_.times(2, _.stubTrue);
// => [true, true]
```

### _.times(n, [iteratee=_.identity])

Invokes `iteratee` `n` times, returning an array of the results of each invocation. The `iteratee` is invoked with one argument: `(index)`.

**Since `0.1.0`**

**Arguments**

| Argument | Type | Description |
| --- | --- | --- |
| `n` | `number` | The number of times to invoke `iteratee`. |
| `[iteratee=_.identity]` | `Function` | The function invoked per iteration. |

**Returns**

`(Array)`: Returns the array of results.

**Example**

```javascript
_.times(3, String);
// => ['0', '1', '2']
```

### _.toPath(value)

Converts `value` to a property path array.

**Since `4.0.0`**

**Arguments**

| Argument | Type | Description |
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

### _.uniqueId([prefix=''])

Generates a unique ID. If `prefix` is given, the ID is appended to it.

**Since `0.1.0`**

**Arguments**

| Argument | Type | Description |
| --- | --- | --- |
| `[prefix='']` | `string` | The prefix of the ID. |

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

Now that you're familiar with Lodash's utility functions, feel free to explore the documentation for the [Function](./api-function.md) or [Seq](./api-seq.md) sections to learn more about functional programming and chaining.
