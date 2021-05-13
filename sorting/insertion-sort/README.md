# Insertion sort
Builds up the sort by gradually creating a larger half which is always sorted.

> It's good when new data is constantly coming in and you need to maintain a sorted array.

> Quadratic sorting algorythm. time complexity: O(n^2)

#### pseudocode:
 - as start pick the second element in the array
 - compare the second element with the first one and swap if necessary
 - pick the next element, compare it to the left, if correct position leave where it is, if not, iterate
 through the array, and put it right to the first value which is smaller

``` javascript
function insertionSort (arr) {
    for (let i = 1; i < arr.length; i ++) {
        let currentVal = arr[i];
        // until currentVal is smaller than given item... (or we reached 0 elem of arr)
        let j = i - 1;
        while (j >= 0 && currentVal < arr[j]) {
            // we push values 1 position right
            arr[j + 1] = arr[j];
            j--;
        }
        // we put to the "discovered lowest point" currentVal
        arr[j + 1] = currentVal;
    }
    return arr;
}
```