# Function

Lodash provides a powerful suite of utilities for manipulating functions. These helpers allow you to control invocation frequency, alter function signatures, and compose complex behaviors from simpler pieces. Common use cases include delaying or limiting function calls with `debounce` and `throttle`, creating reusable, partially applied functions with `partial` and `curry`, and managing function execution flow with `after` and `before`.

These tools are fundamental to writing clean, efficient, and functional JavaScript. For a deeper dive into these concepts, check out our [Functional Programming Guide](./fp-guide.md).

---

## after

Creates a function that invokes `func` once it's called `n` or more times.

### Parameters

<x-field data-name="n" data-type="number" data-required="true" data-desc="The number of calls before func is invoked."></x-field>
<x-field data-name="func" data-type="Function" data-required="true" data-desc="The function to restrict."></x-field>

### Returns

<x-field data-name="restricted" data-type="Function" data-desc="Returns the new restricted function."></x-field>

### Example

```javascript icon=logos:javascript
var saves = ['profile', 'settings'];
 
var done = _.after(saves.length, function() {
  console.log('done saving!');
});
 
_.forEach(saves, function(type) {
  asyncSave({ 'type': type, 'complete': done });
});
// => Logs 'done saving!' after the two async saves have completed.
```

---

## ary

Creates a function that invokes `func`, with up to `n` arguments, ignoring any additional arguments.

### Parameters

<x-field data-name="func" data-type="Function" data-required="true" data-desc="The function to cap arguments for."></x-field>
<x-field data-name="n" data-type="number" data-default="func.length" data-required="false" data-desc="The arity cap."></x-field>

### Returns

<x-field data-name="capped" data-type="Function" data-desc="Returns the new capped function."></x-field>

### Example

```javascript icon=logos:javascript
_.map(['6', '8', '10'], _.ary(parseInt, 1));
// => [6, 8, 10]
```

---

## before

Creates a function that invokes `func`, with the `this` binding and arguments of the created function, while it's called less than `n` times. Subsequent calls to the created function return the result of the last `func` invocation.

### Parameters

<x-field data-name="n" data-type="number" data-required="true" data-desc="The number of calls at which func is no longer invoked."></x-field>
<x-field data-name="func" data-type="Function" data-required="true" data-desc="The function to restrict."></x-field>

### Returns

<x-field data-name="restricted" data-type="Function" data-desc="Returns the new restricted function."></x-field>

### Example

```javascript icon=logos:javascript
jQuery(element).on('click', _.before(5, addContactToList));
// => Allows adding up to 4 contacts to the list.
```

---

## bind

Creates a function that invokes `func` with the `this` binding of `thisArg` and `partials` prepended to the arguments it receives. The `_.bind.placeholder` value (`_`) may be used as a placeholder for partially applied arguments.

### Parameters

<x-field data-name="func" data-type="Function" data-required="true" data-desc="The function to bind."></x-field>
<x-field data-name="thisArg" data-type="any" data-required="true" data-desc="The 'this' binding of func."></x-field>
<x-field data-name="partials" data-type="...any" data-required="false" data-desc="The arguments to be partially applied."></x-field>

### Returns

<x-field data-name="bound" data-type="Function" data-desc="Returns the new bound function."></x-field>

### Example

```javascript icon=logos:javascript
function greet(greeting, punctuation) {
  return greeting + ' ' + this.user + punctuation;
}

var object = { 'user': 'fred' };

var bound = _.bind(greet, object, 'hi');
bound('!');
// => 'hi fred!'

// Bound with placeholders.
var bound = _.bind(greet, object, _, '!');
bound('hi');
// => 'hi fred!'
```

---

## bindKey

Creates a function that invokes the method at `object[key]` with `partials` prepended to its arguments. This method allows bound functions to reference methods that may be redefined later.

### Parameters

<x-field data-name="object" data-type="Object" data-required="true" data-desc="The object to invoke the method on."></x-field>
<x-field data-name="key" data-type="string" data-required="true" data-desc="The key of the method."></x-field>
<x-field data-name="partials" data-type="...any" data-required="false" data-desc="The arguments to be partially applied."></x-field>

### Returns

<x-field data-name="bound" data-type="Function" data-desc="Returns the new bound function."></x-field>

### Example

```javascript icon=logos:javascript
var object = {
  'user': 'fred',
  'greet': function(greeting, punctuation) {
    return greeting + ' ' + this.user + punctuation;
  }
};

var bound = _.bindKey(object, 'greet', 'hi');
bound('!');
// => 'hi fred!'

object.greet = function(greeting, punctuation) {
  return greeting + 'ya ' + this.user + punctuation;
};

bound('!');
// => 'hiya fred!'
```

---

## curry

Creates a function that accepts arguments of `func` and either invokes `func` returning its result, if at least `arity` arguments have been provided, or returns a function that accepts the remaining arguments.

### Parameters

<x-field data-name="func" data-type="Function" data-required="true" data-desc="The function to curry."></x-field>
<x-field data-name="arity" data-type="number" data-default="func.length" data-required="false" data-desc="The arity of func."></x-field>

### Returns

<x-field data-name="curried" data-type="Function" data-desc="Returns the new curried function."></x-field>

### Example

```javascript icon=logos:javascript
var abc = function(a, b, c) {
  return [a, b, c];
};

var curried = _.curry(abc);

curried(1)(2)(3);
// => [1, 2, 3]

curried(1, 2)(3);
// => [1, 2, 3]

// Curried with placeholders.
curried(1)(_, 3)(2);
// => [1, 2, 3]
```

---

## debounce

Creates a debounced function that delays invoking `func` until after `wait` milliseconds have passed since the last time the debounced function was invoked.

### Parameters

<x-field data-name="func" data-type="Function" data-required="true" data-desc="The function to debounce."></x-field>
<x-field data-name="wait" data-type="number" data-default="0" data-required="false" data-desc="The number of milliseconds to delay."></x-field>
<x-field data-name="options" data-type="Object" data-required="false" data-desc="The options object.">
  <x-field data-name="leading" data-type="boolean" data-default="false" data-required="false" data-desc="Specify invoking on the leading edge of the timeout."></x-field>
  <x-field data-name="maxWait" data-type="number" data-required="false" data-desc="The maximum time func is allowed to be delayed before it's invoked."></x-field>
  <x-field data-name="trailing" data-type="boolean" data-default="true" data-required="false" data-desc="Specify invoking on the trailing edge of the timeout."></x-field>
</x-field>

### Returns

<x-field data-name="debounced" data-type="Function" data-desc="Returns the new debounced function, which has 'cancel' and 'flush' methods."></x-field>

### Example

```javascript icon=logos:javascript
// Avoid costly calculations while the window size is in flux.
jQuery(window).on('resize', _.debounce(calculateLayout, 150));

// Cancel the trailing debounced invocation.
jQuery(window).on('popstate', debounced.cancel);
```

---

## defer

Defers invoking the `func` until the current call stack has cleared, similar to `setTimeout` with a timeout of 0.

### Parameters

<x-field data-name="func" data-type="Function" data-required="true" data-desc="The function to defer."></x-field>
<x-field data-name="args" data-type="...any" data-required="false" data-desc="The arguments to invoke func with."></x-field>

### Returns

<x-field data-name="timerId" data-type="number" data-desc="Returns the timer id."></x-field>

### Example

```javascript icon=logos:javascript
_.defer(function(text) {
  console.log(text);
}, 'deferred');
// => Logs 'deferred' after one millisecond.
```

---

## delay

Invokes `func` after `wait` milliseconds. Any additional arguments are provided to `func` when it's invoked.

### Parameters

<x-field data-name="func" data-type="Function" data-required="true" data-desc="The function to delay."></x-field>
<x-field data-name="wait" data-type="number" data-required="true" data-desc="The number of milliseconds to delay invocation."></x-field>
<x-field data-name="args" data-type="...any" data-required="false" data-desc="The arguments to invoke func with."></x-field>

### Returns

<x-field data-name="timerId" data-type="number" data-desc="Returns the timer id."></x-field>

### Example

```javascript icon=logos:javascript
_.delay(function(text) {
  console.log(text);
}, 1000, 'later');
// => Logs 'later' after one second.
```

---

## flip

Creates a function that invokes `func` with arguments reversed.

### Parameters

<x-field data-name="func" data-type="Function" data-required="true" data-desc="The function to flip arguments for."></x-field>

### Returns

<x-field data-name="flipped" data-type="Function" data-desc="Returns the new flipped function."></x-field>

### Example

```javascript icon=logos:javascript
var flipped = _.flip(function() {
  return _.toArray(arguments);
});

flipped('a', 'b', 'c', 'd');
// => ['d', 'c', 'b', 'a']
```

---

## memoize

Creates a function that memoizes the result of `func`. The cache is exposed as the `cache` property on the memoized function.

### Parameters

<x-field data-name="func" data-type="Function" data-required="true" data-desc="The function to have its output memoized."></x-field>
<x-field data-name="resolver" data-type="Function" data-required="false" data-desc="The function to resolve the cache key. By default, the first argument is used."></x-field>

### Returns

<x-field data-name="memoized" data-type="Function" data-desc="Returns the new memoized function."></x-field>

### Example

```javascript icon=logos:javascript
var object = { 'a': 1, 'b': 2 };
var other = { 'c': 3, 'd': 4 };

var values = _.memoize(_.values);
values(object);
// => [1, 2]

values(other);
// => [3, 4]

object.a = 2;
values(object);
// => [1, 2] (returns cached value)

// Modify the result cache.
values.cache.set(object, ['a', 'b']);
values(object);
// => ['a', 'b']
```

---

## negate

Creates a function that negates the result of the predicate `func`.

### Parameters

<x-field data-name="predicate" data-type="Function" data-required="true" data-desc="The predicate to negate."></x-field>

### Returns

<x-field data-name="negated" data-type="Function" data-desc="Returns the new negated function."></x-field>

### Example

```javascript icon=logos:javascript
function isEven(n) {
  return n % 2 == 0;
}

_.filter([1, 2, 3, 4, 5, 6], _.negate(isEven));
// => [1, 3, 5]
```

---

## once

Creates a function that is restricted to invoking `func` once. Repeat calls return the value of the first invocation.

### Parameters

<x-field data-name="func" data-type="Function" data-required="true" data-desc="The function to restrict."></x-field>

### Returns

<x-field data-name="restricted" data-type="Function" data-desc="Returns the new restricted function."></x-field>

### Example

```javascript icon=logos:javascript
var initialize = _.once(createApplication);
initialize();
initialize();
// => `createApplication` is invoked only once.
```

---

## partial

Creates a function that invokes `func` with `partials` prepended to the arguments it receives. This method is like `_.bind` but does not alter the `this` binding.

### Parameters

<x-field data-name="func" data-type="Function" data-required="true" data-desc="The function to partially apply arguments to."></x-field>
<x-field data-name="partials" data-type="...any" data-required="false" data-desc="The arguments to be partially applied."></x-field>

### Returns

<x-field data-name="partialized" data-type="Function" data-desc="Returns the new partially applied function."></x-field>

### Example

```javascript icon=logos:javascript
function greet(greeting, name) {
  return greeting + ' ' + name;
}

var sayHelloTo = _.partial(greet, 'hello');
sayHelloTo('fred');
// => 'hello fred'

// Partially applied with placeholders.
var greetFred = _.partial(greet, _, 'fred');
greetFred('hi');
// => 'hi fred'
```

---

## throttle

Creates a throttled function that only invokes `func` at most once per every `wait` milliseconds.

### Parameters

<x-field data-name="func" data-type="Function" data-required="true" data-desc="The function to throttle."></x-field>
<x-field data-name="wait" data-type="number" data-default="0" data-required="false" data-desc="The number of milliseconds to throttle invocations to."></x-field>
<x-field data-name="options" data-type="Object" data-required="false" data-desc="The options object.">
  <x-field data-name="leading" data-type="boolean" data-default="true" data-required="false" data-desc="Specify invoking on the leading edge of the timeout."></x-field>
  <x-field data-name="trailing" data-type="boolean" data-default="true" data-required="false" data-desc="Specify invoking on the trailing edge of the timeout."></x-field>
</x-field>

### Returns

<x-field data-name="throttled" data-type="Function" data-desc="Returns the new throttled function, which has 'cancel' and 'flush' methods."></x-field>

### Example

```javascript icon=logos:javascript
// Avoid excessively updating the position while scrolling.
jQuery(window).on('scroll', _.throttle(updatePosition, 100));

// Cancel the trailing throttled invocation.
jQuery(window).on('popstate', throttled.cancel);
```

---

## wrap

Creates a function that provides `value` to `wrapper` as its first argument. Any additional arguments are appended to those provided to the `wrapper`.

### Parameters

<x-field data-name="value" data-type="any" data-required="true" data-desc="The value to wrap."></x-field>
<x-field data-name="wrapper" data-type="Function" data-default="identity" data-required="false" data-desc="The wrapper function."></x-field>

### Returns

<x-field data-name="wrapped" data-type="Function" data-desc="Returns the new function."></x-field>

### Example

```javascript icon=logos:javascript
var p = _.wrap(_.escape, function(func, text) {
  return '<p>' + func(text) + '</p>';
});

p('fred, barney, & pebbles');
// => '<p>fred, barney, &amp; pebbles</p>'
```

---

This section has covered Lodash's core function utilities. To explore other utility types, continue to the [Lang](./api-lang.md) section for type-checking and cloning functions.