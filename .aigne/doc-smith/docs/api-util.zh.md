# 工具函数

“工具函数”类别提供了一系列杂项实用函数，为常见的编程任务提供了强大、可重用的逻辑。这些函数的范围涵盖创建回调函数和组合函数，到生成唯一 ID 和处理默认值。它们是编写更简洁、更具声明性代码的重要工具。

---

### _.attempt(func, ...args)

尝试调用 `func`，返回结果或捕获到的错误对象。调用 `func` 时，会传入任何额外的参数。

**Since**
3.0.0

**Arguments**

| Param    | Type     | Description                    |
| :------- | :------- | :----------------------------- |
| `func`   | `Function` | 尝试调用的函数。       |
| `[args]` | `...*`   | 调用 `func` 时传入的参数。 |

**Returns**

`(*)`: 返回 `func` 的结果或错误对象。

**Example**

```javascript
// 避免因选择器无效而抛出错误。
var elements = _.attempt(function(selector) {
  return document.querySelectorAll(selector);
}, '>_>');

if (_.isError(elements)) {
  elements = [];
}
```

---

### _.bindAll(object, methodNames)

将一个对象的方法绑定到该对象本身，并覆盖现有方法。

**Note:** 此方法不会设置绑定函数的“length”属性。

**Since**
0.1.0

**Arguments**

| Param         | Type                | Description                           |
| :------------ | :------------------ | :------------------------------------ |
| `object`      | `Object`            | 要绑定方法的对象。        |
| `methodNames` | `...(string|string[])` | 要绑定的对象方法名。      |

**Returns**

`(Object)`: 返回 `object`。

**Example**

```javascript
var view = {
  'label': 'docs',
  'click': function() {
    console.log('clicked ' + this.label);
  }
};

_.bindAll(view, ['click']);
jQuery(element).on('click', view.click);
// => 点击时输出 'clicked docs'
```

---

### _.constant(value)

创建一个返回 `value` 的函数。

**Since**
2.4.0

**Arguments**

| Param   | Type | Description                            |
| :------ | :--- | :------------------------------------- |
| `value` | `*`  | 新函数要返回的值。 |

**Returns**

`(Function)`: 返回新的常量函数。

**Example**

```javascript
var objects = _.times(2, _.constant({ 'a': 1 }));

console.log(objects);
// => [{ 'a': 1 }, { 'a': 1 }]

console.log(objects[0] === objects[1]);
// => true
```

---

### _.defaultTo(value, defaultValue)

检查 `value`，以确定是否应返回一个默认值。如果 `value` 是 `NaN`、`null` 或 `undefined`，则返回 `defaultValue`。

**Since**
4.14.0

**Arguments**

| Param          | Type | Description           |
| :------------- | :--- | :-------------------- |
| `value`        | `*`  | 要检查的值。   |
| `defaultValue` | `*`  | 默认值。    |

**Returns**

`(*)`: 返回解析后的值。

**Example**

```javascript
_.defaultTo(1, 10);
// => 1

_.defaultTo(undefined, 10);
// => 10
```

---

### _.identity(value)

此方法返回其接收的第一个参数。

**Since**
0.1.0

**Arguments**

| Param   | Type | Description |
| :------ | :--- | :---------- |
| `value` | `*`  | 任意值。  |

**Returns**

`(*)`: 返回 `value`。

**Example**

```javascript
var object = { 'a': 1 };

console.log(_.identity(object) === object);
// => true
```

---

### _.iteratee([func=_.identity])

创建一个函数，该函数会用其自身的参数来调用 `func`。如果 `func` 是一个属性名，所创建的函数会返回给定元素的属性值。如果 `func` 是一个数组或对象，所创建的函数会对包含等效源属性的元素返回 `true`，否则返回 `false`。

**Since**
4.0.0

**Arguments**

| Param  | Type | Description                      |
| :----- | :--- | :------------------------------- |
| `func` | `*`  | 要转换成回调函数的值。 |

**Returns**

`(Function)`: 返回回调函数。

**Example**

```javascript
var users = [
  { 'user': 'barney', 'age': 36, 'active': true },
  { 'user': 'fred',   'age': 40, 'active': false }
];

// _.matches 的迭代器简写。
_.filter(users, _.iteratee({ 'user': 'barney', 'active': true }));
// => [{ 'user': 'barney', 'age': 36, 'active': true }]

// _.matchesProperty 的迭代器简写。
_.filter(users, _.iteratee(['user', 'fred']));
// => [{ 'user': 'fred', 'age': 40 }]

// _.property 的迭代器简写。
_.map(users, _.iteratee('user'));
// => ['barney', 'fred']
```

---

### _.matches(source)

创建一个函数，该函数对给定对象和 `source` 对象进行部分深度比较，如果给定对象拥有相等的属性值，则返回 `true`，否则返回 `false`。

**Since**
3.0.0

**Arguments**

| Param    | Type   | Description                         |
| :------- | :----- | :---------------------------------- |
| `source` | `Object` | 要匹配的属性值对象。 |

**Returns**

`(Function)`: 返回新的规范函数。

**Example**

```javascript
var objects = [
  { 'a': 1, 'b': 2, 'c': 3 },
  { 'a': 4, 'b': 5, 'c': 6 }
];

_.filter(objects, _.matches({ 'a': 4, 'c': 6 }));
// => [{ 'a': 4, 'b': 5, 'c': 6 }]
```

---

### _.matchesProperty(path, srcValue)

创建一个函数，该函数对给定对象的 `path` 路径上的值与 `srcValue` 进行部分深度比较，如果对象值相等，则返回 `true`，否则返回 `false`。

**Since**
3.2.0

**Arguments**

| Param      | Type          | Description                   |
| :--------- | :------------ | :---------------------------- |
| `path`     | `Array|string`  | 要获取的属性路径。 |
| `srcValue` | `*`           | 要匹配的值。           |

**Returns**

`(Function)`: 返回新的规范函数。

**Example**

```javascript
var objects = [
  { 'a': 1, 'b': 2, 'c': 3 },
  { 'a': 4, 'b': 5, 'c': 6 }
];

_.find(objects, _.matchesProperty('a', 4));
// => { 'a': 4, 'b': 5, 'c': 6 }
```

---

### _.method(path, ...args)

创建一个函数，该函数调用给定对象在 `path` 路径上的方法。任何额外的参数都会在调用时传给该方法。

**Since**
3.7.0

**Arguments**

| Param    | Type          | Description                         |
| :------- | :------------ | :---------------------------------- |
| `path`   | `Array|string`  | 要调用的方法的路径。   |
| `[args]` | `...*`        | 调用方法时传入的参数。 |

**Returns**

`(Function)`: 返回新的调用函数。

**Example**

```javascript
var objects = [
  { 'a': { 'b': _.constant(2) } },
  { 'a': { 'b': _.constant(1) } }
];

_.map(objects, _.method('a.b'));
// => [2, 1]

_.map(objects, _.method(['a', 'b']));
// => [2, 1]
```

---

### _.noop()

此方法返回 `undefined`。

**Since**
2.3.0

**Example**

```javascript
_.times(2, _.noop);
// => [undefined, undefined]
```

---

### _.property(path)

创建一个函数，该函数返回给定对象在 `path` 路径上的值。

**Since**
2.4.0

**Arguments**

| Param  | Type          | Description                   |
| :----- | :------------ | :---------------------------- |
| `path` | `Array|string`  | 要获取的属性路径。 |

**Returns**

`(Function)`: 返回新的访问器函数。

**Example**

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

### _.range([start=0], end, [step=1])

创建一个从 `start` 开始但不包含 `end` 的数字（正数和/或负数）递进数组。

**Since**
0.1.0

**Arguments**

| Param   | Type   | Description                         |
| :------ | :----- | :---------------------------------- |
| `start` | `number` | 范围的起始值。             |
| `end`   | `number` | 范围的结束值。               |
| `step`  | `number` | 递增或递减的值。 |

**Returns**

`(Array)`: 返回数字范围数组。

**Example**

```javascript
_.range(4);
// => [0, 1, 2, 3]

_.range(-4);
// => [0, -1, -2, -3]

_.range(1, 5);
// => [1, 2, 3, 4]
```

---

### _.times(n, [iteratee=_.identity])

调用迭代器 `n` 次，返回一个包含每次调用结果的数组。迭代器会传入一个参数：(index)。

**Since**
0.1.0

**Arguments**

| Param      | Type     | Description                      |
| :--------- | :------- | :------------------------------- |
| `n`        | `number` | `iteratee` 的调用次数。 |
| `iteratee` | `Function` | 每次迭代调用的函数。 |

**Returns**

`(Array)`: 返回结果数组。

**Example**

```javascript
_.times(3, String);
// => ['0', '1', '2']

_.times(4, _.constant(0));
// => [0, 0, 0, 0]
```

---

### _.uniqueId([prefix=''])

生成一个唯一的 ID。如果提供了 `prefix`，该 ID 会附加在 `prefix` 后面。

**Since**
0.1.0

**Arguments**

| Param    | Type   | Description                   |
| :------- | :----- | :---------------------------- |
| `prefix` | `string` | ID 的前缀值。 |

**Returns**

`(string)`: 返回唯一的 ID。

**Example**

```javascript
_.uniqueId('contact_');
// => 'contact_104'

_.uniqueId();
// => '105'
```

---

Lodash 的杂项工具函数参考到此结束。要浏览其他类别，您可以返回主 [API 参考](./api.md)。