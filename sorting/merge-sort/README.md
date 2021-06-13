# Merge sort
Merge and Sort.:
Arrays of 0-1 elements are always sorted. So it divides the array into subarrays of 0-1 elements
than builds up a sorted array.

> time complexity: O(n log n) - worst avg best case the same time complexity

A thought: why n log n?:

If 1 split (we split 1 full array, or 2 half arrays - here same thing) is 1 step to split an array of length n into 1 or 0 length subarrays is log n steps
why?
we always half, what means /2, we are interested here how much /2 we need from 1 (2^0) to get to our full array...
ergo: how much of power i'v to make 2 to get there...

> space complexity: O(n) - ^^-^^

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

merge([1, 10, 15, 16, 17], [2, 3, 4, 15, 16]);
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
    return merge(left, right);
}

mergeSort([10,12,48,24,76,73])
```

cool resource:
> https://www.bigocheatsheet.com/