# Community Detection in Networks using NetworkX

This project focuses on community detection in complex networks using two complementary approaches:

- Classical community detection using the **NetworkX library**

- A **custom-designed Evolutionary Algorithm (EA)** for modularity optimization

The goal is to evaluate how well communities can be detected in real-world networks and compare the quality of solutions offered by traditional graph algorithms versus evolutionary-based search.

## Objectives:

* Load real-world networks from .gml format
* Clean structures with duplicated edges where necessary
* Detect communities using NetworkX (greedy modularity maximization)
* Visualize community structure
* Evaluate quality using modularity
* Implement and test a self-developed evolutionary algorithm capable of discovering community partitions that aim to improve modularity

## 1. Classical Method: NetworkX Community Detection:
The notebook uses the algorithm: **Greedy Modularity Communities (Clauset–Newman–Moore)**

### Workflow:

1. Load GML graph
2. Convert node labels to integers
3. Run greedy_modularity_communities
4. Convert communities to vector representation
5. Compute modularity
6. Visualize communities

This method is fast and effective for many networks, but may fall short when:
* the network is sparse,
* community borders are ambiguous,
* modularity landscape contains many local optima.

## 2. Custom Evolutionary Algorithm (EA):
To address the limitations of classical algorithms, this project implements **from scratch** an evolutionary algorithm that evolves partitions of nodes into communities.
### Representation:
Each individual (chromosome) encodes a solution: genes[i] = community assigned to node i

| Operator       | Implementation                                            |
| -------------- | --------------------------------------------------------- |
| Initialization | Random partitioning into 1…k communities                  |
| Evaluation     | Fitness = modularity                                      |
| Selection      | Tournament selection                                      |
| Crossover      | Uniform crossover with community remapping                |
| Mutation       | Reassign node to another community or introduce a new one |
| Replacement    | Optionally supports **elitism**                           |

### Motivation:
Unlike greedy modularity maximization, the EA:

* explores the search space globally
* can escape local optima
* adapts the number of communities dynamically

This provides an experimental way to determine whether **higher modularity values** can be discovered compared to NetworkX.

## 3. Technologies used:

| Category            | Libraries                        |
| ------------------- | -------------------------------- |
| Graph processing    | NetworkX                         |
| Plotting            | Matplotlib                       |
| Evolutionary method | **Custom Python implementation** |
| Data formats        | GML                              |

## 4. Future Improvements:

* Parallel EA population evaluation for speed
* Multi-objective optimization (e.g., size balance vs modularity)
* Hybrid method: EA initialization with NetworkX result
* Automatic tuning of genetic hyperparameters
* Better crossover and mutation functions