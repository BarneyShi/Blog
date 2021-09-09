---
title: Leetcode 17 - Letter combinations of a phone number
date: 2021-09-08 22:51:31
tags:
- leetcode
- backtracking
---
Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent. Return the answer in any order.

A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

```javascript
/**
 * @param {string} digits
 * @return {string[]}
 */
var letterCombinations = function(digits) {
  let ans = [];
  let path = [];
  if (digits.length === 0) return ans;
  let map = {'0':'', '1':'','2':'abc', '3':'def', '4':'ghi', '5':'jkl', '6':'mno', '7':'pqrs', '8':'tuv', '9':'wxyz'};
  backtracking(0, digits);
  return ans;
  
  function backtracking(index, digits) {
    if (index == digits.length) {
      ans.push(path.join(''));
      return;
    }
    const str = map[digits[index]];
    console.log(index)
    for (let i = 0; i < str.length; i++) {
      path.push(str[i]);
      backtracking(index + 1, digits);
      path.pop();
    }
  }
};
```