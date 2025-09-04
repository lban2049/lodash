# 函数

Lodash 提供了一套强大的高阶函数，这些函数可以操作或返回其他函数。这些实用工具对于函数式编程范式至关重要，它们允许你以复杂的方式操纵函数行为，例如控制调用频率、更改参数签名以及管理 `this` 上下文。

主要功能包括：

*   **调用控制**：像 `debounce`、`throttle`、`once`、`before` 和 `after` 这样的函数让你能够精细地控制函数的执行时间以及执行次数。
*   **参数操作**：像 `curry`、`partial`、`flip`、`rearg` 和 `spread` 这样的实用工具允许灵活的函数组合和参数转换。
*   **上下文绑定**：`bind` 和 `bindKey` 为设置函数的 `this` 上下文提供了强大的机制。
*   **记忆化**：`memoize` 会缓存高开销函数调用的结果以提高性能。

这些工具有助于创建更具可重用性、模块化和声明性的代码。关于类型检查函数，请参阅 [Lang](./api-lang.md) 文档中的 `isFunction` 方法。

---

## after

创建一个函数，该函数在被调用 `n` 次或更多次后才会调用 `func`。

### 参数

| Name | Type | Description |
|---|---|---|
| `n` | `number` | 在 `func` 被调用前需要调用的次数。 |
| `func` | `Function` | 要限制的函数。 |

### 返回

- `(Function)`：返回新的受限函数。

### 示例

```javascript
var saves = ['profile', 'settings'];

var done = _.after(saves.length, function() {
  console.log('done saving!');
});

_.forEach(saves, function(type) {
  asyncSave({ 'type': type, 'complete': done });
});
// => 在两次异步保存完成后，打印 'done saving!'
```

---

## ary

创建一个函数，该函数调用 `func` 时最多接受 `n` 个参数，并忽略任何额外的参数。

### 参数

| Name | Type | Description |
|---|---|---|
| `func` | `Function` | 要限制参数数量的函数。 |
| `n` | `number` | （可选）参数数量上限。默认为 `func.length`。 |

### 返回

- `(Function)`：返回新的参数数量受限的函数。

### 示例

```javascript
_.map(['6', '8', '10'], _.ary(parseInt, 1));
// => [6, 8, 10]
```

---

## before

创建一个函数，该函数在被调用少于 `n` 次时，会使用创建函数的 `this` 绑定和参数来调用 `func`。之后对创建函数的调用将返回最后一次 `func` 调用的结果。

### 参数

| Name | Type | Description |
|---|---|---|
| `n` | `number` | 调用次数的阈值，达到该次数后 `func` 将不再被调用。 |
| `func` | `Function` | 要限制的函数。 |

### 返回

- `(Function)`：返回新的受限函数。

### 示例

```javascript
// 假设 jQuery 可用
// jQuery(element).on('click', _.before(5, addContactToList));
// => 允许向列表中添加最多 4 个联系人。
```

---

## bind

创建一个函数，该函数使用 `thisArg` 作为 `this` 绑定来调用 `func`，并将 `partials` 参数预设在它接收的参数前面。`_.bind.placeholder` 的值 (`_`)可以用作部分应用参数的占位符。

### 参数

| Name | Type | Description |
|---|---|---|
| `func` | `Function` | 要绑定的函数。 |
| `thisArg` | `*` | `func` 的 `this` 绑定。 |
| `...partials` | `*` | （可选）要部分应用的参数。 |

### 返回

- `(Function)`：返回新的绑定函数。

### 示例

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

---

## bindKey

创建一个函数，该函数调用 `object[key]` 上的方法，并将 `partials` 参数预设在它接收的参数前面。此方法允许绑定的函数引用可能被重新定义或尚不存在的方法。

### 参数

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | 要在其上调用方法的对象。 |
| `key` | `string` | 方法的键。 |
| `...partials` | `*` | （可选）要部分应用的参数。 |

### 返回

- `(Function)`：返回新的绑定函数。

### 示例

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

创建一个函数，该函数接受 `func` 的参数。如果已提供至少 `arity` 个参数，则调用 `func` 并返回其结果；否则，返回一个接受 `func` 剩余参数的函数，依此类推。

### 参数

| Name | Type | Description |
|---|---|---|
| `func` | `Function` | 要柯里化的函数。 |
| `arity` | `number` | （可选）`func` 的参数个数。默认为 `func.length`。 |

### 返回

- `(Function)`：返回新的柯里化函数。

### 示例

```javascript
var abc = function(a, b, c) {
  return [a, b, c];
};

var curried = _.curry(abc);

curried(1)(2)(3);
// => [1, 2, 3]

curried(1, 2)(3);
// => [1, 2, 3]

// 使用占位符进行柯里化。
curried(1)(_, 3)(2);
// => [1, 2, 3]
```

---

## curryRight

此方法类似于 `_.curry`，不同之处在于参数是从右到左应用于 `func` 的。

### 参数

| Name | Type | Description |
|---|---|---|
| `func` | `Function` | 要柯里化的函数。 |
| `arity` | `number` | （可选）`func` 的参数个数。默认为 `func.length`。 |

### 返回

- `(Function)`：返回新的柯里化函数。

### 示例

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

创建一个防抖函数，该函数会从上次被调用后，延迟 `wait` 毫秒后调用 `func`。防抖函数带有一个 `cancel` 方法，用于取消延迟的 `func` 调用，还有一个 `flush` 方法，用于立即调用。可以提供 `options` 来指定 `func` 是否应在 `wait` 超时的前沿和/或后沿调用。`func` 会使用提供给防抖函数的最后一次参数来调用。

### 参数

| Name | Type | Description |
|---|---|---|
| `func` | `Function` | 要防抖的函数。 |
| `wait` | `number` | （可选）要延迟的毫秒数。默认为 0。 |
| `options` | `Object` | （可选）选项对象。 |
| `options.leading` | `boolean` | （可选）指定在超时的前沿调用。默认为 `false`。 |
| `options.maxWait` | `number` | （可选）`func` 在被调用前被允许延迟的最长时间。 |
| `options.trailing` | `boolean` | （可选）指定在超时的后沿调用。默认为 `true`。 |

### 返回

- `(Function)`：返回新的防抖函数。

### 示例

```javascript
// 假设 jQuery 可用
// 避免在窗口大小不断变化时进行高开销的计算。
// jQuery(window).on('resize', _.debounce(calculateLayout, 150));

// 点击时调用 'sendMail'，并对后续调用进行防抖处理。
// jQuery(element).on('click', _.debounce(sendMail, 300, {
//   'leading': true,
//   'trailing': false
// }));

// 取消在后沿的防抖调用。
// jQuery(window).on('popstate', debounced.cancel);
```

---

## defer

延迟调用 `func`，直到当前调用栈清空为止。调用 `func` 时会提供任何额外的参数。

### 参数

| Name | Type | Description |
|---|---|---|
| `func` | `Function` | 要延迟的函数。 |
| `...args` | `*` | （可选）调用 `func` 时使用的参数。 |

### 返回

- `(number)`：返回计时器 ID。

### 示例

```javascript
_.defer(function(text) {
  console.log(text);
}, 'deferred');
// => 一毫秒后打印 'deferred'。
```

---

## delay

在 `wait` 毫秒后调用 `func`。调用 `func` 时会提供任何额外的参数。

### 参数

| Name | Type | Description |
|---|---|---|
| `func` | `Function` | 要延迟的函数。 |
| `wait` | `number` | 延迟调用的毫秒数。 |
| `...args` | `*` | （可选）调用 `func` 时使用的参数。 |

### 返回

- `(number)`：返回计时器 ID。

### 示例

```javascript
_.delay(function(text) {
  console.log(text);
}, 1000, 'later');
// => 一秒后打印 'later'。
```

---

## flip

创建一个函数，该函数使用反转后的参数调用 `func`。

### 参数

| Name | Type | Description |
|---|---|---|
| `func` | `Function` | 要反转其参数的函数。 |

### 返回

- `(Function)`：返回新的参数反转后的函数。

### 示例

```javascript
var flipped = _.flip(function() {
  return _.toArray(arguments);
});

flipped('a', 'b', 'c', 'd');
// => ['d', 'c', 'b', 'a']
```

---

## memoize

创建一个函数，该函数会记忆 `func` 的结果。如果提供了 `resolver`，它会根据提供给记忆化函数的参数来确定用于存储结果的缓存键。默认情况下，提供给记忆化函数的第一个参数被用作 map 缓存键。缓存通过记忆化函数上的 `cache` 属性暴露出来。

### 参数

| Name | Type | Description |
|---|---|---|
| `func` | `Function` | 要将其输出记忆化的函数。 |
| `resolver` | `Function` | （可选）用于解析缓存键的函数。 |

### 返回

- `(Function)`：返回新的记忆化函数。

### 示例

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

// 修改结果缓存。
values.cache.set(object, ['a', 'b']);
values(object);
// => ['a', 'b']
```

---

## negate

创建一个函数，该函数会对谓词 `func` 的结果取反。`func` 谓词会使用创建函数的 `this` 绑定和参数来调用。

### 参数

| Name | Type | Description |
|---|---|---|
| `predicate` | `Function` | 要取反的谓词。 |

### 返回

- `(Function)`：返回新的取反函数。

### 示例

```javascript
function isEven(n) {
  return n % 2 == 0;
}

_.filter([1, 2, 3, 4, 5, 6], _.negate(isEven));
// => [1, 3, 5]
```

---

## once

创建一个仅能调用 `func` 一次的函数。重复调用该函数会返回第一次调用的值。`func` 会使用创建函数的 `this` 绑定和参数来调用。

### 参数

| Name | Type | Description |
|---|---|---|
| `func` | `Function` | 要限制的函数。 |

### 返回

- `(Function)`：返回新的受限函数。

### 示例

```javascript
// var initialize = _.once(createApplication);
// initialize();
// initialize();
// => `createApplication` 只被调用一次
```

---

## overArgs

创建一个函数，该函数使用转换后的参数调用 `func`。

### 参数

| Name | Type | Description |
|---|---|---|
| `func` | `Function` | 要包装的函数。 |
| `...transforms`| `(Function|Function[])` | （可选）参数转换函数。默认为 `_.identity`。 |

### 返回

- `(Function)`：返回新的函数。

### 示例

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

创建一个函数，该函数调用 `func` 时会将 `partials` 参数预设在它接收的参数前面。此方法类似于 `_.bind`，但它不会改变 `this` 绑定。

### 参数

| Name | Type | Description |
|---|---|---|
| `func` | `Function` | 要部分应用参数的函数。 |
| `...partials` | `*` | （可选）要部分应用的参数。 |

### 返回

- `(Function)`：返回新的部分应用函数。

### 示例

```javascript
function greet(greeting, name) {
  return greeting + ' ' + name;
}

var sayHelloTo = _.partial(greet, 'hello');
sayHelloTo('fred');
// => 'hello fred'

// 使用占位符进行部分应用。
var greetFred = _.partial(greet, _, 'fred');
greetFred('hi');
// => 'hi fred'
```

---

## partialRight

此方法类似于 `_.partial`，不同之处在于部分应用的参数会附加到它接收的参数后面。

### 参数

| Name | Type | Description |
|---|---|---|
| `func` | `Function` | 要部分应用参数的函数。 |
| `...partials` | `*` | （可选）要部分应用的参数。 |

### 返回

- `(Function)`：返回新的部分应用函数。

### 示例

```javascript
function greet(greeting, name) {
  return greeting + ' ' + name;
}

var greetFred = _.partialRight(greet, 'fred');
greetFred('hi');
// => 'hi fred'

// 使用占位符进行部分应用。
var sayHelloTo = _.partialRight(greet, 'hello', _);
sayHelloTo('fred');
// => 'hello fred'
```

---

## rearg

创建一个函数，该函数根据指定的 `indexes` 重新排列参数后调用 `func`。

### 参数

| Name | Type | Description |
|---|---|---|
| `func` | `Function` | 要重排其参数的函数。 |
| `...indexes` | `(number|number[])` | 排列后的参数索引。 |

### 返回

- `(Function)`：返回新的函数。

### 示例

```javascript
var rearged = _.rearg(function(a, b, c) {
  return [a, b, c];
}, [2, 0, 1]);

rearged('b', 'c', 'a')
// => ['a', 'b', 'c']
```

---

## rest

创建一个函数，该函数使用创建函数的 `this` 绑定来调用 `func`，并将从 `start` 位置及之后的所有参数作为一个数组提供。

### 参数

| Name | Type | Description |
|---|---|---|
| `func` | `Function` | 要应用 rest 参数的函数。 |
| `start` | `number` | （可选）rest 参数的起始位置。默认为 `func.length - 1`。 |

### 返回

- `(Function)`：返回新的函数。

### 示例

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

创建一个函数，该函数使用创建函数的 `this` 绑定来调用 `func`，并接受一个参数数组，非常类似于 `Function#apply`。

### 参数

| Name | Type | Description |
|---|---|---|
| `func` | `Function` | 要展开参数的函数。 |
| `start` | `number` | （可选）展开的起始位置。默认为 0。 |

### 返回

- `(Function)`：返回新的函数。

### 示例

```javascript
var say = _.spread(function(who, what) {
  return who + ' says ' + what;
});

say(['fred', 'hello']);
// => 'fred says hello'
```

---

## throttle

创建一个节流函数，该函数在每 `wait` 毫秒内最多调用一次 `func`。节流函数带有一个 `cancel` 方法，用于取消延迟的 `func` 调用，还有一个 `flush` 方法，用于立即调用。

### 参数

| Name | Type | Description |
|---|---|---|
| `func` | `Function` | 要节流的函数。 |
| `wait` | `number` | （可选）节流调用的毫秒数。默认为 0。 |
| `options` | `Object` | （可选）选项对象。 |
| `options.leading` | `boolean` | （可选）指定在超时的前沿调用。默认为 `true`。 |
| `options.trailing` | `boolean` | （可选）指定在超时的后沿调用。默认为 `true`。 |

### 返回

- `(Function)`：返回新的节流函数。

### 示例

```javascript
// 假设 jQuery 可用
// 避免在滚动时过度更新位置。
// jQuery(window).on('scroll', _.throttle(updatePosition, 100));

// 取消在后沿的节流调用。
// jQuery(window).on('popstate', throttled.cancel);
```

---

## unary

创建一个最多接受一个参数的函数，并忽略任何额外的参数。

### 参数

| Name | Type | Description |
|---|---|---|
| `func` | `Function` | 要限制参数数量的函数。 |

### 返回

- `(Function)`：返回新的参数数量受限的函数。

### 示例

```javascript
_.map(['6', '8', '10'], _.unary(parseInt));
// => [6, 8, 10]
```

---

## wrap

创建一个函数，它将 `value` 作为第一个参数提供给 `wrapper`。提供给该函数的任何额外参数都会附加到提供给 `wrapper` 的参数之后。wrapper 会使用创建函数的 `this` 绑定来调用。

### 参数

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 要包装的值。 |
| `wrapper` | `Function` | （可选）包装函数。默认为 `identity`。 |

### 返回

- `(Function)`：返回新的函数。

### 示例

```javascript
var p = _.wrap(_.escape, function(func, text) {
  return '<p>' + func(text) + '</p>';
});

p('fred, barney, & pebbles');
// => '<p>fred, barney, &amp; pebbles</p>'
```

---

函数实用工具的参考到此结束。要探索其他类型的实用工具，接下来你可能需要查看 [Util](./api-util.md) 部分。