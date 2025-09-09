# Object

Lodash's object functions provide a powerful toolkit for creating, modifying, retrieving, and transforming object properties. These utilities simplify common object-related tasks, from merging objects to deep property access. For functions that iterate over objects, you may also find the [Collection](./api-collection.md) documentation useful.

## Creating & Modifying Objects

These functions are used to create new objects or modify existing ones by assigning, merging, or setting properties.

### assign

Assigns own enumerable string keyed properties of source objects to the destination object. Source objects are applied from left to right, and subsequent sources overwrite property assignments of previous sources.

**Note:** This method mutates the `object`.

#### Parameters

| Name      | Type        | Description                |
| --------- | ----------- | -------------------------- |
| `object`  | `Object`    | The destination object.    |
| `[sources]` | `...Object` | The source objects.        |

#### Returns

(`Object`): Returns the modified `object`.

#### Example

```javascript
function Foo() {
  this.a = 1;
}

function Bar() {
  this.c = 3;
}

Foo.prototype.b = 2;
Bar.prototype.d = 4;

_.assign({ 'a': 0 }, new Foo(), new Bar());
// => { 'a': 1, 'c': 3 }
```

### create

Creates an object that inherits from the `prototype` object. If a `properties` object is given, its own enumerable string keyed properties are assigned to the created object.

#### Parameters

| Name         | Type     | Description                          |
| ------------ | -------- | ------------------------------------ |
| `prototype`  | `Object` | The object to inherit from.          |
| `[properties]` | `Object` | The properties to assign to the object. |

#### Returns

(`Object`): Returns the new object.

#### Example

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

### defaults

Assigns own and inherited enumerable string keyed properties of source objects to the destination object for all destination properties that resolve to `undefined`. Source objects are applied from left to right.

**Note:** This method mutates `object`.

#### Parameters

| Name      | Type        | Description                |
| --------- | ----------- | -------------------------- |
| `object`  | `Object`    | The destination object.    |
| `[sources]` | `...Object` | The source objects.        |

#### Returns

(`Object`): Returns `object`.

#### Example

```javascript
_.defaults({ 'a': 1 }, { 'b': 2 }, { 'a': 3 });
// => { 'a': 1, 'b': 2 }
```

### defaultsDeep

This method is like `_.defaults` except that it recursively assigns default properties.

**Note:** This method mutates `object`.

#### Parameters

| Name      | Type        | Description                |
| --------- | ----------- | -------------------------- |
| `object`  | `Object`    | The destination object.    |
| `[sources]` | `...Object` | The source objects.        |

#### Returns

(`Object`): Returns `object`.

#### Example

```javascript
_.defaultsDeep({ 'a': { 'b': 2 } }, { 'a': { 'b': 1, 'c': 3 } });
// => { 'a': { 'b': 2, 'c': 3 } }
```

### merge

Recursively merges own and inherited enumerable string keyed properties of source objects into the destination object. Array and plain object properties are merged recursively. Other objects and value types are overridden by assignment.

**Note:** This method mutates `object`.

#### Parameters

| Name      | Type        | Description                |
| --------- | ----------- | -------------------------- |
| `object`  | `Object`    | The destination object.    |
| `[sources]` | `...Object` | The source objects.        |

#### Returns

(`Object`): Returns `object`.

#### Example

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

### set

Sets the value at `path` of `object`. If a portion of `path` doesn't exist, it's created. Arrays are created for missing index properties while objects are created for all other missing properties.

**Note:** This method mutates `object`.

#### Parameters

| Name    | Type           | Description                     |
| ------- | -------------- | ------------------------------- |
| `object`| `Object`       | The object to modify.           |
| `path`  | `Array`\|`string` | The path of the property to set.|
| `value` | `*`            | The value to set.               |

#### Returns

(`Object`): Returns `object`.

#### Example

```javascript
var object = { 'a': [{ 'b': { 'c': 3 } }] };

_.set(object, 'a[0].b.c', 4);
console.log(object.a[0].b.c);
// => 4

_.set(object, ['x', '0', 'y', 'z'], 5);
console.log(object.x[0].y.z);
// => 5
```

### unset

Removes the property at `path` of `object`.

**Note:** This method mutates `object`.

#### Parameters

| Name    | Type           | Description                         |
| ------- | -------------- | ----------------------------------- |
| `object`| `Object`       | The object to modify.               |
| `path`  | `Array`\|`string` | The path of the property to unset.  |

#### Returns

(`boolean`): Returns `true` if the property is deleted, else `false`.

#### Example

```javascript
var object = { 'a': [{ 'b': { 'c': 7 } }] };
_.unset(object, 'a[0].b.c');
// => true

console.log(object);
// => { 'a': [{ 'b': {} }] };
```

## Accessing & Retrieving Values

These functions help you safely access properties, including nested ones, from objects.

### at

Creates an array of values corresponding to `paths` of `object`.

#### Parameters

| Name    | Type                      | Description                     |
| ------- | ------------------------- | ------------------------------- |
| `object`| `Object`                  | The object to iterate over.     |
| `[paths]` | `...string`\|`string[]` | The property paths to pick.     |

#### Returns

(`Array`): Returns the picked values.

#### Example

```javascript
var object = { 'a': [{ 'b': { 'c': 3 } }, 4] };

_.at(object, ['a[0].b.c', 'a[1]']);
// => [3, 4]
```

### get

Gets the value at `path` of `object`. If the resolved value is `undefined`, the `defaultValue` is returned in its place.

#### Parameters

| Name           | Type           | Description                                  |
| -------------- | -------------- | -------------------------------------------- |
| `object`       | `Object`       | The object to query.                         |
| `path`         | `Array`\|`string` | The path of the property to get.             |
| `[defaultValue]` | `*`            | The value returned for `undefined` resolved values. |

#### Returns

(`*`): Returns the resolved value.

#### Example

```javascript
var object = { 'a': [{ 'b': { 'c': 3 } }] };

_.get(object, 'a[0].b.c');
// => 3

_.get(object, ['a', '0', 'b', 'c']);
// => 3

_.get(object, 'a.b.c', 'default');
// => 'default'
```

### result

This method is like `_.get` except that if the resolved value is a function it's invoked with the `this` binding of its parent object and its result is returned.

#### Parameters

| Name           | Type           | Description                                  |
| -------------- | -------------- | -------------------------------------------- |
| `object`       | `Object`       | The object to query.                         |
| `path`         | `Array`\|`string` | The path of the property to resolve.         |
| `[defaultValue]` | `*`            | The value returned for `undefined` resolved values. |

#### Returns

(`*`): Returns the resolved value.

#### Example

```javascript
var object = { 'a': [{ 'b': { 'c1': 3, 'c2': _.constant(4) } }] };

_.result(object, 'a[0].b.c1');
// => 3

_.result(object, 'a[0].b.c2');
// => 4

_.result(object, 'a[0].b.c3', 'default');
// => 'default'
```

## Keys & Values

Functions for working with object keys and values, such as retrieving them as arrays or inverting key-value pairs.

### keys

Creates an array of the own enumerable property names of `object`.

#### Parameters

| Name     | Type     | Description            |
| -------- | -------- | ---------------------- |
| `object` | `Object` | The object to query.   |

#### Returns

(`Array`): Returns the array of property names.

#### Example

```javascript
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.keys(new Foo());
// => ['a', 'b'] (iteration order is not guaranteed)

_.keys('hi');
// => ['0', '1']
```

### keysIn

Creates an array of the own and inherited enumerable property names of `object`.

#### Parameters

| Name     | Type     | Description            |
| -------- | -------- | ---------------------- |
| `object` | `Object` | The object to query.   |

#### Returns

(`Array`): Returns the array of property names.

#### Example

```javascript
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.keysIn(new Foo());
// => ['a', 'b', 'c'] (iteration order is not guaranteed)
```

### values

Creates an array of the own enumerable string keyed property values of `object`.

#### Parameters

| Name     | Type     | Description            |
| -------- | -------- | ---------------------- |
| `object` | `Object` | The object to query.   |

#### Returns

(`Array`): Returns the array of property values.

#### Example

```javascript
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.values(new Foo());
// => [1, 2] (iteration order is not guaranteed)

_.values('hi');
// => ['h', 'i']
```

### valuesIn

Creates an array of the own and inherited enumerable string keyed property values of `object`.

#### Parameters

| Name     | Type     | Description            |
| -------- | -------- | ---------------------- |
| `object` | `Object` | The object to query.   |

#### Returns

(`Array`): Returns the array of property values.

#### Example

```javascript
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.valuesIn(new Foo());
// => [1, 2, 3] (iteration order is not guaranteed)
```

### invert

Creates an object composed of the inverted keys and values of `object`. If `object` contains duplicate values, subsequent values overwrite property assignments of previous values.

#### Parameters

| Name     | Type     | Description            |
| -------- | -------- | ---------------------- |
| `object` | `Object` | The object to invert.  |

#### Returns

(`Object`): Returns the new inverted object.

#### Example

```javascript
var object = { 'a': 1, 'b': 2, 'c': 1 };

_.invert(object);
// => { '1': 'c', '2': 'b' }
```

## Filtering & Transforming

Create new objects by picking or omitting properties, or by transforming keys and values.

### pick

Creates an object composed of the picked `object` properties.

#### Parameters

| Name    | Type                      | Description                   |
| ------- | ------------------------- | ----------------------------- |
| `object`| `Object`                  | The source object.            |
| `[paths]` | `...string`\|`string[]` | The property paths to pick.   |

#### Returns

(`Object`): Returns the new object.

#### Example

```javascript
var object = { 'a': 1, 'b': '2', 'c': 3 };

_.pick(object, ['a', 'c']);
// => { 'a': 1, 'c': 3 }
```

### omit

The opposite of `_.pick`; this method creates an object composed of the own and inherited enumerable property paths of `object` that are not omitted.

#### Parameters

| Name    | Type                      | Description                   |
| ------- | ------------------------- | ----------------------------- |
| `object`| `Object`                  | The source object.            |
| `[paths]` | `...string`\|`string[]` | The property paths to omit.   |

#### Returns

(`Object`): Returns the new object.

#### Example

```javascript
var object = { 'a': 1, 'b': '2', 'c': 3 };

_.omit(object, ['a', 'c']);
// => { 'b': '2' }
```

### transform

An alternative to `_.reduce`, this method transforms `object` to a new `accumulator` object. The iteratee is invoked with four arguments: `(accumulator, value, key, object)`.

#### Parameters

| Name          | Type       | Description                 |
| ------------- | ---------- | --------------------------- |
| `object`      | `Object`   | The object to iterate over. |
| `[iteratee]`  | `Function` | The function invoked per iteration. |
| `[accumulator]` | `*`        | The custom accumulator value. |

#### Returns

(`*`): Returns the accumulated value.

#### Example

```javascript
_.transform([2, 3, 4], function(result, n) {
  result.push(n *= n);
  return n % 2 == 0;
}, []);
// => [4, 9]

_.transform({ 'a': 1, 'b': 2, 'c': 1 }, function(result, value, key) {
  (result[value] || (result[value] = [])).push(key);
}, {});
// => { '1': ['a', 'c'], '2': ['b'] }
```

## Checking Properties

Functions to check for the existence of properties on an object.

### has

Checks if `path` is a direct property of `object`.

#### Parameters

| Name    | Type           | Description                |
| ------- | -------------- | -------------------------- |
| `object`| `Object`       | The object to query.       |
| `path`  | `Array`\|`string` | The path to check.         |

#### Returns

(`boolean`): Returns `true` if `path` exists, else `false`.

#### Example

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

### hasIn

Checks if `path` is a direct or inherited property of `object`.

#### Parameters

| Name    | Type           | Description                |
| ------- | -------------- | -------------------------- |
| `object`| `Object`       | The object to query.       |
| `path`  | `Array`\|`string` | The path to check.         |

#### Returns

(`boolean`): Returns `true` if `path` exists, else `false`.

#### Example

```javascript
var object = _.create({ 'a': _.create({ 'b': 2 }) });

_.hasIn(object, 'a');
// => true

_.hasIn(object, 'a.b');
// => true

_.hasIn(object, 'b');
// => false
```

---

This guide has covered the extensive suite of functions Lodash provides for object manipulation. From simple property assignment to complex transformations, these utilities can significantly streamline your code. To learn how to combine these operations in powerful, declarative sequences, see the [Seq](./api-seq.md) guide for method chaining.
