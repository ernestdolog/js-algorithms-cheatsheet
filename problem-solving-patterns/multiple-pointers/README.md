# Multiple pointers
Creating pointers or values which correspond to an index/position of an array
and move towards the end/middle/beginning based on a condition

> very good to solve problems with minimal space complexity:
> 1. there is a linear structure (array, list, string, ...)
> 2. we are looking for a pair of values what meet some condition

## examplez:
#### 1. Write a function called 'sumZero' which accepts a sorted array of integers. The function should find the first pair of values where the sum is 0. Return an array which continues only the desired pair of integers, or undefined, if there is no such pair

first hand solution:
``` javascript
function sumZero(arr){
    for(let i = 0; i < arr.length; i++){
        for(let j = i+1; j < arr.length; j++){
            if(arr[i] + arr[j] === 0){
                return [arr[i], arr[j]];
            }
        }
    }
}
```
``` javascript
sumZero([-4,-3,-2,-1,0,1,2,5])
```
really cool solution:
``` javascript
function sumZero(arr) {
    let left = 0;
    let right = arr.length - 1;

    while (left < right) {
        let sum = arr[left] + arr[right];
        if (sum === 0) {
            return [arr[left], arr[right]];
        } else if (sum > 0) {
            right --;
        } else {
            left ++;
        }
    }
}
```
#### 2. Implement a function called 'countUniqueValues' which accepts a sorted array, and counts the unique values in the array. There can be also negative values in the array, but it will be always sorted.

good solution:
``` javascript
function countUniqueValues(arr){
    if (!arr || arr.length < 1) return 0;
    let i = 0;
    let j = 1;
 
    while (j < arr.length + 1) {
        if (arr[i] != arr[j]) {
            i ++;
            arr[i] = arr[j];
        }
        j ++;
    }
  return i;
}
```
good solution:
``` javascript
function countUniqueValues(arr){
    if(arr.length === 0) return 0;
    var i = 0;
    for(var j = 1; j < arr.length; j++){
        if(arr[i] !== arr[j]){
            i++;
            arr[i] = arr[j]
        }
    }
    return i + 1;
}
```
``` javascript
countUniqueValues([1,2,2,5,7,7,99])
```