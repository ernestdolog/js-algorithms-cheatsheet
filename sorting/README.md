# Sorting algoritms
> sorting algorytms comparison: https://www.toptal.com/developers/sorting-algorithms

#### Array.sort (built in sorting algorythm):

takes input as strings, and default sorting is alphabetical:
```
["d", "b", "e", "a", "c"] => ["a", "b", "c", "d", "e"]
```
also when you sort numbers:
```
[15, 5, 10, 9, 1, 2] => [1, 10, 15, 2, 5, 9]
```
in this numeric case we should use the optional comparator to .sort();
(function returns negative, a comes before b , positive, b comes before a, 0, they are equal)
``` javascript
function asc (a, b) {
    return a - b;
}
```
``` javascript
function desc (a, b) {
    return b - a;
}
```

[Visualgo link](https://visualgo.net/en/sorting?slide=1)