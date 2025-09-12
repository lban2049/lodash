# Date

This section provides a detailed reference for Lodash functions that work with Date objects. These utilities help in fetching current timestamps and performing date-related operations.

For more utility functions, you might also be interested in the [Util](./api-util.md) and [Lang](./api-lang.md) API categories.

---

## now

Gets the timestamp of the number of milliseconds that have elapsed since the Unix epoch (1 January 1970 00:00:00 UTC).

### Parameters

This function does not take any parameters.

### Returns

<x-field data-name="timestamp" data-type="number" data-desc="Returns the current timestamp in milliseconds since the Unix epoch."></x-field>

### Example

The `_.now()` function is useful for performance timing and creating unique timestamps.

```javascript Measuring Time icon=logos:javascript
// Defer a function and measure how long it took to execute.
_.defer(function(stamp) {
  console.log(_.now() - stamp);
}, _.now());
// => Logs the number of milliseconds it took for the deferred invocation.
```

---

## Next Steps

After working with dates, you might find these related API sections useful for your projects.

<x-cards>
  <x-card data-title="Function" data-icon="lucide:function-square" data-href="/api/function">
    Discover functions for debouncing, throttling, currying, and more to control function execution.
  </x-card>
  <x-card data-title="Lang" data-icon="lucide:languages" data-href="/api/lang">
    Explore language utilities for type checking, cloning, and type conversion.
  </x-card>
</x-cards>