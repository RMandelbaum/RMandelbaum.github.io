---
layout: post
title:      "JavaScript Type Coercion "
date:       2018-03-05 15:33:04 +0000
permalink:  javascript_type_coercion
---

Like all programming languages, JavaScript has built-in data structures that can be divided into two data types, primitive and complex. 

**Primitive Data Types **

* Boolean
* Null
* Undefined
* Number
* String
* Symbol (new in ES6)

**Complex Data Types**
* Function
* Object 

If you are unsure of your data-type, the browser’s console can be a great help. Simply type in `typeof` followed by some data. Let’s test it out. 
```
typeof 20 // “number”

typeof “Hello” // “string”

typeof false // “boolean”

typeof x // “undefined”

typeof [1,2,3,4,5] // “object” [an array is a JavaScript object]

typeof function dataTypes() {} // “function”

typeof null // “object”

```
Typeof null is considered to be a bug in JavaScript, since null should be “null”, yet it returned as an object 

## Data-Type Coercion 

Programming languages can either be strongly typed or loosely typed. JavaScript falls into the latter category, which means it allows for type coercion. JavaScript can change the data-type behind the scenes without your program crashing. Your program works, but keep in mind that the data-type has been altered. 

### Explicit Type Coercion vs Implicit Type Coercion

Type coercion can occur explicitly or implicitly. 

**Explicit** 
```
Number(“5”) // 5

String(5) // “5”

Boolean(5) // true 
```
**Implicit** 

This occurs when two different data-types are being used with an operator. Since JavaScript is loosely typed, we can do things like add strings to numbers, and know that our data will be implicitly coerced for us. 
```
5 + “5” // “55”

5 + 5 + 5 + “5” // “155” [First adds the numbers (15) and coerced that into “15” to be added to “5” ] 

if (5) {
console.log(“This number is true and implicity coerced to a boolean data-type”)
} 

!!5 // true 
```

**`== ` vs ` ===`**

When you first learn JavaScript, `===` may seem odd, but we use it for type coercion. 

== (loose equality operator) compares and implicitly coerces the data to be the same

```
5 == “5” // true
```

=== (strong equality operator) compares and does not coerce our data. 

```
5 === “5” // false
```

