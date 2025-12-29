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


---

## Pattern 5: Reverse a Number

### Example
```
Input: 7898
Output: 8987
```

### Logic
- Extract last digit using `% 10`
- Build reverse by shifting digits left
- Remove last digit using integer division

```js
let num = 7898;
let reverse = 0;

while (num > 0) {
  let digit = num % 10;
  reverse = reverse * 10 + digit;
  num = Math.floor(num / 10);
}

console.log(reverse); // 8987
```

- Time Complexity: **O(d)** (d = number of digits)
- Space Complexity: **O(1)**


---

## Math.floor() vs Math.ceil()

### Basic Difference
- `Math.floor()` → rounds **downward (toward −∞)**
- `Math.ceil()` → rounds **upward (toward +∞)**

### Positive Numbers

| Number | Math.floor() | Math.ceil() |
|------|-------------|-------------|
| 4.1  | 4 | 5 |
| 4.9  | 4 | 5 |
| 4.0  | 4 | 4 |
| 7.01 | 7 | 8 |

### Negative Numbers (Important)

| Number | Math.floor() | Math.ceil() |
|------|-------------|-------------|
| -4.1 | -5 | -4 |
| -4.9 | -5 | -4 |
| -4.0 | -4 | -4 |

### Key Reminder
- **floor → toward −∞**
- **ceil → toward +∞**

> Very important for digit extraction, math problems, and loops.


---

## Pattern 6: Reverse Integer with Overflow Check (LeetCode Style)

### Problem
Reverse an integer `x`.  
If the reversed integer overflows **32-bit signed integer range** `[-2^31, 2^31 - 1]`, return `0`.

### Logic
- Track sign separately
- Reverse digits using modulo and division
- Before adding a digit, check for overflow:
  - Max value = `2147483647`
- If overflow is detected → return `0`

```js
var reverse = function(x) {
    let isNeg = x < 0;
    let num = Math.abs(x);
    let reverse = 0;

    while (num > 0) {
        let digit = num % 10;
        if (
            reverse > Math.floor(2147483647 / 10) ||
            (reverse === Math.floor(2147483647 / 10) && digit > 7)
        ) {
            return 0;
        }

        reverse = reverse * 10 + digit;
        num = Math.floor(num / 10);
    }

    return isNeg ? -reverse : reverse;
};
```

### Complexity
- **Time Complexity:** `O(d)` (d = number of digits)
- **Space Complexity:** `O(1)`

> Common interview problem focusing on edge cases and overflow handling.


---

## Pattern 7: GCD (Greatest Common Divisor) — Euclidean Algorithm

### Logic
- Uses recursion
- Base case: if `b === 0`, GCD is `a`
- Otherwise, call `GCD(b, a % b)`

```js
function GCD(a, b) {
    if (b === 0) return a;
    return GCD(b, a % b);
}
```

### Complexity
- **Time Complexity:** `O(log(min(a, b)))`
- **Space Complexity:** `O(log(min(a, b)))` (recursive stack)

> One of the most important number algorithms in DSA and interviews.


---

## Pattern 8: Armstrong Number

### Definition
A number is an **Armstrong number** if the sum of its digits raised to the power of the number of digits equals the original number.

### Logic
- Count number of digits
- Extract each digit
- Raise digit to the power of total digits
- Compare sum with original number

```js
function Armstrong(num) {
    let original = num;
    let digits = 0;
    let temp = num;

    // count digits
    while (temp > 0) {
        digits++;
        temp = Math.floor(temp / 10);
    }

    let sum = 0;
    temp = num;

    // calculate power sum
    while (temp > 0) {
        let digit = temp % 10;
        sum += digit ** digits;
        temp = Math.floor(temp / 10);
    }

    return sum === original;
}

console.log(Armstrong(153));  // true
console.log(Armstrong(9474)); // true
console.log(Armstrong(1533)); // false
```

### Complexity
- **Time Complexity:** `O(d)` (d = number of digits)
- **Space Complexity:** `O(1)`

> Commonly asked number problem in interviews and exams.
