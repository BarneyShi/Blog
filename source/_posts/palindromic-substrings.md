---
title: Leetcode 647 - Palindromic substrings
date: 2021-09-24 02:26:55
tags:
- dp
---

Given a string s, return the number of palindromic substrings in it.

A string is a palindrome when it reads the same backward as forward.

A substring is a contiguous sequence of characters within the string.

**Example**
```
Input: s = "abc"
Output: 3
Explanation: Three palindromic strings: "a", "b", "c".
```

**`Brute Force`**
```javascript
/**
 * @param {string} s
 * @return {number}
 */
var countSubstrings = function(s) {
  if (s.length === 1) return 1;
  let result = 1;
  for (let i = 1; i < s.length; i++) {
    for (let j = 0; j <= i; j++) {
      let str = s.slice(j, i + 1);
      if (isPalindrome(str)) {
        result++; 
      }
    }
  }
  return result;
};

function isPalindrome(str) {
  let left = 0, right = str.length-1;
  while (left < right) {
    if (str[left++] !== str[right--]) {
      return false;
    }
  }
  return true;
}
```
