---
title: Leetcode 38 - Count and say
date: 2021-10-15 02:07:20
tags:
---
**`Note:`**
- The description of this question is quite confusing.
- Even it's a medium question, it's not that hard. Don't be terrified!

**`Question:`**

The count-and-say sequence is a sequence of digit strings defined by the recursive formula:

- countAndSay(1) = "1"
- countAndSay(n) is the way you would "say" the digit string from countAndSay(n-1), which is then converted into a different digit string.

To determine how you "say" a digit string, split it into the `minimal` number of groups so that each group is a contiguous section all of the `same character`. Then for each group, say the number of characters, then say the character. To convert the saying into a digit string, replace the counts with a number and concatenate every saying.

For example, the saying and conversion for digit string "`3322251`":
![img](https://assets.leetcode.com/uploads/2020/10/23/countandsay.jpg)
Given a positive integer n, return the nth term of the count-and-say sequence.

**`Example:`**
```
Input: n = 4
Output: "1211"
Explanation:
countAndSay(1) = "1"
countAndSay(2) = say "1" = one 1 = "11"
countAndSay(3) = say "11" = two 1's = "21"
countAndSay(4) = say "21" = one 2 + one 1 = "12" + "11" = "1211"
```

**`Code:`**
```javascript
/**
 * @param {number} n
 * @return {string}
 */
var countAndSay = function(n) {
  let memo = ['1'];
  for (let i = 1; i < n; i++) {
    const toRead = memo[memo.length - 1];
    memo.push(read(toRead));
  }
  return memo[memo.length - 1];
};

function read(str) {
  let count = 0;
  let result = '';
  for (let i = 0; i < str.length; i++) {
    if (str[i+1] && str[i+1] === str[i]) {
      count++;
    } else {
      count++;
      result += `${count}${str[i]}`;
      count = 0;
    }
  }
  return result;
}
```