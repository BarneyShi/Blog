---
title: Leetcode 15 - 3Sum
date: 2021-09-20 22:17:32
tags:
- leetcode
- double pointer
- array
---
**`Note`**
- Use `double pointer` after `sorting` nums.
- Iterate by `i`, then from `i+1` and `nums.length-1`, use `double pointers`.
- To avoid TLE, we need to skip repetitive elements by continuously `incrementing` or `decrementing` two pointers.

Given an integer array nums, return all the triplets [nums[i], nums[j], nums[k]] such that i != j, i != k, and j != k, and nums[i] + nums[j] + nums[k] == 0.

Notice that the solution set must not contain duplicate triplets.

**Example**
```
Input: nums = [-1,0,1,2,-1,-4]
Output: [[-1,-1,2],[-1,0,1]]
```

```javascript
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var threeSum = function(nums) {
  let result = [];
  if (nums.length < 3) return result;
  nums.sort((a, b) => (a - b));
  for (let i = 0; i < nums.length - 2; i++) {
    if (nums[i] > 0) break;
    if (i > 0 && nums[i] === nums[i-1]) continue;
    let left = i + 1, right = nums.length - 1;
    while (left < right) {
      const sum = nums[left] + nums[right] + nums[i];
      if (sum < 0) {
        left++;
        continue;
      } 
      if (sum > 0) {
        right--;
        continue;
      }
      result.push([nums[i], nums[left], nums[right]]);
      while (left < right && nums[left] === nums[++left]);
      while (left < right && nums[right] === nums[--right]);
    }
  }
  return result;
};
```