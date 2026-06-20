15. Reflection Questions

15.1 Problem Formulation
What is a state in this lab?
A state is a position on the grid, represented as a pair (row, column).

What is an action?
An action is a move from one cell to another, like moving up, down, left, or right.

What does the result function do?
The result function takes a state and an action, then returns the new state after that action. For example, if I am at the state (1, 1) and move down, the result returns to state (2, 2).

Why is it useful to separate the problem definition from the search algorithm?
It lets us use the same search algorithms on different problems. We can solve grid puzzles, mazes, or other problems without changing the search code.

15.2 BFS
Why does BFS use a FIFO queue?
FIFO means First-In-First-Out. BFS uses this, so it explores nodes in the order they were added. This makes it check all nodes at depth 0, then depth 1, then depth 2, and so on.
Why does BFS find the shortest path in terms of number of steps on the unweighted grid?
BFS finds the shortest path in terms of number of steps on the unweighted grid, because each move costs 1. It checks all nodes at depth d before checking depth d+1. So the first goal it finds is at the smallest depth, and that is considered the shortest path.
What role does the reached set play in BFS?
The reached set keeps track of states we have already visited, and stops the BFS from going back to the same cell again. 

15.3 DFS
Why does DFS use a stack?
Stack means Last-In-First-Out (LIFO). DFS uses it to explore the most recent node first. This makes it go deep down one path before trying other paths.

Is DFS guaranteed to find the shortest path? Explain.
No. DFS goes deep down one path and might find a long path before finding a shorter one, and it returns the first goal it finds, not necessarily the shortest; it can be the longest or shorter than that.

Under what conditions can DFS use less memory than BFS?
DFS only stores the current path and its siblings. In a very deep tree with few branches, DFS uses much less memory than BFS, which stores all nodes at the current depth.

Under what conditions can DFS perform badly?
DFS can perform badly when there are many dead ends or when the goal is shallow, but DFS goes deep into a wrong branch first. It can also get stuck in infinite loops without cycle checking.


15.4 DLS

What happens when the depth limit is too small?
If the limit is smaller than the solution depth, DLS will not find the goal. It will return "cutoff" instead of success.

What is the meaning of "cutoff"?
Cutoff means the search reached the depth limit before finding the goal. It does not mean failure, but there might still be a solution deeper than the limit.

How is DLS different from ordinary DFS?
DFS has no depth limit. It keeps going deeper until it finds a goal or runs out of nodes. DLS stops searching deeper once it hits the depth limit.

Why do we use path-cycle checking in DLS?
Path-cycle checking stops DLS from going in circles on the same path, and it checks if a child state is already on the current path. If yes, it skips that child to avoid repetitions.


15.5 IDS

Why does IDS repeat DLS with increasing limits?
IDS starts with a limit of 0, then goes to 1, then 2, and so on. It does this to find the most superficial goal without using too much memory.

Why can IDS be complete even though DLS with a small limit is not?
As the limit increases, IDS eventually reaches the depth of the solution. When the limit is big enough, DLS will find it. So IDS will always find a solution if one exists.

Why does IDS use less memory than BFS?
IDS uses DLS, which uses DFS memory because it only stores the current path. BFS stores all nodes at the current depth, which can be much larger.

What is the cost of repeatedly searching from the root?
IDS re-expands nodes many times. For example, a node at depth n is expanded n times; so it costs extra time but saves memory.


15.6 Real-World Drone Context

In a real drone application, what might make one route safer or more practical than another?
For this, I think a path with more open space or fewer obstacles is better when considering things like wind, battery life, and no-fly zones, which can make the route safer. 

Which algorithm would you choose if all moves are equally costly and you only care about the fewest number of moves? Explain.
I would use the BFS algorithm, since it always finds the shortest path in terms of number of steps when all moves cost the same.

Which algorithm would you choose if you want to limit how deep the drone is allowed to search? Explain.
I would use a DLS because it has a depth limit, so the drone will not go beyond that depth, especially if the drone cannot fly too far or if time is limited.

What limitations does this grid model have compared with real drone navigation?
The grid model is simple. It does not have continuous movement, different heights, obstacles that move, weather, or limited battery life. Real drone navigation needs to handle many more factors.

