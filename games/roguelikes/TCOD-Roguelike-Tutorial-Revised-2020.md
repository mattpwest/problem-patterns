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

## TODO: Parts 3 - 8 

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
