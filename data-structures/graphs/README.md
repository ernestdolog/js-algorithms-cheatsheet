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