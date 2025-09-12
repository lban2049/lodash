# 函数

Lodash 提供了一套强大的函数操作工具集。这些辅助函数可以让你控制调用频率、改变函数签名以及从简单的部分组合出复杂的行为。常见用例包括使用 `debounce` 和 `throttle` 延迟或限制函数调用，使用 `partial` 和 `curry` 创建可复用的、部分应用的函数，以及使用 `after` 和 `before` 管理函数执行流程。

这些工具是编写简洁、高效和函数式 JavaScript 的基础。要深入了解这些概念，请查看我们的[函数式编程指南](./fp-guide.md)。

---

## after

创建一个函数，这个函数在被调用 `n` 次或更多次后会调用 `func`。

### 参数

<x-field data-name="n" data-type="number" data-required="true" data-desc="在 func 被调用之前需要调用的次数。"></x-field>
<x-field data-name="func" data-type="Function" data-required="true" data-desc="要限制的函数。"></x-field>

### 返回值

<x-field data-name="restricted" data-type="Function" data-desc="返回新的受限函数。"></x-field>

### 示例

```javascript icon=logos:javascript
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

<x-field data-name="func" data-type="Function" data-required="true" data-desc="要限制参数数量的函数。"></x-field>
<x-field data-name="n" data-type="number" data-default="func.length" data-required="false" data-desc="参数数量上限。"></x-field>

### 返回值

<x-field data-name="capped" data-type="Function" data-desc="返回新的参数数量受限的函数。"></x-field>

### 示例

```javascript icon=logos:javascript
_.map(['6', '8', '10'], _.ary(parseInt, 1));
// => [6, 8, 10]
```

---

## before

创建一个函数，当调用次数少于 `n` 次时，该函数会使用创建函数的 `this` 绑定和参数来调用 `func`。之后对创建函数的调用将返回最后一次 `func` 调用的结果。

### 参数

<x-field data-name="n" data-type="number" data-required="true" data-desc="达到此次数后 func 将不再被调用。"></x-field>
<x-field data-name="func" data-type="Function" data-required="true" data-desc="要限制的函数。"></x-field>

### 返回值

<x-field data-name="restricted" data-type="Function" data-desc="返回新的受限函数。"></x-field>

### 示例

```javascript icon=logos:javascript
jQuery(element).on('click', _.before(5, addContactToList));
// => 允许向列表中添加最多 4 个联系人。
```

---

## bind

创建一个函数，该函数使用 `thisArg` 作为 `this` 绑定，并将 `partials` 预设在接收到的参数前面来调用 `func`。`_.bind.placeholder` 的值 (`_`) 可以用作部分应用参数的占位符。

### 参数

<x-field data-name="func" data-type="Function" data-required="true" data-desc="要绑定的函数。"></x-field>
<x-field data-name="thisArg" data-type="any" data-required="true" data-desc="func 的 'this' 绑定。"></x-field>
<x-field data-name="partials" data-type="...any" data-required="false" data-desc="要部分应用的参数。"></x-field>

### 返回值

<x-field data-name="bound" data-type="Function" data-desc="返回新的绑定函数。"></x-field>

### 示例

```javascript icon=logos:javascript
function greet(greeting, punctuation) {
  return greeting + ' ' + this.user + punctuation;
}

var object = { 'user': 'fred' };

var bound = _.bind(greet, object, 'hi');
bound('!');
// => 'hi fred!'

// 使用占位符绑定。
var bound = _.bind(greet, object, _, '!');
bound('hi');
// => 'hi fred!'
```

---

## bindKey

创建一个函数，该函数调用 `object[key]` 上的方法，并将 `partials` 预设在其参数前面。此方法允许绑定的函数引用稍后可能被重新定义的方法。

### 参数

<x-field data-name="object" data-type="Object" data-required="true" data-desc="要在其上调用方法的对象。"></x-field>
<x-field data-name="key" data-type="string" data-required="true" data-desc="方法的键。"></x-field>
<x-field data-name="partials" data-type="...any" data-required="false" data-desc="要部分应用的参数。"></x-field>

### 返回值

<x-field data-name="bound" data-type="Function" data-desc="返回新的绑定函数。"></x-field>

### 示例

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

创建一个函数，该函数接受 `func` 的参数。如果已提供至少 `arity` 个参数，则调用 `func` 并返回其结果；否则，返回一个接受剩余参数的函数。

### 参数

<x-field data-name="func" data-type="Function" data-required="true" data-desc="要柯里化的函数。"></x-field>
<x-field data-name="arity" data-type="number" data-default="func.length" data-required="false" data-desc="func 的参数数量。"></x-field>

### 返回值

<x-field data-name="curried" data-type="Function" data-desc="返回新的柯里化函数。"></x-field>

### 示例

```javascript icon=logos:javascript
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

## debounce

创建一个防抖函数，该函数会延迟调用 `func`，直到自上次调用防抖函数后经过了 `wait` 毫秒。

### 参数

<x-field data-name="func" data-type="Function" data-required="true" data-desc="要防抖的函数。"></x-field>
<x-field data-name="wait" data-type="number" data-default="0" data-required="false" data-desc="延迟的毫秒数。"></x-field>
<x-field data-name="options" data-type="Object" data-required="false" data-desc="选项对象。">
  <x-field data-name="leading" data-type="boolean" data-default="false" data-required="false" data-desc="指定在超时前沿调用。"></x-field>
  <x-field data-name="maxWait" data-type="number" data-required="false" data-desc="func 在被调用前允许被延迟的最长时间。"></x-field>
  <x-field data-name="trailing" data-type="boolean" data-default="true" data-required="false" data-desc="指定在超时后沿调用。"></x-field>
</x-field>

### 返回值

<x-field data-name="debounced" data-type="Function" data-desc="返回新的防抖函数，该函数具有 'cancel' 和 'flush' 方法。"></x-field>

### 示例

```javascript icon=logos:javascript
// 避免在窗口大小不断变化时进行高开销的计算。
jQuery(window).on('resize', _.debounce(calculateLayout, 150));

// 取消延迟的防抖调用。
jQuery(window).on('popstate', debounced.cancel);
```

---

## defer

延迟调用 `func`，直到当前调用栈清空，类似于超时时间为 0 的 `setTimeout`。

### 参数

<x-field data-name="func" data-type="Function" data-required="true" data-desc="要延迟的函数。"></x-field>
<x-field data-name="args" data-type="...any" data-required="false" data-desc="调用 func 时传入的参数。"></x-field>

### 返回值

<x-field data-name="timerId" data-type="number" data-desc="返回定时器 ID。"></x-field>

### 示例

```javascript icon=logos:javascript
_.defer(function(text) {
  console.log(text);
}, 'deferred');
// => 一毫秒后打印 'deferred'。
```

---

## delay

在 `wait` 毫秒后调用 `func`。调用 `func` 时会提供任何额外的参数。

### 参数

<x-field data-name="func" data-type="Function" data-required="true" data-desc="要延迟的函数。"></x-field>
<x-field data-name="wait" data-type="number" data-required="true" data-desc="延迟调用的毫秒数。"></x-field>
<x-field data-name="args" data-type="...any" data-required="false" data-desc="调用 func 时传入的参数。"></x-field>

### 返回值

<x-field data-name="timerId" data-type="number" data-desc="返回定时器 ID。"></x-field>

### 示例

```javascript icon=logos:javascript
_.delay(function(text) {
  console.log(text);
}, 1000, 'later');
// => 一秒后打印 'later'。
```

---

## flip

创建一个函数，该函数以相反的参数顺序调用 `func`。

### 参数

<x-field data-name="func" data-type="Function" data-required="true" data-desc="要反转参数的函数。"></x-field>

### 返回值

<x-field data-name="flipped" data-type="Function" data-desc="返回新的参数反转后的函数。"></x-field>

### 示例

```javascript icon=logos:javascript
var flipped = _.flip(function() {
  return _.toArray(arguments);
});

flipped('a', 'b', 'c', 'd');
// => ['d', 'c', 'b', 'a']
```

---

## memoize

创建一个函数，该函数会缓存 `func` 的计算结果。缓存作为记忆化函数的 `cache` 属性暴露出来。

### 参数

<x-field data-name="func" data-type="Function" data-required="true" data-desc="其输出需要被记忆化的函数。"></x-field>
<x-field data-name="resolver" data-type="Function" data-required="false" data-desc="用于解析缓存键的函数。默认情况下，使用第一个参数。"></x-field>

### 返回值

<x-field data-name="memoized" data-type="Function" data-desc="返回新的记忆化函数。"></x-field>

### 示例

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
// => [1, 2] (返回缓存值)

// 修改结果缓存。
values.cache.set(object, ['a', 'b']);
values(object);
// => ['a', 'b']
```

---

## negate

创建一个函数，该函数会对谓词函数 `func` 的结果取反。

### 参数

<x-field data-name="predicate" data-type="Function" data-required="true" data-desc="要取反的谓词函数。"></x-field>

### 返回值

<x-field data-name="negated" data-type="Function" data-desc="返回新的取反后的函数。"></x-field>

### 示例

```javascript icon=logos:javascript
function isEven(n) {
  return n % 2 == 0;
}

_.filter([1, 2, 3, 4, 5, 6], _.negate(isEven));
// => [1, 3, 5]
```

---

## once

创建一个函数，该函数只能调用 `func` 一次。重复调用将返回第一次调用的值。

### 参数

<x-field data-name="func" data-type="Function" data-required="true" data-desc="要限制的函数。"></x-field>

### 返回值

<x-field data-name="restricted" data-type="Function" data-desc="返回新的受限函数。"></x-field>

### 示例

```javascript icon=logos:javascript
var initialize = _.once(createApplication);
initialize();
initialize();
// => `createApplication` 只被调用一次。
```

---

## partial

创建一个函数，该函数使用预设的 `partials` 参数和接收到的参数来调用 `func`。此方法类似于 `_.bind`，但不会改变 `this` 的绑定。

### 参数

<x-field data-name="func" data-type="Function" data-required="true" data-desc="要部分应用参数的函数。"></x-field>
<x-field data-name="partials" data-type="...any" data-required="false" data-desc="要部分应用的参数。"></x-field>

### 返回值

<x-field data-name="partialized" data-type="Function" data-desc="返回新的部分应用函数。"></x-field>

### 示例

```javascript icon=logos:javascript
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

## throttle

创建一个节流函数，该函数在每 `wait` 毫秒内最多调用 `func` 一次。

### 参数

<x-field data-name="func" data-type="Function" data-required="true" data-desc="要节流的函数。"></x-field>
<x-field data-name="wait" data-type="number" data-default="0" data-required="false" data-desc="节流调用的毫秒数。"></x-field>
<x-field data-name="options" data-type="Object" data-required="false" data-desc="选项对象。">
  <x-field data-name="leading" data-type="boolean" data-default="true" data-required="false" data-desc="指定在超时前沿调用。"></x-field>
  <x-field data-name="trailing" data-type="boolean" data-default="true" data-required="false" data-desc="指定在超时后沿调用。"></x-field>
</x-field>

### 返回值

<x-field data-name="throttled" data-type="Function" data-desc="返回新的节流函数，该函数具有 'cancel' 和 'flush' 方法。"></x-field>

### 示例

```javascript icon=logos:javascript
// 避免在滚动时过度更新位置。
jQuery(window).on('scroll', _.throttle(updatePosition, 100));

// 取消延迟的节流调用。
jQuery(window).on('popstate', throttled.cancel);
```

---

## wrap

创建一个函数，该函数将 `value` 作为第一个参数提供给 `wrapper`。任何额外的参数都会附加到提供给 `wrapper` 的参数之后。

### 参数

<x-field data-name="value" data-type="any" data-required="true" data-desc="要包装的值。"></x-field>
<x-field data-name="wrapper" data-type="Function" data-default="identity" data-required="false" data-desc="包装函数。"></x-field>

### 返回值

<x-field data-name="wrapped" data-type="Function" data-desc="返回新函数。"></x-field>

### 示例

```javascript icon=logos:javascript
var p = _.wrap(_.escape, function(func, text) {
  return '<p>' + func(text) + '</p>';
});

p('fred, barney, & pebbles');
// => '<p>fred, barney, &amp; pebbles</p>'
```

---

本节介绍了 Lodash 的核心函数工具。要探索其他工具类型，请继续阅读 [Lang](./api-lang.md) 部分，了解类型检查和克隆函数。
