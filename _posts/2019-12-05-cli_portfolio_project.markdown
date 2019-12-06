---
layout: post
title:      "CLI Portfolio Project"
date:       2019-12-06 02:18:21 +0000
permalink:  cli_portfolio_project
---

This portfolio project is a CLI (command line interface) that connects to a database using an API (application programming interface). Using the API the user will send out a request to receive information, in this case it is movies by popularity, and our app will then get that response. This app involves a movie database. 

The first thing to do is to set up the environment. I was able to find how to here https://austinmelchior.com/blog/1. Something to note was that you must `git clone` everytime the IDE loads; also be sure to push commits often. 

Next was to set up the Readme and gemspec file where all the dependencies are located. Fill in the TODO's with appropriate information and add any neccessary dependencies. For this app it was:
```
spec.add_development_dependency "pry"
spec.add_development_dependency "httparty"

*We will require these in the environment file MovieCli.rb which also requires movies.rb, cli.rb, api.rb and version.rb.
```
HTTParty allows our app to access API request methods (GET, POST, PUT, and DELETE)

The bin folder has a file called MoviesCLI which contains the shebang ` #!/usr/bin/env ruby` 
This tells the env command where to run the ruby interpreter. We also require a file called MoviesCli and add this line `CLI.new.start` which starts a new CLI. Ultimately this whole file allows the program to run when `bin/MoviesCli` is entered. 


Next within the MoviesCli folder there are three files I will go over. 

The movies.rb file contains the class method that intializes a new instance of a movie that includes a title, a release date, and an overview of the movie. We are also able to find a movie by name. 

The cli.rb file is what the user will interact with. We once again will create a class method. The use of various intance methods allows the user to input a command and ultimately the command line will post it. Allowing the user to find a movie title was a little difficult for me at first. I had to create an intance method that calls `Movies.find_by_name` and has `input` as a parameter. 

The api.rb file fetches the api from the movie database https://api.themoviedb.org. When you create an account and create an app, themoviedb will give you a key. You add the key and the specific url needed for your request. In my instance I wanted a list of movies sorted by popularity. I iterate through the `results` array in the database and retreive the information I wanted to include (title,release date, overview). 

And there it is. I created a simple project with basic functionality. 
