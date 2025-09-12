# 数学

Lodash 的数学函数提供了一套强大的实用工具，用于执行常见的数学运算。这些函数处理基本算术、四舍五入以及统计计算，如在集合中查找最大值、最小值和平均值。

如需更专业的数值运算，你可能还需要了解 [Number](./api-number.md) 分类的函数。

---

## add

将两个数字相加。

### 参数

<x-field data-name="augend" data-type="number" data-required="true" data-desc="加法运算中的第一个数。"></x-field>
<x-field data-name="addend" data-type="number" data-required="true" data-desc="加法运算中的第二个数。"></x-field>

### 返回值

<x-field data-name="" data-type="number" data-desc="返回总和。"></x-field>

### 示例

```javascript 将两个数字相加
_.add(6, 4);
// => 10
```

---

## ceil

计算 `number` 向上舍入到 `precision` 的结果。

### 参数

<x-field data-name="number" data-type="number" data-required="true" data-desc="要向上舍入的数字。"></x-field>
<x-field data-name="precision" data-type="number" data-default="0" data-desc="向上舍入的精度。"></x-field>

### 返回值

<x-field data-name="" data-type="number" data-desc="返回向上舍入后的数字。"></x-field>

### 示例

```javascript 舍入示例
_.ceil(4.006);
// => 5

_.ceil(6.004, 2);
// => 6.01

_.ceil(6040, -2);
// => 6100
```

---

## divide

将两个数字相除。

### 参数

<x-field data-name="dividend" data-type="number" data-required="true" data-desc="除法运算中的第一个数。"></x-field>
<x-field data-name="divisor" data-type="number" data-required="true" data-desc="除法运算中的第二个数。"></x-field>

### 返回值

<x-field data-name="" data-type="number" data-desc="返回商。"></x-field>

### 示例

```javascript 两数相除
_.divide(6, 4);
// => 1.5
```

---

## floor

计算 `number` 向下舍入到 `precision` 的结果。

### 参数

<x-field data-name="number" data-type="number" data-required="true" data-desc="要向下舍入的数字。"></x-field>
<x-field data-name="precision" data-type="number" data-default="0" data-desc="向下舍入的精度。"></x-field>

### 返回值

<x-field data-name="" data-type="number" data-desc="返回向下舍入后的数字。"></x-field>

### 示例

```javascript 向下舍入示例
_.floor(4.006);
// => 4

_.floor(0.046, 2);
// => 0.04

_.floor(4060, -2);
// => 4000
```

---

## max

计算 `array` 的最大值。如果 `array` 为空或假值，则返回 `undefined`。

### 参数

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要迭代的数组。"></x-field>

### 返回值

<x-field data-name="" data-type="*" data-desc="返回最大值。"></x-field>

### 示例

```javascript 查找最大值
_.max([4, 2, 8, 6]);
// => 8

_.max([]);
// => undefined
```

---

## maxBy

此方法类似于 `_.max`，但它接受 `iteratee`，该函数会为 `array` 中的每个元素调用，以生成用于排序的标准。

### 参数

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要迭代的数组。"></x-field>
<x-field data-name="iteratee" data-type="Function" data-default="_.identity" data-desc="每个元素调用的迭代函数。"></x-field>

### 返回值

<x-field data-name="" data-type="*" data-desc="返回最大值。"></x-field>

### 示例

```javascript 通过迭代函数查找最大值
var objects = [{ 'n': 1 }, { 'n': 2 }];

_.maxBy(objects, function(o) { return o.n; });
// => { 'n': 2 }

// The `_.property` iteratee shorthand.
_.maxBy(objects, 'n');
// => { 'n': 2 }
```

---

## mean

计算 `array` 中值的平均值。

### 参数

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要迭代的数组。"></x-field>

### 返回值

<x-field data-name="" data-type="number" data-desc="返回平均值。"></x-field>

### 示例

```javascript 计算平均值
_.mean([4, 2, 8, 6]);
// => 5
```

---

## meanBy

此方法类似于 `_.mean`，但它接受 `iteratee`，该函数会为 `array` 中的每个元素调用，以生成要计算平均值的值。

### 参数

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要迭代的数组。"></x-field>
<x-field data-name="iteratee" data-type="Function" data-default="_.identity" data-desc="每个元素调用的迭代函数。"></x-field>

### 返回值

<x-field data-name="" data-type="number" data-desc="返回平均值。"></x-field>

### 示例

```javascript 通过迭代函数计算平均值
var objects = [{ 'n': 4 }, { 'n': 2 }, { 'n': 8 }, { 'n': 6 }];

_.meanBy(objects, function(o) { return o.n; });
// => 5

// The `_.property` iteratee shorthand.
_.meanBy(objects, 'n');
// => 5
```

---

## min

计算 `array` 的最小值。如果 `array` 为空或假值，则返回 `undefined`。

### 参数

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要迭代的数组。"></x-field>

### 返回值

<x-field data-name="" data-type="*" data-desc="返回最小值。"></x-field>

### 示例

```javascript 查找最小值
_.min([4, 2, 8, 6]);
// => 2

_.min([]);
// => undefined
```

---

## minBy

此方法类似于 `_.min`，但它接受 `iteratee`，该函数会为 `array` 中的每个元素调用，以生成用于排序的标准。

### 参数

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要迭代的数组。"></x-field>
<x-field data-name="iteratee" data-type="Function" data-default="_.identity" data-desc="每个元素调用的迭代函数。"></x-field>

### 返回值

<x-field data-name="" data-type="*" data-desc="返回最小值。"></x-field>

### 示例

```javascript 通过迭代函数查找最小值
var objects = [{ 'n': 1 }, { 'n': 2 }];

_.minBy(objects, function(o) { return o.n; });
// => { 'n': 1 }

// The `_.property` iteratee shorthand.
_.minBy(objects, 'n');
// => { 'n': 1 }
```

---

## multiply

将两个数字相乘。

### 参数

<x-field data-name="multiplier" data-type="number" data-required="true" data-desc="乘法运算中的第一个数。"></x-field>
<x-field data-name="multiplicand" data-type="number" data-required="true" data-desc="乘法运算中的第二个数。"></x-field>

### 返回值

<x-field data-name="" data-type="number" data-desc="返回乘积。"></x-field>

### 示例

```javascript 两数相乘
_.multiply(6, 4);
// => 24
```

---

## round

计算 `number` 四舍五入到 `precision` 的结果。

### 参数

<x-field data-name="number" data-type="number" data-required="true" data-desc="要四舍五入的数字。"></x-field>
<x-field data-name="precision" data-type="number" data-default="0" data-desc="四舍五入的精度。"></x-field>

### 返回值

<x-field data-name="" data-type="number" data-desc="返回四舍五入后的数字。"></x-field>

### 示例

```javascript 舍入示例
_.round(4.006);
// => 4

_.round(4.006, 2);
// => 4.01

_.round(4060, -2);
// => 4100
```

---

## subtract

将两个数字相减。

### 参数

<x-field data-name="minuend" data-type="number" data-required="true" data-desc="减法运算中的第一个数。"></x-field>
<x-field data-name="subtrahend" data-type="number" data-required="true" data-desc="减法运算中的第二个数。"></x-field>

### 返回值

<x-field data-name="" data-type="number" data-desc="返回差值。"></x-field>

### 示例

```javascript 两数相减
_.subtract(6, 4);
// => 2
```

---

## sum

计算 `array` 中值的总和。

### 参数

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要迭代的数组。"></x-field>

### 返回值

<x-field data-name="" data-type="number" data-desc="返回总和。"></x-field>

### 示例

```javascript 对数组求和
_.sum([4, 2, 8, 6]);
// => 20
```

---

## sumBy

此方法类似于 `_.sum`，但它接受 `iteratee`，该函数会为 `array` 中的每个元素调用，以生成要求和的值。

### 参数

<x-field data-name="array" data-type="Array" data-required="true" data-desc="要迭代的数组。"></x-field>
<x-field data-name="iteratee" data-type="Function" data-default="_.identity" data-desc="每个元素调用的迭代函数。"></x-field>

### 返回值

<x-field data-name="" data-type="number" data-desc="返回总和。"></x-field>

### 示例

```javascript 通过迭代函数求和
var objects = [{ 'n': 4 }, { 'n': 2 }, { 'n': 8 }, { 'n': 6 }];

_.sumBy(objects, function(o) { return o.n; });
// => 20

// The `_.property` iteratee shorthand.
_.sumBy(objects, 'n');
// => 20
```

在了解了这些数学实用工具之后，你可能会发现 [Number](./api-number.md) 部分的函数对于更具体的数值检查和转换很有用。