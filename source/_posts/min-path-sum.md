---
title: Leetcode 64 - Min path sum
date: 2021-11-23 20:51:33
tags:
- dfs
- dp
---
**`Note:`**
- `DFS`
  - Don't worry about visiting a visited cell coz we use `memo` to remmeber the min path that goes through this cell.
- `DP`
  - `dp[i][j] = grid[i][j] + min(dp[i-1][j], dp[i][j-1])`
  - Intialize `first row` and `first col` coz they don't fit above deduction.

**`Question:`**

Given a `m x n` grid filled with non-negative numbers, find a path from `top left` to `bottom right`, which minimizes the sum of all numbers along its path.

Note: You can only move either `down` or `right` at any point in time.

**`Example:`**

![img](https://assets.leetcode.com/uploads/2020/11/05/minpath.jpg)
```
Input: grid = [[1,3,1],[1,5,1],[4,2,1]]
Output: 7
Explanation: Because the path 1 → 3 → 1 → 1 → 1 minimizes the sum.
```

**`Code:`**

**`DFS`**
```javascript
/**
 * @param {number[][]} grid
 * @return {number}
 */
var minPathSum = function(grid) {
  const rows = grid.length;
  const cols = grid[0].length;
  const memo = [...Array(rows)].map(e => Array(cols));
  return dfs(0,0);

  function dfs(i, j) {
    if (memo[i][j]) return memo[i][j];
    if (i === rows - 1 && j === cols - 1) return grid[i][j];
    const dirs = [0, 1, 0];
    let res = Infinity;
    for (let k = 0; k < 2; k++) {
      const nx = i + dirs[k];
      const ny = j + dirs[k + 1];
      if (nx < 0 || nx >= rows || ny < 0 || ny >= cols) continue;
        const val = grid[i][j] + dfs(nx, ny);
        res = Math.min(res, val);
    }
    memo[i][j] = res;
    return res;
  }
};
```
**`DP`**
```javascript
const minPathSum = grid => {
    const row = grid.length,
        col = grid[0].length;
    for (let i = 1; i < row; i++) {
        grid[i][0] += grid[i - 1][0];
    }
    for (let j = 1; j < col; j++) {
        grid[0][j] += grid[0][j - 1];
    }
    for (let i = 1; i < row; i++) {
        for (let j = 1; j < col; j++) {
            grid[i][j] += Math.min(grid[i - 1][j], grid[i][j - 1]);
        }
    }
    return grid[row - 1][col - 1];
};
```