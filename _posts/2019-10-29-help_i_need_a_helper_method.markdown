---
layout: post
title:      "Help, I Need a Helper Method"
date:       2019-10-29 20:20:19 +0000
permalink:  help_i_need_a_helper_method
---


While I was working on my Sinatra portfolio project for Flatiron, I found myself writing some of the same lines of code over and over.  I didn't really see anyway to avoid this and, frankly, was just glad things were working and I was moving forward.  When I had my project assessment, my review coach suggested refactoring some of my code into a helper method.

![](https://media.giphy.com/media/4dQxifEBXoD6w/giphy.gif)

For reference, here is a quick summary of the Sinatra project from the curriculum:

> For this assessment you'll be creating a CRUD, MVC app using Sinatra. This app should be a custom app that is created to track something important to you, whether that's your golf club collection, video games, or travel destinations. Essentially, you're building a simple Content Management System (CMS) using the tools you've learned thus far.

My application is designed to allow users to track their kids' toys.  If you don't have kids, I'm sure you've visited the homes of those that do and witnessed first-hand the epic accumulation of toys.  If you have kids - you are aware of the problem.  

Within my Toys Controller, which handles routing all of the  '/toys' domain  requests from the browser, I have the following code:


```
get '/toys/:id' do
    redirect_if_not_logged_in
    @toy = Toy.find(params[:id])
    if current_user.toys.include?(@toy)
      erb :'toys/show'
    else
      flash[:errors] = "Can't find that toy!"
      redirect to '/toys'
    end
  end
```

Several routes within the Toys Controller, four to be precise, contain these specific lines:

```
 if current_user.toys.include?(@toy)
			erb :'toys/some_view'
    else
      flash[:errors] = "Can't find that toy!"
      redirect to '/toys'
    end
```

This is where a helper method can come in handy.

```
helpers do

    def redirect_if_not_user_owned(toy)
      if !current_user.toys.include?(toy)
        flash[:message] = "Toy not found!"
        redirect to "/toys"
      end
    end

end
```

This is the same logic, just seperated into it's own method which will be accessible to everything within the ToysController Class.  My redirect_if_not_user_owned method takes an argument, but since helper methods have access to instance variables (i.e. '@toy'), it isn't strictly neccesary.  I thought it might provide some flexibility in the instance another method doesn't define the instance variable needed.

So refactoring the route with this new helper method looks like this:

```
get '/toys/:id' do
    redirect_if_not_logged_in
    @toy = Toy.find_by_id(params[:id])
    redirect_if_not_user_owned(@toy)
    erb :'toys/show'
  end
	```
	
The helper method allows for much more readability and simplicity than the alternative.  I was able to clean up 20+ repetitive lines.  I took this same approach for the rest of my controllers and feel like my code looks much cleaner.  Give it a whirl if you are feeling tidy.
	
