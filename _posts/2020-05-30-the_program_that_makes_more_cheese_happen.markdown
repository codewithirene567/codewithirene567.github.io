---
layout: post
title:      "The Program that makes more "Cheese" happen"
date:       2020-05-30 12:18:42 -0400
permalink:  the_program_that_makes_more_cheese_happen
---


It is nearly the beginning of June and I have finally finished my CLI Project at Flatiron's Software Engineering Bootcamp. It's been a rough ride figuring out how to get this whole thing to run smoothly, but what I can say is I have confidently learned, then applied some valuable concepts along the way in terms of how a CLI application looks like.

My CLI app is called Cheesy Laughs which is an app that people can use whenever they don’t feel happy and need a pick me up. It generates customizable jokes based on three predestined categories of jokes to choose from. One feature I particularly like about this app is that it sort of has a personality of its own in that it is determined to give out the requested number of jokes no matter what the user tries to do. You can watch my [video](https://www.youtube.com/watch?v=tVnTLg6_WqY) to see it in action.

Here are the concepts I mentioned earlier that I have learned and applied:

**How a CLI app is structured in terms of the files that make it work**
 
   I started building the app by first creating an environment class that will be the basepoint where all the other code classes "talk" to each other. The classes were listed as follows with a path to trace back to which folder they were coming from. In this scenario they were coming from my lib folder.

```
- require_relative "./lib/jokes"
- require_relative "./lib/api"
- require_relative "./lib/cli"
```

  In addition to the classes being listed, I also wrote code to require which gems will be used.
	
```
- require 'net/http'
- require 'json'
```

  Then I created an executable file in my bin folder which lets me run the program in the first place. Specifically in this project this file is going to require the environment file to get everything set up like so...
	 
	 
`require_relative '../environment'`
	 
	 
 ...and then set a variable of each instance in the CLI class to be equal to a new instance. Then call the start method from the CLI class on each cli_instance.
	 
	 cli_instance = CLI.new
	 cli_instance.start
	 
 As shown above each of the classes are in the lib folder. I have the first class as my API class and its purpose is to make calls to the API which is a series of jokes from an internet page. Then it will turn the URL into an object, and use the JSON parse method to turn everything into a ruby hash set up to make everything more readable. This way I could pull what I wanted from the database easier. After refactoring, I've consolidated this class body into one method which passes in an argument about the type of joke the user will hear which will be defined in the CLI class.

 My CLI class is next and this class's responsibility is to basically show how my application is going to run and use the method from the API class to give the "type" argument value. It shows the flow of what the user is going to see including a greeting message, logic of how it runs, and pulls the jokes from the Jokes class in order to set each joke instance to be used in the logic itself.

 This leads to the last class defined which is the Jokes class. This method is going to keep track of the joke attributes from the API's hash of jokes and will save all the jokes that are created. It iterates over all the jokes and defines which type of joke is called on each instance.
	 
 ```
def self.jokes_instance(type)
    all.select do |joke_instance|
      joke_instance.kind == "#{type}"
      end
```
			
**How to refactor code**

Another key concept I learned was how to refactor code and the "why" behind it. As programmers it pays off to have our code as abstract, yet short and simple as possible in the process. If something is repetitive then the code is longer than it has to be. By the term abstract, I mean condensing code into one complex idea in a way that makes the code run smoother and shorter. An example from my project would be most helpful in explaining this. 

There are three categories of jokes within this app. With that in mind in my API class, I originally wrote my code with three different methods to do the same process for each category. The problem with this code is it doesn't have to be written three times for it to work. To shrink the code, the first thing I did was recognize which lines of code are the same  in the three methods and copy and paste that into a new method after naming that method something general for all categories.

Next I used string interpolation around the joke's type within each URL because each one was exactly the same except that their joke type was different.

I turned these three URLs from three different methods...

```
url = "https://official-joke-api.appspot.com/jokes/programming/ten"

url = "https://official-joke-api.appspot.com/jokes/knock-knock/ten"

url = "https://official-joke-api.appspot.com/jokes/general/ten" 
```

into this...

`url = "https://official-joke-api.appspot.com/jokes/#{type}/ten".`

The next step within this process was to pass in the argument of (type) to have the information be passed into the method. 

`def self.get_jokes(type)`

Finally I defined (type) in the CLI class by putting each of the strings for each category into the start method and had each of these strings represent the (type) method in the API.get_jokes method.

```
def start
    puts "Welcome"
    API.get_jokes("programming")
    API.get_jokes("knock-knock")
    API.get_jokes("general")
```
		
This process produced a final result seen below for my new method which combines the previous three methods.

```
1 def self.get_jokes(type)
   2  url = "https://official-joke-api.appspot.com/jokes/#{type}/ten"
   3 uri = URI(url)
   4 response = Net::HTTP.get(uri)
   5 hash_of_jokes = JSON.parse(response)
   6 hash_of_jokes.each do |joke_hash|
   7     joke_instance = Joke.new
   8     joke_instance.id = joke_hash["id"]
   9     joke_instance.kind = joke_hash["type"]
10     joke_instance.question = joke_hash["setup"]
11     joke_instance.punchline = joke_hash["punchline"]
12     end
13 end
```

*Lines 3 to 13 were the same in the original 3 methods.*

It was quite the learning experience putting everything together into this one project. I thank my wonderful instructor and my classmates for helping me with how it should all come together. I created this app mainly for anyone who gets frustrated throughout the day. Especially people who code or go through a lot of stress points. Yes the jokes are cheesy but you can’t deny that it’s good at making you smile therefore producing more “cheese” or happiness.

If you would like to check out the code for my [project](https://github.com/codewithirene567/cheesylaughs) you are welcome to do so.




