16.Reflection Questions

16.1 Heuristic Functions
In your own words, what does h(n) estimate, and where does its "knowledge" come from in this lab?
h(n) guesses how far the current cell is from the goal, and the knowledge comes from the grid coordinates. 

Manhattan distance is the exact solution cost of a relaxed problem. Which restrictions of the original drone problem does that relaxation remove?
The relaxation removes the obstacles. So, it acts like the drone can fly straight through walls and blocked cells, because it only cares about moving up, down, left, and right.

Both Manhattan and Euclidean distance are admissible on our grid. Which one dominates the other, and what does domination predict about nodes expanded?
Manhattan dominates Euclidean because it gives bigger guesses or fewer nodes that are still safe. 

Why does requiring all terrain costs to be ≥ 1 keep Manhattan distance admissible on the weighted maps? What could go wrong with a terrain cost of 0.5?
If all costs are 1 or more, Manhattan gives a guess that is less than or equal to the real cost. If a terrain cost is 0.5, the real cost could be smaller than the guess. Then the guess would be too high and not safe.


16.2 Greedy Best-First Search
Which quantity does Greedy ignore, and how did the turbulence map punish it for that?
Greedy ignores the cost to reach the current cell. The turbulence map punished this because Greedy might pick a path that looks short but has a high turbulence cost, and ignores that some routes cost more to fly through.

Greedy expanded fewer nodes than A on some maps. Why is that not enough to call it the better algorithm?
Even when expanding fewer nodes, it does not make it better because the path might be longer or more costly. Greedy finds a solution fast, though it’s not always the best one.

Describe a drone mission where Greedy's behaviour would actually be acceptable.
If the drone needs to move fast and any path is okay, like flying over empty land. It does not need the shortest path. It just needs to get there quickly.


16.3 A Search*
Explain f(n) = g(n) + h(n) as a sentence about the drone's flight plan.
f(n) is the total guess of how far the drone has already flown, plus how far it still has to go.

Why must A apply the goal test when a node is popped rather than when it is generated? What could go wrong with an early goal test on the turbulence map?
If A* checks the goal when it first sees it, the path might not be the best one. On the turbulence map, it might find a path early, but that could surely be very costly.

Why does reached need to be a dictionary (state → best node) in this lab, when a plain set was enough for BFS in Part A?
The A* needs to store the best cost for each state; that’s why it finds a cheaper way to reach a state later, and it updates it. 

Compare the nodes expanded by UCS and A on the sample map. What does this gap tell you about the value of the heuristic?
A* expands fewer nodes than UCS. The gap shows that the heuristic is helpful. It guides the search toward the goal faster.


16.4 Admissibility and Consistency
State the definitions of admissible and consistent. Which implies which?
Admissible means the guess is never too high and is always less than or equal to the real cost. Consistent means the guess follows the triangle rule: h(n) ≤ cost + h(next), and it also implies admissible.

What did your inadmissible-heuristic experiment show about the lecture's optimality claim?
When the heuristic is not admissible, A* is not guaranteed to find the best path. The claim that A* is optimal only works if the heuristic is admissible.

Is Manhattan distance consistent on our unit-cost grid? Check the triangle inequality h(n) ≤ c(n, a, n') + h(n') for a single move and explain.
Yes. For one move, h(n) goes down by 1 and c is 1. So h(n) = 1 + h(next). This is equal to c + h(next). So the rule holds.


16.5 Weighted A and Trade-offs
How does the weight W interpolate between UCS, A*, and Greedy?
When W is 0, it is UCS. When W is 1, it is A*. When W is very big, it acts more like Greedy.

What suboptimality bound does Weighted A guarantee, and did your experiments stay well inside that bound?
Weighted A* guarantees the path cost is no more than W times the optimal cost. The experiments likely stayed within that bound.

The drone has 90 seconds of battery margin and the flight computer is slow. Which algorithm and which W would you choose, and why?
I would choose Weighted A* with W=2. It finds a path faster than A* but still gives a path that is not too bad. It saves time for the slow computer.


16.6 Memory and Real-World Drone Context
Which data structures make A memory-hungry? How does IDA (bonus) avoid this, and what does it pay instead?
The frontier and reached dictionary use a lot of memory. IDA* does not store all nodes. It uses less memory but pays with more time because it re-expands nodes.

In a real drone application, what information would you fold into the terrain costs that this lab leaves out (weather forecasts, no-fly zones that change over time, battery state)?
I would add wind speed, rain, temperature, restricted areas, and how much battery is left. These all change how safe or costly a path is.

Our heuristic assumes the goal never moves. What breaks if the drone is tracking a moving target, and which lecture concepts (e.g., learned heuristics, real-time search) become relevant?
The heuristic would no longer work because the goal keeps changing. Real-time search and learning the heuristic from experience would help the drone adjust to the moving goal.

Which single algorithm from Parts A and B combined would you ship on the drone, and under what conditions would you reconsider?
I would ship A* because it finds the best path when all costs are known. I would reconsider if the map is very large and the memory is small. Then I would use IDA* or Weighted A* to save the memory.

