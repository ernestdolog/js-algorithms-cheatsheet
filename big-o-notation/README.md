# Big O notation
**Big O notation** is the number of operations happening in the code.

> We always simplify it:
> O(2n+5) => O(n)
> O(500) => O(1)
> O(2n^2+5n) => O(n^2)
> O(2n^3+5n^2) => O(n^3)

### Space complexity:

**auxiliary space complexity** is the space taken up by the algorithm without the inputs.

 - most primitives are constant space
 - strings require O(n) space
 - reference types require O(n) space - 'n' is length

 > Whole idea here is that you check what's in the input, and totally disregard it through the whole algorythm. 
 Everything else counts in.

 ### Big O of JS **Object** class:
  - insertion: O(1)
  - remove: O(1)
  - search: O(n) - meaning to check a given value if it's contained by some prop
  - access: O(1)
  - Object.keys: O(n)
  - Object.values: O(n)
  - Object.entries: O(n)
  - hasOwnProperty: O(1)

 ### Big O of JS Array (ordered list):
 > array operations are slow, when we are modifying all the indexes (add to the beginning, concating, sliceing)
accessing data is generally very fast
- access: O(1)
- search: O(n)
- adding to the end: O(1) push/pop
- adding to the beginning: O(n) shit/unshift
- concat: O(n)
- slice: O(n)
- splice: O(n)
- forEach/map/reduce/filter: O(n)
- sort: O(n * log(n))


## Examplez:


#### 1. add up numbers till 'n' O(n)

``` javascript 
function addUpTo(n) {
  let total = 0;
  for (let i = 1; i <= n; i++) {
    total += i;
  }
  return total;
}
```
``` javascript 
var t1 = performance.now();
addUpTo(1000000000);
var t2 = performance.now();
console.log(`Time Elapsed: ${(t2 - t1) / 1000} seconds.`)
```
#### 2. add up to with algorithm O(1)
``` javascript 
function addUpTo(n) {
  return n * (n + 1) / 2;
}
```
``` javascript 
var time1 = performance.now();
addUpTo(1000000000);
var time2 = performance.now();
console.log(`Time Elapsed: ${(time2 - time1) / 1000} seconds.`)
```
#### 3. print all pairs of numbers O(n^2)
``` javascript 
function printAllPairs (n) {
    for (var i = 0; i < n; i++) {
        for (var j = 0; j < n; j++) {
            console.log(i, j);
        }
    }
}
```