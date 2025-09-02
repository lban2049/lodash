# Number

Lodash 提供了一组实用的 Number 函数，用于处理和操作数字。这些函数可以帮助你将数字限制在特定范围内、检查数字是否在指定区间，或生成随机数。

对于更复杂的数学计算，可以参考 [Math](./api-math.md) 部分的文档。

---

## clamp

将 `number` 限制在 `lower` 和 `upper` 两个边界值之间（包含边界值）。

#### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `number` | `number` | 要限制的数字。 |
| `[lower]` | `number` | 下边界。 |
| `upper` | `number` | 上边界。 |

#### 返回

`(number)`: 返回被限制的数字。

#### 示例

```javascript
_.clamp(-10, -5, 5);
// => -5

_.clamp(10, -5, 5);
// => 5
```

---

## inRange

检查 `n` 是否在 `start` 与 `end` 之间，但不包含 `end`。如果 `end` 未指定，则 `start` 被设为 0。如果 `start` 大于 `end`，参数会自动交换以支持负数范围。

#### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `number` | `number` | 要检查的数字。 |
| `[start=0]` | `number` | 范围的起始值。 |
| `end` | `number` | 范围的结束值。 |

#### 返回

`(boolean)`: 如果 `number` 在范围内，则返回 `true`，否则返回 `false`。

#### 示例

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

生成一个介于 `lower` 和 `upper`（包含边界值）之间的随机数。如果只提供一个参数，则返回 0 到该参数之间的数字。如果 `floating` 为 `true`，或者 `lower` 或 `upper` 是浮点数，则返回浮点数。

**注意：** JavaScript 遵循 IEEE-754 标准来解析浮点值，这可能会导致一些意外的结果。

#### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `[lower=0]` | `number` | 下边界。 |
| `[upper=1]` | `number` | 上边界。 |
| `[floating]` | `boolean` | 指定是否返回浮点数。 |

#### 返回

`(number)`: 返回随机数。

#### 示例

```javascript
_.random(0, 5);
// => 0 到 5 之间的整数

_.random(5);
// => 同样是 0 到 5 之间的整数

_.random(5, true);
// => 0 到 5 之间的浮点数

_.random(1.2, 5.2);
// => 1.2 到 5.2 之间的浮点数
```

---

本节介绍了 Lodash 中用于处理数字的核心工具函数。这些函数提供了在日常开发中常见的数字操作的便捷方法。接下来，您可以继续探索 [Object](./api-object.md) 相关的函数，学习如何高效地操作和处理对象。