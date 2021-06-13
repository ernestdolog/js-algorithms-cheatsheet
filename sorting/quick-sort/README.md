# Quick sort
Uses the fact that 0 or 1 element long arrays are always sorted.
Picks one element (the "pivot"), and figures out which index it should go in the array.
(moves all the smaller numbers to the left of this num, the bigger to the right -  no sort, just move)

> time complexity: O(n log n) - worst case: O(n^2) (it happens if you pick by default the minimum or the maximum)

### First step: Pivot helper
We want a function that it gets an element of an array as an input.
It puts all smaller elements on the left, and all greater ones on the right.
Order/sortedness doesn't matter here.
It shlould return the index of the inputted element. The "pivot".

``` javascript
function pivotHelper (idx, arr) {
    const pivotVal = arr[idx];
    let smallerAmount = 0;
    swap (arr, idx1, idx2) {
        const temp = arr[idx1];
        arr[idx1] = arr[idx2];
        arr[idx2] = temp;
    }

    for (let i = idx + 1; i < arr.length; i ++) {
        const currentVal = arr[i];
        if (currentVal < pivotVal) {
            swap(arr, idx + 1 + smallerAmount, i);
            smallerAmount ++;
        }
    }

    if (smallerAmount > 0) {
        swap(arr, idx, smallerAmount);
        return smallerAmount;
    }
    return idx;
}

// es6 solution:
function pivot(arr, start = 0, end = arr.length - 1) {
  const swap = (arr, idx1, idx2) => {
    [arr[idx1], arr[idx2]] = [arr[idx2], arr[idx1]];
  };

  // We are assuming the pivot is always the first element
  let pivot = arr[start];
  let swapIdx = start;

  for (let i = start + 1; i <= end; i++) {
    if (pivot > arr[i]) {
      swapIdx++;
      swap(arr, swapIdx, i);
    }
  }

  // Swap the pivot from the start the swapPoint
  swap(arr, start, swapIdx);
  return swapIdx;
}
```

### Second step: Quick Sort implementation
 - call the pivot helper on the first element
 - as pivot helper returns the updated index, recursively call pivot helper on the left and right subarray

``` javascript
function quickSort (arr, left = 0, right = arr.length - 1) {
    if(left !== right) {
        const pivIdx = pivot(arr, left, right);
        // we don't use return val, just mutate the array by `pivot` function
        // left left left - than left left right - than left right left - than left right right ... ... ...
        quickSort(arr, left, pivIdx - 1);
        quickSort(arr, pivIdx + 1, right);
    }
        return arr;

}
```

> Thought: Unlike in merge sort, where we use return values, and merge back, here there is no re-merge. Because whatever sub arrays we touch, we know that it's position is correct, because it's between correctly indexed elements.