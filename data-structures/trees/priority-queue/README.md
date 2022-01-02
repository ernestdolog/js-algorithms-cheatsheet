# Priority Queue
Based on a Min Binary Heap.
Nodes have priority and sorted in a Binary Heap. Those with higher prio get out first.

**enqueue** method:
 - Takes value and prio.
 - Creates a new Node
 - places it into right spot based on its prio

**dequeue** method:
 - Remove Root element
 - Rearranges Heap based on priority

### Priority Queue parent class:
```javascript
class PriorityQueue<T> {
    values: Node<T>[];

    constructor () {
        this.values = [];
    }
}
```

```javascript
class Node<T> {
    val: T;
    priority: number;

    constructor (val: T, priority: number) {
        this.val = val;
        this.priority = priority;
    }
}
```

#### bubbleUp() function is a "reorganize" nodes function starting from last element
> This comes handy when we enqueue, so create a little chaos at the end of our structure
```javascript
private function bubbleUp(): PriorityQueue<T> {
    // start from last element, going upwards
    let idx = this.values.length - 1;
    // it can happen that we bubble up to idx 0... than just leave it
    while (idx > 0) {
        // index of the parent of "idx" element
        const parentIdx = Math.floor( (idx - 1) / 2 );
        // if parent's prio is bigger we are fine, leave it...
        if (this.values[parentIdx].priority >= this.values[idx].priority) break;
        // if not, swap with parent
        this.swap(idx, parentIdx);
        // reorganise our idx to the parent to do this loop again
        idx = parentIdx;
    }
    return this;
}
```

#### sinkDown() function is a "reorganize" nodes function starting from first element
> This comes handy when we dequeue, so create a little chaos in the beginning of our structure
```javascript
private function sinkDown(): PriorityQueue<T> {
    // starting from up
    let idx = 0;
    const length = this.values.length;
    // element which might be positioned wrong
    const element = this.values[idx];
    while(true){
        // children of top element
        let leftChildIdx = 2 * idx + 1;
        let rightChildIdx = 2 * idx + 2;
        let leftChild,rightChild;
        let swapIdx = null;
        // only if they actually do exist (no one guarantees n-th element has children - still can adopt!!! <3)
        if(leftChildIdx < length) {
            leftChild = this.values[leftChildIdx];
            if(leftChild.priority < element.priority) {
                    swapIdx = leftChildIdx;
            }
        }
        // we figure which of the left/right are smaller
        if(rightChildIdx < length) {
            rightChild = this.values[rightChildIdx];
            if(
                (swapIdx === null && rightChild.priority < element.priority) || 
                (swapIdx !== null && rightChild.priority < leftChild.priority)
            ) {
                swapIdx = rightChildIdx;
            }
        }
        // if no swap with children, positioning is already correct
        if(swapIdx === null) break;
        this.swap(idx, swapIdx);
        idx = swap;
    }
    return this;
}
```

```javascript
function enqueue (val: T, priority: number): Node<T> {
    const newNode = new Node(val, priority);
    this.values.push(newNode);
    this.bubbleUp();
    return newNode;
}
```

```javascript
function dequeue (val: T, priority: number): Node<T> {
    // preserve the node to be deleted (first one with highest prio)
    const deletedNode = this.values[0];
    // swap first and last nodes
    this.swap(0, this.values.length - 1);
    // delete new latest node
    this.values.pop();
    // "bubble up", reorganize nodes
    this.sinkDown();
    return deletedNode;
}
```
