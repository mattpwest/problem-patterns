# TCOD Roguelike Tutorial Revised (2020)

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
* :x: (OPTIONAL) Choose an existing tileset to use (if you want to focus on the code / game design)
* :x: (OPTIONAL) Consider joining something like the [7DRL Challenge](https://itch.io/jam/7drl-challenge-2022) for extra motivation

## #2 - Basic Movement ([link](https://youtu.be/SoFOva5FUnI))

* :x: Draw the player character idle / walk animation frames
* :x: Draw a wall tile
* :x: Draw a ground tile
* :x: Draw stairs tiles
* :x: Design a simple map for initial testing
* :x: Code loading the designed map (or define it in code for now)
* :x: Code initial main game state (figure out how to switch states later when you have more)
* :x: Code drawing the map on screen
* :x: Code drawing the player character on screen
* :x: Design character movement (orthogonal, diagonal, both, something unusual?)
* :x: Code moving the player character on screen
* :x: Code recoloring of sprites from code

## Somewhere in the future...

* :x: Code animation of the character or other animated tiles