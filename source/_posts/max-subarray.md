---
title: Leetcode 53 - Max subarray
date: 2021-09-22 17:34:13
tags:
- dp
---
**`Note`**
- For each element, there are two situations, one to `include it` with prev array, or start with it as a `new array`.
- DP deduction is `dp[i] = max(dp[i-1] + nums[i], nums[i]);
- `dp[i]` represents the largest sum of subarray that `ends with nums[i]`.
- Need a `result` to store the result.

Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

A subarray is a contiguous part of an array.

**Example**
```
Input: nums = [-2,1,-3,4,-1,2,1,-5,4]
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
```

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var maxSubArray = function(nums) {
  if (nums.length === 1) return nums[0];
  let dp = [...Array(nums.length).fill(0)];
  dp[0] = nums[0];
  let result = nums[0];
  for (let i = 1; i < nums.length; i++) {
    dp[i] = Math.max(dp[i-1] + nums[i], nums[i]);
    result = Math.max(dp[i], result);
  }
  console.log(dp)
  return result;
};
```