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

TODO

## Part 6 - Doing (and taking) some damage ([link](http://rogueliketutorials.com/tutorials/tcod/v2/part-6/))

TODO

## Part 7 - Creating the Interface ([link](http://rogueliketutorials.com/tutorials/tcod/v2/part-7/))

TODO

## Part 8 - Items and Inventory ([link](http://rogueliketutorials.com/tutorials/tcod/v2/part-8/))

TODO

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
