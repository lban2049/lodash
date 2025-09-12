# Math

Lodash's Math functions provide a robust set of utilities for performing common mathematical operations. These functions handle basic arithmetic, rounding, and statistical calculations like finding maximum, minimum, and mean values within collections.

For more specialized numeric operations, you may also want to explore the [Number](./api-number.md) category functions.

---

## add

Adds two numbers.

### Parameters

<x-field data-name="augend" data-type="number" data-required="true" data-desc="The first number in an addition."></x-field>
<x-field data-name="addend" data-type="number" data-required="true" data-desc="The second number in an addition."></x-field>

### Returns

<x-field data-name="" data-type="number" data-desc="Returns the total."></x-field>

### Example

```javascript Add two numbers
_.add(6, 4);
// => 10
```

---

## ceil

Computes `number` rounded up to `precision`.

### Parameters

<x-field data-name="number" data-type="number" data-required="true" data-desc="The number to round up."></x-field>
<x-field data-name="precision" data-type="number" data-default="0" data-desc="The precision to round up to."></x-field>

### Returns

<x-field data-name="" data-type="number" data-desc="Returns the rounded up number."></x-field>

### Example

```javascript Rounding examples
_.ceil(4.006);
// => 5

_.ceil(6.004, 2);
// => 6.01

_.ceil(6040, -2);
// => 6100
```

---

## divide

Divides two numbers.

### Parameters

<x-field data-name="dividend" data-type="number" data-required="true" data-desc="The first number in a division."></x-field>
<x-field data-name="divisor" data-type="number" data-required="true" data-desc="The second number in a division."></x-field>

### Returns

<x-field data-name="" data-type="number" data-desc="Returns the quotient."></x-field>

### Example

```javascript Divide two numbers
_.divide(6, 4);
// => 1.5
```

---

## floor

Computes `number` rounded down to `precision`.

### Parameters

<x-field data-name="number" data-type="number" data-required="true" data-desc="The number to round down."></x-field>
<x-field data-name="precision" data-type="number" data-default="0" data-desc="The precision to round down to."></x-field>

### Returns

<x-field data-name="" data-type="number" data-desc="Returns the rounded down number."></x-field>

### Example

```javascript Rounding down examples
_.floor(4.006);
// => 4

_.floor(0.046, 2);
// => 0.04

_.floor(4060, -2);
// => 4000
```

---

## max

Computes the maximum value of `array`. If `array` is empty or falsey, `undefined` is returned.

### Parameters

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array to iterate over."></x-field>

### Returns

<x-field data-name="" data-type="*" data-desc="Returns the maximum value."></x-field>

### Example

```javascript Find maximum value
_.max([4, 2, 8, 6]);
// => 8

_.max([]);
// => undefined
```

---

## maxBy

This method is like `_.max` except that it accepts `iteratee` which is invoked for each element in `array` to generate the criterion by which the value is ranked.

### Parameters

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array to iterate over."></x-field>
<x-field data-name="iteratee" data-type="Function" data-default="_.identity" data-desc="The iteratee invoked per element."></x-field>

### Returns

<x-field data-name="" data-type="*" data-desc="Returns the maximum value."></x-field>

### Example

```javascript Find maximum value by iteratee
var objects = [{ 'n': 1 }, { 'n': 2 }];

_.maxBy(objects, function(o) { return o.n; });
// => { 'n': 2 }

// The `_.property` iteratee shorthand.
_.maxBy(objects, 'n');
// => { 'n': 2 }
```

---

## mean

Computes the mean of the values in `array`.

### Parameters

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array to iterate over."></x-field>

### Returns

<x-field data-name="" data-type="number" data-desc="Returns the mean."></x-field>

### Example

```javascript Calculate the mean
_.mean([4, 2, 8, 6]);
// => 5
```

---

## meanBy

This method is like `_.mean` except that it accepts `iteratee` which is invoked for each element in `array` to generate the value to be averaged.

### Parameters

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array to iterate over."></x-field>
<x-field data-name="iteratee" data-type="Function" data-default="_.identity" data-desc="The iteratee invoked per element."></x-field>

### Returns

<x-field data-name="" data-type="number" data-desc="Returns the mean."></x-field>

### Example

```javascript Calculate mean by iteratee
var objects = [{ 'n': 4 }, { 'n': 2 }, { 'n': 8 }, { 'n': 6 }];

_.meanBy(objects, function(o) { return o.n; });
// => 5

// The `_.property` iteratee shorthand.
_.meanBy(objects, 'n');
// => 5
```

---

## min

Computes the minimum value of `array`. If `array` is empty or falsey, `undefined` is returned.

### Parameters

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array to iterate over."></x-field>

### Returns

<x-field data-name="" data-type="*" data-desc="Returns the minimum value."></x-field>

### Example

```javascript Find minimum value
_.min([4, 2, 8, 6]);
// => 2

_.min([]);
// => undefined
```

---

## minBy

This method is like `_.min` except that it accepts `iteratee` which is invoked for each element in `array` to generate the criterion by which the value is ranked.

### Parameters

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array to iterate over."></x-field>
<x-field data-name="iteratee" data-type="Function" data-default="_.identity" data-desc="The iteratee invoked per element."></x-field>

### Returns

<x-field data-name="" data-type="*" data-desc="Returns the minimum value."></x-field>

### Example

```javascript Find minimum value by iteratee
var objects = [{ 'n': 1 }, { 'n': 2 }];

_.minBy(objects, function(o) { return o.n; });
// => { 'n': 1 }

// The `_.property` iteratee shorthand.
_.minBy(objects, 'n');
// => { 'n': 1 }
```

---

## multiply

Multiply two numbers.

### Parameters

<x-field data-name="multiplier" data-type="number" data-required="true" data-desc="The first number in a multiplication."></x-field>
<x-field data-name="multiplicand" data-type="number" data-required="true" data-desc="The second number in a multiplication."></x-field>

### Returns

<x-field data-name="" data-type="number" data-desc="Returns the product."></x-field>

### Example

```javascript Multiply two numbers
_.multiply(6, 4);
// => 24
```

---

## round

Computes `number` rounded to `precision`.

### Parameters

<x-field data-name="number" data-type="number" data-required="true" data-desc="The number to round."></x-field>
<x-field data-name="precision" data-type="number" data-default="0" data-desc="The precision to round to."></x-field>

### Returns

<x-field data-name="" data-type="number" data-desc="Returns the rounded number."></x-field>

### Example

```javascript Rounding examples
_.round(4.006);
// => 4

_.round(4.006, 2);
// => 4.01

_.round(4060, -2);
// => 4100
```

---

## subtract

Subtract two numbers.

### Parameters

<x-field data-name="minuend" data-type="number" data-required="true" data-desc="The first number in a subtraction."></x-field>
<x-field data-name="subtrahend" data-type="number" data-required="true" data-desc="The second number in a subtraction."></x-field>

### Returns

<x-field data-name="" data-type="number" data-desc="Returns the difference."></x-field>

### Example

```javascript Subtract two numbers
_.subtract(6, 4);
// => 2
```

---

## sum

Computes the sum of the values in `array`.

### Parameters

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array to iterate over."></x-field>

### Returns

<x-field data-name="" data-type="number" data-desc="Returns the sum."></x-field>

### Example

```javascript Sum an array
_.sum([4, 2, 8, 6]);
// => 20
```

---

## sumBy

This method is like `_.sum` except that it accepts `iteratee` which is invoked for each element in `array` to generate the value to be summed.

### Parameters

<x-field data-name="array" data-type="Array" data-required="true" data-desc="The array to iterate over."></x-field>
<x-field data-name="iteratee" data-type="Function" data-default="_.identity" data-desc="The iteratee invoked per element."></x-field>

### Returns

<x-field data-name="" data-type="number" data-desc="Returns the sum."></x-field>

### Example

```javascript Sum by iteratee
var objects = [{ 'n': 4 }, { 'n': 2 }, { 'n': 8 }, { 'n': 6 }];

_.sumBy(objects, function(o) { return o.n; });
// => 20

// The `_.property` iteratee shorthand.
_.sumBy(objects, 'n');
// => 20
```

After exploring these mathematical utilities, you might find the functions in the [Number](./api-number.md) section useful for more specific numeric checks and transformations.