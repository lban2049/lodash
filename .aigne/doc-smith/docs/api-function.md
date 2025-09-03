# Function

Lodash provides a suite of powerful higher-order functions to manipulate and enhance other functions. These utilities allow for sophisticated patterns like debouncing user input, throttling frequent events, creating curried functions for partial application, and managing execution flow. They are essential tools for handling asynchronous operations and writing in a more functional style.

For other utilities, see the [Util API documentation](./api-util.md).

## Function Reference

| Function | Description |
| --- | --- |
| `_.after(n, func)` | Creates a function that invokes `func` only after it's called `n` or more times. |
| `_.ary(func, n)` | Creates a function that invokes `func` with up to `n` arguments, ignoring any extras. |
| `_.before(n, func)` | Creates a function that invokes `func` while it's called less than `n` times. |
| `_.bind(func, thisArg, [partials])` | Creates a function that invokes `func` with a bound `this` context and partial arguments. |
| `_.bindKey(object, key, [partials])` | Binds a method of an object to the object itself, allowing for redefinition. |
| `_.curry(func, [arity])` | Creates a function that accepts arguments of `func` and returns a new function until all arguments are supplied. |
| `_.curryRight(func, [arity])` | Like `_.curry`, but arguments are applied from right to left. |
| `_.debounce(func, [wait], [options])` | Creates a debounced function that delays invocation until after a specified wait time. |
| `_.defer(func, [args])` | Defers invoking `func` until the current call stack has cleared. |
| `_.delay(func, wait, [args])` | Invokes `func` after a specified `wait` period. |
| `_.flip(func)` | Creates a function that invokes `func` with its arguments reversed. |
| `_.memoize(func, [resolver])` | Creates a function that memoizes the return value of `func`. |
| `_.negate(predicate)` | Creates a function that negates the result of the predicate `func`. |
| `_.once(func)` | Creates a function that is restricted to invoking `func` only once. |
| `_.overArgs(func, [transforms])` | Creates a function that invokes `func` with its arguments transformed by corresponding functions. |
| `_.partial(func, [partials])` | Creates a function with prepended partial arguments. |
| `_.partialRight(func, [partials])` | Creates a function with appended partial arguments. |
| `_.rearg(func, indexes)` | Creates a function that invokes `func` with arguments rearranged according to `indexes`. |
| `_.rest(func, [start])` | Creates a function that accepts an array of arguments from a given start position. |
| `_.spread(func, [start])` | Creates a function that accepts an array of arguments and applies them to `func`. |
| `_.throttle(func, [wait], [options])` | Creates a throttled function that only invokes `func` at most once per `wait` milliseconds. |
| `_.unary(func)` | Creates a function that accepts only one argument, ignoring any additional ones. |
| `_.wrap(value, wrapper)` | Creates a function that provides `value` as the first argument to `wrapper`. |

---

### `_.after(n, func)`

Creates a function that invokes `func` once it's called `n` or more times.

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `n` | `number` | The number of calls before `func` is invoked. |
| `func` | `Function` | The function to restrict. |

**Returns**

- `(Function)`: Returns the new restricted function.

**Example**

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

### `_.ary(func, n)`

Creates a function that invokes `func`, with up to `n` arguments, ignoring any additional arguments.

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `func` | `Function` | The function to cap arguments for. |
| `[n=func.length]` | `number` | The arity cap. |

**Returns**

- `(Function)`: Returns the new capped function.

**Example**

```javascript
_.map(['6', '8', '10'], _.ary(parseInt, 1));
// => [6, 8, 10]
```

### `_.before(n, func)`

Creates a function that invokes `func` while it's called less than `n` times. Subsequent calls to the created function return the result of the last `func` invocation.

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `n` | `number` | The number of calls at which `func` is no longer invoked. |
| `func` | `Function` | The function to restrict. |

**Returns**

- `(Function)`: Returns the new restricted function.

**Example**

```javascript
jQuery(element).on('click', _.before(5, addContactToList));
// => Allows adding up to 4 contacts to the list.
```

### `_.bind(func, thisArg, [partials])`

Creates a function that invokes `func` with the `this` binding of `thisArg` and `partials` prepended to the arguments it receives. The `_.bind.placeholder` value (`_`) may be used as a placeholder for partially applied arguments.

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `func` | `Function` | The function to bind. |
| `thisArg` | `*` | The `this` binding of `func`. |
| `...[partials]` | `*` | The arguments to be partially applied. |

**Returns**

- `(Function)`: Returns the new bound function.

**Example**

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

### `_.debounce(func, [wait=0], [options={}])`

Creates a debounced function that delays invoking `func` until after `wait` milliseconds have elapsed since the last time the debounced function was invoked. The debounced function provides `cancel` and `flush` methods.

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `func` | `Function` | The function to debounce. |
| `[wait=0]` | `number` | The number of milliseconds to delay. |
| `[options={}]` | `Object` | The options object. |
| `[options.leading=false]` | `boolean` | Specify invoking on the leading edge of the timeout. |
| `[options.maxWait]` | `number` | The maximum time `func` is allowed to be delayed before it's invoked. |
| `[options.trailing=true]` | `boolean` | Specify invoking on the trailing edge of the timeout. |

**Returns**

- `(Function)`: Returns the new debounced function.

**Example**

```javascript
// Avoid costly calculations while the window size is in flux.
jQuery(window).on('resize', _.debounce(calculateLayout, 150));

// Ensure `batchLog` is invoked once after 1 second of debounced calls.
var debounced = _.debounce(batchLog, 250, { 'maxWait': 1000 });

// Cancel the trailing debounced invocation.
jQuery(window).on('popstate', debounced.cancel);
```

### `_.memoize(func, [resolver])`

Creates a function that memoizes the result of `func`. If `resolver` is provided, it determines the cache key for storing the result based on the arguments. By default, the first argument is used as the cache key.

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `func` | `Function` | The function to have its output memoized. |
| `[resolver]` | `Function` | The function to resolve the cache key. |

**Returns**

- `(Function)`: Returns the new memoized function.

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
// => [1, 2] (returns cached value)

// Modify the result cache.
values.cache.set(object, ['a', 'b']);
values(object);
// => ['a', 'b']
```

### `_.throttle(func, [wait=0], [options={}])`

Creates a throttled function that only invokes `func` at most once per every `wait` milliseconds. The throttled function provides `cancel` and `flush` methods.

**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `func` | `Function` | The function to throttle. |
| `[wait=0]` | `number` | The number of milliseconds to throttle invocations to. |
| `[options={}]` | `Object` | The options object. |
| `[options.leading=true]` | `boolean` | Specify invoking on the leading edge of the timeout. |
| `[options.trailing=true]` | `boolean` | Specify invoking on the trailing edge of the timeout. |

**Returns**

- `(Function)`: Returns the new throttled function.

**Example**

```javascript
// Avoid excessively updating the position while scrolling.
jQuery(window).on('scroll', _.throttle(updatePosition, 100));

// Invoke `renewToken` when the click event is fired, but not more than once every 5 minutes.
var throttled = _.throttle(renewToken, 300000, { 'trailing': false });
jQuery(element).on('click', throttled);

// Cancel the trailing throttled invocation.
jQuery(window).on('popstate', throttled.cancel);
```