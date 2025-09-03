# 数学

Lodash 提供了一系列基础的数学工具函数，可用于加法、减法、四舍五入等常见运算，以及从集合中计算最小值、最大值和平均值等聚合值。这些函数能够妥善处理类型转换，并兼具性能和可靠性。

有关更多数字相关的工具函数，请参阅 [Number](./api-number.md) API 参考。

---

## add

将两个数字相加。

**参数**

| Parameter | Type     | Description                      |
| :-------- | :------- | :------------------------------- |
| `augend`  | `number` | 加法运算中的第一个数。 |
| `addend`  | `number` | 加法运算中的第二个数。 |

**返回值**

- `(number)`: 返回总和。

**示例**

```javascript
_.add(6, 4);
// => 10
```

---

## ceil

计算 `number` 向上舍入到 `precision` 的结果。

**参数**

| Parameter      | Type     | Description                        |
| :------------- | :------- | :--------------------------------- |
| `number`       | `number` | 要向上舍入的数字。            |
| `[precision=0]`| `number` | 向上舍入的精度。      |

**返回值**

- `(number)`: 返回向上舍入后的数字。

**示例**

```javascript
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

**参数**

| Parameter  | Type     | Description                      |
| :--------- | :------- | :------------------------------- |
| `dividend` | `number` | 除法运算中的第一个数。  |
| `divisor`  | `number` | 除法运算中的第二个数。 |

**返回值**

- `(number)`: 返回商。

**示例**

```javascript
_.divide(6, 4);
// => 1.5
```

---

## floor

计算 `number` 向下舍入到 `precision` 的结果。

**参数**

| Parameter      | Type     | Description                         |
| :------------- | :------- | :---------------------------------- |
| `number`       | `number` | 要向下舍入的数字。           |
| `[precision=0]`| `number` | 向下舍入的精度。     |

**返回值**

- `(number)`: 返回向下舍入后的数字。

**示例**

```javascript
_.floor(4.006);
// => 4

_.floor(0.046, 2);
// => 0.04

_.floor(4060, -2);
// => 4000
```

---

## max

计算 `array` 中的最大值。如果 `array` 为空或假值，则返回 `undefined`。

**参数**

| Parameter | Type    | Description                   |
| :-------- | :------ | :---------------------------- |
| `array`   | `Array` | 要迭代的数组。    |

**返回值**

- `(*)`: 返回最大值。

**示例**

```javascript
_.max([4, 2, 8, 6]);
// => 8

_.max([]);
// => undefined
```

---

## maxBy

此方法类似于 `_.max`，但它接受一个 `iteratee` 函数。该函数会为 `array` 中的每个元素调用，以生成用于排序的标准。`iteratee` 调用时会传入一个参数：(value)。

**参数**

| Parameter               | Type       | Description                        |
| :---------------------- | :--------- | :--------------------------------- |
| `array`                 | `Array`    | 要迭代的数组。         |
| `[iteratee=_.identity]` | `Function` | 对每个元素调用的 `iteratee` 函数。    |

**返回值**

- `(*)`: 返回最大值。

**示例**

```javascript
var objects = [{ 'n': 1 }, { 'n': 2 }];

_.maxBy(objects, function(o) { return o.n; });
// => { 'n': 2 }

// The `_.property` iteratee shorthand.
_.maxBy(objects, 'n');
// => { 'n': 2 }
```

---

## mean

计算 `array` 中所有值的平均值。

**参数**

| Parameter | Type    | Description                |
| :-------- | :------ | :------------------------- |
| `array`   | `Array` | 要迭代的数组。 |

**返回值**

- `(number)`: 返回平均值。

**示例**

```javascript
_.mean([4, 2, 8, 6]);
// => 5
```

---

## meanBy

此方法类似于 `_.mean`，但它接受一个 `iteratee` 函数。该函数会为 `array` 中的每个元素调用，以生成用于计算平均值的值。`iteratee` 调用时会传入一个参数：(value)。

**参数**

| Parameter               | Type       | Description                     |
| :---------------------- | :--------- | :------------------------------ |
| `array`                 | `Array`    | 要迭代的数组。      |
| `[iteratee=_.identity]` | `Function` | 对每个元素调用的 `iteratee` 函数。 |

**返回值**

- `(number)`: 返回平均值。

**示例**

```javascript
var objects = [{ 'n': 4 }, { 'n': 2 }, { 'n': 8 }, { 'n': 6 }];

_.meanBy(objects, function(o) { return o.n; });
// => 5

// The `_.property` iteratee shorthand.
_.meanBy(objects, 'n');
// => 5
```

---

## min

计算 `array` 中的最小值。如果 `array` 为空或假值，则返回 `undefined`。

**参数**

| Parameter | Type    | Description                   |
| :-------- | :------ | :---------------------------- |
| `array`   | `Array` | 要迭代的数组。    |

**返回值**

- `(*)`: 返回最小值。

**示例**

```javascript
_.min([4, 2, 8, 6]);
// => 2

_.min([]);
// => undefined
```

---

## minBy

此方法类似于 `_.min`，但它接受一个 `iteratee` 函数。该函数会为 `array` 中的每个元素调用，以生成用于排序的标准。`iteratee` 调用时会传入一个参数：(value)。

**参数**

| Parameter               | Type       | Description                        |
| :---------------------- | :--------- | :--------------------------------- |
| `array`                 | `Array`    | 要迭代的数组。         |
| `[iteratee=_.identity]` | `Function` | 对每个元素调用的 `iteratee` 函数。    |

**返回值**

- `(*)`: 返回最小值。

**示例**

```javascript
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

**参数**

| Parameter      | Type     | Description                             |
| :------------- | :------- | :-------------------------------------- |
| `multiplier`   | `number` | 乘法运算中的第一个数。   |
| `multiplicand` | `number` | 乘法运算中的第二个数。  |

**返回值**

- `(number)`: 返回乘积。

**示例**

```javascript
_.multiply(6, 4);
// => 24
```

---

## round

计算 `number` 四舍五入到 `precision` 的结果。

**参数**

| Parameter      | Type     | Description                    |
| :------------- | :------- | :----------------------------- |
| `number`       | `number` | 要进行四舍五入的数字。           |
| `[precision=0]`| `number` | 四舍五入的精度。     |

**返回值**

- `(number)`: 返回四舍五入后的数字。

**示例**

```javascript
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

**参数**

| Parameter    | Type     | Description                          |
| :----------- | :------- | :----------------------------------- |
| `minuend`    | `number` | 减法运算中的第一个数。   |
| `subtrahend` | `number` | 减法运算中的第二个数。  |

**返回值**

- `(number)`: 返回差值。

**示例**

```javascript
_.subtract(6, 4);
// => 2
```

---

## sum

计算 `array` 中所有值的总和。

**参数**

| Parameter | Type    | Description                |
| :-------- | :------ | :------------------------- |
| `array`   | `Array` | 要迭代的数组。 |

**返回值**

- `(number)`: 返回总和。

**示例**

```javascript
_.sum([4, 2, 8, 6]);
// => 20
```

---

## sumBy

此方法类似于 `_.sum`，但它接受一个 `iteratee` 函数。该函数会为 `array` 中的每个元素调用，以生成用于求和的值。`iteratee` 调用时会传入一个参数：(value)。

**参数**

| Parameter               | Type       | Description                     |
| :---------------------- | :--------- | :------------------------------ |
| `array`                 | `Array`    | 要迭代的数组。      |
| `[iteratee=_.identity]` | `Function` | 对每个元素调用的 `iteratee` 函数。 |

**返回值**

- `(number)`: 返回总和。

**示例**

```javascript
var objects = [{ 'n': 4 }, { 'n': 2 }, { 'n': 8 }, { 'n': 6 }];

_.sumBy(objects, function(o) { return o.n; });
// => 20

// The `_.property` iteratee shorthand.
_.sumBy(objects, 'n');
// => 20
```

本节介绍了 Lodash 的核心数学函数。如需了解更多数值运算，请继续阅读 [Number](./api-number.md) API 参考。