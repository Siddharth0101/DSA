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

## Key Takeaways
- Pattern problems are output-dominated
- Time complexity cannot be reduced below **O(n²)**
- Focus on understanding **loop boundaries**
- Builds foundation for DSA problems
