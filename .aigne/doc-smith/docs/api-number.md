# Number

Lodash provides a set of utility Number functions for working with and manipulating numbers. These functions can help you clamp numbers within a specific range, check if a number is within a given interval, or generate random numbers.

For more complex mathematical computations, refer to the [Math](./api-math.md) documentation.

---

## clamp

Clamps `number` within the inclusive `lower` and `upper` bounds.

#### Parameters

| Name | Type | Description |
|---|---|---|
| `number` | `number` | The number to clamp. |
| `[lower]` | `number` | The lower bound. |
| `upper` | `number` | The upper bound. |

#### Returns

`(number)`: Returns the clamped number.

#### Example

```javascript
_.clamp(-10, -5, 5);
// => -5

_.clamp(10, -5, 5);
// => 5
```

---

## inRange

Checks if `n` is between `start` and up to, but not including, `end`. If `end` is not specified, `start` is set to 0. If `start` is greater than `end`, the parameters are swapped to support negative ranges.

#### Parameters

| Name | Type | Description |
|---|---|---|
| `number` | `number` | The number to check. |
| `[start=0]` | `number` | The start of the range. |
| `end` | `number` | The end of the range. |

#### Returns

`(boolean)`: Returns `true` if `number` is in the range, else `false`.

#### Example

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

Produces a random number between `lower` and `upper` (inclusive). If only one argument is provided, a number between 0 and that number is returned. If `floating` is `true`, or either `lower` or `upper` are floats, a floating-point number is returned.

**Note:** JavaScript follows the IEEE-754 standard for floating-point values, which can lead to some unexpected results.

#### Parameters

| Name | Type | Description |
|---|---|---|
| `[lower=0]` | `number` | The lower bound. |
| `[upper=1]` | `number` | The upper bound. |
| `[floating]` | `boolean` | Specify returning a floating-point number. |

#### Returns

`(number)`: Returns the random number.

#### Example

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

This section introduced the core utility functions in Lodash for handling numbers. These functions provide convenient methods for common number operations in daily development. Next, you can continue to explore the [Object](./api-object.md) related functions to learn how to efficiently manipulate and process objects.