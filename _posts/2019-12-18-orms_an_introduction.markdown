---
layout: post
title:      "ORMs an Introduction"
date:       2019-12-18 19:35:14 +0000
permalink:  orms_an_introduction
---


### What is an ORM

> it is simply a manner in which we implement the code that connects our Ruby program to our database. For example, you may have seen code that connects your Ruby program to a given database:

```
database_connection = SQLite3::Database.new('db/my_database.db')

database_connection.execute("Some SQL statement")
```

### Mapping Ruby Classes to Databases

It is the responsibility of our program as a whole to create and establish the database.
config directory that contains an environment.rb file. This file will look something like this:

```
require 'sqlite3'
require_relative '../lib/song.rb'
 
DB = {:conn => SQLite3::Database.new("db/music.db")}
```

Here, we also set up a constant, DB, that is equal to a hash that contains our connection to the database.
`DB[:conn]`

> create a new database called music.db, stored inside the db subdirectory of our app and it will return a Ruby object that represents the connection between our Ruby program and our newly-created SQL database. 
> 

```
#<SQLite3::Database:0x007f9d6c294508
 @authorizer=nil,
 @busy_handler=nil,
 @collations={},
 @encoding=nil,
 @functions={},
 @readonly=false,
 @results_as_hash=nil,
 @tracefunc=nil,
 @type_translation=nil>
 
```
#### Creating the Table
To "map" our class to a database table, we will create a table with the same name as our class and give that table column names that match the attr_accessors of our class.

```
class Song
 
  attr_accessor :name, :album, :id
 
  def initialize(name, album, id=nil)
    @id = id
    @name = name
    @album = album
  end
 
  def self.create_table
    sql =  <<-SQL 
      CREATE TABLE IF NOT EXISTS songs (
        id INTEGER PRIMARY KEY, 
        name TEXT, 
        album TEXT
        )
        SQL
    DB[:conn].execute(sql) 
  end
 
end
```
> why self.create_table? It is not the responsibility of an individual song to create the table it will eventually be saved into. It is the job of the class as a whole to create the table that it is mapped to.
> 

Using the `#save` method makes it easier to insert information into database 

```
class Song
 
  def save
    sql = <<-SQL
      INSERT INTO songs (name, album) 
      VALUES (?, ?)
    SQL
 
    DB[:conn].execute(sql, self.name, self.album)
 
  end
end
```
> For strings that will take up multiple lines in your text editor, use a **heredoc** to create a string that runs on to multiple lines.

> <<- + special word meaning "End of Document" + the string, on multiple lines + special word meaning "End of Document"
> 

**?** characters are placeholders => the SQLite3-Ruby gem's #execute method will take the values we pass in as an argument and apply them as the values of the question marks

#### Giving Our Song Instance an id

```
class Song
 
  attr_accessor :name, :album, :id
 
  def initialize(name, album, id=nil)
    @id = id
    @name = name
    @album = album
  end
 
  def save
    sql = <<-SQL
      INSERT INTO songs (name, album) 
      VALUES (?, ?)
    SQL
 
    DB[:conn].execute(sql, self.name, self.album)
 
    @id = DB[:conn].execute("SELECT last_insert_rowid() FROM songs")[0][0]
 
  end
end
```
At the end of our save method, we use a SQL query to grab the value of the ID column of the last inserted row, and set that equal to the given song instance's id attribute

#### The .create Method

This method will wrap the code we used above to create a new Song instance and save it.

```
class Song
  ...
 
  def self.create(name, album)
    song = Song.new(name, album)
    song.save
    song
  end
end
```

we use the `#save` method to persist that song to the database.

The return value of .create will be the object that we created 
