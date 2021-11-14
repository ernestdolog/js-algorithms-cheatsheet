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

### private Swap

```javascript
private function swap (idx1: number, idx2: number): void {
    [this.values[idx1], this.values[idx2]] = [this.values[idx2], this.values[idx1];
}
```

### Insert

 - add to the end
 - "bubble it up": we swap it until it finds it final correct place 
> By this **swap** I mean adding to the end, getting it's parent (from idx), and see if it's smaller/greater. In case of incorrect positioning, we swap (with its parent). (f ex: 55 is added to the end, parent position has 33. We compare them, and in this case, swap.) Than again we look for next level parent. If incorrect placement, we swap... and so on till we reach the "root".

```javascript
function insert(val: T): BinaryHeap<T> {
    this.values.push(val);
    let idx = this.values.length - 1;
    // it can happen that we bubble up to idx 0... than just leave it
    while (idx > 0) {
        // index of the parent
        const parentIdx = Math.floor( (idx - 1) / 2 );
        // if parent is bigger we are fine, leave it...
        if (this.values[parentIdx] >= val) break;
        // if not, swap with parent
        this.swap(idx, parentIdx);
        // reorganise our idx
        idx = parentIdx;
    }
    return this;
}
```

### ExtractMax

> In priority heaps this will come handy... as we need to extract first an item with bigger prio.

 - swap first and last items of array
 - remove last
 - get children of new first item
 loop (we always remember the new first item as we bubble it down, and loop in it)
    - if both are smaller than it, leave it, we are good
    - swap first item with the biggest child

```javascript
function extractMax(): BinaryHeap<T> {
    this.swap(this.values.length, 0);
    this.pop();

    let elemIdx = 0;
    while (elemIdx < this.values.length) {
        const leftIdx = 2 * elemIdx + 1;
        const rightIdx = 2 * elemIdx + 2;
        if (this.values[leftIdx] <= this.values[elemIdx] 
            && this.values[rightIdx] <= this.values[elemIdx]) break;
        const swapIdx = Math.max(leftIdx, rightIdx);
        this.swap(elemIdx, swapIdx);
        elemIdx = swapIdx;
    }

    return this;
}
```