# JavaScript Data Types — Short Notes

## Overview
- JavaScript is **dynamically typed**
- Type coercion can cause unexpected behavior

---

## Primitive Data Types
- **number** → integers & floating-point numbers
- **string** → text
- **boolean** → true / false
- **undefined** → declared but not assigned
- **null** → intentional absence of value
- **symbol** → unique identifiers

---

## Symbol (In Detail)
- Primitive data type (ES6)
- Used for **unique identifiers**
- Symbols are always unique

```js
let a = Symbol("id");
let b = Symbol("id");
a === b; // false
```

- Used as object keys to avoid conflicts
- Not visible in `for...in` or `Object.keys()`
- Special symbols like `Symbol.iterator` exist

---

## Non-Primitive (Reference) Types
- **object**
- **array**
- **function**

> Arrays and functions are objects in JavaScript.

---

## Conditional Statements

### if–else
Used to execute code based on a condition.

```js
let age = 18;

if (age >= 18) {
  console.log("Adult");
} else {
  console.log("Minor");
}
```

---

### switch Statement
Used when comparing one value with multiple cases.

```js
let day = 2;

switch (day) {
  case 1:
    console.log("Monday");
    break;
  case 2:
    console.log("Tuesday");
    break;
  default:
    console.log("Invalid day");
}
```

---

## Arrays
- Collection of elements
- Can store mixed data types
- Indexed (0-based)

```js
let arr = [1, 2, 3, "JS"];
console.log(arr[0]); // 1
```

---

## Strings
- Used to store text
- Immutable (cannot be changed)

```js
let str = "Hello";
console.log(str.length); // 5
```

---

## Loops

### for Loop
Used when number of iterations is known.

```js
for (let i = 0; i < 3; i++) {
  console.log(i);
}
```

---

### while Loop
Runs while condition is true.

```js
let i = 0;
while (i < 3) {
  console.log(i);
  i++;
}
```

---

## Functions

### Function Declaration
```js
function add(a, b) {
  return a + b;
}
```

---

### Pass by Value
- Primitive types are passed by value
- Original value does not change

```js
let x = 10;

function update(val) {
  val = 20;
}

update(x);
console.log(x); // 10
```

---

### Pass by Reference
- Objects and arrays are passed by reference
- Original value changes

```js
let obj = { value: 10 };

function updateObj(o) {
  o.value = 20;
}

updateObj(obj);
console.log(obj.value); // 20
```

---

## Time Complexity (Basics)
- Measures how runtime grows with input size

| Operation | Time Complexity |
|---------|----------------|
| Single loop | O(n) |
| Nested loop | O(n²) |
| Array access | O(1) |
| Binary search | O(log n) |

---

## Important Quirk
- `typeof null` returns **"object"** (JavaScript bug)
