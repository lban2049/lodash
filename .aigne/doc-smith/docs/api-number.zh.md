# 数值

Lodash 提供了用于执行常见数值运算的实用函数，例如将数字限制在一个范围内、检查一个数字是否在给定范围内以及生成随机数。这些函数可用于数据验证、计算和创建动态数值。

如需了解更高级的数学运算，请参阅 [数学 API 参考](./api-math.md)。

---

## clamp

将数字限制在 `lower` 和 `upper` 边界内（包含边界值）。

### 参数

<x-field data-name="number" data-type="number" data-required="true" data-desc="要限制的数字。"></x-field>
<x-field data-name="lower" data-type="number" data-required="false" data-desc="下边界。"></x-field>
<x-field data-name="upper" data-type="number" data-required="true" data-desc="上边界。"></x-field>

### 返回值

<x-field data-name="clampedNumber" data-type="number" data-desc="返回被限制后的数字。"></x-field>

### 示例

```javascript 将小于下边界的数字限制在范围内
_.clamp(-10, -5, 5);
// => -5
```

```javascript 将大于上边界的数字限制在范围内
_.clamp(10, -5, 5);
// => 5
```

---

## inRange

检查一个数字是否在 `start` 和 `end` 之间（不包含 `end`）。如果未指定 `end`，则将其设置为 `start`，然后将 `start` 设置为 `0`。如果 `start` 大于 `end`，则交换参数以支持负数范围。

### 参数

<x-field data-name="number" data-type="number" data-required="true" data-desc="要检查的数字。"></x-field>
<x-field data-name="start" data-type="number" data-default="0" data-required="false" data-desc="范围的起始值。"></x-field>
<x-field data-name="end" data-type="number" data-required="true" data-desc="范围的结束值。"></x-field>

### 返回值

<x-field data-name="isInRange" data-type="boolean" data-desc="如果数字在范围内，则返回 true，否则返回 false。"></x-field>

### 示例

```javascript 基本用法
_.inRange(3, 2, 4);
// => true
```

```javascript 省略 end
_.inRange(4, 8);
// => true
```

```javascript 交换边界
_.inRange(-3, -2, -6);
// => true
```

```javascript 数字等于 end
_.inRange(4, 2);
// => false
```

```javascript 使用浮点数值
_.inRange(1.2, 2);
// => true
```

---

## random

生成一个介于 `lower` 和 `upper` 边界之间（包含边界值）的随机数。如果只提供一个参数，则返回一个介于 `0` 和给定数字之间的数。如果 `floating` 为 `true`，或者 `lower` 或 `upper` 是浮点数，则返回一个浮点数而不是整数。

**注意：** JavaScript 遵循 IEEE-754 标准来处理浮点数值，这可能会产生意想不到的结果。

### 参数

<x-field data-name="lower" data-type="number" data-default="0" data-required="false" data-desc="下边界。"></x-field>
<x-field data-name="upper" data-type="number" data-default="1" data-required="false" data-desc="上边界。"></x-field>
<x-field data-name="floating" data-type="boolean" data-required="false" data-desc="指定返回一个浮点数。"></x-field>

### 返回值

<x-field data-name="randomNumber" data-type="number" data-desc="返回随机数。"></x-field>

### 示例

```javascript 0 到 5 之间的随机整数
_.random(0, 5);
// => an integer between 0 and 5
```

```javascript 只有上边界的随机整数
_.random(5);
// => an integer between 0 and 5
```

```javascript 随机浮点数
_.random(5, true);
// => a floating-point number between 0 and 5
```

```javascript 具有浮点边界的随机浮点数
_.random(1.2, 5.2);
// => a floating-point number between 1.2 and 5.2
```

现在你已经了解了如何处理数字，可能希望在 [数学 API 参考](./api-math.md) 中探索更复杂的操作。