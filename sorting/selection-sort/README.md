# Selection sort
Goes through the array over and over. Always places the currently found minimum in the beginning.

> It's good if you want to minimise the number of swaps you are making.

> Quadratic sorting algorythm. time complexity: O(n^2)

#### pseudocode:
 - store the first element as the smallest value you have seen so far
 - compare this value to sequential next items until you find a smaller
 - if a smaller number is found designate it as the minimum, and keep on looping till the end of the array
 - if the minimum is not the first value you designated as minimum, swap them

``` javascript
function selectionSort (arr) {
  const swap = (arr, idx1, idx2) => [arr[idx1], arr[idx2]] = [arr[idx2], arr[idx1]];
  for (let i = 0; i < arr.length; i ++) {
    let min = i;
    for (let j = i + 1; j < arr.length; j ++) {
      if (arr[j] < arr[i]) min = j;
    }
    if (i !== min) swap (arr, i, min);
  }
  return arr;
}
```

