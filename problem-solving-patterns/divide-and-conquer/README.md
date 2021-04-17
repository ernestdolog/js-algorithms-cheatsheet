# Divide and conquer
This pattern involves dividing a data set into smaller chunks and then repeating 
a process with a subset of data.

> It can decrease time complexity.

## example:

#### 1. given a sorted array of integers, write a function called 'search', that acceptsd a value and returns the index where the value passed to the function is located. If the value is not found return -1.

first hand solution: O(n)

``` javascript
function search (arr: number[], val: number) {
    for (let i = 0; i < arr.length; i++) {
        if (arr[i] === val) {
            return i;
        }
    }
    return -1;
}
```
a bit more effective soluution: O(log(n))
``` javascript
function search (arr: number[], val: number) {

    let min = 0;
    let max = arr.length - 1;

    while (min <= max) {
        let mid = Math.floor((min + max) / 2);
        let currentElement = array[middle];

        if (array[middle] < val) {
            min = middle + 1;
        } else if (array[middle] > val) {
            max = middle - 1;
        } else {
            return middle;
        }
    }

}
```