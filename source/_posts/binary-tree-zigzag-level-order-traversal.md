---
title: Leetcode 103 - Binary tree zigzag level order traversal
date: 2021-10-16 23:28:46
tags:
- binary tree
---
**`Note:`**
- Use `queue` for level order traversal.
- For `even` level, iterate from `right` to `left`. And add their `right` children first, then `left` children.

Given the `root` of a binary tree, return the zigzag level order traversal of its nodes' values. (i.e., from left to right, then right to left for the next level and alternate between).

**`Question:`**


**`Example:`**

![img](https://assets.leetcode.com/uploads/2021/02/19/tree1.jpg)
```
Input: root = [3,9,20,null,null,15,7]
Output: [[3],[20,9],[15,7]]
```

**`Code:`**
```javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number[][]}
 */
var zigzagLevelOrder = function (root) {
  if (!root) return [];
  let result = [];
  traverse(root);
  return result;

  function traverse(node) {
    let queue = [node];
    let level = 0;

    while (queue.length > 0) {
      const length = queue.length;
      let levelTraversal = [];
      let tmp = [];
      for (let i = 0; i < length; i++) {
        let node;
        if (level % 2 === 0) {
          node = queue.shift();
          levelTraversal.push(node.val);
          node.left && queue.push(node.left);
          node.right && queue.push(node.right);
        } else {
          node = queue[length - i - 1];
          queue.splice(length - i - 1, 1);
          levelTraversal.push(node.val);
          node.right && tmp.push(node.right);
          node.left && tmp.push(node.left);
        }
      }
      if (tmp.length > 0) {
        tmp.reverse();
        queue.push(...tmp);
      }
      level++;
      result.push(levelTraversal);
    }
  }
};
```