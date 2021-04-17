# Bubble sort
goest through the array, swaps 2 values if they are in the incorrect order... repeats this over and over


#### pseudocode:
 - loop with a var from the end of array towards the beginning (this will do the loop over and over)
 - start an inner loop with other var from beginning to length - 1 (comparing loop)
 - if arr[j] greater than arr[j + 1], swap those 2 values like this:
    function swap (arr, idx1, idx2) {
        const temp = arr[idx1];
        arr[idx1] = arr[idx2];
        arr[idx2] = temp;
    }
 - return the sorted array

example coming soon...