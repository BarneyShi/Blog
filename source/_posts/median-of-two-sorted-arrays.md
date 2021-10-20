---
title: Leetcode 4 - Median of two sorted arrays
date: 2021-10-19 23:35:18
tags:
- double pointer
---
**`Note:`**


**`Question:`**

Given two sorted arrays nums1 and nums2 of size m and n respectively, return the median of the two sorted arrays.

The overall run time complexity should be `O(log (m+n))`.

**`Example:`**
```
Input: nums1 = [1,2], nums2 = [3,4]
Output: 2.50000
Explanation: merged array = [1,2,3,4] and median is (2 + 3) / 2 = 2.5.
```

**`Code:`**


**`Double pointer with O(m+n)`**
```javascript
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number}
 */
var findMedianSortedArrays = function (nums1, nums2) {
  const m = nums1.length, n = nums2.length;
  const middle = Math.floor((m+n)/2) + 1;
  let newArr = [...Array(middle).fill(0)];

  let p1 = 0, p2 = 0, isNum1Out = nums1.length === 0, isNum2Out = nums2.length === 0;
  
  for (let i = 0 ; i < newArr.length; i++) {
    if (isNum1Out) {
      newArr[i] = nums2[p2];
      p2++;
      continue;
    }
    if (isNum2Out) {
      newArr[i] = nums1[p1];
      p1++;
      continue;
    }
    if (nums1[p1] < nums2[p2]) {
      newArr[i] = nums1[p1];
      if (p1 === nums1.length - 1) {
        isNum1Out = true;
        continue;
      }
      p1++;
    } else {
      newArr[i] = nums2[p2];
      if (p2 === nums2.length - 1) {
        isNum2Out =  true;
        continue;
      }
      p2++;
    }
  }
  if ((m+n) % 2 === 1) {
    return newArr[Math.floor((m+n)/2)];
  } else {
    return (newArr[newArr.length - 1] + newArr[newArr.length - 2]) / 2;
  }
};
```