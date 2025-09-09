# 对象

Lodash 的对象函数提供了一个强大的工具包，用于创建、修改、检索和转换对象属性。这些实用工具简化了常见的对象相关任务，从合并对象到深度属性访问。对于遍历对象的函数，您可能也会发现 [Collection](./api-collection.md) 文档很有用。

## 创建和修改对象

这些函数用于通过分配、合并或设置属性来创建新对象或修改现有对象。

### assign

将源对象自身的可枚举字符串键属性分配给目标对象。源对象从左到右应用，后续源会覆盖先前源的属性分配。

**注意：** 此方法会改变 `object`。

#### 参数

| Name      | Type        | Description                |
| --------- | ----------- | -------------------------- |
| `object`  | `Object`    | 目标对象。    |
| `[sources]` | `...Object` | 源对象。        |

#### 返回值

(`Object`): 返回修改后的 `object`。

#### 示例

```javascript
function Foo() {
  this.a = 1;
}

function Bar() {
  this.c = 3;
}

Foo.prototype.b = 2;
Bar.prototype.d = 4;

_.assign({ 'a': 0 }, new Foo(), new Bar());
// => { 'a': 1, 'c': 3 }
```

### create

创建一个继承自 `prototype` 对象的对象。如果提供了 `properties` 对象，则其自身的可枚举字符串键属性将被分配给创建的对象。

#### 参数

| Name         | Type     | Description                          |
| ------------ | -------- | ------------------------------------ |
| `prototype`  | `Object` | 要继承的对象。          |
| `[properties]` | `Object` | 要分配给对象的属性。 |

#### 返回值

(`Object`): 返回新对象。

#### 示例

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

### defaults

将源对象自身和继承的可枚举字符串键属性分配给目标对象，但仅限于目标对象中解析为 `undefined` 的属性。源对象从左到右应用。

**注意：** 此方法会改变 `object`。

#### 参数

| Name      | Type        | Description                |
| --------- | ----------- | -------------------------- |
| `object`  | `Object`    | 目标对象。    |
| `[sources]` | `...Object` | 源对象。        |

#### 返回值

(`Object`): 返回 `object`。

#### 示例

```javascript
_.defaults({ 'a': 1 }, { 'b': 2 }, { 'a': 3 });
// => { 'a': 1, 'b': 2 }
```

### defaultsDeep

此方法类似于 `_.defaults`，但它会递归地分配默认属性。

**注意：** 此方法会改变 `object`。

#### 参数

| Name      | Type        | Description                |
| --------- | ----------- | -------------------------- |
| `object`  | `Object`    | 目标对象。    |
| `[sources]` | `...Object` | 源对象。        |

#### 返回值

(`Object`): 返回 `object`。

#### 示例

```javascript
_.defaultsDeep({ 'a': { 'b': 2 } }, { 'a': { 'b': 1, 'c': 3 } });
// => { 'a': { 'b': 2, 'c': 3 } }
```

### merge

递归地将源对象自身和继承的可枚举字符串键属性合并到目标对象中。数组和纯对象属性会进行递归合并。其他对象和值类型则通过赋值来覆盖。

**注意：** 此方法会改变 `object`。

#### 参数

| Name      | Type        | Description                |
| --------- | ----------- | -------------------------- |
| `object`  | `Object`    | 目标对象。    |
| `[sources]` | `...Object` | 源对象。        |

#### 返回值

(`Object`): 返回 `object`。

#### 示例

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

### set

设置 `object` 中 `path` 路径上的值。如果 `path` 的一部分不存在，则会创建它。对于缺失的索引属性会创建数组，而对于所有其他缺失的属性则会创建对象。

**注意：** 此方法会改变 `object`。

#### 参数

| Name    | Type           | Description                     |
| ------- | -------------- | ------------------------------- |
| `object`| `Object`       | 要修改的对象。           |
| `path`  | `Array`\|`string` | 要设置的属性路径。|
| `value` | `*`            | 要设置的值。               |

#### 返回值

(`Object`): 返回 `object`。

#### 示例

```javascript
var object = { 'a': [{ 'b': { 'c': 3 } }] };

_.set(object, 'a[0].b.c', 4);
console.log(object.a[0].b.c);
// => 4

_.set(object, ['x', '0', 'y', 'z'], 5);
console.log(object.x[0].y.z);
// => 5
```

### unset

移除 `object` 中 `path` 路径上的属性。

**注意：** 此方法会改变 `object`。

#### 参数

| Name    | Type           | Description                         |
| ------- | -------------- | ----------------------------------- |
| `object`| `Object`       | 要修改的对象。               |
| `path`  | `Array`\|`string` | 要移除的属性路径。  |

#### 返回值

(`boolean`): 如果属性被删除，则返回 `true`，否则返回 `false`。

#### 示例

```javascript
var object = { 'a': [{ 'b': { 'c': 7 } }] };
_.unset(object, 'a[0].b.c');
// => true

console.log(object);
// => { 'a': [{ 'b': {} }] };
```

## 访问和检索值

这些函数可帮助您安全地从对象中访问属性，包括嵌套属性。

### at

创建一个包含 `object` 中与 `paths` 对应的值的数组。

#### 参数

| Name    | Type                      | Description                     |
| ------- | ------------------------- | ------------------------------- |
| `object`| `Object`                  | 要遍历的对象。     |
| `[paths]` | `...string`\|`string[]` | 要选取的属性路径。     |

#### 返回值

(`Array`): 返回选取的值。

#### 示例

```javascript
var object = { 'a': [{ 'b': { 'c': 3 } }, 4] };

_.at(object, ['a[0].b.c', 'a[1]']);
// => [3, 4]
```

### get

获取 `object` 中 `path` 路径上的值。如果解析出的值为 `undefined`，则返回 `defaultValue`。

#### 参数

| Name           | Type           | Description                                  |
| -------------- | -------------- | -------------------------------------------- |
| `object`       | `Object`       | 要查询的对象。                         |
| `path`         | `Array`\|`string` | 要获取的属性路径。             |
| `[defaultValue]` | `*`            | `undefined` 的解析值返回的默认值。 |

#### 返回值

(`*`): 返回解析出的值。

#### 示例

```javascript
var object = { 'a': [{ 'b': { 'c': 3 } }] };

_.get(object, 'a[0].b.c');
// => 3

_.get(object, ['a', '0', 'b', 'c']);
// => 3

_.get(object, 'a.b.c', 'default');
// => 'default'
```

### result

此方法类似于 `_.get`，不同之处在于，如果解析出的值是一个函数，则会以其父对象作为 `this` 绑定来调用它，并返回其结果。

#### 参数

| Name           | Type           | Description                                  |
| -------------- | -------------- | -------------------------------------------- |
| `object`       | `Object`       | 要查询的对象。                         |
| `path`         | `Array`\|`string` | 要解析的属性路径。         |
| `[defaultValue]` | `*`            | `undefined` 的解析值返回的默认值。 |

#### 返回值

(`*`): 返回解析出的值。

#### 示例

```javascript
var object = { 'a': [{ 'b': { 'c1': 3, 'c2': _.constant(4) } }] };

_.result(object, 'a[0].b.c1');
// => 3

_.result(object, 'a[0].b.c2');
// => 4

_.result(object, 'a[0].b.c3', 'default');
// => 'default'
```

## 键和值

用于处理对象键和值的函数，例如将它们检索为数组或反转键值对。

### keys

创建一个由 `object` 自身的可枚举属性名组成的数组。

#### 参数

| Name     | Type     | Description            |
| -------- | -------- | ---------------------- |
| `object` | `Object` | 要查询的对象。   |

#### 返回值

(`Array`): 返回属性名数组。

#### 示例

```javascript
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.keys(new Foo());
// => ['a', 'b'] (不保证迭代顺序)

_.keys('hi');
// => ['0', '1']
```

### keysIn

创建一个由 `object` 自身和继承的可枚举属性名组成的数组。

#### 参数

| Name     | Type     | Description            |
| -------- | -------- | ---------------------- |
| `object` | `Object` | 要查询的对象。   |

#### 返回值

(`Array`): 返回属性名数组。

#### 示例

```javascript
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.keysIn(new Foo());
// => ['a', 'b', 'c'] (不保证迭代顺序)
```

### values

创建一个由 `object` 自身的可枚举字符串键属性值组成的数组。

#### 参数

| Name     | Type     | Description            |
| -------- | -------- | ---------------------- |
| `object` | `Object` | 要查询的对象。   |

#### 返回值

(`Array`): 返回属性值数组。

#### 示例

```javascript
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.values(new Foo());
// => [1, 2] (不保证迭代顺序)

_.values('hi');
// => ['h', 'i']
```

### valuesIn

创建一个由 `object` 自身和继承的可枚举字符串键属性值组成的数组。

#### 参数

| Name     | Type     | Description            |
| -------- | -------- | ---------------------- |
| `object` | `Object` | 要查询的对象。   |

#### 返回值

(`Array`): 返回属性值数组。

#### 示例

```javascript
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.valuesIn(new Foo());
// => [1, 2, 3] (不保证迭代顺序)
```

### invert

创建一个由 `object` 的键和值反转组成的对象。如果 `object` 包含重复的值，则后续值会覆盖先前值的属性分配。

#### 参数

| Name     | Type     | Description            |
| -------- | -------- | ---------------------- |
| `object` | `Object` | 要反转的对象。  |

#### 返回值

(`Object`): 返回新的反转对象。

#### 示例

```javascript
var object = { 'a': 1, 'b': 2, 'c': 1 };

_.invert(object);
// => { '1': 'c', '2': 'b' }
```

## 筛选与转换

通过选取或忽略属性，或通过转换键和值来创建新对象。

### pick

创建一个由选取的 `object` 属性组成的对象。

#### 参数

| Name    | Type                      | Description                   |
| ------- | ------------------------- | ----------------------------- |
| `object`| `Object`                  | 源对象。            |
| `[paths]` | `...string`\|`string[]` | 要选取的属性路径。   |

#### 返回值

(`Object`): 返回新对象。

#### 示例

```javascript
var object = { 'a': 1, 'b': '2', 'c': 3 };

_.pick(object, ['a', 'c']);
// => { 'a': 1, 'c': 3 }
```

### omit

与 `_.pick` 相反；此方法创建一个由 `object` 中未被省略的自身和继承的可枚举属性路径组成的对象。

#### 参数

| Name    | Type                      | Description                   |
| ------- | ------------------------- | ----------------------------- |
| `object`| `Object`                  | 源对象。            |
| `[paths]` | `...string`\|`string[]` | 要忽略的属性路径。   |

#### 返回值

(`Object`): 返回新对象。

#### 示例

```javascript
var object = { 'a': 1, 'b': '2', 'c': 3 };

_.omit(object, ['a', 'c']);
// => { 'b': '2' }
```

### transform

作为 `_.reduce` 的替代方法，此方法将 `object` 转换为一个新的 `accumulator` 对象。迭代函数会传入四个参数：`(accumulator, value, key, object)`。

#### 参数

| Name          | Type       | Description                 |
| ------------- | ---------- | --------------------------- |
| `object`      | `Object`   | 要遍历的对象。 |
| `[iteratee]`  | `Function` | 每次迭代调用的函数。 |
| `[accumulator]` | `*`        | 自定义的累加器值。 |

#### 返回值

(`*`): 返回累加后的值。

#### 示例

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

## 检查属性

用于检查对象上是否存在属性的函数。

### has

检查 `path` 是否是 `object` 的直接属性。

#### 参数

| Name    | Type           | Description                |
| ------- | -------------- | -------------------------- |
| `object`| `Object`       | 要查询的对象。       |
| `path`  | `Array`\|`string` | 要检查的路径。         |

#### 返回值

(`boolean`): 如果 `path` 存在，则返回 `true`，否则返回 `false`。

#### 示例

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

### hasIn

检查 `path` 是否是 `object` 的直接或继承属性。

#### 参数

| Name    | Type           | Description                |
| ------- | -------------- | -------------------------- |
| `object`| `Object`       | 要查询的对象。       |
| `path`  | `Array`\|`string` | 要检查的路径。         |

#### 返回值

(`boolean`): 如果 `path` 存在，则返回 `true`，否则返回 `false`。

#### 示例

```javascript
var object = _.create({ 'a': _.create({ 'b': 2 }) });

_.hasIn(object, 'a');
// => true

_.hasIn(object, 'a.b');
// => true

_.hasIn(object, 'b');
// => false
```

---

本指南涵盖了 Lodash 为对象操作提供的广泛函数套件。从简单的属性分配到复杂的转换，这些实用工具可以显著简化您的代码。要了解如何以功能强大、声明式的方式组合这些操作，请参阅关于方法链的 [Seq](./api-seq.md) 指南。