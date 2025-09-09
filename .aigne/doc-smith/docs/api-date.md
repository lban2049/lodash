# Date

Lodash provides a utility function for working with dates, primarily for obtaining the current timestamp. This function is useful for performance measurements, logging, or any scenario requiring a high-resolution timestamp.

---

## now

Gets the timestamp of the number of milliseconds that have elapsed since the Unix epoch (1 January 1970 00:00:00 UTC).

This method is a high-resolution alternative to `Date.now()`.

### Parameters

This function does not accept any parameters.

### Returns

(`number`): Returns the current timestamp.

### Example

```javascript icon=logos:javascript
_.defer(function(stamp) {
  console.log(_.now() - stamp);
}, _.now());
// => Logs the number of milliseconds it took for the deferred invocation.
```

---

This section covers Lodash's date utility. For more complex function scheduling related to time, explore the methods in the [Function](./api-function.md) category, such as `_.defer` and `_.delay`.