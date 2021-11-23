---
title: Leetcode 43 - Multiply strings
date: 2021-11-22 18:09:30
tags:
---
**`Note:`**
- `123` can be written as `100 + 20 + 3`, `456` can be written as `400 + 50 + 6`.
- Calculate `100*400, 100*50, ... 3*6`, and put them all in an array.
- To calculate `100*400`, just calculate `num1[0]*num2[0] + trailing 0s`.
- Make a helper function `addTwoString(n1, n2)`.

**`Question:`**

Given two non-negative integers `num1` and `num2` represented as strings, return the product of `num1` and `num2`, also represented as a string.

Note: You must not use any built-in BigInteger library or convert the inputs to integer directly.

**`Example:`**
```
Input: num1 = "123", num2 = "456"
Output: "56088"
```

**`Code:`**
```javascript
/**
 * @param {string} num1
 * @param {string} num2
 * @return {string}
 */
 var multiply = function(num1, num2) {
   if (num1 === '0' || num2 === '0') return '0';

  let num1Arr = [];
  let num2Arr = [];
  for (let i = 0; i < num1.length; i++) {
    num1[i] !== '0' && num1Arr.push(num1[i] + '0'.repeat(num1.length - i - 1));
  }
  for (let i = 0; i < num2.length; i++) {
    num2[i] !== '0' && num2Arr.push(num2[i] + '0'.repeat(num2.length - i - 1));
  }
  let products = [];
  for (let i = 0; i < num1Arr.length; i++) {
    for (let j = 0; j < num2Arr.length; j++) {
      const p = num1Arr[i][0] * num2Arr[j][0] + '0'.repeat(num1Arr[i].length - 1 + num2Arr[j].length - 1);
      products.push(p);
    }
  }
  while (products.length > 1) {
    const str1 = products.pop();
    const str2 = products.pop();
    products.push(addTwoString(str1, str2));
  }
  return products[0];

  function addTwoString(str1, str2) {
    const diff = str1.length - str2.length;
    if (diff < 0) [str1, str2] = [str2, str1];
    str2 = '0'.repeat(Math.abs(diff)) + str2;
    let res = '';
    let carry = 0;
    for (let i = str1.length - 1; i >= 0; i--) {
      const sum = (str1[i] - 0) + (str2[i] - 0) + carry;
      if (sum < 10) {
        res = sum + res;
        carry = 0;
      } else {
        res = (sum - 10) + res;
        carry = 1;
      }
    }
    if (carry === 1) res = 1 + res;
    return res;
  }
};

```