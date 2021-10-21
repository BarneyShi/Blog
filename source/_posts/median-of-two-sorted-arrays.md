---
title: Leetcode 4 - Median of two sorted arrays
date: 2021-10-19 23:35:18
tags:
- double pointer
---
**`Note:`**
- It requires `O(log(m+n))` time complexity, apparently, we need `binary search`.
- How to find the `median`? The median separates the array in half.
  - ![img](https://i.imgur.com/Bq707Eb.png)
- For convenience, we use binary search on the shorter array between nums1 and nums2. If nums2 is shorter than nums1, we swtich them.
- First, we get the `index of median` of `nums1` using `(start + end) >> 1`. Here, both operands are indexes. By basic math, the cut point in nums2 should be `half - i - 2`. Half is the half length of nums1 and nums2 together, we substract (i+1) from it, which is the `length` of `first part` of nums1. But because we need `index`, we still need to minus 1.
- `L1 = nums[i], R1 = nums[i+1]`. `L2 = nums[j], R2 = nums[j+1]`.
- When can we say we've found the result? `L1 <= R2 && L2 <= R1`.
- What if we didn't? 
  - If `L1 > R2`, we need to make `L1` shorter, so `end = i - 1`. If `L2 > R1`, which means `L1` is too short. We need to make i bigger, `start = i + 1`.
- For example, when `L1 > R2`, what would happen will be like 
  - ![img](https://i.imgur.com/Uxr6dul.png)

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

**`Binary search with O(log(m+n))`**
```javascript
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number}
 */
var findMedianSortedArrays = function (nums1, nums2) {
  if (nums2.length < nums1.length) [nums1, nums2] = [[...nums2], [...nums1]];
  const m = nums1.length, n = nums2.length;
  const half = (m + n) >> 1;
  const len = m + n;

  let start = 0, end = m - 1;

  while (true) {
    let i = (start + end) >> 1; // A
    let j = half - i - 2; // B

    let L1 = i < 0 ? -Infinity : nums1[i];
    let L2 = j < 0 ? -Infinity : nums2[j];
    let R1 = (i + 1 >= m) ? Infinity : nums1[i + 1];
    let R2 = j + 1 >= n ? Infinity : nums2[j + 1];

    if (L1 <= R2 && L2 <= R1) {
      if (len % 2 === 1) {
        return Math.min(R1, R2);
      } else {
        return (Math.max(L1, L2) + Math.min(R1, R2)) / 2;
      }
    } else if (L1 > R2) {
      end = i - 1;
    } else {
      start = i + 1;
    }
  }
};
```


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