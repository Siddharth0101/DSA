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


---

## 2️⃣ Rotate Array, Move Zeroes & Missing Number

### Rotate Array (Right Rotation – Reversal Method)

```js
var rotate = function(nums, k) {
    let n = nums.length;
    k = k % n; // important for large k

    // step 1: reverse whole array
    reverse(nums, 0, n - 1);

    // step 2: reverse first k elements
    reverse(nums, 0, k - 1);

    // step 3: reverse remaining elements
    reverse(nums, k, n - 1);

    return nums;
};

function reverse(arr, left, right) {
    while (left < right) {
        let temp = arr[left];
        arr[left] = arr[right];
        arr[right] = temp;
        left++;
        right--;
    }
}

console.log(rotate([1,2,3,4,5,6,7], 3));
// [5,6,7,1,2,3,4]
```

---

### Move Zeroes to End

```js
var moveZeroes = function(nums) {
    let left = 0;
    let right = 1;

    while (right < nums.length) {
        if (nums[right] != 0) {
            let temp = nums[left];
            nums[left] = nums[right];
            nums[right] = temp;
            left++;
        }
        right++;
    }
    return nums;
};

console.log(moveZeroes([0,1,0,3,12]));
```

---

### Missing Number (Sum Formula)

```js
var missingNumber = function(nums) {
    let n = nums.length;
    let expectedSum = n * (n + 1) / 2;
    let actualSum = 0;

    for (let i = 0; i < nums.length; i++) {
        actualSum += nums[i];
    }

    return expectedSum - actualSum;
};
```

---

### Missing Number (XOR Method)

```js
var missingNumber = function(nums) {
    let xor = 0;

    for (let i = 0; i <= nums.length; i++) {
        xor ^= i;
    }

    for (let num of nums) {
        xor ^= num;
    }

    return xor;
};

console.log(missingNumber([3,0,1])); // 2
```
