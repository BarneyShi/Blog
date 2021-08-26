---
title: Leetcode 59 - Spiral matrix
date: 2021-08-25 22:37:59
tags:
- leetcode
- array
- medium
---
Given a positive integer n, generate an n x n matrix filled with elements from 1 to n2 in spiral order.

![img](https://assets.leetcode.com/uploads/2020/11/13/spiraln.jpg)
```
Input: n = 3
Output: [[1,2,3],[8,9,4],[7,6,5]]
```
**Note:** 
- How to initialize an empty `2D` array?
 `const arr = [...Array(n)].map(e => Array(n))`
- Keep `[start, right)` style - make the right boundary open so you won't be lost.

![img](https://img-blog.csdnimg.cn/2020121623550681.png)

 ```javascript
 /**
 * @param {number} n
 * @return {number[][]}
 */
var generateMatrix = function(n) {
  if (n === 1) return [[1]];
  let ans = [...Array(n)].map(e => Array(n));
  let rowStart = 0, rowEnd = n - 1, colStart = 0, colEnd = n - 1;
  let counter = 1;
  while (rowStart <= rowEnd && colStart <= colEnd) {
    for (let i = colStart; i < colEnd; i++) {
      ans[rowStart][i] = counter++;
    }
    for (let i = rowStart; i < rowEnd; i++) {
      ans[i][colEnd] = counter++;
    }
    for (let i = colEnd; i > colStart; i--) {
      ans[rowEnd][i] = counter++;
    }
    for (let i = rowEnd; i > rowStart; i--) {
      ans[i][colStart] = counter++;
    }
    rowStart++;
    rowEnd--;
    colStart++;
    colEnd--;
    // Need to fill the last one if n is odd.
    if (rowStart === rowEnd && colStart === colEnd) ans[(n-1)/2][(n-1)/2] = n**2; 
  }
  return ans;
};
 ```
