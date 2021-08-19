---
title: Leetcode 202 - Happy number
date: 2021-08-18 23:08:37
tags:
- leetcode
- number
---
**Note**: Learnt how to manipulate numbers. Like how to get the last digit with modulues operator `num % 10`

   and `(num - remainder) / 10`

   ```javascript
   var isHappy = function(n) {
       let map = [];
       map.push(n);
       while(true) {
         n = addAlldigitsSquared(n);
         if (n === 1) {
           break;
         }
         if (map.includes(n)) {
           return false;
         }
         map.push(n);
       }
     return true;
   };
   function addAlldigitsSquared(n) {
     let ans = 0;
     while(n) {
       ans += (n % 10)**2;
       n = (n - (n % 10)) / 10;
     }
     return ans;
   }
   ```

