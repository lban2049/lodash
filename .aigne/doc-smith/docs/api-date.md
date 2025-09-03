# Date

Lodash provides utility functions for working with JavaScript's `Date` objects. These helpers simplify common date-related tasks, such as retrieving the current timestamp.

For functions that help manage the timing of function execution, such as `_.defer` and `_.delay`, please see the [Function documentation](./api-function.md).

---

## now()

Gets the timestamp of the number of milliseconds that have elapsed since the Unix epoch (1 January 1970 00:00:00 UTC).

### Parameters

This method does not accept any parameters.

### Returns

| Type | Description |
|---|---|
| `number` | Returns the current timestamp as a number. |

### Example

```javascript
_.defer(function(stamp) {
  console.log(_.now() - stamp);
}, _.now());

// => Logs the number of milliseconds it took for the deferred invocation.
```

The example above demonstrates how to measure the time elapsed for a deferred operation. It captures an initial timestamp with `_.now()`, then calculates the difference after the deferred function executes.