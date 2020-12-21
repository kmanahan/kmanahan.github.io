---
layout: post
title:      "A short explanation of Thunk"
date:       2020-12-21 05:50:06 +0000
permalink:  a_short_explanation_of_thunk
---

Thunk is a special function that is returned by another function. When using thunk with Redux  we are able to perform fetch requests  with redux-thunk which allows you to be able to dispatch an action (the action creators) asynchronously. 

example:

```
function loadCats() {
  // Return a thunk
  return function(dispatch) {
    fetch('cats-api-url')
      .then(res => res.json())
      .then(data => {
        dispatch({
          type: 'ADD_CATS',
          payload: data.cats,
        });
      });
  };
}
```


