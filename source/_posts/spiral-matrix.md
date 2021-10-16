---
title: Leetcode 59 - Spiral matrix II
date: 2021-08-25 22:37:59
tags:
- array
---
**Note:** 
- How to initialize an empty `2D` array?
 `const arr = [...Array(n)].map(e => Array(n))`
- Keep `[start, right)` style - make the right boundary open so you won't be lost.
- Speical case for the last node when `n` is `odd`.

Given a positive integer n, generate an n x n matrix filled with elements from 1 to n2 in spiral order.

![img](https://assets.leetcode.com/uploads/2020/11/13/spiraln.jpg)
```
Input: n = 3
Output: [[1,2,3],[8,9,4],[7,6,5]]
```

![img](https://img-blog.csdnimg.cn/2020121623550681.png)

 ```javascript
/**
 * @param {number} n
 * @return {number[][]}
 */
var generateMatrix = function(n) {
  if (n === 1) return [[1]];
  let result = [...Array(n)].map(e => Array(n).fill(0));
  let count = 1;
  let rowStart = 0, rowEnd = n-1, colStart = 0, colEnd = n - 1; 
  while (count <= n**2) {
    for (let i = colStart; i < colEnd; i++) {
      result[rowStart][i] = count++;
    }
    for (let i = rowStart; i < rowEnd; i++) {
      result[i][colEnd] = count++;
    }
    for (let i = colEnd; i > colStart; i--) {
      result[rowEnd][i] = count++;
    }
    console.log(result)
    for (let i = rowEnd; i > rowStart; i--) {
      result[i][colStart] = count++;
    }
    colStart++;
    colEnd--;
    rowStart++;
    rowEnd--;
    if (n % 2 === 1 && count === n*n) {
      result[Math.floor(n/2)][Math.floor(n/2)] = n**2;
      return result;
    }
  }
  return result;
};
 ```
