# Hotelling-Downs Political Polarization Simulation

This project implements an Agent-Based Model (ABM) to simulate political competition on a 1G grid. Using Python and the Mesa framework, it extends the classic Hotelling-Downs model to explore how voter tolerance and population distribution influence candidate positioning and political polarization.

## Project Overview

The simulation models two candidates seeking to maximize votes on a spectrum ranging from 0 (Left) to 100 (Right). This model introduces a Tolerance Variable: voters will abstain if the closest candidate is too far away from their ideological position.

Furthermore, the model incorporates various Voter Distributions (Uniform, Normal, and Beta) to simulate realistic political landscapes, allowing for the analysis of how population spread affects strategic positioning and convergence.

## Model Logic

### The Voter Agent
* Voters do not move
* **Position:** A fixed location on the political spectrum (0-100)
* **Tolerance:** Determines the flexibility of the voter. If a candidate is further away than this value, the voter refuses to vote for them

### The Candidate Agent
* Their goal is to maximize their vote share by moving along the political spectrum
* Instead of simply checking for immediate neighbours, the candidate scans in a range of +/- 3 positions, enabling them to see across any potential gaps in the voter distribution.
* Calculates the projected votes for every spot in their scanning radius relative to the opponent's current position and strictly prefers more votes
* In case of a tie, candidate prefers a movement towards the center

### The Model
* Orchestrates the simulation environment and population generation
* The `RandomActivation` scheduler shuffles the order of agent execution every step
* The `MultiGrid` allows Candidates and Voters to coexist on the same cell
* **Initialization:** Generates the Voters based on the chosen distribution and places Candidates at the extremes (0 and 100)

## Experiments

The notebook executes a series of scenarios varying the population distribution and voter tolerance levels:

* **Uniform Distribution:** High tolerance leads to convergence at the center, while low tolerance causes stagnation at the edges. Asymmetric tolerance allows the flexible candidate to invade.
* **Normal Distribution:** Candidates rapidly converge to the center peak with high tolerance. With low tolerance, they abandon the empty tails but hit a "density wall," stopping short of the center.
* **Beta Distribution:** High tolerance results in convergence at the population median (skewed left). Low tolerance traps the left candidate, while the right candidate crosses the empty "desert." Asymmetric tolerance leads to "Total Invasion" by the flexible candidate.

## Installation and Usage

1.  Clone the repository.
2.  Install the required dependencies:
    ```bash
    pip install mesa pandas matplotlib numpy
    ```
3.  Run the Jupyter Notebook:
    ```bash
    jupyter lab Polarization.ipynb
    ```

## File Structure

* **Polarization.ipynb:** The main executable notebook containing Agent classes, Model logic, and the experiment reporting dashboard.
* **README.md:** Project documentation.