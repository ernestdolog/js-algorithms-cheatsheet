# Hash Table
> This stuff is built in to most of programming languages.

**BIG O**: 
- insert: O(1)
- delete: O(1)
- retrieve: O(1)
> However it's not exactly reached with the dummy example functions :P
> It all comes down how fast, good and evenly distributing our hash function is.

What is it?
 - Stores key-values pairs.
 > Just like arrays! BUT:
 - Not strictly numeric.
 - Not ordered.
 - It's very fast adding/removing/finding values.
 > It is commonly used because its speed.

In JS we have **Object**-s and **Map**-s. 
> Object keys are strictly string, but it works with the same idea.

**Hash function**: In order to look up values by key, we need a way to convert keys into valid array indices.

Criteria for hash function:
 - We want it fast.
 - Doesn't cluster outputs at specific indices, but distributes uniformly.
 - Same input -> same output.
 - Maps any input into the same size.

#### Our first little hash function ^^:

```javascript
function hash(key, arrayLen) {
    let total = 0;
    // using random prime number in hashing
    // hepls to reduce collisions... there are huge researches in
    // this topic, i can only advise to dig in
    let RND_PRIME = 31;
    // we maximum go until 100
    // just to emphasise the fastness for each input
    const topChar = Math.min(key.length, 100);
    for (let i = 0; i < topChar; i ++) {
        let char = key[i];
        let value = char.charCodeAt(0) - 96
        total = (total * RND_PRIME + value) % arrayLen;
    }
    return total;
}
```

### Let's handle collisions!

> Collision means when you input 2 different stuff in a Hash function, what's results are the same.

#### 1. Separate Chaining
At each index in our array we are storing values using a more sophisticated data structure.

#### 2. Linear Probing
Whenever a collision happens we look up the next free spot in out array.
> This allows single key storage, what's not possible in *Separate Chaining*

### Hash Table class

```javascript
class HashTable<T> {
    keyMap: T[];

    constructor(size = 53){
        this.keyMap = new Array<T>(size);
    }
}
```

### set method
- inputs: key, value
- hash the key
- figure out where to store
- store the key-value in the hash table with Separate Chaining

```javascript
set(key: T, value: T): HashTable<T> {
    const index = this.hash(key);
    if(!this.keyMap[index])
        this.keyMap[index] = [];
    this.keyMap[index].push([key, value]);
    return this;
}
```

### get method
- inpus: key
- hash the key
- retrieve key-value pair in the array in the hash table
- if not found, returns undefined


```javascript
get(key: T): T {
    const index = this.hash(key);
    if (this.keyMap[index]) {
        for (const keyEntity of this.keyMap[index]) {
            if (keyEntity[0] === key)
                return keyEntity[1];
        }
    }
    return undefined;
}
```

### keys method
> Collects and returns all keys into one single array
- inpus: key
- hash the key
- retrieve key-value pair in the array in the hash table
- if not found, returns undefined


```javascript
keys(): T[] {
    let keys: T[] = [];
    for (const position of this.keyMap) {
        const positionKeys = position?.map(keyEnt => keyEnt[0]);
        keys = [...keys, ...positionKeys];
    }
    // only return unique keys
    return [...new Set(keys)];
}
```

### values method
> Collects and returns all values into one single array
**Dealing with duplicate data**: Most times we return unique keys and values. But up to implementation.
- inpus: key
- hash the key
- retrieve key-value pair in the array in the hash table
- if not found, returns undefined


```javascript
values(): T[] {
    let values: T[] = [];
    for (const position of this.keyMap) {
        const positionValues = position?.map(keyEnt => keyEnt[1]);
        values = [...values, ...positionValues];
    }
    // either we can return only unique too...
    return values;
}
```