---
layout: post
title:      "What's Playing at the UCB : My CLI Data Gem Project"
date:       2019-07-18 16:07:24 +0000
permalink:  whats_playing_at_the_ucb_my_cli_data_gem_project
---


This was such a mountain to climb.  I know I am not the only one in this boat, but trying to gain a strong foothold in conceptual understanding while taking care of a one-year-old is a TASK.  For so long, I've been feeling two steps forward, three steps back.  I work full time at night.  I am Daddy full time during the day.  In between my daughter's naps and in the wee hours of the morning is when I find time to code.  The fact that I have reached any level of understanding of Ruby concepts, let alone enough to build this project, is a damn miracle.

After several months of grinding, I arrived at the CLI Data Gem Portfolio Project.  All of the lessons and labs prior allow you to reach out to the school for support.  Not the portfolio projects.  It was so intimidating to be staring at a blank screen, cursor blinking, not knowing where I would even begin to start and not able to rely on a lesson plan or instruction sheet.  I was on the verge of a panic attack for a week.

So I took a vacation and didn't work on anything Flatiron related for ten days.

When I got back, I felt a sense of renewal and new sense of confidence in my ability to complete the [Project Requirements](https://learn.co/tracks/full-stack-web-development-v7/object-oriented-ruby/final-projects/cli-data-gem-portfolio-project) I knew I would want to be interested in the data I was scraping, so I chose a passion of mine, the Upright Citizens Brigade.  The UCB Theaters are some of the most influential and renowned improv comedy theaters in the country.  I had the privilege of being a performer there for several years and one of my favorite things about being a performer was the fact that I could see other shows for free.  Since there are four different theaters (two in LA, two in NYC) and they each have a separate website, I would have to go to multiple sites to see what was playing that night.  I thought it would be great to have my CLI Data Gem scrape all four theater sites and compile that data in an easy-to-read OO Design Ruby Gem.

Before starting, I made sure to review a lot of the concepts that still seemed fuzzy to me.  Re-completing some lessons and digging into the examples that Flatiron provided was very helpful, but I still had to do a ton of googling and asking peers to fully wrap my head around how I would go about writing this code.  Someone recommended I practice "rubber ducky debugging", trying to explain my code to an inanimate object to help my brain process what I had written.  More than anything, that is what got me through this project.

The program itself is fairly straightforward.  When called, it immediately builds four instances of the Venue class, representing the four theaters.  Each venue has a name, a url, and can have many shows.  When presented with the four venues, the user selects the venue for which they'd like to see show listings.  When the venue is selected, the program first checks to see if that venue's show array is empty - if so, that theater's website is scraped and that data is used to create Show class objects, which are assigned to the appropriate Venue class object.  If the show array remains empty after the scrape, a message is given that "There are no shows at that theater tonight."  Otherwise, the listings for that venue are presented and the user can select a show for more information.

Initially, I had all four sites scraped when the program started, but through some feedback, I discovered it was more streamlined to do that only when needed and then store it as a variable, rather than re-scrape, that can be accessed if the user goes back to the same venue.

Some of the more helpful features of the CLI include being able to see the status of a show (sold out, tickets available), an in-depth description of the show, and practical properties like time and cost.

The icing on the cake was being able to play around with colorize towards the end of writing the code.

I am so proud of myself for getting this far and am truly excited to move forward with the confidence that I can do this.

