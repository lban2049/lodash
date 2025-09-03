# 对象

本节提供了用于操作和处理对象的 Lodash 函数的详细参考。这些实用工具涵盖了广泛的操作，包括创建、分配、合并、挑选和转换对象属性。对于迭代对象的函数，您可能也会发现 [Collection](./api-collection.md) 方法很有用。

---

## assign

将源对象的自有可枚举字符串键属性分配给目标对象。源对象从左到右应用。后续的源对象会覆盖之前源对象的属性赋值。

**注意：** 此方法会改变 `object`。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 目标对象。 |
| `...[sources]` | `Object` | 源对象。 |

### 返回值

- `(Object)`: 返回 `object`。

### 示例

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

此方法类似于 `_.assign`，不同之处在于它会迭代源对象的自有和继承属性。

**注意：** 此方法会改变 `object`。

### 别名
- `extend`

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 目标对象。 |
| `...[sources]` | `Object` | 源对象。 |

### 返回值

- `(Object)`: 返回 `object`。

### 示例

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

此方法类似于 `_.assignIn`，不同之处在于它接受一个 `customizer` 函数，该函数被调用以生成赋得的值。如果 `customizer` 返回 `undefined`，则赋值操作由该方法本身处理。`customizer` 调用时会传入五个参数：(objValue, srcValue, key, object, source)。

**注意：** 此方法会改变 `object`。

### 别名
- `extendWith`

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 目标对象。 |
| `...sources` | `Object` | 源对象。 |
| `[customizer]` | `Function` | 用于自定义赋值的函数。 |

### 返回值

- `(Object)`: 返回 `object`。

### 示例

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

此方法类似于 `_.assign`，不同之处在于它接受一个 `customizer` 函数，该函数被调用以生成赋得的值。如果 `customizer` 返回 `undefined`，则赋值操作由该方法本身处理。`customizer` 调用时会传入五个参数：(objValue, srcValue, key, object, source)。

**注意：** 此方法会改变 `object`。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 目标对象。 |
| `...sources` | `Object` | 源对象。 |
| `[customizer]` | `Function` | 用于自定义赋值的函数。 |

### 返回值

- `(Object)`: 返回 `object`。

### 示例

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

创建一个由 `object` 的 `paths` 路径相应的值组成的数组。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要迭代的对象。 |
| `...[paths]` | `(string\|string[])` | 要选取的属性路径。 |

### 返回值

- `(Array)`: 返回选取的值。

### 示例

```javascript
var object = { 'a': [{ 'b': { 'c': 3 } }, 4] };

_.at(object, ['a[0].b.c', 'a[1]']);
// => [3, 4]
```

---

## create

创建一个继承自 `prototype` 对象的新对象。如果提供了 `properties` 对象，则其自身的、可枚举的、字符串键的属性将被分配给创建的对象。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `prototype` | `Object` | 要继承的对象。 |
| `[properties]` | `Object` | 要分配给对象的属性。 |

### 返回值

- `(Object)`: 返回新对象。

### 示例

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

将源对象的自有和继承的可枚举字符串键属性分配给目标对象，但仅限于目标对象中解析为 `undefined` 的属性。源对象从左到右应用。一旦某个属性被设置，后续相同属性的附加值将被忽略。

**注意：** 此方法会改变 `object`。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 目标对象。 |
| `...[sources]` | `Object` | 源对象。 |

### 返回值

- `(Object)`: 返回 `object`。

### 示例

```javascript
_.defaults({ 'a': 1 }, { 'b': 2 }, { 'a': 3 });
// => { 'a': 1, 'b': 2 }
```

---

## defaultsDeep

此方法类似于 `_.defaults`，不同之处在于它会递归地分配默认属性。

**注意：** 此方法会改变 `object`。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 目标对象。 |
| `...[sources]` | `Object` | 源对象。 |

### 返回值

- `(Object)`: 返回 `object`。

### 示例

```javascript
_.defaultsDeep({ 'a': { 'b': 2 } }, { 'a': { 'b': 1, 'c': 3 } });
// => { 'a': { 'b': 2, 'c': 3 } }
```

---

## findKey

此方法类似于 `_.find`，不同之处在于它返回第一个 `predicate` 返回真值的元素的键，而不是元素本身。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要检查的对象。 |
| `[predicate]` | `Function` | 每次迭代时调用的函数。默认为 `_.identity`。 |

### 返回值

- `(string|undefined)`: 返回匹配元素的键，否则返回 `undefined`。

### 示例

```javascript
var users = {
  'barney':  { 'age': 36, 'active': true },
  'fred':    { 'age': 40, 'active': false },
  'pebbles': { 'age': 1,  'active': true }
};

_.findKey(users, function(o) { return o.age < 40; });
// => 'barney' (迭代顺序不保证)

// `_.matches` 的迭代器速记法。
_.findKey(users, { 'age': 1, 'active': true });
// => 'pebbles'

// `_.matchesProperty` 的迭代器速记法。
_.findKey(users, ['active', false]);
// => 'fred'

// `_.property` 的迭代器速记法。
_.findKey(users, 'active');
// => 'barney'
```

---

## findLastKey

此方法类似于 `_.findKey`，不同之处在于它以相反的顺序迭代集合的元素。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要检查的对象。 |
| `[predicate]` | `Function` | 每次迭代时调用的函数。默认为 `_.identity`。 |

### 返回值

- `(string|undefined)`: 返回匹配元素的键，否则返回 `undefined`。

### 示例

```javascript
var users = {
  'barney':  { 'age': 36, 'active': true },
  'fred':    { 'age': 40, 'active': false },
  'pebbles': { 'age': 1,  'active': true }
};

_.findLastKey(users, function(o) { return o.age < 40; });
// => 假设 `_.findKey` 返回 'barney'，则返回 'pebbles'

// `_.matches` 的迭代器速记法。
_.findLastKey(users, { 'age': 36, 'active': true });
// => 'barney'

// `_.matchesProperty` 的迭代器速记法。
_.findLastKey(users, ['active', false]);
// => 'fred'

// `_.property` 的迭代器速记法。
_.findLastKey(users, 'active');
// => 'pebbles'
```

---

## forIn

迭代一个对象的自有和继承的可枚举字符串键属性，并为每个属性调用 `iteratee`。迭代器被调用时会传入三个参数：(value, key, object)。迭代器函数可以通过显式返回 `false` 来提前退出迭代。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要迭代的对象。 |
| `[iteratee]` | `Function` | 每次迭代时调用的函数。默认为 `_.identity`。 |

### 返回值

- `(Object)`: 返回 `object`。

### 示例

```javascript
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.forIn(new Foo, function(value, key) {
  console.log(key);
});
// => 依次打印 'a'、'b'、'c' (迭代顺序不保证)。
```

---

## forInRight

此方法类似于 `_.forIn`，不同之处在于它以相反的顺序迭代 `object` 的属性。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要迭代的对象。 |
| `[iteratee]` | `Function` | 每次迭代时调用的函数。默认为 `_.identity`。 |

### 返回值

- `(Object)`: 返回 `object`。

### 示例

```javascript
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.forInRight(new Foo, function(value, key) {
  console.log(key);
});
// => 假设 `_.forIn` 打印 'a'、'b'、'c'，则打印 'c'、'b'、'a'。
```

---

## forOwn

迭代一个对象的自有可枚举字符串键属性，并为每个属性调用 `iteratee`。迭代器被调用时会传入三个参数：(value, key, object)。迭代器函数可以通过显式返回 `false` 来提前退出迭代。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要迭代的对象。 |
| `[iteratee]` | `Function` | 每次迭代时调用的函数。默认为 `_.identity`。 |

### 返回值

- `(Object)`: 返回 `object`。

### 示例

```javascript
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.forOwn(new Foo, function(value, key) {
  console.log(key);
});
// => 依次打印 'a' 和 'b' (迭代顺序不保证)。
```

---

## forOwnRight

此方法类似于 `_.forOwn`，不同之处在于它以相反的顺序迭代 `object` 的属性。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要迭代的对象。 |
| `[iteratee]` | `Function` | 每次迭代时调用的函数。默认为 `_.identity`。 |

### 返回值

- `(Object)`: 返回 `object`。

### 示例

```javascript
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.forOwnRight(new Foo, function(value, key) {
  console.log(key);
});
// => 假设 `_.forOwn` 打印 'a' 和 'b'，则打印 'b' 和 'a'。
```

---

## functions

创建一个由 `object` 的自有可枚举属性中的函数属性名组成的数组。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要检查的对象。 |

### 返回值

- `(Array)`: 返回函数名。

### 示例

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

创建一个由 `object` 的自有和继承的可枚举属性中的函数属性名组成的数组。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要检查的对象。 |

### 返回值

- `(Array)`: 返回函数名。

### 示例

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

获取 `object` 中 `path` 路径上的值。如果解析出的值为 `undefined`，则返回 `defaultValue`。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要查询的对象。 |
| `path` | `Array\|string` | 要获取的属性路径。 |
| `[defaultValue]` | `*` | 为 `undefined` 的解析值返回的默认值。 |

### 返回值

- `(*)`: 返回解析出的值。

### 示例

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

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要查询的对象。 |
| `path` | `Array\|string` | 要检查的路径。 |

### 返回值

- `(boolean)`: 如果 `path` 存在，则返回 `true`，否则返回 `false`。

### 示例

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

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要查询的对象。 |
| `path` | `Array\|string` | 要检查的路径。 |

### 返回值

- `(boolean)`: 如果 `path` 存在，则返回 `true`，否则返回 `false`。

### 示例

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

创建一个由 `object` 的键和值反转组成的对象。如果 `object` 包含重复的值，后续的值会覆盖先前值的属性赋值。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要反转的对象。 |

### 返回值

- `(Object)`: 返回新的反转对象。

### 示例

```javascript
var object = { 'a': 1, 'b': 2, 'c': 1 };

_.invert(object);
// => { '1': 'c', '2': 'b' }
```

---

## invertBy

此方法类似于 `_.invert`，不同之处在于反转后的对象是通过对 `object` 的每个元素运行 `iteratee` 的结果生成的。每个反转键对应的反转值是一个数组，包含生成该反转值的键。迭代器被调用时会传入一个参数：(value)。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要反转的对象。 |
| `[iteratee]` | `Function` | 每次迭代时调用的迭代器。默认为 `_.identity`。 |

### 返回值

- `(Object)`: 返回新的反转对象。

### 示例

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

调用 `object` 中 `path` 路径上的方法。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要查询的对象。 |
| `path` | `Array\|string` | 要调用的方法的路径。 |
| `...[args]` | `*` | 调用方法时传入的参数。 |

### 返回值

- `(*)`: 返回调用方法的结果。

### 示例

```javascript
var object = { 'a': [{ 'b': { 'c': [1, 2, 3, 4] } }] };

_.invoke(object, 'a[0].b.c.slice', 1, 3);
// => [2, 3]
```

---

## keys

创建一个由 `object` 的自有可枚举属性名组成的数组。

**注意：** 非对象值会被强制转换成对象。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要查询的对象。 |

### 返回值

- `(Array)`: 返回属性名数组。

### 示例

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

创建一个由 `object` 的自有和继承的可枚举属性名组成的数组。

**注意：** 非对象值会被强制转换成对象。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要查询的对象。 |

### 返回值

- `(Array)`: 返回属性名数组。

### 示例

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

`_.mapValues` 的反向方法；此方法创建一个与 `object` 值相同的对象，其键是通过对 `object` 的每个自有可枚举字符串键属性运行 `iteratee` 生成的。迭代器被调用时会传入三个参数：(value, key, object)。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要迭代的对象。 |
| `[iteratee]` | `Function` | 每次迭代时调用的函数。默认为 `_.identity`。 |

### 返回值

- `(Object)`: 返回新的映射对象。

### 示例

```javascript
_.mapKeys({ 'a': 1, 'b': 2 }, function(value, key) {
  return key + value;
});
// => { 'a1': 1, 'b2': 2 }
```

---

## mapValues

创建一个与 `object` 键相同的对象，其值是通过对 `object` 的每个自有可枚举字符串键属性运行 `iteratee` 生成的。迭代器被调用时会传入三个参数：(value, key, object)。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要迭代的对象。 |
| `[iteratee]` | `Function` | 每次迭代时调用的函数。默认为 `_.identity`。 |

### 返回值

- `(Object)`: 返回新的映射对象。

### 示例

```javascript
var users = {
  'fred':    { 'user': 'fred',    'age': 40 },
  'pebbles': { 'user': 'pebbles', 'age': 1 }
};

_.mapValues(users, function(o) { return o.age; });
// => { 'fred': 40, 'pebbles': 1 } (迭代顺序不保证)

// `_.property` 的迭代器速记法。
_.mapValues(users, 'age');
// => { 'fred': 40, 'pebbles': 1 } (迭代顺序不保证)
```

---

## merge

此方法类似于 `_.assign`，不同之处在于它会递归地将源对象的自有和继承的可枚举字符串键属性合并到目标对象中。如果目标值存在，则解析为 `undefined` 的源属性将被跳过。数组和普通对象属性会进行递归合并。其他对象和值类型会通过赋值被覆盖。源对象从左到右应用。后续的源对象会覆盖之前源对象的属性赋值。

**注意：** 此方法会改变 `object`。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 目标对象。 |
| `...[sources]` | `Object` | 源对象。 |

### 返回值

- `(Object)`: 返回 `object`。

### 示例

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

此方法类似于 `_.merge`，不同之处在于它接受一个 `customizer` 函数，该函数被调用以生成目标属性和源属性的合并值。如果 `customizer` 返回 `undefined`，则合并操作由该方法本身处理。`customizer` 调用时会传入六个参数：(objValue, srcValue, key, object, source, stack)。

**注意：** 此方法会改变 `object`。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 目标对象。 |
| `...sources` | `Object` | 源对象。 |
| `customizer` | `Function` | 用于自定义赋值的函数。 |

### 返回值

- `(Object)`: 返回 `object`。

### 示例

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

`_.pick` 的反向方法；此方法创建一个由 `object` 中未被忽略的自有和继承的可枚举属性路径组成的对象。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 源对象。 |
| `...[paths]` | `(string\|string[])` | 要忽略的属性路径。 |

### 返回值

- `(Object)`: 返回新对象。

### 示例

```javascript
var object = { 'a': 1, 'b': '2', 'c': 3 };

_.omit(object, ['a', 'c']);
// => { 'b': '2' }
```

---

## omitBy

`_.pickBy` 的反向方法；此方法创建一个由 `object` 的自有和继承的可枚举字符串键属性组成的对象，这些属性的 `predicate` 不返回真值。 predicate 被调用时会传入两个参数：(value, key)。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 源对象。 |
| `[predicate]` | `Function` | 每个属性调用的函数。默认为 `_.identity`。 |

### 返回值

- `(Object)`: 返回新对象。

### 示例

```javascript
var object = { 'a': 1, 'b': '2', 'c': 3 };

_.omitBy(object, _.isNumber);
// => { 'b': '2' }
```

---

## pick

创建一个由选取的 `object` 属性组成的对象。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 源对象。 |
| `...[paths]` | `(string\|string[])` | 要选取的属性路径。 |

### 返回值

- `(Object)`: 返回新对象。

### 示例

```javascript
var object = { 'a': 1, 'b': '2', 'c': 3 };

_.pick(object, ['a', 'c']);
// => { 'a': 1, 'c': 3 }
```

---

## pickBy

创建一个由 `object` 属性组成的对象，这些属性的 `predicate` 返回真值。 predicate 被调用时会传入两个参数：(value, key)。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 源对象。 |
| `[predicate]` | `Function` | 每个属性调用的函数。默认为 `_.identity`。 |

### 返回值

- `(Object)`: 返回新对象。

### 示例

```javascript
var object = { 'a': 1, 'b': '2', 'c': 3 };

_.pickBy(object, _.isNumber);
// => { 'a': 1, 'c': 3 }
```

---

## result

此方法类似于 `_.get`，不同之处在于如果解析出的值是一个函数，它将被调用，其 `this` 绑定到其父对象，并返回其结果。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要查询的对象。 |
| `path` | `Array\|string` | 要解析的属性路径。 |
| `[defaultValue]` | `*` | 为 `undefined` 的解析值返回的默认值。 |

### 返回值

- `(*)`: 返回解析出的值。

### 示例

```javascript
var object = { 'a': [{ 'b': { 'c1': 3, 'c2': _.constant(4) } }] };

_.result(object, 'a[0].b.c1');
// => 3

_.result(object, 'a[0].b.c2');
// => 4

_.result(object, 'a[0].b.c3', 'default');
// => 'default'

_.result(object, 'a[0].b.c3', _.constant('default'));
// => 'default'
```

---

## set

设置 `object` 中 `path` 路径上的值。如果 `path` 的一部分不存在，则会被创建。数组会为缺失的索引属性创建，而对象会为所有其他缺失的属性创建。使用 `_.setWith` 自定义 `path` 的创建。

**注意：** 此方法会改变 `object`。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要修改的对象。 |
| `path` | `Array\|string` | 要设置的属性路径。 |
| `value` | `*` | 要设置的值。 |

### 返回值

- `(Object)`: 返回 `object`。

### 示例

```javascript
var object = { 'a': [{ 'b': { 'c': 3 } }] };

_.set(object, 'a[0].b.c', 4);
console.log(object.a[0].b.c);
// => 4

_.set(object, ['x', '0', 'y', 'z'], 5);
console.log(object.x[0].y.z);
// => 5
```

---

## setWith

此方法类似于 `_.set`，不同之处在于它接受一个 `customizer` 函数，该函数被调用以生成 `path` 的对象。如果 `customizer` 返回 `undefined`，则路径创建由该方法本身处理。`customizer` 调用时会传入三个参数：(nsValue, key, nsObject)。

**注意：** 此方法会改变 `object`。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要修改的对象。 |
| `path` | `Array\|string` | 要设置的属性路径。 |
| `value` | `*` | 要设置的值。 |
| `[customizer]` | `Function` | 用于自定义赋值的函数。 |

### 返回值

- `(Object)`: 返回 `object`。

### 示例

```javascript
var object = {};

_.setWith(object, '[0][1]', 'a', Object);
// => { '0': { '1': 'a' } }
```

---

## toPairs

为 `object` 创建一个由自有可枚举字符串键值对组成的数组，该数组可被 `_.fromPairs` 使用。如果 `object` 是一个 map 或 set，则返回其条目。

### 别名
- `entries`

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要查询的对象。 |

### 返回值

- `(Array)`: 返回键值对。

### 示例

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

为 `object` 创建一个由自有和继承的可枚举字符串键值对组成的数组，该数组可被 `_.fromPairs` 使用。如果 `object` 是一个 map 或 set，则返回其条目。

### 别名
- `entriesIn`

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要查询的对象。 |

### 返回值

- `(Array)`: 返回键值对。

### 示例

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

`_.reduce` 的替代方法；此方法将 `object` 转换为一个新的 `accumulator` 对象，该对象是通过对 `object` 的每个自有可枚举字符串键属性运行 `iteratee` 的结果，每次调用都可能改变 `accumulator` 对象。如果没有提供 `accumulator`，将使用一个具有相同 `[[Prototype]]` 的新对象。迭代器被调用时会传入四个参数：(accumulator, value, key, object)。迭代器函数可以通过显式返回 `false` 来提前退出迭代。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要迭代的对象。 |
| `[iteratee]` | `Function` | 每次迭代时调用的函数。默认为 `_.identity`。 |
| `[accumulator]` | `*` | 自定义的累加器值。 |

### 返回值

- `(*)`: 返回累加后的值。

### 示例

```javascript
_.transform([2, 3, 4], function(result, n) {
  result.push(n *= n);
  return n % 2 == 0;
}, []);
// => [4, 9]

_.transform({ 'a': 1, 'b': 2, 'c': 1 }, function(result, value, key) {
  (result[value] || (result[value] = [])).push(key);
}, {});
// => { '1': ['a', 'c'], '2': ['b'] }
```

---

## unset

移除 `object` 中 `path` 路径上的属性。

**注意：** 此方法会改变 `object`。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要修改的对象。 |
| `path` | `Array\|string` | 要移除的属性路径。 |

### 返回值

- `(boolean)`: 如果属性被删除，则返回 `true`，否则返回 `false`。

### 示例

```javascript
var object = { 'a': [{ 'b': { 'c': 7 } }] };
_.unset(object, 'a[0].b.c');
// => true

console.log(object);
// => { 'a': [{ 'b': {} }] };

_.unset(object, ['a', '0', 'b', 'c']);
// => true

console.log(object);
// => { 'a': [{ 'b': {} }] };
```

---

## update

此方法类似于 `_.set`，不同之处在于它接受一个 `updater` 来生成要设置的值。使用 `_.updateWith` 自定义 `path` 的创建。`updater` 调用时会传入一个参数：(value)。

**注意：** 此方法会改变 `object`。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要修改的对象。 |
| `path` | `Array\|string` | 要设置的属性路径。 |
| `updater` | `Function` | 用于生成更新值的函数。 |

### 返回值

- `(Object)`: 返回 `object`。

### 示例

```javascript
var object = { 'a': [{ 'b': { 'c': 3 } }] };

_.update(object, 'a[0].b.c', function(n) { return n * n; });
console.log(object.a[0].b.c);
// => 9

_.update(object, 'x[0].y.z', function(n) { return n ? n + 1 : 0; });
console.log(object.x[0].y.z);
// => 0
```

---

## updateWith

此方法类似于 `_.update`，不同之处在于它接受一个 `customizer` 函数，该函数被调用以生成 `path` 的对象。如果 `customizer` 返回 `undefined`，则路径创建由该方法本身处理。`customizer` 调用时会传入三个参数：(nsValue, key, nsObject)。

**注意：** 此方法会改变 `object`。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要修改的对象。 |
| `path` | `Array\|string` | 要设置的属性路径。 |
| `updater` | `Function` | 用于生成更新值的函数。 |
| `[customizer]` | `Function` | 用于自定义赋值的函数。 |

### 返回值

- `(Object)`: 返回 `object`。

### 示例

```javascript
var object = {};

_.updateWith(object, '[0][1]', _.constant('a'), Object);
// => { '0': { '1': 'a' } }
```

---

## values

创建一个由 `object` 的自有可枚举字符串键属性值组成的数组。

**注意：** 非对象值会被强制转换成对象。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要查询的对象。 |

### 返回值

- `(Array)`: 返回属性值数组。

### 示例

```javascript
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.values(new Foo);
// => [1, 2] (迭代顺序不保证)

_.values('hi');
// => ['h', 'i']
```

---

## valuesIn

创建一个由 `object` 的自有和继承的可枚举字符串键属性值组成的数组。

**注意：** 非对象值会被强制转换成对象。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `object` | `Object` | 要查询的对象。 |

### 返回值

- `(Array)`: 返回属性值数组。

### 示例

```javascript
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.valuesIn(new Foo);
// => [1, 2, 3] (迭代顺序不保证)
```

---

本节关于对象函数的参考到此结束。有关方法链和序列操作的实用工具，请继续阅读 [Seq](./api-seq.md) 文档。