---
title: Leetcode 45 - Jump game II
date: 2021-10-05 22:08:37
tags:
- dp
- greedy
---
**`Note:`**
-`DP`
  - `dp[i]` means the min steps from `index 0` to `index i`.
  - For each `i` we need to find the min dp value between `[0, i-1]` and add `1` to it.

Given an array of non-negative integers nums, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Your goal is to reach the last index in the minimum number of jumps.

You can assume that you can always reach the last index.

**Example**
```
Input: nums = [2,3,1,1,4]
Output: 2
Explanation: The minimum number of jumps to reach the last index is 2. Jump 1 step from index 0 to 1, then 3 steps to the last index.
```

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var jump = function(nums) {
  let dp = [...Array(nums.length).fill(Infinity)];
  dp[0] = 0;
  for (let i = 1; i < nums.length; i++) {
    for (let j = 0; j < i; j++) {
      if (i <= nums[j] + j) {
        dp[i] = Math.min(dp[i], dp[j] + 1);
      }
    }
  }
  return dp[nums.length - 1];
};
```