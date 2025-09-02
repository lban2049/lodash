# Date

This section details the functions in Lodash for handling dates and timestamps. These utility functions can help you easily get the current time.

Lodash's date functions focus on providing core functionality. For a wider range of utilities, refer to the [Util](./api-util.md) and [Lang](./api-lang.md) sections.

---

## `_.now()`

Gets the timestamp as the number of milliseconds that have elapsed since the Unix epoch (1 January 1970 00:00:00 UTC). This method is a wrapper for `Date.now()`, providing cross-environment consistency.

### Arguments

This function does not accept any arguments.

### Returns

`(number)`: Returns the current timestamp.

### Example

You can use `_.now()` to simply measure the execution time of a code block.

```javascript
const start = _.now();

// Perform some time-consuming operations...
for (let i = 0; i < 1000000; i++) {
  // Simulate work
}

const end = _.now();
const duration = end - start;

console.log(`Operation took: ${duration} milliseconds`);
// => "Operation took: 5 milliseconds" (the specific value will vary depending on the execution environment)
```

Another example is combining it with `_.defer` to check the time difference of a deferred call:

```javascript
_.defer(function(stamp) {
  console.log(_.now() - stamp);
}, _.now());
// => Logs the time difference of the deferred call after about 1ms, e.g., 1
```

---

`_.now` is a simple and efficient method for getting a high-precision timestamp, often used for performance measurement and timing.

After exploring the date functions, you can continue to explore the [Util](./api-util.md) section to learn about more general-purpose helper functions.