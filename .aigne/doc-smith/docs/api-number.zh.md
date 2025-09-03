# 数字

本节为操作或返回数字的 Lodash 函数提供了详细参考。这些工具可用于将值限制在某个范围内、检查数字是否在特定范围内以及生成随机数。

有关数学运算，请参阅 [Math](./api-math.md) 部分。

---

## clamp

将 `number` 限制在包含 `lower` 和 `upper` 的范围内。

### Parameters

| Name | Type | Description |
|---|---|---|
| `number` | `number` | 要限制的数字。 |
| `[lower]` | `number` | 下限。 |
| `upper` | `number` | 上限。 |

### Returns

`(number)`: 返回被限制的数字。

### Example

```javascript
_.clamp(-10, -5, 5);
// => -5

_.clamp(10, -5, 5);
// => 5
```

---

## inRange

检查 `n` 是否在 `start` 与 `end` 之间，但不包括 `end`。如果未指定 `end`，则其值默认为 `start`，`start` 的值默认为 `0`。如果 `start` 大于 `end`，则交换这两个参数以支持负范围。

### Parameters

| Name | Type | Description |
|---|---|---|
| `number` | `number` | 要检查的数字。 |
| `[start=0]` | `number` | 范围的起始值。 |
| `end` | `number` | 范围的结束值。 |

### Returns

`(boolean)`: 如果 `number` 在范围内，则返回 `true`，否则返回 `false`。

### Example

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

在包含 `lower` 和 `upper` 的范围内生成一个随机数。如果只提供一个参数，则返回 `0` 到该数字之间的一个数。如果 `floating` 为 `true`，或者 `lower` 或 `upper` 是浮点数，则返回一个浮点数而非整数。

**注意：** JavaScript 遵循 IEEE-754 标准来处理浮点值，这可能会产生意想不到的结果。

### Parameters

| Name | Type | Description |
|---|---|---|
| `[lower=0]` | `number` | 下限。 |
| `[upper=1]` | `number` | 上限。 |
| `[floating]` | `boolean` | 指定返回一个浮点数。 |

### Returns

`(number)`: 返回随机数。

### Example

```javascript
_.random(0, 5);
// => 0 到 5 之间的一个整数

_.random(5);
// => 也是 0 到 5 之间的一个整数

_.random(5, true);
// => 0 到 5 之间的一个浮点数

_.random(1.2, 5.2);
// => 1.2 到 5.2 之间的一个浮点数
```

---

本节介绍了 Lodash 中的数字工具函数。如需了解更高级的数值运算，可以接着浏览 [Math](./api-math.md) 函数部分。