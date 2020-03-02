---
layout: post
title:      "Sinatra Review"
date:       2020-03-02 12:54:53 -0500
permalink:  sinatra_review
---


###  MVC
Model - Where the data lives
contains the class and class logic

View - holds html using an erb file (embedded ruby). 
this is what allows the user to interact with the app; how things look and are displayed. 

Controller -bridge between models and view (routes)
actions are passed as blocks to methods that correspond to HTTP request verbs 

###  request/response flow
when user types in URL controller routes url to matching block of code. This then calls on the model which gets data from the database. Which then renders the view. 


###  session scope
a session is a hash that stores data. That data is then passed as a cookie to the client. 

In a controller we can `enable` sessions within the configure block. Below that `set :session_secret, "secret"`, is an encryption key that will be used to create a session_id. The session_id is a string of letters that is unique to a users session.
```
configure do
  enable :sessions
  set :session_secret, "secret"
end
```

Because we enabled sessions, every controller action has access to the session hash.
If the session hash is stored in an instance variable, `@session`, the views will also have access to that data.

###  has_secure_password
has_secure_password is added to the model class and has built in validations to make sure passowrd is not blank.
there is an "invisible" macro method (.authenticate) in has_secure_password that makes sure the password provided is correct
an ActiveRecord macro (method that when called, creates methods)
it works with bcrypt so it isnt stored in plain text. 

###  ActiveRecord associations
Associations are class methods that allow objects to relate (or associate) to each other through foreign keys. 

has_many -more then one object can own many objects of the same class. This is also an ActiveRecord macro. 
belongs_to - one to one association with another class, this class with have the foreign key associated with the class it belongs to. 

Foreign key's are used because tables need to know how to relate to one another. A foreign key will point to a primary key in another table.  

For example:

PostsTable will have :user_id <- this is the foreign key, which sits in the user's table. 


