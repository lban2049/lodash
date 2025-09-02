# Util

本部分提供了 Lodash 中各种实用工具函数的详细参考，这些函数提供了创建函数、处理函数参数以及执行其他元编程任务的基础功能。

## 函数列表

| 函数 | 描述 |
| --- | --- |
| [_.attempt](#_attemptfunc-args) | 尝试调用一个函数，返回其结果或捕获到的错误对象。 |
| [_.bindAll](#_bindallobject-methodnames) | 将一个对象的方法绑定到该对象本身，覆盖现有方法。 |
| [_.cond](#_condpairs) | 创建一个函数，该函数遍历一系列的断言-函数对，并执行第一个返回真值的断言对应的函数。 |
| [_.conforms](#_conformssource) | 创建一个函数，该函数通过调用 `source` 的断言属性来检查给定对象是否符合 `source` 的结构。 |
| [_.constant](#_constantvalue) | 创建一个返回给定值的函数。 |
| [_.defaultTo](#_defaulttovalue-defaultvalue) | 检查一个值，如果它是 `NaN`、`null` 或 `undefined`，则返回默认值。 |
| [_.flow](#_flowfuncs) | 创建一个函数，该函数返回调用给定函数序列的结果，其中每个函数的返回值作为下一个函数的参数。 |
| [_.flowRight](#_flowrightfuncs) | 类似于 `_.flow`，但从右向左调用函数。 |
| [_.identity](#_identityvalue) | 返回接收到的第一个参数。 |
| [_.iteratee](#_iterateefunc) | 将一个值转换成一个可以在 Lodash 中使用的迭代器函数。 |
| [_.matches](#_matchessource) | 创建一个执行部分深比较的函数，以确定给定对象是否包含等效的属性值。 |
| [_.matchesProperty](#_matchespropertypath-srcvalue) | 创建一个函数，该函数对给定对象的 `path` 处的值与 `srcValue` 进行部分深比较。 |
| [_.method](#_methodpath-args) | 创建一个调用给定对象 `path` 处方法的函数。 |
| [_.methodOf](#_methodofobject-args) | `_.method` 的反向版本；创建一个函数，该函数调用给定路径上 `object` 的方法。 |
| [_.mixin](#_mixinobject-source-options) | 将源对象的所有可枚举函数属性添加到目标对象。 |
| [_.noConflict](#_noconflict) | 恢复 `_` 变量到其先前的值，并返回对 `lodash` 函数的引用。 |
| [_.noop](#_noop) | 一个什么都不做的函数，返回 `undefined`。 |
| [_.nthArg](#_nthargn) | 创建一个返回第 n 个参数的函数。 |
| [_.over](#_overiteratees) | 创建一个函数，该函数使用接收到的参数调用每个迭代器并返回结果数组。 |
| [_.overEvery](#_overeverypredicates) | 创建一个函数，该函数检查所有断言在被调用时是否都返回真值。 |
| [_.overSome](#_oversomepredicates) | 创建一个函数，该函数检查是否有任何断言在被调用时返回真值。 |
| [_.property](#_propertypath) | 创建一个返回给定对象 `path` 处值的函数。 |
| [_.propertyOf](#_propertyofobject) | `_.property` 的反向版本；创建一个返回 `object` 给定路径处值的函数。 |
| [_.range](#_rangestart-end-step) | 创建一个数字范围的数组。 |
| [_.rangeRight](#_rangerightstart-end-step) | 类似于 `_.range`，但以递减顺序填充值。 |
| [_.runInContext](#_runincontextcontext) | 使用 `context` 对象创建一个新的纯净 `lodash` 函数。 |
| [_.stubArray](#_stubarray) | 返回一个新的空数组。 |
| [_.stubFalse](#_stubfalse) | 返回 `false`。 |
| [_.stubObject](#_stubobject) | 返回一个新的空对象。 |
| [_.stubString](#_stubstring) | 返回一个空字符串。 |
| [_.stubTrue](#_stubtrue) | 返回 `true`。 |
| [_.times](#_timesn-iteratee) | 调用一个迭代器 n 次，返回一个由每次调用的结果组成的数组。 |
| [_.toPath](#_topathvalue) | 将一个值转换为属性路径数组。 |
| [_.uniqueId](#_uniqueidprefix) | 生成一个唯一的 ID。 |

---

### _.attempt(func, [...args])

尝试调用 `func`，返回结果或捕获到的错误对象。任何附加的参数都会在调用时提供给 `func`。

**从 `3.0.0` 版本开始**

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `func` | `Function` | 要尝试调用的函数。 |
| `[...args]` | `*` | 调用 `func` 的参数。 |

**返回**

`(*)`: 返回 `func` 的结果或错误对象。

**示例**

```javascript
// 避免因无效选择器而抛出错误。
var elements = _.attempt(function(selector) {
  return document.querySelectorAll(selector);
}, '>_>');

if (_.isError(elements)) {
  elements = [];
}
```

### _.bindAll(object, methodNames)

将一个对象的方法绑定到该对象本身，覆盖现有方法。

**注意：** 此方法不设置绑定函数的 "length" 属性。

**从 `0.1.0` 版本开始**

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `object` | `Object` | 要绑定并分配绑定方法的对象。 |
| `methodNames` | `...(string|string[])` | 要绑定的对象方法名。 |

**返回**

`(Object)`: 返回 `object`。

**示例**

```javascript
var view = {
  'label': 'docs',
  'click': function() {
    console.log('clicked ' + this.label);
  }
};

_.bindAll(view, ['click']);
jQuery(element).on('click', view.click);
// => 点击时记录 'clicked docs'。
```

### _.cond(pairs)

创建一个函数，该函数遍历 `pairs`（谓词-函数对），并调用第一个返回真值的谓词对应的函数。谓词-函数对以创建函数的 `this` 绑定和参数进行调用。

**从 `4.0.0` 版本开始**

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `pairs` | `Array` | 谓词-函数对。 |

**返回**

`(Function)`: 返回新的复合函数。

**示例**

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

### _.conforms(source)

创建一个函数，该函数调用 `source` 的谓词属性，并使用给定对象的相应属性值。如果所有谓词都返回真值，则返回 `true`，否则返回 `false`。

**从 `4.0.0` 版本开始**

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `source` | `Object` | 要符合的属性谓词对象。 |

**返回**

`(Function)`: 返回新的规范函数。

**示例**

```javascript
var objects = [
  { 'a': 2, 'b': 1 },
  { 'a': 1, 'b': 2 }
];

_.filter(objects, _.conforms({ 'b': function(n) { return n > 1; } }));
// => [{ 'a': 1, 'b': 2 }]
```

### _.constant(value)

创建一个返回 `value` 的函数。

**从 `2.4.0` 版本开始**

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 新函数要返回的值。 |

**返回**

`(Function)`: 返回新的常量函数。

**示例**

```javascript
var objects = _.times(2, _.constant({ 'a': 1 }));

console.log(objects);
// => [{ 'a': 1 }, { 'a': 1 }]

console.log(objects[0] === objects[1]);
// => true
```

### _.defaultTo(value, defaultValue)

检查 `value` 以确定是否应返回默认值。如果 `value` 为 `NaN`、`null` 或 `undefined`，则返回 `defaultValue`。

**从 `4.14.0` 版本开始**

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要检查的值。 |
| `defaultValue` | `*` | 默认值。 |

**返回**

`(*)`: 返回解析后的值。

**示例**

```javascript
_.defaultTo(1, 10);
// => 1

_.defaultTo(undefined, 10);
// => 10
```

### _.flow([...funcs])

创建一个函数，该函数返回调用给定函数序列的结果，其中每个后续调用都提供前一个的返回值。

**从 `3.0.0` 版本开始**

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `[...funcs]` | `...(Function|Function[])` | 要调用的函数。 |

**返回**

`(Function)`: 返回新的复合函数。

**示例**

```javascript
function square(n) {
  return n * n;
}

var addSquare = _.flow([_.add, square]);
addSquare(1, 2);
// => 9
```

### _.flowRight([...funcs])

此方法类似于 `_.flow`，但它创建的函数从右到左调用给定的函数。

**从 `3.0.0` 版本开始**

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `[...funcs]` | `...(Function|Function[])` | 要调用的函数。 |

**返回**

`(Function)`: 返回新的复合函数。

**示例**

```javascript
function square(n) {
  return n * n;
}

var addSquare = _.flowRight([square, _.add]);
addSquare(1, 2);
// => 9
```

### _.identity(value)

此方法返回它接收的第一个参数。

**从 `0.1.0` 版本开始**

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 任何值。 |

**返回**

`(*)`: 返回 `value`。

**示例**

```javascript
var object = { 'a': 1 };

console.log(_.identity(object) === object);
// => true
```

### _.iteratee([func=_.identity])

创建一个函数，该函数使用创建函数的参数调用 `func`。如果 `func` 是一个属性名，创建的函数将返回给定元素的属性值。如果 `func` 是一个数组或对象，创建的函数对于包含等效源属性的元素返回 `true`，否则返回 `false`。

**从 `4.0.0` 版本开始**

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `[func=_.identity]` | `*` | 要转换为回调的值。 |

**返回**

`(Function)`: 返回回调函数。

**示例**

```javascript
var users = [
  { 'user': 'barney', 'age': 36, 'active': true },
  { 'user': 'fred',   'age': 40, 'active': false }
];

// The `_.matches` iteratee shorthand.
_.filter(users, _.iteratee({ 'user': 'barney', 'active': true }));
// => [{ 'user': 'barney', 'age': 36, 'active': true }]
```

### _.matches(source)

创建一个函数，该函数在给定对象和 `source` 之间执行部分深比较，如果给定对象具有等效的属性值，则返回 `true`，否则返回 `false`。

**从 `3.0.0` 版本开始**

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `source` | `Object` | 要匹配的属性值对象。 |

**返回**

`(Function)`: 返回新的规范函数。

**示例**

```javascript
var objects = [
  { 'a': 1, 'b': 2, 'c': 3 },
  { 'a': 4, 'b': 5, 'c': 6 }
];

_.filter(objects, _.matches({ 'a': 4, 'c': 6 }));
// => [{ 'a': 4, 'b': 5, 'c': 6 }]
```

### _.matchesProperty(path, srcValue)

创建一个函数，该函数在给定对象的 `path` 处的值与 `srcValue` 之间执行部分深比较，如果对象值等效，则返回 `true`，否则返回 `false`。

**从 `3.2.0` 版本开始**

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `path` | `Array|string` | 要获取的属性路径。 |
| `srcValue` | `*` | 要匹配的值。 |

**返回**

`(Function)`: 返回新的规范函数。

**示例**

```javascript
var objects = [
  { 'a': 1, 'b': 2, 'c': 3 },
  { 'a': 4, 'b': 5, 'c': 6 }
];

_.find(objects, _.matchesProperty('a', 4));
// => { 'a': 4, 'b': 5, 'c': 6 }
```

### _.method(path, [...args])

创建一个调用给定对象 `path` 处方法的函数。任何附加的参数都会提供给被调用的方法。

**从 `3.7.0` 版本开始**

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `path` | `Array|string` | 要调用的方法路径。 |
| `[...args]` | `*` | 调用方法的参数。 |

**返回**

`(Function)`: 返回新的调用函数。

**示例**

```javascript
var objects = [
  { 'a': { 'b': _.constant(2) } },
  { 'a': { 'b': _.constant(1) } }
];

_.map(objects, _.method('a.b'));
// => [2, 1]
```

### _.methodOf(object, [...args])

`_.method` 的反向版本；此方法创建一个函数，该函数调用 `object` 的给定路径上的方法。任何附加的参数都会提供给被调用的方法。

**从 `3.7.0` 版本开始**

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `object` | `Object` | 要查询的对象。 |
| `[...args]` | `*` | 调用方法的参数。 |

**返回**

`(Function)`: 返回新的调用函数。

**示例**

```javascript
var array = _.times(3, _.constant),
    object = { 'a': array, 'b': array, 'c': array };

_.map(['a[2]', 'c[0]'], _.methodOf(object));
// => [2, 0]
```

### _.mixin([object=lodash], source, [options={}])

将源对象的所有自有可枚举字符串键的函数属性添加到目标对象。如果 `object` 是一个函数，则方法也会添加到其原型中。

**从 `0.1.0` 版本开始**

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `[object=lodash]` | `Function|Object` | 目标对象。 |
| `source` | `Object` | 要添加的函数对象。 |
| `[options={}]` | `Object` | 选项对象。 |
| `[options.chain=true]` | `boolean` | 指定 mixin 是否可链式调用。 |

**返回**

`(Function|Object)`: 返回 `object`。

**示例**

```javascript
function vowels(string) {
  return _.filter(string, function(v) {
    return /[aeiou]/i.test(v);
  });
}

_.mixin({ 'vowels': vowels });
_.vowels('fred');
// => ['e']
```

### _.noConflict()

将 `_` 变量恢复到其先前的值，并返回对 `lodash` 函数的引用。

**从 `0.1.0` 版本开始**

**返回**

`(Function)`: 返回 `lodash` 函数。

**示例**

```javascript
var lodash = _.noConflict();
```

### _.noop()

此方法返回 `undefined`。

**从 `2.3.0` 版本开始**

**示例**

```javascript
_.times(2, _.noop);
// => [undefined, undefined]
```

### _.nthArg([n=0])

创建一个获取第 `n` 个参数的函数。如果 `n` 为负数，则返回从末尾开始的第 n 个参数。

**从 `4.0.0` 版本开始**

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `[n=0]` | `number` | 要返回的参数索引。 |

**返回**

`(Function)`: 返回新的直通函数。

**示例**

```javascript
var func = _.nthArg(1);
func('a', 'b', 'c', 'd');
// => 'b'

var func = _.nthArg(-2);
func('a', 'b', 'c', 'd');
// => 'c'
```

### _.over([...iteratees=[_.identity]])

创建一个函数，该函数使用它接收的参数调用 `iteratees` 并返回它们的结果。

**从 `4.o.0` 版本开始**

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `[...iteratees=[_.identity]]` | `...(Function|Function[])` | 要调用的迭代器。 |

**返回**

`(Function)`: 返回新函数。

**示例**

```javascript
var func = _.over([Math.max, Math.min]);

func(1, 2, 3, 4);
// => [4, 1]
```

### _.overEvery([...predicates=[_.identity]])

创建一个函数，该函数检查所有 `predicates` 在使用其接收的参数调用时是否都返回真值。

**从 `4.0.0` 版本开始**

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `[...predicates=[_.identity]]` | `...(Function|Function[])` | 要检查的谓词。 |

**返回**

`(Function)`: 返回新函数。

**示例**

```javascript
var func = _.overEvery([Boolean, isFinite]);

func('1');
// => true

func(null);
// => false
```

### _.overSome([...predicates=[_.identity]])

创建一个函数，该函数检查是否有任何 `predicates` 在使用其接收的参数调用时返回真值。

**从 `4.0.0` 版本开始**

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `[...predicates=[_.identity]]` | `...(Function|Function[])` | 要检查的谓词。 |

**返回**

`(Function)`: 返回新函数。

**示例**

```javascript
var func = _.overSome([Boolean, isFinite]);

func('1');
// => true

func(null);
// => true
```

### _.property(path)

创建一个返回给定对象 `path` 处值的函数。

**从 `2.4.0` 版本开始**

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `path` | `Array|string` | 要获取的属性路径。 |

**返回**

`(Function)`: 返回新的访问器函数。

**示例**

```javascript
var objects = [
  { 'a': { 'b': 2 } },
  { 'a': { 'b': 1 } }
];

_.map(objects, _.property('a.b'));
// => [2, 1]
```

### _.propertyOf(object)

`_.property` 的反向版本；此方法创建一个返回 `object` 给定路径处值的函数。

**从 `3.0.0` 版本开始**

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `object` | `Object` | 要查询的对象。 |

**返回**

`(Function)`: 返回新的访问器函数。

**示例**

```javascript
var array = [0, 1, 2],
    object = { 'a': array, 'b': array, 'c': array };

_.map(['a[2]', 'c[0]'], _.propertyOf(object));
// => [2, 0]
```

### _.range([start=0], end, [step=1])

创建一个从 `start` 开始到（但不包括）`end` 的数字数组。如果 `start` 为负数且未指定 `end` 或 `step`，则步长为 `-1`。如果未指定 `end`，则将其设置为 `start`，然后将 `start` 设置为 `0`。

**从 `0.1.0` 版本开始**

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `[start=0]` | `number` | 范围的起始值。 |
| `end` | `number` | 范围的结束值。 |
| `[step=1]` | `number` | 递增或递减的值。 |

**返回**

`(Array)`: 返回数字范围数组。

**示例**

```javascript
_.range(4);
// => [0, 1, 2, 3]

_.range(-4);
// => [0, -1, -2, -3]

_.range(1, 5);
// => [1, 2, 3, 4]
```

### _.rangeRight([start=0], end, [step=1])

此方法类似于 `_.range`，但它以降序填充值。

**从 `4.0.0` 版本开始**

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `[start=0]` | `number` | 范围的起始值。 |
| `end` | `number` | 范围的结束值。 |
| `[step=1]` | `number` | 递增或递减的值。 |

**返回**

`(Array)`: 返回数字范围数组。

**示例**

```javascript
_.rangeRight(4);
// => [3, 2, 1, 0]

_.rangeRight(1, 5);
// => [4, 3, 2, 1]
```

### _.runInContext([context=root])

使用 `context` 对象创建一个新的纯净 `lodash` 函数。

**从 `1.1.0` 版本开始**

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `[context=root]` | `Object` | 上下文对象。 |

**返回**

`(Function)`: 返回一个新的 `lodash` 函数。

**示例**

```javascript
_.mixin({ 'foo': _.constant('foo') });

var lodash = _.runInContext();
lodash.mixin({ 'bar': lodash.constant('bar') });

_.isFunction(_.foo);
// => true
_.isFunction(_.bar);
// => false

lodash.isFunction(lodash.foo);
// => false
lodash.isFunction(lodash.bar);
// => true

// 在 Node.js 中创建一个增强的 `defer`。
var defer = _.runInContext({ 'setTimeout': setImmediate }).defer;
```

### _.stubArray()

此方法返回一个新的空数组。

**从 `4.13.0` 版本开始**

**返回**

`(Array)`: 返回新的空数组。

**示例**

```javascript
var arrays = _.times(2, _.stubArray);

console.log(arrays);
// => [[], []]
```

### _.stubFalse()

此方法返回 `false`。

**从 `4.13.0` 版本开始**

**返回**

`(boolean)`: 返回 `false`。

**示例**

```javascript
_.times(2, _.stubFalse);
// => [false, false]
```

### _.stubObject()

此方法返回一个新的空对象。

**从 `4.13.0` 版本开始**

**返回**

`(Object)`: 返回新的空对象。

**示例**

```javascript
var objects = _.times(2, _.stubObject);

console.log(objects);
// => [{}, {}]
```

### _.stubString()

此方法返回一个空字符串。

**从 `4.13.0` 版本开始**

**返回**

`(string)`: 返回空字符串。

**示例**

```javascript
_.times(2, _.stubString);
// => ['', '']
```

### _.stubTrue()

此方法返回 `true`。

**从 `4.13.0` 版本开始**

**返回**

`(boolean)`: 返回 `true`。

**示例**

```javascript
_.times(2, _.stubTrue);
// => [true, true]
```

### _.times(n, [iteratee=_.identity])

调用 `iteratee` `n` 次，返回一个由每次调用的结果组成的数组。`iteratee` 以一个参数调用：`(index)`。

**从 `0.1.0` 版本开始**

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `n` | `number` | 调用 `iteratee` 的次数。 |
| `[iteratee=_.identity]` | `Function` | 每次迭代调用的函数。 |

**返回**

`(Array)`: 返回结果数组。

**示例**

```javascript
_.times(3, String);
// => ['0', '1', '2']
```

### _.toPath(value)

将 `value` 转换为属性路径数组。

**从 `4.0.0` 版本开始**

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `value` | `*` | 要转换的值。 |

**返回**

`(Array)`: 返回新的属性路径数组。

**示例**

```javascript
_.toPath('a.b.c');
// => ['a', 'b', 'c']

_.toPath('a[0].b.c');
// => ['a', '0', 'b', 'c']
```

### _.uniqueId([prefix=''])

生成一个唯一的 ID。如果提供了 `prefix`，ID 将附加到它后面。

**从 `0.1.0` 版本开始**

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `[prefix='']` | `string` | ID 的前缀。 |

**返回**

`(string)`: 返回唯一的 ID。

**示例**

```javascript
_.uniqueId('contact_');
// => 'contact_104'

_.uniqueId();
// => '105'
```

---

现在您已经了解了 Lodash 的实用工具函数，可以继续探索[函数 (Function)](./api-function.md)或[序列 (Seq)](./api-seq.md)部分的文档，以了解更多关于函数式编程和链式调用的内容。
