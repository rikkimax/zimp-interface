$ python game.py file.save

// reasoning file.save is the savefile that will persist for the game.

Output: No game file found, new game.
Output: The rules of this game can be found at
Output:     http://www.systemreferencedocuments.org/resources/systems/boardgame/zimp/zimp-original.pdf

// if no save file exists that was given at application start then create a new game.
// Only show game rules if new game

// start at last tile if not new game
// start at foyer tile if new game

* Turn loop *
  // use Tile info output section.
  
  // if dining room say this:
  
  Output: The door to outside is ${door to outside}.
  
* Input loop *  
    Input: What do you want to do?
    
    // if the answer to the input is help then use Help message section.
    // if the answer to the input is info then use Tile info section.
    
    // if the answer to the input is move then:
      move in direction specified
    // if the answer to the input is rotate and is in placement mode of a tile then:
      set the direction of the new tile to the inputs value
    // if the answer to the input is place and is in placement mode of a tile and is placement for rotation then:
      place the new tile down
    
    // if either of the three previous statements are false. Then:
      Output: You cannot do that action.
    // if the input is invalid:
      Output: Your input is invalid. Please type help for more information.
    
  // Until in new tile do the input loop
  
  // pick new development card
  Output: You got a development card of ${development card action for time}.
 
* Zombie attack * 
  // if zombies are attacking then:
    Output: Choose option to fight the zombies
    Output: (1) Fight bare handed 1 attack -1 health
    Output: (2) Run away - 1 health
    // if have oil:
      Output: (3) Run away with oil 0 health
    // if item 1 valid for attacking
      Output: (3/4) ${item 1 name} ${item 1 attack value} attack
      // if item 2 valid for attacking
        Output: (4/5) ${item 2 name} ${item 2 attack value} attack
    
   
   Input: Chosen action
   // if action is an attack and won
   
   // if is run away go to Choose tile to go to, previous
    handle health loss
  
  // if item is known on tile then:
    Input: Do you want to look for an item?
    // if yes, get item if not already found.
      goto Item found section

  // if development card has action to be taken:
    Development card action is performned

* Item found *
// if item 1 is not empty
  // if item 2 is not empty
    Output: Which item do you want to get rid of?
    Input: ${List of items with index}
    Replace old item with new
  // otherwise
    Set item 2 to new item
// otherwise
  Set item 1 to new item
   
* Choose tile to go to, previous *
 Output: You can go in directions: ${door list of previous tiles}.
  Input: Please select a door to exit from
  
  // if room is valid
    go to tile chosen
  // otherwise
    repeat
    
* Help message *
Output: 
Output: A direction is left, right, up and down.
Output: To move out of a door type: move [direction].
Output: 
Output: Once in a new room, you must rotate a tile.
Output: To do this type: rotate [direction].
Output: To end rotation of a tile type: place.
Output:
Output: To find out the tile's state type: info

* Tile info output *
Output: You are at ${tile name} tile.
Output: There are doors at ${door list}.

// if room is Evil Temple
  Input: Spend time to find totem?
  // if yes,  get a development card of ${development card action for time}.
    goto Development card action section
	
// if room is Storage Room
	Input: Spend time looking for item?
	// if yes, get item 
      goto Item found section
	  
// if room is dead end
  Input: Choose a wall for an attack.
  Output: 3 Zombies!
  goto Zombies attack section
  
// if room is Kitchen
  Output: Snack time! Gain 1 health.
  
// if Dining Room and go in direction of arrow is chosen
  Patio tile will be chosen
  
// if room is Garden
  Output: Helpful herbs! Gain 1 health.
  
// if room is Graveyard
  Input: Spend time to bury totem?
  // if yes,  get a development card of ${development card action for time}.
    goto Development card action section
	Output: Congratulation! You Win!
	
* Cower *
// if end of turn
  Input: Wait & cower for 3 health?
  
if health <= 0
  Output "You have died! Game Over!
  
if time == 12:00
  Output: You have run out of time! Game Over!
