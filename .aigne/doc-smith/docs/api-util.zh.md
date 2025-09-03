# 工具函数

关于 Lodash 其他工具函数的详细参考。

Util 类别提供了一系列通用的辅助函数，这些函数不适合归入像 Array 或 Object 这样更具体的类别。这些函数是用于创建复杂逻辑、处理回调、生成数据和控制函数执行流程的强大构建块。

如需查看所有可用函数的完整列表，请参阅主 [API 参考](./api.md)。

## 函数

### `_.attempt(func, ...args)`

尝试调用 `func`，返回结果或捕获的错误对象。任何额外的参数都会在调用时提供给 `func`。

**参数**

| Name | Type | Description |
|---|---|---|
| `func` | `Function` | 要尝试调用的函数。 |
| `...args` | `...*` | 用于调用 `func` 的参数。 |

**返回值**

- `(*)`: 返回 `func` 的结果或错误对象。

**示例**

```javascript
// 避免因选择器无效而抛出错误。
var elements = _.attempt(function(selector) {
  return document.querySelectorAll(selector);
}, '>_>');

if (_.isError(elements)) {
  elements = [];
}
// => elements 现在是一个空数组，而不是抛出错误。
```

---

### `_.bindAll(object, ...methodNames)`

将对象的方法绑定到对象本身，并覆盖现有的方法。这对于确保方法在作为回调函数使用时具有正确的 `this` 上下文非常有用。

**注意：** 此方法不会设置绑定函数的 "length" 属性。

**参数**

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | 要绑定并将绑定方法分配给的对象。 |
| `methodNames` | `...(string|string[])` | 要绑定的对象方法名。 |

**返回值**

- `(Object)`: 返回 `object`。

**示例**

```javascript
var view = {
  'label': 'docs',
  'click': function() {
    console.log('clicked ' + this.label);
  }
};

_.bindAll(view, ['click']);
// 现在，如果 view.click 被用作回调函数，'this' 将正确指向 view。
// 例如，在浏览器上下文中：
// element.addEventListener('click', view.click);
// 当元素被点击时，它将输出 'clicked docs'。
```

---

### `_.constant(value)`

创建一个返回给定 `value` 的函数。

**参数**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 新函数要返回的值。 |

**返回值**

- `(Function)`: 返回新的常量函数。

**示例**

```javascript
var objects = _.times(2, _.constant({ 'a': 1 }));

console.log(objects);
// => [{ 'a': 1 }, { 'a': 1 }]

console.log(objects[0] === objects[1]);
// => true，因为它返回的是对同一个对象的引用。
```

---

### `_.identity(value)`

此方法返回它接收的第一个参数。它通常用作默认的迭代器。

**参数**

| Name | Type | Description |
|---|---|---|
| `value` | `*` | 任何值。 |

**返回值**

- `(*)`: 返回 `value`。

**示例**

```javascript
var object = { 'a': 1 };

_.identity(object) === object;
// => true

// 在像 filter 或 map 这样的函数中可用作默认迭代器。
_.filter([0, 1, false, 2, '', 3], _.identity);
// => [1, 2, 3]
```

---

### `_.iteratee([func=_.identity])`

创建一个可用作许多 Lodash 方法的迭代器的函数。这是一种从不同值类型创建灵活回调函数的强大方法。

- 如果 `func` 是一个函数，则原样返回。
- 如果 `func` 是一个对象，则返回一个执行部分深度比较的函数（类似于 `_.matches`）。
- 如果 `func` 是一个数组，则返回一个对属性路径执行部分深度比较的函数（类似于 `_.matchesProperty`）。
- 如果 `func` 是一个字符串，则返回一个获取该路径属性值的函数（类似于 `_.property`）。

**参数**

| Name | Type | Description |
|---|---|---|
| `func` | `*` | 要转换成回调函数的值。默认为 `_.identity`。 |

**返回值**

- `(Function)`: 返回回调函数。

**示例**

```javascript
var users = [
  { 'user': 'barney', 'age': 36, 'active': true },
  { 'user': 'fred',   'age': 40, 'active': false }
];

// _.matches 的简写形式
_.filter(users, _.iteratee({ 'user': 'barney', 'active': true }));
// => [{ 'user': 'barney', 'age': 36, 'active': true }]

// _.matchesProperty 的简写形式
_.filter(users, _.iteratee(['user', 'fred']));
// => [{ 'user': 'fred', 'age': 40, 'active': false }]

// _.property 的简写形式
_.map(users, _.iteratee('user'));
// => ['barney', 'fred']
```

---

### `_.noop()`

此方法返回 `undefined`。当需要一个什么都不做的函数时，它可用作默认回调。

**示例**

```javascript
_.times(2, _.noop);
// => [undefined, undefined]

// 可用作可选回调的默认值
function process(data, callback) {
  const cb = callback || _.noop;
  // ... 处理数据
  cb();
}
```

---

### `_.property(path)`

创建一个函数，该函数返回给定对象在 `path` 路径上的值。

**参数**

| Name | Type | Description |
|---|---|---|
| `path` | `Array|string` | 要获取的属性路径。 |

**返回值**

- `(Function)`: 返回新的访问器函数。

**示例**

```javascript
var objects = [
  { 'a': { 'b': 2 } },
  { 'a': { 'b': 1 } }
];

_.map(objects, _.property('a.b'));
// => [2, 1]

_.map(_.sortBy(objects, _.property(['a', 'b'])), 'a.b');
// => [1, 2]
```

---

### `_.range(start, end, step)`

创建一个从 `start` 开始到（但不包括） `end` 的（正数和/或负数）数字数组。

**参数**

| Name | Type | Description |
|---|---|---|
| `start` | `number` | 范围的起始值。如果未指定 `end`，则默认为 `0`。 |
| `end` | `number` | 范围的结束值。 |
| `step` | `number` | 递增或递减的值。默认为 `1` 或 `-1`。 |

**返回值**

- `(Array)`: 返回数字范围的数组。

**示例**

```javascript
_.range(4);
// => [0, 1, 2, 3]

_.range(-4);
// => [0, -1, -2, -3]

_.range(1, 5);
// => [1, 2, 3, 4]

_.range(0, 20, 5);
// => [0, 5, 10, 15]
```

---

### `_.times(n, [iteratee=_.identity])`

调用 `iteratee` `n` 次，返回一个包含每次调用结果的数组。调用 `iteratee` 时会传入一个参数：`(index)`。

**参数**

| Name | Type | Description |
|---|---|---|
| `n` | `number` | 调用 `iteratee` 的次数。 |
| `iteratee` | `Function` | 每次迭代调用的函数。默认为 `_.identity`。 |

**返回值**

- `(Array)`: 返回结果数组。

**示例**

```javascript
_.times(3, String);
// => ['0', '1', '2']

_.times(4, _.constant(0));
// => [0, 0, 0, 0]
```

---

### `_.uniqueId([prefix=''])`

生成一个唯一的 ID。如果提供了 `prefix`，ID 将附加到它后面。

**参数**

| Name | Type | Description |
|---|---|---|
| `prefix` | `string` | 要为 ID 添加前缀的值。默认为空字符串。 |

**返回值**

- `(string)`: 返回唯一的 ID。

**示例**

```javascript
_.uniqueId('contact_');
// => 'contact_1'

_.uniqueId('contact_');
// => 'contact_2'

_.uniqueId();
// => '3'
```

---

本节概述了 Lodash 中的其他工具函数。这些工具是编写简洁且富有表现力的代码的基础。

如需执行更专业的任务，请考虑浏览 [Function](./api-function.md) 或 [Lang](./api-lang.md) API 部分。
