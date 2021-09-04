# Queue
FIFO data structure.

First element added to the stack will be the first one removed.
It is not an "own data type", it is more a set of a rules. We can use any kind of datatype achieving it.:
We need to manage that whatever is added first, removed first.

`add` and `remove` is prioritized in this type.
We need to `add` to the end, and `remove` from the beginning with minimal space/time complexity.

In case of arrays `.push()` and `.unshift()` would do it.
(we can of course think in a reversed array, and do the same with `.pop()` and `.shift()`)

smallest space/time complexity for this would be using of Singly Linked List:
 - shift / remove from the beginning
 - push / add to the end


 ## Queue class prototype:

```javascript
class Queue<T> {
    first: Node<T>;
    last: Node<T>;
    size: number;

    constructor () {
        this.first = null;
        this.last = null;
        this.size = 0;
    }
}
```

## Queue node:

```javascript
class Node<T> {
    val: T;
    next: Node<T>;

    constructor (val: T) {
        this.val = val;
        this.next = null;
    }
}
```

## enqueue method:
> adds to the end

- accept a value
- create a new node using that value
- if there is no `first` yet, set the freshly created node as `first` and `last`
- otherwise set the `next` property on the `last` to be the freshly created node
- than set the freshly created node as the `last`
- return the `size` of the queue

```javascript
    enqueue (val: T): number {
        const newNode = new Node(val);
        if (!this.first) {
            this.first = newNode;
            this.last = this.head;
        } else {
            this.last.next = newNode;
            this.last = newNode;
        }
        return this.size ++;
    }
```

## dequeue method:
> removes the first

- no nodes? -> return null
- store current head in a variable
- set `first` to current `first`'s `next` prop
- decrement `size` by 1
- remove old `first`
- return removed node's `val`

```javascript
    dequeue (): Node<T> {
        if (!this.first) return null;
        const current = this.first;
        this.first = current.next;
        this.size --;
        // if there was only one element, let's "clear the class"
        if(this.length === 0){
            this.last = null;
        }
        return current.val;
    }
```