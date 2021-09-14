# Recursion
Recursion is a process that calls itself.

> Useful when we are doing for instance "in-depth" search.

#### what happens in call stack when a function calls itself again and again?:

The call stack call a function, and puts in top of the stack. Every function
what is called in this process is putted to the top of the stack. The one at the very topmeans this function is executed right now.
So the top function in the stack will return first adn be taken out from the stack.
Stack is a data structure, where first on top is first to execute. Last in first out.

## pure recursion
Same with recursion, but we don't fallback to a helper function, but the function itself.
``` javascript
function collectOddValues(arr){
    let newArr = [];
    
    if(arr.length === 0) {
        return newArr;
    }
        
    if(arr[0] % 2 !== 0){
        newArr.push(arr[0]);
    }
        
    newArr = newArr.concat(collectOddValues(arr.slice(1)));
    return newArr;
}
```
``` javascript
collectOddValues([1,2,3,4,5])
```                                   
                                                                
                                                
#### Pure recursion tips:

 - for arrays use methods like 'slice', the spread operator and 'concat'. They make copies of the array, so you don't need to mutate.
 - strings are immutable, so use 'slice', 'substr' or 'substring' to make copies of strings
 - to make copies of objects use Object.assign, or the spread operator

## helper function recursion

```javascript
function collectOddValues(arr){
    
    let result = [];

    function helper(helperInput){
        if(helperInput.length === 0) {
            return;
        }
        
        if(helperInput[0] % 2 !== 0){
            result.push(helperInput[0])
        }
        
        helper(helperInput.slice(1))
    }
    
    helper(arr)

    return result;
}

collectOddValues([1,2,3,4,5,6,7,8,9])
```                                         
                                                                             
                            
## ezamplez:

#### count factorial of a number
```javascript
function factorial(num){
    if(num === 1) return 1;
    return num * factorial(num-1);
}
```


#### counts the sum of a range of numbers
```javascript
function sumRange(num){
    if(num === 1) return 1; 
    return num + sumRange(num-1);
 }
 
 sumRange(4)
```