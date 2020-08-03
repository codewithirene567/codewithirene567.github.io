---
layout: post
title:      "Find an Animal and give It Some Love! - Rails Project"
date:       2020-08-02 16:53:26 -0400
permalink:  find_an_animal_and_give_it_some_love_-_rails_project
---

If I thought Sinatra was difficult to learn and use, then that makes the task of learning, then using Rails an ultra-challenge! Yes, it can be magical as it provides more abstraction for code and does automate a lot of the tediousness for the developer using it, but with all of that comes a bunch of new features. These new features can make it harder to solve software bugs because developers sometimes need to understand what things are running in the background, let alone learn them which is a challenge in itself. However as usual, I can't deny it, like any software project from scratch that I've done, making this project was stressful yet a whole lot of fun. My competence in coding has never been at such a high level through all the struggles in creating this project.

For this project, I called it Find Your Animal Today which is a Rails app that lets people either create their own animal and associate the animal with a reason they can come up with or it lets them add a reason why they like that animal to another animal someone else has already created within the database.

The idea for creating this app came from the fact that similar to a lot of people, I have always loved animals, especially my own pets, so I figured this silly yet useful idea of a website would make it easier to keep a positive attitude when the software bugs became tough to solve.

I learned a whole lot as mentioned earlier in the process of creating it, but the two main concepts I learned better are the idea of using path helpers for routes and understanding form helpers with Rails, in particular form_for. Additional honorable mentions of concepts I have really brushed up on understanding include how to use the pry gem more effectively to my advantage to find out what code returns and how to solve undefined object errors.

Path helpers in rails makes readability easier for developers to understand/read their routes. For instance, using ```link_to "Press here to make your profile", new_user_path``` versus ```<a href="/plans/new">Click here to create a new plan</a>, get "/plans/new"```.

Routes of course are parts of a Rails application that give the url value which permits places or views a user can go to in a website through links to connect these pages. Allow me to break this down into steps in terms of how this flows when the user clicks on either of these links.

First take a look at the link someone used to click on in order to make a new plan with the regular HTML:

```<p><a href="/plans/new">Click here to create a new plan</a></p>```

Then the next step of where the program looks to execute this link. Notice how the request goes directly through the plans controller, then goes through the if and else statement.

```
class PlansController < ApplicationController

   get "/plans/new" do
       if logged_in?
        erb :'/plans/new'
      else
        redirect to '/login' 
      end
    end
```

**versus**

Here again is the first step of a user clicking a link to create a new resource except for in this Rails project it looks like this:

```<%= link_to "Make a new animal and assign a category to it", new_animal_path %>```

The second they click on the link, the link_to will let the request go to the ```new_animal_path``` which is a helper method that uses the config/routes file automatically behind the scenes. Writing ```new_animal_path``` reads a lot simpler than having to read ```href=this``` and then follow more logic in the controller.

Let's take a look at the config/routes file to find out where new_animal_path is being represented. By writing this line in my config/routes folder:

```resources :animals```

The line is creating all the routes automatically for the animal object through the resource route through RESTful conventions (CRUD), which includes the route that makes a new animal object which looks like the line of code below, without me having to write this GET route directly.

```new_animal GET  /animals/new(.:format)  animals#new```

At this point the code is running the "new" action in the Animals controller file, which looks like this.

```def new
        @animal = Animal.new
end```

So to summarize with the ```link_to``` format, the link is basically saying, when I am clicked, take me to the ```new_animal_path``` which represents a route that runs in the config/routes folder, through the resource route for animals. After that the resource route is found using the keyword "new" before animal in ```new_animal_path```, and run the action in the animals controller because ```animals#new``` is at the last part of the GET request route.

Although when I explain everything, the Rails way in terms of how link helpers work seems more complicated, in reality it is not from the developer's perspective and this is because Rails does a lot of the work for us with us writing less code.

From my experience, it seems forms are essential for any general web applications as they allow users to store data they submit into the data base. As developers, it is our job to create these forms. Form helpers simplify the form creating process that I've used in the past during my time at Flatiron. In this post though I will be covering the concept of ```form_for``` versus a regular HTML form I used in Sinatra in addition to explaining how ```form_for``` is a better method to create a from.

Both the forms I pulled from both projects represent views that users would see when creating a new resource. In my Rails application they are creating an animal, but in my Sinatra application they were creating a travel plan.

The form from my Sinatra project; a regular HTML form:

```
<form action="/plans" method="POST">

<h1>New Plan</h1><br>

<label>What is it called? </label>
<input type="text" name="plan[name]" id="name" </input>
<br><br>

<label>Where are you going? </label>
<input type="text" name="plan[destination]" id="destination" </input>
<br><br>

<label>How are you going to get there? </label>
<input type="text" name="plan[mode_of_transport]" id="mode_of_transport" </input>
<br><br>

<label>What day? </label>
<input type="text" name="plan[date]" id="date" ></input>
<br><br>

<input type="submit" value="Make Plan">
</form><br>
```

**versus**

The form from my Rails project; which really is a HTML form, but with a Rails helper ```form_for```:

```
<h1>A new Animal and any additional comment about them:</h1>

<%= form_for(@animal) do |f|%>
    <%= f.label :name%>
    <%= f.text_field :name %><br><br>
    <%= f.label :comment %>
    <%= f.text_field :comment%><br><br>
    <%= f.label :category_id %>
    <%= f.collection_select :category_id, Category.all, :id, :value %>
    <% if @animal.errors.any? %><br><br>
<%= f.submit %>
<%end%>
```

After viewing both of these it is obvious which one is easier to read and use. That's the beauty of Rails, it simplifies certain processes so effectively.

For starters, look at how it is not needed for developers to define an action for where the form is submitting to ```<form action="/plans" method="POST">``` versus ```<%= form_for(@animal) do |f| %>```. With Rails, the ```form_for``` method already knows that we want to use the POST verb to create an instance of an animal and assign it to a category. While in the Sinatra form, we need to define the HTTP verb and give it an action through the controller.

Another thing to note is how the fields became simplified in this new form. Through using ```form_for```, I learned Rails creates a FormBuilder object which lets Rails iterate over all the instances of the FormBuilder object as a parameter in this block of code. In other words, ```f.text_field``` is an instance of the object to provide a field for an assigned attribute from the model object, in this case an animal. Which means I only need to write ```<%= f.text_field :name %>``` instead of the longer way of making a label tag on both sides like so: ```<label>What is it called? </label>``` then having to put an input tag in addition to defining every HTML part inside: ```<input type="text" name="plan[name]" id="name" </input>```. ```Form_for``` is writing all of this for developers behind the scenes through the Rails framework.

Although it was difficult to complete, this project educated me and gave me much needed experience in coding through plenty of trial and error. Like I mentioned earlier, through all the difficulties in making it flow, it was still an overall joy to make it come to life through a browser. This project allowed me to understand more of how Rails is structured besides what I learned about the idea of an MVC application structure earlier. A critical part of understanding Rails is that the Rails framework relies on convention over configuration. To put it differently, through following this concept, Rails will automate some processes for you by using the path helpers and form helpers but in order to solve errors for these two helpers in your code, it is important to know what is really happening in these automated processes.

Besides the actual Rails concepts though, through my appreciation of animals, I really liked making a website with the purpose of managing the data of animals and their reasons for why people like them all in one site. Of course after this whole crazy wonderful project was over, I went over and gave my dog an oversized hug and I suggest you do the same if you have an animal. Just don't go hugging animals you see out in the wild, you might come to regret it if they don't have reasons for liking you in their own mental database.

