---
title: Data structure - 🆎 Priority Queue
date: 2021-11-28 16:22:09
tags:
- heap
---
Heap is a tree-based data structure. Generally, we use `MinPriorityQueue` and `MaxPriorityQueue` in JavaScript.

![img](https://upload.wikimedia.org/wikipedia/commons/thumb/3/38/Max-Heap.svg/800px-Max-Heap.svg.png)

**`Time complexity`**

![img](https://i.imgur.com/EwGEWof.png)

Take minHeap for example:
```javascript
let queue = new MinPriorityQueue({priority: (obj) => obj.val});
queue.enqueue({x, y, val});

let obj = queue.dequeue();
//The structure of obj is like {priority : p, element : {x, y, val}};
let {x, y, val} = obj;

queue.enqueue({x, y, val});
```