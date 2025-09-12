# 对象

Lodash 提供了一套丰富的函数，用于创建、操作和访问对象的属性。这些实用工具可以帮助简化常见的任务，例如合并、挑选、转换和遍历对象数据。

对于以类似数组的方式遍历对象的函数，你可能也会发现 [Collection](./api-collection.md) 部分的实用工具很有用。

## assign

将源对象自身的可枚举字符串键属性分配给目标对象。源对象从左到右应用。后续源对象的属性会覆盖先前源对象的属性分配。

**注意：** 此方法会改变 `object`，并且大致基于 [`Object.assign`](https://mdn.io/Object/assign)。

*自 0.10.0 版本起*

### 参数

<x-field data-name="object" data-type="Object" data-required="true" data-desc="目标对象。"></x-field>
<x-field data-name="[sources]" data-type="...Object" data-required="false" data-desc="源对象。"></x-field>

### 返回值

<x-field data-name="object" data-type="Object" data-desc="返回 `object`。"></x-field>

### 示例

```javascript icon=logos:javascript
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

此方法类似于 `_.assign`，但它会遍历源对象自身的和继承的属性。

**注意：** 此方法会改变 `object`。

*自 4.0.0 版本起*

*别名：`extend`*

### 参数

<x-field data-name="object" data-type="Object" data-required="true" data-desc="目标对象。"></x-field>
<x-field data-name="[sources]" data-type="...Object" data-required="false" data-desc="源对象。"></x-field>

### 返回值

<x-field data-name="object" data-type="Object" data-desc="返回 `object`。"></x-field>

### 示例

```javascript icon=logos:javascript
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

此方法类似于 `_.assignIn`，但它接受一个 `customizer` 函数，该函数被调用以生成分配的值。如果 `customizer` 返回 `undefined`，则由该方法处理赋值。`customizer` 调用时会传入五个参数：(objValue, srcValue, key, object, source)。

**注意：** 此方法会改变 `object`。

*自 4.0.0 版本起*

*别名：`extendWith`*

### 参数

<x-field data-name="object" data-type="Object" data-required="true" data-desc="目标对象。"></x-field>
<x-field data-name="sources" data-type="...Object" data-required="true" data-desc="源对象。"></x-field>
<x-field data-name="[customizer]" data-type="Function" data-required="false" data-desc="用于自定义赋值的函数。"></x-field>

### 返回值

<x-field data-name="object" data-type="Object" data-desc="返回 `object`。"></x-field>

### 示例

```javascript icon=logos:javascript
function customizer(objValue, srcValue) {
  return _.isUndefined(objValue) ? srcValue : objValue;
}

var defaults = _.partialRight(_.assignInWith, customizer);

defaults({ 'a': 1 }, { 'b': 2 }, { 'a': 3 });
// => { 'a': 1, 'b': 2 }
```

---

## assignWith

此方法类似于 `_.assign`，但它接受一个 `customizer` 函数，该函数被调用以生成分配的值。如果 `customizer` 返回 `undefined`，则由该方法处理赋值。`customizer` 调用时会传入五个参数：(objValue, srcValue, key, object, source)。

**注意：** 此方法会改变 `object`。

*自 4.0.0 版本起*

### 参数

<x-field data-name="object" data-type="Object" data-required="true" data-desc="目标对象。"></x-field>
<x-field data-name="sources" data-type="...Object" data-required="true" data-desc="源对象。"></x-field>
<x-field data-name="[customizer]" data-type="Function" data-required="false" data-desc="用于自定义赋值的函数。"></x-field>

### 返回值

<x-field data-name="object" data-type="Object" data-desc="返回 `object`。"></x-field>

### 示例

```javascript icon=logos:javascript
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

*自 1.0.0 版本起*

### 参数

<x-field data-name="object" data-type="Object" data-required="true" data-desc="要遍历的对象。"></x-field>
<x-field data-name="[paths]" data-type="... (string|string[])" data-required="false" data-desc="要选取的属性路径。"></x-field>

### 返回值

<x-field data-name="" data-type="Array" data-desc="返回选取的值。"></x-field>

### 示例

```javascript icon=logos:javascript
var object = { 'a': [{ 'b': { 'c': 3 } }, 4] };
 
_.at(object, ['a[0].b.c', 'a[1]']);
// => [3, 4]
```

---

## create

创建一个继承自 `prototype` 对象的对象。如果提供了 `properties` 对象，则其自身的可枚举字符串键属性将被分配给创建的对象。

*自 2.3.0 版本起*

### 参数

<x-field data-name="prototype" data-type="Object" data-required="true" data-desc="要继承的对象。"></x-field>
<x-field data-name="[properties]" data-type="Object" data-required="false" data-desc="要分配给对象的属性。"></x-field>

### 返回值

<x-field data-name="" data-type="Object" data-desc="返回新对象。"></x-field>

### 示例

```javascript icon=logos:javascript
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

对于目标对象中所有解析为 `undefined` 的属性，将源对象自身和继承的可枚举字符串键属性分配给目标对象。源对象从左到右应用。一旦某个属性被设置，相同属性的后续值将被忽略。

**注意：** 此方法会改变 `object`。

*自 0.1.0 版本起*

### 参数

<x-field data-name="object" data-type="Object" data-required="true" data-desc="目标对象。"></x-field>
<x-field data-name="[sources]" data-type="...Object" data-required="false" data-desc="源对象。"></x-field>

### 返回值

<x-field data-name="object" data-type="Object" data-desc="返回 `object`。"></x-field>

### 示例

```javascript icon=logos:javascript
_.defaults({ 'a': 1 }, { 'b': 2 }, { 'a': 3 });
// => { 'a': 1, 'b': 2 }
```

---

## defaultsDeep

此方法类似于 `_.defaults`，但它会递归地分配默认属性。

**注意：** 此方法会改变 `object`。

*自 3.10.0 版本起*

### 参数

<x-field data-name="object" data-type="Object" data-required="true" data-desc="目标对象。"></x-field>
<x-field data-name="[sources]" data-type="...Object" data-required="false" data-desc="源对象。"></x-field>

### 返回值

<x-field data-name="object" data-type="Object" data-desc="返回 `object`。"></x-field>

### 示例

```javascript icon=logos:javascript
_.defaultsDeep({ 'a': { 'b': 2 } }, { 'a': { 'b': 1, 'c': 3 } });
// => { 'a': { 'b': 2, 'c': 3 } }
```

---

## findKey

此方法类似于 `_.find`，但它返回第一个 `predicate` 函数返回真值的元素的键，而不是元素本身。

*自 1.1.0 版本起*

### 参数

<x-field data-name="object" data-type="Object" data-required="true" data-desc="要检查的对象。"></x-field>
<x-field data-name="[predicate=_.identity]" data-type="Function" data-required="false" data-desc="每次迭代时调用的函数。"></x-field>

### 返回值

<x-field data-name="" data-type="string|undefined" data-desc="返回匹配元素的键，否则返回 `undefined`。"></x-field>

### 示例

```javascript icon=logos:javascript
var users = {
  'barney':  { 'age': 36, 'active': true },
  'fred':    { 'age': 40, 'active': false },
  'pebbles': { 'age': 1,  'active': true }
};

_.findKey(users, function(o) { return o.age < 40; });
// => 'barney' (不保证迭代顺序)
```

---

## findLastKey

此方法类似于 `_.findKey`，但它以相反的顺序遍历集合的元素。

*自 2.0.0 版本起*

### 参数

<x-field data-name="object" data-type="Object" data-required="true" data-desc="要检查的对象。"></x-field>
<x-field data-name="[predicate=_.identity]" data-type="Function" data-required="false" data-desc="每次迭代时调用的函数。"></x-field>

### 返回值

<x-field data-name="" data-type="string|undefined" data-desc="返回匹配元素的键，否则返回 `undefined`。"></x-field>

### 示例

```javascript icon=logos:javascript
var users = {
  'barney':  { 'age': 36, 'active': true },
  'fred':    { 'age': 40, 'active': false },
  'pebbles': { 'age': 1,  'active': true }
};

_.findLastKey(users, function(o) { return o.age < 40; });
// => 假设 `_.findKey` 返回 'barney'，则返回 'pebbles'
```

---

## get

获取 `object` 中 `path` 路径上的值。如果解析出的值为 `undefined`，则返回 `defaultValue`。

*自 3.7.0 版本起*

### 参数

<x-field data-name="object" data-type="Object" data-required="true" data-desc="要查询的对象。"></x-field>
<x-field data-name="path" data-type="Array|string" data-required="true" data-desc="要获取的属性路径。"></x-field>
<x-field data-name="[defaultValue]" data-type="*" data-required="false" data-desc="为 `undefined` 的解析值返回的值。"></x-field>

### 返回值

<x-field data-name="" data-type="*" data-desc="返回解析出的值。"></x-field>

### 示例

```javascript icon=logos:javascript
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

*自 0.1.0 版本起*

### 参数

<x-field data-name="object" data-type="Object" data-required="true" data-desc="要查询的对象。"></x-field>
<x-field data-name="path" data-type="Array|string" data-required="true" data-desc="要检查的路径。"></x-field>

### 返回值

<x-field data-name="" data-type="boolean" data-desc="如果 `path` 存在，则返回 `true`，否则返回 `false`。"></x-field>

### 示例

```javascript icon=logos:javascript
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

## hasIn

检查 `path` 是否是 `object` 的直接或继承属性。

*自 4.0.0 版本起*

### 参数

<x-field data-name="object" data-type="Object" data-required="true" data-desc="要查询的对象。"></x-field>
<x-field data-name="path" data-type="Array|string" data-required="true" data-desc="要检查的路径。"></x-field>

### 返回值

<x-field data-name="" data-type="boolean" data-desc="如果 `path` 存在，则返回 `true`，否则返回 `false`。"></x-field>

### 示例

```javascript icon=logos:javascript
var object = _.create({ 'a': _.create({ 'b': 2 }) });

_.hasIn(object, 'a');
// => true

_.hasIn(object, 'a.b');
// => true
```

---

## invert

创建一个由 `object` 的键和值反转组成的对象。如果 `object` 包含重复的值，后续的值会覆盖先前值的属性分配。

*自 0.7.0 版本起*

### 参数

<x-field data-name="object" data-type="Object" data-required="true" data-desc="要反转的对象。"></x-field>

### 返回值

<x-field data-name="" data-type="Object" data-desc="返回新的反转对象。"></x-field>

### 示例

```javascript icon=logos:javascript
var object = { 'a': 1, 'b': 2, 'c': 1 };

_.invert(object);
// => { '1': 'c', '2': 'b' }
```

---

## invertBy

此方法类似于 `_.invert`，但反转后的对象是通过对 `object` 的每个元素运行 `iteratee` 函数的结果生成的。每个反转键对应的反转值是一个数组，其中包含生成该反转值的键。iteratee 调用时会传入一个参数：(value)。

*自 4.1.0 版本起*

### 参数

<x-field data-name="object" data-type="Object" data-required="true" data-desc="要反转的对象。"></x-field>
<x-field data-name="[iteratee=_.identity]" data-type="Function" data-required="false" data-desc="每个元素调用的 iteratee 函数。"></x-field>

### 返回值

<x-field data-name="" data-type="Object" data-desc="返回新的反转对象。"></x-field>

### 示例

```javascript icon=logos:javascript
var object = { 'a': 1, 'b': 2, 'c': 1 };

_.invertBy(object, function(value) {
  return 'group' + value;
});
// => { 'group1': ['a', 'c'], 'group2': ['b'] }
```

---

## keys

创建一个由 `object` 自身的可枚举属性名组成的数组。

**注意：** 非对象值会被强制转换成对象。

*自 0.1.0 版本起*

### 参数

<x-field data-name="object" data-type="Object" data-required="true" data-desc="要查询的对象。"></x-field>

### 返回值

<x-field data-name="" data-type="Array" data-desc="返回属性名数组。"></x-field>

### 示例

```javascript icon=logos:javascript
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.keys(new Foo);
// => ['a', 'b'] (不保证迭代顺序)

_.keys('hi');
// => ['0', '1']
```

---

## keysIn

创建一个由 `object` 自身和继承的可枚举属性名组成的数组。

**注意：** 非对象值会被强制转换成对象。

*自 3.0.0 版本起*

### 参数

<x-field data-name="object" data-type="Object" data-required="true" data-desc="要查询的对象。"></x-field>

### 返回值

<x-field data-name="" data-type="Array" data-desc="返回属性名数组。"></x-field>

### 示例

```javascript icon=logos:javascript
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.keysIn(new Foo);
// => ['a', 'b', 'c'] (不保证迭代顺序)
```

---

## mapKeys

与 `_.mapValues` 相反；此方法创建一个与 `object` 具有相同值的新对象，其键是通过对 `object` 自身的每个可枚举字符串键属性运行 `iteratee` 函数生成的。iteratee 调用时会传入三个参数：(value, key, object)。

*自 3.8.0 版本起*

### 参数

<x-field data-name="object" data-type="Object" data-required="true" data-desc="要遍历的对象。"></x-field>
<x-field data-name="[iteratee=_.identity]" data-type="Function" data-required="false" data-desc="每次迭代时调用的函数。"></x-field>

### 返回值

<x-field data-name="" data-type="Object" data-desc="返回新的映射对象。"></x-field>

### 示例

```javascript icon=logos:javascript
_.mapKeys({ 'a': 1, 'b': 2 }, function(value, key) {
  return key + value;
});
// => { 'a1': 1, 'b2': 2 }
```

---

## mapValues

创建一个与 `object` 具有相同键的新对象，其值是通过对 `object` 自身的每个可枚举字符串键属性运行 `iteratee` 函数生成的。iteratee 调用时会传入三个参数：(value, key, object)。

*自 2.4.0 版本起*

### 参数

<x-field data-name="object" data-type="Object" data-required="true" data-desc="要遍历的对象。"></x-field>
<x-field data-name="[iteratee=_.identity]" data-type="Function" data-required="false" data-desc="每次迭代时调用的函数。"></x-field>

### 返回值

<x-field data-name="" data-type="Object" data-desc="返回新的映射对象。"></x-field>

### 示例

```javascript icon=logos:javascript
var users = {
  'fred':    { 'user': 'fred',    'age': 40 },
  'pebbles': { 'user': 'pebbles', 'age': 1 }
};

_.mapValues(users, function(o) { return o.age; });
// => { 'fred': 40, 'pebbles': 1 } (不保证迭代顺序)

// `_.property` iteratee 的简写形式。
_.mapValues(users, 'age');
// => { 'fred': 40, 'pebbles': 1 }
```

---

## merge

此方法类似于 `_.assign`，但它会递归地将源对象自身和继承的可枚举字符串键属性合并到目标对象中。如果目标值已存在，则会跳过解析为 `undefined` 的源属性。数组和纯对象属性会递归合并。其他对象和值类型会通过赋值被覆盖。源对象从左到右应用。后续源对象的属性会覆盖先前源对象的属性分配。

**注意：** 此方法会改变 `object`。

*自 0.5.0 版本起*

### 参数

<x-field data-name="object" data-type="Object" data-required="true" data-desc="目标对象。"></x-field>
<x-field data-name="[sources]" data-type="...Object" data-required="false" data-desc="源对象。"></x-field>

### 返回值

<x-field data-name="object" data-type="Object" data-desc="返回 `object`。"></x-field>

### 示例

```javascript icon=logos:javascript
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

此方法类似于 `_.merge`，但它接受一个 `customizer` 函数，该函数被调用以生成目标属性和源属性的合并值。如果 `customizer` 返回 `undefined`，则由该方法处理合并。`customizer` 调用时会传入六个参数：(objValue, srcValue, key, object, source, stack)。

**注意：** 此方法会改变 `object`。

*自 4.0.0 版本起*

### 参数

<x-field data-name="object" data-type="Object" data-required="true" data-desc="目标对象。"></x-field>
<x-field data-name="sources" data-type="...Object" data-required="true" data-desc="源对象。"></x-field>
<x-field data-name="customizer" data-type="Function" data-required="true" data-desc="用于自定义赋值的函数。"></x-field>

### 返回值

<x-field data-name="object" data-type="Object" data-desc="返回 `object`。"></x-field>

### 示例

```javascript icon=logos:javascript
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

与 `_.pick` 相反；此方法创建一个由 `object` 中未被忽略的自身和继承的可枚举属性路径组成的对象。

**注意：** 此方法比 `_.pick` 慢得多。

*自 0.1.0 版本起*

### 参数

<x-field data-name="object" data-type="Object" data-required="true" data-desc="源对象。"></x-field>
<x-field data-name="[paths]" data-type="... (string|string[])" data-required="false" data-desc="要忽略的属性路径。"></x-field>

### 返回值

<x-field data-name="" data-type="Object" data-desc="返回新对象。"></x-field>

### 示例

```javascript icon=logos:javascript
var object = { 'a': 1, 'b': '2', 'c': 3 };

_.omit(object, ['a', 'c']);
// => { 'b': '2' }
```

---

## omitBy

与 `_.pickBy` 相反；此方法创建一个由 `object` 自身和继承的可枚举字符串键属性组成的对象，这些属性的 `predicate` 函数不会返回真值。predicate 调用时会传入两个参数：(value, key)。

*自 4.0.0 版本起*

### 参数

<x-field data-name="object" data-type="Object" data-required="true" data-desc="源对象。"></x-field>
<x-field data-name="[predicate=_.identity]" data-type="Function" data-required="false" data-desc="每个属性调用的函数。"></x-field>

### 返回值

<x-field data-name="" data-type="Object" data-desc="返回新对象。"></x-field>

### 示例

```javascript icon=logos:javascript
var object = { 'a': 1, 'b': '2', 'c': 3 };

_.omitBy(object, _.isNumber);
// => { 'b': '2' }
```

---

## pick

创建一个由选取的 `object` 属性组成的对象。

*自 0.1.0 版本起*

### 参数

<x-field data-name="object" data-type="Object" data-required="true" data-desc="源对象。"></x-field>
<x-field data-name="[paths]" data-type="... (string|string[])" data-required="false" data-desc="要选取的属性路径。"></x-field>

### 返回值

<x-field data-name="" data-type="Object" data-desc="返回新对象。"></x-field>

### 示例

```javascript icon=logos:javascript
var object = { 'a': 1, 'b': '2', 'c': 3 };

_.pick(object, ['a', 'c']);
// => { 'a': 1, 'c': 3 }
```

---

## pickBy

创建一个由 `object` 属性中 `predicate` 返回真值的属性组成的对象。predicate 调用时会传入两个参数：(value, key)。

*自 4.0.0 版本起*

### 参数

<x-field data-name="object" data-type="Object" data-required="true" data-desc="源对象。"></x-field>
<x-field data-name="[predicate=_.identity]" data-type="Function" data-required="false" data-desc="每个属性调用的函数。"></x-field>

### 返回值

<x-field data-name="" data-type="Object" data-desc="返回新对象。"></x-field>

### 示例

```javascript icon=logos:javascript
var object = { 'a': 1, 'b': '2', 'c': 3 };

_.pickBy(object, _.isNumber);
// => { 'a': 1, 'c': 3 }
```

---

## result

此方法类似于 `_.get`，但如果解析出的值是一个函数，它会以其父对象的 `this` 绑定被调用，并返回其结果。

*自 0.1.0 版本起*

### 参数

<x-field data-name="object" data-type="Object" data-required="true" data-desc="要查询的对象。"></x-field>
<x-field data-name="path" data-type="Array|string" data-required="true" data-desc="要解析的属性路径。"></x-field>
<x-field data-name="[defaultValue]" data-type="*" data-required="false" data-desc="为 `undefined` 的解析值返回的值。"></x-field>

### 返回值

<x-field data-name="" data-type="*" data-desc="返回解析出的值。"></x-field>

### 示例

```javascript icon=logos:javascript
var object = { 'a': [{ 'b': { 'c1': 3, 'c2': _.constant(4) } }] };

_.result(object, 'a[0].b.c1');
// => 3

_.result(object, 'a[0].b.c2');
// => 4
```

---

## set

设置 `object` 中 `path` 路径上的值。如果 `path` 的一部分不存在，则会被创建。对于缺失的索引属性会创建数组，对于所有其他缺失的属性会创建对象。使用 `_.setWith` 可以自定义 `path` 的创建过程。

**注意：** 此方法会改变 `object`。

*自 3.7.0 版本起*

### 参数

<x-field data-name="object" data-type="Object" data-required="true" data-desc="要修改的对象。"></x-field>
<x-field data-name="path" data-type="Array|string" data-required="true" data-desc="要设置的属性路径。"></x-field>
<x-field data-name="value" data-type="*" data-required="true" data-desc="要设置的值。"></x-field>

### 返回值

<x-field data-name="object" data-type="Object" data-desc="返回 `object`。"></x-field>

### 示例

```javascript icon=logos:javascript
var object = { 'a': [{ 'b': { 'c': 3 } }] };
 
_.set(object, 'a[0].b.c', 4);
console.log(object.a[0].b.c);
// => 4
```

---

## setWith

此方法类似于 `_.set`，但它接受一个 `customizer` 函数，该函数被调用以生成 `path` 中的对象。如果 `customizer` 返回 `undefined`，则由该方法处理路径创建。`customizer` 调用时会传入三个参数：(nsValue, key, nsObject)。

**注意：** 此方法会改变 `object`。

*自 4.0.0 版本起*

### 参数

<x-field data-name="object" data-type="Object" data-required="true" data-desc="要修改的对象。"></x-field>
<x-field data-name="path" data-type="Array|string" data-required="true" data-desc="要设置的属性路径。"></x-field>
<x-field data-name="value" data-type="*" data-required="true" data-desc="要设置的值。"></x-field>
<x-field data-name="[customizer]" data-type="Function" data-required="false" data-desc="用于自定义赋值的函数。"></x-field>

### 返回值

<x-field data-name="object" data-type="Object" data-desc="返回 `object`。"></x-field>

### 示例

```javascript icon=logos:javascript
var object = {};

_.setWith(object, '[0][1]', 'a', Object);
// => { '0': { '1': 'a' } }
```

---

## toPairs

为 `object` 创建一个由自身可枚举的字符串键值对组成的数组，该数组可被 `_.fromPairs` 使用。如果 `object` 是一个 map 或 set，则返回其条目。

*自 4.0.0 版本起*

*别名：`entries`*

### 参数

<x-field data-name="object" data-type="Object" data-required="true" data-desc="要查询的对象。"></x-field>

### 返回值

<x-field data-name="" data-type="Array" data-desc="返回键值对数组。"></x-field>

### 示例

```javascript icon=logos:javascript
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.toPairs(new Foo);
// => [['a', 1], ['b', 2]] (不保证迭代顺序)
```

---

## toPairsIn

为 `object` 创建一个由自身和继承的可枚举字符串键值对组成的数组，该数组可被 `_.fromPairs` 使用。如果 `object` 是一个 map 或 set，则返回其条目。

*自 4.0.0 版本起*

*别名：`entriesIn`*

### 参数

<x-field data-name="object" data-type="Object" data-required="true" data-desc="要查询的对象。"></x-field>

### 返回值

<x-field data-name="" data-type="Array" data-desc="返回键值对数组。"></x-field>

### 示例

```javascript icon=logos:javascript
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.toPairsIn(new Foo);
// => [['a', 1], ['b', 2], ['c', 3]] (不保证迭代顺序)
```

---

## transform

`_.reduce` 的一个替代方法；此方法将 `object` 转换为一个新的 `accumulator` 对象，该对象是通过对 `object` 自身的每个可枚举字符串键属性运行 `iteratee` 函数的结果，每次调用都可能改变 `accumulator` 对象。如果没有提供 `accumulator`，将使用一个具有相同 `[[Prototype]]` 的新对象。iteratee 调用时会传入四个参数：(accumulator, value, key, object)。Iteratee 函数可以通过显式返回 `false` 来提前退出迭代。

*自 1.3.0 版本起*

### 参数

<x-field data-name="object" data-type="Object" data-required="true" data-desc="要遍历的对象。"></x-field>
<x-field data-name="[iteratee=_.identity]" data-type="Function" data-required="false" data-desc="每次迭代时调用的函数。"></x-field>
<x-field data-name="[accumulator]" data-type="*" data-required="false" data-desc="自定义的累加器值。"></x-field>

### 返回值

<x-field data-name="" data-type="*" data-desc="返回累加后的值。"></x-field>

### 示例

```javascript icon=logos:javascript
_.transform({ 'a': 1, 'b': 2, 'c': 1 }, function(result, value, key) {
  (result[value] || (result[value] = [])).push(key);
}, {});
// => { '1': ['a', 'c'], '2': ['b'] }
```

---

## unset

移除 `object` 中 `path` 路径上的属性。

**注意：** 此方法会改变 `object`。

*自 4.0.0 版本起*

### 参数

<x-field data-name="object" data-type="Object" data-required="true" data-desc="要修改的对象。"></x-field>
<x-field data-name="path" data-type="Array|string" data-required="true" data-desc="要移除的属性路径。"></x-field>

### 返回值

<x-field data-name="" data-type="boolean" data-desc="如果属性被删除，则返回 `true`，否则返回 `false`。"></x-field>

### 示例

```javascript icon=logos:javascript
var object = { 'a': [{ 'b': { 'c': 7 } }] };
_.unset(object, 'a[0].b.c');
// => true

console.log(object);
// => { 'a': [{ 'b': {} }] };
```

---

## update

此方法类似于 `_.set`，但它接受一个 `updater` 函数来生成要设置的值。使用 `_.updateWith` 可以自定义 `path` 的创建过程。`updater` 调用时会传入一个参数：(value)。

**注意：** 此方法会改变 `object`。

*自 4.6.0 版本起*

### 参数

<x-field data-name="object" data-type="Object" data-required="true" data-desc="要修改的对象。"></x-field>
<x-field data-name="path" data-type="Array|string" data-required="true" data-desc="要设置的属性路径。"></x-field>
<x-field data-name="updater" data-type="Function" data-required="true" data-desc="用于生成更新值的函数。"></x-field>

### 返回值

<x-field data-name="object" data-type="Object" data-desc="返回 `object`。"></x-field>

### 示例

```javascript icon=logos:javascript
var object = { 'a': [{ 'b': { 'c': 3 } }] };

_.update(object, 'a[0].b.c', function(n) { return n * n; });
console.log(object.a[0].b.c);
// => 9
```

---

## updateWith

此方法类似于 `_.update`，但它接受一个 `customizer` 函数，该函数被调用以生成 `path` 中的对象。如果 `customizer` 返回 `undefined`，则由该方法处理路径创建。`customizer` 调用时会传入三个参数：(nsValue, key, nsObject)。

**注意：** 此方法会改变 `object`。

*自 4.6.0 版本起*

### 参数

<x-field data-name="object" data-type="Object" data-required="true" data-desc="要修改的对象。"></x-field>
<x-field data-name="path" data-type="Array|string" data-required="true" data-desc="要设置的属性路径。"></x-field>
<x-field data-name="updater" data-type="Function" data-required="true" data-desc="用于生成更新值的函数。"></x-field>
<x-field data-name="[customizer]" data-type="Function" data-required="false" data-desc="用于自定义赋值的函数。"></x-field>

### 返回值

<x-field data-name="object" data-type="Object" data-desc="返回 `object`。"></x-field>

### 示例

```javascript icon=logos:javascript
var object = {};

_.updateWith(object, '[0][1]', _.constant('a'), Object);
// => { '0': { '1': 'a' } }
```

---

## values

创建一个由 `object` 自身的可枚举字符串键属性值组成的数组。

**注意：** 非对象值会被强制转换成对象。

*自 0.1.0 版本起*

### 参数

<x-field data-name="object" data-type="Object" data-required="true" data-desc="要查询的对象。"></x-field>

### 返回值

<x-field data-name="" data-type="Array" data-desc="返回属性值数组。"></x-field>

### 示例

```javascript icon=logos:javascript
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.values(new Foo);
// => [1, 2] (不保证迭代顺序)

_.values('hi');
// => ['h', 'i']
```

---

## valuesIn

创建一个由 `object` 自身和继承的可枚举字符串键属性值组成的数组。

**注意：** 非对象值会被强制转换成对象。

*自 3.0.0 版本起*

### 参数

<x-field data-name="object" data-type="Object" data-required="true" data-desc="要查询的对象。"></x-field>

### 返回值

<x-field data-name="" data-type="Array" data-desc="返回属性值数组。"></x-field>

### 示例

```javascript icon=logos:javascript
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.valuesIn(new Foo);
// => [1, 2, 3] (不保证迭代顺序)
```
