# Math

数学函数库提供了一系列用于执行基本数学运算的实用工具。这些函数涵盖了从简单的加减乘除到更复杂的聚合计算，如求和、平均值、最大值和最小值。

如需处理数字的特定功能（例如范围检查），请参阅 [Number API 参考](./api-number.md)。

---

## `_.add`

计算两个数的和。

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `augend` | `number` | 加数。 |
| `addend` | `number` | 被加数。 |

**返回**

- `(number)`: 返回两个数的和。

**示例**

```javascript
_.add(6, 4);
// => 10
```

---

## `_.ceil`

根据指定的精度向上舍入 `number`。

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `number` | `number` | 要向上舍入的数字。 |
| `[precision=0]` | `number` | 舍入的精度。 |

**返回**

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

## `_.divide`

计算两个数的商。

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `dividend` | `number` | 被除数。 |
| `divisor` | `number` | 除数。 |

**返回**

- `(number)`: 返回两个数的商。

**示例**

```javascript
_.divide(6, 4);
// => 1.5
```

---

## `_.floor`

根据指定的精度向下舍入 `number`。

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `number` | `number` | 要向下舍入的数字。 |
| `[precision=0]` | `number` | 舍入的精度。 |

**返回**

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

## `_.max`

计算数组 `array` 中的最大值。如果 `array` 是空或假值，则返回 `undefined`。

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `array` | `Array` | 要迭代的数组。 |

**返回**

- `(*)`: 返回最大值。

**示例**

```javascript
_.max([4, 2, 8, 6]);
// => 8

_.max([]);
// => undefined
```

---

## `_.maxBy`

此方法类似于 `_.max`，但它接受一个 `iteratee`（迭代函数），该函数会为 `array` 中的每个元素调用，以生成其排序标准。

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `array` | `Array` | 要迭代的数组。 |
| `[iteratee=_.identity]` | `Function` | 每个元素调用的迭代函数。 |

**返回**

- `(*)`: 返回最大值。

**示例**

```javascript
var objects = [{ 'n': 1 }, { 'n': 2 }];

_.maxBy(objects, function(o) { return o.n; });
// => { 'n': 2 }

// 使用 _.property 的简写形式
_.maxBy(objects, 'n');
// => { 'n': 2 }
```

---

## `_.mean`

计算数组 `array` 中值的平均值。

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `array` | `Array` | 要迭代的数组。 |

**返回**

- `(number)`: 返回平均值。

**示例**

```javascript
_.mean([4, 2, 8, 6]);
// => 5
```

---

## `_.meanBy`

此方法类似于 `_.mean`，但它接受一个 `iteratee`（迭代函数），该函数会为 `array` 中的每个元素调用，以生成要计算平均值的值。

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `array` | `Array` | 要迭代的数组。 |
| `[iteratee=_.identity]` | `Function` | 每个元素调用的迭代函数。 |

**返回**

- `(number)`: 返回平均值。

**示例**

```javascript
var objects = [{ 'n': 4 }, { 'n': 2 }, { 'n': 8 }, { 'n': 6 }];

_.meanBy(objects, function(o) { return o.n; });
// => 5

// 使用 _.property 的简写形式
_.meanBy(objects, 'n');
// => 5
```

---

## `_.min`

计算数组 `array` 中的最小值。如果 `array` 是空或假值，则返回 `undefined`。

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `array` | `Array` | 要迭代的数组。 |

**返回**

- `(*)`: 返回最小值。

**示例**

```javascript
_.min([4, 2, 8, 6]);
// => 2

_.min([]);
// => undefined
```

---

## `_.minBy`

此方法类似于 `_.min`，但它接受一个 `iteratee`（迭代函数），该函数会为 `array` 中的每个元素调用，以生成其排序标准。

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `array` | `Array` | 要迭代的数组。 |
| `[iteratee=_.identity]` | `Function` | 每个元素调用的迭代函数。 |

**返回**

- `(*)`: 返回最小值。

**示例**

```javascript
var objects = [{ 'n': 1 }, { 'n': 2 }];

_.minBy(objects, function(o) { return o.n; });
// => { 'n': 1 }

// 使用 _.property 的简写形式
_.minBy(objects, 'n');
// => { 'n': 1 }
```

---

## `_.multiply`

计算两个数的积。

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `multiplier` | `number` | 乘数。 |
| `multiplicand` | `number` | 被乘数。 |

**返回**

- `(number)`: 返回两个数的积。

**示例**

```javascript
_.multiply(6, 4);
// => 24
```

---

## `_.round`

根据指定的精度四舍五入 `number`。

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `number` | `number` | 要舍入的数字。 |
| `[precision=0]` | `number` | 舍入的精度。 |

**返回**

- `(number)`: 返回舍入后的数字。

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

## `_.subtract`

计算两个数的差。

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `minuend` | `number` | 被减数。 |
| `subtrahend` | `number` | 减数。 |

**返回**

- `(number)`: 返回两个数的差。

**示例**

```javascript
_.subtract(6, 4);
// => 2
```

---

## `_.sum`

计算数组 `array` 中值的总和。

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `array` | `Array` | 要迭代的数组。 |

**返回**

- `(number)`: 返回总和。

**示例**

```javascript
_.sum([4, 2, 8, 6]);
// => 20
```

---

## `_.sumBy`

此方法类似于 `_.sum`，但它接受一个 `iteratee`（迭代函数），该函数会为 `array` 中的每个元素调用，以生成要相加的值。

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `array` | `Array` | 要迭代的数组。 |
| `[iteratee=_.identity]` | `Function` | 每个元素调用的迭代函数。 |

**返回**

- `(number)`: 返回总和。

**示例**

```javascript
var objects = [{ 'n': 4 }, { 'n': 2 }, { 'n': 8 }, { 'n': 6 }];

_.sumBy(objects, function(o) { return o.n; });
// => 20

// 使用 _.property 的简写形式
_.sumBy(objects, 'n');
// => 20
```

---

现在您已经了解了数学函数，可以继续探索 [Number API 参考](./api-number.md) 以获取更多数字处理工具。
