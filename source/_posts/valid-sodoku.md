---
title: Leetcode 36 - Valid sodoku
date: 2021-11-04 23:47:58
tags:
---
**`Note:`**
- Just use brute force way is enough.
- Don't have to iterate once and solve the problem.
- Save some time for other more meaningful things.

**`Question:`**

Determine if a `9 x 9` Sudoku board is valid. Only the filled cells need to be validated according to the following rules:

- Each row must contain the digits `1-9` without repetition.
- Each column must contain the digits `1-9` without repetition.
- Each of the nine 3 x 3 sub-boxes of the grid must contain the digits `1-9` without repetition.

`Note`:

- A Sudoku board (partially filled) could be valid but is not necessarily solvable.
- Only the filled cells need to be validated according to the mentioned rules.

**`Example:`**

![img](https://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png)
```
Output: true
```

**`Code:`**
```javascript
/**
 * @param {character[][]} board
 * @return {boolean}
 */
 var isValidSudoku = function (board) {
  const rows = board.length;
  const cols = board[0].length;

  for (let i = 0; i < rows; i++) {
    let rowMap = new Map();
    for (const char of board[i]) {
      if (!isNaN(char) && rowMap.has(char)) return false;
      if (!isNaN(char)) rowMap.set(char, true);
    }
  }
  for (let j = 0; j < cols; j++) {
    let colMap = new Map();
    for (let i = 0; i < rows; i++) {
      const char = board[i][j];
      if (!isNaN(char) && colMap.has(char)) return false;
      if (!isNaN(char)) colMap.set(char, true);
    }
  }
  return check3x3(0, 0) && check3x3(0, 3) && check3x3(0, 6) && check3x3(3, 0) && check3x3(3, 3) && check3x3(3, 6) && check3x3(6, 0) && check3x3(6, 3) && check3x3(6, 6);

  function check3x3(rowStart, colStart) {
    let arr = [];
    for (let i = 0; i < 3; i++) {
      arr = arr.concat(board[rowStart + i].slice(colStart, colStart + 3));
    }
    let map = new Map();
    for (const char of arr) {
      if (!isNaN(char) && map.has(char)) return false;
      if (!isNaN(char)) map.set(char, true);
    }
    return true;
  }
};
```