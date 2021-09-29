---
title: Leetcode 105 - Construct binary tree from inorder and preorder  traversal
date: 2021-09-28 23:56:11
tags:
- binatry tree
---
**`Note:`**
- Much like what we did in `postorder`, the first element of `preorder` is the current root.
- Steps
  - Get the `root`
  - Split `inorder` array based on its value, then we have `leftSubtreeInorder` and `rightSubtreeInorder`.
  - Based on the length of them, we can get `leftSubtreePreorder` and `rightSubtreePreorder`.

Given two integer arrays preorder and inorder where preorder is the preorder traversal of a binary tree and inorder is the inorder traversal of the same tree, construct and return the binary tree.

**Example**

![img](https://assets.leetcode.com/uploads/2021/02/19/tree.jpg)
```
Input: preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
Output: [3,9,20,null,null,15,7]
```

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
 * @param {number[]} preorder
 * @param {number[]} inorder
 * @return {TreeNode}
 */
var buildTree = function(preorder, inorder) {
  return traverse(preorder, inorder);
  
  function traverse(preorderArr, inorderArr) {
    if (!preorderArr && !inorderArr) return null;
    
    const rootValue = preorderArr.shift();
    const root = new TreeNode(rootValue);
    if (preorderArr.length === 0) {
      return root;
    }
    
    const rootIndex = inorderArr.indexOf(rootValue);
    const leftInorder = inorderArr.slice(0, rootIndex);
    const rightInorder = inorderArr.slice(rootIndex + 1)
    const leftPreorder = preorderArr.slice(0, leftInorder.length);
    const rightPreorder = preorderArr.slice(leftInorder.length);
    root.left = traverse(leftPreorder, leftInorder);
    root.right = traverse(rightPreorder, rightInorder);
    return root;
  } 
};
```