# Binary Search Tree
One node can have maximum 2 children

Nodes are sorted in a particular way, that it makes search very effective.

It is a "search tree" as data is sorted, this makes it different from simple binary trees.

Every node left to the parent is less than the parent, and every node right to the parent is greater than the parent.

Binary Search Tree parent class:

```javascript
class BinarySearchTree<T> {
    root: Node<T>;

    constructor () {
        this.root = null;
    }
}
```

Binary Search Tree Node class:

```javascript
class Node<T> {
    value: T;
    left: Node<T>;
    right: Node<T>;

    constructor (value) {
        this.value = value;
        this.left = null;
        this.right = null;
    }
}
```

insert function:

(can be solved iteratively and recursively)
- create new `Node`
- if no `root`, new `Node` will be `root`
- if there is a `root`, check if value is smaller or greater
    - greater?:
        - check if there is `Node` to the `right`
        - if there is, repeat previous steps
        - if not, add `Node` as new `right` property
    - smaller?:
        - check if there is `Node` to the `left`
        - if there is, repeat previous steps
        - if not, add `Node` as new `left` property

```javascript
function insert(val: T) {

}
```