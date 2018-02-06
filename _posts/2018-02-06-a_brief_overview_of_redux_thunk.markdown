---
layout: post
title:      "A Brief Overview of Redux Thunk  "
date:       2018-02-06 00:18:54 -0500
permalink:  a_brief_overview_of_redux_thunk
---


Anyone who is learning React with Redux knows that an explanation is anything but brief. But, I promise to keep this one short by focusing primarily on Redux Thunk, rather than the whole picture. While trying to find a good resource to define Redux Thunk and why I would need it for my app, I came across my favorite answer by Dan Abramov, co-author of Redux and Create React App. 
> If you’re not sure whether you need it, you probably don’t. 

 I'm sure he meant this in a helpful nature, but all I hear is if you have to ask about it, you clearly aren't ready to use Redux at this level. And I love that answer.     

For now, let's say we are sure we need Redux Thunk, and want to learn how it affects our Redux pattern in our React app. You may be thinking* Oh I know all about Thunk, it's that middleware that I use..,* and then move on. 

**But What Exactly is Middleware?** 

Redux docs explains it as: 

> Middleware is some code you can put between the framework receiving a request, and the framework generating a response.
> 
> Redux middleware [...] provides a third-party extension point between dispatching an action, and the moment it reaches the reducer. People use Redux middleware for logging, crash reporting, talking to an asynchronous API, routing, and more.

Alright, so to sum this up in the most basic way, Redux Thunk helps us connect an action with a reducer. But doesn't that already happen? Why do we need a third-party extension? 

Turns out Redux doesn't support asynchronous actions. All those web requests we send in JavaScript are all asynchronous. Generally, when we make calls to our API,  we'd write something like this:

```
export function fetchItems() {
  const items = fetch('http://www.exampleAPI.com');
  return {
    type: 'FETCH_ITEMS', 
    items
  };
};
```

This function may seem correct, but we must keep in mind two things:
1. This function will run asynchronously, which means it will try to return a value before all of our data is fetched. To work around this, we could add `.then() `to our `fetch()`, making our *fetch* function synchronous. However, this does not stop our overall function of *fetchItems* from returning asynchronously, and we just learned, Redux action creators do not support these asynchronous actions. 

2. Retrieving data takes time, and since this is Redux on top of JavaScript, we'd want to represent this time in our state.

This just got a whole lot more complicated than we originally thought. But that's why we turn to our Redux Thunk middleware. Thankfully, someone else already figured out how to work around this and all we need to do is:  

```
npm install --save redux-thunk

import { createStore, applyMiddleware } from 'redux';
import thunk from 'redux-thunk';
import rootReducer from './reducers/index';

const store = createStore(
  rootReducer,
  applyMiddleware(thunk)
);

```

**Understanding a Thunk**

Redux Thunk allows us to create an action creator that returns a *function*, rather than an action object. This action creator is now a **thunk**.

> A thunk is a function that wraps an expression to delay its evaluation. 

This is incredibly useful because now we can pass store methods (like dispatch) into our returned function, allowing us to update the store and control our return values.

```
export function fetchItems() {
  return (dispatch) => {
    dispatch({ type: 'START_ADDING_ITEMS_REQUEST' });
    return fetch('http://www.exampleAPI.com')
      .then(response => response.json())
      .then(items => dispatch({ type: 'ADD_ITEMS', items }));
  };
}
```

We wrap our `fetch()` in a thunk, by passing `dispatch` into our return function. This triggers a state change, and ensures that our return `fetch() `gets resolved before we invoke our responses. Our thunk controls the flow of the entire function, and allows us to properly communicate with an asynchronous API. 

I hope this blog helped explain how Redux Thunk can fit into your app, and you can confidently decide whether or not you need to use this middleware. 

