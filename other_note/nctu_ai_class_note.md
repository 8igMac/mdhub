交大人工智慧概論筆記
===
**授課老師：王才沛**
[toc]

# Deep Neural Network

Before DNNs became popular, most application use networks with just one or two hidden layers.
1. The complexity and danger of overfitting for larger networks.
2. Theoretically, more layers do not increase the _expressize power_(the ability of modeling a given mapping) of a neural network. ([Universal Approximator Theorem](https://www.youtube.com/watch?v=Ijqkc7OLenI))

## A Look at Features
To understand why DNN, especially CNNs(convolutional neural networks), become popular, we need to consider a very important part of supervised leaerning: **Features**.

For many problem, the "raw" features are diffcult to use.
Examples:
- Images
- Speech(audio signal)
- Trajecory(such as online handwriting recognition)
- Text

For problems where it is impractical to use the "raw" features, we need to find a way to extract meaningful and manageable "derived features" from the raw features.

Good features are usually more important than good classifiers/regressors for solving a particular problems.

However, even good hand-crafted features are never good enough.
- They can't capture all the useful information.
- They can only represent the low-level information(easier to define and compute) well. It is very difficult to design features for high-level and sematically rich information.
:::info
To understand this, consider the HOG(Histogram of oriented gradients) features for pedestrain detection. They do not provide us with information regarding whether and where the head, arms, or legs are detected.
:::

## Neural Networks as Features Extractors

It is well known that the outputs of the hidden neurons can be considered as derived features that make the task easier.

**Raw Data** -> **Low-Level Features** -> **Mid-Level Features** -> **High-Level Features** -> **Classifier/Regressor**
This is how our brain processes visual inputs. Yes, this is quite DEEP.

## Convolutional Neural Networks
{%youtube FTr3n7uBIuE %}

# Unsupervised Learning
Dealing with data **without label**, our goal is to group objects into clusters.

In clusting, there are no "correct" or "incorrect" results. We can only look for "informative" or "reasonable" results based on what we know about the data.

**Clusting criterion** is what we want to base the clusting on. For example, by shape or by color.

## K-means
- The most popular and wildly used clusting algorithm. 
- An example of **competitive learning**, a main type of unsupervised learning  method.
- The number of clusters is predetermined(the **k**).
- Clustering representatives(prototypes) required. The standard form use "**mean points**".
- Variations:
    - None-point prototypes
    - Partially overlapping clusters(soft partition)

# Reinforcement Learning
- The task involves a series of action. For a given state, there is no teacher to tell the agent what the "correct" or "optimal" anwser is from the state.
- Feedback (reward/panalty) is available, but not after every action.

## Policy, Reward, and Utility
**Policy**: A policy determines the action to be taken at each state, that is, it is a function from states to actions.
**Reward**: This can be represented as a reward function of a state. Penalties are just negative rewards.
**Utility**: The "expected(期望值) total reward" from a given state to the terminal state. 

:::info
Utility is like the averaged reward of all the possible paths from the given state to the terminal states, weighted by probabilities of the paths.
:::

# Local Search

## Hill-Climbing Search

### Other variation

## Simulated Annealing

## Gentic Algorithms
- **population**: multiple simultaneous search individuals.
- **fitness function**: for evaluating the goodness of an individual.
- Each step of an search is a **generation**
- **crossover**: two individual exchange part of their genes.
- **mutation**: local move of an individual with a small probability.
- **parent selection**: which individuals can pass their genes to the next generation.
- **survival slelection**: removal of worse individuals and addition of newly generated ones.

## Local search in continuous spaces
Our search are limited in dicrete spaces, but the real world is continuous. 
We can:
- Discretize it.
- Solve the equation the find local optima either numerically (like differencial equaltion) or analytically.
- Steepest ascend/descent (hill-climbing)

## Search with no observation
I know the state space, but I don't know where I'm at. 

**Sensorless problem**: The agent has no percept to determine the state.

**Belief state**: Belief state is what the agent "think" the possible state its in. Each belief state contains some real states.

An action from a belief states result in a new belief state containing the real states that can result from applying the action to any of the real states in the original belief state.

Solution can be found by searching the belief-state space.

Example: The vacuum-cleaner have no idea at the begining whether its locaction and the cleaness of the floor.

## Searching with partial observation
Some percept is available. The percept received 







