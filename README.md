# Rockpool Detective - GA Project One - 7 Days

![Rockpool Detective](https://i.imgur.com/1E7ZomE.png)

Rockpool Detective is based on the classic code-breaking game Mastermind.  A hidden pattern of four Rockpool Creatures is generated at the start of each game and the player must try to guess the correct pattern within six attempts. The player is given clues based on how close they are to the correct pattern as they go, which helps them to inform their next guess. 

## Deployment link

The project was deployed using Github and can be experienced [here](https://bit.ly/Rockpool-Detective).

## Brief 
* The game should be playable for one player with the computer creating the code to guess.
* Once the game has been completed the player should be able to play again.

## Timeframe

The time allocated to complete this project was one week. This was a solo project and was completed during week four of the GA Software Engineering Immersive course.<img width="646" alt="Screenshot 2023-01-04 at 16 58 34" src="https://user-images.githubusercontent.com/114397080/210608791-de239cc5-04ff-41a5-b8f6-e5eb51dbec23.png">


## Technologies Used
JavaScript, HTML, CSS.

## Planning

### Project management

![Trello](https://i.imgur.com/r5AuFa2.png)
I used Trello to plan the project which enabled me to keep all notes and ideas in the same place, map a timeline and monitor progress. This kept me focussed and helped with achieving the key goals of the brief. 

### Wireframe

![Wireframe](https://i.imgur.com/K3FRWtw.png)
Using a wireframe (drawn with [Excalidraw](https://excalidraw.com)) helped me visualize the HTML components, as well as ideas for styling the user interface.

### Pseudocode
I wrote a framework for JavaScript in plain English, including the elements, variables, executions and events. I included methods and the logic I planned to use. 
```
  function playerChoice() {
    // Player makes a choice of Rockpool Creature to add to decoding grid
    // * clicking on choice will select from the choicesArray
    // * pushes this into playerCurrentChoiceArray
    // Player choice displayed in decoding grid cell ( will need to target 1 row at a time- arrays of grid cells and rows)
    // * add choice to the decoding grid cell in DOM with classList.add().
    // Continue loop through clicking and adding to grid, until all available cell are full for that round
    // * move onto the next row, target next 4 cells- ? function nextRow()
    // Loop through rows 1-6 as above, until either:
    //  * playerChoiceArray != computerChoiceArray and  number of rows in decoding grid is less than or = to (no of rows)6   - keep playing
    //  * playerChoiceArray != computerChoiceArray and number of rows in decoding grid is greater than (no of rows)6 - computer wins - gameover()
    //  * playerChoiceArray = computerChoiceArray and  number of rows in decoding grid is less than or = to (no of rows) 6 - player wins- gameover()
  }

  function compareMatches() {
    // the playerCurrentChoiceArray compared against the computer computerCurrentChoiceArray
    // 1) compare both Value and position
    // * If a playerChoiceArray[i] = computerChoiceArray[i] &  playerChoiceArray value = computerChoiceArray value -->  add to a rightChoiceRightPlaceArray
    // * This is repeated for the array.length
    // 2) Compare only Value
    // * Then if playerChoiceArray[value] = computerChoiceArray[value]and playerChoiceArray[i] != computerChoiceArray[i]-->  save to rightChoiceWrongPlaceArray
    // * This is repeated for the array.length
    // 3) Then add clues
    // * rightChoiceRightPlace[i].lenght + 1  =  number of black clue keys --> saved to blackKeysArray and added as class to clue grid cell - classList.add()
    // * rightChoiceWrongPlace[i].lenght +1  =  number of white clue keys to be printed --> saved to whiteKeysArray and added as class to clue grid cell - classList.add()
  }
```


##  Build Process

I spent day one planning: understanding the brief, researching the game, creating a timeline, setting goals, and generating the wireframe and pseudocode. My approach meant that by day two I was able to complete the HTML and get the styling to the minimal viable product.

### Making the decoding and clue grids
As the  decoding and clue grids are the central part of the game, it was key to get these made early on. Initially, I used JavaScript to the grids dynamically, however it was evident after trying for a long time to manipulate them into the correct grid/row formation and place them side by side, I was not going to achieve the desired placement without compromising the progress of the project.  Since these grids were not going to be used for character movement (e.g as in Pac Man),  I decided to instead hard code them in HTML, then style with CSS using display:flex and display:grid

<img width="488" alt="Screenshot 2023-01-04 at 16 53 39" src="https://user-images.githubusercontent.com/114397080/210608558-7ac5e0db-66b4-43e0-871a-fc3442b8703b.png">

### Creating the random code and player choice
The secret code was randomly generated by selecting 4 items from the choiceArray:
<img width="636" alt="Screenshot 2023-01-04 at 17 00 19" src="https://user-images.githubusercontent.com/114397080/210609163-0bb57058-4265-4f11-b783-b6a726a087fa.png">


Random series of choices was generated using Math.random() and pushed into the empty computerCurrentChoiceArray

<img width="565" alt="Screenshot 2023-01-04 at 16 59 32" src="https://user-images.githubusercontent.com/114397080/210608992-450fe644-f2cd-469c-a3ce-5713ed36a7ed.png">

The player choice was made using a click , which also corresponded with the values in the choiceArray. I used the forEach method to add the event listener . Each creature had a class of “choice” and its own ID.
<img width="633" alt="Screenshot 2023-01-04 at 17 00 55" src="https://user-images.githubusercontent.com/114397080/210609287-29c13348-facc-4e97-a409-1438cab82652.png">

The playerChoice function added player selected choices into the playerCurrentChoiceArray. Once the length of the array as equal to four, no further choices were added.
<img width="445" alt="Screenshot 2023-01-04 at 17 01 32" src="https://user-images.githubusercontent.com/114397080/210609433-9c6774a3-a387-4e27-9ab2-58f0f0f58315.png">

Later I created the disableChoices() with a removeEventListener to disable the click event.

### Preparing the grids for play
<img width="643" alt="Screenshot 2023-01-04 at 17 01 52" src="https://user-images.githubusercontent.com/114397080/210609502-9a96ee5a-4e0b-4f63-b899-15e4357a6109.png">

In this game, each row of the grid is equivalent to a round of the game. During each round, four choices are placed in a row in the decoding grid,before being appraised with clues. 

I therefore needed to transform my HTML list into arrays of four decodingCells (“rows”). These 6 arrays are held within the “rowsArray”. The starting row is actually the bottom of the grid and the last array of cells in the rowsArray, hence the currentRow variable. 
<img width="463" alt="Screenshot 2023-01-04 at 17 04 00" src="https://user-images.githubusercontent.com/114397080/210609899-33c076ae-f0d2-42fc-9e44-233f5207f683.png">

Similarly for the clue cells, I created a function called “prepareClue” in which the “cellsArray” is built, containing six “cells” arrays , each with four targetable clueCells within them. These correspond to the number of clues which can be awarded each round. 

### Displaying player choice in the DOM
This is a function that displays  the values in the playerChoice array, based on the index of the decodingCell in the current row.  
<img width="446" alt="Screenshot 2023-01-04 at 17 04 25" src="https://user-images.githubusercontent.com/114397080/210609998-5e81bb2d-5bc4-42d0-8bf2-d2d80986c16a.png">

The updateDOMRow() function is then called within playerChoice().
<img width="534" alt="Screenshot 2023-01-04 at 17 05 00" src="https://user-images.githubusercontent.com/114397080/210610109-c5d5b0ef-6518-4dfa-acdb-89e6d3de0197.png">

### Comparing the randomly generated secret code with the players chosen code
Initially I used multiple array methods, however a simpler solution was to create objects for the player and the computer and pass the “full” or “partial” matches into these. 		The diagram shows how the partial and full matching process works
<img width="628" alt="Screenshot 2023-01-04 at 17 05 36" src="https://user-images.githubusercontent.com/114397080/210610233-96845a0b-d68f-4f9c-bfad-37c8a997a65d.png">

First full matches were checked. I cycled through the computerCurrentChoiceArray and compared it one by one with the values in the playerCurrentChoiceArray. The value and the index position is compared, and if both match the value full is added into both the player and computer arrays at the corresponding key (e.g. “starfish” direct match and ‘full is added to key 3 in both objects. 
<img width="642" alt="Screenshot 2023-01-04 at 17 05 59" src="https://user-images.githubusercontent.com/114397080/210610283-3e46a214-0586-4c16-8b2c-dea790248cf9.png">

### Comparing the partial matches….more info here

### Giving clues to the player choice
I targeted the DOM elements for the clue grid  (clue cells) in the same way, to display the “partial” and “full” matches. The matches are generated and passed into the empty clueArray at the end of each round. 
<img width="367" alt="Screenshot 2023-01-04 at 17 06 33" src="https://user-images.githubusercontent.com/114397080/210610382-8efc0ed1-d156-42bd-ba07-a3df02861514.png">

The updateDOMClue gets called within a function called compareChoices()
<img width="382" alt="Screenshot 2023-01-04 at 17 06 57" src="https://user-images.githubusercontent.com/114397080/210610459-b2b7644f-d7fc-4747-8cad-3663f4f71f3e.png">

## Challenges

The main difficulty in this project was the logic behind comparing the player choice against the randomly generated code. Comparing full matches was more straightforward, but the partial matches were more problematic, as I didn't want duplicates in the players, or any of the full matches to be counted twice.

<img width="633" alt="Screenshot 2023-01-04 at 17 07 17" src="https://user-images.githubusercontent.com/114397080/210610534-913c7cfa-c99f-462d-8550-05726b43e959.png">
<img width="631" alt="Screenshot 2023-01-04 at 17 08 08" src="https://user-images.githubusercontent.com/114397080/210610672-d4906a6f-f387-4c0c-81d1-432cd08c4e13.png">

## Wins
* Responsive design for smaller screens and phones
* Strong visual design and theme

## Key Learning Points

* Understanding the importance of creating a good plan, and working through things one step at a time. 
* Feeling more adept at using CSS
* Appreciating the value of DRY code and use of semantic naming
* Improved understanding of classes 
* Utilizing vanilla JavaScript for DOM manipulation 

## Bugs

I am aware of an issue with white clue keys when the game is restarted using the play again function. 

## Future Improvements

* Refactor some of the code (e.g. make. the playerWon) a function and restructure the code.
* Refine the CSS to make it a little more DRY.
* Make it possible to clear one row on the decoding grid, rather than resetting the entire game if the player wishes to change their choice.
* Enable the player to drag and drop choices, and move them around on the decoding grid until they are happy, then submit guesses for each row via a button click. 
* Game difficulty could be altered e.g made easier for children with fewer choices, shorter rows and more guesses (longer grid). 
* I could include more CSS keyframes animation to make it more visually appealing, for example highlighting the player choices using border pulse or shaking the Play Again button after Game Over.








