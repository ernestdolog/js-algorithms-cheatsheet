# InOrder Depth-first Tree Traversal
Visit the entire left side, traverse the entire left side. Than the right.

> To reach: loop down-down-down leftwards, save, than check the right.

Basically "just change the order" of PostOrder code.
difference is in the helper function... first we call helper fuction in it, than save the val, than we call it on the right

 - create a queue to store values from the visited Nodes
 - write a helper function that accepts a node (here the recursive funny-fun starts ^^)
  - if the node has `left`/ prop, call the helper function in that node
  - push the val of the node to the queue storing visited values
  - if the node has `left`/ prop, call the helper function in that node
 - invoke helper function with the root
 - return the queue with collected values

``` javascript
function postOrderDepthFirst <T> (tree: Tree): Queue<T> {
    if (!tree?.root) return;
    const values = new Queue();
    function traverse (node: Node) {
        if (node.left) traverse (node.left);
        values.push(node.val);
        if (node.right) traverse (node.right);
    }
    traverse (tree.root);
    return values;
}
```