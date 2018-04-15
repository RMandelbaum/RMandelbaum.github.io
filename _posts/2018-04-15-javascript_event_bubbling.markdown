---
layout: post
title:      "JavaScript Event Bubbling "
date:       2018-04-15 14:23:18 -0400
permalink:  javascript_event_bubbling
---


Ever wonder what is happening under the hood when we click something in the browser? Well, a whole lot, but let’s start with a small piece called event bubbling. 


Event bubbling occurs when an event is triggered, like a mouse click on a button, and then is also triggered on all of that element’s ancestors. 
> Essentially, the event bubbles up from the originating element to the top of the DOM tree. 
> 

Let's look at some code
﻿
```
<div id =”grandparent-div”>
Grandparent
    <div id = “parent-div”>
 Parent
        <div id ="child-div>
  Child
        </div>      
    </div>
</div>
```

To add an event listener to our elements with bubbling we use this syntax
	`eventTarget.addEventListener(type, listener,[useCapture]);`


To add a click event to our divs we’d do something like this:
```
$(“#child-div”).addEventListener(“click”, function (event) {
		console.log(“I’m the child”);
	}, false); 

$(“#parent-div”).addEventListener(“click”, function (event) {
		console.log(“I’m the parent”);
	}, false); 

$(“#grandparent-div”).addEventListener(“click”, function (event) {
		console.log(“I’m the grandparent”);
	}, false); 
```

When we click on the child div, we will see this output:

```
<“I'm the child”
<“I’m the parent”
<“I’m the grandparent”
```

If we clicked on just the grandparent, we’d only see this output: 

```
<“I’m the grandparent”
```

We put `false`, which is the default for useCapture. If we set it to `true`, our event would enter a capturing phase, where the event trickles down from parent to child, rather than bubble up from child to parent. 

Event bubbling is usually associated with event capturing and event propagation. These concepts work together to create the event delegation pattern, which, when used correctly, allows us to add an event handler to a more specific target and write cleaner code. 
