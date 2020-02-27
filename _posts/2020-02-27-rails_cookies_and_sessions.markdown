---
layout: post
title:      "Rails Cookies and Sessions"
date:       2020-02-27 19:09:49 +0000
permalink:  rails_cookies_and_sessions
---


###  Cookies and Sessions:

Because HTTP servers are stateless cookies and sessions allow user to access previous session information (such as cart id). A cookie is stored in plain text in user's browser, so using the sessions method is more secure. 

 **set cart_id**
  session[:cart_id] = @cart.id
 
  **load the cart referenced in the session**
  @cart = Cart.find(session[:cart_id])

Rails has a method, let's call it sign, which takes a message and a key and returns a signature, which is just a string:
	
*sign(message: string, key: string) -> signature: string*

```
  def sign(message, key):
  *cryptographic magic here*
  return signature
end
```

So when a cookie is recevied, Rails creates and  verifies a signature to make sure there is a match 
Example:
sign(cookie_body, secret_key_base) == cookie_signature

We can also use sessions to log in and out. 

```

class SessionsController < ApplicationController
    def new
        # nothing to do here!
    end
 
    def create
        session[:username] = params[:username]
        redirect_to '/'
    end
end
```
In the example about, we've set a session cookie by adding the username into the session hash


