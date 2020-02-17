---
layout: post
title:      "Sinatra-Flash"
date:       2020-02-17 01:27:22 +0000
permalink:  sinatra-flash
---

For my portfolio project I used sinatra-flash for any error messages that might be helpful to the user when something goes wrong. 

To use it for my project i pasted 'gem 'sinatra-flash'' into my Gemfile, then ran `$ gem install sinatra-flash`.  To use the gem all I had to do was register it in my ApplicationController class. This allows me to use it throughout my whole app. 

 ```
class ApplicationController < Sinatra::Base
   configure do
     set :public_folder, 'public'
     set :views, 'app/views'
     enable :sessions
     set :session_secret, "secret"
     register Sinatra::Flash
   end
```
   

Now I can place my message wherever fit. In this case when logging in. 

 ```
 post "/login" do 
    #find  
    @farmer = Farmer.find_by(username: params[:username])
    #authenticate 
    if @farmer && @farmer.authenticate(params[:password])
     session[:farmer_id] = @farmer.id
       redirect "/farmers/#{@farmer.id}"
    else 
     flash[:message] = "username and/or password in not valid. please try again."
      reirect "/login"
    end 
   end 
 
```

 Adding this line `flash[:message] = "username and/or password in not valid. please try again."` will allow the user to know what when wrong when logging in. 
 
I also styled my message to be red:

```
 <% if flash[:message] %>
       <center style ="color:red;"><%= flash[:message] %></center>
			 <br>
	<% end %>
```
     


