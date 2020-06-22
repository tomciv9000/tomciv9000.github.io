---
layout: post
title:      "A Virtual Stroll Down Memory Lane "
date:       2020-06-22 19:19:57 +0000
permalink:  a_virtual_stroll_down_memory_lane
---




I’ve been stuck inside, along with the rest of the responsible world, for the better part of three months.  Looking out of the same windows, pacing down the same hallway, staring at the same walls, I found myself asking the same question over and over.

“How did did I get here?”

How did I get from Andrews, Texas to Woodside, Queens?  How did I get from a little boy who wanted to be a “breakdancing army soldier” to a nearly 40-year-old man who is finishing a software development program, trying to make sure his two-year-old daughter doesn’t put her toys in the potty.  How does the starting point of my life connect to the current moment?  If I were to plot all the important moments in my life, where I was and what I remember about a specific time, would that give me some insight into the original question - how did I get here?  I had the time to find out.

So I built a virtual memory lane.  It’s called Stroll.  Using React Redux and integrating that with Google Maps API, I built an application that allows the User to explore the places in their life that have helped shape who they are today.  By first creating Places (e.g., “Cleveland”) and then creating Spots (e.g., “The Rock and Roll Hall of Fame”), the User is taken to a GoogleMap Streetview to explore the area and record any relevant memories.  All of this data is stored on a Rails API backend with a PostgreSQL database.

This project is so different from anything else I’ve built during my time at the Flatiron School in the sense that it feels more like a personal exploration than a practical application.  I wanted to challenge myself to build something that connected the User to a sense of self, a place of reflection. 

There are so many features that I’m proud of in Stroll.
* JWT Token Based User Authentication
* Protected Routes with a custom Auth component
* GoogleMaps API Integration through the application
* Using ClusterMarkers to provide a sense of the areas where a User's memories are concentrated.
* A map that provides a view of all the spots a User has created.
* Dropping the user directly into StreetView after entering a spot.
* Centering the map based on relevant User data.
* Using GoogleMap’s Autocomplete to connect User input to Google Places.
* CRUD functionality with all resources: Users, Places, Spots, and Memories.
* Using Bootstrap-React framework as a foundation for the UI, and then customizing much of the visual elements to craft a unique interactive experience.
* Responsive background with multiple images depending on screen size.
* Animated buttons with a unified color scheme
* Validations on both the front-end and back-end, including helpful error messages on forms and real-time reminders (e.g. “Password must contain a digit”) that respond to what the User is typing at that moment.

As you’ll read in most final project blogs, this was a huge undertaking and took me well over a month to complete and it is by no means complete.  It’s a step, but a really big one.  This 18-month journey has really shaped me in a lot of ways, but what I will take away most from this experience is how powerful learning can be, especially after you’ve completed school and been out in the world for awhile.  So often we forget to learn, to open ourselves up to the idea that we don’t know everything we need to know.  

It’s time to evolve.  It’s time to listen.  And goddamnit, it’s always time to learn.

