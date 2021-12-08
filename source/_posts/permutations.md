---
title: Leetcode 46 - Permutations
date: 2021-09-11 18:19:18
tags:
- dfs
- backtracking
---
**`Note:`**
- This is a backtracking problem.
- We don't need `startIndex` because each path must contain all elements.
- We do need a `used` array to keep track if we've used the element.

Given an array nums of distinct integers, return all the possible permutations. You can return the answer in any order.

**Example**
```
Input: nums = [1,2,3]
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
```

```javascript
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var permute = function(nums) {
  let ans = [];
  let path = [];
  let used = [...Array(nums.length).fill(false)]
  backtracking(nums);
  return ans;
  
  function backtracking(nums) {
    if (path.length === nums.length) {
      ans.push([...path]);
      return;
    }
    
    for (let i = 0; i < nums.length; i++) {
      if (!used[i]) {
        path.push(nums[i]);
        used[i] = true;
        backtracking(nums);
        used[i] = false;
        path.pop();
      } else {
        continue;
      }
    }
  }
};
```

