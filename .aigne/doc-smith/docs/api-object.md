# Object

This section provides a detailed reference for Lodash functions used for manipulating and working with objects. These utilities help with tasks like creating, modifying, retrieving, and transforming object properties.

For functions that iterate over objects in a generic way (similar to arrays), see the [Collection](./api-collection.md) documentation.

---

### `_.assign(object, ...sources)`

Assigns own enumerable string keyed properties of source objects to the destination object. Source objects are applied from left to right. Subsequent sources overwrite property assignments of previous sources.

**Note:** This method mutates `object` and is loosely based on [`Object.assign`](https://mdn.io/Object/assign).

**Since**: 0.10.0

**Parameters**

| Parameter | Type | Description |
|---|---|---|
| `object` | `Object` | The destination object. |
| `...sources`| `...Object` | The source objects. |

**Returns**

- `(Object)`: Returns the modified `object`.

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

### `_.create(prototype, [properties])`

Creates an object that inherits from the `prototype` object. If a `properties` object is given, its own enumerable string keyed properties are assigned to the created object.

**Since**: 2.3.0

**Parameters**

| Parameter | Type | Description |
|---|---|---|
| `prototype` | `Object` | The object to inherit from. |
| `[properties]`| `Object` | The properties to assign to the object. |

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
console.log(circle instanceof Circle);
// => true

console.log(circle instanceof Shape);
// => true
```

---

### `_.defaults(object, ...sources)`

Assigns own and inherited enumerable string keyed properties of source objects to the destination object for all destination properties that resolve to `undefined`. Source objects are applied from left to right. Once a property is set, additional values of the same property are ignored.

**Note:** This method mutates `object`.

**Since**: 0.1.0

**Parameters**

| Parameter | Type | Description |
|---|---|---|
| `object` | `Object` | The destination object. |
| `...sources`| `...Object` | The source objects. |

**Returns**

- `(Object)`: Returns the modified `object`.

**Example**

```javascript
_.defaults({ 'a': 1 }, { 'b': 2 }, { 'a': 3 });
// => { 'a': 1, 'b': 2 }
```

---

### `_.get(object, path, [defaultValue])`

Gets the value at `path` of `object`. If the resolved value is `undefined`, the `defaultValue` is returned in its place.

**Since**: 3.7.0

**Parameters**

| Parameter | Type | Description |
|---|---|---|
| `object` | `Object` | The object to query. |
| `path` | `Array|string` | The path of the property to get. |
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

### `_.has(object, path)`

Checks if `path` is a direct property of `object`.

**Since**: 0.1.0

**Parameters**

| Parameter | Type | Description |
|---|---|---|
| `object` | `Object` | The object to query. |
| `path` | `Array|string` | The path to check. |

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

_.has(other, 'a');
// => false
```

---

### `_.keys(object)`

Creates an array of the own enumerable property names of `object`.

**Note:** Non-object values are coerced to objects.

**Since**: 0.1.0

**Parameters**

| Parameter | Type | Description |
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

### `_.merge(object, ...sources)`

This method is like `_.assign` except that it recursively merges own and inherited enumerable string keyed properties of source objects into the destination object. Source properties that resolve to `undefined` are skipped if a destination value exists. Array and plain object properties are merged recursively. Other objects and value types are overridden by assignment.

**Note:** This method mutates `object`.

**Since**: 0.5.0

**Parameters**

| Parameter | Type | Description |
|---|---|---|
| `object` | `Object` | The destination object. |
| `...sources`| `...Object` | The source objects. |

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

### `_.omit(object, ...paths)`

The opposite of `_.pick`; this method creates an object composed of the own and inherited enumerable property paths of `object` that are not omitted.

**Since**: 0.1.0

**Parameters**

| Parameter | Type | Description |
|---|---|---|
| `object` | `Object` | The source object. |
| `...paths`| `...(string|string[])` | The property paths to omit. |

**Returns**

- `(Object)`: Returns the new object.

**Example**

```javascript
var object = { 'a': 1, 'b': '2', 'c': 3 };
 
_.omit(object, ['a', 'c']);
// => { 'b': '2' }
```

---

### `_.pick(object, ...paths)`

Creates an object composed of the picked `object` properties.

**Since**: 0.1.0

**Parameters**

| Parameter | Type | Description |
|---|---|---|
| `object` | `Object` | The source object. |
| `...paths`| `...(string|string[])` | The property paths to pick. |

**Returns**

- `(Object)`: Returns the new object.

**Example**

```javascript
var object = { 'a': 1, 'b': '2', 'c': 3 };
 
_.pick(object, ['a', 'c']);
// => { 'a': 1, 'c': 3 }
```

---

### `_.set(object, path, value)`

Sets the value at `path` of `object`. If a portion of `path` doesn't exist, it's created. Arrays are created for missing index properties while objects are created for all other missing properties.

**Note:** This method mutates `object`.

**Since**: 3.7.0

**Parameters**

| Parameter | Type | Description |
|---|---|---|
| `object` | `Object` | The object to modify. |
| `path` | `Array|string` | The path of the property to set. |
| `value` | `*` | The value to set. |

**Returns**

- `(Object)`: Returns `object`.

**Example**

```javascript
var object = { 'a': [{ 'b': { 'c': 3 } }] };
 
_.set(object, 'a[0].b.c', 4);
console.log(object.a[0].b.c);
// => 4
 
_.set(object, ['x', '0', 'y', 'z'], 5);
console.log(object.x[0].y.z);
// => 5
```

---

### `_.values(object)`

Creates an array of the own enumerable string keyed property values of `object`.

**Note:** Non-object values are coerced to objects.

**Since**: 0.1.0

**Parameters**

| Parameter | Type | Description |
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

This covers the core object manipulation functions in Lodash. These utilities provide powerful and flexible ways to work with object data structures.
For chaining these operations together in a readable sequence, see the [Seq](./api-seq.md) documentation.