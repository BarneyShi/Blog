---
title: Leetcode 73 - Set matrix zeroes
date: 2021-11-08 00:22:09
tags:
---
**`Note:`**
- Use `[prev, 0]` to mark zeroes.
- Need to check if cur tile is an `array` or `num`.

**`Question:`**

Given an `m x n` integer matrix `matrix`, if an element is 0, set its `entire row and column` to `0`'s, and return the matrix.

You must do it in place.

**`Example:`**

![img](https://assets.leetcode.com/uploads/2020/08/17/mat1.jpg)
```
Input: matrix = [[1,1,1],[1,0,1],[1,1,1]]
Output: [[1,0,1],[0,0,0],[1,0,1]]
```

**`Code:`**
```javascript
/**
 * @param {number[][]} matrix
 * @return {void} Do not return anything, modify matrix in-place instead.
 */
var setZeroes = function (matrix) {
  const rows = matrix.length;
  const cols = matrix[0].length;
  for (let i = 0; i < rows; i++) {
    for (let j = 0; j < cols; j++) {
      const cur = matrix[i][j];
      if (!isNaN(cur) && cur === 0 || isNaN(cur) && cur[0] === 0) {
        for (let m = 0; m < rows; m++) {
          const tmp = matrix[m][j];
          if (isNaN(tmp)) continue;
          matrix[m][j] = [matrix[m][j], 0];
        }
        for (let n = 0; n < cols; n++) {
          const tmp = matrix[i][n];
          if (isNaN(tmp)) continue;
          matrix[i][n] = [matrix[i][n], 0];
        }
      }
    }
  }
  for (let i = 0; i < rows; i++) {
    for (let j = 0; j < cols; j++) {
      const cur = matrix[i][j];
      if (isNaN(cur)) {
        matrix[i][j] = cur[1];
      }
    }
  }
};
```