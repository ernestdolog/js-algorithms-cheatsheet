# PostOrder Depth-first Tree Traversal
Going from the depth up. -> We only mark a node visited, as all of it's children are visited.

Basically "just change the order" of PreOrder code.
difference is in the helperfiunction... stuff happens the opposite way

> **When to use?**: When you would like to clone or store a Tree, and than recreate it from that structure. As this traversal will give you the Node val's in order from root, than it's left, than that's left and the right.

 - create a queue to store values from the visited Nodes
 - write a helper function that accepts a node (here the recursive funny-fun starts ^^)
  - if the node has `left`/`right` prop, call the helper function in that node
  - push the val of the node to the queue storing visited values
 - invoke helper function with the root
 - return the queue with collected values

``` javascript
function postOrderDepthFirst <T> (tree: Tree): Queue<T> {
    if (!tree?.root) return;
    const values = new Queue();
    function traverse (node: Node) {
        if (node.left) traverse (node.left);
        if (node.right) traverse (node.right);
        values.push(node.val);
    }
    traverse (tree.root);
    return values;
}
```