# Util

The Util category provides a collection of miscellaneous utility functions that don't neatly fit into other categories. These functions help with common programming tasks such as creating function compositions, generating unique IDs, managing properties, and more. They are powerful tools for simplifying complex logic and improving code readability.

For more function-related utilities, explore the [Function](./api-function.md) category. For type-checking and cloning, see the [Lang](./api-lang.md) category.

---

### attempt

Attempts to invoke `func`, returning either the result or the caught error object. Any additional arguments are provided to `func` when it's invoked.

**Parameters**

<x-field data-name="func" data-type="Function" data-required="true" data-desc="The function to attempt."></x-field>
<x-field data-name="...args" data-type="any" data-required="false" data-desc="The arguments to invoke func with."></x-field>

**Returns**

<x-field data-name="" data-type="any" data-desc="Returns the func result or error object."></x-field>

**Example**

```javascript
// Avoid throwing errors for invalid operations.
var elements = _.attempt(function(value) {
  if (typeof value !== 'number') {
    throw new TypeError('Expected a number');
  }
  return value * 2;
}, 'oops');

if (_.isError(elements)) {
  console.log('Caught an error!');
  elements = [];
}
// => Logs 'Caught an error!'
```

---

### bindAll

Binds methods of an object to the object itself, overwriting the existing methods. This is useful for ensuring that methods have the correct `this` context when passed as callbacks.

**Note:** This method doesn't set the "length" property of bound functions.

**Parameters**

<x-field data-name="object" data-type="Object" data-required="true" data-desc="The object to bind and assign the bound methods to."></x-field>
<x-field data-name="...methodNames" data-type="string|string[]" data-required="true" data-desc="The object method names to bind."></x-field>

**Returns**

<x-field data-name="" data-type="Object" data-desc="Returns the modified object."></x-field>

**Example**

```javascript
var view = {
  'label': 'docs',
  'click': function() {
    console.log('clicked ' + this.label);
  }
};

_.bindAll(view, ['click']);

// When view.click is used as a callback, `this` will refer to `view`.
// setTimeout(view.click, 100); // => Logs 'clicked docs' after 100ms.
```

---

### cond

Creates a function that iterates over `pairs` and invokes the corresponding function of the first predicate to return truthy. The predicate-function pairs are invoked with the `this` binding and arguments of the created function.

**Parameters**

<x-field data-name="pairs" data-type="Array" data-required="true" data-desc="The predicate-function pairs."></x-field>

**Returns**

<x-field data-name="" data-type="Function" data-desc="Returns the new composite function."></x-field>

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

### conforms

Creates a function that invokes the predicate properties of `source` with the corresponding property values of a given object, returning `true` if all predicates return truthy, else `false`.

**Note:** The created function is equivalent to `_.conformsTo` with `source` partially applied.

**Parameters**

<x-field data-name="source" data-type="Object" data-required="true" data-desc="The object of property predicates to conform to."></x-field>

**Returns**

<x-field data-name="" data-type="Function" data-desc="Returns the new spec function."></x-field>

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

### constant

Creates a function that returns the `value` it was created with. No matter what arguments are passed to the function, it will always return the same value.

**Parameters**

<x-field data-name="value" data-type="any" data-required="true" data-desc="The value to return from the new function."></x-field>

**Returns**

<x-field data-name="" data-type="Function" data-desc="Returns the new constant function."></x-field>

**Example**

```javascript
var objects = _.times(2, _.constant({ 'a': 1 }));

console.log(objects);
// => [{ 'a': 1 }, { 'a': 1 }]

console.log(objects[0] === objects[1]);
// => true
```

---

### defaultTo

Checks `value` to determine whether a default value should be returned in its place. The `defaultValue` is returned if `value` is `NaN`, `null`, or `undefined`.

**Parameters**

<x-field data-name="value" data-type="any" data-required="true" data-desc="The value to check."></x-field>
<x-field data-name="defaultValue" data-type="any" data-required="true" data-desc="The default value."></x-field>

**Returns**

<x-field data-name="" data-type="any" data-desc="Returns the resolved value."></x-field>

**Example**

```javascript
_.defaultTo(1, 10);
// => 1

_.defaultTo(undefined, 10);
// => 10
```

---

### flow

Creates a function that returns the result of invoking the given functions from left to right. Each successive function is invoked with the return value of the previous.

**Parameters**

<x-field data-name="...funcs" data-type="Function|Function[]" data-required="false" data-desc="The functions to invoke."></x-field>

**Returns**

<x-field data-name="" data-type="Function" data-desc="Returns the new composite function."></x-field>

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

### flowRight

This method is like `_.flow` except that it creates a function that invokes the given functions from right to left.

**Parameters**

<x-field data-name="...funcs" data-type="Function|Function[]" data-required="false" data-desc="The functions to invoke."></x-field>

**Returns**

<x-field data-name="" data-type="Function" data-desc="Returns the new composite function."></x-field>

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

### identity

This method returns the first argument it receives. It's useful as a default iteratee.

**Parameters**

<x-field data-name="value" data-type="any" data-required="true" data-desc="Any value."></x-field>

**Returns**

<x-field data-name="" data-type="any" data-desc="Returns value."></x-field>

**Example**

```javascript
var object = { 'a': 1 };

_.identity(object) === object;
// => true
```

---

### iteratee

Creates a function that can be used as an iteratee for other Lodash methods. It accepts various shorthands:
- **String**: Creates a `_.property` iteratee.
- **Array**: Creates a `_.matchesProperty` iteratee.
- **Object**: Creates a `_.matches` iteratee.

**Parameters**

<x-field data-name="func" data-type="any" data-default="_.identity" data-desc="The value to convert to a callback."></x-field>

**Returns**

<x-field data-name="" data-type="Function" data-desc="Returns the callback."></x-field>

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
// => [{ 'user': 'fred', 'age': 40, 'active': false }]

// The `_.property` iteratee shorthand.
_.map(users, _.iteratee('user'));
// => ['barney', 'fred']
```

---

### matches

Creates a function that performs a partial deep comparison between a given object and `source`, returning `true` if the given object has equivalent property values, else `false`.

**Parameters**

<x-field data-name="source" data-type="Object" data-required="true" data-desc="The object of property values to match."></x-field>

**Returns**

<x-field data-name="" data-type="Function" data-desc="Returns the new spec function."></x-field>

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

### matchesProperty

Creates a function that performs a partial deep comparison between the value at `path` of a given object to `srcValue`, returning `true` if the object value is equivalent, else `false`.

**Parameters**

<x-field data-name="path" data-type="Array|string" data-required="true" data-desc="The path of the property to get."></x-field>
<x-field data-name="srcValue" data-type="any" data-required="true" data-desc="The value to match."></x-field>

**Returns**

<x-field data-name="" data-type="Function" data-desc="Returns the new spec function."></x-field>

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

### method

Creates a function that invokes the method at `path` of a given object. Any additional arguments are provided to the invoked method.

**Parameters**

<x-field data-name="path" data-type="Array|string" data-required="true" data-desc="The path of the method to invoke."></x-field>
<x-field data-name="...args" data-type="any" data-required="false" data-desc="The arguments to invoke the method with."></x-field>

**Returns**

<x-field data-name="" data-type="Function" data-desc="Returns the new invoker function."></x-field>

**Example**

```javascript
var objects = [
  { 'a': { 'b': _.constant(2) } },
  { 'a': { 'b': _.constant(1) } }
];

_.map(objects, _.method('a.b'));
// => [2, 1]
```

---

### methodOf

The opposite of `_.method`; this method creates a function that invokes the method at a given path of `object`. Any additional arguments are provided to the invoked method.

**Parameters**

<x-field data-name="object" data-type="Object" data-required="true" data-desc="The object to query."></x-field>
<x-field data-name="...args" data-type="any" data-required="false" data-desc="The arguments to invoke the method with."></x-field>

**Returns**

<x-field data-name="" data-type="Function" data-desc="Returns the new invoker function."></x-field>

**Example**

```javascript
var array = [0, 1, 2],
    object = { 'a': array, 'b': array, 'c': array };

_.map(['a[2]', 'c[0]'], _.methodOf(object));
// => [2, 0]
```

---

### mixin

Adds all own enumerable string keyed function properties of a source object to the destination object. If `object` is a function, then methods are added to its prototype as well.

**Parameters**

<x-field data-name="object" data-type="Function|Object" data-default="lodash" data-desc="The destination object."></x-field>
<x-field data-name="source" data-type="Object" data-required="true" data-desc="The object of functions to add."></x-field>
<x-field data-name="options" data-type="Object" data-required="false" data-desc="The options object.">
  <x-field data-name="chain" data-type="boolean" data-default="true" data-desc="Specify whether mixins are chainable."></x-field>
</x-field>

**Returns**

<x-field data-name="" data-type="Function|Object" data-desc="Returns object."></x-field>

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

### noConflict

Reverts the `_` variable to its previous value and returns a reference to the `lodash` function. This is useful for avoiding namespace collisions in environments where another library might also use the underscore variable.

**Returns**

<x-field data-name="" data-type="Function" data-desc="Returns the lodash function."></x-field>

**Example**

```javascript
// In a browser environment where another library uses `_`
var lodash = _.noConflict();
// `_` is now restored to its original value.
// `lodash` can be used to call Lodash functions.
```

---

### noop

This method returns `undefined`. It's a useful placeholder for functions or callbacks that do nothing.

**Example**

```javascript
_.times(2, _.noop);
// => [undefined, undefined]
```

---

### nthArg

Creates a function that gets the argument at index `n`. If `n` is negative, the nth argument from the end is returned.

**Parameters**

<x-field data-name="n" data-type="number" data-default="0" data-desc="The index of the argument to return."></x-field>

**Returns**

<x-field data-name="" data-type="Function" data-desc="Returns the new pass-thru function."></x-field>

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

### over

Creates a function that invokes `iteratees` with the arguments it receives and returns their results as an array.

**Parameters**

<x-field data-name="...iteratees" data-type="Function|Function[]" data-default="_.identity" data-desc="The iteratees to invoke."></x-field>

**Returns**

<x-field data-name="" data-type="Function" data-desc="Returns the new function."></x-field>

**Example**

```javascript
var func = _.over([Math.max, Math.min]);

func(1, 2, 3, 4);
// => [4, 1]
```

---

### overEvery

Creates a function that checks if **all** of the `predicates` return truthy when invoked with the arguments it receives.

**Parameters**

<x-field data-name="...predicates" data-type="Function|Function[]" data-default="_.identity" data-desc="The predicates to check."></x-field>

**Returns**

<x-field data-name="" data-type="Function" data-desc="Returns the new function."></x-field>

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

### overSome

Creates a function that checks if **any** of the `predicates` return truthy when invoked with the arguments it receives.

**Parameters**

<x-field data-name="...predicates" data-type="Function|Function[]" data-default="_.identity" data-desc="The predicates to check."></x-field>

**Returns**

<x-field data-name="" data-type="Function" data-desc="Returns the new function."></x-field>

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

### property

Creates a function that returns the value at `path` of a given object.

**Parameters**

<x-field data-name="path" data-type="Array|string" data-required="true" data-desc="The path of the property to get."></x-field>

**Returns**

<x-field data-name="" data-type="Function" data-desc="Returns the new accessor function."></x-field>

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

### propertyOf

The opposite of `_.property`; this method creates a function that returns the value at a given path of `object`.

**Parameters**

<x-field data-name="object" data-type="Object" data-required="true" data-desc="The object to query."></x-field>

**Returns**

<x-field data-name="" data-type="Function" data-desc="Returns the new accessor function."></x-field>

**Example**

```javascript
var array = [0, 1, 2],
    object = { 'a': array, 'b': array, 'c': array };

_.map(['a[2]', 'c[0]'], _.propertyOf(object));
// => [2, 0]
```

---

### range

Creates an array of numbers (positive and/or negative) progressing from `start` up to, but not including, `end`.

**Parameters**

<x-field data-name="start" data-type="number" data-default="0" data-desc="The start of the range."></x-field>
<x-field data-name="end" data-type="number" data-required="true" data-desc="The end of the range."></x-field>
<x-field data-name="step" data-type="number" data-default="1" data-desc="The value to increment or decrement by."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns the range of numbers."></x-field>

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

### rangeRight

This method is like `_.range` except that it populates values in descending order.

**Parameters**

<x-field data-name="start" data-type="number" data-default="0" data-desc="The start of the range."></x-field>
<x-field data-name="end" data-type="number" data-required="true" data-desc="The end of the range."></x-field>
<x-field data-name="step" data-type="number" data-default="1" data-desc="The value to increment or decrement by."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns the range of numbers."></x-field>

**Example**

```javascript
_.rangeRight(4);
// => [3, 2, 1, 0]

_.rangeRight(1, 5);
// => [4, 3, 2, 1]
```

---

### stubArray

This method returns a new empty array. It's useful as a default value or callback that should return an array.

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns the new empty array."></x-field>

**Example**

```javascript
var arrays = _.times(2, _.stubArray);

console.log(arrays);
// => [[], []]

console.log(arrays[0] === arrays[1]);
// => false
```

---

### stubFalse

This method returns `false`. It's useful as a default predicate that always fails.

**Returns**

<x-field data-name="" data-type="boolean" data-desc="Returns false."></x-field>

**Example**

```javascript
_.times(2, _.stubFalse);
// => [false, false]
```

---

### stubObject

This method returns a new empty object. It's useful as a default value or callback that should return an object.

**Returns**

<x-field data-name="" data-type="Object" data-desc="Returns the new empty object."></x-field>

**Example**

```javascript
var objects = _.times(2, _.stubObject);

console.log(objects);
// => [{}, {}]

console.log(objects[0] === objects[1]);
// => false
```

---

### stubString

This method returns an empty string. It's useful as a default value or callback that should return a string.

**Returns**

<x-field data-name="" data-type="string" data-desc="Returns the empty string."></x-field>

**Example**

```javascript
_.times(2, _.stubString);
// => ['', '']
```

---

### stubTrue

This method returns `true`. It's useful as a default predicate that always passes.

**Returns**

<x-field data-name="" data-type="boolean" data-desc="Returns true."></x-field>

**Example**

```javascript
_.times(2, _.stubTrue);
// => [true, true]
```

---

### times

Invokes the iteratee `n` times, returning an array of the results of each invocation. The iteratee is invoked with one argument: `index`.

**Parameters**

<x-field data-name="n" data-type="number" data-required="true" data-desc="The number of times to invoke iteratee."></x-field>
<x-field data-name="iteratee" data-type="Function" data-default="_.identity" data-desc="The function invoked per iteration."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns the array of results."></x-field>

**Example**

```javascript
_.times(3, String);
// => ['0', '1', '2']

_.times(4, _.constant(0));
// => [0, 0, 0, 0]
```

---

### toPath

Converts `value` to a property path array. This is useful for normalizing property accessors.

**Parameters**

<x-field data-name="value" data-type="any" data-required="true" data-desc="The value to convert."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns the new property path array."></x-field>

**Example**

```javascript
_.toPath('a.b.c');
// => ['a', 'b', 'c']

_.toPath('a[0].b.c');
// => ['a', '0', 'b', 'c']
```

---

### uniqueId

Generates a unique ID. If `prefix` is given, the ID is appended to it.

**Parameters**

<x-field data-name="prefix" data-type="string" data-default="''" data-desc="The value to prefix the ID with."></x-field>

**Returns**

<x-field data-name="" data-type="string" data-desc="Returns the unique ID."></x-field>

**Example**

```javascript
_.uniqueId('contact_');
// => 'contact_1'

_.uniqueId();
// => '2'
```
