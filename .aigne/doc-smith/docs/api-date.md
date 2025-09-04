# Date

This section provides a reference for Lodash functions that work with Date objects. These utilities help in managing time-related data within your applications. For other miscellaneous utilities, you may also find the [Util](./api-util.md) section helpful.

---

## now()

Gets the timestamp of the number of milliseconds that have elapsed since the Unix epoch (1 January 1970 00:00:00 UTC).

### Details

| Detail      | Description                                  |
| :---------- | :------------------------------------------- |
| **Since**   | 2.4.0                                        |
| **Returns** | `(number)`: Returns the current timestamp.   |

### Example

This example uses `_.defer` to show how `_.now()` can be used to measure an interval.

```javascript
_.defer(function(stamp) {
  console.log(_.now() - stamp);
}, _.now());
// => Logs the number of milliseconds it took for the deferred invocation.
```

---

This covers the core date utility in Lodash. For functions that manipulate other data types, please refer back to the main [API Reference](./api.md).