# API Reference

This section serves as a comprehensive guide to all Lodash methods, categorized by their primary data type or utility. Each method entry provides its syntax, detailed parameters, expected return values, and practical examples to aid you in development.

For a foundational understanding of Lodash's architecture and design principles, refer to the [Core Concepts](./core-concepts.md) section. If you are interested in functional programming with Lodash, explore the [Functional Programming (FP)](./functional-programming.md) guide.

## Array Methods

### chunk

Creates an array of elements split into groups the length of `size`. If `array` can't be split evenly, the final chunk will be the remaining elements.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to process. |
| `size` | `number` | The length of each chunk (default: 1). |
| `guard` | `Object` | Enables use as an iteratee for methods like `_.map`. |

**Returns**

| Name | Type | Description |
|---|---|---|
| `Array` | `Array` | Returns the new array of chunks. |

**Example**

```javascript
_.chunk(['a', 'b', 'c', 'd'], 2);
// => [['a', 'b'], ['c', 'd']]

_.chunk(['a', 'b', 'c', 'd'], 3);
// => [['a', 'b', 'c'], ['d']]
```

This example demonstrates how `_.chunk` divides an array into smaller arrays of a specified size.

### compact

Creates an array with all falsey values removed. The values `false`, `null`, `0`, `""`, `undefined`, and `NaN` are falsey.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to compact. |

**Returns**

| Name | Type | Description |
|---|---|---|
| `Array` | `Array` | Returns the new array of filtered values. |

**Example**

```javascript
_.compact([0, 1, false, 2, '', 3]);
// => [1, 2, 3]
```

This example shows `_.compact` removing all falsey values from an array, leaving only truthy elements.

### head

Gets the first element of `array`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to query. |

**Returns**

| Name | Type | Description |
|---|---|---|
| `*` | `*` | Returns the first element of `array`. |

**Example**

```javascript
_.head([1, 2, 3]);
// => 1

_.head([]);
// => undefined
```

This example retrieves the first element from an array using `_.head`.

### tail

Gets all but the first element of `array`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `array` | `Array` | The array to query. |

**Returns**

| Name | Type | Description |
|---|---|---|
| `Array` | `Array` | Returns the slice of `array`. |

**Example**

```javascript
_.tail([1, 2, 3]);
// => [2, 3]
```

This example demonstrates how `_.tail` returns all elements of an array except the first one.

### union

Creates an array of unique values, in order, from all given arrays using `SameValueZero` for equality comparisons.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `arrays` | `Array` | The arrays to inspect. |

**Returns**

| Name | Type | Description |
|---|---|---|
| `Array` | `Array` | Returns the new array of combined values. |

**Example**

```javascript
_.union([2], [1, 2]);
// => [2, 1]
```

This example combines two arrays into a single array containing only unique values.

## Collection Methods

### forEach

Iterates over elements of `collection` and invokes `iteratee` for each element. The iteratee is invoked with three arguments: (value, index|key, collection). Iteratee functions may exit iteration early by explicitly returning `false`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `collection` | `Array` \| `Object` | The collection to iterate over. |
| `iteratee` | `Function` | The function invoked per iteration (default: `_.identity`). |

**Returns**

| Name | Type | Description |
|---|---|---|
| `collection` | `Array` \| `Object` | Returns `collection`. |

**Example**

```javascript
_.forEach([1, 2], function(value) {
  console.log(value);
});
// => Logs `1` then `2`.

_.forEach({ 'a': 1, 'b': 2 }, function(value, key) {
  console.log(key);
});
// => Logs 'a' then 'b' (iteration order is not guaranteed).
```

This example demonstrates iterating over an array and an object using `_.forEach`, logging values or keys respectively.

### map

Creates an array of values by running each element in `collection` thru `iteratee`. The iteratee is invoked with three arguments: (value, index|key, collection).

**Parameters**

| Name | Type | Description |
|---|---|---|
| `collection` | `Array` \| `Object` | The collection to iterate over. |
| `iteratee` | `Function` | The function invoked per iteration (default: `_.identity`). |

**Returns**

| Name | Type | Description |
|---|---|---|
| `Array` | `Array` | Returns the new mapped array. |

**Example**

```javascript
function square(n) {
  return n * n;
}

_.map([4, 8], square);
// => [16, 64]

_.map({ 'a': 4, 'b': 8 }, square);
// => [16, 64] (iteration order is not guaranteed)

var users = [
  { 'user': 'barney' },
  { 'user': 'fred' }
];

// The `_.property` iteratee shorthand.
_.map(users, 'user');
// => ['barney', 'fred']
```

This example transforms elements of an array and an object using `_.map`, applying a `square` function or extracting a property.

### filter

Iterates over elements of `collection`, returning an array of all elements `predicate` returns truthy for. The predicate is invoked with three arguments: (value, index|key, collection).

**Parameters**

| Name | Type | Description |
|---|---|---|
| `collection` | `Array` \| `Object` | The collection to iterate over. |
| `predicate` | `Function` | The function invoked per iteration (default: `_.identity`). |

**Returns**

| Name | Type | Description |
|---|---|---|
| `Array` | `Array` | Returns the new filtered array. |

**Example**

```javascript
var users = [
  { 'user': 'barney', 'age': 36, 'active': true },
  { 'user': 'fred',   'age': 40, 'active': false }
];

_.filter(users, function(o) { return !o.active; });
// => objects for ['fred']

// The `_.matches` iteratee shorthand.
_.filter(users, { 'age': 36, 'active': true });
// => objects for ['barney']

// The `_.matchesProperty` iteratee shorthand.
_.filter(users, ['active', false]);
// => objects for ['fred']

// The `_.property` iteratee shorthand.
_.filter(users, 'active');
// => objects for ['barney']
```

This example demonstrates filtering a collection of user objects based on different predicates, including function, object match, property match, and property existence.

### reduce

Reduces `collection` to a value which is the accumulated result of running each element in `collection` thru `iteratee`, where each successive invocation is supplied the return value of the previous. If `accumulator` is not given, the first element of `collection` is used as the initial value. The iteratee is invoked with four arguments: (accumulator, value, index|key, collection).

**Parameters**

| Name | Type | Description |
|---|---|---|
| `collection` | `Array` \| `Object` | The collection to iterate over. |
| `iteratee` | `Function` | The function invoked per iteration (default: `_.identity`). |
| `accumulator` | `*` | The initial value. |

**Returns**

| Name | Type | Description |
|---|---|---|
| `*` | `*` | Returns the accumulated value. |

**Example**

```javascript
_.reduce([1, 2], function(sum, n) {
  return sum + n;
}, 0);
// => 3

_.reduce({ 'a': 1, 'b': 2, 'c': 1 }, function(result, value, key) {
  (result[value] || (result[value] = [])).push(key);
  return result;
}, {});
// => { '1': ['a', 'c'], '2': ['b'] } (iteration order is not guaranteed)
```

This example shows `_.reduce` summing numbers in an array and grouping keys by value in an object.

## Function Methods

### debounce

Creates a debounced function that delays invoking `func` until after `wait` milliseconds have elapsed since the last time the debounced function was invoked. The debounced function comes with a `cancel` method to cancel delayed `func` invocations and a `flush` method to immediately invoke them.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `func` | `Function` | The function to debounce. |
| `wait` | `number` | The number of milliseconds to delay (default: 0). |
| `options` | `Object` | The options object. |
| `options.leading` | `boolean` | Specify invoking on the leading edge of the timeout (default: `false`). |
| `options.maxWait` | `number` | The maximum time `func` is allowed to be delayed before it's invoked. |
| `options.trailing` | `boolean` | Specify invoking on the trailing edge of the timeout (default: `true`). |

**Returns**

| Name | Type | Description |
|---|---|---|
| `Function` | `Function` | Returns the new debounced function. |

**Example**

```javascript
// Avoid costly calculations while the window size is in flux.
// jQuery(window).on('resize', _.debounce(calculateLayout, 150));

// Invoke `sendMail` when clicked, debouncing subsequent calls.
// jQuery(element).on('click', _.debounce(sendMail, 300, {
//   'leading': true,
//   'trailing': false
// }));

// Ensure `batchLog` is invoked once after 1 second of debounced calls.
// var debounced = _.debounce(batchLog, 250, { 'maxWait': 1000 });
// var source = new EventSource('/stream');
// jQuery(source).on('message', debounced);

// Cancel the trailing debounced invocation.
// jQuery(window).on('popstate', debounced.cancel);
```

This example (commented out as it often relies on external libraries like jQuery) illustrates how `_.debounce` can prevent a function from being called too frequently, such as on window resize events or rapid clicks.

### throttle

Creates a throttled function that only invokes `func` at most once per every `wait` milliseconds. The throttled function comes with a `cancel` method to cancel delayed `func` invocations and a `flush` method to immediately invoke them.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `func` | `Function` | The function to throttle. |
| `wait` | `number` | The number of milliseconds to throttle invocations to (default: 0). |
| `options` | `Object` | The options object. |
| `options.leading` | `boolean` | Specify invoking on the leading edge of the timeout (default: `true`). |
| `options.trailing` | `boolean` | Specify invoking on the trailing edge of the timeout (default: `true`). |

**Returns**

| Name | Type | Description |
|---|---|---|
| `Function` | `Function` | Returns the new throttled function. |

**Example**

```javascript
// Avoid excessively updating the position while scrolling.
// jQuery(window).on('scroll', _.throttle(updatePosition, 100));

// Invoke `renewToken` when the click event is fired, but not more than once every 5 minutes.
// var throttled = _.throttle(renewToken, 300000, { 'trailing': false });
// jQuery(element).on('click', throttled);

// Cancel the trailing throttled invocation.
// jQuery(window).on('popstate', throttled.cancel);
```

Similar to `debounce`, this example (commented out) shows how `_.throttle` can limit the rate at which a function is called, useful for scroll events or API calls that shouldn't happen too often.

### memoize

Creates a function that memoizes the result of `func`. If `resolver` is provided, it determines the cache key for storing the result based on the arguments provided to the memoized function. By default, the first argument provided to the memoized function is used as the map cache key.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `func` | `Function` | The function to have its output memoized. |
| `resolver` | `Function` | The function to resolve the cache key. |

**Returns**

| Name | Type | Description |
|---|---|---|
| `Function` | `Function` | Returns the new memoized function. |

**Example**

```javascript
var object = { 'a': 1, 'b': 2 };
var other = { 'c': 3, 'd': 4 };

var values = _.memoize(_.values);
values(object);
// => [1, 2]

values(other);
// => [3, 4]

object.a = 2;
values(object);
// => [1, 2]

// Modify the result cache.
values.cache.set(object, ['a', 'b']);
values(object);
// => ['a', 'b']

// Replace `_.memoize.Cache`.
// _.memoize.Cache = WeakMap;
```

This example illustrates `_.memoize` caching the results of `_.values` for objects, showing how subsequent calls with the same object return the cached result until the cache is manually modified or replaced.

## Lang Methods

### isObject

Checks if `value` is the language type of `Object`. (e.g. arrays, functions, objects, regexes, `new Number(0)`, and `new String('')`)

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to check. |

**Returns**

| Name | Type | Description |
|---|---|---|
| `boolean` | `boolean` | Returns `true` if `value` is an object, else `false`. |

**Example**

```javascript
_.isObject({});
// => true

_.isObject([1, 2, 3]);
// => true

_.isObject(_.noop);
// => true

_.isObject(null);
// => false
```

This example demonstrates how `_.isObject` identifies various JavaScript object types.

### isEqual

Performs a `SameValueZero` comparison between two values to determine if they are equivalent. This method supports comparing arrays, array buffers, booleans, date objects, error objects, maps, numbers, `Object` objects, regexes, sets, strings, symbols, and typed arrays. `Object` objects are compared by their own, not inherited, enumerable properties. Functions and DOM nodes are compared by strict equality, i.e. `===`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to compare. |
| `other` | `*` | The other value to compare. |

**Returns**

| Name | Type | Description |
|---|---|---|
| `boolean` | `boolean` | Returns `true` if the values are equivalent, else `false`. |

**Example**

```javascript
var object = { 'a': 1 };
var other = { 'a': 1 };

_.isEqual(object, other);
// => true

object === other;
// => false
```

This example shows that `_.isEqual` performs a deep comparison, returning `true` for structurally equivalent objects that are not strictly equal.

### cloneDeep

Recursively clones `value`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to recursively clone. |

**Returns**

| Name | Type | Description |
|---|---|---|
| `*` | `*` | Returns the deep cloned value. |

**Example**

```javascript
var objects = [{ 'a': 1 }, { 'b': 2 }];

var deep = _.cloneDeep(objects);
console.log(deep[0] === objects[0]);
// => false
```

This example demonstrates `_.cloneDeep` creating a new array and new objects within it, ensuring no shared references with the original.

## Object Methods

### get

Gets the value at `path` of `object`. If the resolved value is `undefined`, the `defaultValue` is returned in its place.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | The object to query. |
| `path` | `Array` \| `string` | The path of the property to get. |
| `defaultValue` | `*` | The value returned for `undefined` resolved values. |

**Returns**

| Name | Type | Description |
|---|---|---|
| `*` | `*` | Returns the resolved value. |

**Example**

```javascript
var object = { 'a': [{ 'b': { 'c': 3 } }] };

_.get(object, 'a[0].b.c');
// => 3

_.get(object, ['a', '0', 'b', 'c']);
// => 3

_.get(object, 'a.b.c', 'default');
// => 'default'
```

This example shows how to safely access nested properties in an object using `_.get`, with support for array indexing and a default value for missing paths.

### set

Sets the value at `path` of `object`. If a portion of `path` doesn't exist, it's created. Arrays are created for missing index properties while objects are created for all other missing properties.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | The object to modify. |
| `path` | `Array` \| `string` | The path of the property to set. |
| `value` | `*` | The value to set. |

**Returns**

| Name | Type | Description |
|---|---|---|
| `Object` | `Object` | Returns `object`. |

**Example**

```javascript
var object = { 'a': [{ 'b': { 'c': 3 } }] };

_.set(object, 'a[0].b.c', 4);
console.log(object.a[0].b.c);
// => 4

_.set(object, ['x', '0', 'y', 'z'], 5);
console.log(object.x[0].y.z);
// => 5
```

This example illustrates `_.set`'s ability to create nested paths and set values within an object.

### merge

Recursively merges own and inherited enumerable string keyed properties of source objects into the destination object. Source properties that resolve to `undefined` are skipped if a destination value exists. Array and plain object properties are merged recursively. Other objects and value types are overridden by assignment.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | The destination object. |
| `sources` | `Object` | The source objects. |

**Returns**

| Name | Type | Description |
|---|---|---|
| `Object` | `Object` | Returns `object`. |

**Example**

```javascript
var object = {
  'a': [{ 'b': 2 }, { 'd': 4 }]
};

var other = {
  'a': [{ 'c': 3 }, { 'e': 5 }]
};

_.merge(object, other);
// => { 'a': [{ 'b': 2, 'c': 3 }, { 'd': 4, 'e': 5 }] }
```

This example demonstrates how `_.merge` combines objects and arrays recursively.

## String Methods

### camelCase

Converts `string` to [camel case](https://en.wikipedia.org/wiki/CamelCase).

**Parameters**

| Name | Type | Description |
|---|---|---|
| `string` | `string` | The string to convert (default: `''`). |

**Returns**

| Name | Type | Description |
|---|---|---|
| `string` | `string` | Returns the camel cased string. |

**Example**

```javascript
_.camelCase('Foo Bar');
// => 'fooBar'

_.camelCase('--foo-bar--');
// => 'fooBar'

_.camelCase('__FOO_BAR__');
// => 'fooBar'
```

This example shows `_.camelCase` converting various string formats into camel case.

### trim

Removes leading and trailing whitespace or specified characters from `string`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `string` | `string` | The string to trim (default: `''`). |
| `chars` | `string` | The characters to trim (default: whitespace). |
| `guard` | `Object` | Enables use as an iteratee for methods like `_.map`. |

**Returns**

| Name | Type | Description |
|---|---|---|
| `string` | `string` | Returns the trimmed string. |

**Example**

```javascript
_.trim('  abc  ');
// => 'abc'

_.trim('-_-abc-_-', '_-');
// => 'abc'

_.map(['  foo  ', '  bar  '], _.trim);
// => ['foo', 'bar']
```

This example demonstrates `_.trim` removing leading/trailing whitespace or custom characters from strings.

### words

Splits `string` into an array of its words.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `string` | `string` | The string to inspect (default: `''`). |
| `pattern` | `RegExp` \| `string` | The pattern to match words. |
| `guard` | `Object` | Enables use as an iteratee for methods like `_.map`. |

**Returns**

| Name | Type | Description |
|---|---|---|
| `Array` | `Array` | Returns the words of `string`. |

**Example**

```javascript
_.words('fred, barney, & pebbles');
// => ['fred', 'barney', 'pebbles']

_.words('fred, barney, & pebbles', /[^, ]+/g);
// => ['fred', 'barney', '&', 'pebbles']
```

This example shows `_.words` extracting words from a string, with optional pattern matching.

## Number Methods

### add

Adds two numbers.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `augend` | `number` | The first number in an addition. |
| `addend` | `number` | The second number in an addition. |

**Returns**

| Name | Type | Description |
|---|---|---|
| `number` | `number` | Returns the total. |

**Example**

```javascript
_.add(6, 4);
// => 10
```

This example performs a simple addition using `_.add`.

### random

Produces a random number between the inclusive `lower` and `upper` bounds. If only one argument is provided a number between `0` and the given number is returned. If `floating` is `true`, or either `lower` or `upper` are floats, a floating-point number is returned instead of an integer.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `lower` | `number` | The lower bound (default: 0). |
| `upper` | `number` | The upper bound (default: 1). |
| `floating` | `boolean` | Specify returning a floating-point number. |

**Returns**

| Name | Type | Description |
|---|---|---|
| `number` | `number` | Returns the random number. |

**Example**

```javascript
_.random(0, 5);
// => an integer between 0 and 5

_.random(5);
// => also an integer between 0 and 5

_.random(5, true);
// => a floating-point number between 0 and 5

_.random(1.2, 5.2);
// => a floating-point number between 1.2 and 5.2
```

This example generates random numbers within specified ranges, including floating-point numbers.

## Utility Methods

### identity

This method returns the first argument it receives.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | Any value. |

**Returns**

| Name | Type | Description |
|---|---|---|
| `*` | `*` | Returns `value`. |

**Example**

```javascript
var object = { 'a': 1 };

console.log(_.identity(object) === object);
// => true
```

This example shows `_.identity` returning the exact value it was given.

### uniqueId

Generates a unique ID. If `prefix` is given, the ID is appended to it.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `prefix` | `string` | The value to prefix the ID with (default: `''`). |

**Returns**

| Name | Type | Description |
|---|---|---|
| `string` | `string` | Returns the unique ID. |

**Example**

```javascript
_.uniqueId('contact_');
// => 'contact_104'

_.uniqueId();
// => '105'
```

This example generates unique IDs, with and without a custom prefix.

---

This API Reference provides a detailed look into some of Lodash's most commonly used methods across various categories. By understanding these methods, you can write more concise, readable, and performant JavaScript code. Continue your exploration by learning how to contribute to the Lodash project in the [Contributing](./contributing.md) section.