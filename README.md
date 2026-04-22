# Reinforcement Learning Autonomous Driving Agent (7-Day Assessment)

## Context

This repository contains my submission for a 7-day technical assessment focused on training a reinforcement learning (RL) agent for autonomous driving scenarios using the nuScenes dataset.

A core requirement of the assessment was to learn the necessary reinforcement learning concepts within the same limited timeframe. This project was therefore completed within 7 days with no prior formal background in reinforcement learning or machine learning. The emphasis was on rapidly understanding new concepts and building a functional, end-to-end solution.

## Problem Overview

The objective was to train an RL-based autonomous vehicle agent capable of handling different driving scenarios extracted from the nuScenes dataset, including:

* Highway driving
* Intersections
* Roundabouts
* Collision / near-miss scenarios

The agent should learn to exhibit safe, smooth, and efficient driving behavior while interacting with realistic driving environments.

## Approach

### 1. Scenario Extraction from nuScenes

Driving scenarios were extracted from the **nuScenes v1.0-mini dataset** using ego vehicle trajectories, semantic maps, and object annotations.

* Semantic map layers (e.g., drivable area, walkways, stop lines) were accessed via nuScenes map expansion
* Ego trajectories were reconstructed from sequential samples
* Near-collision and interaction scenarios were identified using proximity thresholds

Trajectory visualization over semantic maps was used to verify extracted scenarios.

---

### 2. Conversion to Simulation Scenarios

To make the data usable for RL training, raw nuScenes data was converted into structured scenarios using **ScenarioNet**:

```
python -m scenarionet.convert_nuscenes \
--database_path <scenario_db> \
--split v1.0-mini \
--dataroot <nuscenes_root>
```

This step transforms high-dimensional sensor data into simulation-ready scenarios.

---

### 3. Simulation Environment

A custom environment was built using **MetaDrive’s `ScenarioEnv`**:

* Scenario database generated via ScenarioNet was used as input
* Multiple scenarios sampled during training (`num_scenarios = 5`)
* Episode horizon limited to 500 steps

This setup enables interaction with realistic driving scenes derived from real-world data.

---

### 4. State Representation

The agent directly uses observations provided by the environment, which include:

* Vehicle kinematics (position, velocity)
* Lane and road structure information
* Relative positions of nearby objects
* Local traffic context

This avoids manual feature engineering while retaining structured environmental information.

---

### 5. Action Space

A **continuous control space** was used:

* Steering ∈ [-1, 1]
* Throttle/Brake ∈ [-1, 1]

This allows smoother and more realistic vehicle behavior compared to discrete actions.

---

### 6. Reinforcement Learning Algorithm

A **Proximal Policy Optimization (PPO)** agent (Stable-Baselines3) was implemented:

* Policy-based method suitable for continuous control
* Trained through interaction with the simulation environment
* Learns driving strategies via reward-driven optimization

---

### 7. Reward Function Design

A custom reward function was defined to guide behavior:

* Positive reward for forward progress
* Penalty for excessive steering (encouraging smooth control)
* Large penalty for collisions
* Penalty for lane deviation

This balances safety, stability, and efficiency.

---

### 8. Training and Visualization

The trained agent was evaluated in simulation:

* Generated trajectories within driving scenarios
* Produced **2D and 3D GIF visualizations** (see `/gif` folder)
* Demonstrated basic navigation and control behavior

## Results

* Functional PPO-based RL agent interacting with scenario-based environments
* Successful integration of nuScenes → ScenarioNet → MetaDrive pipeline
* Visual outputs demonstrating learned behavior

## Repository Structure

* `Driving_agent_reinforcement_learning.ipynb` – Main implementation and explanations
* `gif/` – 2D and 3D trajectory visualizations
* `ppo_agent/` – PPO-related components (if applicable)
* `Assessment.pdf` – Original assignment description

## Limitations

Given the strict 7-day timeframe and the need to learn RL concepts concurrently, the following limitations exist:

* Simplified environment configuration and scenario coverage
* Limited hyperparameter tuning
* Reward function is heuristic and not fully optimized
* Partial abstraction of full nuScenes complexity

The focus was on achieving a working pipeline rather than full-scale optimization.

## Key Takeaways

* Rapid understanding and application of reinforcement learning (PPO)
* Experience working with real-world autonomous driving data (nuScenes)
* Exposure to scenario-based simulation (ScenarioNet + MetaDrive)
* Practical insight into reward design and control in RL systems

## How to Run

1. Download nuScenes dataset (v1.0-mini recommended)
2. Convert dataset using ScenarioNet
3. Install dependencies (MetaDrive, Stable-Baselines3, nuScenes-devkit)
4. Run the notebook:

```
jupyter notebook Driving_agent_reinforcement_learning.ipynb
```

## Note

This project is best interpreted as a time-constrained learning exercise demonstrating rapid adaptation and implementation, rather than a fully optimized or production-ready autonomous driving system.
