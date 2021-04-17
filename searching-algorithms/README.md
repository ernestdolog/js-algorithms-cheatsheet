# Searching algorithms
## Binary search
> only on sorted array
halfs the array all over

#### how to:
 - take a sorted array
 - create 2 pointers (left - beginning of the array - and right - end of the array -)
 - loop only until left pointer has lower index than right
    - make a pointer in the middle
    - if value found return index
    - if value is small move left pointer up
    - if value is too large move right pointer down
 - if not found, return non found var, maybe -1
``` javacript 
function binarySearch(arr, searchVal){
  let leftPointer = 0;
  let rightPointer = arr.length - 1;
  while (leftPointer < rightPointer) {
      let midPointer = Math.floor((leftPointer + rightPointer)/2);
      if (arr[midPointer] === searchVal) return midPointer;
      if (arr[midPointer] < searchVal) {
          leftPointer = midPointer;
      }
      if (arr[midPointer] > searchVal) {
          rightPointer = midPointer;
      }
      continue;
  }
  return -1;
}
```
## Linear search
Loops linearly in one direction until it finds... basic for loop
## String search

#### pseudocode:

 - loop over the longer string
 - loop over the shorter string
 - if chars doesn't match break out from the inner loop
 - if chars match keep going
 - if you complete the inner loop and find a complete match increment the count of matches
 - return count at the end
 'abcdefgh'

first hand solution:
``` javacript
 function naiveSearch(long, short){
    var count = 0;
    for(var i = 0; i < long.length; i++){
        for(var j = 0; j < short.length; j++){
           if(short[j] !== long[i+j]) break;
           if(j === short.length - 1) count++;
        }
    }
    return count;
}
```
maybe a bit more effective:
``` javascript
function naiiveString (basicStr, searchStr) {
    const fullLength = basicStr.length;
    const searchLength = searchStr.length;
    let counter = 0;
    let idx = 0;
    while (idx < fullLength) {
        if (basicStr.slice(idx, idx + searchLength) === searchStr) {
            counter ++;
            idx = idx + searchLength;
        } else {
            idx ++;
        }
        continue;
    }
    return counter;
}
```
