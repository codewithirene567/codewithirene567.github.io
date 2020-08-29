---
layout: post
title:      "Test Your Knowledge on Countries All Over the World!"
date:       2020-08-29 23:58:11 +0000
permalink:  test_your_knowledge_on_countries_all_over_the_world
---


There's nothing like seriously learning a brand-new programming language within a matter of weeks build a project on it while combining it with another language you knew before. I have done just that very recently and as a result couldn't be prouder and more confident of who I've become in terms of getting places with my software development career. One day I am confident that my skills through what I've learned so far will help bring much needed value to a company.

Javascript might just be the most popular language in the world with it covering over 95% of websites on the world wide web. When I learned that fact from my other cohort members, I was shocked, yet at the same time I wasn't. I had working with Javascript before I even started the Flatiron Software Engineering, and in building my first couple projects basically all I heard about was Javascript this and Javascript that all over the internet. The idea that the concepts from it was mentioned everywhere before, now represented by a percentage, made me recognize it as more valuable than ever before.

Putting that aside, my Javascript Project that I have created this time is called Traveler's Trivia and it is exactly what it sounds like: a place for travelers to try their hand at some trivia for all the countries they could visit.

Let me briefly explain how it is built. I would first like to point out that in this specific project there is no framework for the Javascipt. Javascript is heavily used for the front end through creating functions, which a synonymous term for these would be "named actions to display information", while HTML builds the structure of what is displayed, and Rails is used for the backend to create an API which through a database creates and retrieves data to make the website interface display the correct resources.

The way the front-end retrieves data is through making fetch requests, which were an essential part of building this project.

In Traveler's Trivia there were 3 fetch requests being made to the API. Two of them were GET requests for two resources called countries and questions. The last request was a POST request which was used to let users create high scores in the API database.

I will break down what the first fetch request is doing to better explain how it was implemented into my project.

```
fetchCountries(){
```

This first line is naming the function, fetchCountries, and is establishing it as a function by adding a () after it with a {. The curly bracket { opening means that the code in here will be executed anytime fetchCountries() is called.

```
        fetch(this.baseUrl)
				
```
Now the above line is saying that this function is going to contain a fetch request because of the key word fetch along with an argument area which will contain a URL source in the (). Fetch requests to GET something have to start their request from what is at the URL that is passed in. This means that at the URL it has all of our countries in it as an API.

Where does this.baseUrl have value? Obviously this.baseUrl copy and pasted into any sort of browser won't return us any API, but this request works because ```this.baseUrl``` is a variable that is in reference to the code before ```fetchCountries()``` is written. The code that it is referring to looks like this: 

```
class CountriesAdapter{
    constructor(){
        this.baseUrl = "http://127.0.0.1:3000/countries"
    }
```

The important part to recognize here is that this.baseUrl has value in this line and because all of this code is wrapped in the curly brackets of the ```class CountriesAdapter ``` we are able to use the "this" keyword to refer to the ```this.baseUrl ``` variable.

```
        .then(resp => resp.json())
				
```
The above next line is using the ```.then``` method to hold an argument of whatever response we get back which is what ```resp``` stands for. As of right now ```resp``` holds all of the countries from our API. Then it is turned into a Javascript Oriented Notated Object which is why ```.json()``` is there. This way Javascript can work with the object in a format that it understands.

```
        .then(json => renderCountries(json))
```
Next up we have the above line which is taking the JSON made response and putting it into the renderCountries() function, which is in another part of this file. This is why it is passed in as an argument like so ```(json)```.

```
      }
}

```

Every function in Javascript has to end with a closing curly bracket like this }. The first one is closing the ```fetchCountries()``` function and the second one is closing the class itself since this fetch request is part of what represents the ```class CountriesAdapter```.

Altogether our fetch request looks like the following:

```
fetchCountries(){
        fetch(this.baseUrl)
        .then(resp => resp.json())
        .then(json => renderCountries(json))
      }
```

Now it becomes easy to see why fetch requests are kind of like the start button on our whole frontend; because they retrieve everything and put it into the correct format. However, fetch requests are no good without being able to show these results from our fetch requests in our HTML, which is how the user is able to see anything.

The basic pattern for being able to show the results can be done by knowing how to add things to the DOM and specifically what that looks like in Object Oriented Javascript. I've broken this pattern down into six steps with an example of each of these listed below the steps.

1) Create a function in a file named by the name of your resource with .js on the end after creating an object class.

Example: I will use the example from my project where I wrote a function which will make a new high score show up on the DOM after the user inputs their name.

a) Created a file called highscore.js
b) Created an object class called ```class Highscore{```
c) Created a function ```addHighscoretoDOM(){```

2) Create an element you want to add and set it equal to a variable using const or let.

Example: ```const highscore = document.createElement('li')```

In this case I have created a variable called ```highscore``` which is going to be a li element or a list element with a bullet next to it.

3) Select an element from your HTML where it is going to be added by using document.[write selector name] and set that equal to a different variable.

Example: ```const newHighscoreArea = document.getElementById('all-high-scores')```

The variable newHighscoreArea is set equal to the whole HTML document in another file which is represented by the word document. Then using a selector ```.getElementById``` I am selecting the element by its ID which in this case is ```('all-high-scores')```.

4) Give the element value in some kind of way by adding a .[write property name] after the name of the variable.

Example: ```highscore.textContent ```

TextContent is a property of high score which means that it is the text of whatever will go into the li element.

5) Set the value equal to what you want it to be.


Example:```+= ` Name: ${this.name} ` ```

In this case, the keyword "this" refers to a high score object which has an attribute of a name. So the by writing ```${this.name}``` we are telling the code to display the name of the person who is associated with that high score and setting this name equal to the textContent of the high score.

6) Add the variable to the DOM by using some sort of method that will add it to an element bigger than itself, which should be the variable you created in step 3.

Example:```newHighscoreArea.appendChild(highscore)```

The final step includes using both of our variables. the ```(highscore)``` needs to be added to the ```newHighscoreArea```. We using the method ```.appendChild``` to add small thing to the big thing which will now show up on the DOM.

As Javascript is such a popular language, the actions someone is able to do with it and the number of syntax formats is massive. Because of this fact, there are so many concepts in Javascript that I haven't even learned yet, but this is exactly what makes it so exciting to me is because it gives me a chance, as I get better at writing it, to learn new ways to code lines of it in many different ways.

This project has been a great achievement so far even if some of these Javascript concepts have been so new to me and I can't wait to see how Javascript frameworks look like and how to use them. That experience I would think would be similar to how I learned how Rails looked like for Ruby in the past.

In addition to the concepts covered in this blog for the making of this project, click [here](https://github.com/codewithirene567/travelerstrivia-frontend) to see the repo for the frontend part of it and click [here](https://github.com/codewithirene567/travelerstrivia-backend) to see the repo for the backend of the project.

Hopefully if you have messed with my website already after you've forked and cloned it, the questions weren't too hard for you. But then again, nothing says "trip" like "tripping" up on some of these trivia questions before you even get there. :)

Thanks again to my incredible instructor Jenn and my other super helpful cohort members for helping me to see things that I couldn't in my code, and helping me to improve it.
