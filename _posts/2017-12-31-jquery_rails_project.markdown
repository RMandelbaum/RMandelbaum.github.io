---
layout: post
title:      "jQuery/Rails Project"
date:       2017-12-31 16:22:09 -0500
permalink:  jquery_rails_project
---



As burgeoning web developers, we would be nowhere without Javascript in our applications. For this project, we were given the task to add jQuery and Ajax to our previous Rails application. This meant breaking my working rails project to put it back together for a friendlier user experience.

**The Plan**

I would use JS on the dog index page, to access each individual dog's show page. I wanted to click on each dog, and render the dog's age, breed, and temperament, and also a list of the walks that belonged to that dog. Then there would be the option to add a new walk, save it to the database, and also post it to that same page. This entire process would happen without a full page reload using Ajax. 

**The Process**

1. Set up the server side to render JSON through a serialization gem, and the Javacript asset pipeline.
2. Add classes and/or Ids to my HTML to target each element for jQuery. 
3. Attach event handler's to listen to click's on the page. Previously, when a user clicked on a dog's name, it would redirect to that dog's show page. Now, this would be prevented and continue on to use Ajax to render the data from a JSON formatted API. 
4. Create a new dog model object with the response data, and set up prototype methods to format the data and append it to the DOM. 
5. Add a link to create a new walk form and use Ajax with the formatters to post it to the DOM. 
6. Add a close button to toggle all of the additional details on the DOM. 

**The Outcome**

The dogs index page now implemented Javascript and is easier to use. Instead of the user going back and forth between 3 different web pages, they could access and add information all on one page. 
