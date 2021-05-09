# Bubble sort
goest through the array, swaps 2 values if they are in the incorrect order... repeats this over and over

> It's good if you know surely that the data is almost totally sorted with 1-2 mistakes.


#### pseudocode:
 - loop with a var from the end of array towards the beginning (this will do the loop over and over)
 - start an inner loop with other var from beginning to length - 1 (comparing loop)
 - if arr[j] greater than arr[j + 1], swap those 2 values like this:
    function swap (arr, idx1, idx2) {
        const temp = arr[idx1];
        arr[idx1] = arr[idx2];
        arr[idx2] = temp;
    }
    const swap = (arr, idx1, idx2) => [arr[idx1], arr[idx2]] = [arr[idx2], arr[idx1]];
 - return the sorted array

O(n^2)
``` javascript
function bubbleSort(arr){
  for(var i = arr.length; i > 0; i--){
    for(var j = 0; j < i - 1; j++){
      if(arr[j] > arr[j+1]){
        var temp = arr[j];
        arr[j] = arr[j+1];
        arr[j+1] = temp;         
      }
    }
  }
  return arr;
}
```

O(n^2)
either this:
``` javascript
function bubbleSort(arr) {
  const swap = (arr, idx1, idx2) => {
    [arr[idx1], arr[idx2]] = [arr[idx2], arr[idx1]];
  };

  for (let i = arr.length; i > 0; i--) {
    for (let j = 0; j < i - 1; j++) {
      if (arr[j] > arr[j + 1]) {
        swap(arr, j, j + 1);
      }
    }
  }
  return arr;
}
```
O(n)
least amount of loops:
``` javascript
function bubbleSort(arr) {
  const swap = (arr, idx1, idx2) => {
    [arr[idx1], arr[idx2]] = [arr[idx2], arr[idx1]];
  };
  let swapped = false;
  do {
    swapped = false;
    for (let i = 0; i < arr.length; i++) {
      if (arr[i] > arr[i + 1]) {
        console.log('arr[i]', arr[i], 'arr[i + 1]', arr[i + 1])
        swap(arr, i, i + 1);
        swapped = true;
      };
    }
  } while (swapped);
  return arr;
};
```
``` javascript
bubbleSort([8,1,2,3,4,5,6,7]);
```