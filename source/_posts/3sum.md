---
title: Leetcode 15 - 3Sum
date: 2021-10-12 01:56:28
tags:
- double pointer
---
**`Note:`**
- For each `i`, do what we did in `2sum` between `[i+1, length - 1]` for target `-nums[i]`.
- Even with `Set`, it cannot check whethere we've already had a same array in the `Set`. Because set checks duplicates by `reference` for objects/arrays.
- Sort nums, and avoid duplicates manually.

**`Question:`**

Given an integer array nums, return all the triplets [nums[i], nums[j], nums[k]] such that i != j, i != k, and j != k, and nums[i] + nums[j] + nums[k] == 0.

Notice that the solution set must `not` contain `duplicate` triplets.

**`Example:`**
```
Input: nums = [-1,0,1,2,-1,-4]
Output: [[-1,-1,2],[-1,0,1]]
```

**`Code:`**
```javascript
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var threeSum = function(nums) {
  nums.sort((a, b) => a - b);
  const result = [];
  for (let i = 0; i < nums.length - 1; i++) {
    /* Avoid duplicates */
    if (i >= 1 && nums[i] === nums[i-1]) continue;
    let left = i + 1;
    let right = nums.length - 1;
    const target = -nums[i];
    while (left < right) {
      const sum = nums[left] + nums[right];
      if (sum > target) {
        right--;
        continue;
      }
      if (sum < target) {
        left++;
        continue;
      }
      result.push([nums[i], nums[left], nums[right]]);
      /* Avoid duplicates */
      while(left < right && nums[right] === nums[right - 1]) {
        right--;
      }
      while(left < right && nums[left] === nums[left + 1]) {
        left++;
      }
      right--;
      left++;
    }
  }
  return result;
};
```