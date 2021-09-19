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

### insert function:

O(log n) in best scenario of well distributed tree

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
 - return entire tree

#### iterative solution:
```javascript
function insert(val: T): BinarySearchTree<T> {
    const newNode = new Node(val);
    if (!this.root) {
        this.root = newNode;
        return this;
    }
    let currentNode = this.root;
    while (true) {
        // otherwise it's an infinite loop!!!
        if (newNode.val === currentNode.val) return this;
        if (newNode.val > currentNode.val) {
            if (!currentNode.right) {
                currentNode.right = newNode;
                return this;
            }
            currentNode = currentNode.right;
        } else {
            if (!currentNode.left) {
                currentNode.left = newNode;
                return this;
            }
            currentNode = currentNode.left;
        }
    }
    return this;
}
```

#### recursive solution
```javascript
function insert(val: T): BinarySearchTree<T> {
    if (!this.root) {
        this.root = new Node(val);
        return this;
    }
    const doInsert = (currentNode: Node) => {
        // otherwise it's an infinite loop!!!
        if (current.val === val) return this;
        if (val > currentNode.val) {
            if (!currentNode.right) {
                currentNode.right = new Node(val);
                return this;
            }
            doInsert(currentNode.right);
        } else {
            if (!currentNode.left) {
                currentNode.left = new Node(val);
                return this;
            }
            doInsert(currentNode.left);
        }
    }
    doInsert(this.root);
}
```

### get function:

O(log n) in best scenario

(can be solved iteratively and recursively)
- if no `root`, return smth falsey
- if there is a `root`, check `val`, if found, return
- check if value is smaller or greater than `val`
    - equal?: return `Node`
    - greater?:
        - check if there is `Node` to the `right`
        - if there is, repeat previous steps
        - if not, return smth falsey
    - smaller?:
        - check if there is `Node` to the `left`
        - if there is, repeat previous steps
        - if not, return smth falsey
 - return entire tree

If or as we return a boolean when found, not found, we can make a `contains` function.

#### iterative solutions:
```javascript
function get(val: T): Node<T> {
    if (!this.root) return undefined;
    let currentNode = this.root;
    while (true) {
        if (val === currentNode.val) return currentNode;
        if (val > currentNode.val) {
            if (!currentNode.right) return undefined;
            currentNode = currentNode.right;
        } else {
            if (!currentNode.left) return undefined;
            currentNode = currentNode.left;
        }
    }
    return this;
}
```

```javascript
function get (val: T): Node<T> {
        if(!this.root) return undefined;
        let currentNode = this.root, found = false;
        while(currentNode && !found){
            if(value < currentNode.value){
                currentNode = currentNode.left;
            } else if(value > currentNode.value){
                currentNode = currentNode.right;
            } else {
                found = true;
            }
        }
        if(!found) return undefined;
        return current;
    }
```

#### recursive solution
```javascript
function get(val: T): BinarySearchTree<T> {
    if (!this.root) return undefined;

    const doGet = (currentNode: Node) => {
        if (current.val === val) return currentNode;
        if (val > currentNode.val) {
            if (!currentNode.right) return undefined;
            doGet(currentNode.right);
        } else {
            if (!currentNode.left) return undefined;
            doGet(currentNode.left);
        }
    }

    doGet(this.root);
}
```
