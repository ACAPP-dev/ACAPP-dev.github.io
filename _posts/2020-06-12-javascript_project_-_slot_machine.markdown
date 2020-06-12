---
layout: post
title:      "JavaScript Project - Slot Machine"
date:       2020-06-12 23:30:08 +0000
permalink:  javascript_project_-_slot_machine
---


My fourth class, JavaScript, focused on the front end user experience. So for my project I chose to make a game - a slot machine - with better odds so the player will generally win. I used Ruby on Rails to provide an interface to a database, but the focus was on the user experience so most of the work went into providing front end functionality (the slot machine).

Features of my slot machine include the ability for a user to create an account and for returning users to log in and retrieve their prior balance. Once logged in, users can make pretend deposits and withdrawals, adjust the bet amount, 'spin' the slot machine (with bets deducted from and wins added to the user balance), view their last five transactions (deposits and/or withdrawals), and view a win payout table.  An updated user balance is persisted to the database after each spin.

Since making a game was a completely new experience, I had a tougher time outlining a detailed design. Instead I focused on the features I wanted my slot machine to have and then just jumped in and started coding the features one-by-one. I ended up spending much more time in trial and error as a result.  However, this should get much easier as I get more experience working with these types of projects.

One design issue I faced was how to persist the results of the slot machine games to the database.  I originally thought to persist each win or loss to the transactions table with the user balance a sum of all transactions. However, this adds complication (lots of transactions) and is error prone. I also thought about just saving the net win or loss each time the user quits the current session, but what happens if the user just closes the window?  My final choice was to persist the updated user balance to the database after each spin.  I feel like this was a balanced solution and kept the code reasonably simple.

Making the layout of the slot machine in HTML and styling the elements with CSS was also challenging. This is mostly the result of the relatively complicated functionality. One thing I had to get more comfortable with is using lots of <div> elements so that I can identify and change things with JavaScript.

The most challenging part of the project was coding the spin functionality in JavaScript. I had to use timers to get the images to 'spin' and to make sure the results didn't appear too soon.  I used the setTimeout() function in a couple of places in order to (1) slow down the appearance of each image in the reel, and (2) delay appearance of the results until all spins were finished.  My approach to timing the events included the following steps:

<ul>
<li>Identify the starting and ending (winning) images</li>
<li>Create an array of all images for each reel (total of 3 reels)</li>
<li>Start spinning all three reels using a 150 millisecond delay for each image</li>
<li>Delay the remaining steps until the 3rd reel (longest spinning reel) is finished</li>
</ul>

The delay of the final steps was accomplished using the setTimeout() function to delay 150 milliseconds times the number of images in the array for the 3rd reel:

> window.setTimeout(() => { code for remaining steps... }, (reel3SpinArry.length + 2) * 150)

There were many other challenges to overcome including displaying and hiding forms, coding objects for the images, user, and game, and coding the fetch calls to Rails.  However, with lots of trial and error I was able to make everything work. I'm pleased with my progress so far and feel that I've learned a lot. JavaScript is tricky and challenging to learn, but interesting as well.  I'm looking forward to my final class with Flatiron Academy which is also JavaScript related.
