# 对象

本节提供了用于操作和处理对象的 Lodash 函数的详细参考。这些实用工具可帮助完成创建、修改、检索和转换对象属性等任务。

对于以通用方式（类似于数组）迭代对象的函数，请参阅 [Collection](./api-collection.md) 文档。

---

### `_.assign(object, ...sources)`

将源对象自身的可枚举字符串键属性分配给目标对象。源对象从左到右应用。后续源对象的属性会覆盖先前源对象的属性赋值。

**注意：** 此方法会改变 `object`，并且大致基于 [`Object.assign`](https://mdn.io/Object/assign)。

**版本**：0.10.0

**参数**

| Parameter | Type | Description |
|---|---|---|
| `object` | `Object` | 目标对象。 |
| `...sources`| `...Object` | 源对象。 |

**返回值**

- `(Object)`: 返回修改后的 `object`。

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

### `_.create(prototype, [properties])`

创建一个继承自 `prototype` 对象的对象。如果提供了 `properties` 对象，则其自身的可枚举字符串键属性将被分配给创建的对象。

**版本**：2.3.0

**参数**

| Parameter | Type | Description |
|---|---|---|
| `prototype` | `Object` | 要继承的对象。 |
| `[properties]`| `Object` | 要分配给对象的属性。 |

**返回值**

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
console.log(circle instanceof Circle);
// => true

console.log(circle instanceof Shape);
// => true
```

---

### `_.defaults(object, ...sources)`

将源对象自身和继承的可枚举字符串键属性分配给目标对象，但仅限于目标对象中解析为 `undefined` 的属性。源对象从左到右应用。一旦某个属性被设置，后续相同属性的其他值将被忽略。

**注意：** 此方法会改变 `object`。

**版本**：0.1.0

**参数**

| Parameter | Type | Description |
|---|---|---|
| `object` | `Object` | 目标对象。 |
| `...sources`| `...Object` | 源对象。 |

**返回值**

- `(Object)`: 返回修改后的 `object`。

**示例**

```javascript
_.defaults({ 'a': 1 }, { 'b': 2 }, { 'a': 3 });
// => { 'a': 1, 'b': 2 }
```

---

### `_.get(object, path, [defaultValue])`

获取 `object` 中 `path` 路径上的值。如果解析出的值为 `undefined`，则返回 `defaultValue`。

**版本**：3.7.0

**参数**

| Parameter | Type | Description |
|---|---|---|
| `object` | `Object` | 要查询的对象。 |
| `path` | `Array|string` | 要获取的属性路径。 |
| `[defaultValue]` | `*` | 当解析值为 `undefined` 时返回的值。 |

**返回值**

- `(*)`: 返回解析出的值。

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

### `_.has(object, path)`

检查 `path` 是否是 `object` 的直接属性。

**版本**：0.1.0

**参数**

| Parameter | Type | Description |
|---|---|---|
| `object` | `Object` | 要查询的对象。 |
| `path` | `Array|string` | 要检查的路径。 |

**返回值**

- `(boolean)`: 如果 `path` 存在，则返回 `true`，否则返回 `false`。

**示例**

```javascript
var object = { 'a': { 'b': 2 } };
var other = _.create({ 'a': _.create({ 'b': 2 }) });

_.has(object, 'a');
// => true

_.has(object, 'a.b');
// => true

_.has(other, 'a');
// => false
```

---

### `_.keys(object)`

创建一个由 `object` 自身的可枚举属性名组成的数组。

**注意：** 非对象值会被强制转换成对象。

**版本**：0.1.0

**参数**

| Parameter | Type | Description |
|---|---|---|
| `object` | `Object` | 要查询的对象。 |

**返回值**

- `(Array)`: 返回属性名数组。

**示例**

```javascript
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.keys(new Foo);
// => ['a', 'b'] (iteration order is not guaranteed)

_.keys('hi');
// => ['0', '1']
```

---

### `_.merge(object, ...sources)`

此方法类似于 `_.assign`，但它会递归地将源对象自身和继承的可枚举字符串键属性合并到目标对象中。如果目标对象中存在某个值，则会跳过解析为 `undefined` 的源属性。数组和纯对象属性会进行递归合并。其他对象和值类型则通过赋值来覆盖。

**注意：** 此方法会改变 `object`。

**版本**：0.5.0

**参数**

| Parameter | Type | Description |
|---|---|---|
| `object` | `Object` | 目标对象。 |
| `...sources`| `...Object` | 源对象。 |

**返回值**

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

### `_.omit(object, ...paths)`

`_.pick` 的反向方法；此方法创建一个由 `object` 中未被忽略的自身和继承的可枚举属性路径组成的对象。

**版本**：0.1.0

**参数**

| Parameter | Type | Description |
|---|---|---|
| `object` | `Object` | 源对象。 |
| `...paths`| `...(string|string[])` | 要忽略的属性路径。 |

**返回值**

- `(Object)`: 返回新对象。

**示例**

```javascript
var object = { 'a': 1, 'b': '2', 'c': 3 };
 
_.omit(object, ['a', 'c']);
// => { 'b': '2' }
```

---

### `_.pick(object, ...paths)`

创建一个由选中的 `object` 属性组成的对象。

**版本**：0.1.0

**参数**

| Parameter | Type | Description |
|---|---|---|
| `object` | `Object` | 源对象。 |
| `...paths`| `...(string|string[])` | 要选取的属性路径。 |

**返回值**

- `(Object)`: 返回新对象。

**示例**

```javascript
var object = { 'a': 1, 'b': '2', 'c': 3 };
 
_.pick(object, ['a', 'c']);
// => { 'a': 1, 'c': 3 }
```

---

### `_.set(object, path, value)`

设置 `object` 中 `path` 路径上的值。如果 `path` 的一部分不存在，则会被创建。对于缺失的索引属性，会创建数组；对于所有其他缺失的属性，则会创建对象。

**注意：** 此方法会改变 `object`。

**版本**：3.7.0

**参数**

| Parameter | Type | Description |
|---|---|---|
| `object` | `Object` | 要修改的对象。 |
| `path` | `Array|string` | 要设置的属性路径。 |
| `value` | `*` | 要设置的值。 |

**返回值**

- `(Object)`: 返回 `object`。

**示例**

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

### `_.values(object)`

创建一个由 `object` 自身的可枚举字符串键属性值组成的数组。

**注意：** 非对象值会被强制转换成对象。

**版本**：0.1.0

**参数**

| Parameter | Type | Description |
|---|---|---|
| `object` | `Object` | 要查询的对象。 |

**返回值**

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

以上涵盖了 Lodash 中核心的对象操作函数。这些实用工具为处理对象数据结构提供了强大而灵活的方式。
要将这些操作以可读的顺序链接在一起，请参阅 [Seq](./api-seq.md) 文档。