# Planning for Simon 

## Analyze the App's Functionality 
Minimal Viable Products

As a user, I want to... 
- view a gameboard with four different colored squares that each have a different sound when clicked
- click a "start" button to begin the game 
- watch the game generate a flashing sequence pattern with different sounds for each square for me to try to repeat from memory, starting with just one flash
- continue playing the game with an increasingly longer pattern sequence to repeat if my pattern matches the game pattern, building off of the previous round by one flash/click
- see a level counter so I know how many rounds I've successfully completed
- click a "play again" button after losing to try again!

## Overall design and feel 

- clean and minimalistic 
- yellow square with a laser sound 
- red square with a cow sound 
- blue square with a dog sound 
- green square with a siren sound 
- font of Quicksand 
```html 
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Quicksand&display=swap" rel="stylesheet">
```
CSS rules are: 
```css 
font-family: 'Quicksand', sans-serif;
``` 

## Wireframe the UI 
![wireframe img](/Screenshot%202023-04-20%20at%2011.20.02%20AM.png)


## Psuedocode 

1. Define required constants 
    - a **squareBoard** variable as an array that stores each square 
    - an **audio** variable as an object that will store the corresponding sound for each square
    - a **squareColors** variable as an object that stores the corresponding color for each square
     

2. Define required variables used to track the state of the game 
    - a **gameSequence** variable as an empty array that will store the flash sequence generated by the computer
    - a **playerSequence** variable as an empty array to store the player click pattern sequence 
    - a **roundCounter** variable to keep track of what round it is 
    - a **gameMove** variable that allows the computer to wait for the player's turn before moving again 
    - a **startButton** variable that disappears when the game begins
    - a **gameOver**/boolean variable that indicates whether the game is over or not; the game will end when the player makes a mistake/does not match the game pattern
    - a **playAgainButton** variable that only displays after the game is over

3. cache DOM elements 
    - color squares 
    - sounds for the squares 
    - start button 
    - play again button 
    - round counter

4. Upon loading, the app should: 
    - initialize the state variables 
        - set the **roundCounter** variable to 0
        - generate a starting game pattern seequence of 1 flash 
        - the **gameOver** variable should be set to false 

    - render the gameboard to the page 
        - render the start button
        - render the gameboard with 4 different colored squares with different sounds for each 
        - render the counter with a value of "0" so the player knows it's the first round 
        - render the play again button, should not be visible on first load
       - display the first randomly generated flash sequence (should just be one flash)
    - wait for the player to click a button 

5. Handle the player clicking a button 
    - collect the player sequence click(s) in the playerSequence array 
    - compare playerSequence array to gameSequence array
    - if the sequences match:
        - update the **roundCounter** variable 
        - add a new randomly generated value to the gameSequence array 
        - display the full game sequence pattern from the beginning + 1 new flash per round
        - wait for the player to click a button 

6. Handle the player clicking the play again button
    - reset the state variables 
    - render the start button 
    - render the gameboard 

## Identify the Application's State (data)

```js
const SQUAREBOARD = ["yellow", "red", "blue", "green"] 

const SQUARECOLORS = {
    yellow: "255, 255, 0",
    red: "255, 0, 0",
    blue: "0, 0, 255", 
    green: "0, 128, 0"
}

const AUDIO = {
    yellow: "http://www.freesound.org/data/previews/42/42106_70164-lq.mp3", 
    red: "http://www.freesound.org/data/previews/58/58277_634166-lq.mp3", 
    blue: "http://www.freesound.org/data/previews/327/327666_5632380-lq.mp3", 
    green: "http://www.freesound.org/data/previews/336/336899_4939433-lq.mp3"
}

let gameSequence // holds the game pattern sequence 
let playerSequence // holds the player sequence
let gameMove // allows the computer to play a move at intervals
let gameOver // indicates when the player enters an incorrect sequence
``` 