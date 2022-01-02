# Hash Table
> This stuff is built in to most of programming languages.

What is it?
 - Stores key-values pairs.
 > Just like arrays! BUT:
 - Not strictly numeric.
 - Not ordered.
 - It's very fast adding/removing/finding values.
 > It is commonly used because its speed.

In JS we have **Object**-s and **Map**-s. 
> Object keys are strictly string, but it works with the same idea.

**Hash function**: In order to look up values by key, we need a way to convert keys into valid array indices.

Criteria for hash function:
 - We want it fast.
 - Doesn't cluster outputs at specific indices, but distributes uniformly.
 - Same input -> same output.
 - Maps any input into the same size.