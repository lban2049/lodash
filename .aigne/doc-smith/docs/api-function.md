# Function

Lodash provides a powerful suite of utilities for manipulating and working with functions. These helpers allow you to control invocation timing, alter function signatures, and compose complex logic from simpler pieces. Whether you need to limit the rate of function calls with `_.debounce` and `_.throttle`, create partially applied functions with `_.partial`, or build pipelines with `_.flow`, these utilities are essential tools for writing clean and efficient JavaScript.

This section provides a detailed reference for each function utility. For utilities that help with sequential method chaining, see the [Seq](./api-seq.md) documentation.

## Function Reference

| Function | Description |
|---|---|
| `_.after(n, func)` | Creates a function that invokes `func` once it's called `n` or more times. |
| `_.ary(func, [n=func.length])` | Creates a function that invokes `func`, with up to `n` arguments, ignoring any additional arguments. |
| `_.before(n, func)` | Creates a function that invokes `func`, with the `this` binding and arguments of the created function, while it's called less than `n` times. |
| `_.bind(func, thisArg, [partials])` | Creates a function that invokes `func` with the `this` binding of `thisArg` and `partials` prepended to the arguments it receives. |
| `_.bindKey(object, key, [partials])` | Creates a function that invokes the method at `object[key]` with `partials` prepended to the arguments it receives. |
| `_.curry(func, [arity=func.length])` | Creates a function that accepts arguments of `func` and either invokes `func` returning its result, if at least `arity` number of arguments have been provided, or returns a function that accepts the remaining `func` arguments. |
| `_.curryRight(func, [arity=func.length])` | Like `_.curry` except that arguments are applied to `func` in the manner of `_.partialRight`. |
| `_.debounce(func, [wait=0], [options={}])` | Creates a debounced function that delays invoking `func` until after `wait` milliseconds have elapsed since the last time the debounced function was invoked. |
| `_.defer(func, [args])` | Defers invoking the `func` until the current call stack has cleared. |
| `_.delay(func, wait, [args])` | Invokes `func` after `wait` milliseconds. |
| `_.flip(func)` | Creates a function that invokes `func` with arguments reversed. |
| `_.memoize(func, [resolver])` | Creates a function that memoizes the result of `func`. |
| `_.negate(predicate)` | Creates a function that negates the result of the predicate `func`. |
| `_.once(func)` | Creates a function that is restricted to invoking `func` once. |
| `_.overArgs(func, [transforms])` | Creates a function that invokes `func` with its arguments transformed. |
| `_.partial(func, [partials])` | Creates a function that invokes `func` with `partials` prepended to the arguments it receives. |
| `_.partialRight(func, [partials])` | Like `_.partial` except that partially applied arguments are appended to the arguments it receives. |
| `_.rearg(func, indexes)` | Creates a function that invokes `func` with arguments arranged according to the specified `indexes`. |
| `_.rest(func, [start=func.length-1])` | Creates a function that invokes `func` with the `this` binding of the created function and arguments from `start` and beyond provided as an array. |
| `_.spread(func, [start=0])` | Creates a function that invokes `func` with an array of arguments. |
| `_.throttle(func, [wait=0], [options={}])` | Creates a throttled function that only invokes `func` at most once per every `wait` milliseconds. |
| `_.unary(func)` | Creates a function that accepts up to one argument, ignoring any additional arguments. |
| `_.wrap(value, [wrapper=identity])` | Creates a function that provides `value` to `wrapper` as its first argument. |

---

### `_.after(n, func)`

Creates a function that invokes `func` once it's called `n` or more times.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `n` | `number` | The number of calls before `func` is invoked. |
| `func` | `Function` | The function to restrict. |

**Returns**

- `(Function)`: Returns the new restricted function.

**Example**

```javascript Trigger after multiple events icon=logos:javascript
var saves = ['profile', 'settings'];

var done = _.after(saves.length, function() {
  console.log('done saving!');
});

_.forEach(saves, function(type) {
  // Simulating async save
  setTimeout(done, 100);
});
// => Logs 'done saving!' after the two async saves have completed.
```

---

### `_.ary(func, [n=func.length])`

Creates a function that invokes `func` with up to `n` arguments, ignoring any additional arguments.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `func` | `Function` | The function to cap arguments for. |
| `[n=func.length]` | `number` | The arity cap. |

**Returns**

- `(Function)`: Returns the new capped function.

**Example**

```javascript Cap arguments for an iteratee icon=logos:javascript
_.map(['6', '8', '10'], _.ary(parseInt, 1));
// => [6, 8, 10]
```

---

### `_.before(n, func)`

Creates a function that invokes `func` while it's called less than `n` times. Subsequent calls to the created function return the result of the last `func` invocation.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `n` | `number` | The number of calls at which `func` is no longer invoked. |
| `func` | `Function` | The function to restrict. |

**Returns**

- `(Function)`: Returns the new restricted function.

**Example**

```javascript Limit event handler invocations icon=logos:javascript
// Assuming jQuery is available
// jQuery(element).on('click', _.before(5, addContactToList));
// => Allows adding up to 4 contacts to the list.
```

---

### `_.debounce(func, [wait=0], [options={}])`

Creates a debounced function that delays invoking `func` until after `wait` milliseconds have elapsed since the last time the debounced function was invoked. The debounced function comes with a `cancel` method to cancel delayed `func` invocations and a `flush` method to immediately invoke them.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `func` | `Function` | The function to debounce. |
| `[wait=0]` | `number` | The number of milliseconds to delay. |
| `[options={}]` | `Object` | The options object. |
| `[options.leading=false]` | `boolean` | Specify invoking on the leading edge of the timeout. |
| `[options.maxWait]` | `number` | The maximum time `func` is allowed to be delayed before it's invoked. |
| `[options.trailing=true]` | `boolean` | Specify invoking on the trailing edge of the timeout. |

**Returns**

- `(Function)`: Returns the new debounced function.

**Example**

```javascript Debounce a resize handler icon=logos:javascript
// Assuming jQuery is available
// Avoid costly calculations while the window size is in flux.
// jQuery(window).on('resize', _.debounce(calculateLayout, 150));
```

---

### `_.throttle(func, [wait=0], [options={}])`

Creates a throttled function that only invokes `func` at most once per every `wait` milliseconds. The throttled function comes with a `cancel` method to cancel delayed `func` invocations and a `flush` method to immediately invoke them.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `func` | `Function` | The function to throttle. |
| `[wait=0]` | `number` | The number of milliseconds to throttle invocations to. |
| `[options={}]` | `Object` | The options object. |
| `[options.leading=true]` | `boolean` | Specify invoking on the leading edge of the timeout. |
| `[options.trailing=true]` | `boolean` | Specify invoking on the trailing edge of the timeout. |

**Returns**

- `(Function)`: Returns the new throttled function.

**Example**

```javascript Throttle a scroll handler icon=logos:javascript
// Assuming jQuery is available
// Avoid excessively updating the position while scrolling.
// jQuery(window).on('scroll', _.throttle(updatePosition, 100));
```

---

### `_.memoize(func, [resolver])`

Creates a function that memoizes the result of `func`. If `resolver` is provided, it determines the cache key for storing the result based on the arguments. By default, the first argument is used as the cache key. The cache is exposed as the `cache` property on the memoized function.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `func` | `Function` | The function to have its output memoized. |
| `[resolver]` | `Function` | The function to resolve the cache key. |

**Returns**

- `(Function)`: Returns the new memoized function.

**Example**

```javascript Memoize a function icon=logos:javascript
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

You've now explored the core function utilities in Lodash. These tools are fundamental for managing asynchronous operations, creating reusable function configurations, and building robust applications. To continue, explore the miscellaneous utilities in the [Util](./api-util.md) section or dive into language-level helpers in the [Lang](./api-lang.md) section.