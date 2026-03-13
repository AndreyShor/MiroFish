# MiroFish Simulation Guide

The simulation engine is the heart of MiroFish, enabling parallel world simulations on Twitter and Reddit clones.

---

## 🔄 Simulation Lifecycle

A simulation goes through several distinct states, managed by the backend:

| State | Description |
| :--- | :--- |
| **CREATED** | Initial state after setting project and graph IDs. |
| **PREPARING** | Generating agent personas and simulation parameters (LLM-driven). |
| **READY** | Sandbox is configured and scripts are prepared. |
| **RUNNING** | Simulation processes are active and interaction logs are being generated. |
| **COMPLETED** | Simulation reached the maximum number of rounds naturally. |
| **STOPPED** | Manually terminated by the user. |
| **FAILED** | Encountered an error during preparation or execution. |

---

## 🛠 Management Services

### Simulation Manager (`SimulationManager`)
The architect of the simulation sandbox.
- **Role**: Pre-simulation configuration.
- **Key Functions**:
    - Reads and filters entities from the Zep Knowledge Graph.
    - Uses an LLM to generate high-fidelity OASIS Agent Profiles (personas).
    - Intelligently generates `simulation_config.json` containing timing, activity levels, and platform rules.

### Simulation Runner (`SimulationRunner`)
The engine that executes the simulation.
- **Role**: Runtime orchestration.
- **Key Functions**:
    - Spawns background subprocesses for `run_twitter_simulation.py` and `run_reddit_simulation.py`.
    - Implements Inter-Process Communication (IPC) for controlling agent flows.
    - Monitors `actions.jsonl` files to provide real-time updates on agent activities, rounds, and system health.

---

## 🌐 Parallel Sandbox Execution

MiroFish supports a dual-platform simulation model:

1. **Twitter Sandbox**: Focuses on short-form communication, broadcast-style interactions, and viral trends.
2. **Reddit Sandbox**: Focuses on community-based discussions, nested threads, and deep-dive subculture evolution.

Simulations can be run on either platform individually or in parallel to observe cross-platform information flow.

---

## 📄 Action Logs

All agent interactions are recorded in `actions.jsonl` files within the simulation's `uploads/simulations/<id>/` directory:
- **twitter/actions.jsonl**: Records tweets, retweets, and likes.
- **reddit/actions.jsonl**: Records posts, comments, and upvotes.

These logs are the primary data source for the **Report Agent** when generating prediction analytics.
