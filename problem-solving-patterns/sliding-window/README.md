# Sliding windows
This pattern involves creating a window which can be either an array or 
number from one position to the other.
Depending on a certain condition, the window either increases or closes
(and a new window is created)

> comes handy when dealing with a subset of an array/string

## examplez:

#### 1. Write a function called maxSubArraySum which accepts an array of integers and a number called n. The function should calculate the maximum sum of n consecutive elements in the array. 

first hand solution:
``` javascript
function maxSubarraySum(arr, num) {
  if ( num > arr.length){
    return null;
  }
  var max = -Infinity;
  for (let i = 0; i < arr.length - num + 1; i ++){
    temp = 0;
    for (let j = 0; j < num; j++){
      temp += arr[i + j];
    }
    if (temp > max) {
      max = temp;
    }
  }
  return max;
}
```
``` javascript
maxSubarraySum([2,6,9,2,1,8,5,6,3],3)
```
super solution:
``` javascript
function maxSubarraySum(arr, num){
  let maxSum = 0;
  let tempSum = 0;
  if (arr.length < num) return null;
  for (let i = 0; i < num; i++) {
    maxSum += arr[i];
  }
  tempSum = maxSum;
  for (let i = num; i < arr.length; i++) {
    tempSum = tempSum - arr[i - num] + arr[i];
    maxSum = Math.max(maxSum, tempSum);
  }
  return maxSum;
}
```
``` javascript
maxSubarraySum([2,6,9,2,1,8,5,6,3],3)
```