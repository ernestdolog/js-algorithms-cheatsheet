# Stack
LIFO data structure.

Last element added to the stack will be the first one removed.
It is not an "own data type", it is more a set of a rules. We can use any kind of datatype achieving it.:
We need to manage that whatever is added last, removed first.

Add and remove is prioritized in this type.

> JS Call Stack is a Stack!

## Where is it used?

- managing function invocations
- undo/redo things
- routing (history object is like a stack)

## Simple example:

```javascript
const stack = [];

stack.push('one pony');

stack.push('two ponies');

stack.push('n*10^23 ponies');

stack.pop();

stack.pop();

stack.pop();

```

> until we make sure to only use `.push()` and `.pop()` on the array to add/remove values, it is a stack.

This is fine, but reindexing while `.push()`/`.pop()` is too heavy.
We need some data structure, where `.push()`/`.pop()` is constant time (O(1))! This will be `Doubly Linked List`.
BUT: Doubly Linked list is heavier than Singly Linked list. 
We could use Singly linked list's `.shift()`/`.unshift()` (O(1)) methods. They do remove/add to the first, but if we only use this 2, it is LIFO.
We will create a `Stack` class very similar to `Singly Linked List` with only `.shift()`/`.unshift()` functions.


## Stack class prototype:

```javascript
class Stack<T> {
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

## Stack node:

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

## push method:
> adds to the end

- accept a value
- create a new node using that value
- if there is 0 `size`, set the freshly created node as `first` and `last`
- otherwise store `first` prop in a variable
- assign newly created node to `first`
- set `first`'s next as the old `first`
- return new `size`

```javascript
    push (val: T): number {
        const newNode = new Node(val);
        if(this.size === 0){
            this.first = newNode;
            this.last = newNode;
        } else {
            const temp = this.first;
            this.first = newNode;
            this.first.next = temp;
        }
        return ++this.size;
    }
```

## pop method:
> removes from the end

- if no `first` element, return null
- save `first` in a temporary variable
- if `first` === `last`, remove `last` (later on we will remove the `first` too)
- assign the `first`'s next node to `first`
- decrease size by 1
- return deleted node's value

```javascript
    pop (): T {
        if(!this.first) return null;
        const temp = this.first;
        if(this.first === this.last){
            this.last = null;
        }
        this.first = this.first.next;
        this.size--;
        return temp.value;
    }
```