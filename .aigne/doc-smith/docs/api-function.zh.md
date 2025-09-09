# 函数

Lodash 提供了一套强大的实用工具集，用于操作和处理函数。这些辅助函数可以让你控制调用时机、更改函数签名，以及将简单的部分组合成复杂的逻辑。无论你是需要使用 `_.debounce` 和 `_.throttle` 来限制函数调用频率，使用 `_.partial` 创建偏函数，还是使用 `_.flow` 构建管道，这些实用工具都是编写简洁高效的 JavaScript 的必备工具。

本节为每个函数实用工具提供了详细的参考。有关有助于顺序方法链式调用的实用工具，请参阅 [Seq](./api-seq.md) 文档。

## 函数参考

| 函数 | 描述 |
|---|---|
| `_.after(n, func)` | 创建一个函数，当它被调用 `n` 次或更多次后，会调用 `func`。 |
| `_.ary(func, [n=func.length])` | 创建一个函数，该函数调用 `func` 时最多接受 `n` 个参数，并忽略任何额外的参数。 |
| `_.before(n, func)` | 创建一个函数，当它被调用少于 `n` 次时，会使用创建函数的 `this` 绑定和参数来调用 `func`。 |
| `_.bind(func, thisArg, [partials])` | 创建一个函数，该函数使用 `thisArg` 的 `this` 绑定和预设的 `partials` 参数来调用 `func`。 |
| `_.bindKey(object, key, [partials])` | 创建一个函数，该函数使用预设的 `partials` 参数来调用 `object[key]` 上的方法。 |
| `_.curry(func, [arity=func.length])` | 创建一个函数，该函数接受 `func` 的参数，如果已经提供了至少 `arity` 个参数，则调用 `func` 并返回其结果，否则返回一个接受 `func` 剩余参数的函数。 |
| `_.curryRight(func, [arity=func.length])` | 类似于 `_.curry`，但参数以 `_.partialRight` 的方式应用于 `func`。 |
| `_.debounce(func, [wait=0], [options={}])` | 创建一个防抖函数，该函数会从上一次被调用后，延迟 `wait` 毫秒后调用 `func`。 |
| `_.defer(func, [args])` | 延迟调用 `func`，直到当前调用栈清空为止。 |
| `_.delay(func, wait, [args])` | 在 `wait` 毫秒后调用 `func`。 |
| `_.flip(func)` | 创建一个函数，该函数以相反的参数顺序调用 `func`。 |
| `_.memoize(func, [resolver])` | 创建一个会记忆 `func` 结果的函数。 |
| `_.negate(predicate)` | 创建一个函数，该函数会否定谓词 `func` 的结果。 |
| `_.once(func)` | 创建一个仅能调用 `func` 一次的函数。 |
| `_.overArgs(func, [transforms])` | 创建一个函数，该函数会使用转换后的参数来调用 `func`。 |
| `_.partial(func, [partials])` | 创建一个函数，该函数使用预设的 `partials` 参数来调用 `func`。 |
| `_.partialRight(func, [partials])` | 类似于 `_.partial`，但预设的参数会附加到它接收的参数后面。 |
| `_.rearg(func, indexes)` | 创建一个函数，该函数会根据指定的 `indexes` 重新排列参数后调用 `func`。 |
| `_.rest(func, [start=func.length-1])` | 创建一个函数，该函数使用创建函数的 `this` 绑定来调用 `func`，并将从 `start` 位置开始的参数作为一个数组提供。 |
| `_.spread(func, [start=0])` | 创建一个函数，该函数使用一个参数数组来调用 `func`。 |
| `_.throttle(func, [wait=0], [options={}])` | 创建一个节流函数，在每 `wait` 毫秒内最多调用 `func` 一次。 |
| `_.unary(func)` | 创建一个最多接受一个参数的函数，并忽略任何额外的参数。 |
| `_.wrap(value, [wrapper=identity])` | 创建一个函数，该函数将 `value` 作为第一个参数提供给 `wrapper`。 |

---

### `_.after(n, func)`

创建一个函数，当它被调用 `n` 次或更多次后，会调用 `func`。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `n` | `number` | 在 `func` 被调用前需要调用的次数。 |
| `func` | `Function` | 要限制的函数。 |

**返回值**

- `(Function)`: 返回新的受限函数。

**示例**

```javascript 在多个事件后触发 icon=logos:javascript
var saves = ['profile', 'settings'];

var done = _.after(saves.length, function() {
  console.log('done saving!');
});

_.forEach(saves, function(type) {
  // 模拟异步保存
  setTimeout(done, 100);
});
// => 在两次异步保存完成后，打印 'done saving!'
```

---

### `_.ary(func, [n=func.length])`

创建一个函数，该函数调用 `func` 时最多接受 `n` 个参数，并忽略任何额外的参数。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `func` | `Function` | 要限制参数数量的函数。 |
| `[n=func.length]` | `number` | 参数数量上限。 |

**返回值**

- `(Function)`: 返回新的参数受限的函数。

**示例**

```javascript 限制迭代器的参数 icon=logos:javascript
_.map(['6', '8', '10'], _.ary(parseInt, 1));
// => [6, 8, 10]
```

---

### `_.before(n, func)`

创建一个函数，当它被调用少于 `n` 次时会调用 `func`。之后对创建函数的调用将返回最后一次 `func` 调用的结果。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `n` | `number` | `func` 不再被调用的调用次数。 |
| `func` | `Function` | 要限制的函数。 |

**返回值**

- `(Function)`: 返回新的受限函数。

**示例**

```javascript 限制事件处理程序的调用次数 icon=logos:javascript
// 假设 jQuery 可用
// jQuery(element).on('click', _.before(5, addContactToList));
// => 允许向列表中添加最多 4 个联系人。
```

---

### `_.debounce(func, [wait=0], [options={}])`

创建一个防抖函数，该函数会从上一次被调用后，延迟 `wait` 毫秒后调用 `func`。防抖函数提供一个 `cancel` 方法用于取消延迟的 `func` 调用，以及一个 `flush` 方法用于立即调用。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `func` | `Function` | 要防抖的函数。 |
| `[wait=0]` | `number` | 要延迟的毫秒数。 |
| `[options={}]` | `Object` | 选项对象。 |
| `[options.leading=false]` | `boolean` | 指定在超时前沿调用。 |
| `[options.maxWait]` | `number` | `func` 在被调用前被允许延迟的最长时间。 |
| `[options.trailing=true]` | `boolean` | 指定在超时后沿调用。 |

**返回值**

- `(Function)`: 返回新的防抖函数。

**示例**

```javascript 为调整大小处理程序添加防抖 icon=logos:javascript
// 假设 jQuery 可用
// 避免在窗口大小不断变化时进行高开销的计算。
// jQuery(window).on('resize', _.debounce(calculateLayout, 150));
```

---

### `_.throttle(func, [wait=0], [options={}])`

创建一个节流函数，在每 `wait` 毫秒内最多调用 `func` 一次。节流函数提供一个 `cancel` 方法用于取消延迟的 `func` 调用，以及一个 `flush` 方法用于立即调用。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `func` | `Function` | 要节流的函数。 |
| `[wait=0]` | `number` | 节流调用的毫秒数。 |
| `[options={}]` | `Object` | 选项对象。 |
| `[options.leading=true]` | `boolean` | 指定在超时前沿调用。 |
| `[options.trailing=true]` | `boolean` | 指定在超时后沿调用。 |

**返回值**

- `(Function)`: 返回新的节流函数。

**示例**

```javascript 为滚动处理程序添加节流 icon=logos:javascript
// 假设 jQuery 可用
// 避免在滚动时过度更新位置。
// jQuery(window).on('scroll', _.throttle(updatePosition, 100));
```

---

### `_.memoize(func, [resolver])`

创建一个会记忆 `func` 结果的函数。如果提供了 `resolver`，它将根据参数决定用于存储结果的缓存键。默认情况下，第一个参数用作缓存键。缓存作为记忆化函数的 `cache` 属性暴露出来。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `func` | `Function` | 要将其输出记忆化的函数。 |
| `[resolver]` | `Function` | 用于解析缓存键的函数。 |

**返回值**

- `(Function)`: 返回新的记忆化函数。

**示例**

```javascript 记忆化一个函数 icon=logos:javascript
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

你现在已经了解了 Lodash 中的核心函数实用工具。这些工具是管理异步操作、创建可复用的函数配置以及构建健壮应用程序的基础。要继续学习，可以浏览 [Util](./api-util.md) 部分的其他实用工具，或深入研究 [Lang](./api-lang.md) 部分的语言级别辅助函数。
