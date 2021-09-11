---
title: Leetcode 93 - Restore ip address
date: 2021-09-11 16:23:17
tags:
- leetcode
- backtracking
---
**`Note:`**
- This is a backtracking problem, very similar to `palindrome partitioning`.
- Need to write a helper `isValidIP`
- Pay attention to the `termination condition` because `path.length === s.lenght` is not enough. We also need to check if `path.length === s.length`.

Given a string s containing only digits, return all possible valid IP addresses that can be obtained from s. You can return them in any order.

A valid IP address consists of exactly four integers, each integer is between 0 and 255, separated by single dots and cannot have leading zeros. For example, "0.1.2.201" and "192.168.1.1" are valid IP addresses and "0.011.255.245", "192.168.1.312" and "192.168@1.1" are invalid IP addresses. 

**Example**
```
Input: s = "25525511135"
Output: ["255.255.11.135","255.255.111.35"]

Input: s = "0000"
Output: ["0.0.0.0"]
```

```javascript
/**
 * @param {string} s
 * @return {string[]}
 */
var restoreIpAddresses = function(s) {
  let ans = [];
  let path = [];
  if (s.length > 12) return ans;
  backtracking(s, 0);
  return ans;
  
  function backtracking(s, startIndex) {
    let tmp = path.join('');
    if (path.length === 4 && tmp.length === s.length) {
      ans.push(path.join('.'));
      return;
    }
    
    for (let i = startIndex; i < s.length; i++) {
      let substr = s.substr(startIndex, i - startIndex + 1);
      if (isValidIP(substr)) {
        path.push(substr);
        backtracking(s, i + 1);
        path.pop();
      } else {
        continue;
      }
    }
  }
};

function isValidIP(str) {
  const num = parseInt(str);
  if (isNaN(num) || str.length !== num.toString().length || num < 0 || num > 255) {
    return false;
  } else {
    if (str.length === 1) {
      return true;
    } else {
      if (str[0] === '0') {
        return false;
      }
      return true;
    }
  }
}
```