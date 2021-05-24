# Merge sort
Merge and Sort.:
Arrays of 0-1 elements are always sorted. So it divides the array into subarrays of 0-1 elements
than builds up a sorted array.

when we merge, we merge 2 sorted arrays:

``` javascript
function merge(arr1, arr2){
    let results = [];
    let i = 0;
    let j = 0;
    while(i < arr1.length && j < arr2.length){
        if(arr2[j] > arr1[i]){
            results.push(arr1[i]);
            i++;
        } else {
            results.push(arr2[j])
            j++;
        }
    }
    while(i < arr1.length) {
        results.push(arr1[i])
        i++;
    }
    while(j < arr2.length) {
        results.push(arr2[j])
        j++;
    }
    return results;
}

mergeSortedArrays([1, 10, 15, 16, 17], [2, 3, 4, 15, 16]);
```

than let's divide the array to subarrays:

#### pseudocode:
 - break the array to it's half recursively until you have subarrays 0-1 length
 - as you have smaller arrays, merge them back until you get back the full length array
 - once it's merged together, return the final array

 ``` javascript
function mergeSort(arr){
    if(arr.length <= 1) return arr;
    let mid = Math.floor(arr.length/2);
    let left = mergeSort(arr.slice(0,mid));
    let right = mergeSort(arr.slice(mid));
    // merge function from earlier
    return merge(left, sright);
}

mergeSort([10,24,76,73])
```