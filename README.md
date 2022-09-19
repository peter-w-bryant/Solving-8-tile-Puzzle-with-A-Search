# Solving-8-tile-Puzzle-with-A-Search
## Description
This program uses A* search algorithm to solve instances of 8-tile puzzle games, requiring state space generation given a configuration of a 3x3 grid of 7 numbers and 2 black spaces.

## An Example

If my program receives as input a <b>state</b>, which is just a list of integers such as <i>[2, 5, 1, 4, 3, 6, 7, 0, 0]</i>, my program interprets every three integers as elements of a row of an 8-tile board with '0' denoting blank spaces. Thus my example state represents the following 8-tile board,

![demoConfig1](https://user-images.githubusercontent.com/72423203/190935228-c66cfeae-1714-4235-8641-b028cac22f26.png)


In this case, moving one tile can result in one of the following possible states,

![demoConfig2](https://user-images.githubusercontent.com/72423203/190934654-7e7f3eea-4365-4c5e-8d62-068f2d294f83.png)

Here, the left state is if we chose to move the 3 tile down, the middle state is if we chose to move the 6 tile down, and the right state is if we were to move the 7 tile right. These configurations are those successor states for which we can achieve after one move from our initial input state - it should be clear from here that the process of generating the successor states from these three new states can be repeated indefinitely. The goal of my program is to thus, first generate a list of all successor states (or a state space for the initial configuration), and then to solve the puzzle using the A* search algorithm.

## The Goal State

In order to "solve" the 8-tile puzzle, it is necessary to specify the <b>goal state</b> of the puzzle. The goal state of the puzzle is,

<i>[1, 2, 3, 4, 5, 6, 7, 0, 0]</i>

which can be depicted visually as,

![goalConfig](https://user-images.githubusercontent.com/72423203/190935101-3b564c34-3773-4a69-83d3-db5d24749a20.png)

Additionally, the way I have implemented the program allows the user to specify the goal state to be anything they choose. However, the default goal state is as it is above.

I will be ommitting the proof, but it should be said that every initial state is <b>solvable</b> in our case. In a version of this game that uses 8 numbers and 1 space, the solvability of an initial state is dependent on weather the number of inversions in the input state is odd, but this will not be a factor for this program.


 solve([6, 0, 0, 3, 5, 1, 7, 2, 4], goal_state=[1, 2, 3, 4, 5, 6, 7, 0, 0])
