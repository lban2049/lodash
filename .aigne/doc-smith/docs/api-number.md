# Number

This section provides a detailed reference for Lodash functions that operate on or return numbers. These utilities help with common numerical tasks like clamping values within a range, checking if a number falls within specific bounds, and generating random numbers.

For mathematical operations, see the [Math](./api-math.md) section.

---

## clamp

Clamps `number` within the inclusive `lower` and `upper` bounds.

**Syntax**
`_.clamp(number, [lower], upper)`

**Arguments**

| Parameter | Type | Description |
| --- | --- | --- |
| `number` | `number` | The number to clamp. |
| `[lower]` | `number` | The lower bound. |
| `upper` | `number` | The upper bound. |

**Returns**

(`number`): Returns the clamped number.

**Example**

```javascript
_.clamp(-10, -5, 5);
// => -5

_.clamp(10, -5, 5);
// => 5
```

---

## inRange

Checks if `n` is between `start` and up to, but not including, `end`. If `end` is not specified, it's set to `start` with `start` then set to `0`. If `start` is greater than `end` the params are swapped to support negative ranges.

**Syntax**
`_.inRange(number, [start=0], end)`

**Arguments**

| Parameter | Type | Description |
| --- | --- | --- |
| `number` | `number` | The number to check. |
| `[start=0]` | `number` | The start of the range. |
| `end` | `number` | The end of the range. |

**Returns**

(`boolean`): Returns `true` if `number` is in the range, else `false`.

**Example**

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

Produces a random number between the inclusive `lower` and `upper` bounds. If only one argument is provided a number between `0` and the given number is returned. If `floating` is `true`, or either `lower` or `upper` are floats, a floating-point number is returned instead of an integer.

**Note:** JavaScript follows the IEEE-754 standard for resolving floating-point values which can produce unexpected results.

**Syntax**
`_.random([lower=0], [upper=1], [floating])`

**Arguments**

| Parameter | Type | Description |
| --- | --- | --- |
| `[lower=0]` | `number` | The lower bound. |
| `[upper=1]` | `number` | The upper bound. |
| `[floating]` | `boolean` | Specify returning a floating-point number. |

**Returns**

(`number`): Returns the random number.

**Example**

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

After reviewing these number utilities, you might want to explore functions for object manipulation in the [Object](./api-object.md) section.