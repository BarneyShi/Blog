---
title: Leetcode 461 - Hamming distance
date: 2021-10-24 19:00:07
tags:
- bitwise
---
**`Note:`**
- Use `XOR` ^ to check if two binary numbers are different on the last digit.
- Use `>>` to shift.
- Be careful of precedence such as `!==` has a higher precedence than `&`.

**`Question:`**

The `Hamming distance` between two integers is the number of positions at which the corresponding bits are different.

Given two integers `x` and `y`, return the Hamming distance between them.

**`Example:`**
```
Input: x = 1, y = 4
Output: 2
Explanation:
1   (0 0 0 1)
4   (0 1 0 0)
       ↑   ↑
The above arrows point to positions where the corresponding bits are different.
```

**`Code:`**
```javascript
/**
 * @param {number} x
 * @param {number} y
 * @return {number}
 */
 var hammingDistance = function(x, y) {
  let result = 0;
  while (x !== 0 || y !== 0) {
    if (x & 1 ^ y & 1) result++;
    x = x >> 1;
    y = y >> 1;
  }
  return result;
};
```