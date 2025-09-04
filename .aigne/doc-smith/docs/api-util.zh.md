# 工具函数

Lodash 其他工具函数的详细参考。这些函数提供了广泛的辅助功能，从创建新函数、控制调用，到生成唯一 ID 和管理函数上下文。

---

## _.attempt(func, [...args])

尝试调用 `func`，返回结果或捕获到的错误对象。任何附加的参数都会在调用 `func` 时提供给它。

**Since**: 3.0.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
| `func` | `Function` | 要尝试调用的函数。 |
| `[...args]` | `...*` | 调用 `func` 时使用的参数。 |

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

## _.bindAll(object, methodNames)

将对象的方法绑定到该对象自身，并覆盖现有的方法。

**注意**：此方法不会为绑定的函数设置 "length" 属性。

**Since**: 0.1.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
| `object` | `Object` | 要绑定并将绑定后的方法赋值给的对象。 |
| `methodNames` | `...(string|string[])` | 要绑定的对象方法名。 |

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
// => 点击时输出 'clicked docs'。
```

---

## _.cond(pairs)

创建一个函数，该函数遍历 `pairs` 并调用第一个返回真值的断言函数所对应的函数。断言函数和对应的函数在调用时，会传入所创建函数的 `this` 绑定和参数。

**Since**: 4.0.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
| `pairs` | `Array` | 断言函数与对应函数的配对。 |

**Returns**

`(Function)`: 返回新的复合函数。

**Example**

```javascript
var func = _.cond([
  [_.matches({ 'a': 1 }),           _.constant('matches A')],
  [_.conforms({ 'b': _.isNumber }), _.constant('matches B')],
  [_.stubTrue,                      _.constant('no match')]
]);

func({ 'a': 1, 'b': 2 });
// => 'matches A'

func({ 'a': 0, 'b': 1 });
// => 'matches B'

func({ 'a': '1', 'b': '2' });
// => 'no match'
```

---

## _.conforms(source)

创建一个函数，该函数会用给定对象的相应属性值来调用 `source` 对象中的断言函数。如果所有断言函数都返回真值，则该函数返回 `true`，否则返回 `false`。

**注意**：创建的函数等同于 `_.conformsTo`，且 `source` 已被部分应用。

**Since**: 4.0.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
| `source` | `Object` | 包含属性断言函数的对象，用于检查一致性。 |

**Returns**

`(Function)`: 返回新的规范函数。

**Example**

```javascript
var objects = [
  { 'a': 2, 'b': 1 },
  { 'a': 1, 'b': 2 }
];

_.filter(objects, _.conforms({ 'b': function(n) { return n > 1; } }));
// => [{ 'a': 1, 'b': 2 }]
```

---

## _.constant(value)

创建一个返回 `value` 的函数。

**Since**: 2.4.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
| `value` | `*` | 新函数要返回的值。 |

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

## _.defaultTo(value, defaultValue)

检查 `value`，以确定是否应返回默认值来代替它。如果 `value` 是 `NaN`、`null` 或 `undefined`，则返回 `defaultValue`。

**Since**: 4.14.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
| `value` | `*` | 要检查的值。 |
| `defaultValue` | `*` | 默认值。 |

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

## _.flow([...funcs])

创建一个函数，该函数返回从左到右调用给定函数的结果。每次后续调用都会传入前一次调用的返回值。

**Since**: 3.0.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
| `[...funcs]` | `...(Function|Function[])` | 要调用的函数。 |

**Returns**

`(Function)`: 返回新的复合函数。

**See Also**: `_.flowRight`

**Example**

```javascript
function square(n) {
  return n * n;
}

var addSquare = _.flow([_.add, square]);
addSquare(1, 2);
// => 9
```

---

## _.flowRight([...funcs])

此方法类似于 `_.flow`，不同之处在于它创建的函数会从右到左调用给定的函数。

**Since**: 3.0.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
| `[...funcs]` | `...(Function|Function[])` | 要调用的函数。 |

**Returns**

`(Function)`: 返回新的复合函数。

**See Also**: `_.flow`

**Example**

```javascript
function square(n) {
  return n * n;
}

var addSquare = _.flowRight([square, _.add]);
addSquare(1, 2);
// => 9
```

---

## _.identity(value)

此方法返回其接收的第一个参数。

**Since**: 0.1.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
| `value` | `*` | 任何值。 |

**Returns**

`(*)`: 返回 `value`。

**Example**

```javascript
var object = { 'a': 1 };

console.log(_.identity(object) === object);
// => true
```

---

## _.iteratee([func=_.identity])

创建一个函数，该函数使用所创建函数的参数来调用 `func`。如果 `func` 是属性名，则创建的函数会返回给定元素的属性值。如果 `func` 是一个数组或对象，则创建的函数会对包含等效源属性的元素返回 `true`，否则返回 `false`。

**Since**: 4.0.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
| `[func=_.identity]` | `*` | 要转换为回调函数的值。 |

**Returns**

`(Function)`: 返回回调函数。

**Example**

```javascript
var users = [
  { 'user': 'barney', 'age': 36, 'active': true },
  { 'user': 'fred',   'age': 40, 'active': false }
];

// `_.matches` 迭代器的简写形式。
_.filter(users, _.iteratee({ 'user': 'barney', 'active': true }));
// => [{ 'user': 'barney', 'age': 36, 'active': true }]

// `_.matchesProperty` 迭代器的简写形式。
_.filter(users, _.iteratee(['user', 'fred']));
// => [{ 'user': 'fred', 'age': 40 }]

// `_.property` 迭代器的简写形式。
_.map(users, _.iteratee('user'));
// => ['barney', 'fred']
```

---

## _.matches(source)

创建一个函数，该函数在给定对象和 `source` 之间执行部分深度比较，如果给定对象具有等效的属性值，则返回 `true`，否则返回 `false`。

**Since**: 3.0.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
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

## _.matchesProperty(path, srcValue)

创建一个函数，该函数对给定对象的 `path` 路径上的值与 `srcValue` 进行部分深度比较，如果对象值等效，则返回 `true`，否则返回 `false`。

**Since**: 3.2.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
| `path` | `Array|string` | 要获取的属性路径。 |
| `srcValue` | `*` | 要匹配的值。 |

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

## _.method(path, [...args])

创建一个函数，该函数调用给定对象的 `path` 路径上的方法。任何附加的参数都会提供给被调用的方法。

**Since**: 3.7.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
| `path` | `Array|string` | 要调用的方法的路径。 |
| `[...args]` | `...*` | 调用该方法时使用的参数。 |

**Returns**

`(Function)`: 返回新的调用器函数。

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

## _.methodOf(object, [...args])

与 `_.method` 相反；此方法创建一个函数，该函数调用 `object` 上给定路径的方法。任何附加的参数都会提供给被调用的方法。

**Since**: 3.7.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
| `object` | `Object` | 要查询的对象。 |
| `[...args]` | `...*` | 调用该方法时使用的参数。 |

**Returns**

`(Function)`: 返回新的调用器函数。

**Example**

```javascript
var array = _.times(3, _.constant),
    object = { 'a': array, 'b': array, 'c': array };

_.map(['a[2]', 'c[0]'], _.methodOf(object));
// => [2, 0]

_.map([['a', '2'], ['c', '0']], _.methodOf(object));
// => [2, 0]
```

---

## _.mixin([object=lodash], source, [options={}])

将源对象所有可枚举的字符串键函数属性添加到目标对象。如果 `object` 是一个函数，则方法也会被添加到其原型上。

**Since**: 0.1.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
| `[object=lodash]` | `Function|Object` | 目标对象。 |
| `source` | `Object` | 要添加的函数对象。 |
| `[options={}]` | `Object` | 选项对象。 |
| `[options.chain=true]` | `boolean` | 指定 mixin 是否可链式调用。 |

**Returns**

`(Function|Object)`: 返回 `object`。

**Example**

```javascript
function vowels(string) {
  return _.filter(string, function(v) {
    return /[aeiou]/i.test(v);
  });
}

_.mixin({ 'vowels': vowels });
_.vowels('fred');
// => ['e']

_('fred').vowels().value();
// => ['e']
```

---

## _.noConflict()

将 `_` 变量恢复为其先前的值，并返回对 `lodash` 函数的引用。

**Since**: 0.1.0

**Returns**

`(Function)`: 返回 `lodash` 函数。

**Example**

```javascript
var lodash = _.noConflict();
```

---

## _.noop()

此方法返回 `undefined`。

**Since**: 2.3.0

**Example**

```javascript
_.times(2, _.noop);
// => [undefined, undefined]
```

---

## _.nthArg([n=0])

创建一个函数，该函数获取索引为 `n` 的参数。如果 `n` 是负数，则返回从末尾开始的第 n 个参数。

**Since**: 4.0.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
| `[n=0]` | `number` | 要返回的参数的索引。 |

**Returns**

`(Function)`: 返回新的传递函数。

**Example**

```javascript
var func = _.nthArg(1);
func('a', 'b', 'c', 'd');
// => 'b'

var func = _.nthArg(-2);
func('a', 'b', 'c', 'd');
// => 'c'
```

---

## _.over([...iteratees=[_.identity]])

创建一个函数，该函数使用其接收到的参数调用 `iteratees`，并返回它们的结果。

**Since**: 4.0.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
| `[...iteratees=[_.identity]]` | `...(Function|Function[])` | 要调用的迭代函数。 |

**Returns**

`(Function)`: 返回新的函数。

**Example**

```javascript
var func = _.over([Math.max, Math.min]);

func(1, 2, 3, 4);
// => [4, 1]
```

---

## _.overEvery([...predicates=[_.identity]])

创建一个函数，该函数检查在使用其接收到的参数调用时，是否**所有**的 `predicates` 都返回真值。

**Since**: 4.0.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
| `[...predicates=[_.identity]]` | `...(Function|Function[])` | 要检查的断言函数。 |

**Returns**

`(Function)`: 返回新的函数。

**Example**

```javascript
var func = _.overEvery([Boolean, isFinite]);

func('1');
// => true

func(null);
// => false

func(NaN);
// => false
```

---

## _.overSome([...predicates=[_.identity]])

创建一个函数，该函数检查在使用其接收到的参数调用时，是否有**任何**一个 `predicates` 返回真值。

**Since**: 4.0.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
| `[...predicates=[_.identity]]` | `...(Function|Function[])` | 要检查的断言函数。 |

**Returns**

`(Function)`: 返回新的函数。

**Example**

```javascript
var func = _.overSome([Boolean, isFinite]);

func('1');
// => true

func(null);
// => true

func(NaN);
// => false
```

---

## _.property(path)

创建一个函数，该函数返回给定对象的 `path` 路径上的值。

**Since**: 2.4.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
| `path` | `Array|string` | 要获取的属性路径。 |

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

## _.propertyOf(object)

与 `_.property` 相反；此方法创建一个函数，该函数返回 `object` 上给定路径的值。

**Since**: 3.0.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
| `object` | `Object` | 要查询的对象。 |

**Returns**

`(Function)`: 返回新的访问器函数。

**Example**

```javascript
var array = [0, 1, 2],
    object = { 'a': array, 'b': array, 'c': array };

_.map(['a[2]', 'c[0]'], _.propertyOf(object));
// => [2, 0]

_.map([['a', '2'], ['c', '0']], _.propertyOf(object));
// => [2, 0]
```

---

## _.range([start=0], end, [step=1])

创建一个从 `start` 开始到（但不包括）`end` 的数字数组。

**Since**: 0.1.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
| `[start=0]` | `number` | 范围的起始值。 |
| `end` | `number` | 范围的结束值。 |
| `[step=1]` | `number` | 递增或递减的值。 |

**Returns**

`(Array)`: 返回数字范围数组。

**See Also**: `_.rangeRight`

**Example**

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

## _.rangeRight([start=0], end, [step=1])

此方法类似于 `_.range`，不同之处在于它以降序填充值。

**Since**: 4.0.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
| `[start=0]` | `number` | 范围的起始值。 |
| `end` | `number` | 范围的结束值。 |
| `[step=1]` | `number` | 递增或递减的值。 |

**Returns**

`(Array)`: 返回数字范围数组。

**See Also**: `_.range`

**Example**

```javascript
_.rangeRight(4);
// => [3, 2, 1, 0]

_.rangeRight(1, 5);
// => [4, 3, 2, 1]
```

---

## _.runInContext([context=root])

使用 `context` 对象创建一个新的、纯净的 `lodash` 函数。

**Since**: 1.1.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
| `[context=root]` | `Object` | 上下文对象。 |

**Returns**

`(Function)`: 返回一个新的 `lodash` 函数。

**Example**

```javascript
_.mixin({ 'foo': _.constant('foo') });

var lodash = _.runInContext();
lodash.mixin({ 'bar': lodash.constant('bar') });

_.isFunction(_.bar);
// => false

lodash.isFunction(lodash.bar);
// => true
```

---

## 存根函数

这些函数返回一个常量值，可用作默认的迭代函数。

| Function | Return Value | Since |
| --- | --- | --- |
| `_.stubArray()` | `[]` (一个新的空数组) | 4.13.0 |
| `_.stubFalse()` | `false` | 4.13.0 |
| `_.stubObject()` | `{}` (一个新的空对象) | 4.13.0 |
| `_.stubString()` | `''` (一个空字符串) | 4.13.0 |
| `_.stubTrue()` | `true` | 4.13.0 |

**Example**

```javascript
var objects = _.times(2, _.stubObject);

console.log(objects);
// => [{}, {}]

console.log(objects[0] === objects[1]);
// => false
```

---

## _.times(n, [iteratee=_.identity])

调用迭代函数 `n` 次，返回一个包含每次调用结果的数组。迭代函数调用时会传入一个参数：(index)。

**Since**: 0.1.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
| `n` | `number` | 调用 `iteratee` 的次数。 |
| `[iteratee=_.identity]` | `Function` | 每次迭代调用的函数。 |

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

## _.toPath(value)

将 `value` 转换为属性路径数组。

**Since**: 4.0.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
| `value` | `*` | 要转换的值。 |

**Returns**

`(Array)`: 返回新的属性路径数组。

**Example**

```javascript
_.toPath('a.b.c');
// => ['a', 'b', 'c']

_.toPath('a[0].b.c');
// => ['a', '0', 'b', 'c']
```

---

## _.uniqueId([prefix=''])

生成一个唯一的 ID。如果提供了 `prefix`，ID 会附加到它后面。

**Since**: 0.1.0

**Arguments**

| Param | Type | Description |
| --- | --- | --- |
| `[prefix='']` | `string` | 用于作为 ID 前缀的值。 |

**Returns**

`(string)`: 返回唯一的 ID。

**Example**

```javascript
_.uniqueId('contact_');
// => 'contact_104'

_.uniqueId();
// => '105'
```
