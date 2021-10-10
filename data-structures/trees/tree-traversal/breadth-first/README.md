# Breadth-first Tree Traversal
Going through each stages "horizontally" of a tree.

### How to:
 - create a queue to store values of visited nodes
 - place `root` node to the queue
 - loop as long as there is something in the queue:
  - dequeue a node from the queue, and push it's value to the variable containing those values
  - if there is a left/right val at the dequeued, add it to the queue
 - return the va storing our values

``` javascript
function breadthFirst <T> (tree: Tree): Queue<T> {
    let node = tree.root;
    if (!node) return;
    const operational = new Queue();
    const values = new Queue();
    operational.push(node);
    while (operational.size) {
        node = operational.shift();
        values.push(node.val);
        if (node.left) operational.push(node.left);
        if (node.right) operational.push(node.right);
    }
    return values;
}
```