---
title: Leetcode 42 - Trapping rain water
date: 2021-11-03 02:42:08
tags:
- priority queue
---
**`Note:`**
- Just like `trapping rain water ii`, use `min-heap` priority queue `[position, height]`.
- This time, we don't start with the outermost, instead we start from both ends.
- Popping PQ based on the height.
- Use `visited` to mark visited bars.

**`Question:`**

Given `n` non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it can trap after raining

**`Example:`**

![img](https://assets.leetcode.com/uploads/2018/10/22/rainwatertrap.png)
```
Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
Explanation: The above elevation map (black section) is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped.
```

**`Code:`**
```java
class Solution {
    public int trap(int[] height) {
      int length = height.length;
      boolean[] visited = new boolean[length];
      // Mark both ends as visited so we won't iterate them again.
      visited[0] = visited[length - 1] = true;
      PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> a[1] - b[1]);
      pq.offer(new int[]{0, height[0]});
      pq.offer(new int[]{length - 1, height[length - 1]});

      int res = 0;
      int[] dirs = {-1, 1};
      while (!pq.isEmpty()) {
        int[] poll = pq.poll();
        for (int dir : dirs) {
          int pos = poll[0] + dir;
          if (pos >= 0 && pos < length && !visited[pos]) {
            if (height[pos] < poll[1]) {
              res += poll[1] - height[pos];
            }
            pq.offer(new int[]{pos, Math.max(height[pos], poll[1])});
            visited[pos] = true;
          }
        }
      }
      return res;
    }
}
```