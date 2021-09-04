---
title: Leetcode - 1D knapsack optimization
date: 2021-09-04 02:56:13
tags:
-leetcode
- dp
---
We can optimize what we got from using a 2D array.
In `DP[i][j] = max(DP[i-1][j], DP[i-1][j-weight[i] + value[i])`, we can see the state of `DP[i]` is only related to `DP[i-1]`. Somehow, we can use a 1D array to get what we want: 
`DP[j] = max(DP[j - weight(i)] + value[i])`.

**Note:**
1. We have to iterate `item` first then `bag`.
2. We have to iterate `bag` from the `end` to the `start`.

```javascript
function 1DKnapsack(weight, value, bagWeight) {
  let dp = [...Array(weight.length + 1).fill(0)];

  for (let i = 0; i < weight.length; i++) {
    for (let j = bagWeight; j >=weight[i]; j-- ) {
      dp[j] = Math.max(dp[j], dp[j - weight[i]] + value[i]);
    }
  }

  return dp[bagWeight];
}
```
