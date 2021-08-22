---
title: combinations
date: 2021-08-21 17:46:32
tags:
- leetcode
- medium
- backtracking
---
Given two integers n and k, return all possible combinations of k numbers out of the range [1, n].

You may return the answer in any order.

**Example 1:**

Input: n = 4, k = 2
Output:
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
**Note:** One of the most typical backtracking problems. Remeber to use spread operator while pushing element into ans because we are passing `path` as `reference`.
```javascript
/**
 * @param {number} n
 * @param {number} k
 * @return {number[][]}
 */
var combine = function(n, k) {
  let ans = [];
  let path = [];
  
  backtrack(n, k, 1);
  return ans;
  
  function backtrack(n, k, startIndex) {
    if (path.length == k) {
      ans.push([...path]);
      return;
    }
    
    for (let i = startIndex; i <= n; i++) {
      path.push(i);
      backtrack(n, k, i+1);
      path.pop();
    }
  }
};
```
