---
title: Leetcode 54 - Spiral matrix
date: 2021-11-07 00:09:17
tags:
---
**`Note:`**
- Modify matrix is eaiser.
- Use recursion to pop and add `topRow` first, then `right col most`, then `reversed bottom row`, then `leftmost col`.

**`Question:`**

Given an m x n matrix, return all elements of the matrix in spiral order.

**`Example:`**

![img](https://assets.leetcode.com/uploads/2020/11/13/spiral1.jpg)
```
Input: matrix = [[1,2,3],[4,5,6],[7,8,9]]
Output: [1,2,3,6,9,8,7,4,5]
```

**`Code:`**
```javascript
/**
 * @param {number[][]} matrix
 * @return {number[]}
 */
var spiralOrder = function (matrix) {
  let res = [];
  traverse(matrix);
  return res;

  function traverse(matrix) {
    if (matrix.length === 0) return;
    if (matrix.length === 1) {
      res.push(...matrix.pop());
      return;
    }
    const topRow = matrix.shift();
    const bottomRow = matrix.pop();
    let rightCol = [];
    let leftCol = [];
    for (let i = 0; i < matrix.length; i++) {
      const right = matrix[i].pop();
      right && rightCol.push(right);
      const left = matrix[i].shift();
      left && leftCol.push(left);
    }
    res.push(...topRow)
    res.push(...rightCol)
    bottomRow.length && res.push(...bottomRow.reverse())
    leftCol.length && res.push(...leftCol.reverse());
    traverse(matrix);
  }
};
```