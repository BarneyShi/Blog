---
title: Leetcode 79 - Word search
date: 2021-11-10 00:57:00
tags:
- dfs
- backtracking
---
**`Note:`**
- This is a `DFS + backtracking` problem.
- Intialize `path` with `path[word[0]]`.
- Call `dfs()` from `board[i][j] = word[0]`.
- Use `used[][]` to mark elements that have been visited.
- Use `directional array` to get `4 directions`.

**`Question:`**

Given an `m x n` grid of characters `board` and a string `word`, return `true` if word exists in the grid.

The word can be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once.

**`Example:`**

![img](https://assets.leetcode.com/uploads/2020/11/04/word2.jpg)
```
Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
Output: true
```

**`Code:`**
```javascript
/**
 * @param {character[][]} board
 * @param {string} word
 * @return {boolean}
 */
 var exist = function (board, word) {
  const rows = board.length;
  const cols = board[0].length;
  let used = [...Array(rows)].map(e => Array(cols).fill(false));
  let path = [word[0]];
  let flag = false;

  for (let i = 0; i < rows; i++) {
    for (let j = 0; j < cols; j++) {
      if (flag) return true;
      if (board[i][j] === word[0]) {
        used[i][j] = true;
        dfs(board, word, i, j, 1);
        used[i][j] = false;
      }
    }
  }
  return flag;

  function dfs(board, word, x, y, wordIndex) {
    if (flag) return;
    if (path.join('') === word) {
      flag = true;
      return;
    }
    const dirs = [-1, 0, 1, 0, -1];
    for (let k = 0; k < 4; k++) {
      const nx = x + dirs[k];
      const ny = y + dirs[k + 1];
      if (nx < 0 || nx >= rows || ny < 0 || ny >= cols) continue;
      if (board[nx][ny] !== word[wordIndex] || used[nx][ny]) continue;
      used[nx][ny] = true;
      path.push(board[nx][ny]);
      dfs(board, word, nx, ny, wordIndex + 1);
      used[nx][ny] = false;
      path.pop();
    }
  }
};
```