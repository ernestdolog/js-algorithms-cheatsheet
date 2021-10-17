# PreOrder Depth-first Tree Traversal
Going from the root to the depth.

Recursive thingy. :)

> **When to use?**: When you would like to clone or store a Tree, and than recreate it from that structure. As this traversal will give you the Node val's in order from root, than it's left, than that's left and the right.

 - create a queue to store values from the visited Nodes
 - create a variable called `node` to store current Node... assign `root` to it
 - write a helper function that accepts a node (here the recursive funny-fun starts ^^)
  - push the val of the node to the queue storing visited values
  - if the node has `left`/`right` prop, call the helper function in that node
 - invoke helper function with the root
 - return the queue with collected values

``` javascript
function preOrderDepthFirst <T> (tree: Tree): Queue<T> {
    if (!tree.root) return;
    const values = new Queue();
    function traverse (i: Node<T>) {
        values.push(i.val);
        if (i.left) traverse (i.left);
        if (i.right) traverse (i.right);
    }
    traverse (tree.root);
    return values;
}
```