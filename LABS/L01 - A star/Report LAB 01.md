# LAB1 - A* search

I first tried to implement a new distance function for the A* search method, called `distance_A_star`: this function has the goal to create a score associated to each state that will be used to compare states in the priority queue of the frontier. 

The first attempt to implement this function was to return 2 metrics: 

- distance from the goal (i.e. how many elements need to be covered yet until the goal is reached).
- `n_overlaps`: it tells how many overlaps (of True values) exists in a state, implemented in function `get_n_overlaps`. Given 2 state with same distance from the goal, the purpose of this metric is to give priority to the state which has less overlaps.

I tried to combine this 2 metrics in different ways to create a unique value that can be used as comparison in priority queue: summing them (`distance+n_overlpas`), give more importance to the distance instead of the number of overlaps (`distance**2 + n_overlpas`, or using some weights: `w1*distance + w2*n_overlpas, w1>w2`). The results did not show any significant improvement.

When we were shown the new notebook `set-covering_path-search.ipynb`, which contains a comparison of all algorithms, I changed the structure of `distance_A_star`:

- I implemented a cost function `g`: It simply tells how many element are already covered in a state.
- I created a custom `h` functions that estimates the distance from the goal in a different way: it generates an optimistic heuristic on how distant a state is from the goal trying find a set that better fits into the remaining False position that are not already covered. So it tries to fully cover the remaining False positions with a specific set and return the difference between the number of False tiles to cover and the number of True tiles in the set that best cover that tiles.

I made some optimizations to avoid adding to the frontier sets that contains only False values, since they do not help in reaching out goal and only slow down our search.

So the final `distance_A_star` function includes 3 metrics: `g` cost function, `h` estimated cost function and `n_overlaps`(normalized by the `PROBLEM_SIZE`). It is possible to give different weights to these 3 terms setting different values for `w1`, `w2` and `w3`.

Here’s some results:

![SCR-20231025-osot.png](LAB1%20-%20A%20search%206548cdab3fb749d89385332ae4e35c31/SCR-20231025-osot.png)

![SCR-20231025-oueu.png](LAB1%20-%20A%20search%206548cdab3fb749d89385332ae4e35c31/SCR-20231025-oueu.png)

![SCR-20231025-pdcv.png](LAB1%20-%20A%20search%206548cdab3fb749d89385332ae4e35c31/SCR-20231025-pdcv.png)

I also implemented a section in which it is possible to run N (`SIM_ITER` in code) simulations to compare 2 different algorithm. For each simulation it computes a score of the algorithm performances based on number of steps to reach the solution, number of tiles used, numbers of overlaps, and time elapsed. An higher score means better performances of the algorithm.