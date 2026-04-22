# Reinforcement Learning Autonomous Driving Agent (7-Day Assessment)

## Context

This repository contains my submission for a 7-day technical assessment focused on training a reinforcement learning (RL) agent for autonomous driving scenarios using the nuScenes dataset.

A key aspect of this assessment was that it required learning reinforcement learning concepts within the same limited timeframe. Prior to this task, I had no formal background in reinforcement learning or machine learning. The objective was therefore not only to build a working solution, but also to demonstrate the ability to quickly understand new concepts and apply them to a complex, real-world problem.

## Problem Overview

The goal of the assessment was to train an RL-based autonomous vehicle agent capable of handling different driving scenarios extracted from the nuScenes dataset, such as:

* Highway driving
* Intersections
* Roundabouts
* Collision / near-miss scenarios

The agent is expected to learn safe, efficient, and smooth driving behavior while interacting with a dynamic environment.

## Approach

### 1. Data Handling and Scenario Representation

* Selected relevant subsets from the nuScenes dataset
* Focused on extracting structured information from high-dimensional inputs (e.g., vehicle state, environment context)
* Simplified representations were used to make the problem tractable within the time constraint

### 2. State and Action Design

* Defined state representations based on available vehicle and environment features
* Considered both continuous and discrete aspects of control
* Actions were designed to approximate realistic vehicle maneuvers

### 3. Reinforcement Learning Method

* Implemented a Proximal Policy Optimization (PPO) agent
* Used policy-based learning to handle continuous control aspects
* Training loop designed to iteratively improve driving behavior

### 4. Reward Function Design

The reward function was constructed to encourage:

* Safe driving (avoiding collisions)
* Lane discipline
* Smooth control inputs
* Forward progress and efficiency

Penalties were incorporated for:

* Collisions
* Lane departures
* Abrupt or unstable movements

### 5. Handling Data Challenges

* Addressed noise and inconsistencies through simplified preprocessing
* Managed missing or sparse information via assumptions and approximations
* Focused on robustness rather than perfect fidelity due to time constraints

### 6. Trajectory Planning and Visualization

* The trained agent is able to follow trajectories within a simulated driving environment
* Outputs include 2D and 3D visualizations (GIFs) demonstrating agent behavior

### 7. Simulation

* Integrated the RL agent within a simulation framework (simplified/custom setup)
* Demonstrated real-time or near real-time trajectory execution

## Results

* A working PPO-based RL agent capable of navigating simplified driving scenarios
* Visualization of agent trajectories (see `/gif` folder)
* Executable Jupyter Notebook for training and evaluation

## Repository Structure

* `Driving_agent_reinforcement_learning.ipynb` – Main notebook containing implementation and explanations
* `gif/` – Contains 2D and 3D trajectory visualizations
* `ppo_agent/` – PPO agent implementation (if applicable)
* `Assessment.pdf` – Original assignment description

## Limitations

Given the 7-day timeframe and the need to learn RL from scratch, several limitations exist:

* Simplified state and environment representations
* Limited hyperparameter tuning
* Partial coverage of all nuScenes complexities
* Simulation environment is not as comprehensive as full-scale platforms like CARLA

These trade-offs were made to prioritize end-to-end functionality and learning within the given constraints.

## Key Takeaways

* Rapid acquisition of reinforcement learning fundamentals (especially PPO)
* Practical experience in designing reward functions for control problems
* Exposure to real-world autonomous driving datasets (nuScenes)
* Understanding challenges in high-dimensional data and simulation integration

## How to Run

1. Download the required subset of the nuScenes dataset (as referenced in the notebook)
2. Install required dependencies
3. Run the Jupyter Notebook:

   ```bash
   jupyter notebook Driving_agent_reinforcement_learning.ipynb
   ```

## Note

This project is best interpreted as a time-constrained learning exercise rather than a fully optimized or production-ready RL system. The emphasis was on problem understanding, rapid implementation, and demonstrating the ability to work with unfamiliar concepts under tight deadlines.
