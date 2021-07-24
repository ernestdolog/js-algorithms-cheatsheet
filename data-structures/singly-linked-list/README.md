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
    pop (): Node<T>  {
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

> Visualgo: https://visualgo.net/en/list