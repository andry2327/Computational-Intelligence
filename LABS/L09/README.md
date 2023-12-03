# LAB9

The following solution was developed together with [Lorenzo Tozzi](https://github.com/anubis09/Computational-Intelligence).

The evolution strategy we implemented follows these steps for each generation:
- Parent selection: with a variable tournament size (default value 3).
- Uniform crossover: we always apply crossover to two parents.
- Mutation: we apply mutation with a certain probabiity to the result of the crossover operation.
- Survival selection: select the best ```population_size``` between population and offsprings.

One can choose two different implementations of the evolution algorithm and two different mutation strategies.
The evolutionary algorithm creates generations until the optimal fitness value remains constant for a specified number of generations.

## Classic EA
This is just the implementation of the steps described above.

## Island model
We created a given number of islands where an island is a population itself. We evolve each island independently for a given number of generations (regulated by ```migration_frequency``` parameter), after that we remove a certain amount of population from each island and we migrate them to a random island. 

## Bit flip mutation
If mutation occurs, we itereate through the genotype and with a given probability (```Ea.__bit_change```), we flip the gene.

## Bit assign mutation
If mutation occurs, we choose the value (0/1) to assign based on a given probability (```Ea.__prob_to_set_1```). 
we itereate through the genotype and with a given probability (```Ea.__bit_change```), we assign the value to the gene.
The mutated individual is evaluated and if it's better than the parent, we increment a counter for the value assigned (```Ea.__better_with_0_1```). 
At the end of whole generation, ```Ea.__prob_to_set_1``` is self adjusted based on the performance of the bit assigned.

# Results
