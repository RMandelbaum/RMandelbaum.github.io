---
layout: post
title:      "Jest: Applying TDD To Our Code"
date:       2018-05-06 18:47:51 +0000
permalink:  jest_applying_tdd_to_our_code
---

While learning to code, I worked on many mini projects that were equipped with tests. Boy, was I spoiled. I know TDD is essential for good programming, but I never tried writing my own set of tests for my code. As I’m applying to jobs, I’ve been assigned ‘code challenges’ that include adding tests. So, I had to rewind and learn how. 

Since I’ve been practicing algorithm problems with JavaScript, I decided to start with Jest. I quickly realized that a huge reason we should use tests is that often it’s easier to understand what the code is doing through the english written in the tests than by parsing through all the code without the tests. Basically, that they not only catch errors and make sure your code works, but they act as notes to other developers.

I was learning how to code a function to tell if the input is a palindrome, and decided to write a test to help drive my code. 

```
function checkForPalindrome(number){
  return true
}
```


First we have to tell the tests which file to look for so we add:
```
const checkForPalindrome = require('./palindrome.js').checkForPalindrome
```

Then the series of tests relating to that function begin with a “describe” keyword: 

`describe('checkForPalindrome', function()`

Within the “describe” part, there is an “expect” keyword, that articulates the actual thing you are testing. In this case we call the function with a test number, 1001, and assert that it should return true.

```
   test('returns true if number is the same forward and backward',     
   function(){   
       expect(checkForPalindrome(1001)).toEqual(true)
   })
```

In order to run it there are a few other necessities including setting up the testing environment, running ‘npm run test’ or ‘npm t’ in the terminal, and including this line in your original file so that it knows to communicate with your spec file.

```
module.exports = {checkForPalindrome}
```

Final results: 
```
const checkForPalindrome = require('./palindrome.js').checkForPalindrome
describe('checkForPalindrome', function(){
test('returns true if number is the same forward and backward', function(){
 expect(checkForPalindrome(1001)).toEqual(true)
})
test('return true if it is a 1-digit number', function(){
 expect(checkForPalindrome(1)).toEqual(true)
})
test('return false if number does not read the same forward & backward', function(){  expect(checkForPalindrome(2075)).toEqual(false)
})
test('return false if user does not input an integer', function(){
 expect(checkForPalindrome('racecar')).toEqual(false)
})
})
```
Learning this gave me a lot more context and understanding for TDD and helped me visual what I’m trying to do before I actually attempt to do it. 


