---
title: Leetcode 207 - Course schedule
date: 2021-10-23 04:04:18
tags:
- topological sort
- dfs
---
**`Note:`**
- **`DFS`**
  - //TODO

There are a total of `numCourses` courses you have to take, labeled from 0 to numCourses - 1. You are given an array prerequisites where `prerequisites[i] = [ai, bi]` indicates that you must take course bi first if you want to take course ai.

- For example, the pair `[0, 1]`, indicates that to take course 0 you have to first take course 1.
Return `true` if you can finish all courses. Otherwise, return `false`.

**`Question:`**


**`Example:`**
```
Input: numCourses = 2, prerequisites = [[1,0]]
Output: true
Explanation: There are a total of 2 courses to take. 
To take course 1 you should have finished course 0. So it is possible.
```

**`Code:`**
```javascript
/**
 * @param {number} numCourses
 * @param {number[][]} prerequisites
 * @return {boolean}
 */
var canFinish = function (numCourses, prerequisites) {
  let preMap = new Map();
  let visited = new Set();
  for (const [course, pre] of prerequisites) {
    if (!preMap.has(course)) {
      preMap.set(course, [pre]);
    } else {
      preMap.set(course, [...preMap.get(course), pre]);
    }
  }

  for (let course of Array.from(Array(numCourses).keys())) {
    if (!dfs(course)) return false;
  }
  return true;

  function dfs(course) {
    if (visited.has(course)) return false;
    if (!preMap.has(course) || preMap.get(course).length === 0) return true;
    visited.add(course);

    for (let pre of preMap.get(course)) {
      if (!dfs(pre)) return false;
    }
    visited.delete(course);
    preMap.set(course, []);
    return true;
  }

};
```