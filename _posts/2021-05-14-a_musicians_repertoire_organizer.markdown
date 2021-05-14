---
layout: post
title:      "A Musician's Repertoire Organizer"
date:       2021-05-14 15:41:38 -0400
permalink:  a_musicians_repertoire_organizer
---


This little Sinatra application allows the user to keep track of the musical works in their repertoire, and view them by period and type. This is a necessary task in my other life. I have a repertoire list posted on promotional websites, and when selecting a performance program I can build a themed concert, or just a varied and interesting concert of music. It is also helpful for study and reflection - are there any gaps in my repertoire or areas of interest that I have yet to explore? This is an MVC, CRUD app.

I quickly generated a basic architecture for my app using the [Corneal](https://github.com/thebrianemory/corneal) gem. This built the necessary files and even fills out the environment, gemfile, and config.ru. It also makes a basic layout page, which I only scarcely edited in my haste to churn this app out.

From there I started making my database and migrations. I needed a table for users, of course, and compositions. But how to organize them? These lists are usually presented by category. You can have lists by time period: Renaissance, Baroque, Classical, Romantic, and Contemporary. But are pieces from 1920 really contemporary? Not so much, so I added 20th Century as a separate category. Repertoire is also organized into the follow List Types: Solo pieces, Chamber music, and Concertos. All these categories are standard, so I seeded in the time periods and gave the use limited choices. My tables are as follows:

**User**
* name
* password_digest (encrypted with bcrypt)

**List_types**
* name
* user_id

**Era**
* name

**Compositions**
* title
* composer
* instrumentation
* list_type_id
* era_id

This makes for some slightly complex associations, but hey let's do it right! The User has many ListTypes, and through those has many Compositions. The Compositions belong to the ListTypes, but also to an Era. The User does not interact with the Era model at all, except to add Compositions to it. CRUD operations are performed on Compositions, but the ListType also has a "show" page. There are, then, four controllers:
* ApplicationController to get things started, contain the helper methods
* UserController for signing up, logging in and out, and viewing a personal home page
* CompositionController with all the CRUD actions
* ListTypeController that displays lists of pieces by solo works, chamber music, and concerto categories.

Users sign up, and when logged in are tracked with two helper methods: #logged_in? and #current_user. The user, once signed up, can add compositions. Upon creation, compositions are assigned to a list type, which is created for the user if it did not already exist. This means that the "list_types" table may have a "solo" list for every user, all with the same name but differentiated by user_id. 

The "compositions/new" page was fun to build. Not only was there a complex *params* hash, but I used three different input types in the form: a dropdown select menu for the list type, text input (for title, composer, and instrumentation), and checkboxes for the time period. Although it took a long time to build, doing so make the editing page and route so much easier!

Overall, this was a great exercise, and it made me realize how much I need to build and edit things over and over if I am to retain things from the curriculum. 

**Things I should remember or would like to extend in my app:**
* If I had a nickel for every time a forgotten "/" caused Sinatra to forget his song...grr
* I was not able to find a way to preselect the list type in the dropdown of my edit page
* It would be nice if the composer name input was standardized with last name and first name fields. This would allow lists to be organized alphabetically by composer, and maybe to search by composer. I admit, I was trying to crank this thing out without creating a search engine or a library catalog system.





