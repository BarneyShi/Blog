---
title: Leetcode 114 - Flatten binary tree to linked list
date: 2021-11-25 23:07:15
tags:
- dfs
- binary tree
---
**`Note:`**
- Use `recursion` with O(1) extra space.
- Flatten `left` subtree first.
- Let `root.right = left`.
- Use `tmp` to get the last node of flattened `left`.
- Let `tmp.next = right`. 

**`Question:`**

Given the `root` of a binary tree, flatten the tree into a "linked list":

- The "linked list" should use the same `TreeNode` class where the `right` child pointer points to the next node in the list and the `left` child pointer is always `null`.
- The "linked list" should be in the same order as a` pre-order` traversal of the binary tree.

**`Example:`**

![img](https://assets.leetcode.com/uploads/2021/01/14/flaten.jpg)
```
Input: root = [1,2,5,3,4,null,6]
Output: [1,null,2,null,3,null,4,null,5,null,6]
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
 * @return {void} Do not return anything, modify root in-place instead.
 */
var flatten = function(root) {
   if (!root) return null;
   let left = flatten(root.left);
   let right = flatten(root.right);

   let tmp = left;
   while (tmp && tmp.right) {
     tmp = tmp.right;
   }
   
  tmp && (tmp.right = right);
  left && (root.right = left);
  root.left = null;
   return root;
};
```