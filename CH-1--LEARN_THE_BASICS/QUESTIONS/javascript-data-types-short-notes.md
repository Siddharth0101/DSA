# JavaScript Data Types — Short Notes

## Overview
- JavaScript is **dynamically typed**
- Type coercion can cause unexpected behavior

## Primitive Data Types
- **number** → integers & floating-point numbers
- **string** → text
- **boolean** → true / false
- **undefined** → declared but not assigned
- **null** → intentional absence of value
- **symbol** → unique identifiers

## Symbol (In Detail)
- **Symbol** is a primitive data type introduced in **ES6**
- Used to create **unique identifiers**
- Every Symbol is **unique**, even with the same description

```js
let a = Symbol("id");
let b = Symbol("id");
a === b; // false
```

- Mostly used as **object keys** to avoid naming conflicts
- Symbol properties:
  - Not visible in `for...in`
  - Not returned by `Object.keys()`
- Helps in:
  - Hiding internal properties
  - Avoiding collisions in large applications
  - Implementing special behaviors (`Symbol.iterator`)

- Global symbols:
```js
Symbol.for("key");
```

- Symbols do **not auto-convert to strings**

## Non-Primitive (Reference) Types
- **object**
- **array**
- **function**

> Note: Arrays and functions are also objects.

## Important Quirk
- `typeof null` returns **"object"** (legacy JavaScript bug)
