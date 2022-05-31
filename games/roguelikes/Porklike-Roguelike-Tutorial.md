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
* :x: (OPTIONAL) If necessary, refactor the code to represent the player reusable to also represent monsters
  * I.e. if the player is an object, make it possible to represent monsters with the same type of object
* :x: Draw a slime monster (with 4 frame animation)
* :x: Code spawning the slime monster on the test map
* :x: Code to draw and animate all spawned monsters

## #10 - Mob System ([link](https://youtu.be/CSIHQElMdF0))

* :x: Code a data structure for storing animation frames and switch monster spawning to use it
  * Just storing the first frame may be viable if all animations have the same number of frames
  * If not, store a list of each frame in the animation
* :x: If still necessary, refactor the code to represent, draw and animate the player so that it can also be used for monsters (or mobs)
  * Definition of mob is: mobiles. So players and monsters. Hence, mob system.
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

* :x: (OPTIONAL) Code a way to spawn monsters from map data
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
  * In the tutorial we have 2 equipment slots: weapon, armor
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
  * Items will for now just have a name, e.g. broad sword, leather armor, red potion
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
  * `player.def = 1 + armor?.def`
* :x: Code to replace placeholder stats display with the real values
* :x: Code to make the defense stat randomly reduce damage from incoming attacks:
  * Split stat on items into minimum and maximum defense
  * Add the same fields on the mob and update stats update code
  * E.g. leather armor is 0 - 2 points of damage blocked
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
* :x: Code to carve out random rooms:
  * Minimum width and height of 3 tiles
  * Maximum width and height of 5 tiles
  * Width and height may be different
  * Set initial position to 0,0
* :x: Code to randomly place the room in the level
* WIP TBC...
