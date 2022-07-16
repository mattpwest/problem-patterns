# Porklike Roguelike Tutorial

This problem pattern is extracted from https://youtu.be/HnY7Inp74dw.

Unlike the original tutorial, the focus here is not on guiding you through building a roguelike in PICO-8. Instead I've tried to extract the requirements for building a fairly feature complete Roguelike into simple TODO lists that you can follow through while choosing your implementation technologies and design patterns.

Unlike the TCOD Roguelike tutorial, this one assumes that you are creating a tile-based roguelike, so it includes tasks for art and animation.

The following icons can be used to indicate progress as you work through your copy of this file:
 * :x: : not started
 * :warning: : work in progress
 * :no_entry: : skipped / ignored
 * :heavy_check_mark: : finished

## #1 - Overview ([link](https://youtu.be/HnY7Inp74dw))

* :x: Read the [Berlin Interpretation](http://www.roguebasin.com/index.php/Berlin_Interpretation) as an introduction to Roguelike mechanics
* :x: Study any required knowledge about tools or techniques
* :x: Choose and setup your programming language
* :x: Choose and setup your IDE
* :x: (OPTIONAL) Choose and setup your sound tools
* :x: (OPTIONAL) Choose and setup your tile map editing tools
* :x: (OPTIONAL) Choose and setup your art tools (if you want to use a tile-based style)
* :x: (OPTIONAL) Choose an existing tile set to use (if you want to focus on the code / game design)
* :x: (OPTIONAL) Consider joining something like the [7DRL Challenge](https://itch.io/jam/7drl-challenge-2022) for extra motivation

## #2 - Basic Movement ([link](https://youtu.be/SoFOva5FUnI))

* :x: Draw the player character idle / walk animation frames
* :x: Draw a wall tile
* :x: Draw a ground tile
* :x: Draw stairs tiles
* :x: Design a simple one room map for initial testing using all of the above
* :x: Code loading the designed map (or define it in code for now)
* :x: Code initial main game state (figure out how to switch states later when you have more)
* :x: Code drawing the map on screen
* :x: Code drawing the player character on screen
* :x: Design character movement (orthogonal, diagonal, both, something unusual?)
* :x: Code moving the player character on screen
* :x: Code recoloring of sprites from code

## #3 - Animation ([link](https://youtu.be/CO1qTJMH8mU))

* :x: Code simple looping animation of the player character (walk / idle cycle)
* :x: (OPTIONAL) Make it easy to control animation speed (e.g. play at half / quarter speed)
* :x: Code a movement animation to smoothly slide the character between tiles when moving
* :x: (OPTIONAL) A separate game state that doesn't accept input during movement animations

## #4 - Token Optimization ([link](https://youtu.be/1ZUhxXQiDCA))

* :x: (OPTIONAL) (PICO-8) Learn how to refactor code to reduce repetition and minimize token usage
* :x: (OPTIONAL) Refactor code to express a movement direction as an index into two arrays of deltaX and deltaY
  * This is a surprisingly useful idea!
* :x: (OPTIONAL) Refactor animation system to use a floating point counter with the formula `value = finalValue * (1.0 - counter)`

## #5 - Wall Collision ([link](https://youtu.be/PnE5S4DoNEg))

* :x: Code flipping the character sprite horizontally to indicate moving left or right
* :x: Code character collision with wall tiles to prevent walking through walls
* :x: Code a bump animation when the player tries to walk into a wall
  * Move halfway into the tile and then slide back to their original tile
  * While animation progress 0.0 - 0.5 move to the target position
  * WHile animation progress 0.5 - 1.0 move back to the original position

## #6 - Object Interaction ([link](https://youtu.be/y3uNmCL414M))

* :x: Design a test level with player spawn, stairs up and stairs down
* :x: Draw a door tile
* :x: Draw at least 2 variants of a treasure chest tile with open and closed state
* :x: Draw at least 2 variants of smashable pots
* :x: Draw a stone tablet
* :x: Create tiles for all of the above, they should all block movement
* :x: Incorporate all of these into your test level design
* :x: Refactor code so the bump animation plays for any tile that blocks movement (not just walls anymore)
* :x: Code effects that occur when bumping into the various interactive tiles:
  * :x: Vase being destroyed (replace with floor tile)
  * :x: Door opening (simply replace with floor in this game)
  * :x: Chest opening (replace with open chest tile)
* :x: Test out your test level
* :x: (OPTIONAL) Refactor code to queue up a single key press during animation state
  * So that the game reacts to a key that was pressed during animation
  * In the main state only accept new input if the button buffer is empty
  * Controls should feel much more responsive after this change

## #7 - Text Boxes ([link](https://youtu.be/6G2StWNTFlo))

* :x: Create: Walking sound
* :x: Create: Door opening sound
* :x: Create: Chest opening sound
* :x: Create: Bad thing happened sound
* :x: Create: Breaking vase sound
* :x: Code to play all of these when appropriate
  * Bad thing happened will be used in a later step of the tutorial
* :x: Code to popup a dialog box containing some text
  * Accepting an array of lines of text gives good flexibility for laying out messages

## #8 - Message System ([link](https://youtu.be/XuT3nwDuRiw))

* :x: Code popping up a text box when interacting with a stone tablet
* :x: Code a variant of the text box that shows a one-line message which disappears automatically after a configurable time
  * This variant should set its width automatically based on the text to show
  * It should also be automatically centered on the screen
* :x: (OPTIONAL) Code a snap-shut animation when a window closes
  * That is reduce text box height by percentage decrements until <= 0
* :x: (OPTIONAL) Ensure the text boxes have some padding to improve readability
* :x: Code a variant of the text box that must be dismissed manually
  * This variant should have fixed width, but display a variable number of lines
  * It should be automatically centered on the screen
  * It should show an 'x' icon to hint to the player that it needs to be dismissed
* :x: Code a way to print text with an outline
  * A simple way to do this is print the outline 1 pixel in each of the 8 directions
  * Then printing the text at the target location
  * This is useful for the dismissal icon above to ensure contrast for readability
* :x: Code a bounce animation for the dismissal icon
  * A simple `+ sin(time())` on the y coordinate tends to work well
* :x: Hide the button during the window closing animation
* :x: (OPTIONAL) Code a way to have different messages for different stone tablets
  * (OPTION 1): Based on coordinates
  * (OPTION 2): Based on tile data

## #9 - Monsters ([link](https://youtu.be/rjWxDQcYUwo))

* :books: Lots of theory discussion in this video - hence not many TODO items...
* :x: Draw a slime monster (with 4 frame animation)
* :x: Code spawning the slime monster on the test map
* :x: Code to draw and animate all spawned monsters

## #10 - Mob System ([link](https://youtu.be/CSIHQElMdF0))

* :x: Code a data structure for storing animation frames and switch monster spawning to use it
  * Just storing the first frame may be viable if all animations have the same number of frames
  * If not, store a list of each frame in the animation
* :x: Refactor the code to represent, draw and animate the player so that it can also be used for monsters (or mobs)
  * The definition of mob is: mobiles... so players and monsters. Hence, mob system.
* :x: Code a way to get the mob at a certain map position (if any)
* :x: Code a way to check if a tile is walkable
  * Include a map bounds check here to prevent the player moving outside the map if we're missing some walls
  * Include an optional mode in this for also checking if there is a mob on the tile and blocking movement if there is

## #11 - Combat ([link](https://youtu.be/FvSLsmTCIO4))

* :books: This video features an interesting theoretical discussion about RPG combat design
  * This tutorial game will have an unconventional style of combat
  * Units will do a reliable amount of damage instead of a random value
  * To encourage planning rather than gambling
* :x: Code to add mob data for starting hit points
* :x: Code to add mob data for attack power
* :x: Code to initialize mobs with hit points and attack power
* :x: Code for attacking the mob in a tile if the mob moves into a tile containing another mob
  * Simply subtract attack power from hit points
  * If hit points are 0 or less, the mob should be destroyed
  * For now give the slimes 2 HP for testing
* :x: Code to animate a mob with a flash if it takes damage
  * Simply coloring the mob white for a few frames should suffice
* :x: Create: Hitting enemy mob sound
* :x: Create: Getting hit sound
* :x: Code to play the hitting enemy mob sound when the player attacks a mob
* :x: Code to show a damage floater when a mob takes damage
  * That is: a particle effect, showing the amount of damage...
  * ... which briefly floats above the damaged unit's head
  * Tween function: `currentY = (targetY - currentY) / 10`
  * Use a black outline print for legibility

## #12 - Simple Pathfinding ([link](https://youtu.be/qLIPY0ro5UY))

* :x: (OPTIONAL) Code a way to spawn mobs from map data
  * More useful if you want to use some hand-designed content in addition to procedural
* :x: Code to calculate the distance between two points on the map
  * `dx=tx-x; dy=ty-y; dist=sqrt(dx * dx + dy * dy);`
  * As an optimization you can often skip the `sqrt`
* :x: Code turn structure and "stupid" movement AI
  * After the player has moved, iterate through all mobs other than the player
  * Search through each of the 4 (or 8) adjacent squares for an open one with the lowest distance to the target (the player)
  * Move the unit to this tile
  * If no tile was found skip the mob
  * If the target (player) is in the tile, attack it
* :x: (OPTIONAL) Code a system for showing AI debug information on screen

## #13 - Death ([link](https://youtu.be/1jQJQ_l4geM))

* :x: Code a game over state
* :x: Code a check for player death which switches to the game over state
* :x: Code to restart the game on a button press in the game over mode
* :x: (OPTIONAL) Try to find and fix any issues from restarting the game
* :x: Code to continue displaying and animating dying mobs
  * For a short time before they are finally removed
* :x: (OPTIONAL) Code animation to make the dying mob flash
* :x: (OPTIONAL) Refactor drawing to draw player mob last
  * I.e. ensure the player is always on top

## #14 - HP Display ([link](https://youtu.be/LIlFLoU9S1w))

* :x: Code for fading the screen in / out
* :x: Code to fade in the screen at the start of the game
* :x: Code to fade out the screen if the player dies, before going to the game over screen
* :x: (OPTIONAL) Freeze the game for a couple of seconds on death before or during the fade out
  * To give the player a moment to see what killed them
* :x: Code to fade out the game over screen when the player presses a key
  * Effectively resulting a cross-fade with the game start
* :x: Code a small hit points display dialog to show the player health
  * A box with `HP: current / max` essentially
  * Position the box dynamically to not be "in the way", i.e. bottom of the screen when the player is a the top, top when the player is at the bottom...
* :x: (OPTIONAL) Code to tween the dialog position smoothly when it moves
* :x: (OPTIONAL) Code to remove the HP dialog when the player dies
  * I.e. ensure it is no longer shown on the game over screen

## #15 - AI ([link](https://youtu.be/eTdD1vRC9OY))

* :x: Code for checking line of sight
  * Can one tile position see another tile position?
  * Non-walkable tiles can be considered to block line of sight
  * (OPTIONAL) You can use the naive algorithm from [Line Drawing Algorithm](https://en.wikipedia.org/wiki/Line_drawing_algorithm) if your map size is small enough
  * (OPTIONAL) Considering distance 1 as visible is a good tweak to handle rare edge cases where a unit is standing on a blocking tile
* :x: Code a simple state machine for AI controlled mobs
  * WAIT:
    * Stay in place
    * If you see the player switch to ATTACK
  * ATTACK:
    * If you see the player update your target to their position
    * Move to the target
    * Attack if possible
    * If target reached switch back to WAIT
* :x: Reuse the floater code from part 11 to:
  * :x: show an exclamation point when a mob sees the player
  * :x: show a question mark when the mob loses track of the player

## #16 - Fog of War ([link](https://youtu.be/QF5jZWAhl1s))

* :x: (OPTIONAL) This is a good point to test what you have so far and squash any bugs you find
* :x: Reuse the line of sight function from part 15 to implement simple fog of war:
  * All tiles on the map start invisible
  * On the player turn loop through all tiles on the map:
    * Check line of sight from the player to that tile
    * If a tile is visible, remove the fog
  * Once uncovered a tile will remain visible forever
* :x: (OPTIONAL) Research and implement more sophisticated line of sight and fog of war algorithms
  * If you want to have more realistic line of sight
  * Or if you want to have larger maps than 15x15, because the approach described above is very simple and brute force and likely won't scale to larger map sizes

## #17 - Fog Polish ([link](https://youtu.be/0cTutS4CC5c))

* :x: Improve line of sight check to distinguish between walkable and being able to see past or through something
  * :x: Chests should not block LOS
  * :x: Pots should not block LOS
* :x: Improve line of sight down long hallways where you see the floor tiles, but not the walls
  * When removing fog from a tile
  * If the tile is walkable
  * Also uncover adjacent tiles that would block line of sight (typically walls)
* :x: Limit the range of line of sight per mob
  * So the player doesn't uncover the entire map so quickly
  * So that mobs don't aggro from so far away
  * In the tutorial the value used was 4 tiles

## #18 - Token Tweaks ([link](https://youtu.be/VRxd1oDsvx4))

* :x: (OPTIONAL) If you are using PICO-8, spend some time [optimizing your token count](https://www.lexaloffle.com/bbs/?tid=45114)

## #19 - Pathfinding ([link](https://youtu.be/zA1uMY5f4Js))

* :x: Code a better path finding algorithm
  * The tutorial uses Dijkstra Mapping and provides a good example of implementing it
  * Here are some additional resources:
    * [Flow Field Pathfinding for Tower Defense](https://www.redblobgames.com/pathfinding/tower-defense/)
    * [The Incredible Power of Dijkstra Maps](http://www.roguebasin.com/index.php/The_Incredible_Power_of_Dijkstra_Maps)
    * [Dijkstra Maps Visualized](http://www.roguebasin.com/index.php/Dijkstra_Maps_Visualized)

## #20 - Path Tweaking ([link](https://youtu.be/D54YMXRrS5I))

* :x: Code to choose a random step if there are multiple options with the same distance
  * To prevent predictable AI that ends up in an endless stalemate dance with the player

## #21 - Inventory UI ([link](https://youtu.be/QAP5bPkuIdc))

This chapter does a lot and the description here is a bit rambling. Probably needs a second pass to condense this into requirements rather than step-by-step instructions for the process of coding this feature.

* :x: Code for storing the inventory
  * In the tutorial we have 6 inventory slots
* :x: Code for storing the equipment slots
  * In the tutorial we have 2 equipment slots: weapon, armour
* :x: Code new game state to display a window and handle inventory input:
  * Enter this state on a specific button press
  * Use placeholder text in the slots for initial testing
  * Show 2 equipment slots at the top
  * Show a line
  * Show 6 inventory slots
  * Press a key to dismiss
* :x: Code for windows to have an optional cursor mode
  * Some padding on the left of the window to leave room for the cursor
  * Index to store which line of the window the cursor is on
  * Draw the cursor 
* :x: Code to control the cursor in any window
  * Called in the inventory state to allow cursor control
  * Up moves the cursor up
  * Down move the cursor down
  * Either restrict the cursor to the visible lines or allow wrap-around
  * One key for selecting
  * Another key for closing the window
* :x: Code to animate the cursor left and right (sin wave is fine)
  * To help draw attention to the element the player is currently controlling
* :x: Code to color the inventory text:
  * Use a brighter color for filled slots
  * And a dimmer color for empty slots and the separator
* :x: Code to add a second window during inventory mode to show player stats
  * For now just placeholders: "ATK:1   DEF:1"
* :x: Code to create initial placeholder items into free inventory slots:
  * Items will for now just have a name, e.g. broad sword, leather armour, red potion
  * If a slot is available, create the item and put it into that slot
  * If no slot is available the item is lost (no floor items in this game)
* :x: Code change for inventory display code to use the item and equipment names instead of placeholders

## #22 - Use Menu ([link](https://youtu.be/Ku_xe6wXdvs))

* :x: Data to define item types (also showed here what you can do with each type):
  * Weapon: Equip, Throw, Trash
  * Armor: Equip, Throw, Trash
  * Food: Eat, Throw, Trash
  * Throwable: Throw, Trash
* :x: Code to pop up a sub-menu window when an item is selected in inventory
  * Ensure the sub-menu lines up with the inventory item
  * Only show the actions relevant to the selected item type

## #23 - Equipment ([link](https://youtu.be/15Yw4gzqHX8))

* :x: Code to trash an equipment or inventory item
  * In this game items don't get dropped on the floor, they are simply destroyed
* :x: Code to equip an item from inventory
  * If there was already an item in that equipment slot put it back in the inventory
* :x: Code tweak to make sure you cannot equip an already equipped item
* :x: Code to keep the inventory open after certain inventory actions
  * For example equipping should keep it open
  * Remember to update the inventory display after changes to equipment
* :x: Define item data for weapon attack value
* :x: Define item ata for armour defense value
* :x: Code to recalculate player attack / defense when equipment changes
  * `player.atk = 1 + weapon?.atk`
  * `player.def = 1 + armour?.def`
* :x: Code to replace placeholder stats display with the real values
* :x: Code to make the defense stat randomly reduce damage from incoming attacks:
  * Split stat on items into minimum and maximum defense
  * Add the same fields on the mob and update stats update code
  * E.g. leather armour is 0 - 2 points of damage blocked
  * Enemies will have 0 defense, instead just give them more health
  * On damaging an entity roll a random number in the range and deduct it from the damage
    * `dmg=max(0, dmg - (defmin + flr(rng(defmax - defmin + 1))))`

## #24 - Eating ([link](https://youtu.be/pLa-GoNzvfI))

* :x: Data for what effect eating a specific item has
  * One placeholder effect to start: heal
* :x: Code for eating things
  * Heal adds 1 HP
  * But not more than the unit's max HP
  * Animated floater should show actual HP healed
  * Destroy the item afterwards
* :x: Code for a mob to wait (skip turn)
  * Use this after player eats to make it take a turn
* :x: Code new game state for targeting the throw of a selected item
  * Pressing a direction button selects the direction to throw in
  * Pressing the cancel button goes back to the inventory
  * Draw a line from the player to 1 tile away in the throw direction

## #25 - Throw UI - ([link](https://youtu.be/dtiSXv1YD7w))

* :x: Code to detect the closest mob along the throw line (the one that will be hit)
  * Checking for walkable excluding tiles populated with mobs is the easiest way
* :x: Code change to draw the throw line to the tile that will be 
* :x: Code change to draw a dotted throw line instead of a solid line
* :x: (OPTIONAL) Extra polish on the throw line:
  * Draw a black dotted line on each side of the line to get an outline to improve contrast
  * Draw a + with outline at the end of the line to show where the throw ends
  * Constrain the end of the line to always be on screen (even if throwing outside the screen)
  * Animate the dotted line (in PICO-8, simply inverting the fill pattern every few frames works well)

## #26 - Throwing ([link](https://youtu.be/fWDi8G2In9k))

* :x: Code to play a bump animation of the player in the throw direction when throwing
* :x: Code to apply the thrown item's effect to the target mob (if any)
  * Food items will simply be eaten by the target
  * Thrown weapons will do damage like attacking
* :x: Code to delete the thrown item from the player's inventory
* :x: Code to animate the targeted mob flashing during targeting
* :x: Code to play the mob hit sound when damaging the mob with a thrown item


## #27 - Gameplay Test ([link](https://youtu.be/yOrDUsF1OpI))

* :x: Code to give the player a random item when they open a chest
* :x: Code to give the player a random item 30% of the time when they break a pot
* :x: Code change - some actions should not trigger an AI turn:
  * Reading a tablet
  * Bumping a wall
* :x: Data change: slime mobs from 2 HP to 1 HP
* :x: Hand-design an interesting level for testing the game design
  * Spend some time iterating until it is at least a little bit fun
  * This level will serve as inspiration for the type of level the level generator should generate in future

## #28 - Random Rooms ([link](https://www.youtube.com/watch?v=3sWIQocOoq8))

* :x: Temporarily disable fog of war while working on level generation
* :x: Read up on the [Rooms and Mazes algorithm](https://journal.stuffwithstuff.com/2014/12/21/rooms-and-mazes/) by Bob Nystrom
* :x: Code to fill the map with walls
* :x: Code to generate a random rooms:
  * Minimum width and height of 3 tiles
  * Maximum width and height of 5 tiles
  * Width and height may be different
  * Set initial position to 0,0
* :x: Code to randomly place the room in the level
  * Pick a random coordinate
  * Dig out the room dimensions by replacing walls with floors
* :x: Code to randomly add multiple rooms
  * Add a check to ensure a new room won't overlap any existing room
  * Try for a target number of rooms
  * Give up if you have more than a target number of failures to place
  * The parameters from the tutorial were:
    * 5 rooms with size 5x5 and up to 5 failures
    * On each failure maximum room dimensions are reduced (to a minimum of 3x3)
* :x: Code change to room generation to provide more varied room dimensions:
  * No room should have more than 35 tiles
  * Roll width first
  * Then calculate a new max height to ensure <= 35 tiles
  * Then roll height

## #29 - Tile Signature ([link](https://youtu.be/LV0OhUWMCg8))

* :x: Code to calculate a tile signature that identifies the tiles around a position
  * Will be used to figure if we can tunnel at a position for now
  * Also used later to smartly place objects within the level
  * If you use the exact algorithm provided here you can later use the same signatures in your code
  * Algorithm:
  ```javascript
  // Iterating through neighbor tiles goes:
  //   left, right, up, down, up-right, down-right, down-left, up-left
  dirX=[-1,1,0,0,1,1,-1,-1];
  dirY=[0,0,-1,1,-1,1,1,-1];

  function getSignature(x, y) {
    var sig = 0;
    for (var i = 0; i < 8; i++) {
      var tx = x + dirX[i];
      var ty = y + dirY[i];
      var digit = 0;
      if (!walkable(tx, ty)) {
        digit = 1;
      }
      // To make the pseudo-code clear:
      //   binaryOr: performs a bitwise OR operation on its two inputs
      //   bitShiftLeft: shifts the bits in the first argument left by a number of
      //                 bits specified by the second argument
      sig = binaryOr(sig, bitShiftLeft(digit, 8 - i - 1));
    }
    return sig;
  }
  ```

## #30 - Signature Mask ([link](https://youtu.be/zX0qNqWeoQk))

* :x: Code the maze worm function that will carve a maze in the remaining space between rooms
  * Step 1: just highlight viable tiles to see if signature works
    * Any tile that is a walkable
    * That is also completely surrounded by wall
    * I.e. has a signature of 0b11111111
    * Replace these tiles with a differently colored wall to test this
  * Step 2: to help figure out the worm make the player the worm
    * Change maze worm to reset any tiles that no longer match the signature to normal walls
    * Change the player bumping a wall so that it digs out the bumped wall
    * You can now see the viable start areas changing as you dig out tiles
  * Step 3: code a function to check if a tile signature matches a bit mask
    * Inputs are:
      * signature: signature to check
      * match: what signature to match
      * mask: optional defaults to 0, marks certain bits as insignificant
    * The code is simple:
      ```javascript
        function binaryComp(sig, match, mask = 0) {
          return binaryOr(sig, mask) == binaryOr(match, mask);
        }
      ```
    * The matches and masks are built from the following values:
      * 0b1101 x11x:
        * match: 0b1101 0110
        * mask : 0b0000 1001
      * 0b0111 11xx:
        * match: 0b0111 1100
        * mask : 0b0000 0011
      * 0b1011 xx11:
        * match: 0b1011 0011
        * mask : 0b0000 1100
      * 0b1110 1xx1:
        * match: 0b1110 1001
        * mask : 0b0000 0110
  * Step 4: code a new canCarve function to check if an x,y coordinate can be carved
    * Get the signature of the tile at x,y
    * Loop through each of the match/mask pairs identified above
    * If any of them matches return true
    * If none match return false
  * Step 5: also highlight carveable tiles as in step 1
    * Now you can test it out and see this clearly shows where to carve next

## #31 - Maze Worm ([link](https://youtu.be/OUWNiOxVbYs))

* :x: Code change to canCarve function: target tile must not be walkable
* :x: Code change to room generation: max rooms from 5 to 4
  * To allow more room for the maze function to work
* :x: Code the real maze worm function
  * Replace the existing code which was temporary to help understand the algorithm
  * In outline:
    * Put tiles that can be carved into a list of candidates
    * Pick a random candidate
    * Start a worm dig from that tile
      * Pick a random direction
      * Repeat until we cannot continue carving tiles:
        * Carve the current tile
        * Check if the next tile in the current direction can be carved
          * If yes, move there and carve
          * If no, make a list of directions containing tiles that can be carved
            * Pick a random direction

This episode in the video series felt a bit incoherent compared to previous ones, so here is some javascript pseudo code of the mazeWorm and digWorm functions to try to make sure the requirements are clear. The code is roughly a literal translation of the code in the episode, no effort has been made to refactor it, though I suspect it could perhaps be rewritten a bit more simply:
```javascript
// Iterating through neighbor tiles goes:
//   left, right, up, down, up-right, down-right, down-left, up-left
dirX=[-1,1,0,0,1,1,-1,-1];
dirY=[0,0,-1,1,-1,1,1,-1];

function mazeWorm() {
  const candidates=[];
  repeat {
    candidates.clear();
    for (var x = 0; x <= MAP_WIDTH; x++) {
      for (var y = 0; y <= MAP_HEIGHT; y++) {
        if (!isWalkable(x, y) && getSignature(x, y) == 255) {
          candidates.add({x=x, y=y});
        }
      }
    }

    if (candidates.length > 0) {
      var c = getRandomFromList(candidates);
      digWorm(c.x, c.y);
    }
  } until candidates.length <= 1;
}

function digWorm(x, y) {
  var direction = randomInRangeIncludingStartAndEnd(0, 3);
  var step = 0;

  repeat {
    setMapTile(x, y, TILE_FLOOR);

    if (!canCarve(x + dirX[direction], y + dirY[direction]) || (random() < 0.5 && step > 2)) {
      step = 0;
      var candidates = [];
      for (int i = 0; i < 4; i++) {
        if (canCarve(x + dirX[i], y + dirY[i])) {
          candidates.add(i);
        }
      }

      if (candidates.length == 0) {
        direction = 8;
      } else {
        direction = getRandomFromList(candidates);
      }
    }

    x += dirX[direction];
    y += dirY[direction];
    step++;
  } until direction == 8;
}
```

## #32 - Merging Areas ([link](https://youtu.be/TILFOPcS5GM))

* :x: Code a map of flags
  * Empty map
  * Same dimensions as the world map
  * Initialized to 0
* :x: Code to color the floor tile (a unique color per flag value)
  * Temporary, needed for testing / debugging
* :x: Code a `placeFlags` function
  * Will run after mazeWorm
  * Create an empty map of flags initialized to 0
  * Create a currentFlag initialized to 1
  * Loop through the entire map area
  * If a tile is walkable and not flagged yet:
    * FloodFill from that location with the currentFlag
    * Increment currentFlag by 1
* :x: Code a `floodFill` function
  * Takes x, y and currentFlag as arguments
  * Create a candidates list containing the initial x,y
  * Create a newCandidates list that is empty
  * Repeat until no candidates remain
    * Loop through all current candidates
      * Flag the current candidate's position
      * Loop through all tiles adjacent to the current position
        * If it is walkable and not equal to currentFlag yet add it to newCandidates
    * Set candidates to newCandidates
* :x: Code a carveDoors function
  * Will run after placeFlags function
  * Repeat until no possible doors are found:
    * Create an empty list of possible doors
    * Loop through the entire map
    * If a tile is not walkable
      * New variable found = false
      * New variable flag1 = 0
      * New variable flag2 = 0
      * Get its signature
      * Check if the signature is a valid place to carve with binaryComp:
        * 1100 xxxx
          * If yes:
            * Set found = true
            * Set x1,y1 and x2,y2 to positions above and below the tile
        * 0011 xxxx
          * If yes:
            * Set found = true
            * Set x1,y1 and x2,y2 to positions left and right of the tile
      * Set flag1 to flags at x1,y1
      * Set flag2 to flags at x2,y2
      * If found and flag1 != flag2
        * Add to doors list:
          * x
          * y
          * flag1
          * flag2
    * If 1 or more door candidates were found:
      * Pick a random candidate
      * Carve that x,y to a floor tile
      * Run FloodFill to fill from that position with flag1 or flag2

## #33 Shortcuts ([link](https://youtu.be/b2GMyOZRXOM))

* :x: Remove code to color the floor tile a unique color per flag value
* :x: Code a carveShortcuts function
  * Will run after carveDoors
  * Similar structure to carveDoors, but instead tries to find door candidates where digging would connect two areas that are many steps apart
  * Repeat until no possible shortcuts are found or 3 shortcuts have been made
    * Create an empty list of possible shortcuts
    * Loop through the entire map
    * If a tile is not walkable
      * New variable found = false
      * Get its signature
      * Check if the signature is a valid place to carve with binaryComp:
        * 1100 xxxx
          * If yes:
            * Set found = true
            * Set x1,y1 and x2,y2 to positions above and below the tile
        * 0011 xxxx
          * If yes:
            * Set found = true
            * Set x1,y1 and x2,y2 to positions left and right of the tile
      * If found:
        * Calculate the distance in steps between x1,y1 and x2,y2
        * If distance > 20:
          * Add x,y to shortcuts list
    * If 1 or more door candidates were found:
      * Pick a random candidate
      * Carve that x,y to a floor tile
      * Increment the number of shortcuts made
* :x: Code a fillEnds function
  * Will run after carveShortcuts
  * Fills in any dead-ends create by the worm
  * Repeat until no candidates are found:
    * Loop through the entire map
    * If a tile is walkable and only has 1 exit, add it to candidates
      * Repurpose canCarve without the is not walkable check to identify having 1 exit
    * Loop through each candidate
      * Fill the tile with a wall again
* :x: Optimize floodFill function code:
  * Immediately flag candidate tiles
  * So that other neighbors don't add the tile to candidates again

## #34 - Stairs ([link](https://youtu.be/cuTet3kI51o))

* :x: Code a startEnd function to generate the player's starting position and the stairs
  * Runs after fillEnds
  * Pick a random initial point (any walkable tile)
  * Place the starting position
    * Calculate a distance map from the initial point
    * Find the furthest walkable tile in the distance map that is carveable
      * This will put the stairs in a little alcove
    * Place the stairs that return to the previous level there
    * Spawn the character there
  * Place the stairs to go to the next level
    * Calculate a distance map from the starting position
    * Find the furthest walkable tile in the distance map that is carveable
      * This will put the stairs in a little alcove
    * Place the stairs to the next level there
* :x: Code changes to have more information about rooms
  * Create a global list of rooms
  * Create a global room map (like a distance map)
  * When about to carve a room:
    * Save the room into the list of rooms
    * In the carve function, for each tile being carved:
      * Set the tile being carved to the number of the room list on the room map
* :x: Code a function to detect possible doors
  * Code function to check if a tile is a possible door
  * Call it when carving shortcuts or to connect two areas:
    * Check adjacent tiles in the rooms map
    * If the tile is non-zero (i.e. in a room)
    * Save this to a global list of possible doors
* :x: Code a installDoors function to put doors in appropriate places
  * Runs after all previous level generation steps
  * Loop through the list of doors:
    * If location is walkable and isDoor is still true
      * Place a door tile

## #35 - Floors ([link](https://youtu.be/YnetPcmmVXw))

* :x: (OPTIONAL) Check if any of the code fixes / optimizations in the video are applicable to your code base
* :x: Swap these two operations in your level generator:
  * `fillEnds`
  * `startEnd`
  * Tweak `fillEnds` candidate list generation to check that the tile we can carve is not one of the stairs
* :x: Fix the possibility of entrance and exit stairs spawning next to each other
  * Instead of finding both in a single loop
  * Find one, then the other
* :x: Code a `genFloor` function
  * Single floor number argument
  * Sets global floor to the argument
  * Call map generator afterwards
  * Replace initial call of `mapGen` with `genFloor(0)`
* :x: Code to go up the stairs
  * On the player stepping on the stairs up:
    * Skip the AI turn
    * Fade out the screen
    * Create the new floor with `genFloor(floor + 1)`
    * Pop up a message showing the floor number for 4 seconds

## #36 - Shepherding ([link](https://youtu.be/JCVTI0ve9KU))

* :x: Update isDoors function to prevent some bad door placements:
  * Things to prevent:
    * Two doors next to each other
    * A door that leaves a diagonal gap
      * e.g. has wall above and right, so open spaces are left and down
    * A door placement deleting the exit stairs
  * How to do it?
    * Use the signature function from earlier and require these signatures:
      * 1100 xxxx
      * 0011 xxxx
    * Change the isDoor check to check that the tile is a floor tile instead of that it is walkable
* :x: Try to reduce the chance of having disconnected rooms
  * Add a function to check if a tile is next to a room
    * Using the existing room map created earlier
  * Add an extra loop to the end of `mazeWorm`:
    * Loop over all tiles to build a candidate list
    * Consider candidates that can be carved and that are NOT next to a room
    * Carve these tiles to floor tiles
    * Repeat until there are no more candidates left
  * This should prevent double-walled rooms in the earlier phase of generation before `fillEnds`
* :x: Improve `startEnd` to prevent scenarios where the start and end are close together
  * Change the canCarve checks to check for both walkable and not walkable:
    * `if tmp > high and (canCarve(x, y, false) or canCarve(x, y, true)) {`
    * `if tmp >= 0 and tmp < low and (canCarve(x, y, false) or canCarve(x, y, true)) {`

## #37 - Hub Floor ([link](https://youtu.be/mO49X3Jrmy8))

* :x: Design a hub level where the player will start a new game
  * Add a stone tablet with a message that explains the goal of the game
* :x: Design a final level where the game will end
* :x: Code to load a hand-designed map instead of using level generation
  * The video covers many PICO-8 specific details, it's probably easier in other game engines
  * Load the hub level for level 0
  * Load the end level for level 9
* :x: Draw the final goal
  * In the tutorial it's the Golden Kielbasa, make it whatever you want
* :x: Code to display the game start message when interacting with the stone tablet
* :x: Code to end the game when the player retrieves the final goal
  * Switch to a new game state similar to the game over screen
  * Can use the same update loop as dying, just show a "You win" message for now
  * This can be replaced with a flashy win screen later
* :x: (OPTIONAL) Replace function to fill level with walls with loading a level full of walls
  * Mainly just a token optimization for PICO-8
* :x: Code the `spawnMobs` function
  * Call this as the next step of level generation
  * Place all rooms in a list of candidates
  * Initialize the counter of mobs placed to 0
  * Repeat:
    * Pick a random room
    * Remove the room from the candidates
    * Increment the count of placed mobs
    * Call a new `infestRoom` function that places mobs in a room
    * Until no candidate rooms remain OR we have placed the target number of mobs
* :x: Code the `infestRoom` function
  * Pick a random number of mobs to place
    * For now between 2 and 3
  * Loop for the number of mobs you want to place:
    * Initialize targetX and targetY as 0
    * Repeat:
      * set targetX to a random position in the room
      * set targetY to a random position in the room
      * Until `isWalkable(targetX, targetY)` (excluding other mobs)
    * Add the mob at targetX, targetY
* :x: Code fix: clear the mobs list when switching levels
  * Remember to put the player back in the list if you clear it

## #38 - Optimizations ([link](https://youtu.be/KT72ydigoxk))

* This chapter is mostly fixes and token optimizations for the PICO-8 project
  * If you are interested in those details, watch the video
  * I will just list below traps that you are likely to have fallen into anyway or optimizations that are useful in a non-PICO-8 setting
    * :x: Code fix: mobs are probably only being cleared on level generation not on level switch
      * If so, move it to level switch, otherwise leftover mobs stick around in the loaded level
    * :x: The `mazeWorm` function can be optimized to remove the second phase of worms that can start next to tunnels dug by previous worms:
      * Change the candidate check to: canCarve and not next to room

## #39 - Tile Borders ([link](https://youtu.be/y4wcaXzhAdM))

* :x: Read this blog post by [Boris The Brave](https://www.boristhebrave.com/2013/07/14/tileset-roundup/)
  * To understand how to construct a blob tileset that will cover all corner cases for walls
* :x: For this particular topic watching the video is also a good idea to understand the complexity

## #40 - Pretty Walls ([link](https://youtu.be/VHCMLoeZG2s))

* :x: Code a new function `prettyWalls()` that replaces the walls with the new tiles
  * The author of the video did all the heavy lifting of figuring out tile signatures and masks to check for with `binaryComp(...)`
  ```javascript
  wall_sig={251,233,253,84,146,80,16,144,112,208,241,248,210,177,225,120,179,0,124,104,161,64,240,128,224,176,242,244,116,232,178,212,247,214,254,192,48,96,32,160,245,250,243,249,246,252}
  wall_msk={0,6,0,11,13,11,15,13,3,9,0,0,9,12,6,3,12,15,3,7,14,15,0,15,6,12,0,0,3,6,12,9,0,9,0,15,15,7,15,14,0,0,0,0,0,0}
  ```
  * The missing ingredients are:
    * Your tilemap must follow the same layout as his (check the previous video)
	* You need the offset into your tilemap for the first tile in the list
	* Remember to treat all the new tiles as unwalkable walls like the original wall tile
  * Then the algorithm is simply:
    * Loop through the map
	  * Loop through all signatures and masks
	    * If any signature matches, set the tile to the one corresponding to the coordinate `index + offset_into_tilemap`
* :x: (OPTIONAL) If you want to use a different tile map layout you will need to create your own arrays to map signatures to your layout

## #41 - Wall Overlap ([link](https://youtu.be/ZYFdJSMMdN8))

* :x: (OPTIONAL) Tweak the code so that loaded levels have no fog of war, but generated levels do
  * Only really needed if it makes sense for your game design
* :x: (OPTIONAL) If you are using PICO-8: copying the function to create data arrays from strings will save you many tokens
  * You can copy the `explode` and `explodeval` functions from [here](https://github.com/omgmog/lazydevs-pico8-roguelike/commit/2018087fa0ca8b27258f38ee8e6008ddf85e7412)
* :x: Draw new partial wall floor tiles to put below top walls of rooms
  * (OPTIONAL) Also draw full wall tile and window wall tile for high rooms
* :x: Code update to `prettyWalls` function to replace floor tiles below top walls with wall floor tiles
* :x: Code change to level generation:
  * Call `prettyWalls` before `installDoors`
    * This results in prettier doorways

## #42 - Decorations ([link](https://youtu.be/SHCGjkdBx3g))

* :x: Code fix: `installDoors` should also check for the wall floor tiles and install doors on them
* :x: Draw some additional tiles for decorating the dungeon:
  * Giant goal items for your final level (a golden kielbasa sausage in the case of Porklike)
  * Animated torches on left or right wall
  * Carpeted floor tile and carpeted wall floor tile
  * Two variants of a fern floor tile
  * 3-4 variants of a debris floor tile
* :x: Redesign the final level to incorporate the goal item
* :x: Code an `animateMap` function
  * Loop through all map tiles:
    * If you see a tile that matches one of the torch tiles, flip it to the other frame
    * Introduce some kind of delayed frame counter to slow down the animation speed
  * Call this in your main game update function
* :x: Code a `decorateRooms` function to place decorations in the level:
  * To be called after mob placement in the level generation
  * Loop through all rooms:
    * Randomly select a room decoration function to call to generate a specific type of room (these will be defined below)
* :x: Code a `decorateCarpet` function:
  * Loop through all the tiles in the room:
    * Replace all the floor tiles except the edges at the walls with the carpeted floor tile
* :x: Code a `decorateDebris` function:
  * Loop through all the tiles in the room:
    * If the tiles is a normal floor tile:
      * Have a random chance to replace the floor tile with a random debris floor tile or a normal floor tile
* :x: Code a `decorateTorches` function:
  * Loop through all the tiles in the room:
    * If the tiles is at the left or right edge of the room:
	  * If the y coordinate is divisible by 2 and there is no door next to the target tile and on a 66% chance:
	    * Replace the tile with a left or right torch tile

## #43 - Managing Stats ([link](https://youtu.be/rdoanMNlu24))

* :x: Code a `decorateFerns` function:
  * This room type will impair line of sight
  * Loop through all the tiles in the room:
    * Randomly replace the floor with one of:
      * fern variant 1 (blocks LOS) (3 of 10 chances)
      * fern variant 2 (blocks LOS) (3 of 10 chances)
      * grass variant 1 (allows LOS) (1 of 10 chances)
      * grass variant 2 (allows LOS) (1 of 10 chances)
      * dirt (allows LOS) (1 of 10 chances)
      * normal floor (allows LOS) (1 of 10 chances)
* :x: Code a `decorateVases` function:
  * This room type will contain a few vases
  * Loop through all the tiles in the room:
    * If:
      * it is a floor tile
      * and there is no mob there
      * and it's not next to a door
      * and the signature is not out in the open (no walls adjacent)
    * Then:
      * Replace the tile with a random one from:
        * normal floor (2 of 4 chances)
        * vase variant 1 (1 of 4 chances)
        * vase variant 2 (1 of 4 chances)
* :x: Create a spreadsheet to manage data for monsters and items
  * Google sheets is free and works well
  * You can see the video for the current placeholder items
  * You will have the following sheets:
    * Items sheet:
      * Name
      * Type (weapon, armour, food, throwable)
      * Stat 1
      * Stat 2
    * Monsters sheet:
      * Name
      * Animation
      * Attack
      * Hit Points
      * LOS Distance
    * Export sheet where formulas for export will go
  * Add formulas to export the data to strings that you can paste into your game:
    * This example handles the item names column and writes a line of code to parse CSV to array in PICO-8:
      * `itm_name="explode(""" & JOIN(",",Items!A2A6)& """)"`
    * Do this for all data columns
* :x: Add two new stats for items and monsters:
  * MinFloor: the minimum dungeon floor where it will spawn
  * MaxFloor: the maximum floor where it will spawn
  * For now set min to 1 and max to 8...

## #44 - More Monsters ([link](https://youtu.be/cNJtErJwhZ8))

* :x: Design all the items for the game
  * These are distributed between level 1 through 8
  * In the tutorial there are:
    * 6 weapons
    * 6 armours
    * 6 foods
      * THese are going to be dynamically generated and will need to be identified like potions in other roguelikes
    * 4 throwables
* :x: Design all the monsters for the game
  * These are distributed between level 1 through 8
  * In the tutorial there are:
    * The player
    * 7 monsters
* :x: (OPTIONAL) Listen to the explanation in the tutorial video about how just increasing numbers on the same type of item is not good game design
* :x: Copy all this new data from the spreadsheet into the game
* :x: (OPTIONAL) There are some PICO-8 specific optimizations and code improvements in the video
* :x: Draw or copy tiles for showing all the monsters from the data
  * Remember to update the monster data with correct tile numbers / tile data
* :x: Code change for `spawnMobs` function:
  * Start by creating a `mobPool` array of all mobs from the mob data that can spawn on the current level
  * When spawning a mob select a random type to spawn from this `mobPool`
  * Tweak the number of mobs spawned to change per level and be be between:
    * Minimum: 3,5,7,9,10,11,12,13
    * Maximum: 6,10,14,18,20,22,24
    * Change the loop to go until maximum mobs are reached
    * If we placed less than the minimum mobs, spawn hallway mobs:
      * Repeat:
        * Repeat:
          * Generate a random x
          * Generate a random y
          * Until x,y is walkable and doesn't contain a mob
        * Spawn a mob at x,y
        * Until minimum mobs are placed

## #45 - Chests ([link](https://youtu.be/--jn8PfA7BY))

* :x: Code a new function `spawnChests`:
  * Runs after `installDoors` before `spawnMobs`
  * Pick a random number of chests to spawn from {0, 1, 1, 1, 2, 3}
  * Create a list of candidate rooms
  * For the number of chests:
    * Pick a random room
    * Remove it from the list
    * Pick a random walkable tile in the room that is not at an edge of the room
    * Place a chest at this position:
      * The first chest should be the big chest containing rare items like armour or weapons
      * The subsequent chests should be the small chests containing food or throwables
* :x: Code a `makeItemPool` function:
  * Runs once at the start of the game
  * Create two global arrays:
    * `rareItems`: contains all weapons and armour
    * `commonItems`: contains all food and throwables
* :x: Code a `makeLevelItemPool` function:
  * Runs each time a level is generated
  * Create a list of rare items for the level:
    * Loop through all the rare items
    * Filter out any items where currentLevel is not between minimum and maximum floor
  * Do the same for common items for the level
* :x: Code a `getRareItem` function:
  * Randomly pick an item from the rare level items array
  * Delete the item from the rare level items array
  * Delete the item from the rare global items array
  * Return the item
* :x: Code a `getCommonItem` function:
  * Randomly pick an item from the common items array and return it
* :x: Code for interacting with a chest:
  * If inventory is full, show a message to the player saying so...
    * Also skip the AI turn (so this takes no time)
  * Otherwise:
    * Call the correct getItem based on the type of chest
    * Place it in the player inventory
    * Show a message to the player displaying the type of item found
* :x: Code for interacting with vases:
  * If a 33% chance happens:
    * If a 20% chance happens:
      * Spawn a random mob at the vase position
    * Otherwise:
      * If inventory is full, show a message to the player saying so...
        * Also skip the AI turn (so this takes no time)
      * Otherwise:
        * Call `getCommonItem`
        * Place it in the player inventory
        * Show a message to the player displaying the type of item found
* :x: Bugfix: increment number of mobs placed by 1 in `spawnMobs` when placing mobs randomly
  * To prevent an occasional endless loop

## #46 - Random Food ([link](https://youtu.be/so_YhJk34FU))

* :x: Bugfix: when spawning hallway mobs ensure the tile is also a floor tile
  * To ensure they don't spawn on important locations like the stairs
* :x: Code tweak to `decorateRooms`:
  * First decoration function should be vases
  * Only randomize the next room decoration type to use at the end of the loop
  * This guarantees at least 1 vase room per level
* :x: Code tweak to destroying vases:
  * Destroying a vase should spawn a debris floor tile instead of a regular floor tile
* :x: Code to randomize food names:
  * Replace the names for the items "Food 1" through "Food 6"
  * With randomly generate ones:
    * Pick a random adjective, e.g. yellow, marinated, cheesy, zesty, etc.
    * Pick a random food noun, e.g. Jerky, Mett, Calzone, Chops, etc.
    * Combine them separated with a space
* :x: Code some of the new item effects in the eat function:
  * Heal should already be done
  * Do these now:
    * Heal a lot:
      * Heal by 3 instead of 1
    * Increase maximum hit points:
      * Increase max HP by 1
      * Heal by 1
    * Stun:
      * Add a stunned flag on mobs that starts out false
      * Code a `stunMob` function:
        * Flash the target
        * Change the stun flag to true
        * Float a message above the mob saying "stunned"
      * Update the AI function:
        * If mob is stunned:
          * Reset stun flag to false
        * Else:
          * Move as normal
        * On switching back to the player turn:
          * If player is stunned:
            * Reset the stun flag to false
            * Run the AI
  * Do these next time:  
    * Curse
    * Bless
* :x: Code to tell the player the effect of eating an item:
  * Pop up a message box describing the effect

## #47 - Curses ([link](https://youtu.be/so_YhJk34FU))

* :x: Code for mobs with the stun ability to stun the player
  * Add a charge property to mobs with an initial value of 1
    * Each mob can only stun the player once to avoid stun lock
  * On AI attack:
    * If special ability is stun and charge is positive:
      * stun the player
      * reduce the charge
    * Else attack as normal
* :x: Code a `blessMob(mob, val)` function to put blesses / curses on mobs:
  * To be called when eating food with the bless effect
  * Add a bless property to mobs that starts at 0
  * On bless:
    * Set mob bless to `mid(-1, 1, mob.bless+val)`
      * A mob can be blessed or cursed - not both
    * Show a text float with the word bless / curse
    * Flash the target mob
  * On changing dungeon level: clear the player's blessing (reset back to 0)
* :x: Code to handle blesses and curses in combat:
  * If defending mob is cursed and gets hit: multiply damage by 2
  * If defending mob is blessed and gets hit: divide damage by 2
  * In both cases reset blessing to 0 (it only works for one hit)
* :x: Code update for the status window to show blessed / cursed status:
  * Text defaults to "OK"
  * If bless>0 switch to "Bless"
  * If bless<0 switch to "Curse"
  * Show it before the ATK and DEF values in the stats
* :x: Code slow mobs:
  * Add a `lastMoved` flag that starts as false
  * In mob movement AI:
    * If mob special is slow and `lastMoved=true`
      * Set `lastMoved=false`
      * Return instead of moving
    * Else:
      * Move as normal
      * Set `lastMoved=true`
  * Reset `lastMoved=false` in some cases:
    * When the mob loses track of the player and stops being aggressive
    * When the mob notices the player and starts being aggressive
* :x: Code for the ghost mob to curse the player when they attack
  * During attack:
    * If special is cursed and charge > 0:
      * Hit the player as normal
      * Curse the player
      * Deplete the charge
  * During `blessMob`:
    * If target special is curse and val > 0:
      * Kill the mob instead of blessing it

## #48 - Stats ([link](https://youtu.be/jg9E9DM5270))

* :x: Modify level generation code to handle disconnected levels:
  * Keep track of the flags used in `placeFlags` and `floodFill`
  * If more than 1 flag remains after `carveDoors` the level is not fully connected
  * So loop the first part of level generation up to and including `carveDoors` until there is only 1 flag
* :x: (OPTIONAL) Improve the main menu screen:
  * Create a nice logo for your game
  * Show it for a short time on the first level
  * Then animate it floating off-screen
* :x: Code to collect some stats during the play-through:
  * Floor: maximum floor reached
  * Steps: number of steps walked
  * Kills: number of monsters killed
  * Meals: number of food items eaten
  * Killer: who / what killed the player
* :x: Improve the victory and game over screens:
  * (OPTIONAL) Some fancy extra large logo style text looks good for the "You won" or "You died" messages
  * Display the stats collected in the previous step
  * Display a flashing hint to press a key to try again

## #49 - Freestanding ([link](https://youtu.be/7OPJ_QXaRUU))

* :x: Copy the sound effects and music from the tutorial file and copy it to your project
  * If you use the music credit Sebastian Hassler
* :x: (OPTIONAL) Compose your own music and create your own sound effects that fit your game
  * Main theme music
  * You died music
  * You won music
  * Bass line of the music to be played at the beginning
* :x: (OPTIONAL) Create your own sound effects in addition to the ones defined initially:
  * Status effect applied
  * Throwing
  * Confirm Menu
  * Cancel Menu
  * Menu Cursor Move
  * Going up stairs
* :x: Code for playing the music:
  * Play the bassline on the start level
  * When going up the stairs switch to the full main theme looped
  * When the game ended due to death: play the "You died" music
  * When the game ended due to winning: play the "You won" music
* :x: Code the new sound effects:
  * When triggering stairs: play the "Going up stairs" sound effect
  * When applying healing or any status effect: play the "Status effect applied"
  * When throwing an item: "Throwing" sound effect
  * The various menu items when moving the cursor, selecting or cancelling
  * Also use the menu sound effects when showing and hiding a text window
* :x: Code tweak to room generation:
  * Make the first room generated have max size of 10 x 10 tiles
  * After that use the 5 x 5 size from before
* :x: Code a `freestanding` function for checking if a tile is "well connected":
  * 0b0000 x000:
    * match: 0b0000 0000 (0)
    * mask : 0b0000 1000 (8)
  * 0b0000 0x00:
    * match: 0b0000 0000 (0)
    * mask : 0b0000 0100 (4)
  * 0b0000 00x0:
    * match: 0b0000 0000 (0)
    * mask : 0b0000 0010 (2)
  * 0b0000 000x:
    * match: 0b0000 0000 (0)
    * mask : 0b0000 0001 (1)
  * 0b0001 0xx0:
    * match: 0b0001 0000 (16)
    * mask : 0b0000 0110 (6)
  * 0b0100 xx00:
    * match: 0b0100 0000 (64)
    * mask : 0b0000 1100 (12)
  * 0b0010 0x0x:
    * match: 0b0010 0000 (32)
    * mask : 0b0000 0101 (9)
  * 0b1000 00xx:
    * match: 0b1000 0000 (128)
    * mask : 0b0000 0011 (3)
  * 0b1100 x0x1:
    * match: 0b1100 0001 (161)
    * mask : 0b0000 1010 (10)
  * 0b0110 1x0x:
    * match: 0b0110 1000 (104)
    * mask : 0b0000 0101 (5)
  * 0b0101 x1x0:
    * match: 0b0101 0100 (84)
    * mask : 0b0000 1010 (10)
  * 0b1001 0x1x:
    * match: 0b1001 0010 (146)
    * mask : 0b0000 0101 (5)
* :x: Code a `startScore` function to act as a heuristic for the fitness of potential starting position:
  * If outside a room:
    * If next to a room, score is -1
    * If freestanding > 0, score is 5
      * Otherwise if can carve, score is 0
  * Otherwise (inside a room):
    * If matching one of the first 8 freestanding signatures, score is 3
      * Otherwise score is 0
  * Score is -1
* :x: Code change to the `startEnd` function when spawning the player:
  * Deduct `startScore` from the previous position score before deciding if is the new lowest score
  * This may now lead to the player occasionally spawning inside rooms

## #50 - Bugfixing ([link](https://youtu.be/PCaW7PoEKRo))

* :x: These are the bugs found in the tutorial implementation. Fix them if you have them or fix any bugs you find in your own code. I did not include PICO-8 token-saving changes here.
  * :x: Used food names were not being deleted when used
  * :x: Some of the monsters in the tile set are facing the wrong way
  * :x: Ignore negative start scores as potential starting locations in level generation
  * :x: Start score should check next to room diagonally, not just orthogonally
  * :x: Music loops were shifted in the last cartridge, so update the music play functions
  * :x: The combination of making the first room larger and making the first room a vase room results in humongous vase rooms and the player getting too many items. Change to picking the rooms to decorate randomly from a list of all rooms until it is empty.
  * :x: Extend the check if the tile we are spawning on is floor from spawning hallway monsters to the spawns in the regular infest room function.
  * :x: If players stun themselves while no monster is around they carry it with them until they see a monster and are then suddenly stunned. Remove the stun in the AI function, regardless of if any monsters took a turn.
  * :x: Tweak blinking of characters to never blink the player character
    * Otherwise the player is sometimes hidden during death
  * :x: Try to make the line of sight calculation more symmetrical
    * Sometimes the player can see a monster without the monster seeing the player
    * Tweak the line algorithm so the Y coordinate always increases (i.e. in the case you would draw a line from top to bottom swap the coordinates)
      * This improves it slightly
      * Switching algorithms may be a better option
* :x: These are last minute features you could try to add:
  * :x: Smoothly transition from the bassline on level 0 to the full music track on level 1
    * Move the bassline to be pattern 0 and to loop endlessly
    * When you want to transition use code to remove the loop back flag from pattern 0
    * This will cause the song to continue to pattern 1 smoothly
  * :x: Sound effects when picking up items:
    * Regular pickup sound if an item is picked up
    * Warning pickup sound if:
      * The player tries to pick up an item but their inventory is full
      * Breaking a vase spawns an enemy instead of an item
  * :x: Help the player remember what food they have eaten does:
    * Show the effect as a hint in the inventory screen if the food has been used before otherwise simply show "???"
  * :x: Add screen shake when the player is hit
  * :x: Don't spawn monsters in a room if the player is spawning in that room

## #51 - What now? ([link](https://youtu.be/9BMSGNd39Uk))

* This is the end of the tutorial - mostly a discussion about the game's design:
  * There's too much items, it feels wasteful how much you can throw them away
  * The stun didn't work well and probably should be for 2 turns
  * Some of the enemies were boring and didn't add anything new to the game
  * The "hallway issue": being trapped in a hallway with one of the tougher monsters will almost always get you killed - player needs more solutions to that problem...
  * Talks about item variety: try to make every item do something unique rather than for example, just increasing damage on weapons
  * Think of some items that can fix Zugzwang
  * There are not enough systems in the game and the ones we have can be more interconnected:
    * Line of sight
    * AI
    * Mobs
    * Armour / Weapons
    * Food
    * Map
    * Status
  * Ideas for other systems should try to add more variety and more connections between them
  * Think of ways to provide more map variety
  * Maybe reconsider the enemy design to match the food theme
  * Some discussion about the PICO-8 token limit

## #52 - Game Launch ([link](https://youtu.be/MQCF6GFz96E))

* This video gives a tour of the final game release
  * Almost exactly a year after the end of the tutorial
  * There are many major changes / new systems
  * You can watch it for some interesting thoughts on how to make a real polished game out of the tutorial, but I wouldn't consider trying to make all the same changes as part of the tutorial
