---
title: Leetcode 868 - Binary gap
date: 2022-01-17 16:32:06
tags:
- bitwise
---
**`Note:`**
- Use a flag to denote that we've found the first 1.
- Count distance.

**`Question:`**

Given a positive integer `n`, find and return the `longest distance` between any `two adjacent 1's` in the binary representation of n. If there are no two adjacent 1's, return 0.

Two 1's are `adjacent` if there are `only 0's separating them` (possibly no 0's). The distance between two 1's is the absolute difference between their bit positions. For example, the two 1's in "1001" have a distance of 3.

**`Example:`**
```
Input: n = 22
Output: 2
Explanation: 22 in binary is "10110".
The first adjacent pair of 1's is "10110" with a distance of 2.
The second adjacent pair of 1's is "10110" with a distance of 1.
The answer is the largest of these two distances, which is 2.
Note that "10110" is not a valid pair since there is a 1 separating the two 1's underlined.
```

**`Code:`**
```javascript
/**
 * @param {number} n
 * @return {number}
 */
 var binaryGap = function(n) {
  let start = 0, max = 0;
  let distance = 0;
  let hasFoundTheFirstOne = false;
  while (n !== 0) {
    if ((n & 1) === 0 && !hasFoundTheFirstOne) {
      n = n >> 1;
      distance++;
      continue;
    }
    if ((n & 1) === 1 && !hasFoundTheFirstOne) {
      hasFoundTheFirstOne = !hasFoundTheFirstOne;
      start = distance;
    } else if ((n & 1) === 1) {
      if (distance - start > max) max = distance - start;
      start = distance;
    }
    distance++;
    n = n >> 1;
  }
  return max;
};
```