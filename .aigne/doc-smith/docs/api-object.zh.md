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

本节介绍了 Lodash 中用于对象操作的核心函数。掌握这些工具可以极大地简化数据处理和状态管理。接下来，可以继续探索 [Seq](./api-seq.md) 部分，了解如何使用链式调用来组合这些操作。
