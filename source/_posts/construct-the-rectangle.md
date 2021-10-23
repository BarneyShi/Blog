---
title: Leetcode 492 - Construct the rectangle
date: 2021-10-22 17:38:17
tags:
- double pointer
---
**`Note:`**
- `Double pointer` set as `floor(sqrt(area))`.
- Check if `left*right === area`. If too big, `left--`, otherwise `right++`

**`Question:`**

A web developer needs to know how to design a web page's size. So, given a specific rectangular web page’s area, your job by now is to design a rectangular web page, whose length L and width W satisfy the following requirements:

1. The area of the rectangular web page you designed must equal to the given target area.
2. The width W should not be larger than the length L, which means `L >= W`.
3. The difference between length L and width W should be as small as possible.
Return an array `[L, W]` where `L` and `W` are the length and width of the web page you designed in sequence.

**`Example:`**
```
Input: area = 4
Output: [2,2]
Explanation: The target area is 4, and all the possible ways to construct it are [1,4], [2,2], [4,1]. 
But according to requirement 2, [1,4] is illegal; according to requirement 3,  [4,1] is not optimal compared to [2,2]. So the length L is 2, and the width W is 2.

Input: area = 122122
Output: [427,286]
```

**`Code:`**
```javascript
/**
 * @param {number} area
 * @return {number[]}
 */
var constructRectangle = function(area) {
  const middle = Math.floor(Math.sqrt(area));
  let left = middle, right = middle;
  while (left * right !== area) {
    const res = left * right;
    if (res > area) {
      left--;
    } else {
      right++;
    }
  }
  return [right, left];
};
```