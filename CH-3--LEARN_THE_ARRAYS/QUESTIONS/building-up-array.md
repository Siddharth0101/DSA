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

---

## 3️⃣ Single Number

### Idea
- XOR all numbers: `a ^ a = 0` and `a ^ 0 = a`
- Since every number appears twice except one, duplicates cancel out.
- The remaining result is the single number.

```js
var singleNumber = function(nums) {
    let ans = 0;

    for (let num of nums) {
        ans ^= num;
    }

    return ans;
};

console.log(singleNumber([4,1,2,1,2])); // 4
```

### Complexity
- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

---

## 4️⃣ Sort Colors

### Solution 1: Two Pointers with Auxiliary Array
```js
var sortColors = function(nums) {
    const newArr = new Array(nums.length).fill(1);
    let left = 0;
    let right = nums.length - 1;
    for (let i = 0; i < nums.length; i++) {
        if (nums[i] == 0) {
            newArr[left] = 0;
            left++;
        } else if (nums[i] == 2) {
            newArr[right] = 2;
            right--;
        }
    }
    for (let i = 0; i < newArr.length; i++) {
        nums[i] = newArr[i];
    }
    return nums;
};
console.log(sortColors([2, 0, 2, 1, 1, 0]));
// const arr=new Array(6).fill(1)
// console.log(arr)
```

### Solution 2: Dutch National Flag Algorithm (Optimal In-Place)
- **Idea**: Use three pointers (`low`, `mid`, `high`).
  - `0` to `low-1`: Zeros
  - `low` to `mid-1`: Ones
  - `high+1` to `n-1`: Twos
- **Steps**:
  - If `nums[mid] == 0`: Swap with `nums[low]`, increment `low` and `mid`.
  - If `nums[mid] == 1`: Increment `mid`.
  - If `nums[mid] == 2`: Swap with `nums[high]`, decrement `high`.

```js
var sortColorsDutchFlag = function(nums) {
    let low = 0;
    let mid = 0;
    let high = nums.length - 1;

    while (mid <= high) {
        if (nums[mid] === 0) {
            // Swap mid and low
            [nums[low], nums[mid]] = [nums[mid], nums[low]];
            low++;
            mid++;
        } else if (nums[mid] === 1) {
            mid++;
        } else {
            // Swap mid and high
            [nums[high], nums[mid]] = [nums[mid], nums[high]];
            high--;
        }
    }
    return nums;
};

console.log(sortColorsDutchFlag([2, 0, 2, 1, 1, 0]));
```

### Complexity
- **Time Complexity**: O(n) (One pass)
- **Space Complexity**: O(1) (In-place)

---

## 5️⃣ Majority Element (>n/2)

### Boyer-Moore Voting Algorithm
- **Idea**: If a number appears more than `n/2` times, it will survive cancellations against other numbers.
- **Steps**:
  - Maintain a `candidate` and a `count`.
  - If `count` is 0, update `candidate` to current number.
  - If current number matches `candidate`, increment `count`.
  - Otherwise, decrement `count`.

```js
var majorityElement = function(nums) {
    let candidate = null;
    let count = 0;

    for (let num of nums) {
        if (count === 0) {
            candidate = num;
        }
        
        // If current num matches candidate, count goes up, else down
        count += (num === candidate) ? 1 : -1;
    }

    return candidate;
};
// console.log(majorityElement([3,2,3])); // 3
// console.log(majorityElement([2,2,1,1,1,2,2])); // 2
```

### Complexity
- **Time Complexity**: O(n)
- **Space Complexity**: O(1)
