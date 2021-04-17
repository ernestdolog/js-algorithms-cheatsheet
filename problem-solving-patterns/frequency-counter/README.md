# Frequency counter

In case of objects or sets to collect values/frequencies of values.

> This helps us to avoid nested loops O(n^2) with arrays, or strings.

## examplez:

#### 1. Write a function, called 'same' which accepts 2 arrays. The function should return true if every value in the array have it's corresponding value squared in the other array. The frequency of the arrays has to be the same.

``` javascript
same([1,1,3,2], [9,1,4,4]) false
same([1,2,3,2], [9,1,4,4]) true
same([1,2,3], [9,1,4]) true
```
first hand solution:
``` javascript
function same(arr1, arr2){
    if(arr1.length !== arr2.length){
        return false;
    }
    for(let i = 0; i < arr1.length; i++){
        let correctIndex = arr2.indexOf(arr1[i] ** 2)
        if(correctIndex === -1) {
            return false;
        }
        console.log(arr2);
        arr2.splice(correctIndex,1)
    }
    return true;
}
```
``` javascript
same([1,2,3,2], [9,1,4,4])
```

very cool solution:

> instead of looping through the first array and checking for each value in the other array (nested loop)
we loop through the 2 arrays 2 times and fill our metadata objects
``` javascript
function same(arr1, arr2){
    if(arr1.length !== arr2.length){
        return false;
    }
    let frequencyCounter1 = {}
    let frequencyCounter2 = {}
    for(let val of arr1){
        frequencyCounter1[val] = (frequencyCounter1[val] || 0) + 1
    }
    for(let val of arr2){
        frequencyCounter2[val] = (frequencyCounter2[val] || 0) + 1        
    }
    console.log(frequencyCounter1);
    console.log(frequencyCounter2);
    for(let key in frequencyCounter1){
        if(!(key ** 2 in frequencyCounter2)){
            return false
        }
        if(frequencyCounter2[key ** 2] !== frequencyCounter1[key]){
            return false
        }
    }
    return true
}
```
``` javascript
same([1,2,3,2,5], [9,1,4,4,11])
```
#### 2. We have 2 strings, write a function that determines if the second string is the anagram of the first. An anargam is a re-arrangement of the letters of a word.
``` javascript
function validAnagram(first, second) {
  if (first.length !== second.length) {
    return false;
  }

  const lookup = {};

  for (let i = 0; i < first.length; i++) {
    let letter = first[i];
    // if letter exists, increment, otherwise set to 1
    lookup[letter] ? lookup[letter] += 1 : lookup[letter] = 1;
  }
  console.log(lookup)

  for (let i = 0; i < second.length; i++) {
    let letter = second[i];
    // can't find letter or letter is zero then it's not an anagram
    if (!lookup[letter]) {
      return false;
    } else {
      lookup[letter] -= 1;
    }
  }

  return true;
}
```
``` javascript
// {a: 0, n: 0, g: 0, r: 0, m: 0,s:1}
validAnagram('anagrams', 'nagaramm')
```
