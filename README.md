## Computational Intelligence - Lab2: Traveling Salesman Problem

Repository for the second Lab of the Computational Intelligence course, aiming to find an optimal solution to the Traveling Salesman prioblem. ([Wikipedia](https://en.wikipedia.org/wiki/Travelling_salesman_problem) for more information).

The `TSP.ipynb` file is splitted in two main sections. In then first one an **Evolutionary Algorithm**, implementing *Random Mutation* and *Cycle Crossover*, is used to find a solution. In the second part an **Hill Climbing** algorithm, coming from Lab1, is used to solve the same problem.
Both options proved to fit the task, with the **Evolutionary Algorithm** showing to be the fastest method.

### Evolutionary Algorithm

The first part starts with the creation of a random population using the function `generate_cycle`. It generates apopulation, in which each individual's genome is generated by randomly shuffling a sequence of number whose lenght matches the number of total cities.
The first and last genes are matched, so that the sequence is a proper tour (cycle).

After defining the total *number of generations* and the *offspring size*, the population starts to be "evolved" using an **hypermodern approach** combining mutation and cycle crossover, using the functions `mutation` and `cycle_xover`, respectively. 

The `mutation` function selects a random individual and swap the positions of a couple of genes, at least. The parameter defining the number of swaps is set to *0.1*, so that the genome does not change drastically when mutated (exploitation).

The `cycle_xover` is used to combine genoms of two different individuals (referred as parents):
- Two different genes are selected randomly;
- The genome sequence, going from the first selected gene to the second selected gene, is extracted from *parent 1*, using a `mask`;
- All the genes not belonging to the sequence are extracted, preserving their order, from the genome of *parent 2* (saved in `remainig_genes` list in the code);
- A new genome is created strating from the sequence from *parent 1*, keeping fixed the position of the original genes in the sequence, and arranging the remaining genes, according to their order in the genome of *parent 2*;
- A new individual, the *child*, is associated to the new genome.

Since the algorithm implements an **Hypermodern approach**, the method to generate each child of the current generation is sampled randomly; with both ways, *mutation* and *crossover*, associated with the same probability. 

In each generation, only the top 10 individuals, with the lowest total *path lenght*, are selected to be mutated in the following step.

### Hill Climbing

In the second part a **Steepest Step Hill Climbing**, performing *Simulated Annealing*, is used to find a possible solution to the same problem.

The `tsp_climb` function generates a random initial solution (a random cycle) and, at each step, tweaks the current state using the same `mutation` function of the *Evolutionary Algorithm*.

### Results

Both approaches can achieve good performance in finding a minimal lenght path, but the Evolutionary Algorithm showed to be able to find it in a shorter time, with respect to the Hill Climb method, whch require a lot more steps (and time) to find a similar solution.
