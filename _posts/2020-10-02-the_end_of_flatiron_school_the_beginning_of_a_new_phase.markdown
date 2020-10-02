---
layout: post
title:      "The End of Flatiron School, The Beginning of a New Phase"
date:       2020-10-02 21:49:14 +0000
permalink:  the_end_of_flatiron_school_the_beginning_of_a_new_phase
---

I cannot believe I have reached the end of this coding bootcamp and made it through! It has been such an enlightening experience no matter how much I struggled. By enlightening I mean I didn't realize how much I could accomplish and how my mind could absorb so much information in just 5 months through my coding experience here at Flatiron.

Anyways to get to the point of this blog, my final project from this bootcamp is a combination of everything I have learned in terms of the frameworks, libraries, and programming languages I have learned to use. These languages mainly include Ruby (backend) and JavaScript (frontend) and the frameworks used in this project were React (frontend) and Rails (backend). Along with these, one critical library I used was Redux and an external dice package.

As you can probably guess by me mentioning a dice package, my project is most certainly a game. It is in fact my very own version of Snakes and Ladders. Now lots of board games are exciting to code, but this snakes and ladders game really had its ups and downs. Jokes aside what I am really trying to say is it was no easy task to create, but because it was a game I was excited to make, I was able to enjoy the ups enough to keep me motivated on working on it during the downs with what seemed like an endless amount of errors I was facing consistently.

In case you have been living under a rock though or to refresh your memory, this game can have multiple players who all take turns rolling a die and the number of die is the number of spaces they move on the board which has 100 squares to land on. When they get to a ladder space, the player game piece is supposed to move up until it reaches the end of that ladder object placed on the board. On the other hand, if they land on a snake, they will move down until they reach the end of that snake object on the board. The first player who gets to 100 spaces officially wins the game.

Now that I've gotten the how-to-play part out of the way, I'll get to some of the most important concepts in my code to make the game function.

Firstly, working with React I learned the difference between class components and functional components to make up the skeleton of how the game looks like.

To explain briefly, a functional component is much simpler than a class component and only returns JSX
```
return (
        <div>
            <div id="ladder-1" className="ladder-1">
						```
						
instead of rendering it like so...

```
render() {
      
        return (
          <div>
            <ReactDice
						``` 				 

An example of a class component would be my dice component which has to keep track of the state of what number it has rolled which will determine the current position of the player pawns on the board. In terms of functional components, an instance of this would be when I coded my ladder component which is only responsible for showing the JSX to display 3 ladder objects on the game page which is also a child component of my game container component. In other words, this ladder component is just one of the many objects which will render in the game container.
				
Another difference would be that functional components are all about displaying information without using state or lifecycle methods. With state or lifecycle methods it is best to use class components instead. In fact, one line of code that is consistently different in terms of structure between these two types of components would be 
				
```
class Dice extends Component {
```
				
versus...
				
```
export default function Ladder() {
```
				
You can see the key difference here would be that the keyword "extends" isn't used in a functional component while in a class component it must be used.

Speaking of key words, another keyword I got to know fairly quick about while working with React is the word "props" which is a useful tool in terms of passing values from one component to the next and lets our components be more dynamic rather than repetitive. Props, short for properties, is a word that is connected to a variable that is set equal to anything you want as JSX in curly brackets.

When coding my projects, I made good use of creating container components that represented each of my routes from the routes I wrote with the React Router. By good use I mean passing props from my container components to my presentational components to keep everything organized the way React’s design intended it to be.

For example in my code I had a home page which was going to let users type in their name to submit it to the state that way on the next page, which I called game, the program would render the amount of players' names typed in as pawns on the board.

This is my child component called PlayerInfo which is supposed to contain the form for the players to submit their name.

```
1 class PlayerInfo extends Component { 

2 handleSubmit = (event) =>{
     3 event.preventDefault()

		4 this.props.addPlayer({name: this.state.name, currentPostion: 0, playerId: this.variable})
		5 this.setState({name: ' '})

		6 }

		7 render () {

				8 return (
						9 <div>
						10 <form onSubmit={this.handleSubmit}>
						11 <label>
								12 Name:
								13 <input type="text" name = "name"value={this.state.name} onChange={this.handleChange} />
						14 </label>
						15 <br></br>
						16 <br></br>

						17 <input type="submit" value="Save Player" />
						18 </form>
						```
				
Here below is my parent component for my home page which in line 7 I am rendering my form and rendering my form into my container component every time the home page is on the user's screen.

```1 class Home extends React.Component {```
				
```
2 render () {
3 return (
      
 4 <div>
 5 <div>
 6 <h1>Welcome to Snakes and Ladders! Make some players by filling out your information below</h1><br></br>
 7 <PlayerInfo addPlayer={this.props.addPlayer} moveForward={this.props.moveForward}/>
 8  </div>
			```

Allow me to explain in terms of props how the concept applies in my home component. On line 7 I have assigned a variable to the words ```addPlayer``` and have set its value to ```={this.props.addPlayer}```. What this value is doing is it is attaching the word ```this``` because it is in a class, and attaching the word props to an action I have written in my action creator file called ```addPlayer ```. ```addPlayer``` will be called every time the variable addPlayer is called in the PlayerInfo form. This ```addPlayer ``` action is used in line 4 in my PlayerInfo form which will add a player, but this was only possible through giving ```addPlayer``` value because I used the keyword props in the parent component.

I am so glad I have made it this far in learning how to code, growing in mental strength and believing that I could get to this point. From my perspective, finishing this bootcamp has given me the future confidence to achieve more later on down the road. More specifically, even if I know things won't get any easier in terms of how hard I want to continue to work with code, I'm at the point where I'm thinking to myself, if I can get through this bootcamp, I can handle any other challenges that will come later on down the road.

My appreciation again goes out to my other cohort members, the software engineering community through the internet, and my wonderful instructor Jenn for teaching me so much directly and helping me to fix issues I wouldn't have seen by myself in my code.

Click [here](https://github.com/codewithirene567/snakes-and-ladders-react) to see the repo for the frontend of this project and click [here](https://github.com/codewithirene567/snakes-and-ladders-backend) to see the repo for the backend of the project. For more of a visual experience, click [here](https://www.youtube.com/watch?v=vm3m8XwftXs) to see my demo video for how this project looks like.






