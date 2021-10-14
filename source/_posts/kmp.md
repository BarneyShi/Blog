---
title: Algorithm - KMP
date: 2021-10-13 17:58:31
tags:
- algorithm
---
- What is prefix table? 
  - Table's length is the length of `pattern`. 
  - Each value is the `max` length of substring that can fit as `prefix` and `suffix`.
    - `Prefix` are substrings that don't include the last char.
    - `Suffix` are the substrings that don't include the first char.
    - For example `aaba`, `next[3] == 1` as in `a`.
- How to get the prefix table?
  - Let `i = 0`, `j = 1`. Take `aaa` for example, if `pattern[i] === pattern[j]`, then `next[j] === i + 1`.
  - if `pattern[i] !== pattern[j]`, use a while loop to find a `pattern[i]` that can make `pattern[i] !== pattern[j]`. While jumping backwards, make `i = next[i - 1]` every time.
- The techqinue:
  - Deal with situations where chars are not equal `first`. 
  - Use `while` loops.
  - Try to remember it. A algo from 1977 is now a leetcode easy question, what a world.


```javascript
/**
 * @param {string} haystack
 * @param {string} needle
 * @return {number}
 */
var strStr = function(haystack, needle) {
  if (needle.length === 0) return 0;
  const next = geneNext(needle);
  let j = 0;
  for (let i = 0; i < haystack.length; i++) {
    while (j > 0 && haystack[i] !== needle[j]) {
      j = next[j - 1];
    }
    if (haystack[i] === needle[j]) j++;
    if (j === needle.length) return i - needle.length + 1;
  }
  return -1;
};

function geneNext(str) {
  const next = [...Array(str.length).fill(0)];
  let i = 0;
  for (let j = 1; j < str.length; j++) {
    while (i > 0 && str[i] !== str[j]) {
      // We let i be next[i-1] instead of i = next[indexOf(str[j])]
      i = next[i - 1];
    }
    if (str[i] === str[j]) {
      i++;
    }
    next[j] = i;
  }
  return next;
}
```
