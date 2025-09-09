# Math

This section provides a detailed reference for Lodash's mathematical utility functions. These functions perform basic arithmetic operations, calculate aggregates like sum and mean, and provide rounding utilities.

For functions that operate on or return numbers in other contexts, see the [Number](./api-number.md) documentation.

---

## _.add

Adds two numbers.

**Since:** 3.4.0

### Parameters

| Name     | Type     | Description                        |
|----------|----------|------------------------------------|
| `augend` | `number` | The first number in an addition.   |
| `addend` | `number` | The second number in an addition.  |

### Returns

- `(number)`: Returns the total.

### Example

```javascript
_.add(6, 4);
// => 10
```

---

## _.ceil

Computes `number` rounded up to `precision`.

**Since:** 3.10.0

### Parameters

| Name        | Type     | Description                   |
|-------------|----------|-------------------------------|
| `number`    | `number` | The number to round up.       |
| `[precision=0]` | `number` | The precision to round up to. |

### Returns

- `(number)`: Returns the rounded up number.

### Example

```javascript
_.ceil(4.006);
// => 5

_.ceil(6.004, 2);
// => 6.01

_.ceil(6040, -2);
// => 6100
```

---

## _.divide

Divides two numbers.

**Since:** 4.7.0

### Parameters

| Name       | Type     | Description                      |
|------------|----------|----------------------------------|
| `dividend` | `number` | The first number in a division.  |
| `divisor`  | `number` | The second number in a division. |

### Returns

- `(number)`: Returns the quotient.

### Example

```javascript
_.divide(6, 4);
// => 1.5
```

---

## _.floor

Computes `number` rounded down to `precision`.

**Since:** 3.10.0

### Parameters

| Name        | Type     | Description                     |
|-------------|----------|---------------------------------|
| `number`    | `number` | The number to round down.       |
| `[precision=0]` | `number` | The precision to round down to. |

### Returns

- `(number)`: Returns the rounded down number.

### Example

```javascript
_.floor(4.006);
// => 4

_.floor(0.046, 2);
// => 0.04

_.floor(4060, -2);
// => 4000
```

---

## _.max

Computes the maximum value of `array`. If `array` is empty or falsey, `undefined` is returned.

**Since:** 0.1.0

### Parameters

| Name    | Type    | Description                 |
|---------|---------|-----------------------------|
| `array` | `Array` | The array to iterate over.  |

### Returns

- `(*)`: Returns the maximum value.

### Example

```javascript
_.max([4, 2, 8, 6]);
// => 8

_.max([]);
// => undefined
```

---

## _.maxBy

This method is like `_.max` except that it accepts `iteratee` which is invoked for each element in `array` to generate the criterion by which the value is ranked. The iteratee is invoked with one argument: (value).

**Since:** 4.0.0

### Parameters

| Name       | Type     | Description                       |
|------------|----------|-----------------------------------|
| `array`    | `Array`  | The array to iterate over.        |
| `[iteratee=_.identity]` | `Function` | The iteratee invoked per element. |

### Returns

- `(*)`: Returns the maximum value.

### Example

```javascript
var objects = [{ 'n': 1 }, { 'n': 2 }];

_.maxBy(objects, function(o) { return o.n; });
// => { 'n': 2 }

// The `_.property` iteratee shorthand.
_.maxBy(objects, 'n');
// => { 'n': 2 }
```

---

## _.mean

Computes the mean of the values in `array`.

**Since:** 4.0.0

### Parameters

| Name    | Type    | Description                 |
|---------|---------|-----------------------------|
| `array` | `Array` | The array to iterate over.  |

### Returns

- `(number)`: Returns the mean.

### Example

```javascript
_.mean([4, 2, 8, 6]);
// => 5
```

---

## _.meanBy

This method is like `_.mean` except that it accepts `iteratee` which is invoked for each element in `array` to generate the value to be averaged. The iteratee is invoked with one argument: (value).

**Since:** 4.7.0

### Parameters

| Name       | Type     | Description                       |
|------------|----------|-----------------------------------|
| `array`    | `Array`  | The array to iterate over.        |
| `[iteratee=_.identity]` | `Function` | The iteratee invoked per element. |

### Returns

- `(number)`: Returns the mean.

### Example

```javascript
var objects = [{ 'n': 4 }, { 'n': 2 }, { 'n': 8 }, { 'n': 6 }];

_.meanBy(objects, function(o) { return o.n; });
// => 5

// The `_.property` iteratee shorthand.
_.meanBy(objects, 'n');
// => 5
```

---

## _.min

Computes the minimum value of `array`. If `array` is empty or falsey, `undefined` is returned.

**Since:** 0.1.0

### Parameters

| Name    | Type    | Description                 |
|---------|---------|-----------------------------|
| `array` | `Array` | The array to iterate over.  |

### Returns

- `(*)`: Returns the minimum value.

### Example

```javascript
_.min([4, 2, 8, 6]);
// => 2

_.min([]);
// => undefined
```

---

## _.minBy

This method is like `_.min` except that it accepts `iteratee` which is invoked for each element in `array` to generate the criterion by which the value is ranked. The iteratee is invoked with one argument: (value).

**Since:** 4.0.0

### Parameters

| Name       | Type     | Description                       |
|------------|----------|-----------------------------------|
| `array`    | `Array`  | The array to iterate over.        |
| `[iteratee=_.identity]` | `Function` | The iteratee invoked per element. |

### Returns

- `(*)`: Returns the minimum value.

### Example

```javascript
var objects = [{ 'n': 1 }, { 'n': 2 }];

_.minBy(objects, function(o) { return o.n; });
// => { 'n': 1 }

// The `_.property` iteratee shorthand.
_.minBy(objects, 'n');
// => { 'n': 1 }
```

---

## _.multiply

Multiplies two numbers.

**Since:** 4.7.0

### Parameters

| Name         | Type     | Description                             |
|--------------|----------|-----------------------------------------|
| `multiplier` | `number` | The first number in a multiplication.   |
| `multiplicand` | `number` | The second number in a multiplication.  |

### Returns

- `(number)`: Returns the product.

### Example

```javascript
_.multiply(6, 4);
// => 24
```

---

## _.round

Computes `number` rounded to `precision`.

**Since:** 3.10.0

### Parameters

| Name        | Type     | Description                |
|-------------|----------|----------------------------|
| `number`    | `number` | The number to round.       |
| `[precision=0]` | `number` | The precision to round to. |

### Returns

- `(number)`: Returns the rounded number.

### Example

```javascript
_.round(4.006);
// => 4

_.round(4.006, 2);
// => 4.01

_.round(4060, -2);
// => 4100
```

---

## _.subtract

Subtracts two numbers.

**Since:** 4.0.0

### Parameters

| Name         | Type     | Description                         |
|--------------|----------|-------------------------------------|
| `minuend`    | `number` | The first number in a subtraction.  |
| `subtrahend` | `number` | The second number in a subtraction. |

### Returns

- `(number)`: Returns the difference.

### Example

```javascript
_.subtract(6, 4);
// => 2
```

---

## _.sum

Computes the sum of the values in `array`.

**Since:** 3.4.0

### Parameters

| Name    | Type    | Description                 |
|---------|---------|-----------------------------|
| `array` | `Array` | The array to iterate over.  |

### Returns

- `(number)`: Returns the sum.

### Example

```javascript
_.sum([4, 2, 8, 6]);
// => 20
```

---

## _.sumBy

This method is like `_.sum` except that it accepts `iteratee` which is invoked for each element in `array` to generate the value to be summed. The iteratee is invoked with one argument: (value).

**Since:** 4.0.0

### Parameters

| Name       | Type     | Description                       |
|------------|----------|-----------------------------------|
| `array`    | `Array`  | The array to iterate over.        |
| `[iteratee=_.identity]` | `Function` | The iteratee invoked per element. |

### Returns

- `(number)`: Returns the sum.

### Example

```javascript
var objects = [{ 'n': 4 }, { 'n': 2 }, { 'n': 8 }, { 'n': 6 }];

_.sumBy(objects, function(o) { return o.n; });
// => 20

// The `_.property` iteratee shorthand.
_.sumBy(objects, 'n');
// => 20
```