# Number

Lodash provides a set of utility functions for performing common operations on numbers, such as clamping a value within a range or generating random numbers. These functions are designed for convenience and readability in numerical manipulations.

For more advanced mathematical operations, you may also want to explore the [Math](./api-math.md) category.

---

## _.clamp

Clamps `number` within the inclusive `lower` and `upper` bounds.

### Parameters

| Name    | Type     | Description              |
| :------ | :------- | :----------------------- |
| `number`| `number` | The number to clamp.     |
| `lower` | `number` | The lower bound.         |
| `upper` | `number` | The upper bound.         |

### Returns

- `(number)`: Returns the clamped number.

### Example

```javascript
_.clamp(-10, -5, 5);
// => -5

_.clamp(10, -5, 5);
// => 5
```

---

## _.inRange

Checks if `n` is between `start` and up to, but not including, `end`. If `end` is not specified, it's set to `start` with `start` then set to `0`. If `start` is greater than `end` the parameters are swapped to support negative ranges.

### Parameters

| Name     | Type     | Description                    |
| :------- | :------- | :----------------------------- |
| `number` | `number` | The number to check.           |
| `start`  | `number` | The start of the range. (Default: 0) |
| `end`    | `number` | The end of the range.          |

### Returns

- `(boolean)`: Returns `true` if `number` is in the range, else `false`.

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

## _.random

Produces a random number between the inclusive `lower` and `upper` bounds. If only one argument is provided, a number between `0` and the given number is returned. If `floating` is `true`, or either `lower` or `upper` are floats, a floating-point number is returned instead of an integer.

**Note:** JavaScript follows the IEEE-754 standard for resolving floating-point values which can produce unexpected results.

### Parameters

| Name      | Type      | Description                                     |
| :-------- | :-------- | :---------------------------------------------- |
| `lower`   | `number`  | The lower bound. (Default: 0)                   |
| `upper`   | `number`  | The upper bound. (Default: 1)                   |
| `floating`| `boolean` | Specify returning a floating-point number.      |

### Returns

- `(number)`: Returns the random number.

### Example

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

This section covers the number utility functions in Lodash. For mathematical computations, continue to the [Math](./api-math.md) section.