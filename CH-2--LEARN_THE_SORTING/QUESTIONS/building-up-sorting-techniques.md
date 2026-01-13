# Building Up Sorting Techniques (JavaScript)

---

## 1. Selection Sort

### Idea
- Repeatedly select the minimum element
- Place it at the correct position

```js
function selectionSort(arr) {
  let n = arr.length;

  for (let i = 0; i < n - 1; i++) {
    let minIdx = i;
    for (let j = i + 1; j < n; j++) {
      if (arr[j] < arr[minIdx]) minIdx = j;
    }
    [arr[i], arr[minIdx]] = [arr[minIdx], arr[i]];
  }
  return arr;
}
```

**Time:** O(n²) | **Space:** O(1)

---

## 2. Insertion Sort

### Idea
- Build sorted array one element at a time

```js
function insertionSort(arr) {
  for (let i = 1; i < arr.length; i++) {
    let key = arr[i];
    let j = i - 1;

    while (j >= 0 && arr[j] > key) {
      arr[j + 1] = arr[j];
      j--;
    }
    arr[j + 1] = key;
  }
  return arr;
}
```

**Best:** O(n) | **Worst:** O(n²) | **Space:** O(1)

---

## 3. Merge Sort

### Idea
- Divide array into halves
- Sort recursively and merge

```js
function mergeSort(arr) {
  if (arr.length <= 1) return arr;

  let mid = Math.floor(arr.length / 2);
  let left = mergeSort(arr.slice(0, mid));
  let right = mergeSort(arr.slice(mid));

  return merge(left, right);
}

function merge(left, right) {
  let res = [], i = 0, j = 0;

  while (i < left.length && j < right.length) {
    if (left[i] < right[j]) res.push(left[i++]);
    else res.push(right[j++]);
  }
  return res.concat(left.slice(i)).concat(right.slice(j));
}
```

**Time:** O(n log n) | **Space:** O(n)

---

## 4. Recursive Bubble Sort

```js
function bubbleSortRec(arr, n = arr.length) {
  if (n === 1) return arr;

  for (let i = 0; i < n - 1; i++) {
    if (arr[i] > arr[i + 1]) {
      [arr[i], arr[i + 1]] = [arr[i + 1], arr[i]];
    }
  }
  return bubbleSortRec(arr, n - 1);
}
```

**Time:** O(n²) | **Space:** O(n)

---

## 5. Recursive Insertion Sort

```js
function insertionSortRec(arr, n = arr.length) {
  if (n <= 1) return arr;

  insertionSortRec(arr, n - 1);

  let last = arr[n - 1];
  let j = n - 2;

  while (j >= 0 && arr[j] > last) {
    arr[j + 1] = arr[j];
    j--;
  }
  arr[j + 1] = last;

  return arr;
}
```

**Time:** O(n²) | **Space:** O(n)

---

## 6. Quick Sort

### Idea
- Pick pivot
- Partition array

```js
function quickSort(arr) {
  if (arr.length <= 1) return arr;

  let pivot = arr[arr.length - 1];
  let left = [], right = [];

  for (let i = 0; i < arr.length - 1; i++) {
    if (arr[i] < pivot) left.push(arr[i]);
    else right.push(arr[i]);
  }
  return [...quickSort(left), pivot, ...quickSort(right)];
}
```

**Avg:** O(n log n) | **Worst:** O(n²) | **Space:** O(n)

---

## 7. Counting Sort

```js
function countSort(arr) {
  let max = Math.max(...arr);
  let count = Array(max + 1).fill(0);

  for (let num of arr) count[num]++;
  let idx = 0;

  for (let i = 0; i < count.length; i++) {
    while (count[i]-- > 0) arr[idx++] = i;
  }
  return arr;
}
```

**Time:** O(n + k) | **Space:** O(k)

---

## 8. Radix Sort

```js
function radixSort(arr) {
  let max = Math.max(...arr);

  for (let exp = 1; Math.floor(max / exp) > 0; exp *= 10) {
    countingSortByDigit(arr, exp);
  }
  return arr;
}

function countingSortByDigit(arr, exp) {
  let output = Array(arr.length).fill(0);
  let count = Array(10).fill(0);

  for (let i = 0; i < arr.length; i++) {
    let idx = Math.floor(arr[i] / exp) % 10;
    count[idx]++;
  }

  for (let i = 1; i < 10; i++) count[i] += count[i - 1];

  for (let i = arr.length - 1; i >= 0; i--) {
    let idx = Math.floor(arr[i] / exp) % 10;
    output[--count[idx]] = arr[i];
  }

  for (let i = 0; i < arr.length; i++) arr[i] = output[i];
}
```

**Time:** O(d·(n + k)) | **Space:** O(n + k)

---

### Summary
- Comparison sorts: Bubble, Selection, Insertion, Merge, Quick
- Non-comparison sorts: Counting, Radix
- Sorting choice depends on **data size, range, and constraints**


---

## 0. Bubble Sort (Optimized)

### Idea
- Repeatedly compare adjacent elements
- Swap if they are in the wrong order
- Largest element bubbles to the end after each pass
- Stop early if no swaps happen in a pass

```js
function bubbleSort(arr) {
  let n = arr.length;

  for (let i = 0; i < n - 1; i++) {
    let swapped = false;

    for (let j = 0; j < n - 1 - i; j++) {
      if (arr[j] > arr[j + 1]) {
        [arr[j], arr[j + 1]] = [arr[j + 1], arr[j]];
        swapped = true;
      }
    }

    // If no swaps → array already sorted
    if (!swapped) break;
  }

  return arr;
}
```

### Complexity
- **Best Case:** O(n)
- **Average Case:** O(n²)
- **Worst Case:** O(n²)
- **Space Complexity:** O(1)

> First sorting algorithm to learn; helps build intuition.
