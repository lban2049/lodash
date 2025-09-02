# Function

本节详细介绍了 Lodash 中用于操作或返回函数的实用工具。这些函数支持函数式编程技术，如柯里化（currying）、防抖（debouncing）、节流（throttling）和部分应用（partial application），从而可以创建更强大、更灵活的代码。

这些工具在处理事件处理、异步操作和函数组合等场景时尤其有用。要了解如何将这些函数与方法链结合使用，请参阅 [Seq](./api-seq.md) 部分的文档。

## after

`_.before` 的反向操作，创建一个函数，该函数在被调用 `n` 次或更多次后才会调用 `func`。

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `n` | `number` | `func` 被调用前需要调用的次数。 |
| `func` | `Function` | 要限制的函数。 |

**返回**

- `(Function)`: 返回新的受限函数。

**示例**

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

## ary

创建一个函数，该函数最多接受 `n` 个参数，忽略任何额外的参数。

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `func` | `Function` | 要限制参数数量的函数。 |
| `[n=func.length]` | `number` | 参数数量上限。 |

**返回**

- `(Function)`: 返回新的参数受限函数。

**示例**

```javascript
_.map(['6', '8', '10'], _.ary(parseInt, 1));
// => [6, 8, 10]
```

## before

创建一个函数，当它被调用少于 `n` 次时，调用 `func`。之后对该函数的调用将返回最后一次 `func` 调用的结果。

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `n` | `number` | 不再调用 `func` 的调用次数。 |
| `func` | `Function` | 要限制的函数。 |

**返回**

- `(Function)`: 返回新的受限函数。

**示例**

```javascript
jQuery(element).on('click', _.before(5, addContactToList));
// => 最多允许向列表中添加 4 个联系人。
```

## bind

创建一个函数，该函数使用 `thisArg` 作为 `this` 绑定，并预设 `partials` 参数来调用 `func`。`_.bind.placeholder` 值（在整体构建中默认为 `_`）可用作部分应用参数的占位符。

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `func` | `Function` | 要绑定的函数。 |
| `thisArg` | `*` | `func` 的 `this` 绑定。 |
| `[...partials]` | `*` | 要预设的参数。 |

**返回**

- `(Function)`: 返回新的绑定函数。

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

## bindKey

创建一个函数，该函数使用 `partials` 预设的参数调用 `object[key]` 处的方法。此方法与 `_.bind` 的不同之处在于，它允许绑定的函数引用可能被重新定义或尚不存在的方法。

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `object` | `Object` | 要调用方法的对象。 |
| `key` | `string` | 方法的键。 |
| `[...partials]` | `*` | 要预设的参数。 |

**返回**

- `(Function)`: 返回新的绑定函数。

**示例**

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

## curry

创建一个函数，该函数接受 `func` 的参数。如果提供了足够数量的参数，则调用 `func` 并返回结果；否则，返回一个接受剩余参数的函数。`_.curry.placeholder` 值可用作参数占位符。

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `func` | `Function` | 要柯里化的函数。 |
| `[arity=func.length]` | `number` | `func` 的参数数量。 |

**返回**

- `(Function)`: 返回新的柯里化函数。

**示例**

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

## curryRight

此方法类似于 `_.curry`，但参数是以 `_.partialRight` 的方式应用于 `func`。

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `func` | `Function` | 要柯里化的函数。 |
| `[arity=func.length]` | `number` | `func` 的参数数量。 |

**返回**

- `(Function)`: 返回新的柯里化函数。

**示例**

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

## debounce

创建一个防抖函数，该函数延迟调用 `func`，直到自上次调用防抖函数后经过 `wait` 毫秒。防抖函数附带一个 `cancel` 方法用于取消延迟的 `func` 调用和一个 `flush` 方法用于立即调用它们。提供 `options` 来指示 `func` 是否应在 `wait` 超时的前缘和/或后缘调用。

```d2
shape: sequence_diagram

"用户操作" -> "_.debounce(func)": "调用 1 (参数1)"
"_.debounce(func)" -> "定时器": "启动等待定时器"

"用户操作" -> "_.debounce(func)": "调用 2 (参数2)"
"_.debounce(func)" -> "定时器": "重置等待定时器"

"定时器" -> "_.debounce(func)": "定时器到期"
"_.debounce(func)" -> "原始函数": "使用最新参数(参数2)调用"
```

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `func` | `Function` | 要防抖的函数。 |
| `[wait=0]` | `number` | 延迟的毫秒数。 |
| `[options={}]` | `Object` | 选项对象。 |
| `[options.leading=false]` | `boolean` | 指定在超时的前缘调用。 |
| `[options.maxWait]` | `number` | `func` 被允许延迟调用的最长时间。 |
| `[options.trailing=true]` | `boolean` | 指定在超时的后缘调用。 |

**返回**

- `(Function)`: 返回新的防抖函数。

**示例**

```javascript
// 在窗口大小变化时避免昂贵的计算。
jQuery(window).on('resize', _.debounce(calculateLayout, 150));

// 单击时调用 sendMail，并对后续调用进行防抖。
jQuery(element).on('click', _.debounce(sendMail, 300, {
  'leading': true,
  'trailing': false
}));

// 取消后缘的防抖调用。
jQuery(window).on('popstate', debounced.cancel);
```

## defer

延迟调用 `func` 直到当前调用栈清空。任何额外的参数都会在调用 `func` 时提供给它。

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `func` | `Function` | 要延迟的函数。 |
| `[...args]` | `*` | 调用 `func` 的参数。 |

**返回**

- `(number)`: 返回定时器 ID。

**示例**

```javascript
_.defer(function(text) {
  console.log(text);
}, 'deferred');
// => 在一毫秒后打印 'deferred'。
```

## delay

在 `wait` 毫秒后调用 `func`。任何额外的参数都会在调用 `func` 时提供给它。

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `func` | `Function` | 要延迟的函数。 |
| `wait` | `number` | 延迟调用的毫秒数。 |
| `[...args]` | `*` | 调用 `func` 的参数。 |

**返回**

- `(number)`: 返回定时器 ID。

**示例**

```javascript
_.delay(function(text) {
  console.log(text);
}, 1000, 'later');
// => 一秒后打印 'later'。
```

## flip

创建一个函数，该函数以相反的参数顺序调用 `func`。

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `func` | `Function` | 要翻转参数的函数。 |

**返回**

- `(Function)`: 返回新的翻转函数。

**示例**

```javascript
var flipped = _.flip(function() {
  return _.toArray(arguments);
});

flipped('a', 'b', 'c', 'd');
// => ['d', 'c', 'b', 'a']
```

## memoize

创建一个函数，该函数会缓存 `func` 的结果。如果提供了 `resolver`，它将根据提供给记忆化函数的参数来确定缓存键。默认情况下，提供给记忆化函数的第一个参数用作缓存键。

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `func` | `Function` | 要记忆其输出的函数。 |
| `[resolver]` | `Function` | 用于解析缓存键的函数。 |

**返回**

- `(Function)`: 返回新的记忆化函数。

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
// => [1, 2] (返回缓存的结果)

// 修改结果缓存。
values.cache.set(object, ['a', 'b']);
values(object);
// => ['a', 'b']
```

## negate

创建一个函数，该函数否定谓词 `func` 的结果。

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `predicate` | `Function` | 要否定的谓词。 |

**返回**

- `(Function)`: 返回新的否定函数。

**示例**

```javascript
function isEven(n) {
  return n % 2 == 0;
}

_.filter([1, 2, 3, 4, 5, 6], _.negate(isEven));
// => [1, 3, 5]
```

## once

创建一个函数，该函数仅受限于调用 `func` 一次。重复调用该函数将返回第一次调用的值。

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `func` | `Function` | 要限制的函数。 |

**返回**

- `(Function)`: 返回新的受限函数。

**示例**

```javascript
var initialize = _.once(createApplication);
initialize();
initialize();
// => `createApplication` 只被调用一次
```

## overArgs

创建一个函数，该函数使用转换后的参数调用 `func`。

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `func` | `Function` | 要包装的函数。 |
| `[...transforms]` | `(Function|Function[])` | 参数的转换函数。 |

**返回**

- `(Function)`: 返回新的函数。

**示例**

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
```

## partial

创建一个函数，该函数使用预设的 `partials` 参数调用 `func`。此方法类似于 `_.bind`，但不改变 `this` 绑定。

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `func` | `Function` | 要部分应用参数的函数。 |
| `[...partials]` | `*` | 要部分应用的参数。 |

**返回**

- `(Function)`: 返回新的部分应用函数。

**示例**

```javascript
function greet(greeting, name) {
  return greeting + ' ' + name;
}

var sayHelloTo = _.partial(greet, 'hello');
sayHelloTo('fred');
// => 'hello fred'
```

## partialRight

此方法类似于 `_.partial`，但部分应用的参数会附加到它接收的参数之后。

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `func` | `Function` | 要部分应用参数的函数。 |
| `[...partials]` | `*` | 要部分应用的参数。 |

**返回**

- `(Function)`: 返回新的部分应用函数。

**示例**

```javascript
function greet(greeting, name) {
  return greeting + ' ' + name;
}

var greetFred = _.partialRight(greet, 'fred');
greetFred('hi');
// => 'hi fred'
```

## rearg

创建一个函数，该函数根据指定的 `indexes` 重新排列参数后调用 `func`。

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `func` | `Function` | 要重新排列参数的函数。 |
| `[...indexes]` | `(number|number[])` | 排列后的参数索引。 |

**返回**

- `(Function)`: 返回新的函数。

**示例**

```javascript
var rearged = _.rearg(function(a, b, c) {
  return [a, b, c];
}, [2, 0, 1]);

rearged('b', 'c', 'a')
// => ['a', 'b', 'c']
```

## rest

创建一个函数，该函数使用 `this` 绑定和从 `start` 位置开始的参数数组来调用 `func`。

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `func` | `Function` | 要应用剩余参数的函数。 |
| `[start=func.length-1]` | `number` | 剩余参数的起始位置。 |

**返回**

- `(Function)`: 返回新的函数。

**示例**

```javascript
var say = _.rest(function(what, names) {
  return what + ' ' + _.initial(names).join(', ') +
    (_.size(names) > 1 ? ', & ' : '') + _.last(names);
});

say('hello', 'fred', 'barney', 'pebbles');
// => 'hello fred, barney, & pebbles'
```

## spread

创建一个函数，该函数使用 `this` 绑定和参数数组来调用 `func`，类似于 `Function#apply`。

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `func` | `Function` | 要展开参数的函数。 |
| `[start=0]` | `number` | 展开的起始位置。 |

**返回**

- `(Function)`: 返回新的函数。

**示例**

```javascript
var say = _.spread(function(who, what) {
  return who + ' says ' + what;
});

say(['fred', 'hello']);
// => 'fred says hello'
```

## throttle

创建一个节流函数，该函数在每 `wait` 毫秒内最多只调用 `func` 一次。节流函数附带一个 `cancel` 方法用于取消延迟的 `func` 调用和一个 `flush` 方法用于立即调用它们。

```d2
shape: sequence_diagram

"用户操作" -> "_.throttle(func, wait)": "调用 1"
"_.throttle(func, wait)" -> "原始函数": "调用 (前缘)"

"用户操作" -> "_.throttle(func, wait)": "调用 2"

"_.throttle(func, wait)" -> "原始函数": "使用调用2的参数调用 (后缘)"
```

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `func` | `Function` | 要节流的函数。 |
| `[wait=0]` | `number` | 节流调用的毫秒数。 |
| `[options={}]` | `Object` | 选项对象。 |
| `[options.leading=true]` | `boolean` | 指定在超时的前缘调用。 |
| `[options.trailing=true]` | `boolean` | 指定在超时的后缘调用。 |

**返回**

- `(Function)`: 返回新的节流函数。

**示例**

```javascript
// 避免在滚动时过度更新位置。
jQuery(window).on('scroll', _.throttle(updatePosition, 100));

// 取消后缘的节流调用。
jQuery(window).on('popstate', throttled.cancel);
```

## unary

创建一个函数，该函数最多接受一个参数，忽略任何额外的参数。

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `func` | `Function` | 要限制参数数量的函数。 |

**返回**

- `(Function)`: 返回新的参数受限函数。

**示例**

```javascript
_.map(['6', '8', '10'], _.unary(parseInt));
// => [6, 8, 10]
```

## wrap

创建一个函数，该函数将 `value` 作为第一个参数提供给 `wrapper`。提供给该函数的任何额外参数都将附加到提供给 `wrapper` 的参数之后。

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要包装的值。 |
| `[wrapper=identity]` | `Function` | 包装函数。 |

**返回**

- `(Function)`: 返回新的函数。

**示例**

```javascript
var p = _.wrap(_.escape, function(func, text) {
  return '<p>' + func(text) + '</p>';
});

p('fred, barney, & pebbles');
// => '<p>fred, barney, &amp; pebbles</p>'
```

---

本节涵盖了 Lodash 中核心的函数式实用工具。掌握这些函数将有助于编写更简洁、更具声明性的代码。接下来，您可以探索 [Lang](./api-lang.md) 部分，了解类型检查和对象克隆等实用工具。