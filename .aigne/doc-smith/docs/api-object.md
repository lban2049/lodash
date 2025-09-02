# Object

Lodash provides numerous functions for manipulating and processing JavaScript objects. These utilities help you merge, transform, select, inspect, and set object properties, forming a core part of data processing workflows. These functions focus on handling both own and inherited properties of objects, offering more powerful and flexible capabilities than native JavaScript.

For more information on iterating over objects and arrays, see the functions in the [Collection](./api-collection.md) section.

---

## assign

Assigns own enumerable string-keyed properties of one or more source objects to a destination object. Source objects are applied from left to right. Subsequent sources overwrite property assignments of previous sources.

**Note:** This method mutates `object`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | The destination object. |
| `[sources]` | `...Object` | One or more source objects. |

**Returns**

- `(Object)`: Returns the mutated `object`.

**Example**

```javascript
function Foo() {
  this.a = 1;
}

function Bar() {
  this.c = 3;
}

Foo.prototype.b = 2;
Bar.prototype.d = 4;

_.assign({ 'a': 0 }, new Foo, new Bar);
// => { 'a': 1, 'c': 3 }
```

---

## assignIn

This method is like `_.assign`, except that it iterates over own and inherited source properties. Aliased as `_.extend`.

**Note:** This method mutates `object`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | The destination object. |
| `[sources]` | `...Object` | One or more source objects. |

**Returns**

- `(Object)`: Returns `object`.

**Example**

```javascript
function Foo() {
  this.a = 1;
}

function Bar() {
  this.c = 3;
}

Foo.prototype.b = 2;
Bar.prototype.d = 4;

_.assignIn({ 'a': 0 }, new Foo, new Bar);
// => { 'a': 1, 'b': 2, 'c': 3, 'd': 4 }
```

---

## assignInWith

This method is like `_.assignIn`, except that it accepts a `customizer` which is invoked to produce the assigned values. If `customizer` returns `undefined`, assignment is handled by the method instead. The `customizer` is invoked with five arguments: (objValue, srcValue, key, object, source).

**Note:** This method mutates `object`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | The destination object. |
| `sources` | `...Object` | One or more source objects. |
| `[customizer]` | `Function` | The function to customize assigned values. |

**Returns**

- `(Object)`: Returns `object`.

**Example**

```javascript
function customizer(objValue, srcValue) {
  return _.isUndefined(objValue) ? srcValue : objValue;
}

var defaults = _.partialRight(_.assignInWith, customizer);

defaults({ 'a': 1 }, { 'b': 2 }, { 'a': 3 });
// => { 'a': 1, 'b': 2 }
```

---

## assignWith

This method is like `_.assign`, except that it accepts a `customizer` which is invoked to produce the assigned values. If `customizer` returns `undefined`, assignment is handled by the method instead. The `customizer` is invoked with five arguments: (objValue, srcValue, key, object, source).

**Note:** This method mutates `object`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | The destination object. |
| `sources` | `...Object` | One or more source objects. |
| `[customizer]` | `Function` | The function to customize assigned values. |

**Returns**

- `(Object)`: Returns `object`.

**Example**

```javascript
function customizer(objValue, srcValue) {
  return _.isUndefined(objValue) ? srcValue : objValue;
}

var defaults = _.partialRight(_.assignWith, customizer);

defaults({ 'a': 1 }, { 'b': 2 }, { 'a': 3 });
// => { 'a': 1, 'b': 2 }
```

---

## at

Creates an array of values corresponding to `paths` of `object`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | The object to iterate over. |
| `[paths]` | `...(string|string[])` | The property paths to pick. |

**Returns**

- `(Array)`: Returns the picked values.

**Example**

```javascript
var object = { 'a': [{ 'b': { 'c': 3 } }, 4] };

_.at(object, ['a[0].b.c', 'a[1]']);
// => [3, 4]
```

---

## create

Creates an object that inherits from the `prototype` object. If a `properties` object is provided, its own enumerable string-keyed properties are assigned to the created object.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `prototype` | `Object` | The object to inherit from. |
| `[properties]` | `Object` | The properties to assign to the new object. |

**Returns**

- `(Object)`: Returns the new object.

**Example**

```javascript
function Shape() {
  this.x = 0;
  this.y = 0;
}

function Circle() {
  Shape.call(this);
}

Circle.prototype = _.create(Shape.prototype, {
  'constructor': Circle
});

var circle = new Circle;
circle instanceof Circle;
// => true

circle instanceof Shape;
// => true
```

---

## defaults

Assigns own enumerable string-keyed properties of source objects to the destination object for all destination properties that are `undefined`. Source objects are applied from left to right. Once a property is set, additional values of the same property are ignored.

**Note:** This method mutates `object`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | The destination object. |
| `[sources]` | `...Object` | One or more source objects. |

**Returns**

- `(Object)`: Returns `object`.

**Example**

```javascript
_.defaults({ 'a': 1 }, { 'b': 2 }, { 'a': 3 });
// => { 'a': 1, 'b': 2 }
```

---

## defaultsDeep

This method is like `_.defaults` except that it recursively assigns default properties.

**Note:** This method mutates `object`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | The destination object. |
| `[sources]` | `...Object` | One or more source objects. |

**Returns**

- `(Object)`: Returns `object`.

**Example**

```javascript
_.defaultsDeep({ 'a': { 'b': 2 } }, { 'a': { 'b': 1, 'c': 3 } });
// => { 'a': { 'b': 2, 'c': 3 } }
```

---

## findKey

This method is like `_.find` except that it returns the key of the first element `predicate` returns truthy for instead of the element itself.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | The object to inspect. |
| `[predicate]` | `Function` | The function invoked per iteration. |

**Returns**

- `(string|undefined)`: Returns the key of the matched element, else `undefined`.

**Example**

```javascript
var users = {
  'barney':  { 'age': 36, 'active': true },
  'fred':    { 'age': 40, 'active': false },
  'pebbles': { 'age': 1,  'active': true }
};

_.findKey(users, function(o) { return o.age < 40; });
// => 'barney' (iteration order is not guaranteed)
```

---

## findLastKey

This method is like `_.findKey` except that it iterates over elements of a collection from right to left.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | The object to inspect. |
| `[predicate]` | `Function` | The function invoked per iteration. |

**Returns**

- `(string|undefined)`: Returns the key of the matched element, else `undefined`.

**Example**

```javascript
var users = {
  'barney':  { 'age': 36, 'active': true },
  'fred':    { 'age': 40, 'active': false },
  'pebbles': { 'age': 1,  'active': true }
};

_.findLastKey(users, function(o) { return o.age < 40; });
// => 'pebbles' (assuming `_.findKey` returns 'barney')
```

---

## forIn

Iterates over own and inherited enumerable string-keyed properties of an object and invokes `iteratee` for each property. The `iteratee` is invoked with three arguments: (value, key, object). Iteratee functions may exit iteration early by explicitly returning `false`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | The object to iterate over. |
| `[iteratee]` | `Function` | The function invoked per iteration. |

**Returns**

- `(Object)`: Returns `object`.

**Example**

```javascript
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.forIn(new Foo, function(value, key) {
  console.log(key);
});
// => Logs 'a', 'b', then 'c' (iteration order is not guaranteed).
```

---

## forInRight

This method is like `_.forIn` except that it iterates over properties of `object` in the opposite order.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | The object to iterate over. |
| `[iteratee]` | `Function` | The function invoked per iteration. |

**Returns**

- `(Object)`: Returns `object`.

**Example**

```javascript
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.forInRight(new Foo, function(value, key) {
  console.log(key);
});
// => Assuming `_.forIn` logs 'a', 'b', 'c', this logs 'c', 'b', 'a'.
```

---

## forOwn

Iterates over own enumerable string-keyed properties of an object and invokes `iteratee` for each property. The `iteratee` is invoked with three arguments: (value, key, object). Iteratee functions may exit iteration early by explicitly returning `false`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | The object to iterate over. |
| `[iteratee]` | `Function` | The function invoked per iteration. |

**Returns**

- `(Object)`: Returns `object`.

**Example**

```javascript
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.forOwn(new Foo, function(value, key) {
  console.log(key);
});
// => Logs 'a' then 'b' (iteration order is not guaranteed).
```

---

## forOwnRight

This method is like `_.forOwn` except that it iterates over properties of `object` in the opposite order.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | The object to iterate over. |
| `[iteratee]` | `Function` | The function invoked per iteration. |

**Returns**

- `(Object)`: Returns `object`.

**Example**

```javascript
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.forOwnRight(new Foo, function(value, key) {
  console.log(key);
});
// => Assuming `_.forOwn` logs 'a', 'b', this logs 'b', 'a'.
```

---

## functions

Creates an array of function property names from own enumerable properties of `object`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | The object to inspect. |

**Returns**

- `(Array)`: Returns the array of function names.

**Example**

```javascript
function Foo() {
  this.a = _.constant('a');
  this.b = _.constant('b');
}

Foo.prototype.c = _.constant('c');

_.functions(new Foo);
// => ['a', 'b']
```

---

## functionsIn

Creates an array of function property names from own and inherited enumerable properties of `object`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | The object to inspect. |

**Returns**

- `(Array)`: Returns the array of function names.

**Example**

```javascript
function Foo() {
  this.a = _.constant('a');
  this.b = _.constant('b');
}

Foo.prototype.c = _.constant('c');

_.functionsIn(new Foo);
// => ['a', 'b', 'c']
```

---

## get

Gets the value at `path` of `object`. If the resolved value is `undefined`, the `defaultValue` is returned in its place.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | The object to query. |
| `path` | `Array` or `string` | The path of the property to retrieve. |
| `[defaultValue]` | `*` | The value returned for `undefined` resolved values. |

**Returns**

- `(*)`: Returns the resolved value.

**Example**

```javascript
var object = { 'a': [{ 'b': { 'c': 3 } }] };

_.get(object, 'a[0].b.c');
// => 3

_.get(object, ['a', '0', 'b', 'c']);
// => 3

_.get(object, 'a.b.c', 'default');
// => 'default'
```

---

## has

Checks if `path` is a direct property of `object`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | The object to query. |
| `path` | `Array` or `string` | The path to check. |

**Returns**

- `(boolean)`: Returns `true` if `path` exists, else `false`.

**Example**

```javascript
var object = { 'a': { 'b': 2 } };
var other = _.create({ 'a': _.create({ 'b': 2 }) });

_.has(object, 'a');
// => true

_.has(object, 'a.b');
// => true

_.has(object, ['a', 'b']);
// => true

_.has(other, 'a');
// => false
```

---

## hasIn

Checks if `path` is a direct or inherited property of `object`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | The object to query. |
| `path` | `Array` or `string` | The path to check. |

**Returns**

- `(boolean)`: Returns `true` if `path` exists, else `false`.

**Example**

```javascript
var object = _.create({ 'a': _.create({ 'b': 2 }) });

_.hasIn(object, 'a');
// => true

_.hasIn(object, 'a.b');
// => true

_.hasIn(object, ['a', 'b']);
// => true

_.hasIn(object, 'b');
// => false
```

---

## invert

Creates an object composed of the inverted keys and values of `object`. If `object` contains duplicate values, subsequent values overwrite property assignments of previous values.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | The object to invert. |

**Returns**

- `(Object)`: Returns the new inverted object.

**Example**

```javascript
var object = { 'a': 1, 'b': 2, 'c': 1 };

_.invert(object);
// => { '1': 'c', '2': 'b' }
```

---

## invertBy

This method is like `_.invert` except that the inverted object is generated from the results of running each element of `object` thru `iteratee`. The corresponding value of each inverted key is an array of keys responsible for generating the inverted value. The `iteratee` is invoked with one argument: (value).

**Parameters**

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | The object to invert. |
| `[iteratee]` | `Function` | The function invoked per iteration. |

**Returns**

- `(Object)`: Returns the new inverted object.

**Example**

```javascript
var object = { 'a': 1, 'b': 2, 'c': 1 };

_.invertBy(object);
// => { '1': ['a', 'c'], '2': ['b'] }

_.invertBy(object, function(value) {
  return 'group' + value;
});
// => { 'group1': ['a', 'c'], 'group2': ['b'] }
```

---

## invoke

Invokes the method at `path` of `object`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | The object to query. |
| `path` | `Array` or `string` | The path of the method to invoke. |
| `[args]` | `...*` | The arguments to invoke the method with. |

**Returns**

- `(*)`: Returns the result of the invoked method.

**Example**

```javascript
var object = { 'a': [{ 'b': { 'c': [1, 2, 3, 4] } }] };

_.invoke(object, 'a[0].b.c.slice', 1, 3);
// => [2, 3]
```

---

## keys

Creates an array of the own enumerable property names of `object`.

**Note:** Non-object values are coerced to objects.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | The object to query. |

**Returns**

- `(Array)`: Returns the array of property names.

**Example**

```javascript
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.keys(new Foo);
// => ['a', 'b'] (iteration order is not guaranteed)

_.keys('hi');
// => ['0', '1']
```

---

## keysIn

Creates an array of the own and inherited enumerable property names of `object`.

**Note:** Non-object values are coerced to objects.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | The object to query. |

**Returns**

- `(Array)`: Returns the array of property names.

**Example**

```javascript
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.keysIn(new Foo);
// => ['a', 'b', 'c'] (iteration order is not guaranteed)
```

---

## mapKeys

The opposite of `_.mapValues`; this method creates an object with the same values as `object` and keys generated by running each own enumerable string-keyed property of `object` thru `iteratee`. The `iteratee` is invoked with three arguments: (value, key, object).

**Parameters**

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | The object to iterate over. |
| `[iteratee]` | `Function` | The function invoked per iteration. |

**Returns**

- `(Object)`: Returns the new mapped object.

**Example**

```javascript
_.mapKeys({ 'a': 1, 'b': 2 }, function(value, key) {
  return key + value;
});
// => { 'a1': 1, 'b2': 2 }
```

---

## mapValues

Creates an object with the same keys as `object` and values generated by running each own enumerable string-keyed property of `object` thru `iteratee`. The `iteratee` is invoked with three arguments: (value, key, object).

**Parameters**

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | The object to iterate over. |
| `[iteratee]` | `Function` | The function invoked per iteration. |

**Returns**

- `(Object)`: Returns the new mapped object.

**Example**

```javascript
var users = {
  'fred':    { 'user': 'fred',    'age': 40 },
  'pebbles': { 'user': 'pebbles', 'age': 1 }
};

_.mapValues(users, function(o) { return o.age; });
// => { 'fred': 40, 'pebbles': 1 } (iteration order is not guaranteed)
```

---

## merge

Recursively merges own and inherited enumerable properties of source objects into the destination object. Source properties that are `undefined` are skipped. Arrays and plain objects are merged recursively. Other objects and value types are overridden by assignment. Source objects are applied from left to right.

**Note:** This method mutates `object`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | The destination object. |
| `[sources]` | `...Object` | One or more source objects. |

**Returns**

- `(Object)`: Returns `object`.

**Example**

```javascript
var object = {
  'a': [{ 'b': 2 }, { 'd': 4 }]
};

var other = {
  'a': [{ 'c': 3 }, { 'e': 5 }]
};

_.merge(object, other);
// => { 'a': [{ 'b': 2, 'c': 3 }, { 'd': 4, 'e': 5 }] }
```

---

## mergeWith

This method is like `_.merge` except that it accepts a `customizer` which is invoked to produce the merged values. If `customizer` returns `undefined`, merging is handled by the method instead. The `customizer` is invoked with six arguments: (objValue, srcValue, key, object, source, stack).

**Note:** This method mutates `object`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | The destination object. |
| `sources` | `...Object` | One or more source objects. |
| `customizer` | `Function` | The function to customize assigned values. |

**Returns**

- `(Object)`: Returns `object`.

**Example**

```javascript
function customizer(objValue, srcValue) {
  if (_.isArray(objValue)) {
    return objValue.concat(srcValue);
  }
}

var object = { 'a': [1], 'b': [2] };
var other = { 'a': [3], 'b': [4] };

_.mergeWith(object, other, customizer);
// => { 'a': [1, 3], 'b': [2, 4] }
```

---

## omit

The opposite of `_.pick`; this method creates an object omitting the properties at `paths`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | The source object. |
| `[paths]` | `...(string|string[])` | The property paths to omit. |

**Returns**

- `(Object)`: Returns the new object.

**Example**

```javascript
var object = { 'a': 1, 'b': '2', 'c': 3 };

_.omit(object, ['a', 'c']);
// => { 'b': '2' }
```

---

## omitBy

The opposite of `_.pickBy`; this method creates an object composed of the own and inherited enumerable properties of `object` that `predicate` does not return truthy for. The `predicate` is invoked with two arguments: (value, key).

**Parameters**

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | The source object. |
| `[predicate]` | `Function` | The function invoked per iteration. |

**Returns**

- `(Object)`: Returns the new object.

**Example**

```javascript
var object = { 'a': 1, 'b': '2', 'c': 3 };

_.omitBy(object, _.isNumber);
// => { 'b': '2' }
```

---

## pick

Creates an object composed of the picked `object` properties.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | The source object. |
| `[paths]` | `...(string|string[])` | The property paths to pick. |

**Returns**

- `(Object)`: Returns the new object.

**Example**

```javascript
var object = { 'a': 1, 'b': '2', 'c': 3 };

_.pick(object, ['a', 'c']);
// => { 'a': 1, 'c': 3 }
```

---

## pickBy

Creates an object composed of the `object` properties `predicate` returns truthy for. The `predicate` is invoked with two arguments: (value, key).

**Parameters**

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | The source object. |
| `[predicate]` | `Function` | The function invoked per iteration. |

**Returns**

- `(Object)`: Returns the new object.

**Example**

```javascript
var object = { 'a': 1, 'b': '2', 'c': 3 };

_.pickBy(object, _.isNumber);
// => { 'a': 1, 'c': 3 }
```

---

## result

This method is like `_.get` except that if the resolved value is a function it's invoked and its result is returned.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | The object to query. |
| `path` | `Array` or `string` | The path of the property to resolve. |
| `[defaultValue]` | `*` | The value returned for `undefined` resolved values. |

**Returns**

- `(*)`: Returns the resolved value.

**Example**

```javascript
var object = { 'a': [{ 'b': { 'c1': 3, 'c2': _.constant(4) } }] };

_.result(object, 'a[0].b.c1');
// => 3

_.result(object, 'a[0].b.c2');
// => 4

_.result(object, 'a[0].b.c3', 'default');
// => 'default'
```

---

## set

Sets the value at `path` of `object`. If a portion of `path` doesn't exist, it's created. Arrays are created for missing index properties while objects are created for all other missing properties. Use `_.setWith` to customize `path` creation.

**Note:** This method mutates `object`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | The object to modify. |
| `path` | `Array` or `string` | The path of the property to set. |
| `value` | `*` | The value to set. |

**Returns**

- `(Object)`: Returns `object`.

**Example**

```javascript
var object = { 'a': [{ 'b': { 'c': 3 } }] };

_.set(object, 'a[0].b.c', 4);
// object.a[0].b.c is 4

_.set(object, ['x', '0', 'y', 'z'], 5);
// object.x[0].y.z is 5
```

---

## setWith

This method is like `_.set` except that it accepts a `customizer` which is invoked to produce the objects for portions of `path`. If `customizer` returns `undefined`, path creation is handled by the method instead. The `customizer` is invoked with three arguments: (nsValue, key, nsObject).

**Note:** This method mutates `object`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | The object to modify. |
| `path` | `Array` or `string` | The path of the property to set. |
| `value` | `*` | The value to set. |
| `[customizer]` | `Function` | The function to customize assigned values. |

**Returns**

- `(Object)`: Returns `object`.

**Example**

```javascript
var object = {};

_.setWith(object, '[0][1]', 'a', Object);
// => { '0': { '1': 'a' } }
```

---

## toPairs

Creates an array of own enumerable string-keyed-value pairs for `object`. If `object` is a map or set, its entries are returned.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | The object to query. |

**Returns**

- `(Array)`: Returns the key-value pairs.

**Example**

```javascript
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.toPairs(new Foo);
// => [['a', 1], ['b', 2]] (iteration order is not guaranteed)
```

---

## toPairsIn

Creates an array of own and inherited enumerable string-keyed-value pairs for `object`. If `object` is a map or set, its entries are returned.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | The object to query. |

**Returns**

- `(Array)`: Returns the key-value pairs.

**Example**

```javascript
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.toPairsIn(new Foo);
// => [['a', 1], ['b', 2], ['c', 3]] (iteration order is not guaranteed)
```

---

## transform

An alternative to `_.reduce`; this method transforms `object` to a new `accumulator` object, the result of running each of its own enumerable string-keyed properties thru `iteratee`, with each invocation potentially mutating the `accumulator` object. If `accumulator` is not provided, a new object is created. The `iteratee` is invoked with four arguments: (accumulator, value, key, object). Iteratee functions may exit iteration early by explicitly returning `false`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | The object to iterate over. |
| `[iteratee]` | `Function` | The function invoked per iteration. |
| `[accumulator]` | `*` | The custom accumulator value. |

**Returns**

- `(*)`: Returns the accumulated value.

**Example**

```javascript
_.transform([2, 3, 4], function(result, n) {
  result.push(n *= n);
  return n % 2 == 0;
}, []);
// => [4, 9]
```

---

## unset

Removes the property at `path` of `object`.

**Note:** This method mutates `object`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | The object to modify. |
| `path` | `Array` or `string` | The path of the property to unset. |

**Returns**

- `(boolean)`: Returns `true` if the property is deleted, else `false`.

**Example**

```javascript
var object = { 'a': [{ 'b': { 'c': 7 } }] };
_.unset(object, 'a[0].b.c');
// => true

// object is { 'a': [{ 'b': {} }] };
```

---

## update

This method is like `_.set` except that it accepts `updater` to generate the value to set. The `updater` is invoked with one argument: (value).

**Note:** This method mutates `object`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | The object to modify. |
| `path` | `Array` or `string` | The path of the property to set. |
| `updater` | `Function` | The function to generate the updated value. |

**Returns**

- `(Object)`: Returns `object`.

**Example**

```javascript
var object = { 'a': [{ 'b': { 'c': 3 } }] };

_.update(object, 'a[0].b.c', function(n) { return n * n; });
// object.a[0].b.c is 9
```

---

## updateWith

This method is like `_.update` except that it accepts a `customizer` which is invoked to produce the objects for portions of `path`. If `customizer` returns `undefined`, path creation is handled by the method instead. The `customizer` is invoked with three arguments: (nsValue, key, nsObject).

**Note:** This method mutates `object`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | The object to modify. |
| `path` | `Array` or `string` | The path of the property to set. |
| `updater` | `Function` | The function to generate the updated value. |
| `[customizer]` | `Function` | The function to customize assigned values. |

**Returns**

- `(Object)`: Returns `object`.

**Example**

```javascript
var object = {};

_.updateWith(object, '[0][1]', _.constant('a'), Object);
// => { '0': { '1': 'a' } }
```

---

## values

Creates an array of the own enumerable property values of `object`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | The object to query. |

**Returns**

- `(Array)`: Returns the array of property values.

**Example**

```javascript
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.values(new Foo);
// => [1, 2] (iteration order is not guaranteed)

_.values('hi');
// => ['h', 'i']
```

---

## valuesIn

Creates an array of the own and inherited enumerable property values of `object`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | The object to query. |

**Returns**

- `(Array)`: Returns the array of property values.

**Example**

```javascript
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.valuesIn(new Foo);
// => [1, 2, 3] (iteration order is not guaranteed)
```

---

This section covered the core functions in Lodash for object manipulation. Mastering these tools can greatly simplify data processing and state management. Next, you can explore the [Seq](./api-seq.md) section to learn how to combine these operations using chaining.
