---
title: Leetcode 96 - Unique Binary Search Tree
date: 2021-09-02 23:09:35
tags:
- leetcode
- bst
- dp
---
Given an integer n, return the number of structurally unique BST's (binary search trees) which has exactly n nodes of unique values from 1 to n.

**Example:**
![img](https://assets.leetcode.com/uploads/2021/01/18/uniquebstn3.jpg)
```
Input: n = 3
Output: 5
```

**`Note:`** 
- `DP[i]` represents the number of unique BST trees.
- The DP formula is `DP[i] += DP[j] + DP[i-j-1]`.
  - Explaination: 
  ![img](https://img-blog.csdnimg.cn/20210107093106367.png)
  ![img](https://img-blog.csdnimg.cn/20210107093129889.png)
  `DP[3] = DP[0]*DP[2] + DP[1]*DP[1] + DP[2]*DP[0]`. 
  - For n=3, when 1 is the root, the number of trees with 1 as the root is `DP[0]*DP[2]`. When 2 is the root, the number of trees with 2 as the root is `DP[1]*DP[1]`. When 3 is the root, the number of trees with 3 as the root is `DP[2]*DP[0]`.

```javascript
/**
 * @param {number} n
 * @return {number}
 */
var numTrees = function(n) {
  let dp = [...Array(n+1).fill(0)];
  dp[0] = 1;
  for (let i = 1; i <= n; i++) {
    for (let j = 0; j <= i-1; j++) {
      dp[i] += dp[j]*dp[i-j-1];
    }
  }
  return dp[n];
};
```