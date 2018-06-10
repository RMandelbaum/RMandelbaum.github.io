---
layout: post
title:      "Memoization"
date:       2018-06-10 19:33:11 -0400
permalink:  memoization
---


Memoization is when we store the arguments of each function call along with the result. If the function is called again with the same arguments, we return the precomputed result, rather than running the function again. This allows for a faster function, and more efficient time complexity. 

Let’s use Memoization to speed up a Fibonacci function. 

```
function memoize(fn) {
 const cache = {};
 return function (...args) {
     if (cache[args]) {
        return cache[args];
    } 

 const result = fn.apply(this, args);
 cache[args] = result;

 return result;
 };
};

function fib(n) {
 if (n < 2) {
  return n; 
 }
 return fib(n-1) + fib(n-2);
} 

fib = memoize(fib); 
```

