---
title: Leetcode 131 - Palindrome partitioning
date: 2021-09-11 00:43:49
tags:
- leetcode
- backtracking
---
**`Note:`**
- This is a backtracking problem.
- Need a helper `isPalindrome`
- We need to pass a param `startIndex` as usual, and `[startIndex, i]` is just what we got by spliting.
![img](https://code-thinking.cdn.bcebos.com/pics/131.%E5%88%86%E5%89%B2%E5%9B%9E%E6%96%87%E4%B8%B2.jpg)

Given a string s, partition s such that every substring of the partition is a palindrome. Return all possible palindrome partitioning of s.

A palindrome string is a string that reads the same backward as forward.

**Example:**
```
Input: s = "aab"
Output: [["a","a","b"],["aa","b"]]
```

```javascript
/**
 * @param {string} s
 * @return {string[][]}
 */
var partition = function(s) {
  let ans = [];
  let path = [];
  backtracking(s, 0);
  return ans;
  
  function backtracking(s, startIndex) {
    if (startIndex > s.length) return;
    if (startIndex === s.length) {
      ans.push([...path]);
      return;
    }
  
    for (let i = startIndex; i < s.length; i++) {
      let substr = s.substr(startIndex, i - startIndex + 1);
      if(isPalindrome(substr)) {
        path.push(substr);
      } else {
        continue;
      }
      backtracking(s, i+1);
      path.pop();    
    }
  }
};

function isPalindrome(str) {
  let left = 0, right = str.length-1;
  while (left < right) {
    if (str[left] !== str[right]) {
      return false;
    }
    left++;
    right--;
  }
  return true;
}
```
