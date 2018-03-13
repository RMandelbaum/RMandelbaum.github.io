---
layout: post
title:      "Don't Repeat Yourself: An Intro to Partials in Rails"
date:       2018-03-12 21:55:57 -0400
permalink:  dont_repeat_yourself_an_intro_to_partials_in_rails
---


When I first started building applications with Rails, my main focus was getting the app to work, not so much on making my code look neat. Now, that I have a bit more experience, I like to implement partials to keep my code DRY. 

**What is a Partial?**

A partial is a piece of reusable view code that you can use to keep your project compact. Let’s say we have a form in two sections that are almost identical (very common with new and edit forms). Instead of rewriting the same code, we can simply implement a partial to be rendered in both locations. 

Let’s look at an example. We have a form to create new posts and form to edit our posts. 

```
views/posts/new.html.erb

<h1> New Post Form </h1>

<%= form for (@post) do |f| %>
	<div>
	  <%= f.label :title %>
		<%= f.text_field :title %>
		<%= f.label :body %>
	  <%= f.text_area :body %>
	  <%= f.submit %> 
	</div>
<% end %> 
```

```
views/posts/edit.html.erb

<h1> Edit Post Form </h1>

<%= form for (@post) do |f| %>
	<div>
	  <%= f.label :title %>
    <%= f.text_field :title %>
	  <%= f.label :body %>
	  <%= f.text_area :body %>
	  <%= f.submit %> 
	</div>
<% end %> 
```

Now, these two forms look almost identical, so we should use a partial to keep our code DRY. To create a partial, simply add a `_` before the file name. Let’s go ahead and do this.

```
views/posts/_form.html.erb

<%= form for (@post) do |f| %>
	<div>
	  <%= f.label :title %>
    <%= f.text_field :title %>
	  <%= f.label :body %>
	  <%= f.text_area :body %>
	  <%= f.submit %> 
	</div>
<% end %> 
```

```
views/posts/new.html.erb

<h1> New Post Form </h1>

<%= render ‘form’ %> 
```

```
views/posts/edit.html.erb

<h1> Edit Post Form </h1>

<%= render ‘form’ %>
``` 

And with that, our code is now more compact, and easier to change. If we wanted to add a new field in our form, we only would have to do this once. 
