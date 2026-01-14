# Building Up Array

---

## Check If Array Is Sorted and Rotated

### Idea
- Count how many times the order breaks
- Use modulo to compare last element with first
- Array is sorted & rotated if breaks ≤ 1

```js
function checkSorted(nums) {
    let breaks = 0;

    for (let i = 0; i < nums.length; i++) {
        if (nums[i] > nums[(i + 1) % nums.length]) {
            breaks++;
            if (breaks > 1) return false; // early exit
        }
    }

    return true;
}
```

### Complexity
- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

> Common array interview problem (sorted + rotated check).
