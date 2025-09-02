# Object

Lodash provides a large number of functions for manipulating and processing JavaScript objects. These tools can help you merge, transform, select, check, and set object properties, and are a core part of data processing workflows. These functions focus on handling an object's own and inherited properties, offering more powerful and flexible functionality than native JavaScript.

To learn more about iterating over objects and arrays, please refer to the functions in the [Collection](./api-collection.md) section.

---

## assign

Assigns own enumerable string keyed properties of one or more source objects to a destination object. Source objects are applied from left to right. Subsequent sources overwrite property assignments of previous sources.

**Note:** This method mutates `object`.

**Arguments**

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

This method is like `_.assign` except that it iterates over and inherits properties from source objects. Alias: `_.extend`.

**Note:** This method mutates `object`.

**Arguments**

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

## create

Creates an object that inherits from the `prototype` object. If a `properties` object is provided, its own enumerable string keyed properties are assigned to the created object.

**Arguments**

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

Assigns own enumerable string keyed properties of source objects to the destination object for all destination properties that resolve to `undefined`. Source objects are applied from left to right. Once a property is set, additional values of the same property are ignored.

**Note:** This method mutates `object`.

**Arguments**

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

**Arguments**

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

## get

Gets the value at `path` of `object`. If the resolved value is `undefined`, the `defaultValue` is returned in its place.

**Arguments**

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

**Arguments**

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

## invert

Creates an object composed of the inverted keys and values of `object`. If `object` contains duplicate values, subsequent values overwrite property assignments of previous values.

**Arguments**

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

## keys

Creates an array of the own enumerable property names of `object`.

**Note:** Non-object values are coerced to objects.

**Arguments**

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

## merge

This method recursively merges own and inherited enumerable properties of source objects into the destination object. Source properties that are `undefined` are skipped. Arrays and plain objects are merged recursively. Other objects and value types are overridden by assignment. Source objects are applied from left to right.

**Note:** This method mutates `object`.

**Arguments**

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

## omit

The inverse of `_.pick`; this method creates an object that omits the properties in `paths`.

**Arguments**

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

## pick

Creates an object composed of the picked `object` properties.

**Arguments**

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

## set

Sets the value at `path` of `object`. If a portion of `path` doesn't exist, it's created. Arrays are created for missing index properties while objects are created for all other missing properties. Use `_.setWith` to customize path creation.

**Note:** This method mutates `object`.

**Arguments**

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

## unset

Removes the property at `path` of `object`.

**Note:** This method mutates `object`.

**Arguments**

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | The object to modify. |
| `path` | `Array` or `string` | The path of the property to remove. |

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

## values

Creates an array of the own enumerable property values of `object`.

**Arguments**

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

This section introduced the core functions in Lodash for object manipulation. Mastering these tools can greatly simplify data processing and state management. Next, you can continue to explore the [Seq](./api-seq.md) section to learn how to combine these operations using chaining.