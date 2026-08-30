# Self-Driving Universities: A Neuro-Symbolic Multi-Agent Framework

**Status:** Under Review (*IEEE Access*)  
**Keywords:** Multi-Agent Systems, Neuro-Symbolic AI, Formal Verification, Edge Computing, Resource Optimization.

## Overview
This repository contains the datasets, execution logs, and empirical telemetry for the research paper: *"Self-Driving Universities: A Neuro-Symbolic Multi-Agent Framework for Autonomous Institutional Scheduling."* 

The project investigates the deployment of a hybrid agentic-symbolic control system designed to automate complex institutional resource allocation. It utilizes a network of Large Language Model (LLM) agents to negotiate academic scheduling, bounded by a **Z3 Formal Verification Engine** acting as an immutable mathematical gatekeeper. To ensure system continuity during catastrophic neural failures (such as the documented *Autoregressive Token Explosion*), the architecture integrates a sub-millisecond greedy heuristic fallback.

## Repository Structure

To isolate the computational value of the verification and agentic layers, the pipeline was executed across three distinct hardware environments. The repository is organized to separate shared environmental inputs from hardware-specific telemetry outputs.

### 1. `datasets/` (Shared Environment)
Contains the IRB-free synthetic environments utilized across all hardware tiers.
*   **Curriculum Topologies (`.graphml`):** Directed Acyclic Graphs modeling strict prerequisite chains for `Univ_A_Centralized` (deep, rigid STEM tracking) and `Univ_B_Elective` (flat, modular liberal arts).
*   **Student Demographics (`.csv`):** Monte Carlo-parameterized populations of 10,000 synthetic student agents featuring distributed academic standings and failure probabilities.

### 2. Experimental Execution Tiers
Each folder contains the specific `analysis`, `checkpoints`, `logs`, and `tier_figures` generated during the 16-semester longitudinal simulations.

*   **`tier1_mock/` (Deterministic Baseline):** Execution without neural inference to establish the absolute minimum latency of the Python/SimPy environment and the Z3 verification engine.
*   **`tier2_gpu/` (High-Performance):** Telemetry from a centralized administrative server utilizing an NVIDIA RTX 2000 Ada GPU and an 8-billion parameter LLM.
*   **`tier3_edge/` (Constrained Infrastructure):** Telemetry from a decentralized legacy Edge CPU (Ubuntu Intel Core i3) running a quantized 3-billion parameter model. This tier exposes severe hardware bottlenecks and documents the *Autoregressive Token Explosion* failure mode.

### 3. Key Telemetry and Analysis
Reviewers seeking to validate the core findings of the manuscript should direct their attention to the following files within each tier's `analysis/` folder:
*   `[tier]_telemetry.csv`: Logs the sub-millisecond recovery times of the heuristic fallback during structural and personnel shocks.
*   `[tier]_z3_verification_benchmark.csv`: Demonstrates the 100% violation catch rate and zero percent false-positive rate of the formal symbolic gatekeeper.
*   `[tier]_research_summary.md`: Auto-generated synthesis of the hardware-specific runtimes and failure states.

## Experimental Protocol: The Perturbation Matrix
The logs provided in this repository document an 8-semester continuous simulation per university graph. The system was subjected to the following injected operational shocks:
*   **Semester 1–3:** Stable baseline operations.
*   **Semester 4:** 20% loss of classroom capacity (Structural Shock).
*   **Semester 6:** 20% loss of available teaching faculty (Personnel Shock).

## How to Run the Code
1. Clone the repository to your local machine.
2. Install the required dependencies: `pip install -r requirements.txt`
3. Launch Jupyter Notebook and open the pipeline file corresponding to the hardware tier you wish to evaluate (e.g., `tier1_mock_pipeline.ipynb`).

## Citation
*Citation details will be updated upon publication.*
