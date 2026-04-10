# Traveling Salesman Optimization using Genetic Algorithms

Implementation of a route optimization workflow that solves the Traveling Salesman Problem (TSP) using a Genetic Algorithm (GA), with explicit focus on system design decisions and reproducible experimentation.

## Overview

This project implements an AI-driven combinatorial optimization pipeline for TSP, where the objective is to find a minimum-distance closed tour across a fixed set of cities.

The implementation is built as an end-to-end optimization system, not only a model-training exercise:

- Ingests structured city nodes and coordinates.
- Encodes candidate routes as valid permutations.
- Iteratively improves route quality through selection, crossover, mutation, and replacement.
- Exposes measurable outputs (best route and total tour distance) for decision support.

Real-world use cases:

- Last-mile logistics route planning.
- Field service scheduling for multi-stop technician visits.
- Robotics and autonomous inspection path sequencing.
- Delivery simulation benchmarks for operations research teams.

## Architecture

The workflow follows a deterministic pipeline with stochastic optimization at the core:

Input Layer -> Representation Layer -> Fitness Layer -> Evolutionary Engine -> Output Layer

### Component Design

- Input Layer: Defines the city set and coordinate map.
- Representation Layer: Uses permutation-based chromosomes to guarantee each city is visited exactly once.
- Fitness Layer: Computes closed-tour Euclidean distance and transforms it into fitness using inverse distance.
- Evolutionary Engine:
	- Parent selection via roulette wheel (fitness-weighted sampling).
	- Order-preserving crossover to create valid offspring.
	- Swap mutation with low probability for controlled exploration.
	- Random replacement strategy to maintain population diversity.
- Output Layer: Returns best tour and distance after configured generations.

## Architecture Diagram

![Traveling Salesman Optimization Architecture](./assets/Traveling%20Salesman%20Optimization%20Architecture.png)

## Features

- End-to-end GA pipeline for permutation-based route optimization.
- Constraint-safe route encoding that avoids invalid city duplication.
- Fitness-proportional parent sampling for adaptive search pressure.
- Order-aware crossover strategy to preserve useful subsequences.
- Mutation-driven diversity control to reduce premature convergence.
- Simple notebook workflow for fast iteration and transparent experimentation.

## Model Details

- Model type: Genetic Algorithm for permutation-based combinatorial optimization.
- Why this approach: TSP has factorial search complexity, and GA provides a practical near-optimal search strategy for non-trivial route spaces.
- Optimization approach: Population initialized with random valid tours, then evolved for 100 generations using roulette selection, crossover, mutation, and replacement.
- Evaluation method: Deterministic Euclidean tour distance with closed-loop return to origin city.
- Current configuration: population_size=50, num_generations=100, mutation_rate=0.02.

## Technical Highlights

- System design decision: permutation encoding is used to enforce TSP feasibility by construction.
- Selection strategy: roulette-wheel selection balances exploitation of strong candidates with exploration.
- Crossover design: segment inheritance plus fill-in logic preserves route validity while mixing parent structure.
- Mutation policy: probabilistic index swaps improve exploration without destabilizing convergence.
- Optimization loop design: randomized replacement keeps the population dynamic and computationally lightweight.
- Evaluation approach: exact Euclidean route scoring provides interpretable optimization signals.

## Tech Stack

- Python
- Jupyter Notebook
- Standard library: random
- Core numerical logic: Euclidean distance and permutation operations
- Problem domain: combinatorial optimization (Traveling Salesman Problem)

## Getting Started

### Prerequisites

- Python 3.9+
- Jupyter Notebook or VS Code with Jupyter extension

### Setup

```bash
git clone https://github.com/<your-username>/Traveling-Salesman-Problem.git
cd Traveling-Salesman-Problem
python -m pip install --upgrade pip jupyter
```

### Run

1. Open The Traveling Salesman.ipynb.
2. Execute cells from top to bottom.
3. Review the final printed route and distance.

### Tune Hyperparameters

Update the following variables in the notebook to test convergence behavior and solution quality:

- population_size
- num_generations
- mutation_rate

## Results

Reference output from the current notebook run:

- Best route: [Phoenix, London, Dunedin, Beijing, Tokyo, Victoria, Singapore, Venice]
- Best distance: 32.62002766011951

Interpretation:

- The GA converges to a compact feasible route over 8 cities under the current parameter setting.
- This baseline validates the optimization pipeline and provides a starting point for scaling to larger city sets.
