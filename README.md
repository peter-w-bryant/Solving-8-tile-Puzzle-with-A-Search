# Solving-8-tile-Puzzle-with-A-Search
## Description
Implemented A* search algorithm to solve instances of 8-tile puzzle games, requiring sorting different configurations of a 3x3 grid of 7 numbers and 2 black spaces.

## An example

If my program receives as input a <b>state</b>, which is just a list of integers such as <b>[2, 5, 1, 4, 3, 6, 7, 0, 0]</b>, my program interprets every three integers as elements of a row of an 8-tile board with '0' denoting blank spaces. Thus this state represents this 8-tile board,

![demoConfig1](https://user-images.githubusercontent.com/72423203/190934505-3bfac3ea-0578-4897-8071-de3b2b87b94f.png)


 solve([6, 0, 0, 3, 5, 1, 7, 2, 4], goal_state=[1, 2, 3, 4, 5, 6, 7, 0, 0])
