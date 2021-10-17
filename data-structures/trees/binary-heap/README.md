# Binary Heap
A Binary Heap is very similar to a Binary Tree. Difference is:
- **MaxBinaryHeap**: Parent node is always bigger than the child nodes.
- **MinBinaryHeap**: Parent node is always smaller than the child nodes.

> There is no order. Only thing is: child is smaller/bigger than it's parent. Breadth level relation doesn't matter either.

 - every parent has maximum two children nodes
 - value of every parent node is always bigger than its children nodes
 - nn a MaxBinaryHeap the parent is bigger than the children, but there are no guarantees between sibling nodes.
 - Binary Heap is as compact as possible. All the children of each node are as full as they can be and left children are filled out first. So no depressing one sided heap as it's f ex possible in Search Trees.
 - in case of adding we start with left child always


How to store a Biunary Heap?:

![Binary Heap](https://github.com/ernestdolog/js-algorithms-cheatsheet/blob/main/assets/pics/binary_heap_storage.png)

**How to retrieve childs from parent**: For any `n` idx in the array, `left child`: 2n + 1, `right child`: 2n + 2.
**How to retrieve parent from any child**: For any `n` idx in the array, `parent`: Math.floor( (n - 1) / 2 ).

#### Let's model Binary Heap with only Max Binary Heap. Min Binary Heap is the very same just different direction. :)

### Max Binary Heap parent class:
```javascript
class BinaryHeap<T> {
    values: []<T>;

    constructor () {
        this.values = [];
    }
}
```

> No Node class here. We use an array (indexed values), and add/retreive parents/childs from the index.

### Insert

 - add to the end
 - "bubble it up": we swap it until it finds it final correct place
> By this **swap** I mean adding to the end, getting it's parent (from idx), and see if it's smaller/greater. In case of incorrect positioning, we swap. (f ex: 55 is added to the end, parent position has 33. We compare them, and in this case, swap.) Than again we look for next level parent. If incorrect placement, we swap... and so on till we reach the "root".