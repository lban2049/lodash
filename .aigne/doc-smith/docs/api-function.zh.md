# 函数

Lodash 提供了一套强大的高阶函数，用于操作和增强其他函数。这些实用工具支持复杂的模式，例如对用户输入进行防抖、对频繁事件进行节流、创建用于部分应用的柯里化函数以及管理执行流。它们是处理异步操作和以更函数化的风格编写代码的重要工具。

有关其他实用工具，请参阅 [Util API 文档](./api-util.md)。

## 函数参考

| 函数 | 描述 |
| --- | --- |
| `_.after(n, func)` | 创建一个函数，该函数仅在被调用 `n` 次或更多次后才调用 `func`。 |
| `_.ary(func, n)` | 创建一个函数，该函数调用 `func` 时最多接受 `n` 个参数，并忽略任何多余的参数。 |
| `_.before(n, func)` | 创建一个函数，该函数在被调用次数少于 `n` 次时调用 `func`。 |
| `_.bind(func, thisArg, [partials])` | 创建一个函数，该函数调用 `func` 时绑定了 `this` 上下文和部分参数。 |
| `_.bindKey(object, key, [partials])` | 将对象的方法绑定到对象本身，从而允许重新定义。 |
| `_.curry(func, [arity])` | 创建一个函数，该函数接受 `func` 的参数，并返回一个新函数，直到提供了所有参数。 |
| `_.curryRight(func, [arity])` | 与 `_.curry` 类似，但参数是从右到左应用的。 |
| `_.debounce(func, [wait], [options])` | 创建一个防抖函数，该函数在指定的等待时间后延迟调用。 |
| `_.defer(func, [args])` | 延迟调用 `func`，直到当前调用堆栈清空。 |
| `_.delay(func, wait, [args])` | 在指定的 `wait` 时间后调用 `func`。 |
| `_.flip(func)` | 创建一个函数，该函数调用 `func` 时其参数是反转的。 |
| `_.memoize(func, [resolver])` | 创建一个函数，该函数会记忆化 `func` 的返回值。 |
| `_.negate(predicate)` | 创建一个函数，该函数会对谓词 `func` 的结果取反。 |
| `_.once(func)` | 创建一个函数，该函数被限制为只能调用 `func` 一次。 |
| `_.overArgs(func, [transforms])` | 创建一个函数，该函数调用 `func` 时其参数由相应的函数转换。 |
| `_.partial(func, [partials])` | 创建一个带有预设部分参数的函数。 |
| `_.partialRight(func, [partials])` | 创建一个带有追加部分参数的函数。 |
| `_.rearg(func, indexes)` | 创建一个函数，该函数调用 `func` 时其参数根据 `indexes` 重新排列。 |
| `_.rest(func, [start])` | 创建一个函数，该函数接受从给定起始位置开始的参数数组。 |
| `_.spread(func, [start])` | 创建一个函数，该函数接受一个参数数组并将其应用于 `func`。 |
| `_.throttle(func, [wait], [options])` | 创建一个节流函数，该函数在每 `wait` 毫秒内最多调用 `func` 一次。 |
| `_.unary(func)` | 创建一个函数，该函数只接受一个参数，并忽略任何其他参数。 |
| `_.wrap(value, wrapper)` | 创建一个函数，该函数将 `value` 作为第一个参数提供给 `wrapper`。 |

---

### `_.after(n, func)`

创建一个函数，该函数在被调用 `n` 次或更多次后调用 `func`。

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `n` | `number` | 在调用 `func` 之前需要调用的次数。 |
| `func` | `Function` | 要限制的函数。 |

**返回值**

- `(Function)`：返回新的受限函数。

**示例**

```javascript
var saves = ['profile', 'settings'];

var done = _.after(saves.length, function() {
  console.log('done saving!');
});

_.forEach(saves, function(type) {
  asyncSave({ 'type': type, 'complete': done });
});
// => 在两个异步保存操作完成后，打印 'done saving!'。
```

### `_.ary(func, n)`

创建一个函数，该函数调用 `func` 时最多接受 `n` 个参数，并忽略任何额外的参数。

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `func` | `Function` | 要限制参数数量的函数。 |
| `[n=func.length]` | `number` | 参数数量上限。 |

**返回值**

- `(Function)`：返回新的参数数量受限的函数。

**示例**

```javascript
_.map(['6', '8', '10'], _.ary(parseInt, 1));
// => [6, 8, 10]
```

### `_.before(n, func)`

创建一个函数，该函数在被调用次数少于 `n` 次时调用 `func`。对所创建函数的后续调用将返回最后一次 `func` 调用的结果。

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `n` | `number` | 不再调用 `func` 的调用次数阈值。 |
| `func` | `Function` | 要限制的函数。 |

**返回值**

- `(Function)`：返回新的受限函数。

**示例**

```javascript
jQuery(element).on('click', _.before(5, addContactToList));
// => 允许向列表中添加最多 4 个联系人。
```

### `_.bind(func, thisArg, [partials])`

创建一个函数，该函数调用 `func` 时，`this` 绑定为 `thisArg`，并将 `partials` 预设到其接收的参数前面。`_.bind.placeholder` 的值 (`_`) 可用作部分应用参数的占位符。

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `func` | `Function` | 要绑定的函数。 |
| `thisArg` | `*` | `func` 的 `this` 绑定。 |
| `...[partials]` | `*` | 要部分应用的参数。 |

**返回值**

- `(Function)`：返回新的绑定函数。

**示例**

```javascript
function greet(greeting, punctuation) {
  return greeting + ' ' + this.user + punctuation;
}

var object = { 'user': 'fred' };

var bound = _.bind(greet, object, 'hi');
bound('!');
// => 'hi fred!'

// 使用占位符进行绑定。
var bound = _.bind(greet, object, _, '!');
bound('hi');
// => 'hi fred!'
```

### `_.debounce(func, [wait=0], [options={}])`

创建一个防抖函数，该函数会延迟调用 `func`，直到自上次调用防抖函数后经过了 `wait` 毫秒。该防抖函数提供了 `cancel` 和 `flush` 方法。

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `func` | `Function` | 要进行防抖处理的函数。 |
| `[wait=0]` | `number` | 延迟的毫秒数。 |
| `[options={}]` | `Object` | 选项对象。 |
| `[options.leading=false]` | `boolean` | 指定在超时前沿调用。 |
| `[options.maxWait]` | `number` | 在调用 `func` 之前允许其延迟的最长时间。 |
| `[options.trailing=true]` | `boolean` | 指定在超时后沿调用。 |

**返回值**

- `(Function)`：返回新的防抖函数。

**示例**

```javascript
// 避免在窗口大小不断变化时进行高开销的计算。
jQuery(window).on('resize', _.debounce(calculateLayout, 150));

// 确保在 1 秒的防抖调用后，batchLog 被调用一次。
var debounced = _.debounce(batchLog, 250, { 'maxWait': 1000 });

// 取消后沿的防抖调用。
jQuery(window).on('popstate', debounced.cancel);
```

### `_.memoize(func, [resolver])`

创建一个函数，用于记忆化 `func` 的结果。如果提供了 `resolver`，它将根据参数确定用于存储结果的缓存键。默认情况下，第一个参数用作缓存键。

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `func` | `Function` | 要将其输出进行记忆化的函数。 |
| `[resolver]` | `Function` | 用于解析缓存键的函数。 |

**返回值**

- `(Function)`：返回新的记忆化函数。

**示例**

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
// => [1, 2] (返回缓存值)

// 修改结果缓存。
values.cache.set(object, ['a', 'b']);
values(object);
// => ['a', 'b']
```

### `_.throttle(func, [wait=0], [options={}])`

创建一个节流函数，该函数在每 `wait` 毫秒内最多只调用 `func` 一次。该节流函数提供了 `cancel` 和 `flush` 方法。

**参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `func` | `Function` | 要进行节流处理的函数。 |
| `[wait=0]` | `number` | 节流调用的毫秒数。 |
| `[options={}]` | `Object` | 选项对象。 |
| `[options.leading=true]` | `boolean` | 指定在超时前沿调用。 |
| `[options.trailing=true]` | `boolean` | 指定在超时后沿调用。 |

**返回值**

- `(Function)`：返回新的节流函数。

**示例**

```javascript
// 避免在滚动时过度更新位置。
jQuery(window).on('scroll', _.throttle(updatePosition, 100));

// 在点击事件触发时调用 renewToken，但每 5 分钟最多调用一次。
var throttled = _.throttle(renewToken, 300000, { 'trailing': false });
jQuery(element).on('click', throttled);

// 取消后沿的节流调用。
jQuery(window).on('popstate', throttled.cancel);
```