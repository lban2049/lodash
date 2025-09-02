# Math

The math function library provides a series of utility tools for performing basic mathematical operations. These functions cover everything from simple addition, subtraction, multiplication, and division to more complex aggregate calculations, such as sum, average, maximum, and minimum.

For specific functions for handling numbers (e.g., range checking), see the [Number API Reference](./api-number.md).

---

## `_.add`

Computes the sum of two numbers.

**Parameters**

| Parameter | Type | Description |
| --- | --- | --- |
| `augend` | `number` | The augend. |
| `addend` | `number` | The addend. |

**Returns**

- `(number)`: Returns the sum.

**Example**

```javascript
_.add(6, 4);
// => 10
```

---

## `_.ceil`

Rounds `number` up to a given precision.

**Parameters**

| Parameter | Type | Description |
| --- | --- | --- |
| `number` | `number` | The number to round up. |
| `[precision=0]` | `number` | The precision to round up to. |

**Returns**

- `(number)`: Returns the rounded up number.

**Example**

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

Computes the quotient of two numbers.

**Parameters**

| Parameter | Type | Description |
| --- | --- | --- |
| `dividend` | `number` | The dividend. |
| `divisor` | `number` | The divisor. |

**Returns**

- `(number)`: Returns the quotient.

**Example**

```javascript
_.divide(6, 4);
// => 1.5
```

---

## `_.floor`

Rounds `number` down to a given precision.

**Parameters**

| Parameter | Type | Description |
| --- | --- | --- |
| `number` | `number` | The number to round down. |
| `[precision=0]` | `number` | The precision to round down to. |

**Returns**

- `(number)`: Returns the rounded down number.

**Example**

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

Computes the maximum value of `array`. If `array` is empty or falsey, `undefined` is returned.

**Parameters**

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | The array to iterate over. |

**Returns**

- `(*)`: Returns the maximum value.

**Example**

```javascript
_.max([4, 2, 8, 6]);
// => 8

_.max([]);
// => undefined
```

---

## `_.maxBy`

This method is like `_.max` except that it accepts an `iteratee` which is invoked for each element in `array` to generate the criterion to compare.

**Parameters**

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | The array to iterate over. |
| `[iteratee=_.identity]` | `Function` | The iteratee invoked per element. |

**Returns**

- `(*)`: Returns the maximum value.

**Example**

```javascript
var objects = [{ 'n': 1 }, { 'n': 2 }];

_.maxBy(objects, function(o) { return o.n; });
// => { 'n': 2 }

// The `_.property` iteratee shorthand.
_.maxBy(objects, 'n');
// => { 'n': 2 }
```

---

## `_.mean`

Computes the mean of the values in `array`.

**Parameters**

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | The array to iterate over. |

**Returns**

- `(number)`: Returns the mean.

**Example**

```javascript
_.mean([4, 2, 8, 6]);
// => 5
```

---

## `_.meanBy`

This method is like `_.mean` except that it accepts an `iteratee` which is invoked for each element in `array` to generate the value to be averaged.

**Parameters**

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | The array to iterate over. |
| `[iteratee=_.identity]` | `Function` | The iteratee invoked per element. |

**Returns**

- `(number)`: Returns the mean.

**Example**

```javascript
var objects = [{ 'n': 4 }, { 'n': 2 }, { 'n': 8 }, { 'n': 6 }];

_.meanBy(objects, function(o) { return o.n; });
// => 5

// The `_.property` iteratee shorthand.
_.meanBy(objects, 'n');
// => 5
```

---

## `_.min`

Computes the minimum value of `array`. If `array` is empty or falsey, `undefined` is returned.

**Parameters**

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | The array to iterate over. |

**Returns**

- `(*)`: Returns the minimum value.

**Example**

```javascript
_.min([4, 2, 8, 6]);
// => 2

_.min([]);
// => undefined
```

---

## `_.minBy`

This method is like `_.min` except that it accepts an `iteratee` which is invoked for each element in `array` to generate the criterion to compare.

**Parameters**

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | The array to iterate over. |
| `[iteratee=_.identity]` | `Function` | The iteratee invoked per element. |

**Returns**

- `(*)`: Returns the minimum value.

**Example**

```javascript
var objects = [{ 'n': 1 }, { 'n': 2 }];

_.minBy(objects, function(o) { return o.n; });
// => { 'n': 1 }

// The `_.property` iteratee shorthand.
_.minBy(objects, 'n');
// => { 'n': 1 }
```

---

## `_.multiply`

Computes the product of two numbers.

**Parameters**

| Parameter | Type | Description |
| --- | --- | --- |
| `multiplier` | `number` | The multiplier. |
| `multiplicand` | `number` | The multiplicand. |

**Returns**

- `(number)`: Returns the product.

**Example**

```javascript
_.multiply(6, 4);
// => 24
```

---

## `_.round`

Rounds `number` to a given precision.

**Parameters**

| Parameter | Type | Description |
| --- | --- | --- |
| `number` | `number` | The number to round. |
| `[precision=0]` | `number` | The precision to round to. |

**Returns**

- `(number)`: Returns the rounded number.

**Example**

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

Computes the difference of two numbers.

**Parameters**

| Parameter | Type | Description |
| --- | --- | --- |
| `minuend` | `number` | The minuend. |
| `subtrahend` | `number` | The subtrahend. |

**Returns**

- `(number)`: Returns the difference.

**Example**

```javascript
_.subtract(6, 4);
// => 2
```

---

## `_.sum`

Computes the sum of the values in `array`.

**Parameters**

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | The array to iterate over. |

**Returns**

- `(number)`: Returns the sum.

**Example**

```javascript
_.sum([4, 2, 8, 6]);
// => 20
```

---

## `_.sumBy`

This method is like `_.sum` except that it accepts an `iteratee` which is invoked for each element in `array` to generate the value to be summed.

**Parameters**

| Parameter | Type | Description |
| --- | --- | --- |
| `array` | `Array` | The array to iterate over. |
| `[iteratee=_.identity]` | `Function` | The iteratee invoked per element. |

**Returns**

- `(number)`: Returns the sum.

**Example**

```javascript
var objects = [{ 'n': 4 }, { 'n': 2 }, { 'n': 8 }, { 'n': 6 }];

_.sumBy(objects, function(o) { return o.n; });
// => 20

// The `_.property` iteratee shorthand.
_.sumBy(objects, 'n');
// => 20
```

---

Now that you are familiar with the Math functions, you can continue to explore the [Number API Reference](./api-number.md) for more tools for number processing.