---
layout: post
title:      "Second Project - Sinatra Family Tree Web App"
date:       2020-02-13 21:36:48 +0000
permalink:  second_project_-_sinatra_family_tree_web_app
---


Hello!  My project review from my first class went well and I’m happy to say that I was able to progress to my second class.  It is now mid-February 2020 and I’m getting ready for another project review.

In my second class, I really enjoyed learning some new subjects including databases, the Ruby Active Record Gem, and the Ruby Sinatra Gem.  We learned how to use Ruby to write fully functioning web applications that include a database, backend logic, and web pages that can accept user input as well as display data.  I like that we continue to use Ruby which expands my Ruby knowledge as well as gives me practice with our previous concepts.

Now about my project...

Our project requirements were to build a functioning web application that allows a user to securely create, read, update, and delete a collection of items.  I chose to make a family tree web application that is a collection of families and family members.  Little did I realize how complicated this choice would be!

I had to first design the structure of the database (and associated models).  There were many questions about how this might work:

* Do I associate family members with the user? What happens if another user adds family members?

* How do relationships work? Do I have daughters, sons, cousins, grandparents, etc.?  That is a lot of relationships to manage!

* What happens if I have more than one family I want to work on?  My family, my girlfriend's family, my dog's family, etc.

This is more complicated than I initially expected!  After experimenting with a few different options, I decided on the following setup:

1.	A user can have many families.
2.	Families can have many family members, but a family member can only have one family.  This is known as a has many / belongs to relationship.
3.	Families can also have many users.  This is known as a many to many relationship that requires a special join table.  I created a separate join table called userfamilies to accomplish this.
4.	Family members can have many relationships, but this is currently limited to four options: wife, husband, mother, father.
5.	Family members can have many related family members through relationships.  This was more complicated to set up as the related family member is also a regular family member.  However, the solution is quite simple in Active Record. 

Just modify the Familymember model has_many relationship with a custom class_name as follows:

       has_many :related_familymembers, class_name: “Relationship”

I then put the following belongs_to statement in my Relationship model:

      belongs_to :related_familymember, class_name: “Familymember”

Now that I had the tables and models set up, I needed to set up my forms.  This got complicated at times because I needed to provide a list of relationships and available family members as well as save these associations.

I used select tags in my family member forms to provide this list of family members and quite a bit of logic to iterate through each relationship and identify the related family member.  

For example, on my family member listing view (index):

1.	Iterate through each family member: `<% familymembers.each do |member| %>`
2.	Iterate through each relationship: `<% member.relationships.each do |relationship| %>`
3.	Show related family member info (name, etc.): `<%= relationship.related_familymember.first_name %>`

It took me some time to code this all out and create the web pages (views).  I experimented with html and css to create a navigation bar and nicer formatting as well.  It was great practice and I enjoyed the chance to be creative.

I continue to enjoy learning Ruby and I'm excited to be developing working web applications now.  Our next class is a further extension of Ruby: Ruby on Rails.  I'm looking forward to starting this class after our Spring Break.

If you would like to check out my project, you can review the code here at [Github](https://github.com/ACAPP-dev/familytree.git).








