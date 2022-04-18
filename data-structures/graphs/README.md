# Graph
> Used to model relationships.

### Terminology:
 - **Vertex**: a Node
 - **Edge**: connection between two Nodes
 - **Weighted/Unweighted**: values assigned/non assigned to distances between vertices
 - **Directed/Undeirected**: directions assigned/non assigned to distances between vertices
 - **Adjacency Matrix**: boolean matrix with rows and columns of nodes, representing all edges
 - **Adjacency List**: array of nodes with array value of all other nodes with which they have connections to

**Adjacency Matrix** and **Adjacency List** are used to store a graph. **Adjacency Matrix** is a matrix growing V^2 times 
when adding a new node, so it is rather huge. Finding a given connection is tho easier in it. But because the big size let's prefer **Adjacency List** when storing a matrix.

Implementation:

### Graph class:
```javascript
class Graph<T>{
    adjacencyList: Record<T, T[]>;

    constructor() {
        this.adjacencyList = {};
    }
}
```

### Add vertex:
- accepts a name of a vertex (Node :) )
- adds a new key to adjacency list with the name of our vertex, gives it an empty array

```javascript
addVertex(vertex: T): T[] {
    if(!this.adjacencyList[vertex])
        this.adjacencyList[vertex] = [];
    return this.adjacencyList[vertex];
}
```

### Add edge:
> Draw a connection between 2 vertexes.

- needs to accept 2 keys of Vertexes
- find Vertex1 in the list, and push Verttex2 in the array
- find Vertex2 in the list, and push Verttex1 in the array
- find/create Vertex with `addVertex` function
> For now let's theorize we only work with primitive types.

```javascript
addEdge(vertex1Key: T, vertex2Key: T): Graph<T> {
    const vertex1Connections = this.addVertex(vertex1Key);
    const vertex2Connections = this.addVertex(vertex2Key);
    vertex1Connections.push(vertex2Key);
    vertex2Connections.push(vertex1Key);
    return this;
}
```

### Remove edge:

- needs to accept 2 keys of Vertexes
- find Vertex1 in the list, and remove Verttex2 from the array
- find Vertex2 in the list, and remove Verttex1 from the array
> For now let's theorize we only work with primitive types.

```javascript
removeEdge(vertex1Key: T, vertex2Key: T): Graph<T> {
    let vertex1Connections = this.adjacencyList[vertex1Key];
    const vertex2Connections = this.adjacencyList[vertex2Key];
    if (this.adjacencyList[vertex1Key]?.length > 0) {
        this.adjacencyList[vertex1Key] =
            this.adjacencyList[vertex1Key].filter(
                entry => entry !== vertex2Key
            );
    }
    if (this.adjacencyList[vertex2Key]?.length > 0) {
        this.adjacencyList[vertex2Key] =
            this.adjacencyList[vertex2Key].filter(
                entry => entry !== vertex1Key
            );
    }
    return this;
}
```

### Remove vertex:
> Remove all connections pointing to this vertex + remove vertex

- needs to accept 1 key of Vertex
- loop through all verticles, what our vertex has, and remove edge with those ones
- find Vertex, and delete it
> For now let's theorize we only work with primitive types.

```javascript
removeVertex(vertex: T): Graph<T> {
    while (this.adjacencyList[vertex]?.length) {
        const adjacentVertex =
            this.adjacencyList[vertex].pop();
        this.removeEdge(vertex, adjacentVertex);
    }
    delete this.adjacencyList[vertex]
    return this;
}
```

# Graph traversal:
> Welcome to the fleshy stuff! <3

Traversal: Visiting every single node in the Graph. 
But it can of course mean more practically: collecting all similar Nodes, visiting all neighbouring Nodes to a Node etc...

### Depth first traversal:

#### Pseudocode:

- function should accept a starting node
- create a list to store result (to be returned)
- create object to store visited vertices (start empty)
- create helper function which accepts a vertex
    - if vertex empty, return
    - should place the vertex into visited object and push it into return array
    - loop over each values of that vertex
    - if those haven't been visited, call helper in them recursively

```javascript
DFS(vertex: T): void {
    if vertex is empty
        return (base case);
    add vertex to results list
    mark vertex as visited
    for each vertex in our vertexes neighbour:
        if neighbour is not visited:
            call (recursive) DFS in neighbour
}
```

#### Là real code:

```javascript
depthFirstTraverse (start: T): T[] {
    const result: T[] = [];
    const visited: Record<T, boolean> = {};
    const adjacencyList = this.adjacencyList;

    (function dfs (vertex): void {
        if(!vertex) return null;
        visited[vertex] = true;
        result.push(vertex);
        adjacencyList[vertex].forEach(
            neighbor => {
                if(!visited[neighbor]){
                    return dfs(neighbor);
                }
            }
        );
    })(start);

    return result;
}
```

### Iterative traversal:

#### Pseudocode:

- function should accept a starting node
- create a Stack to help use keep track of visited Vertices (list/array)
- create a list to store end results (what we will return)
- create object to store visited vertices (start empty)
- add the starting Vertex to the Stack, and mark it visited
- while Stack has smth in it:
    - pop next vertex from the Stack
    - if Vertex hasn'tbeen visited yet
        - mark it as visited
        - add it to result list
        - push all of its neighbours to Stack

```javascript
DFS-Iterative(start: T): void {
    Let S be a stack!
    S.push(start);
    while S is not empty
        vertex = S.pop();
        if vertex is not labeled discovered
            visit vertex (add to result list)
            label vertex as discovered
            for each of vertex`'`s neighbours
                => neighbour do S.push(neighbour)
}
```

#### Là real code:

```javascript
depthFirstIterativeTraverse (start: T): T[] {
    const stack = [start];
    const result: T[] = [];
    const visited: Record<T, boolean> = {};
    let currentVertex: T;

    visited[start] = true;
    while(stack?.length){
        currentVertex = stack.pop();
        result.push(currentVertex);

        this.adjacencyList[currentVertex].forEach(
            neighbor => {
               if (!visited[neighbor]) {
                   visited[neighbor] = true;
                   stack.push(neighbor);
               } 
            }
        );
    }
    return result;
}
```

### Breadth first traversal:

#### Pseudocode:

- function should accept a starting vertex
- create a Queue (modeling purposes an array will do it!) and put starting Vertex into it
- create a list to store result (to be returned)
- create object to store visited vertices (start empty)
- mark the starting Vertex as visited
- while Queue has smth in it:
    - shift first Vertex from the Queue -> push it into result array (note that we don't touch visited object here)
    - loop over each values of that vertex
    - if those haven't been visited, push them into Queue and add them to visited object (here we are with the visited)

#### Là real code:

```javascript
breadthFirstTraverse (start: T): T[]{
    const queue: T[] = [start];
    const result: T[] = [];
    const visited: Record<T, boolean> = {};
    let currentVertex: T;
    visited[start] = true;

    while (queue.length){
        currentVertex = queue.shift();
        result.push(currentVertex);
           

        this.adjacencyList[currentVertex].forEach(
            neighbor => {
                if (!visited[neighbor]) {
                    visited[neighbor] = true;
                    queue.push(neighbor);
                }
            }
        );
    }
    return result;
}
```

## Weighted graph:
> Minimalistic example of ho to imagine the weight ordered to an Edge

```javascript
class WeightedGraph<T>{
    adjacencyList: Record<T, {node: T, weight: number}[]>;

    constructor() {
        this.adjacencyList = {};
    }

    addVertex(vertex): {node: T, weight: number}[] {
        if(!this.adjacencyList[vertex])
            this.adjacencyList[vertex] = [];
        return this.adjacencyList[vertex];
    }

    addEdge(vertex1: T,vertex2: T, weight: number): Record<T, {node: T, weight: number}[]>{
        this.adjacencyList[vertex1]
            .push({
                node:vertex2,
                weight,
            });
        this.adjacencyList[vertex2]
            .push({
                node:vertex1,
                weight,
            });
    }
}
```