---
layout: post
title:      "Who's Damn Toy Is This?"
date:       2019-10-27 15:11:38 +0000
permalink:  whos_damn_toy_is_this
---

> "This app should be a custom app that is created to track something important to you."

I have a daughter.  She is a toddler.  She is only one tiny person, but somehow has accumulated what feels like thousands of toys.  Half of my apartment is toddler toys.  The other half - infant toys that she no longer plays with, but still somehow have found permanent residence in our home.  Many of these toys were gifts from family or purchased at special milestones that have sentimental value to us.  But there are...so...many...toys.  When I read the description of what this portfolio project was asking you to do, track something important to you, the first thing that came to mind was a toy tracker, a way to manage the different toys your child can accumulate.

For reference, here are the requirements of the project:

* Build an MVC Sinatra application.
* Use ActiveRecord with Sinatra.
* Use multiple models.
* Use at least one has_many relationship on a User model and one belongs_to relationship on another model.
* Must have user accounts - users must be able to sign up, sign in, and sign out.
* Validate uniqueness of user login attribute (username or email).
* Once logged in, a user must have the ability to create, read, update and destroy the resource that belongs_to user.
* Ensure that users can edit and delete only their own resources - not resources created by other users.
* Validate user input so bad data cannot be persisted to the database.
* BONUS: Display validation failures to user with error messages. (This is an optional feature, challenge yourself and give it a shot!)

Before typing any code whatsoever, I thought it would be helpful to diagram  my model relationships.  I created a [gliffy](https://www.gliffy.com/) account and attempted to draw the relationships in a similar fashion to what I've seen on some of the codealongs, but all my diagrams ended up looking like poorly drawn stick-houses and were not helpful in the least.  So I went with the tried-and-true method of ripping a piece of paper out of my notebook and grabbing a nearby sharpie.

![Probably ends up in the Smithsonian ](https://photos.app.goo.gl/Jt5Ri4dnN1Kaojt79)

Here we are.


