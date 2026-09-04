# Enhanced Autonomous Navigation Using Reinforcement Learning

## Overview

This project presents an enhanced reinforcement learning approach for autonomous navigation in a grid-based environment. The implementation evaluates and compares **Q-Learning** and **Deep Q-Network (DQN)** and extends the experiments with hyperparameter sensitivity, grid scalability, and dynamic obstacles.

The project is implemented in Python using a Jupyter Notebook.

## Objectives

- Compare Q-Learning and DQN for autonomous navigation.
- Analyze the effect of the learning rate (α).
- Analyze the effect of the exploration rate (ε).
- Evaluate performance as the grid size increases.
- Investigate navigation with dynamic obstacles.
- Visualize learning curves and learned navigation policies.

## Environment

The navigation problem is implemented using a **10 × 10 GridWorld** environment.

The environment contains:

- A start position
- A goal position
- Fixed obstacles
- Four actions: Up, Down, Left, Right

### Reward Structure

| Event | Reward |
|---|---:|
| Reaching the goal | +100 |
| Collision with an obstacle | -100 |
| Normal movement | -1 |

Each episode is limited to **200 steps**.

## Algorithms

### Q-Learning

- Learning rate (α): `0.10`
- Discount factor (γ): `0.90`
- Exploration rate (ε): `0.10`
- Training episodes: `1000`
- Number of runs: `20`

### Deep Q-Network (DQN)

- Hidden layers: `2`
- Neurons per hidden layer: `64`
- Activation: ReLU
- Optimizer: Adam
- Learning rate: `0.001`
- Discount factor (γ): `0.90`
- Exploration rate (ε): `0.20`
- Replay buffer: `50,000`
- Batch size: `64`
- Training episodes: `500`
- Number of runs: `5`

## Experimental Setup

Performance is evaluated using:

- Success rate
- Successful path length
- Convergence episode
- Training rewards
- Learned greedy policies

The convergence criterion is the first episode at which the **50-episode moving average of returns exceeds 50**.

## Experiments

### 1. Baseline Q-Learning vs DQN

The baseline experiment compares Q-Learning and DQN on the fixed 10 × 10 grid environment using success rate, path length, convergence, learning curves, and greedy navigation paths.

### 2. Learning-Rate Sensitivity

Q-Learning is evaluated using:

```text
α = 0.01, 0.05, 0.10, 0.20, 0.50
```

### 3. Exploration-Rate Sensitivity

Q-Learning is evaluated using:

```text
ε = 0.05, 0.10, 0.20, 0.30, 0.50
```

### 4. Grid Scalability

Q-Learning is evaluated on:

```text
10 × 10
15 × 15
20 × 20
```

### 5. Dynamic Obstacles

A moving obstacle is introduced to create a changing environment. The dynamic-obstacle experiment achieved a mean success rate of **62.20%** across three runs. None of the three runs reached the convergence threshold within 500 episodes.

## Key Results

### Baseline Results

| Metric | Q-Learning | DQN |
|---|---:|---:|
| Success Rate | 98.99% ± 0.14% | 49.72% ± 17.61% |
| Successful Path Length | 26.41 ± 20.92 steps | 72.79 ± 49.66 steps |
| Convergence | 152.55 ± 13.65 episodes | 396.67 ± 49.08 episodes* |

*DQN convergence was observed in 3 of the 5 runs within the training horizon.

The tested Q-Learning configuration achieved substantially higher success and shorter successful paths than the tested DQN configuration on the fixed grid environment.

## Learning-Rate Results

At α = 0.50, the experiment achieved approximately **99.47% success** with approximately **24.40 successful steps**.

The observations are experimental results and are not formal statistical significance tests.

## Exploration-Rate Results

The observed results show that:

- Success rates remained relatively high across the tested exploration rates.
- Lower exploration generally produced shorter successful paths in the stationary environment.
- Higher exploration could delay convergence.
- At ε = 0.50, the observed mean successful path length increased to approximately **47.52 steps**, with convergence not reached within the 500-episode sensitivity experiment.

## Grid Scalability Results

| Grid Size | Success Rate | Mean Successful Steps | Convergence |
|---|---:|---:|---:|
| 10 × 10 | 98.13% | 30.92 | 148.33 episodes |
| 15 × 15 | 96.27% | 85.87 | 416.00 episodes |
| 20 × 20 | 96.13% | 182.07 | Not reached |

Increasing the grid size substantially increases navigation difficulty. Although success rate decreases only moderately, successful path length increases significantly and convergence becomes slower.

## Dynamic-Obstacle Results

- Grid size: 10 × 10
- Training episodes: 500
- Number of runs: 3
- Learning rate: 0.10
- Discount factor: 0.90
- Exploration rate: 0.10
- Mean success rate: **62.20%**

Individual run success rates:

- Run 1: 62.2%
- Run 2: 62.8%
- Run 3: 61.6%

None of the three runs reached the convergence threshold within 500 episodes.

## Visualizations

The notebook contains visualizations for:

- GridWorld environment
- Fixed obstacle configuration
- Training and learning curves
- Q-Learning and DQN performance
- Greedy policy paths
- Learning-rate sensitivity
- Exploration-rate sensitivity
- Grid scalability
- Dynamic-obstacle navigation

## Project Structure

```text
Enhanced-Autonomous-Navigation-RL/
│
├── Enhanced_Autonomous_Navigation_RL.ipynb
│
└── README.md
```

The Jupyter Notebook contains the complete implementation, experiments, results, and visualizations.

## Requirements

```text
numpy
pandas
matplotlib
scikit-learn
tensorflow
jupyter
```

## How to Run

### 1. Clone the Repository

```bash
git clone https://github.com/vindyakiran90/Enhanced-Autonomous-Navigation-Reinforcement-Learning.git
```

### 2. Open the Project Directory

```bash
cd Enhanced-Autonomous-Navigation-RL
```

### 3. Install the Required Libraries

```bash
pip install numpy pandas matplotlib scikit-learn torch jupyter
```

### 4. Start Jupyter Notebook

```bash
jupyter notebook
```

### 5. Open the Notebook

```text
Enhanced_Autonomous_Navigation_RL.ipynb
```

### 6. Run the Notebook

Run the cells sequentially from beginning to end to reproduce the experiments, results, and visualizations.

## Reproducibility

Random seeds are used in the experiments to improve reproducibility.

The notebook contains:

- Environment implementation
- Q-Learning implementation
- DQN implementation
- Training procedures
- Evaluation procedures
- Hyperparameter sensitivity experiments
- Grid scalability experiments
- Dynamic-obstacle experiments
- Result calculations
- Visualizations

The reproduced DQN success rate is **49.72%**, while the reference paper reports **52.52%**. The reproduced convergence behavior also differs from the reference report.

Therefore, this implementation should be considered an **independent Python reproduction under the documented experimental assumptions**, rather than an exact reimplementation of every original experimental detail.

## Limitations

- The environment is a relatively small discrete grid-world benchmark.
- The main Q-Learning and DQN configurations are not exhaustively hyperparameter-tuned.
- DQN uses five runs, while Q-Learning uses twenty runs.
- The dynamic-obstacle experiment uses a simplified moving-obstacle scenario.
- Formal statistical significance testing is not included.
- The 18-step greedy path is a single demonstration and does not represent aggregate path statistics.
- Real-world vehicle dynamics are not modeled.
- Sensor noise is not modeled.
- Localization errors are not modeled.
- Perception uncertainty is not modeled.
- Continuous control is not considered.

## Future Work

- Extend the environment to continuous state and action spaces.
- Incorporate realistic vehicle dynamics.
- Use prioritized or improved experience replay.
- Perform systematic DQN hyperparameter optimization.
- Compare Double DQN and Dueling DQN.
- Investigate curriculum learning for larger environments.
- Investigate transfer learning for larger maps.
- Introduce multiple dynamic obstacles.
- Introduce stochastic obstacle movement.
- Evaluate robustness under sensor noise.
- Investigate partial observability.
- Compare learned policies with A* and Dijkstra algorithms.
- Perform statistical significance testing.
- Report confidence intervals using larger independent samples.
- Deploy the navigation policy in a simulated or physical vehicle platform.

## Reference

Z. H. A. Aldahlaki, H. F. Hadi Kaze, S. S. Jabbar, and R. S. Hassan, "Comparison of Q-Learning and Deep Q-Network for Autonomous Navigation in Grid-Based Environments," Journal of Theory, Mathematics and Physics, vol. 5, no. 4, 2026.

Additional theoretical foundations:

- E. W. Dijkstra, "A note on two problems in connexion with graphs," *Numerische Mathematik*, vol. 1, pp. 269–271, 1959.
- P. E. Hart, N. J. Nilsson, and B. Raphael, "A formal basis for the heuristic determination of minimum cost paths," *IEEE Transactions on Systems Science and Cybernetics*, vol. 4, no. 2, pp. 100–107, 1968.
- C. J. C. H. Watkins and P. Dayan, "Q-learning," *Machine Learning*, 1992.
- V. Mnih et al., "Human-level control through deep reinforcement learning," *Nature*, 2015.
- R. S. Sutton and A. G. Barto, *Reinforcement Learning: An Introduction*, 2nd ed., MIT Press, 2018.

## Author

**Vindya Kiran Jain**

## Academic Purpose

This repository is created for academic and educational purposes as part of a reinforcement learning study on autonomous navigation.

The notebook demonstrates the implementation, evaluation, and analysis of reinforcement learning algorithms for grid-based autonomous navigation.
