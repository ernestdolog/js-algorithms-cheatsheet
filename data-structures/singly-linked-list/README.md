# Singly linked list
Ordered list of data, like an array. Difference from array: array data points are indexed.
Linked list nodes/elements aren't indexed. They just contain a pointer to the next element.

Contains a **head** (beginning of the list), **tail** (end of the list) and **length** property.

> Use case: When we have a really long list, where we care about insertion/deletion time and efficiency, and don't want random access to elements.

![Singly Linked list](https://github.com/ernestdolog/js-algorithms-cheatsheet/blob/main/assets/pics/singly_linked_list.png)

If we want the n-th node, we need to go through all nodes before it.

**Singly** linked list is single, because it has one way connections. One node is only connected to the next, and not the previous.

## Singly linked list node:

```javascript
class Node<T> {
    val: T;
    next: Node<T>

    constructor (val: T) {
        this.val = val;
        this.next = null;
    }
}
```
## Singly linked list class prototype:

```javascript
class SinglyLinkedList<T> {
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

## push method:
> adds to the end

- accept a value
- create a new node using that value
- if there is no head yet, set the freshly created node as tail and head
- otherwise set the next property on the tail to be the freshly created node
- than set the freshly created node as the tail

```javascript
    push (val: T): SinglyLinkedList<T> {
        const newNode = new Node(val);
        if (!this.head) {
            this.head = newNode;
            this.tail = this.head;
        } else {
            this.tail.next = newNode;
            this.tail = newNode;
        }
        this.length ++;
        return this;
    }
```

## pop method:
> removes from the end

- if there is no values in the list return undefined
- loop until you reach the tail (.next === null)
- set the .next prop on 2nd to last item to null
- decrement length by 1

```javascript
    pop (): Node<T> {
        // this is what we unlink
        let current = this.head;
        // this is what will be the new head (always has to be one before "current")
        let newTail = current;
        if (!current) return undefined;
        while (current.next) {
            newTail = current
            current = current.next;
        }
        this.tail = newTail;
        this.tail.next = null;
        this.length--;
        // if there was only one element, let's "clear the class"
        if(this.length === 0){
            this.head = null;
            this.tail = null;
        }
        return current;
    }
```

## shift method:
> removes the first (head)

- no nodes? -> return undefined
- store current head in a var
- set head to current head's next prop
- decrement length by 1
- remove old head

```javascript
    shift (): Node<T> {
        if (!this.head) return undefined
        let current = this.head;
        this.head = current.next;
        this.length --;
        // if there was only one element, let's "clear the class"
        if(this.length === 0){
            this.tail = null;
        }
        return current;
    }
```

## unshift method:
> adds to the beginning of the list

- function should accept a value
- create a new Node
- if there is no head, we set freshly created as tail and head
- otherwise set the newly created Node's next to the current head
- assign newly created Node to the head
- increment length by one
- return the linked list

```javascript
    unshift (val: T): SinglyLinkedList<T> {
        const newNode = new Node(val);
        if (!this.head) {
            this.head = newNode;
            this.tail = this.head;
        } else {
            newNode.next = this.head;
            this.head = newNode;
        }
        this.length ++;
        return this;
    }
```

## get method:
> returns the n-th item from the list

- function should accept an index (number)
- if index is outside (0, this.length - 1) stadium in any direction, return null
- loop through the list until you reach that index && return Node at that index

```javascript
    get (idx: number): Node<T> {
        if (idx < 0 || idx >= this.length) return null;
        let counter: number = 0;
        let current: Node<T> = this.head;
        while (counter !== idx) {
            current = current.next;
            counter ++;
        }
        return current;
    }
```

## set method:
> Changing the value of a Node in the list based on it's position.

- function should accept a value and an index
- use this.get to find that node
- if Node is not found, return false
- if Node is found change it's value and return true;

```javascript
    set (value: T, idx: number): boolean {
        const item: Node<T> = this.get(idx);
        if (!item) return false;
        item.val = value;
        return true;
    }
```

## insert method:
> Inserting a node at whatever index we specify.

How it looks by steps:

![Singly Linked list insert 1](https://github.com/ernestdolog/js-algorithms-cheatsheet/blob/main/assets/pics/singly_linked_list_inert_1.png)
![Singly Linked list insert 2](https://github.com/ernestdolog/js-algorithms-cheatsheet/blob/main/assets/pics/singly_linked_list_inert_2.png)
![Singly Linked list insert 3](https://github.com/ernestdolog/js-algorithms-cheatsheet/blob/main/assets/pics/singly_linked_list_inert_3.png)
![Singly Linked list insert 4](https://github.com/ernestdolog/js-algorithms-cheatsheet/blob/main/assets/pics/singly_linked_list_inert_4.png)

- function should accept a value and an index
- if index is outside (0, this.length) stadium in any direction, return false
- if index === this.length, just insert new Node to the end
- if index === 0, unshift a new Node to the beginning
- otherwise use this.get to access Node at index - 1
- set .next at that Node to be the newly created
- set .next at the newly created Node to be the .next of the previous's .next
- increment length
- return true

```javascript
    insert (value: T, idx: number): boolean {
        if (idx < 0 || idx > this.length) return false;

        // important to not to proceed on them... .length is modified in these functions!!!
        if (idx === this.length) return !!this.push(value);
        if (idx === 0) return !!this.unshift(value);

        const previousItem = this.get(idx - 1);
        const nextItem = previousItem.next;
        const newNode = new Node(value);
        previousItem.next = newNode;
        newNode.next = nextItem;
        this.length ++;
        return true;
    }
```

## remove method:
> Remove the Node at the n-th place.

- function should accept an idx
- if index is outside (0, this.length - 1) stadium in any direction, return undefined
- if idx === this.length - 1, this.pop
- if idx === 0, this.shift
- otherwise this.get(idx - 1), sent it's next value the .next of it's .next
- decrement length
- return .val of removed node

```javascript
    remove (idx: number): T {
        if (idx < 0 || idx >= this.length) return undefined;
        if (idx === this.length - 1) return this.pop();
        if (idx === 0) return this.shift();
        const previousNode = this.get(idx - 1);
        const currentNode = previous.next;
        previousNode.next = previous.next.next;
        this.length --;
        return currentNode.val;
    }
```

## reverse method:
> Changing the value of a Node in the list based on it's position.

![Singly Linked list rev](https://github.com/ernestdolog/js-algorithms-cheatsheet/blob/main/assets/pics/singly_linked_list_reverse.png)

- swap head and tail
- create a variable for **next**, **previous**, and **node**. **Node** is current head, **prev** is null, **next** is undefined.
- loop through the list
- **next** has to be the current .next
- **node**.next has to be previous (turn opposite the relation)
- increase **prev** and than **node**

> **prev** is null, because we are currently (**node**) on the tail, next has to be null

```javascript
    reverse (): SinglyLinkedList<T> {
      let node: Node<T> = this.head;
      this.head = this.tail;
      this.tail = node;

      let next: Node<T>;
      let prev: Node<T> = null;

      for(let i = 0; i < this.length; i++){
        next = node.next;
        node.next = prev;
        prev = node;
        node = next;
      }
      return this;
    }
```

> Visualgo: https://visualgo.net/en/list

