---
layout: post
title:      "active record method .where cheat sheet "
date:       2020-07-14 01:52:34 +0000
permalink:  active_record_method_where_cheat_sheet
---


Returns a new relation, which is the result of filtering the current relation according to the conditions in the arguments.

#where accepts conditions in one of several formats. In the examples below, the resulting SQL is given as an illustration; the actual query generated may be different depending on the database adapter.

string
A single string, without additional arguments, is passed to the query constructor as an SQL fragment, and used in the where clause of the query.

Client.where("orders_count = '2'")
# SELECT * from clients where orders_count = '2';
Note that building your own string from user input may expose your application to injection attacks if not done properly. As an alternative, it is recommended to use one of the following methods.

array
If an array is passed, then the first element of the array is treated as a template, and the remaining elements are inserted into the template to generate the condition. Active Record takes care of building the query to avoid injection attacks, and will convert from the ruby type to the database type where needed. Elements are inserted into the string in the order in which they appear.

User.where(["name = ? and email = ?", "Joe", "joe@example.com"])
# SELECT * FROM users WHERE name = 'Joe' AND email = 'joe@example.com';
Alternatively, you can use named placeholders in the template, and pass a hash as the second element of the array. The names in the template are replaced with the corresponding values from the hash.

User.where(["name = :name and email = :email", { name: "Joe", email: "joe@example.com" }])
# SELECT * FROM users WHERE name = 'Joe' AND email = 'joe@example.com';
This can make for more readable code in complex queries.

Lastly, you can use sprintf-style % escapes in the template. This works slightly differently than the previous methods; you are responsible for ensuring that the values in the template are properly quoted. The values are passed to the connector for quoting, but the caller is responsible for ensuring they are enclosed in quotes in the resulting SQL. After quoting, the values are inserted using the same escapes as the Ruby core method +Kernel::sprintf+.

User.where(["name = '%s' and email = '%s'", "Joe", "joe@example.com"])
# SELECT * FROM users WHERE name = 'Joe' AND email = 'joe@example.com';
If #where is called with multiple arguments, these are treated as if they were passed as the elements of a single array.

User.where("name = :name and email = :email", { name: "Joe", email: "joe@example.com" })
# SELECT * FROM users WHERE name = 'Joe' AND email = 'joe@example.com';
When using strings to specify conditions, you can use any operator available from the database. While this provides the most flexibility, you can also unintentionally introduce dependencies on the underlying database. If your code is intended for general consumption, test with multiple database backends.


