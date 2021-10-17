# Depth-first Tree Traversal
Going from one end to the other. 

> **When to use?**: A tree more wide than deep. (By space complexity / this case it takes less space than breadth-first would)

There are 3 ways:
 - PreOrder: Starting from the root working down reaching the depth of the Tree.
 - PostOrder
 - InOrder

> Generally they are not really more/less effective one an other. No huge difference. Very specific cases might need one of these.

> There is tho difference in the "nature" of data we get back. I elaborate on it in the specific traversals. :)

> Here we are doing some recursion. Very interesting, eye opener stuff!

> From recursive solutions we study from the power and real usage of recursion. It is a kind of a loop. Loops are really great for looping sequentially front of backwards. But when we have a tree-like branched pattern where we want to loop, looping is not enough. Here comes recursion in the picture. This fills the hole,and offers us unlimited opportunity to loop basically in any kind of parth through each steps. Amazing stuff, isn't it? :) :) :)