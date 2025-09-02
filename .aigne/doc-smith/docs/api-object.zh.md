# Object

Lodash 提供了大量用于操作和处理 JavaScript 对象的函数。这些工具可以帮助你合并、转换、选择、检查和设置对象的属性，是数据处理流程中的核心部分。这些函数专注于处理对象自身的和继承的属性，提供了比原生 JavaScript 更强大和灵活的功能。

想了解更多关于迭代对象和数组的内容，请参考 [Collection](./api-collection.md) 部分的函数。

---

## assign

将一个或多个源对象的自身可枚举字符串键属性分配到目标对象。源对象从左到右应用，后续源的属性会覆盖先前源的属性。

**注意：** 此方法会改变 `object`。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 目标对象。 |
| `[sources]` | `...Object` | 一个或多个源对象。 |

**返回**

- `(Object)`: 返回改变后的 `object`。

**示例**

```javascript
function Foo() {
  this.a = 1;
}

function Bar() {
  this.c = 3;
}

Foo.prototype.b = 2;
Bar.prototype.d = 4;

_.assign({ 'a': 0 }, new Foo, new Bar);
// => { 'a': 1, 'c': 3 }
```

---

## assignIn

此方法类似 `_.assign`，但是它会遍历并继承源对象的属性。别名 `_.extend`。

**注意：** 此方法会改变 `object`。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 目标对象。 |
| `[sources]` | `...Object` | 一个或多个源对象。 |

**返回**

- `(Object)`: 返回 `object`。

**示例**

```javascript
function Foo() {
  this.a = 1;
}

function Bar() {
  this.c = 3;
}

Foo.prototype.b = 2;
Bar.prototype.d = 4;

_.assignIn({ 'a': 0 }, new Foo, new Bar);
// => { 'a': 1, 'b': 2, 'c': 3, 'd': 4 }
```

---

## assignInWith

此方法类似 `_.assignIn`，除了它接受一个 `customizer` 来自定义分配的值。如果 `customizer` 返回 `undefined`，则由方法本身处理分配。`customizer` 会被调用并传入五个参数：(objValue, srcValue, key, object, source)。

**注意：** 此方法会改变 `object`。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 目标对象。 |
| `sources` | `...Object` | 一个或多个源对象。 |
| `[customizer]` | `Function` | 自定义分配值的函数。 |

**返回**

- `(Object)`: 返回 `object`。

**示例**

```javascript
function customizer(objValue, srcValue) {
  return _.isUndefined(objValue) ? srcValue : objValue;
}

var defaults = _.partialRight(_.assignInWith, customizer);

defaults({ 'a': 1 }, { 'b': 2 }, { 'a': 3 });
// => { 'a': 1, 'b': 2 }
```

---

## assignWith

此方法类似 `_.assign`，除了它接受一个 `customizer` 来自定义分配的值。如果 `customizer` 返回 `undefined`，则由方法本身处理分配。`customizer` 会被调用并传入五个参数：(objValue, srcValue, key, object, source)。

**注意：** 此方法会改变 `object`。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 目标对象。 |
| `sources` | `...Object` | 一个或多个源对象。 |
| `[customizer]` | `Function` | 自定义分配值的函数。 |

**返回**

- `(Object)`: 返回 `object`。

**示例**

```javascript
function customizer(objValue, srcValue) {
  return _.isUndefined(objValue) ? srcValue : objValue;
}

var defaults = _.partialRight(_.assignWith, customizer);

defaults({ 'a': 1 }, { 'b': 2 }, { 'a': 3 });
// => { 'a': 1, 'b': 2 }
```

---

## at

创建一个数组，包含从 `object` 中按 `paths` 提取的值。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要迭代的对象。 |
| `[paths]` | `...(string|string[])` | 要挑选的属性路径。 |

**返回**

- `(Array)`: 返回挑选出的值。

**示例**

```javascript
var object = { 'a': [{ 'b': { 'c': 3 } }, 4] };

_.at(object, ['a[0].b.c', 'a[1]']);
// => [3, 4]
```

---

## create

创建一个继承自 `prototype` 的对象。如果提供了 `properties` 对象，它的自身可枚举字符串键属性会被分配到创建的对象上。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `prototype` | `Object` | 要继承的对象。 |
| `[properties]` | `Object` | 分配给新对象的属性。 |

**返回**

- `(Object)`: 返回新对象。

**示例**

```javascript
function Shape() {
  this.x = 0;
  this.y = 0;
}

function Circle() {
  Shape.call(this);
}

Circle.prototype = _.create(Shape.prototype, {
  'constructor': Circle
});

var circle = new Circle;
circle instanceof Circle;
// => true

circle instanceof Shape;
// => true
```

---

## defaults

分配来源对象的可枚举属性到目标对象所有 `undefined` 的属性上。来源对象从左到右应用。一旦设置了属性，后续的相同属性将被忽略。

**注意：** 此方法会改变 `object`。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 目标对象。 |
| `[sources]` | `...Object` | 一个或多个源对象。 |

**返回**

- `(Object)`: 返回 `object`。

**示例**

```javascript
_.defaults({ 'a': 1 }, { 'b': 2 }, { 'a': 3 });
// => { 'a': 1, 'b': 2 }
```

---

## defaultsDeep

此方法类似 `_.defaults`，但是它会递归地分配默认属性。

**注意：** 此方法会改变 `object`。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 目标对象。 |
| `[sources]` | `...Object` | 一个或多个源对象。 |

**返回**

- `(Object)`: 返回 `object`。

**示例**

```javascript
_.defaultsDeep({ 'a': { 'b': 2 } }, { 'a': { 'b': 1, 'c': 3 } });
// => { 'a': { 'b': 2, 'c': 3 } }
```

---

## findKey

此方法类似 `_.find`，但它返回第一个 `predicate` 返回真值的元素的键，而不是元素本身。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要检查的对象。 |
| `[predicate]` | `Function` | 每次迭代调用的函数。 |

**返回**

- `(string|undefined)`: 返回匹配元素的键，否则返回 `undefined`。

**示例**

```javascript
var users = {
  'barney':  { 'age': 36, 'active': true },
  'fred':    { 'age': 40, 'active': false },
  'pebbles': { 'age': 1,  'active': true }
};

_.findKey(users, function(o) { return o.age < 40; });
// => 'barney' (迭代顺序不保证)
```

---

## findLastKey

此方法类似 `_.findKey`，但它从右到左遍历集合的元素。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要检查的对象。 |
| `[predicate]` | `Function` | 每次迭代调用的函数。 |

**返回**

- `(string|undefined)`: 返回匹配元素的键，否则返回 `undefined`。

**示例**

```javascript
var users = {
  'barney':  { 'age': 36, 'active': true },
  'fred':    { 'age': 40, 'active': false },
  'pebbles': { 'age': 1,  'active': true }
};

_.findLastKey(users, function(o) { return o.age < 40; });
// => 'pebbles' (假设 _.findKey 返回 'barney')
```

---

## forIn

遍历对象的自身和继承的可枚举字符串键属性，并为每个属性调用 `iteratee`。`iteratee` 调用时传入三个参数：(value, key, object)。如果 `iteratee` 显式返回 `false`，则会提前退出迭代。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要迭代的对象。 |
| `[iteratee]` | `Function` | 每次迭代调用的函数。 |

**返回**

- `(Object)`: 返回 `object`。

**示例**

```javascript
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.forIn(new Foo, function(value, key) {
  console.log(key);
});
// => 依次打印 'a', 'b', 'c' (迭代顺序不保证)
```

---

## forInRight

此方法类似 `_.forIn`，但它以相反的顺序遍历对象的属性。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要迭代的对象。 |
| `[iteratee]` | `Function` | 每次迭代调用的函数。 |

**返回**

- `(Object)`: 返回 `object`。

**示例**

```javascript
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.forInRight(new Foo, function(value, key) {
  console.log(key);
});
// => 假设 _.forIn 打印 'a', 'b', 'c'，则打印 'c', 'b', 'a'
```

---

## forOwn

遍历对象的自身可枚举字符串键属性，并为每个属性调用 `iteratee`。`iteratee` 调用时传入三个参数：(value, key, object)。如果 `iteratee` 显式返回 `false`，则会提前退出迭代。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要迭代的对象。 |
| `[iteratee]` | `Function` | 每次迭代调用的函数。 |

**返回**

- `(Object)`: 返回 `object`。

**示例**

```javascript
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.forOwn(new Foo, function(value, key) {
  console.log(key);
});
// => 依次打印 'a', 'b' (迭代顺序不保证)
```

---

## forOwnRight

此方法类似 `_.forOwn`，但它以相反的顺序遍历对象的属性。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要迭代的对象。 |
| `[iteratee]` | `Function` | 每次迭代调用的函数。 |

**返回**

- `(Object)`: 返回 `object`。

**示例**

```javascript
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.forOwnRight(new Foo, function(value, key) {
  console.log(key);
});
// => 假设 _.forOwn 打印 'a', 'b'，则打印 'b', 'a'
```

---

## functions

创建一个包含 `object` 自身可枚举属性中所有函数属性名的数组。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要检查的对象。 |

**返回**

- `(Array)`: 返回函数名数组。

**示例**

```javascript
function Foo() {
  this.a = _.constant('a');
  this.b = _.constant('b');
}

Foo.prototype.c = _.constant('c');

_.functions(new Foo);
// => ['a', 'b']
```

---

## functionsIn

创建一个包含 `object` 自身和继承的可枚举属性中所有函数属性名的数组。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要检查的对象。 |

**返回**

- `(Array)`: 返回函数名数组。

**示例**

```javascript
function Foo() {
  this.a = _.constant('a');
  this.b = _.constant('b');
}

Foo.prototype.c = _.constant('c');

_.functionsIn(new Foo);
// => ['a', 'b', 'c']
```

---

## get

获取 `object` 的 `path` 路径上的值。如果解析值为 `undefined`，则返回 `defaultValue`。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要查询的对象。 |
| `path` | `Array` or `string` | 要获取的属性路径。 |
| `[defaultValue]` | `*` | 如果解析值为 `undefined` 时返回的值。 |

**返回**

- `(*)`: 返回解析后的值。

**示例**

```javascript
var object = { 'a': [{ 'b': { 'c': 3 } }] };

_.get(object, 'a[0].b.c');
// => 3

_.get(object, ['a', '0', 'b', 'c']);
// => 3

_.get(object, 'a.b.c', 'default');
// => 'default'
```

---

## has

检查 `path` 是否是 `object` 的直接属性。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要查询的对象。 |
| `path` | `Array` or `string` | 要检查的路径。 |

**返回**

- `(boolean)`: 如果 `path` 存在，则返回 `true`，否则返回 `false`。

**示例**

```javascript
var object = { 'a': { 'b': 2 } };
var other = _.create({ 'a': _.create({ 'b': 2 }) });

_.has(object, 'a');
// => true

_.has(object, 'a.b');
// => true

_.has(object, ['a', 'b']);
// => true

_.has(other, 'a');
// => false
```

---

## hasIn

检查 `path` 是否是 `object` 的直接或继承属性。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要查询的对象。 |
| `path` | `Array` or `string` | 要检查的路径。 |

**返回**

- `(boolean)`: 如果 `path` 存在，则返回 `true`，否则返回 `false`。

**示例**

```javascript
var object = _.create({ 'a': _.create({ 'b': 2 }) });

_.hasIn(object, 'a');
// => true

_.hasIn(object, 'a.b');
// => true

_.hasIn(object, ['a', 'b']);
// => true

_.hasIn(object, 'b');
// => false
```

---

## invert

创建一个键值倒置后的对象。如果 `object` 包含重复的值，后续的值会覆盖先前的值。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要倒置的对象。 |

**返回**

- `(Object)`: 返回新的倒置对象。

**示例**

```javascript
var object = { 'a': 1, 'b': 2, 'c': 1 };

_.invert(object);
// => { '1': 'c', '2': 'b' }
```

---

## invertBy

此方法类似 `_.invert`，但倒置的对象是通过对 `object` 的每个元素执行 `iteratee` 生成的。每个倒置键对应的值是一个由生成该倒置值的键组成的数组。`iteratee` 调用时传入一个参数：(value)。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要倒置的对象。 |
| `[iteratee]` | `Function` | 每次迭代调用的函数。 |

**返回**

- `(Object)`: 返回新的倒置对象。

**示例**

```javascript
var object = { 'a': 1, 'b': 2, 'c': 1 };

_.invertBy(object);
// => { '1': ['a', 'c'], '2': ['b'] }

_.invertBy(object, function(value) {
  return 'group' + value;
});
// => { 'group1': ['a', 'c'], 'group2': ['b'] }
```

---

## invoke

调用 `object` 上 `path` 处的函数。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要查询的对象。 |
| `path` | `Array` or `string` | 要调用的函数路径。 |
| `[args]` | `...*` | 调用函数时传入的参数。 |

**返回**

- `(*)`: 返回调用函数的结果。

**示例**

```javascript
var object = { 'a': [{ 'b': { 'c': [1, 2, 3, 4] } }] };

_.invoke(object, 'a[0].b.c.slice', 1, 3);
// => [2, 3]
```

---

## keys

创建一个 `object` 自身可枚举属性名为一个数组。

**注意：** 非对象的值会被强制转换为对象。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要查询的对象。 |

**返回**

- `(Array)`: 返回属性名数组。

**示例**

```javascript
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.keys(new Foo);
// => ['a', 'b'] (迭代顺序不保证)

_.keys('hi');
// => ['0', '1']
```

---

## keysIn

创建一个 `object` 自身和继承的可枚举属性名为一个数组。

**注意：** 非对象的值会被强制转换为对象。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要查询的对象。 |

**返回**

- `(Array)`: 返回属性名数组。

**示例**

```javascript
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.keysIn(new Foo);
// => ['a', 'b', 'c'] (迭代顺序不保证)
```

---

## mapKeys

`_.mapValues` 的反向方法；此方法创建一个与 `object` 值相同的对象，键是通过对 `object` 的每个自身可枚举字符串键属性执行 `iteratee` 生成的。`iteratee` 调用时传入三个参数：(value, key, object)。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要迭代的对象。 |
| `[iteratee]` | `Function` | 每次迭代调用的函数。 |

**返回**

- `(Object)`: 返回新的映射对象。

**示例**

```javascript
_.mapKeys({ 'a': 1, 'b': 2 }, function(value, key) {
  return key + value;
});
// => { 'a1': 1, 'b2': 2 }
```

---

## mapValues

创建一个与 `object` 键相同的对象，值是通过对 `object` 的每个自身可枚举字符串键属性执行 `iteratee` 生成的。`iteratee` 调用时传入三个参数：(value, key, object)。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要迭代的对象。 |
| `[iteratee]` | `Function` | 每次迭代调用的函数。 |

**返回**

- `(Object)`: 返回新的映射对象。

**示例**

```javascript
var users = {
  'fred':    { 'user': 'fred',    'age': 40 },
  'pebbles': { 'user': 'pebbles', 'age': 1 }
};

_.mapValues(users, function(o) { return o.age; });
// => { 'fred': 40, 'pebbles': 1 } (迭代顺序不保证)
```

---

## merge

递归地合并来源对象的自身和继承的可枚举属性到目标对象。如果目标值存在，源值是 `undefined` 则会被跳过。数组和普通对象会递归合并，其他对象和值类型则会被直接覆盖。源对象从左到右应用。

**注意：** 此方法会改变 `object`。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 目标对象。 |
| `[sources]` | `...Object` | 一个或多个源对象。 |

**返回**

- `(Object)`: 返回 `object`。

**示例**

```javascript
var object = {
  'a': [{ 'b': 2 }, { 'd': 4 }]
};

var other = {
  'a': [{ 'c': 3 }, { 'e': 5 }]
};

_.merge(object, other);
// => { 'a': [{ 'b': 2, 'c': 3 }, { 'd': 4, 'e': 5 }] }
```

---

## mergeWith

此方法类似 `_.merge`，除了它接受一个 `customizer` 来自定义合并的值。如果 `customizer` 返回 `undefined`，则由方法本身处理合并。`customizer` 会被调用并传入六个参数：(objValue, srcValue, key, object, source, stack)。

**注意：** 此方法会改变 `object`。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 目标对象。 |
| `sources` | `...Object` | 一个或多个源对象。 |
| `customizer` | `Function` | 自定义分配值的函数。 |

**返回**

- `(Object)`: 返回 `object`。

**示例**

```javascript
function customizer(objValue, srcValue) {
  if (_.isArray(objValue)) {
    return objValue.concat(srcValue);
  }
}

var object = { 'a': [1], 'b': [2] };
var other = { 'a': [3], 'b': [4] };

_.mergeWith(object, other, customizer);
// => { 'a': [1, 3], 'b': [2, 4] }
```

---

## omit

反向版 `_.pick`；这个方法创建一个忽略 `paths` 中属性的 `object`。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 源对象。 |
| `[paths]` | `...(string|string[])` | 要忽略的属性路径。 |

**返回**

- `(Object)`: 返回新对象。

**示例**

```javascript
var object = { 'a': 1, 'b': '2', 'c': 3 };

_.omit(object, ['a', 'c']);
// => { 'b': '2' }
```

---

## omitBy

反向版 `_.pickBy`；这个方法创建一个 `object` 自身和继承的可枚举属性，`predicate` 对其返回假值。`predicate` 调用时传入两个参数：(value, key)。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 源对象。 |
| `[predicate]` | `Function` | 每次迭代调用的函数。 |

**返回**

- `(Object)`: 返回新对象。

**示例**

```javascript
var object = { 'a': 1, 'b': '2', 'c': 3 };

_.omitBy(object, _.isNumber);
// => { 'b': '2' }
```

---

## pick

创建一个从 `object` 中挑选 `paths` 属性的对象。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 源对象。 |
| `[paths]` | `...(string|string[])` | 要挑选的属性路径。 |

**返回**

- `(Object)`: 返回新对象。

**示例**

```javascript
var object = { 'a': 1, 'b': '2', 'c': 3 };

_.pick(object, ['a', 'c']);
// => { 'a': 1, 'c': 3 }
```

---

## pickBy

创建一个 `object` 自身和继承的可枚举属性，`predicate` 对其返回真值。`predicate` 调用时传入两个参数：(value, key)。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 源对象。 |
| `[predicate]` | `Function` | 每次迭代调用的函数。 |

**返回**

- `(Object)`: 返回新对象。

**示例**

```javascript
var object = { 'a': 1, 'b': '2', 'c': 3 };

_.pickBy(object, _.isNumber);
// => { 'a': 1, 'c': 3 }
```

---

## result

此方法类似 `_.get`，但如果解析的值是函数，则会调用它并返回其结果。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要查询的对象。 |
| `path` | `Array` or `string` | 要解析的属性路径。 |
| `[defaultValue]` | `*` | 如果解析值为 `undefined` 时返回的值。 |

**返回**

- `(*)`: 返回解析后的值。

**示例**

```javascript
var object = { 'a': [{ 'b': { 'c1': 3, 'c2': _.constant(4) } }] };

_.result(object, 'a[0].b.c1');
// => 3

_.result(object, 'a[0].b.c2');
// => 4

_.result(object, 'a[0].b.c3', 'default');
// => 'default'
```

---

## set

设置 `object` 的 `path` 路径上的值。如果路径不存在，则会创建它。缺少索引属性时会创建数组，缺少其他属性时会创建对象。使用 `_.setWith` 自定义路径创建。

**注意：** 此方法会改变 `object`。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要修改的对象。 |
| `path` | `Array` or `string` | 要设置的属性路径。 |
| `value` | `*` | 要设置的值。 |

**返回**

- `(Object)`: 返回 `object`。

**示例**

```javascript
var object = { 'a': [{ 'b': { 'c': 3 } }] };

_.set(object, 'a[0].b.c', 4);
// object.a[0].b.c is 4

_.set(object, ['x', '0', 'y', 'z'], 5);
// object.x[0].y.z is 5
```

---

## setWith

此方法类似 `_.set`，除了它接受一个 `customizer` 来自定义路径的对象。如果 `customizer` 返回 `undefined`，则由方法本身处理路径创建。`customizer` 调用时传入三个参数：(nsValue, key, nsObject)。

**注意：** 此方法会改变 `object`。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要修改的对象。 |
| `path` | `Array` or `string` | 要设置的属性路径。 |
| `value` | `*` | 要设置的值。 |
| `[customizer]` | `Function` | 自定义分配值的函数。 |

**返回**

- `(Object)`: 返回 `object`。

**示例**

```javascript
var object = {};

_.setWith(object, '[0][1]', 'a', Object);
// => { '0': { '1': 'a' } }
```

---

## toPairs

创建一个 `object` 自身可枚举字符串键的键值对数组。如果 `object` 是 Map 或 Set，则返回其条目。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要查询的对象。 |

**返回**

- `(Array)`: 返回键值对数组。

**示例**

```javascript
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.toPairs(new Foo);
// => [['a', 1], ['b', 2]] (迭代顺序不保证)
```

---

## toPairsIn

创建一个 `object` 自身和继承的可枚举字符串键的键值对数组。如果 `object` 是 Map 或 Set，则返回其条目。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要查询的对象。 |

**返回**

- `(Array)`: 返回键值对数组。

**示例**

```javascript
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.toPairsIn(new Foo);
// => [['a', 1], ['b', 2], ['c', 3]] (迭代顺序不保证)
```

---

## transform

`_.reduce` 的替代方法；此方法将 `object` 转换为一个新的 `accumulator` 对象，该对象是 `object` 的每个自身可枚举属性经过 `iteratee` 处理的结果，每次调用都可能改变 `accumulator` 对象。如果未提供 `accumulator`，则会使用一个新的对象。`iteratee` 调用时传入四个参数：(accumulator, value, key, object)。如果 `iteratee` 显式返回 `false`，则会提前退出迭代。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要迭代的对象。 |
| `[iteratee]` | `Function` | 每次迭代调用的函数。 |
| `[accumulator]` | `*` | 自定义的累加器值。 |

**返回**

- `(*)`: 返回累加后的值。

**示例**

```javascript
_.transform([2, 3, 4], function(result, n) {
  result.push(n *= n);
  return n % 2 == 0;
}, []);
// => [4, 9]
```

---

## unset

移除 `object` 中 `path` 路径上的属性。

**注意：** 此方法会改变 `object`。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要修改的对象。 |
| `path` | `Array` or `string` | 要移除的属性路径。 |

**返回**

- `(boolean)`: 如果属性被删除，则返回 `true`，否则返回 `false`。

**示例**

```javascript
var object = { 'a': [{ 'b': { 'c': 7 } }] };
_.unset(object, 'a[0].b.c');
// => true

// object is { 'a': [{ 'b': {} }] };
```

---

## update

此方法类似 `_.set`，但它接受一个 `updater` 来生成要设置的值。`updater` 调用时传入一个参数：(value)。

**注意：** 此方法会改变 `object`。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要修改的对象。 |
| `path` | `Array` or `string` | 要设置的属性路径。 |
| `updater` | `Function` | 生成更新值的函数。 |

**返回**

- `(Object)`: 返回 `object`。

**示例**

```javascript
var object = { 'a': [{ 'b': { 'c': 3 } }] };

_.update(object, 'a[0].b.c', function(n) { return n * n; });
// object.a[0].b.c is 9
```

---

## updateWith

此方法类似 `_.update`，但它接受一个 `customizer` 来自定义路径的对象。如果 `customizer` 返回 `undefined`，则由方法本身处理路径创建。`customizer` 调用时传入三个参数：(nsValue, key, nsObject)。

**注意：** 此方法会改变 `object`。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要修改的对象。 |
| `path` | `Array` or `string` | 要设置的属性路径。 |
| `updater` | `Function` | 生成更新值的函数。 |
| `[customizer]` | `Function` | 自定义分配值的函数。 |

**返回**

- `(Object)`: 返回 `object`。

**示例**

```javascript
var object = {};

_.updateWith(object, '[0][1]', _.constant('a'), Object);
// => { '0': { '1': 'a' } }
```

---

## values

创建一个 `object` 自身可枚举属性值的数组。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要查询的对象。 |

**返回**

- `(Array)`: 返回属性值数组。

**示例**

```javascript
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.values(new Foo);
// => [1, 2] (iteration order is not guaranteed)

_.values('hi');
// => ['h', 'i']
```

---

## valuesIn

创建一个 `object` 自身和继承的可枚举属性值的数组。

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要查询的对象。 |

**返回**

- `(Array)`: 返回属性值数组。

**示例**

```javascript
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.valuesIn(new Foo);
// => [1, 2, 3] (iteration order is not guaranteed)
```

---

本节介绍了 Lodash 中用于对象操作的核心函数。掌握这些工具可以极大地简化数据处理和状态管理。接下来，可以继续探索 [Seq](./api-seq.md) 部分，了解如何使用链式调用来组合这些操作。
