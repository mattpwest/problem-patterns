# TCOD Roguelike Tutorial Revised (2020)

This problem pattern is extracted from http://rogueliketutorials.com/tutorials/tcod/v2/.

Unlike the original tutorial, the focus here is not on guiding you through building a roguelike in Python with LibTCOD. Instead I've tried to extract the requirements for building a fairly feature complete Roguelike into simple TODO lists that you can follow through while choosing your implementation technologies and design patterns.

The following icons can be used to indicate progress as you work through your copy of this file:
 * :x: : not started
 * :warning: : work in progress
 * :no_entry: : skipped / ignored
 * :heavy_check_mark: : finished

Feel free to add your own TODO items as you work through the project.

## Part 0 - Setting Up ([link](http://rogueliketutorials.com/tutorials/tcod/v2/part-0))

* :x: Study any required knowledge about tools or techniques
* :x: Choose and setup your programming language
* :x: Choose and setup your IDE
* :x: (OPTIONAL) Choose and setup your sound tools
* :x: (OPTIONAL) Choose and setup your tile map editing tools
* :x: (OPTIONAL) Choose and setup your art tools (if you want to use a tile-based style)
* :x: (OPTIONAL) Choose an existing tile set to use (if you want to focus on the code / game design)
* :x: (OPTIONAL) Consider joining something like the [7DRL Challenge](https://itch.io/jam/7drl-challenge-2022) for extra motivation

## Part 1 - Drawing the '@' symbol and moving it around ([link](http://rogueliketutorials.com/tutorials/tcod/v2/part-1))

* :x: Code "hello world"
* :x: Replace printing "hello world" with displaying your character (`@` or a tile)
* :x: Code a way for the user to quit the application
* :x: (OPTIONAL) Make some basic items easily configurable (screen width, screen height, tile set)
* :x: Decide on a movement scheme (e.g. orthogonal, orthogonal+diagonal, something unique)
* :x: Code moving the player character across the screen

## Part 2 - The generic Entity, the render functions and the map ([link](http://rogueliketutorials.com/tutorials/tcod/v2/part-2/))

* :x: Code a more generic "Entity" that can represent the player as well as any NPC units
* :x: Make it possible to color entities (or visually distinguish them from each other in some other way)
* :x: Code a tile-based map
* :x: Code collision detection to prevent entities moving through impassible tiles
  * You can temporarily manually put a wall tile next to the player to test 

## Part 3 - Generating a dungeon ([link](https://rogueliketutorials.com/tutorials/tcod/v2/part-3/))

* :x: Prepare everything needed to code the random level generation:
  * :x: Code to fill the map with walls at the start
  * :x: Code to represent a rectangular room
    * Have the coordinates for a room include 2 layers of walls, so you can simply put rooms next to each other and still have a wall between them
  * :x: Code to dig out a room
  * :x: Code to tunnel between two rooms
    * 50% to go horizontal then vertical
    * 50% to go vertical then horizontal
  * :x: Code to check if two rooms overlap
* :x: Code to generate a random level:
  * Define your map parameters, the ones used in the tutorial are:
    * mapWidth: 45?
    * mapHeight: 45
    * roomMaxSize: 10
    * roomMinSize: 6
    * maxRooms: 30
  * Loop for maxRooms:
    * Generate a random room
    * If it overlaps with an existing room discard it be continuing the loop
    * Otherwise:
      * Add it to the room list
      * Dig it out
      * If it's the first room:
        * Place the player in the center of it
      * Otherwise:
        * Dig a tunnel between the new room and the previous room

## Part 4 - Field of View ([link](http://rogueliketutorials.com/tutorials/tcod/v2/part-4/))

* :x: Code an exploration mechanic (instead of just showing the entire map)
  * :x: Store a field of vision (FOV)
    * This can be 1 overlay map or multiple overlay maps depending on how you want to implement it
    * It should store the visibility of each tile, which can be in 1 of 3 states:
      * Not visible
      * Not visible, but previously seen
      * Visible
    * Initialize the entire field of vision to not visible at the start of a level
  * :x: Update map rendering code to use this FOV information:
    * Not visible: don't draw any tiles, items or mobs on this tile
    * Not visible, but previously seen: draw the tile in darker shade than normal
      * Consider if you want to show items or remembered mob positions as well
    * Visible: draw the tile as you used to
  * :x: Code a function to calculate updates to FOV
    * The tutorial uses Python LibTCOD's `tcod.map.compute_fov` [function](https://python-tcod.readthedocs.io/en/latest/tcod/map.html#tcod.map.compute_fov)
    * If you are using a different language, libraries or game engine you may need to code your own - some options are:
      * [Bob Nystrom's Shadow Casting algorithm](https://journal.stuffwithstuff.com/2015/09/07/what-the-hero-sees/)
      * [One of the many FOV algorithms mentioned on Roguebasin](http://www.roguebasin.com/index.php/Field_of_Vision)
  * :x: Use the FOV algorithm to update the FOV:
    * Initially at the start of the level
    * Each time the player character moves

## Part 5 - Placing Enemies and kicking them (harmlessly) ([link](http://rogueliketutorials.com/tutorials/tcod/v2/part-5/))

* :x: Code refactor: move units / entities / mobs to be part of the map so they can be easily stored with the level
  * Ensure the player can be passed as an initial entity to a map for switching levels later
* :x: Code a module that defines all the entities that will currently be in the game:
  * Player: brown @
  * Orc: green o
  * Troll: neon green T
* :x: Code to clone an entity
  * So the entities defined above can be used as templates for all the other entities
* :x: Code spawning of enemies as part of dungeon generation
  * A random number of enemies between 0 to 2 per room should suffice
  * Enemies can be placed at random open positions within the room
  * Spawn enemies with the following chances:
    * 80% chance of an Orc (weaker enemy)
    * 20% chance of a Troll (stronger enemy)
* :x: Code to check for collision with enemies when an entity moves
* :x: Refactor movement code from just a movement action to a bump action which:
  * Checks if there is an entity in the tile an entity is moving to:
    * If yes, attack it
      * For now just print a message saying the player attacked the entity, real combat will be implemented in the next chapter...
    * If no, move into it
* :x: Refactor the main loop to handle enemy entity turns:
  * Keep it simple for now
  * After the player has moved
  * Loop through all non-player entities
    * For now just print out a message saying they acted - AI will be implemented later

## Part 6 - Doing (and taking) some damage ([link](http://rogueliketutorials.com/tutorials/tcod/v2/part-6/))

* :x: Code to add combat information to entities:
  * Hit points
  * Max hit points
  * Attack
  * Defense
* :x: Update the code defining entities to add combat information for all entities:
  * Player:
    * 30 HP
    * 2 Defense
    * 5 Power
  * Orc:
    * 10 HP
    * 0 Defense
    * 3 Power
  * Troll:
    * 16 HP
    * 1 Defense
    * 4 Power
* :x: Code a wait action that entities can use to skip their turn:
  * Add input handling to let the player skip their turn with this
* :x: Code a simple path-finding function to let the entity find a path to a goal tile
* :x: Code to control hostile non-player entities with AI:
  * If the entity is not in the player's vision:
    * Skip their turn
  * Otherwise:
    * If the player is at distance 1, attack them.
    * Otherwise:
      * Calculate a path to the player and move one step towards them
* :x: Code melee combat:
  * `damage = attacker.power - defender.defense`
  * `defender.hp = defender.hp - damage`
  * Print some messages describing what's happening
* :x: Code entities dying:
  * Print a message indicating which entity died
  * Change their display character to a `%` to represent a corpse
  * Change their color to red
  * Change them to no longer block movement
  * Disable their AI (if any)
  * Update their description to `remains of {entity.name}`
* :x: Some fixes that will probably be needed at this point:
  * Ensure the player entity is drawn over all other entities so that it isn't hidden by corpses
  * The player can continue to move around after dying, instead stop accepting any input except quitting the game
* :x: Code some basic placeholder UI (maybe a simple print) to show the player's current and maximum hit points to help test all of this

## Part 7 - Creating the Interface ([link](http://rogueliketutorials.com/tutorials/tcod/v2/part-7/))

* :x: Code a health bar UI (user interface) element to visualize the current player health
* :x: Code a message log UI element to show all the messages on screen
  * Instead of printing to the console as you've probably done until now...
* :x: Code simple mouse look to display the names of monsters when the mouse hovers over them
* :x: Code a second version of the message log for viewing the full history of messages:
  * This can be activated with a key of your choice
  * It should be scrollable with the arrow keys to be able to see all older messages

## Part 8 - Items and Inventory ([link](http://rogueliketutorials.com/tutorials/tcod/v2/part-8/))

* :x: Code for entities to to heal a specified number of hit points
* :x: Code for entities to take damage that bypasses armor
* :x: Code to prevent the player from consuming a resource and losing a turn when that would do nothing useful
  * There are several useful cases that may be implemented:
    * Drinking a health potion while on full health
    * Walking into a wall
    * Walking out of bounds
    * Walking into an entity that cannot be attacked
    * AI attempting to do a nonsensical action should skip their turn and log it for debugging
* :x: Code to represent items as entities:
  * Needed attributes are:
    * Name
    * Character (if text-based)
    * Color
  * Items should be rendered on a different layer: above the floor, but below unit entities
* :x: Code for consumable items:
  * Consumable items apply some effect
  * Then they are destroyed
* :x: Code for a healing potion:
  * A consumable item
  * Which uses the heal function from earlier to heal an entity
* :x: Code to spawn some health potions on the floor during dungeon generation
  * Can be very similar to the logic used to place enemies
  * A random number of potions per room, randomly scattered about the room
* :x: Code to add an inventory that can hold items to an entity:
  * For this tutorial probably only the player needs an inventory, but you could add it on all units
  * Inventory should have functionality to:
    * Add an item
    * Drop an item (move from inventory to floor)
    * List the items in the inventory
  * A typical size for an inventory in text-based roguelikes is 26 items
    * This leaves every item addressable by a letter of the alphabet for quick selection
* :x: Code a grab action:
  * Press a key like `g` for get or `,` (common mapping from older Angband family roguelikes)
  * Pick up the item on the tile (if any), placing it into the inventory
  * If no item is present use the nonsensical action prevention code from earlier to warn the player
* :x: Code an inventory UI that can be displayed by pressing `i`
  * Lists all items in the inventory
  * Try to position the inventory display to not overlap the character
  * Show a selection cursor on the first item
  * Arrow up and down keys can be used to move the cursor
  * On selecting an item prompt the player to select one of the following actions:
    * Drop the item
    * Use the item

## Part 9 - Ranged Scrolls and Targeting ([link](https://rogueliketutorials.com/tutorials/tcod/v2/part-9/))

* :x: Code a Scroll of Lightning which damages a random nearby enemy
* :x: Code a look mode that allows the player to look around the map with the keyboard
* :x: Code a target mode based on the look mode for selecting the target of a scroll
* :x: Code a confusion scroll that can be aimed at a specific entity
* :x: Code a fireball scroll that can be aimed at an enemy or a tile and damages everything in a radius
* :x: (OPTIONAL) Code random spawning of these new items in the level generation code

## Part 10 - Saving and Loading ([link](http://rogueliketutorials.com/tutorials/tcod/v2/part-10/))

* :x: Code a new game state for showing the main menu, with options for:
  * New game
  * Continue game
  * Quit game
* :x: (OPTIONAL) Background image for the main menu to make it look good
* :x: Code to save the game
  * A single save slot is fine for this tutorial
* :x: Code to load the save game
* :x: Code to start a new game
* :x: Code to delete the save game if the player dies

## Part 11 - Delving into the Dungeon ([link](http://rogueliketutorials.com/tutorials/tcod/v2/part-11))

* TODO

## Part 12 - Increasing difficulty ([link](http://rogueliketutorials.com/tutorials/tcod/v2/part-12))

* TODO

## Part 13 - Gearing up ([link](http://rogueliketutorials.com/tutorials/tcod/v2/part-13))

* TODO
