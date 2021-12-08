---
title: Leetcode 34 - Find first and last position of element in sorted array
date: 2021-10-27 21:38:57
tags:
- double pointers
---
**`Note:`**
- The required time complexity is `O(logn)`, so we need to use `binary search`, and DON'T USE `DOUBLE POINTERS`!
- Double-pointer is `O(n)` but not `O(logn)`.
- Take findLeftBoundary for example:
  - When `nums[middle] < target`, `left = middle + 1`.
  - When `nums[middle] > target`, `right = middle - 1`.
  - When `nums[middle] === target`, `left` must be on the left side. But we need to check edge cases:
    - `middle === 0` or `nums[middle - 1] !== target`. Return middle in this case.
    - Otherwise `right = middle - 1`;

**`Question:`**

Given an array of integers nums sorted in non-decreasing order, find the starting and ending position of a given target value.

If target is not found in the array, return [-1, -1].

You must write an algorithm with O(log n) runtime complexity.

**`Example:`**
```
Input: nums = [5,7,7,8,8,10], target = 8
Output: [3,4]
```

**`Code:`**
```javascript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var searchRange = function(nums, target) {
  const left = findLeftBoundary(nums, target);
  const right = findRightBoundary(nums, target);
  return [left, right];

  function findLeftBoundary(nums, target) {
    let left = 0, right = nums.length - 1;
    while (left <= right) {
      const middle = left + ~~((right - left) / 2);
      if (nums[middle] > target) {
        right = middle - 1;
      } else if (nums[middle] < target) {
        left = middle + 1;
      } else if (nums[middle] === target) {
        if (middle > 0 && nums[middle - 1] !== target || middle === 0) return middle;
        right = middle - 1;
      }
    }
    return -1;
  }

  function findRightBoundary(nums, target) {
    let left = 0, right = nums.length - 1;
    while (left <= right) {
      const middle = left + ~~((right - left) / 2);
      if (nums[middle] > target) {
        right = middle - 1;
      } else if (nums[middle] < target) {
        left = middle + 1;
      } else if (nums[middle] === target) {
        if (middle < nums.length - 1 && nums[middle + 1] !== target || middle === nums.length - 1) return middle;
        left = middle + 1;
      }
    }
    return -1;
  }
};
```