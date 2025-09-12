# Number

Lodash provides utility functions for performing common numerical operations, such as clamping a number within a range, checking if a number falls within a given range, and generating random numbers. These functions are useful for data validation, calculations, and creating dynamic numerical values.

For more advanced mathematical operations, see the [Math API Reference](./api-math.md).

---

## clamp

Clamps a number within the inclusive `lower` and `upper` bounds.

### Parameters

<x-field data-name="number" data-type="number" data-required="true" data-desc="The number to clamp."></x-field>
<x-field data-name="lower" data-type="number" data-required="false" data-desc="The lower bound."></x-field>
<x-field data-name="upper" data-type="number" data-required="true" data-desc="The upper bound."></x-field>

### Returns

<x-field data-name="clampedNumber" data-type="number" data-desc="Returns the clamped number."></x-field>

### Examples

```javascript Clamp a number below the lower bound
_.clamp(-10, -5, 5);
// => -5
```

```javascript Clamp a number above the upper bound
_.clamp(10, -5, 5);
// => 5
```

---

## inRange

Checks if a number is between `start` and up to, but not including, `end`. If `end` is not specified, it's set to `start` with `start` then set to `0`. If `start` is greater than `end` the parameters are swapped to support negative ranges.

### Parameters

<x-field data-name="number" data-type="number" data-required="true" data-desc="The number to check."></x-field>
<x-field data-name="start" data-type="number" data-default="0" data-required="false" data-desc="The start of the range."></x-field>
<x-field data-name="end" data-type="number" data-required="true" data-desc="The end of the range."></x-field>

### Returns

<x-field data-name="isInRange" data-type="boolean" data-desc="Returns true if the number is in the range, else false."></x-field>

### Examples

```javascript Basic usage
_.inRange(3, 2, 4);
// => true
```

```javascript With end omitted
_.inRange(4, 8);
// => true
```

```javascript With swapped bounds
_.inRange(-3, -2, -6);
// => true
```

```javascript With number equal to end
_.inRange(4, 2);
// => false
```

```javascript With float values
_.inRange(1.2, 2);
// => true
```

---

## random

Produces a random number between the inclusive `lower` and `upper` bounds. If only one argument is provided, a number between `0` and the given number is returned. If `floating` is `true`, or either `lower` or `upper` are floats, a floating-point number is returned instead of an integer.

**Note:** JavaScript follows the IEEE-754 standard for resolving floating-point values which can produce unexpected results.

### Parameters

<x-field data-name="lower" data-type="number" data-default="0" data-required="false" data-desc="The lower bound."></x-field>
<x-field data-name="upper" data-type="number" data-default="1" data-required="false" data-desc="The upper bound."></x-field>
<x-field data-name="floating" data-type="boolean" data-required="false" data-desc="Specify returning a floating-point number."></x-field>

### Returns

<x-field data-name="randomNumber" data-type="number" data-desc="Returns the random number."></x-field>

### Examples

```javascript Random integer between 0 and 5
_.random(0, 5);
// => an integer between 0 and 5
```

```javascript Random integer with only upper bound
_.random(5);
// => an integer between 0 and 5
```

```javascript Random floating-point number
_.random(5, true);
// => a floating-point number between 0 and 5
```

```javascript Random floating-point number with float bounds
_.random(1.2, 5.2);
// => a floating-point number between 1.2 and 5.2
```

Now that you understand how to work with numbers, you might want to explore more complex operations in the [Math API Reference](./api-math.md).