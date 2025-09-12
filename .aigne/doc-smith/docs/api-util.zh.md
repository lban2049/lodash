# 工具函数

Util 类别提供了一系列不方便归入其他类别的杂项工具函数。这些函数有助于处理常见的编程任务，例如创建函数组合、生成唯一 ID、管理属性等。它们是简化复杂逻辑和提高代码可读性的强大工具。

要了解更多与函数相关的工具，请浏览 [Function](./api-function.md) 类别。要了解类型检查和克隆，请参阅 [Lang](./api-lang.md) 类别。

---

### attempt

尝试调用 `func`，返回结果或捕获的错误对象。调用 `func` 时，会提供任何额外的参数。

**Parameters**

<x-field data-name="func" data-type="Function" data-required="true" data-desc="要尝试调用的函数。"></x-field>
<x-field data-name="...args" data-type="any" data-required="false" data-desc="用于调用 func 的参数。"></x-field>

**Returns**

<x-field data-name="" data-type="any" data-desc="返回 func 的结果或错误对象。"></x-field>

**Example**

```javascript
// 避免因无效操作而抛出错误。
var elements = _.attempt(function(value) {
  if (typeof value !== 'number') {
    throw new TypeError('Expected a number');
  }
  return value * 2;
}, 'oops');

if (_.isError(elements)) {
  console.log('Caught an error!');
  elements = [];
}
// => 打印 'Caught an error!'
```

---

### bindAll

将对象的方法绑定到对象本身，并覆盖现有方法。这对于确保方法作为回调传递时具有正确的 `this` 上下文很有用。

**注意：** 此方法不会设置绑定函数的“length”属性。

**Parameters**

<x-field data-name="object" data-type="Object" data-required="true" data-desc="要绑定并分配已绑定方法的对象。"></x-field>
<x-field data-name="...methodNames" data-type="string|string[]" data-required="true" data-desc="要绑定的对象方法名。"></x-field>

**Returns**

<x-field data-name="" data-type="Object" data-desc="返回修改后的对象。"></x-field>

**Example**

```javascript
var view = {
  'label': 'docs',
  'click': function() {
    console.log('clicked ' + this.label);
  }
};

_.bindAll(view, ['click']);

// 当 view.click 作为回调使用时，`this` 将指向 `view`。
// setTimeout(view.click, 100); // => 100 毫秒后打印 'clicked docs'。
```

---

### cond

创建一个函数，该函数遍历 `pairs` 并调用第一个返回真值的谓词所对应的函数。谓词-函数对在调用时会绑定所创建函数的 `this` 和参数。

**Parameters**

<x-field data-name="pairs" data-type="Array" data-required="true" data-desc="谓词-函数对。"></x-field>

**Returns**

<x-field data-name="" data-type="Function" data-desc="返回新的复合函数。"></x-field>

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

### conforms

创建一个函数，该函数使用给定对象的相应属性值来调用 `source` 的谓词属性。如果所有谓词都返回真值，则返回 `true`，否则返回 `false`。

**注意：** 创建的函数等效于 `_.conformsTo`，其中 `source` 已被部分应用。

**Parameters**

<x-field data-name="source" data-type="Object" data-required="true" data-desc="要符合的属性谓词对象。"></x-field>

**Returns**

<x-field data-name="" data-type="Function" data-desc="返回新的规范函数。"></x-field>

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

### constant

创建一个函数，该函数返回创建时所用的 `value`。无论向该函数传递什么参数，它都将始终返回相同的值。

**Parameters**

<x-field data-name="value" data-type="any" data-required="true" data-desc="新函数要返回的值。"></x-field>

**Returns**

<x-field data-name="" data-type="Function" data-desc="返回新的常量函数。"></x-field>

**Example**

```javascript
var objects = _.times(2, _.constant({ 'a': 1 }));

console.log(objects);
// => [{ 'a': 1 }, { 'a': 1 }]

console.log(objects[0] === objects[1]);
// => true
```

---

### defaultTo

检查 `value` 以确定是否应返回默认值来代替它。如果 `value` 是 `NaN`、`null` 或 `undefined`，则返回 `defaultValue`。

**Parameters**

<x-field data-name="value" data-type="any" data-required="true" data-desc="要检查的值。"></x-field>
<x-field data-name="defaultValue" data-type="any" data-required="true" data-desc="默认值。"></x-field>

**Returns**

<x-field data-name="" data-type="any" data-desc="返回解析后的值。"></x-field>

**Example**

```javascript
_.defaultTo(1, 10);
// => 1

_.defaultTo(undefined, 10);
// => 10
```

---

### flow

创建一个函数，该函数返回从左到右调用给定函数的结果。每个后续函数都使用前一个函数的返回值进行调用。

**Parameters**

<x-field data-name="...funcs" data-type="Function|Function[]" data-required="false" data-desc="要调用的函数。"></x-field>

**Returns**

<x-field data-name="" data-type="Function" data-desc="返回新的复合函数。"></x-field>

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

### flowRight

此方法类似于 `_.flow`，只是它创建的函数会从右到左调用给定的函数。

**Parameters**

<x-field data-name="...funcs" data-type="Function|Function[]" data-required="false" data-desc="要调用的函数。"></x-field>

**Returns**

<x-field data-name="" data-type="Function" data-desc="返回新的复合函数。"></x-field>

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

### identity

此方法返回它接收到的第一个参数。它可用作默认的迭代器。

**Parameters**

<x-field data-name="value" data-type="any" data-required="true" data-desc="任何值。"></x-field>

**Returns**

<x-field data-name="" data-type="any" data-desc="返回值。"></x-field>

**Example**

```javascript
var object = { 'a': 1 };

_.identity(object) === object;
// => true
```

---

### iteratee

创建一个可用作其他 Lodash 方法的迭代器的函数。它接受多种简写形式：
- **字符串**：创建一个 `_.property` 迭代器。
- **数组**：创建一个 `_.matchesProperty` 迭代器。
- **对象**：创建一个 `_.matches` 迭代器。

**Parameters**

<x-field data-name="func" data-type="any" data-default="_.identity" data-desc="要转换为回调的值。"></x-field>

**Returns**

<x-field data-name="" data-type="Function" data-desc="返回回调。"></x-field>

**Example**

```javascript
var users = [
  { 'user': 'barney', 'age': 36, 'active': true },
  { 'user': 'fred',   'age': 40, 'active': false }
];

// _.matches 迭代器的简写形式。
_.filter(users, _.iteratee({ 'user': 'barney', 'active': true }));
// => [{ 'user': 'barney', 'age': 36, 'active': true }]

// _.matchesProperty 迭代器的简写形式。
_.filter(users, _.iteratee(['user', 'fred']));
// => [{ 'user': 'fred', 'age': 40, 'active': false }]

// _.property 迭代器的简写形式。
_.map(users, _.iteratee('user'));
// => ['barney', 'fred']
```

---

### matches

创建一个函数，该函数在给定对象和 `source` 之间执行部分深度比较，如果给定对象具有等效的属性值，则返回 `true`，否则返回 `false`。

**Parameters**

<x-field data-name="source" data-type="Object" data-required="true" data-desc="要匹配的属性值对象。"></x-field>

**Returns**

<x-field data-name="" data-type="Function" data-desc="返回新的规范函数。"></x-field>

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

### matchesProperty

创建一个函数，该函数将给定对象在 `path` 处的值与 `srcValue` 进行部分深度比较，如果对象值等效，则返回 `true`，否则返回 `false`。

**Parameters**

<x-field data-name="path" data-type="Array|string" data-required="true" data-desc="要获取的属性路径。"></x-field>
<x-field data-name="srcValue" data-type="any" data-required="true" data-desc="要匹配的值。"></x-field>

**Returns**

<x-field data-name="" data-type="Function" data-desc="返回新的规范函数。"></x-field>

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

### method

创建一个函数，该函数调用给定对象在 `path` 处的​​方法。任何其他参数都会提供给被调用的方法。

**Parameters**

<x-field data-name="path" data-type="Array|string" data-required="true" data-desc="要调用的方法的路径。"></x-field>
<x-field data-name="...args" data-type="any" data-required="false" data-desc="用于调用方法的参数。"></x-field>

**Returns**

<x-field data-name="" data-type="Function" data-desc="返回新的调用函数。"></x-field>

**Example**

```javascript
var objects = [
  { 'a': { 'b': _.constant(2) } },
  { 'a': { 'b': _.constant(1) } }
];

_.map(objects, _.method('a.b'));
// => [2, 1]
```

---

### methodOf

`_.method` 的反向方法；此方法创建一个函数，该函数调用 `object` 在给定路径上的方法。任何其他参数都会提供给被调用的方法。

**Parameters**

<x-field data-name="object" data-type="Object" data-required="true" data-desc="要查询的对象。"></x-field>
<x-field data-name="...args" data-type="any" data-required="false" data-desc="用于调用方法的参数。"></x-field>

**Returns**

<x-field data-name="" data-type="Function" data-desc="返回新的调用函数。"></x-field>

**Example**

```javascript
var array = [0, 1, 2],
    object = { 'a': array, 'b': array, 'c': array };

_.map(['a[2]', 'c[0]'], _.methodOf(object));
// => [2, 0]
```

---

### mixin

将源对象所有可枚举的字符串键函数属性添加到目标对象。如果 `object` 是一个函数，则方法也会添加到其原型中。

**Parameters**

<x-field data-name="object" data-type="Function|Object" data-default="lodash" data-desc="目标对象。"></x-field>
<x-field data-name="source" data-type="Object" data-required="true" data-desc="要添加的函数对象。"></x-field>
<x-field data-name="options" data-type="Object" data-required="false" data-desc="选项对象。">
  <x-field data-name="chain" data-type="boolean" data-default="true" data-desc="指定 mixin 是否可链式调用。"></x-field>
</x-field>

**Returns**

<x-field data-name="" data-type="Function|Object" data-desc="返回对象。"></x-field>

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

### noConflict

将 `_` 变量恢复到其先前的值，并返回对 `lodash` 函数的引用。这对于在其他库也可能使用下划线变量的环境中避免命名空间冲突非常有用。

**Returns**

<x-field data-name="" data-type="Function" data-desc="返回 lodash 函数。"></x-field>

**Example**

```javascript
// 在另一个库也使用 _ 的浏览器环境中
var lodash = _.noConflict();
// `_` 现在已恢复为其原始值。
// `lodash` 可用于调用 Lodash 函数。
```

---

### noop

此方法返回 `undefined`。它是一个有用的占位符，可用于表示不执行任何操作的函数或回调。

**Example**

```javascript
_.times(2, _.noop);
// => [undefined, undefined]
```

---

### nthArg

创建一个函数，该函数获取索引为 `n` 的参数。如果 `n` 是负数，则返回从末尾算起的第 n 个参数。

**Parameters**

<x-field data-name="n" data-type="number" data-default="0" data-desc="要返回的参数的索引。"></x-field>

**Returns**

<x-field data-name="" data-type="Function" data-desc="返回新的直通函数。"></x-field>

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

### over

创建一个函数，该函数使用接收到的参数调用 `iteratees`，并将其结果作为数组返回。

**Parameters**

<x-field data-name="...iteratees" data-type="Function|Function[]" data-default="_.identity" data-desc="要调用的迭代器。"></x-field>

**Returns**

<x-field data-name="" data-type="Function" data-desc="返回新函数。"></x-field>

**Example**

```javascript
var func = _.over([Math.max, Math.min]);

func(1, 2, 3, 4);
// => [4, 1]
```

---

### overEvery

创建一个函数，该函数检查在使用其接收到的参数调用时，是否**所有** `predicates` 都返回真值。

**Parameters**

<x-field data-name="...predicates" data-type="Function|Function[]" data-default="_.identity" data-desc="要检查的谓词。"></x-field>

**Returns**

<x-field data-name="" data-type="Function" data-desc="返回新函数。"></x-field>

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

### overSome

创建一个函数，该函数检查在使用其接收到的参数调用时，是否有**任何** `predicates` 返回真值。

**Parameters**

<x-field data-name="...predicates" data-type="Function|Function[]" data-default="_.identity" data-desc="要检查的谓词。"></x-field>

**Returns**

<x-field data-name="" data-type="Function" data-desc="返回新函数。"></x-field>

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

### property

创建一个函数，该函数返回给定对象在 `path` 处的值。

**Parameters**

<x-field data-name="path" data-type="Array|string" data-required="true" data-desc="要获取的属性路径。"></x-field>

**Returns**

<x-field data-name="" data-type="Function" data-desc="返回新的访问器函数。"></x-field>

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

### propertyOf

`_.property` 的反向方法；此方法创建一个函数，该函数返回 `object` 在给定路径上的值。

**Parameters**

<x-field data-name="object" data-type="Object" data-required="true" data-desc="要查询的对象。"></x-field>

**Returns**

<x-field data-name="" data-type="Function" data-desc="返回新的访问器函数。"></x-field>

**Example**

```javascript
var array = [0, 1, 2],
    object = { 'a': array, 'b': array, 'c': array };

_.map(['a[2]', 'c[0]'], _.propertyOf(object));
// => [2, 0]
```

---

### range

创建一个从 `start` 开始到 `end`（不包括 `end`）的数字（正数和/或负数）递增数组。

**Parameters**

<x-field data-name="start" data-type="number" data-default="0" data-desc="范围的起始值。"></x-field>
<x-field data-name="end" data-type="number" data-required="true" data-desc="范围的结束值。"></x-field>
<x-field data-name="step" data-type="number" data-default="1" data-desc="递增或递减的值。"></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="返回数字范围。"></x-field>

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

### rangeRight

此方法类似于 `_.range`，只是它按降序填充值。

**Parameters**

<x-field data-name="start" data-type="number" data-default="0" data-desc="范围的起始值。"></x-field>
<x-field data-name="end" data-type="number" data-required="true" data-desc="范围的结束值。"></x-field>
<x-field data-name="step" data-type="number" data-default="1" data-desc="递增或递减的值。"></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="返回数字范围。"></x-field>

**Example**

```javascript
_.rangeRight(4);
// => [3, 2, 1, 0]

_.rangeRight(1, 5);
// => [4, 3, 2, 1]
```

---

### stubArray

此方法返回一个新的空数组。它可用作应返回数组的默认值或回调。

**Returns**

<x-field data-name="" data-type="Array" data-desc="返回新的空数组。"></x-field>

**Example**

```javascript
var arrays = _.times(2, _.stubArray);

console.log(arrays);
// => [[], []]

console.log(arrays[0] === arrays[1]);
// => false
```

---

### stubFalse

此方法返回 `false`。它可用作始终失败的默认谓词。

**Returns**

<x-field data-name="" data-type="boolean" data-desc="返回 false。"></x-field>

**Example**

```javascript
_.times(2, _.stubFalse);
// => [false, false]
```

---

### stubObject

此方法返回一个新的空对象。它可用作应返回对象的默认值或回调。

**Returns**

<x-field data-name="" data-type="Object" data-desc="返回新的空对象。"></x-field>

**Example**

```javascript
var objects = _.times(2, _.stubObject);

console.log(objects);
// => [{}, {}]

console.log(objects[0] === objects[1]);
// => false
```

---

### stubString

此方法返回一个空字符串。它可用作应返回字符串的默认值或回调。

**Returns**

<x-field data-name="" data-type="string" data-desc="返回空字符串。"></x-field>

**Example**

```javascript
_.times(2, _.stubString);
// => ['', '']
```

---

### stubTrue

此方法返回 `true`。它可用作始终通过的默认谓词。

**Returns**

<x-field data-name="" data-type="boolean" data-desc="返回 true。"></x-field>

**Example**

```javascript
_.times(2, _.stubTrue);
// => [true, true]
```

---

### times

调用迭代器 `n` 次，返回一个包含每次调用结果的数组。调用迭代器时会传入一个参数：`index`。

**Parameters**

<x-field data-name="n" data-type="number" data-required="true" data-desc="调用迭代器的次数。"></x-field>
<x-field data-name="iteratee" data-type="Function" data-default="_.identity" data-desc="每次迭代调用的函数。"></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="返回结果数组。"></x-field>

**Example**

```javascript
_.times(3, String);
// => ['0', '1', '2']

_.times(4, _.constant(0));
// => [0, 0, 0, 0]
```

---

### toPath

将 `value` 转换为属性路径数组。这对于规范化属性访问器很有用。

**Parameters**

<x-field data-name="value" data-type="any" data-required="true" data-desc="要转换的值。"></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="返回新的属性路径数组。"></x-field>

**Example**

```javascript
_.toPath('a.b.c');
// => ['a', 'b', 'c']

_.toPath('a[0].b.c');
// => ['a', '0', 'b', 'c']
```

---

### uniqueId

生成一个唯一的 ID。如果提供了 `prefix`，则会将该 ID 附加到其后。

**Parameters**

<x-field data-name="prefix" data-type="string" data-default="''" data-desc="要为 ID 添加前缀的值。"></x-field>

**Returns**

<x-field data-name="" data-type="string" data-desc="返回唯一的 ID。"></x-field>

**Example**

```javascript
_.uniqueId('contact_');
// => 'contact_1'

_.uniqueId();
// => '2'
```