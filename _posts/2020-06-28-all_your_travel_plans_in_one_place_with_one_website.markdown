---
layout: post
title:      "All your Travel Plans in one place with one website"
date:       2020-06-29 02:22:59 +0000
permalink:  all_your_travel_plans_in_one_place_with_one_website
---


What a week it has been! I swear after this Sinatra project I won't be looking at websites and code the same way ever again. Looking back on all the code I have written for this project and making it all function correctly, it has been one of the most difficult tasks I have ever accomplished in my life, yet one of the most satisfying.

This project, named Travel Planner, lets users make their own profiles and create and keep a record of their own travel plans. Users create their profiles through forms that are from views. These views are generated through restful routes with CRUD actions. As the form for creating a profile gets filled out, the user's information is stored in a data base, enabling them to return to their profile by logging in at another time in order to keep track of all their plans. I will be explaining more of my understanding of views, routes, and some other nuts and bolts of my app. For a more visual approach, similar to my CLI project (Cheesy Laughs), I have created a YouTube [video](https://www.youtube.com/watch?v=TAzPvTJlAsc&feature=youtu.be) to show more of how it works.

Before learning about how restful routes work, I first learned the structure of how a MVC Sinatra application is formed. MVC is of course an acronym. The "M" stands for models which are ruby coded objects that are represented by a class. Through learning how models are structured, I was also able to understand how has_many and belongs_to relationships work with ActiveRecord. In the Travel Planner app, users have many plans and plans belong to users. To illustrate this concept, I coded the models as shown below.

```
class Plan < ActiveRecord::Base
  belongs_to :user
end
```

```
class User < ActiveRecord::Base
  has_many :plans
  has_secure_password 
  validates :username, presence: true 
  validates :username, uniqueness: true 
end
```

By using the key words has_many and belongs_to, ActiveRecord forms relationships automatically.

In the middle of the acronym MVC, "V" which stands for views which are viewable pages the user sees in their browser. Then finally the "C" stands for controllers which are a series of files that have all the routes inside of them containing the logic for the flow of the application. 

To expand upon the concept of the seven restful routes with CRUD (create, read, update, and destroy), I will refer to a few of the following routes I have written in my controllers for my models. The program starts with the ``` get "/signup" do``` route which is located in my user controller. This route is a "read" action and gets the request when the user clicks on the signup link from the home page. Doing this will display the embedded ruby file using the code ```erb :'/users/signup'``` which is the second line of this method. This line represents a view form the user fills out to create their profile by entering their name, a username, and a password which is formed by using HTML. Last but not least, the whole method is closed with an end line.  A snippet of the particular form looks like this:
	 
	 ```<h1>Create Your Profile</h1><form action="/signup" method="POST">
	 <label>Your Name:</label>
	 <input type="text" name="name" placeholder="What do they call you?" required><br><br>```

Another route that I coded was the ```post '/plans' do``` route which goes through a series of if and else statements to "create" a new plan for the user. It ensures the fields for creating a plan through the form are not empty. If they are empty, then the user will be redirected to the same form again to fill it out with a value for each field. If they filled it out correctly the first time, the code will use the create method to put each of the values into the form through params. An example of this would be the following line of code:

```@plan = Plan.create(name: params[:plan][:name]```

Then after the code saves the plan, it will redirect the user to the plans route, which will show the user their new plan.

While creating the project, I tried to make the app aesthetically designed so that users can enjoy the way it looks through HTML. Wanting to make it look good, it was particularly enjoyable to learn how HTML text elements can have placeholders, which can contain pre-written text adding humor to the webpage. In this project, I decided to add some travel song references into the placeholders for the "Create a Plan" form. Here's some examples: 

```
<input type="text" name="plan[name]" id="name" size="30" placeholder="I've got two tickets to paradise..."></input>
<br><br>

<label>Where are you going? </label>
<input type="text" name="plan[destination]" id="destination" size="33" placeholder="Aruba, Jamaica, ooh I wanna take ya..."></input>
<br><br>

<label>How are you going to get there? </label>
<input type="text" name="plan[mode_of_transport]" id="mode_of_transport" size="35" placeholder="It's a bird! It's a plane! It's a travel plan!"></input>
<br><br>
```

I cracked myself up. But in all seriousness, this project gave me a great opportunity to brush up on my online research skills finding HTML options to make a webpage more customized and unique. There were more customizable HTML options than I thought, which reinforces why HTML is such an innovative tool.

All in all, this project took countless hours of my time, endless amounts of my energy, and possibly halved my sleep for the past week. However, the return investment will pay off with a foundation of knowledge I will use in future projects. I improved my skills and I am more confident in my coding abilities. I like the idea of being able to make a database online where people can create accounts, retrieve information, and have it be useful to them in the future.



