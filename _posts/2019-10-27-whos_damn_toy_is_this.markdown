---
layout: post
title:      "Who's Damn Toy Is This : My Sinatra Portfolio Project. "
date:       2019-10-27 11:11:39 -0400
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

![Imgur](https://i.imgur.com/9JIWFSmb.jpg)


Being able to have a visual representation of my model relationships was truly helpful in wrapping my head around how to approach coding this project.  My initial models were:

* User 
* Kid 
* Toys
* Manufacturer
* Types

Describing the idea to my wife, she told me that something that might be helpful would be development stages as opposed to manufactuers.  She explained she doesn't really care about who makes the toy and so many toys don't have a manufacturer listed or are hand-me-downs where we just don't know who made it.  Linking a toy with a development stage is helpful as you would be able to compare it with the development stage of your child.  

I won't go into detail about it in this post, but I eventually ran problems having a "Type" model as that language became confusing for Activerecord.  I decided Category was a much better label for that class.

This led to my final models of:

* User (name, email, secure password)
* Kid (name, development stage)
* Toy (name, development stage, categories)
* Stage (name)
* Category (name)

After building my model classes, I wrote migrations to create the appropriate tables.  My diagram of relationships came in handy at this point and I was able to understand that:

* A User has many Kids.  A User also has many Toys through Kids.
* A Kid has many Toys and belongs to User.  A Kid also belongs to a Stage.
* A Stage has many Kids and many Toys.
* A Toy belongs to a Kid, belongs to a Stage, and has many Categories.
* A Category has many toys.

I was able to see where I had a many-to-many relationship and needed to create a join table (toy-categories) as well as use Toys as a join for Users and Kids.


*A quick note on Stage and Category.  I initially played around with the idea that Stages and Categories would be able to be created by a User, but ultimately decided against it.  I wanted a standard set of development stages that most caregivers would recognize and for that same reason I wanted a standard set of Categories that are used most frequently.  It seemed like a smoother, more streamlined experience for the user (and also probably the programmer).
*

I quickly setup my environment, thanks to the "Sinatra App From Scratch" video lesson which walked me through a lot of the basics that are taken care of in the labs and codealongs.  Once the environment looked good, I ran 'tux'.

**Run tux, run tux, run tux.  This was arguably the most helpful thing during this entire project.  Having a really solid grasp of how your objects are created and their interconectively was invaluable at all stages of this project.**


Building the Controllers and Views was really enjoyable after building out my model relationships, which felt like a massive brain teaser (the not-fun kind.)  I looked at a few example projects and saw that several of them used [Bootstrap](https://getbootstrap.com/).

> Bootstrap is an open source toolkit for developing with HTML, CSS, and JS. Quickly prototype your ideas or build your entire app with our Sass variables and mixins, responsive grid system, extensive prebuilt components, and powerful plugins built on jQuery.
> 

I had to google every damn word of the above paragraph.  Not really, but I didn't know anything about Bootstrap and had to look up what half of these features actually did .  Many of them didn't seem neccesary (to my limited understanding and ability) to accomplish I was trying to do, but Bootstrap did seem to offer a visual template that looked clean and simple.  It also had some[ typography settings](https://getbootstrap.com/docs/4.3/content/typography/) that I thought looked sharp.  I made a note that it seems like a great tool for building a responsive grid-container view, but for the sake of time, I didn't think that was needed.  I recommened checking it out as you approach your project.  Their documentation is fantastic and really easy to follow. 

Most of my work with controllers and views went smoothly as this felt like habit after many of the lessons leading up to this.  If I had a question, I found myself going to documentation rather than re-reading a lesson or reaching out to friends.  Making documentation my friend is something I am happy to have accomplished during this lab, maybe more than anything else I did.

When my application seemed to be functioning as I had hoped, I moved on to the final piece, **validation**.  Within my controllers, I had built several methods that would check to see if a user's input was valid and therefore proper to be persisted into the database.  For example, this is the post '/toys' route from my ToysController:

```
post '/toys' do
    if logged_in?
      if params[:toy][:name] == "" || !params[:toy][:stage_id] || !params[:toy][:kid_id]
        redirect to "/toys/new"
      else
        @toy = Toy.new(params[:toy])
        if @toy.save
          redirect to "/toys/#{@toy.id}"
        else
          redirect to "/toys/new"
        end
      end
    else
      redirect to '/login'
    end
  end
```


You can see I am manually check to see if the :name string isn't a blank string, if there is an associated stage_id as well as an associated kid_id. 
```
if params[:toy][:name] == "" || !params[:toy][:stage_id] || !params[:toy][:kid_id]
```
I knew I would eventually want to move this logic from the controller to the model, but I wasn't exactly sure how to go about it.  I found documentation on [Active Record Validations](https://guides.rubyonrails.org/active_record_validations.html#validations-overview) and discovered several resources that helped me shift the responsibility for validation over to the models and away from the controllers.  I'm including a passage that gives a great overview below:

> There are several other ways to validate data before it is saved into your database, including native database constraints, client-side validations and controller-level validations. Here's a summary of the pros and cons:
> 
> * Database constraints and/or stored procedures make the validation mechanisms database-dependent and can make testing and maintenance more difficult. However, if your database is used by other applications, it may be a good idea to use some constraints at the database level. Additionally, database-level validations can safely handle some things (such as uniqueness in heavily-used tables) that can be difficult to implement otherwise.
> * Client-side validations can be useful, but are generally unreliable if used alone. If they are implemented using JavaScript, they may be bypassed if JavaScript is turned off in the user's browser. However, if combined with other techniques, client-side validation can be a convenient way to provide users with immediate feedback as they use your site.
> * Controller-level validations can be tempting to use, but often become unwieldy and difficult to test and maintain. Whenever possible, it's a good idea to keep your controllers skinny, as it will make your application a pleasure to work with in the long run.
> 
> Choose these in certain, specific cases. It's the opinion of the Rails team that model-level validations are the most appropriate in most circumstances.
> 

With the model handling the validations, my classes began to look like this:

```
class User < ActiveRecord::Base
  has_secure_password
  has_many :kids
  has_many :toys, :through => :kids
  validates :username, :email, presence: true
  validates_uniqueness_of :username
end
```

and this:

```
class Toy < ActiveRecord::Base
  belongs_to :kid
  belongs_to :user
  belongs_to :stage
  has_many :toy_categories
  has_many :categories, :through => :toy_categories
  validates :name, :stage, :kid, presence: true
 end
```

In the first example, the User Class, the line:
```
validates_uniqueness_of :username
```
ensures that no two users can have the same name.  It will not allow a User object to be persisted to the database without ensuring that the username attribute is unique. 

In the second example, the Toy Class, the line:
```
validates :name, :stage, :kid, presence: true
```
requires that a object of the Toy Class contains a name, a stage, and is assigned to a kid.  Again, it will not allow an improper object to be persisted into the database.

I went through all objects that could be created by the user and made sure that any data that was to be persisted underwent some type of validation.  Using this approach also allowed me to reach into the validation errors that would be created in the instance that something was invalid.  Returning to the Toys Controller:

```
  post '/toys' do
    redirect_if_not_logged_in
    @toy = Toy.new(params[:toy])
    if !@toy.valid?
      flash[:errors] = @toy.errors.full_messages
      redirect to "/toys/new"
    else
      @toy.save
      flash[:message] = "Successfully added toy."
      redirect to "/toys/#{@toy.id}"
    end
  end
	```
	
After checking to see if the new object is valid, I am able to take  invalid objects and store their error messages into a  hash and then return those error messages into the view using the gem 'rack-flash'.  From my layout.erb :

```
<% if flash[:errors] != nil %>
    <div class="error message">
      <% flash[:errors].each do |msg| %>
      <mark><%= msg %></mark><br>
      <% end %>
    </div>
  <% end %>
	```
	
There is so much more I could cover with regards to what I learned completing this project.  Once again, I am filled with a sense of accomplishment and progress having navigated uncharted territory and come out the wiser.  
	
	



