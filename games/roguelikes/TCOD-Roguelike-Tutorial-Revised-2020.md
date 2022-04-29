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
* :x: (OPTIONAL) Choose an existing tileset to use (if you want to focus on the code / game design)
* :x: (OPTIONAL) Consider joining something like the [7DRL Challenge](https://itch.io/jam/7drl-challenge-2022) for extra motivation

## Part 1 - Drawing the '@' symbol and moving it around ([link](http://rogueliketutorials.com/tutorials/tcod/v2/part-1))

* :x: Code "hello world"
* :x: Replace printing "hello world" with displaying your character (`@` or a tile)
* :x: Code a way for the user to quit the application
* :x: (OPTIONAL) Make some basic items easily configurable (screen width, screen height, tileset)
* :x: Decide on a movement scheme (e.g. orthogonal, orthogonal+diagonal, something unique)
* :x: Implement moving the player character across the screen

## Part 2 - The generic Entity, the render functions and the map ([link](http://rogueliketutorials.com/tutorials/tcod/v2/part-2/))

* :x: Implement a more generic "Entity" that can represent the player as well as any NPC units
* :x: Make it possible to colour entities (or visually distinguish them from each other in some other way)
* :x: Implement a tile-based map
* :x: Implement collision detection to prevent entities moving through impassible tiles
