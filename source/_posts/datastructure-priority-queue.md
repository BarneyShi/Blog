---
title: Data structure - 🆎 Heap (ft. Priority Queue)
date: 2021-11-28 16:22:09
tags:
- heap
- priority queue
---
Heap is actually `an array` physically, but logically it's a tree-based data structure. 
We often use `MinPriorityQueue` and `MaxPriorityQueue` in JavaScript.

![img](https://i.imgur.com/o9lSXNa.png)

```
Background knowledge:
  ParentIndex = (i - 1) >> 1;
  LeftChildIndex = 2*i + 1;
  RightChildIndex = 2*i + 2;

  Proof:
    Assume node with index `i` is on (n-1)th level, and there are `x` nodes `before` it on n-th level.
    Then, we can say `totalNodesBeforei = 2^(n - 1) - 1 + x = i`.
    On nth level, before its left, there will be `2x` node.
    `totalNodesBeforeJ = 2^n - 1 + 2x = 2*(2^(n-1) - 1 + x) + 1` = 2*i + 1. 
```

**`MinHeap implementation`**
```javascript
class MinHeap {
  constructor() {
    this.heap = [];
  }

  swap(i, j) {
    [this.heap[i], this.heap[j]] = [this.heap[j], this.heap[i]];
  }
  
  /**
   * @param {*} i
   * @return {*}
   */
  getParentIndex (i) {
    return (i - 1) >> 1;
  }

  /**
   * @param {*} i
   * @return {*}
   */
  getLeftIndex(i) {
    return i * 2 + 1;
  }
  
  /**
   * @param {*} i
   * @return {*}
   */
  getRightIndex(i) {
    return i * 2 + 2;
  }

  shiftUp(i) {
    if (i === 0) return;
    const parentIndex = this.getParentIndex(i);
    if (this.heap[i] < this.heap[parentIndex]) {
      this.swap(i, parentIndex);
      this.shiftUp(parentIndex);
    }
  }

  /**
   * @param {*} index
   */
  shiftDown(i) {
    const leftIndex = this.getLeftIndex(i);
    const rightIndex = this.getRightIndex(i);
    if (leftIndex < this.heap.length && this.heap[leftIndex] < this.heap[i]) {
      this.swap(leftIndex, i);
      this.shiftDown(leftIndex);
    }
    if (rightIndex < this.heap.length && this.heap[rightIndex] < this.heap[i]) {
      this.swap(rightIndex, i);
      this.shiftDown(rightIndex);
    }
  }

  /**
   * @param {*} value
   */
  insert(val) {
    this.heap.push(val);
    this.shiftUp(this.heap.length - 1);
  }

  pop() {
    const first = this.heap[0];
    const last = this.heap.pop();
    if (this.heap.length !== 0) {
      this.heap[0] = last;
      this.shiftDown(0);
    }
    return first;
  }

  peek() {
    return this.heap[0];
  }

  size() {
    return this.heap.length;
  }
}
```


**`Time complexity`**

![img](https://i.imgur.com/EwGEWof.png)




Code example : minHeap:
```javascript
let queue = new MinPriorityQueue({priority: (obj) => obj.val});
queue.enqueue({x, y, val});

let obj = queue.dequeue();
//The structure of obj is like {priority : p, element : {x, y, val}};
let {x, y, val} = obj;

queue.enqueue({x, y, val});
```