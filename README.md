# Solving-8-tile-Puzzle-with-A*-Search
## Description
This program uses A* search algorithm to solve instances of 8-tile puzzle games, requiring state space generation given a configuration of a 3x3 grid of 7 numbers and 2 black spaces.

## An Example

If my program receives as input a <b>state</b>, which is just a list of integers such as, 

<i>[2, 5, 1, 4, 3, 6, 7, 0, 0]</i>

my program interprets every three integers as elements of a row of an 8-tile board with '0' denoting blank spaces. Thus my example state represents the following 8-tile board,

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

## Defining a Heuristic
Since I am using the A* search algorithm, I needed to define a <b>heuristic function</b> h(s) in order to evaluate different states. For my program I just decided to use the sum of the L1-Norm of each tile to its goal position as h(s); thus the L1-norm of two tiles in this case is the absolute difference between their x coordinates plus the absolute distance between their y coordinates. There are a number of different heuristic functions I could have chosen, however this one serves my purpose  well for this simplified version of 8-tile.

In the example puzzle, the initial state is,

s = <i>[2, 5, 1, 4, 3, 6, 7, 0, 0]</i>  and  <i>h(s) = 6</i>

In this case h(s) is computed by calculating the L1-Norm of each tile to the goal and summing all of them. We can see that tiles 4, 6, and 7 are already in the place where they will end up in our goal state, so they have L1-Norm equal to 0. Tile 1 has an L1-norm of 2,

<i>L1-Norm([0,2],[0,0]) = abs(0-0) + abs(2-0) = 2</i>

I will omit computing the L1-Norm of the remaining tiles but if you were to check tiles 2, 3, and 5 they have L1-Norms of 1, 2, and 1 respectively. I think it is important to add that I do not count the distance of tiles with the value '0' since they are not actually representing tiles but rather empty sections of the puzzle.

## Functions
This program contains two functions written in Python,

<ol>
 <li>print_succ(state) — given a state of the puzzle, represented as a single list of integers with a 0 in the empty spaces, prints to the console all of the possible successor states and h(s) for that particular state.</li>
 <li>solve(state) — given a state of the puzzle, performs the A* search algorithm and prints the solution path from the current state to the goal state and h(s) for each intermediate state up to the goal state. This function also takes into account a cost function g(n), which is simply the total number of moves so far - meaning every valid successor has an additional cost of 1. </li>
</ol>

## Running the Program and Sample Output

You can run the program yourself by downloading this repo, writing solve(<i>state</i>) in the main function of solve_puzzle.py, and executing the script. For example, to run the initial example state add, 

<i>solve([2, 5, 1, 4, 3, 6, 7, 0, 0])</i>

to the main function and execute the script with 

<i> python3 solve_puzzle.py </i>

The result of running the script with this initial state is, 

[2, 5, 1, 4, 3, 6, 7, 0, 0] h=6 moves: 0
[2, 5, 1, 4, 3, 0, 7, 0, 6] h=7 moves: 1
[2, 5, 1, 4, 0, 3, 7, 0, 6] h=6 moves: 2
[2, 0, 1, 4, 5, 3, 7, 0, 6] h=5 moves: 3
[0, 2, 1, 4, 5, 3, 7, 0, 6] h=4 moves: 4
[0, 2, 1, 4, 0, 3, 7, 5, 6] h=5 moves: 5
[0, 0, 1, 4, 2, 3, 7, 5, 6] h=6 moves: 6
[0, 1, 0, 4, 2, 3, 7, 5, 6] h=5 moves: 7
[0, 1, 3, 4, 2, 0, 7, 5, 6] h=4 moves: 8
[0, 1, 3, 4, 2, 6, 7, 5, 0] h=3 moves: 9
[1, 0, 3, 4, 2, 6, 7, 5, 0] h=2 moves: 10
[1, 2, 3, 4, 0, 6, 7, 5, 0] h=1 moves: 11
[1, 2, 3, 4, 5, 6, 7, 0, 0] h=0 moves: 12
