# 数字

本节提供了对操作或返回数字的 Lodash 函数的详细参考。这些实用工具可帮助处理常见的数值任务，例如将值限制在某个范围内、检查数字是否在特定边界内以及生成随机数。

有关数学运算，请参阅 [Math](./api-math.md) 部分。

---

## clamp

将 `number` 限制在包含 `lower` 和 `upper` 的边界内。

**语法**
`_.clamp(number, [lower], upper)`

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `number` | `number` | 要限制的数字。 |
| `[lower]` | `number` | 下边界。 |
| `upper` | `number` | 上边界。 |

**返回值**

(`number`): 返回被限制的数字。

**示例**

```javascript
_.clamp(-10, -5, 5);
// => -5

_.clamp(10, -5, 5);
// => 5
```

---

## inRange

检查 `n` 是否在 `start` 与 `end` 之间，但不包括 `end`。如果未指定 `end`，则将其设置为 `start`，并将 `start` 设置为 `0`。如果 `start` 大于 `end`，则交换参数以支持负数范围。

**语法**
`_.inRange(number, [start=0], end)`

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `number` | `number` | 要检查的数字。 |
| `[start=0]` | `number` | 范围的起始值。 |
| `end` | `number` | 范围的结束值。 |

**返回值**

(`boolean`): 如果 `number` 在范围内，则返回 `true`，否则返回 `false`。

**示例**

```javascript
_.inRange(3, 2, 4);
// => true

_.inRange(4, 8);
// => true

_.inRange(4, 2);
// => false

_.inRange(2, 2);
// => false

_.inRange(1.2, 2);
// => true

_.inRange(5.2, 4);
// => false

_.inRange(-3, -2, -6);
// => true
```

---

## random

生成一个介于 `lower` 和 `upper`（包含边界）之间的随机数。如果只提供一个参数，则返回一个介于 `0` 和给定数字之间的数。如果 `floating` 为 `true`，或者 `lower` 或 `upper` 是浮点数，则返回一个浮点数而不是整数。

**注意：** JavaScript 遵循 IEEE-754 标准来解析浮点值，这可能会产生意外结果。

**语法**
`_.random([lower=0], [upper=1], [floating])`

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `[lower=0]` | `number` | 下边界。 |
| `[upper=1]` | `number` | 上边界。 |
| `[floating]` | `boolean` | 指定返回一个浮点数。 |

**返回值**

(`number`): 返回随机数。

**示例**

```javascript
_.random(0, 5);
// => an integer between 0 and 5

_.random(5);
// => also an integer between 0 and 5

_.random(5, true);
// => a floating-point number between 0 and 5

_.random(1.2, 5.2);
// => a floating-point number between 1.2 and 5.2
```

---

在回顾了这些数字实用工具后，您可能想在 [Object](./api-object.md) 部分中探索用于对象操作的函数。