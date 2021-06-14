# Radix sort
This algorythm works on binary stuff... numers and strings basically
No direct comparisons between elements (that's where it's power comes from!)
Uses the fact that size of a number is encoded in the digits.

> time complexity: O(nk) (k means the biggest amount of digits present together in an element) - if all values are distinct, than k = log(n)
> space complexity: O(n + k)

### First step: Get Digit
We need a function to take a number, and get it's digit at a position.
Take the number, divide with 10^idx, floor it, than take rest from dividing by 10

> Positions are counted from right to left

``` javascript
getDigit (idx, input) {
    return Math.floor(Math.abs(input) / Math.pow(10, idx)) % 10;
}
```

### Second step: Digit Count
> Per element
Function to count number of digits in a number.

``` javascript
function digitCount(num) {
  if (num === 0) return 1;
  return Math.floor(Math.log10(Math.abs(num))) + 1;
}
```

### Third step: Most Digits
> Per array
Function to return the amount of digits in the element where the most digits are.

``` javascript
function mostDigits(nums) {
  let maxDigits = 0;
  for (let i = 0; i < nums.length; i++) {
    maxDigits = Math.max(maxDigits, digitCount(nums[i]));
  }
  return maxDigits;
}
```

### Fourth step: Radix sort
 - define a function that takes an array of numbers
 - figure how many digits is the current maximum
 - loop from 0 to this largest number:
  - create buckets for each digits between 0 and 9
  - place each number in the buckets according to it's currently evaluated digit
 - replace current array with values from the buckets (ascending manner)
 - return the list

``` javascript
function radixSort(nums){
    let maxDigitCount = mostDigits(nums);
    for(let k = 0; k < maxDigitCount; k++){
        let digitBuckets = Array.from({length: 10}, () => []);
        for(let i = 0; i < nums.length; i++){
            let digit = getDigit(nums[i],k);
            digitBuckets[digit].push(nums[i]);
        }
        nums = [].concat(...digitBuckets);
    }
    return nums;
}
```