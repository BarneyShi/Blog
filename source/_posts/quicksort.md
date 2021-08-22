---
title: Sort - Quicksort
date: 2021-08-21 21:51:51
tags:
- sort
- algorithm
---
### Analysis:
- Average time complexity: After a long deduction, it's `O(nlogn)`
- Worst time complexity: It happens when the `pivot` is always picked as the `largest` or `smallest` value. So it's `O(n^2)`. 
### Steps: 
1. Choose an element as a pivot
2. Next, partition the remaining items into two disjoint sublists,
such that all items greater than the pivot follow it, and all
elements less than the pivot precede it.
3. Start recursion.
### Note: The tricky part is how to implememnt `partition`.
```javascript
const qSort = (arr, start, end) => {
  /* Terminating calls */
  if (start >= end) {
    return;
  }
  let pivotIndex = partition(arr, start, end);
  qSort(arr, start, pivotIndex - 1);
  qSort(arr, pivotIndex + 1, end);
};

const partition = (arr, start, end) => {
  // Initialize the point as the start
  let pointer = start + 1;
  // Initialize pivot value as the first element
  let pivotValue = arr[start];
  for (let i = pointer; i <= end; i++) {
    if (arr[i] < pivotValue) {
      [arr[i], arr[pointer]] = [arr[pointer], arr[i]];
      pointer++;
    }
  }
  /* Here we swtich pivot value with (pointer - 1) instead of (pointer), because the pointer is currently pointing to an element bigger than pivot value. Think about that */
  [arr[pointer - 1], arr[start]] = [arr[start], arr[pointer - 1]];
  return pointer - 1;
};
```
Take `[4, 2, 7, 1, 3, 9, 8]` for example:
```
Intial: [4, 2, 7, 1, 3, 9, 8]
    *
After iteration: [4, 2, 7, 1, 3, 9, 8]
                        *
After iteration: [4, 2, 7, 1, 3, 9, 8]
                        *
After iteration: [4, 2, 1, 7, 3, 9, 8]
                           *
After iteration: [4, 2, 1, 3, 7, 9, 8]
                              *
After iteration: [4, 2, 1, 3, 7, 9, 8]
                              *
... end                              
```
As you can say, eventually, the pointer will be pointing to an element that is `bigger` than our `pivot`
                  