---
layout: post
title:      "Hoisting: Understanding the Order of Your Code "
date:       2018-01-13 15:18:29 -0500
permalink:  hoisting_understanding_the_order_of_your_code
---

I got it, I got it. I got it. [thump] I ain't got it. 

When we talk about hoisting, I instantly picture that guy from *High Anxiety* trying his best to push up a variable declaration. Maybe I’ve spent too much time at my computer chugging caffeine, or maybe I’m onto something real. Either way, let’s talk about hoisting. 

**What Is Hoisting?**
> Hoisting is when a variable, function, or class declaration gets moved to the top of their scope.

**Variables**

Let’s take a look at a code example using a variable to translate what that means.  

```
coffeeOrder = “1 Large Latte”;
var coffeeOrder; 
console.log(coffeeOrder);
// “1 Large Latte”  
```

When first looking at this code, we may think that it will be undefined, as the variable is being declared after it is being assigned to a value. However, in Javascript, the code is compiled, and any variable declaration is pushed to the top of the lexical scope. 

Let’s play around with the order of this code to cement this a bit further. 

```
console.log(coffeeOrder);
var coffeeOrder = “1 Large Latte;
// undefined 
```


You may be thinking, didn’t you just say that variable declarations get hoisted to the top?! Well yes, they do, but the assignment of the variable does not. The compiler is actually reading this code as:

```
var coffeeOrder; 
console.log(coffeeOrder);
coffeeOrder = “1 Large Latte”;
```


**Functions**

Now that we are more comfortable with variable hoisting, let’s move on to functions. When we are dealing with functions, we need to keep in mind that *function declarations are hoisted, but  function expressions are not.* Let’s review the difference between a function declaration and a function expression. 

Function Declaration: 
```
function giveMeCoffee() {
  var coffeeOrder = “1 Large Latte”;
  console.log(coffeeOrder); 
} 
```

Function Expression:
```
var giveMeCoffee = () => {
	var coffeeOrder = “1 Large Latte”;
	console.log(coffeeOrder);
	}
```

So now let’s test the difference, by invoking the function before we write a function declaration: 


```
giveMeCoffee();

function giveMeCoffee(){
  var coffeeOrder = “1 Large Latte”;
  console.log(coffeeOrder); 
} 

// “1 Large Latte”. 
```

This function is a declaration, and we just learned that those are hoisted to the top of the scope, so the compiler reads this as:


```
function giveMeCoffee() {
  var coffeeOrder = “1 Large Latte”;
  console.log(coffeeOrder); 
} 

giveMeCoffee();
```


Now let’s try invoking the function before writing a function expression:

```
giveMeCoffee();

var giveMeCoffee = () => {
	var coffeeOrder = “1 Large Latte”;
	console.log(coffeeOrder);
	}
// Uncaught TypeError: giveMeCoffee is not a function
```
    
We are getting an error, since function expressions *are not* hoisted.

**Classes**

Let’s move on to JavaScript classes. Classes can also be written as a declaration or an expression, and behave similarly to functions when it comes to hoisting.  

Let’s review what a class declaration looks like in comparison to a class expression before we get to hoisting. 

Class Declaration:

```
class Coffee{
	constructor(size, type) {
	 this.size = size;
	 this.type = type;
	}
}
```

Class Expression:

```
var Coffee = class {
	constructor(size, type) {
	 this.size = size;
	 this.type = type;
	}
}
```

Now, let’s compare these two classes and see how they react when we create a new class object. 


```
var Drink = new Coffee();
   Drink.size = "large";
   Drink.type = "latte";
   console.log(Drink)


 class Coffee {
	constructor(size, type) {
	 this.size = size;
	 this.type = type;
	}
}

// Uncaught ReferenceError: Coffee is not defined
```

What is happening here? Just like a function declaration, this class declaration is in fact getting hoisted (as we’re not getting `TypeError` or `undefined`), but a class isn’t initialized until it is evaluated, which results in a `ReferenceError`. 

As we saw with function expressions, class expressions are also not hoisted. Let’s take a look at an example:

```
var Drink = new Coffee();
   Drink.size = "large";
   Drink.type = "latte";
   console.log(Drink)

var Coffee = class {
	constructor(size, type) {
  	this.size = size;
	  this.type = type;
	}
}
//Uncaught TypeError: Coffee is not a constructor
```

Here we are getting a `TypeError` because our expression hasn’t been hoisted

> Classes may seem a bit tricky, so just keep in mind that any form of a class must be declared first.
> 

```
 class Coffee {
	constructor(size, type) {
	 this.size = size;
	 this.type = type;
	}
}

var Drink = new Coffee();
   Drink.size = "large";
   Drink.type = "latte";
   console.log(Drink)

//Coffee {size: "large", type: "latte"}
	//size: "large"
	//type: "latte"
	//__proto__: Object 
```

We’ve reviewed hoisting for variables, functions, and classes, and saw how expressions differ from declarations when it comes to functions and classes. Now go and test out your code and see how hoisting can work for you. 
