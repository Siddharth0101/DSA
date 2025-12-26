# Building Up Logical Thinking (Star Patterns)

## Pattern 1: Right-Angled Triangle

### Output
```
*
* *
* * *
* * * *
* * * * *
```

### Logic (Nested Loops)
- Outer loop → rows
- Inner loop → stars per row
- Stars = row number

```js
let n = 5;

for (let i = 1; i <= n; i++) {
  let row = "";
  for (let j = 1; j <= i; j++) {
    row += "* ";
  }
  console.log(row);
}
```

- Time Complexity: **O(n²)**
- Space Complexity: **O(1)**

---

## Pattern 2: Inverted Centered Pyramid

### Output
```
*********
 *******
  *****
   ***
    *
```

### Logic
- Outer loop runs from `rows → 1`
- Spaces increase each row
- Stars decrease using odd count formula `2*i - 1`

```js
let rows = 5;

for (let i = rows; i >= 1; i--) {
  let row = "";

  // leading spaces
  for (let s = 0; s < rows - i + 1; s++) {
    row += " ";
  }

  // stars (odd count)
  for (let j = 0; j < 2 * i - 1; j++) {
    row += "*";
  }

  console.log(row);
}
```

- Time Complexity: **O(n²)**
- Space Complexity: **O(1)**

---

## Pattern 3: Hollow Square

### Output (n = 4)
```
****
*  *
*  *
****
```

### Logic
- First and last rows → all stars
- Middle rows → star + spaces + star
- Focuses on **upper and lower halves**

```js
let n = 4;

/* ===== Upper Half ===== */

// top row
let top = '';
for (let i = 0; i < n; i++) {
  top += '*';
}
console.log(top);

// one middle row
let mid = '*';
for (let i = 0; i < n - 2; i++) {
  mid += ' ';
}
mid += '*';
console.log(mid);

/* ===== Lower Half ===== */

// one middle row
let mid2 = '*';
for (let i = 0; i < n - 2; i++) {
  mid2 += ' ';
}
mid2 += '*';
console.log(mid2);

// bottom row
let bottom = '';
for (let i = 0; i < n; i++) {
  bottom += '*';
}
console.log(bottom);
```

- Time Complexity: **O(n²)**
- Space Complexity: **O(1)**

---

## Key Takeaways
- Pattern problems are output-dominated
- Time complexity cannot be reduced below **O(n²)**
- Splitting patterns into halves improves clarity
- Builds strong logical foundation for DSA


---

## Pattern 4: Concentric Number Square

### Output (n = 4)
```
4 4 4 4 4 4 4
4 3 3 3 3 3 4
4 3 2 2 2 3 4
4 3 2 1 2 3 4
4 3 2 2 2 3 4
4 3 3 3 3 3 4
4 4 4 4 4 4 4
```

### Logic
- Grid size = `2 * n - 1`
- Numbers decrease layer by layer toward the center
- Uses boundary (layer) conditions

```js
let n = 4;
let size = 2 * n - 1;

for (let i = 0; i < size; i++) {
  let row = "";

  for (let j = 0; j < size; j++) {

    if (i === 0 || j === 0 || i === size - 1 || j === size - 1) {
      row += "4 ";
    }
    else if (
      i === 1 || j === 1 || i === size - 2 || j === size - 2
    ) {
      row += "3 ";
    }
    else if (
      i === 2 || j === 2 || i === size - 3 || j === size - 3
    ) {
      row += "2 ";
    }
    else {
      row += "1 ";
    }

  }
  console.log(row);
}
```

- Time Complexity: **O(n²)**
- Space Complexity: **O(1)**
