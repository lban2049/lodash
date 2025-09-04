# Function

Lodash provides a suite of powerful higher-order functions that operate on or return other functions. These utilities are essential for functional programming paradigms, allowing you to manipulate function behavior in sophisticated ways, such as controlling invocation frequency, altering argument signatures, and managing `this` context.

Key capabilities include:

*   **Invocation Control**: Functions like `debounce`, `throttle`, `once`, `before`, and `after` give you fine-grained control over when and how many times a function is executed.
*   **Argument Manipulation**: Utilities such as `curry`, `partial`, `flip`, `rearg`, and `spread` allow for flexible function composition and argument transformation.
*   **Context Binding**: `bind` and `bindKey` provide robust mechanisms for setting the `this` context of a function.
*   **Memoization**: `memoize` caches the results of expensive function calls to improve performance.

These tools help create more reusable, modular, and declarative code. For type-checking functions, see the `isFunction` method in the [Lang](./api-lang.md) documentation.

---

## after

Creates a function that invokes `func` once it's called `n` or more times.

### Parameters

| Name | Type | Description |
|---|---|---|
| `n` | `number` | The number of calls before `func` is invoked. |
| `func` | `Function` | The function to restrict. |

### Returns

- `(Function)`: Returns the new restricted function.

### Example

```javascript
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

| Name | Type | Description |
|---|---|---|
| `func` | `Function` | The function to cap arguments for. |
| `n` | `number` | (Optional) The arity cap. Defaults to `func.length`. |

### Returns

- `(Function)`: Returns the new capped function.

### Example

```javascript
_.map(['6', '8', '10'], _.ary(parseInt, 1));
// => [6, 8, 10]
```

---

## before

Creates a function that invokes `func`, with the `this` binding and arguments of the created function, while it's called less than `n` times. Subsequent calls to the created function return the result of the last `func` invocation.

### Parameters

| Name | Type | Description |
|---|---|---|
| `n` | `number` | The number of calls at which `func` is no longer invoked. |
| `func` | `Function` | The function to restrict. |

### Returns

- `(Function)`: Returns the new restricted function.

### Example

```javascript
// Assuming jQuery is available
// jQuery(element).on('click', _.before(5, addContactToList));
// => Allows adding up to 4 contacts to the list.
```

---

## bind

Creates a function that invokes `func` with the `this` binding of `thisArg` and `partials` prepended to the arguments it receives. The `_.bind.placeholder` value (`_`) may be used as a placeholder for partially applied arguments.

### Parameters

| Name | Type | Description |
|---|---|---|
| `func` | `Function` | The function to bind. |
| `thisArg` | `*` | The `this` binding of `func`. |
| `...partials` | `*` | (Optional) The arguments to be partially applied. |

### Returns

- `(Function)`: Returns the new bound function.

### Example

```javascript
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

Creates a function that invokes the method at `object[key]` with `partials` prepended to the arguments it receives. This method allows bound functions to reference methods that may be redefined or don't yet exist.

### Parameters

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | The object to invoke the method on. |
| `key` | `string` | The key of the method. |
| `...partials` | `*` | (Optional) The arguments to be partially applied. |

### Returns

- `(Function)`: Returns the new bound function.

### Example

```javascript
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

Creates a function that accepts arguments of `func` and either invokes `func` returning its result, if at least `arity` number of arguments have been provided, or returns a function that accepts the remaining `func` arguments, and so on.

### Parameters

| Name | Type | Description |
|---|---|---|
| `func` | `Function` | The function to curry. |
| `arity` | `number` | (Optional) The arity of `func`. Defaults to `func.length`. |

### Returns

- `(Function)`: Returns the new curried function.

### Example

```javascript
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

## curryRight

This method is like `_.curry` except that arguments are applied to `func` from right to left.

### Parameters

| Name | Type | Description |
|---|---|---|
| `func` | `Function` | The function to curry. |
| `arity` | `number` | (Optional) The arity of `func`. Defaults to `func.length`. |

### Returns

- `(Function)`: Returns the new curried function.

### Example

```javascript
var abc = function(a, b, c) {
  return [a, b, c];
};

var curried = _.curryRight(abc);

curried(3)(2)(1);
// => [1, 2, 3]

curried(2, 3)(1);
// => [1, 2, 3]
```

---

## debounce

Creates a debounced function that delays invoking `func` until after `wait` milliseconds have elapsed since the last time the debounced function was invoked. The debounced function comes with a `cancel` method to cancel delayed `func` invocations and a `flush` method to immediately invoke them. Provide `options` to indicate whether `func` should be invoked on the leading and/or trailing edge of the `wait` timeout. The `func` is invoked with the last arguments provided to the debounced function.

### Parameters

| Name | Type | Description |
|---|---|---|
| `func` | `Function` | The function to debounce. |
| `wait` | `number` | (Optional) The number of milliseconds to delay. Defaults to 0. |
| `options` | `Object` | (Optional) The options object. |
| `options.leading` | `boolean` | (Optional) Specify invoking on the leading edge of the timeout. Defaults to `false`. |
| `options.maxWait` | `number` | (Optional) The maximum time `func` is allowed to be delayed before it's invoked. |
| `options.trailing` | `boolean` | (Optional) Specify invoking on the trailing edge of the timeout. Defaults to `true`. |

### Returns

- `(Function)`: Returns the new debounced function.

### Example

```javascript
// Assuming jQuery is available
// Avoid costly calculations while the window size is in flux.
// jQuery(window).on('resize', _.debounce(calculateLayout, 150));

// Invoke `sendMail` when clicked, debouncing subsequent calls.
// jQuery(element).on('click', _.debounce(sendMail, 300, {
//   'leading': true,
//   'trailing': false
// }));

// Cancel the trailing debounced invocation.
// jQuery(window).on('popstate', debounced.cancel);
```

---

## defer

Defers invoking the `func` until the current call stack has cleared. Any additional arguments are provided to `func` when it's invoked.

### Parameters

| Name | Type | Description |
|---|---|---|
| `func` | `Function` | The function to defer. |
| `...args` | `*` | (Optional) The arguments to invoke `func` with. |

### Returns

- `(number)`: Returns the timer id.

### Example

```javascript
_.defer(function(text) {
  console.log(text);
}, 'deferred');
// => Logs 'deferred' after one millisecond.
```

---

## delay

Invokes `func` after `wait` milliseconds. Any additional arguments are provided to `func` when it's invoked.

### Parameters

| Name | Type | Description |
|---|---|---|
| `func` | `Function` | The function to delay. |
| `wait` | `number` | The number of milliseconds to delay invocation. |
| `...args` | `*` | (Optional) The arguments to invoke `func` with. |

### Returns

- `(number)`: Returns the timer id.

### Example

```javascript
_.delay(function(text) {
  console.log(text);
}, 1000, 'later');
// => Logs 'later' after one second.
```

---

## flip

Creates a function that invokes `func` with arguments reversed.

### Parameters

| Name | Type | Description |
|---|---|---|
| `func` | `Function` | The function to flip arguments for. |

### Returns

- `(Function)`: Returns the new flipped function.

### Example

```javascript
var flipped = _.flip(function() {
  return _.toArray(arguments);
});

flipped('a', 'b', 'c', 'd');
// => ['d', 'c', 'b', 'a']
```

---

## memoize

Creates a function that memoizes the result of `func`. If `resolver` is provided, it determines the cache key for storing the result based on the arguments provided to the memoized function. By default, the first argument provided to the memoized function is used as the map cache key. The cache is exposed as the `cache` property on the memoized function.

### Parameters

| Name | Type | Description |
|---|---|---|
| `func` | `Function` | The function to have its output memoized. |
| `resolver` | `Function` | (Optional) The function to resolve the cache key. |

### Returns

- `(Function)`: Returns the new memoized function.

### Example

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
```

---

## negate

Creates a function that negates the result of the predicate `func`. The `func` predicate is invoked with the `this` binding and arguments of the created function.

### Parameters

| Name | Type | Description |
|---|---|---|
| `predicate` | `Function` | The predicate to negate. |

### Returns

- `(Function)`: Returns the new negated function.

### Example

```javascript
function isEven(n) {
  return n % 2 == 0;
}

_.filter([1, 2, 3, 4, 5, 6], _.negate(isEven));
// => [1, 3, 5]
```

---

## once

Creates a function that is restricted to invoking `func` once. Repeat calls to the function return the value of the first invocation. The `func` is invoked with the `this` binding and arguments of the created function.

### Parameters

| Name | Type | Description |
|---|---|---|
| `func` | `Function` | The function to restrict. |

### Returns

- `(Function)`: Returns the new restricted function.

### Example

```javascript
// var initialize = _.once(createApplication);
// initialize();
// initialize();
// => `createApplication` is invoked once
```

---

## overArgs

Creates a function that invokes `func` with its arguments transformed.

### Parameters

| Name | Type | Description |
|---|---|---|
| `func` | `Function` | The function to wrap. |
| `...transforms`| `(Function|Function[])` | (Optional) The argument transforms. Defaults to `_.identity`. |

### Returns

- `(Function)`: Returns the new function.

### Example

```javascript
function doubled(n) {
  return n * 2;
}

function square(n) {
  return n * n;
}

var func = _.overArgs(function(x, y) {
  return [x, y];
}, [square, doubled]);

func(9, 3);
// => [81, 6]

func(10, 5);
// => [100, 10]
```

---

## partial

Creates a function that invokes `func` with `partials` prepended to the arguments it receives. This method is like `_.bind` except it does not alter the `this` binding.

### Parameters

| Name | Type | Description |
|---|---|---|
| `func` | `Function` | The function to partially apply arguments to. |
| `...partials` | `*` | (Optional) The arguments to be partially applied. |

### Returns

- `(Function)`: Returns the new partially applied function.

### Example

```javascript
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

## partialRight

This method is like `_.partial` except that partially applied arguments are appended to the arguments it receives.

### Parameters

| Name | Type | Description |
|---|---|---|
| `func` | `Function` | The function to partially apply arguments to. |
| `...partials` | `*` | (Optional) The arguments to be partially applied. |

### Returns

- `(Function)`: Returns the new partially applied function.

### Example

```javascript
function greet(greeting, name) {
  return greeting + ' ' + name;
}

var greetFred = _.partialRight(greet, 'fred');
greetFred('hi');
// => 'hi fred'

// Partially applied with placeholders.
var sayHelloTo = _.partialRight(greet, 'hello', _);
sayHelloTo('fred');
// => 'hello fred'
```

---

## rearg

Creates a function that invokes `func` with arguments arranged according to the specified `indexes`.

### Parameters

| Name | Type | Description |
|---|---|---|
| `func` | `Function` | The function to rearrange arguments for. |
| `...indexes` | `(number|number[])` | The arranged argument indexes. |

### Returns

- `(Function)`: Returns the new function.

### Example

```javascript
var rearged = _.rearg(function(a, b, c) {
  return [a, b, c];
}, [2, 0, 1]);

rearged('b', 'c', 'a')
// => ['a', 'b', 'c']
```

---

## rest

Creates a function that invokes `func` with the `this` binding of the created function and arguments from `start` and beyond provided as an array.

### Parameters

| Name | Type | Description |
|---|---|---|
| `func` | `Function` | The function to apply a rest parameter to. |
| `start` | `number` | (Optional) The start position of the rest parameter. Defaults to `func.length - 1`. |

### Returns

- `(Function)`: Returns the new function.

### Example

```javascript
var say = _.rest(function(what, names) {
  return what + ' ' + _.initial(names).join(', ') +
    (_.size(names) > 1 ? ', & ' : '') + _.last(names);
});

say('hello', 'fred', 'barney', 'pebbles');
// => 'hello fred, barney, & pebbles'
```

---

## spread

Creates a function that invokes `func` with the `this` binding of the create function and an array of arguments much like `Function#apply`.

### Parameters

| Name | Type | Description |
|---|---|---|
| `func` | `Function` | The function to spread arguments over. |
| `start` | `number` | (Optional) The start position of the spread. Defaults to 0. |

### Returns

- `(Function)`: Returns the new function.

### Example

```javascript
var say = _.spread(function(who, what) {
  return who + ' says ' + what;
});

say(['fred', 'hello']);
// => 'fred says hello'
```

---

## throttle

Creates a throttled function that only invokes `func` at most once per every `wait` milliseconds. The throttled function comes with a `cancel` method to cancel delayed `func` invocations and a `flush` method to immediately invoke them.

### Parameters

| Name | Type | Description |
|---|---|---|
| `func` | `Function` | The function to throttle. |
| `wait` | `number` | (Optional) The number of milliseconds to throttle invocations to. Defaults to 0. |
| `options` | `Object` | (Optional) The options object. |
| `options.leading` | `boolean` | (Optional) Specify invoking on the leading edge of the timeout. Defaults to `true`. |
| `options.trailing` | `boolean` | (Optional) Specify invoking on the trailing edge of the timeout. Defaults to `true`. |

### Returns

- `(Function)`: Returns the new throttled function.

### Example

```javascript
// Assuming jQuery is available
// Avoid excessively updating the position while scrolling.
// jQuery(window).on('scroll', _.throttle(updatePosition, 100));

// Cancel the trailing throttled invocation.
// jQuery(window).on('popstate', throttled.cancel);
```

---

## unary

Creates a function that accepts up to one argument, ignoring any additional arguments.

### Parameters

| Name | Type | Description |
|---|---|---|
| `func` | `Function` | The function to cap arguments for. |

### Returns

- `(Function)`: Returns the new capped function.

### Example

```javascript
_.map(['6', '8', '10'], _.unary(parseInt));
// => [6, 8, 10]
```

---

## wrap

Creates a function that provides `value` to `wrapper` as its first argument. Any additional arguments provided to the function are appended to those provided to the `wrapper`. The wrapper is invoked with the `this` binding of the created function.

### Parameters

| Name | Type | Description |
|---|---|---|
| `value` | `*` | The value to wrap. |
| `wrapper` | `Function` | (Optional) The wrapper function. Defaults to `identity`. |

### Returns

- `(Function)`: Returns the new function.

### Example

```javascript
var p = _.wrap(_.escape, function(func, text) {
  return '<p>' + func(text) + '</p>';
});

p('fred, barney, & pebbles');
// => '<p>fred, barney, &amp; pebbles</p>'
```

---

This concludes the reference for Function utilities. To explore other utility types, you might want to look at the [Util](./api-util.md) section next.