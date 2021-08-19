---
title: Leetcode 94 - Binary tree inorder traversal
date: 2021-08-18 23:05:20
tags:
- leetcode
- tree
---
**Note:** Inorder traversal is to traverse in `left node right` order. Just **TRUST the natural recursion** and don't think about it too much.

   ```javascript
   var inorderTraversal = function(root) {
     let arr = [];
     if(!root) {
       return arr;
     }
     function inorder(node) {
       node.left && inorder(node.left);
       arr.push(node.val);
       node.right && inorder(node.right);
     }
     inorder(root);
     return arr;
   };
   ```