# 数学

本节提供了 Lodash 数学工具函数的详细参考。这些函数可执行基本算术运算、计算总和与平均值等聚合数据，并提供舍入功能。

如需了解在其他上下文中操作或返回数字的函数，请参阅 [Number](./api-number.md) 文档。

---

## _.add

将两个数字相加。

**版本：** 3.4.0

### 参数

| Name     | Type     | Description                        |
|----------|----------|------------------------------------|
| `augend` | `number` | 加法中的第一个数字。   |
| `addend` | `number` | 加法中的第二个数字。  |

### 返回值

- `(number)`: 返回总和。

### 示例

```javascript
_.add(6, 4);
// => 10
```

---

## _.ceil

计算 `number` 向上舍入到 `precision` 的值。

**版本：** 3.10.0

### 参数

| Name        | Type     | Description                   |
|-------------|----------|-------------------------------|
| `number`    | `number` | 要向上舍入的数字。       |
| `[precision=0]` | `number` | 向上舍入的精度。 |

### 返回值

- `(number)`: 返回向上舍入后的数字。

### 示例

```javascript
_.ceil(4.006);
// => 5

_.ceil(6.004, 2);
// => 6.01

_.ceil(6040, -2);
// => 6100
```

---

## _.divide

将两个数字相除。

**版本：** 4.7.0

### 参数

| Name       | Type     | Description                      |
|------------|----------|----------------------------------|
| `dividend` | `number` | 除法中的第一个数字。  |
| `divisor`  | `number` | 除法中的第二个数字。 |

### 返回值

- `(number)`: 返回商。

### 示例

```javascript
_.divide(6, 4);
// => 1.5
```

---

## _.floor

计算 `number` 向下舍入到 `precision` 的值。

**版本：** 3.10.0

### 参数

| Name        | Type     | Description                     |
|-------------|----------|---------------------------------|
| `number`    | `number` | 要向下舍入的数字。       |
| `[precision=0]` | `number` | 向下舍入的精度。 |

### 返回值

- `(number)`: 返回向下舍入后的数字。

### 示例

```javascript
_.floor(4.006);
// => 4

_.floor(0.046, 2);
// => 0.04

_.floor(4060, -2);
// => 4000
```

---

## _.max

计算 `array` 的最大值。如果 `array` 为空或假值，则返回 `undefined`。

**版本：** 0.1.0

### 参数

| Name    | Type    | Description                 |
|---------|---------|-----------------------------|
| `array` | `Array` | 要迭代的数组。  |

### 返回值

- `(*)`: 返回最大值。

### 示例

```javascript
_.max([4, 2, 8, 6]);
// => 8

_.max([]);
// => undefined
```

---

## _.maxBy

此方法类似于 `_.max`，但它接受一个 `iteratee`，该函数会为 `array` 中的每个元素调用，以生成用于排序的标准。iteratee 调用时会传入一个参数：(value)。

**版本：** 4.0.0

### 参数

| Name       | Type     | Description                       |
|------------|----------|-----------------------------------|
| `array`    | `Array`  | 要迭代的数组。        |
| `[iteratee=_.identity]` | `Function` | 每个元素调用的 iteratee。 |

### 返回值

- `(*)`: 返回最大值。

### 示例

```javascript
var objects = [{ 'n': 1 }, { 'n': 2 }];

_.maxBy(objects, function(o) { return o.n; });
// => { 'n': 2 }

// `_.property` iteratee 的简写。
_.maxBy(objects, 'n');
// => { 'n': 2 }
```

---

## _.mean

计算 `array` 中值的平均值。

**版本：** 4.0.0

### 参数

| Name    | Type    | Description                 |
|---------|---------|-----------------------------|
| `array` | `Array` | 要迭代的数组。  |

### 返回值

- `(number)`: 返回平均值。

### 示例

```javascript
_.mean([4, 2, 8, 6]);
// => 5
```

---

## _.meanBy

此方法类似于 `_.mean`，但它接受一个 `iteratee`，该函数会为 `array` 中的每个元素调用，以生成用于计算平均值的值。iteratee 调用时会传入一个参数：(value)。

**版本：** 4.7.0

### 参数

| Name       | Type     | Description                       |
|------------|----------|-----------------------------------|
| `array`    | `Array`  | 要迭代的数组。        |
| `[iteratee=_.identity]` | `Function` | 每个元素调用的 iteratee。 |

### 返回值

- `(number)`: 返回平均值。

### 示例

```javascript
var objects = [{ 'n': 4 }, { 'n': 2 }, { 'n': 8 }, { 'n': 6 }];

_.meanBy(objects, function(o) { return o.n; });
// => 5

// `_.property` iteratee 的简写。
_.meanBy(objects, 'n');
// => 5
```

---

## _.min

计算 `array` 的最小值。如果 `array` 为空或假值，则返回 `undefined`。

**版本：** 0.1.0

### 参数

| Name    | Type    | Description                 |
|---------|---------|-----------------------------|
| `array` | `Array` | 要迭代的数组。  |

### 返回值

- `(*)`: 返回最小值。

### 示例

```javascript
_.min([4, 2, 8, 6]);
// => 2

_.min([]);
// => undefined
```

---

## _.minBy

此方法类似于 `_.min`，但它接受一个 `iteratee`，该函数会为 `array` 中的每个元素调用，以生成用于排序的标准。iteratee 调用时会传入一个参数：(value)。

**版本：** 4.0.0

### 参数

| Name       | Type     | Description                       |
|------------|----------|-----------------------------------|
| `array`    | `Array`  | 要迭代的数组。        |
| `[iteratee=_.identity]` | `Function` | 每个元素调用的 iteratee。 |

### 返回值

- `(*)`: 返回最小值。

### 示例

```javascript
var objects = [{ 'n': 1 }, { 'n': 2 }];

_.minBy(objects, function(o) { return o.n; });
// => { 'n': 1 }

// `_.property` iteratee 的简写。
_.minBy(objects, 'n');
// => { 'n': 1 }
```

---

## _.multiply

将两个数字相乘。

**版本：** 4.7.0

### 参数

| Name         | Type     | Description                             |
|--------------|----------|-----------------------------------------|
| `multiplier` | `number` | 乘法中的第一个数字。   |
| `multiplicand` | `number` | 乘法中的第二个数字。  |

### 返回值

- `(number)`: 返回乘积。

### 示例

```javascript
_.multiply(6, 4);
// => 24
```

---

## _.round

计算 `number` 四舍五入到 `precision` 的值。

**版本：** 3.10.0

### 参数

| Name        | Type     | Description                |
|-------------|----------|----------------------------|
| `number`    | `number` | 要四舍五入的数字。       |
| `[precision=0]` | `number` | 四舍五入的精度。 |

### 返回值

- `(number)`: 返回四舍五入后的数字。

### 示例

```javascript
_.round(4.006);
// => 4

_.round(4.006, 2);
// => 4.01

_.round(4060, -2);
// => 4100
```

---

## _.subtract

将两个数字相减。

**版本：** 4.0.0

### 参数

| Name         | Type     | Description                         |
|--------------|----------|-------------------------------------|
| `minuend`    | `number` | 减法中的第一个数字。  |
| `subtrahend` | `number` | 减法中的第二个数字。 |

### 返回值

- `(number)`: 返回差值。

### 示例

```javascript
_.subtract(6, 4);
// => 2
```

---

## _.sum

计算 `array` 中值的总和。

**版本：** 3.4.0

### 参数

| Name    | Type    | Description                 |
|---------|---------|-----------------------------|
| `array` | `Array` | 要迭代的数组。  |

### 返回值

- `(number)`: 返回总和。

### 示例

```javascript
_.sum([4, 2, 8, 6]);
// => 20
```

---

## _.sumBy

此方法类似于 `_.sum`，但它接受一个 `iteratee`，该函数会为 `array` 中的每个元素调用，以生成用于求和的值。iteratee 调用时会传入一个参数：(value)。

**版本：** 4.0.0

### 参数

| Name       | Type     | Description                       |
|------------|----------|-----------------------------------|
| `array`    | `Array`  | 要迭代的数组。        |
| `[iteratee=_.identity]` | `Function` | 每个元素调用的 iteratee。 |

### 返回值

- `(number)`: 返回总和。

### 示例

```javascript
var objects = [{ 'n': 4 }, { 'n': 2 }, { 'n': 8 }, { 'n': 6 }];

_.sumBy(objects, function(o) { return o.n; });
// => 20

// `_.property` iteratee 的简写。
_.sumBy(objects, 'n');
// => 20
```