---
title: 🌴 Binary Tree
date: 2021-09-14 19:12:11
tags:
- binary tree
---
## How many kinds of binary tree are there?
- Perfect binary tree
  - Every node has either `0` or `2` child nodes.
![img](https://img-blog.csdnimg.cn/20200806185805576.png)
- Complete binary tree
  - every level, except possibly the last, is completely `filled`, and all nodes are as `far left` as possible.
![img](https://i.ibb.co/HCc5xxX/Screen-Shot-2021-09-14-at-7-15-51-PM.png)
- Binary search tree
  - `val(node.left) < val(node.right)`
  ![img](https://img-blog.csdnimg.cn/20200806190304693.png)
- Balanced binary tree
  - The difference of height between `left substreet` and `right subtree` differ by `no more than 1`.
  ![img](https://img-blog.csdnimg.cn/20200806190511967.png)

## Different traversal ways
![img](https://i.imgur.com/Lutiahp.png)
- `Pre order`: 5, 4, 1, 2, 6, 7, 8
- `In order`: 1, 4, 2, 5, 7, 6, 8
- `Post order`: 1, 2, 4, 7, 8, 6, 5

## How to define your own tree node?
```javascript
unction TreeNode(val, left, right) {
    this.val = (val===undefined ? 0 : val)
    this.left = (left===undefined ? null : left)
    this.right = (right===undefined ? null : right)
}
```