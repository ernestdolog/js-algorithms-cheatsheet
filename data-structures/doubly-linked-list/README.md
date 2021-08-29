# Doubly linked list
Ordered list of data, like an array. Difference from array: array data points are indexed.
Doubly linked list nodes/elements aren't indexed. They just contain a pointer to the next, and previous element.

Contains a **head** (beginning of the list), **tail** (end of the list) and **length** property.

![Doubly Linked list](https://visualgo.net/en/list?slide=1)

## Doubly linked list class prototype:

```javascript
class DoublyLinkedList<T> {
    head: Node<T>;
    tail: Node<T>;
    length: number;

    constructor () {
        this.head = null;
        this.tail = null;
        this.length = 0;
    }
}
```

## Singly linked list node:

```javascript
class Node<T> {
    val: T;
    next: Node<T>;
    prev: Node<T>

    constructor (val: T) {
        this.val = val;
        this.next = null;
        this.prev = null;
    }
}
```

## push method:
> adds to the end

- accept a value
- create a new node using that value
- if there is 0 length, set the freshly created node as tail and head
- otherwise set the next property on the tail to be the freshly created node
- than set the prev property on the freshly created node to be the tail
- than set the freshly created node as the tail

```javascript
    push (val: T): DoublyLinkedList<T> {
        const newNode = new Node(val);
        if (this.length === 0) {
            this.head = newNode;
            this.tail = this.head;
        } else {
            this.tail.next = newNode;
            newNode.prev = this.tail;
            this.tail = newNode;
        }
        this.length ++;
        return this;
    }
```

## pop method:
> removes from the end

- if `length` === 0, return undefined
- if `length` === 1, assign `null` to `head` and `tail`
- assign `null` to `tail`'s prev element's `next`
- set `tail`'s prev element as `tail`
- subtract one from `length`

```javascript
    pop (): Node<T> {
        if (this.length === 0) return undefined;
        const poppedNode = this.tail;
        if (this.length === 1) {
            this.head = null;
            this.tail = null;
        } else {
            this.tail = poppedNode.prev;
            this.tail.next = null;
            // because we return this node... shouldn;t be connected to anything
            poppedNode.prev = null;
        }
        this.length --;
        return poppedNode;
    }
```

## shift method:
> removes a node from the beginning

- if `length` === 0 / `!head`, return undefined
- if `length` === 1, assign `null` to `head` and `tail`
- assign `null` to `heads`'s next element's `prev`
- set `heads`'s next element as `head`
- subtract one from `length`

```javascript
    shift (): Node<T> {
        if (!this.head) return undefined;
        const shiftedNode = this.head;
        if (this.length === 1) {
            this.head = null;
            this.tail = null;
        } else {
            this.head = shiftedNode.next;
            this.head.prev = null;
            // because we return this node... shouldn;t be connected to anything
            shiftedNode.next = null;
        }
        this.length --;
        return shiftedNode;
    }
```

## unshift method:
> adding a node to the beginning

- create a new node
- if `length` === 0 / `!head`, `head` and `tail` equals to the new node
- set `head`'s prev to newly created, than newly created's next to `head`
- set newly created node as `head`
- `length` ++
- return list

```javascript
    unshift (val: T): DoublyLinkedList<T> {
        const newNode = new Node(val);
        if (!this.head) {
            this.head = newNode;
            this.tail = newNode;
        } else {
            const oldHead = this.head;
            oldHead.prev = newNode;
            newNode.next = oldHead;
            this.head = newNode;
        }
        this.length ++;
        return this;
    }
```

## get method:
> accessing a node by its position

- check for this: idx < 0, >= length and return null if true (empty list is also handled by this)
- if idx <= `length`/2:
    - from `head` loop through the middle
    - when found return
- else:
    - from `tail` loop through the middle
    - when found return

> O(n) (technically O(n/2))

```javascript
    get (idx: number): Node<T> {
        if (!idx || idx < 0 || idx >= this.length) return null;
        let counter, currentNode;
        if (idx <= this.length / 2) {
            counter = 0;
            currentNode = this.head;

            while (counter < idx) {
                currentNode = currentNode.next;
                counter ++;
            }

            return currentNode;
        } else {
            counter = this.length - 1;
            currentNode = this.tail;

            while (counter > idx) {
                currentNode = currentNode.prev;
                counter --;
            }

            return currentNode;
        }
    }
```

## set method:
> replace the value of a node based on it's index

- create a variable from the node this.get returned
- if not null, replace node's value, than return true
- if null return false

```javascript
    set (val: T, idx: number): boolean {
        const node = this.get(idx);
        if (!node) return false;
        node.val = val;
        return true;
    }
```

## insert method:
> create a new node, and adds it in the given index

> O(1)

- check for this: idx < 0, >= length and return false if they apply (empty list is also handled by this)
- if idx === 0, `unshift` the value
- if idx === length - 1, `push` the value
- use `get` to accessd the node at index - 1
- create new node
- wire the connections together
- increase `length` by 1
- return true

```javascript
    insert (val: T, idx: number): boolean {
        if (!idx || idx < 0 || idx >= this.length) return false;
        if (idx === 0) {
            this.unshift(val);
            return true;
        } else if (idx === this.length - 1) {
            this.push(val);
            return true;
        } else {
            const newNode = new Node(val);
            // this will return, same value check happens in this function too!!!
            const previousNode = this.get(idx);
            const nextNode = previousNode.next;
            previousNode.next = newNode;
            newNode.prev = previousNode;
            newNode.next = nextNode;
            nextNode.prev = previousNode;
            this.length ++;
            return true;
        }
    }
```

## remove method:
> remove node from certain index

> O(1)

- check for this: idx < 0, >= length and return null if they apply (empty list is also handled by this)
- if idx === 0, `shift` the idx
- if idx === length - 1, `pop` the idx
- use `get` to accessd the node at index
- wire the connections together
- unconnect deleted node from its `prev` and `next`
- decrease `length` by 1
- return deleted node

```javascript
    remove (idx: number): Node<T> {
        if (!idx || idx < 0 || idx >= this.length) return null;
        if (idx === 0) return this.shift(val);
        if (idx === this.length - 1) this.pop(val);

        const toDeleteNode = this.get(idx);
        const previousNode = toDeleteNode.prev;
        const nextNode = toDeleteNode.next;

        toDeleteNode.prev = null;
        toDeleteNode.next = null;

        previousNode.next = nextNode;
        nextNode.prev = previousNode;

        this.length --;

        return toDeleteNode;
    }
```