---
layout: post
title:      "password_digest"
date:       2020-05-11 10:56:46 -0400
permalink:  password_digest
---


If using Ruby to create an app that has a login in form, password_digest allows the user to have a secure password. 

The password_digest will be included the user's migration schema as a string. To avoid a user's password from being stolen we use a gem called bcrypt. 

Bcrypt then uses has_secure_password to hash and salt the password which is then stored in the password_digest. 

A salt is a random string which is added to the password. For a user to successfully log in the password must much. This can be determeined with .authenticate which is provided by has_secure_password. 
