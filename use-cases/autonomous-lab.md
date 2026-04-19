# Use Case: AI-Driven Autonomous Laboratory Research & Experiment Orchestration

Maximize scientific discovery and reproducibility by using OpenClaw to automate experiment design, lab automation control, and real-time data analysis.

## 1. Technical Overview
This agent acts as an **Autonomous Research Scientist**, integrating with Laboratory Information Management Systems (LIMS), lab automation hardware (Opentrons, Tecan), and scientific instruments (HPLC, PCR). It uses the `python` tool for experimental design and the `shell` tool to interact with lab-specific control software.

### Required Skills
- `lims-connector`: To securely retrieve and manage experiment protocols and sample metadata.
- `lab-automator`: To control and monitor liquid handling robots and other lab automation hardware.
- `experiment-optimizer`: To use Bayesian optimization to suggest the next set of experimental conditions.

## 2. Implementation Steps

### Step 1: Set Up the Research Workspace
Create a secure, isolated workspace with access to the necessary lab and scientific tools:
```bash
openclaw workspace create autonomous-lab --tools "lims-connector,lab-automator,python"
```

### Step 2: Configure the Research Agent
Set the system prompt to design experiments and analyze real-time data:
```markdown
System: You are an Autonomous Research Scientist. 
1. When a new 'Research Goal' (e.g., 'Maximize Protein Yield') is received:
   a. Use the `lims-connector` to find the 'Baseline Protocol' and 'Available Reagents'.
   b. Use the `python` tool to design a 'Design of Experiments' (DoE) with 8 initial conditions.
   c. Use the `lab-automator` to execute the 'Liquid Handling' protocol for the initial experiments.
   d. Every 30 minutes, monitor the 'Real-Time Yield' from the HPLC.
   e. If the 'Yield' in any 'Sub-Zone' (96-well plate) is > 2x the baseline:
      i. Flag the condition as 'High Yield' in the research database.
      ii. Use the `experiment-optimizer` to suggest the next 4 'Refinement' conditions.
   f. Generate a 'Live Experiment Dashboard' on the OpenClaw Canvas.
2. Every 24 hours, generate a 'Scientific Brief' on the OpenClaw Canvas.
```

### Step 3: Automate Scientific Literature Reviews
Enable the agent to find and summarize relevant papers:
```bash
openclaw message send --to autonomous-lab --message "Search for 'Recent Advances in Protein Expression' on PubMed. Summarize the top 5 papers and identify any 'Novel Reagents' or 'Optimized Conditions' that can be applied to our current research goal."
```

## 3. Advanced Feature: AI-Powered Closed-Loop Discovery
The agent can operate in a 'Closed-Loop' mode. It designs an experiment, executes it via lab automation, analyzes the results, and uses those results to design the next experiment—all without human intervention. This significantly accelerates the pace of discovery in fields like drug development, materials science, and synthetic biology.

## 4. Safety & Scientific Guardrails
- **Laboratory Safety**: All lab automation tasks MUST comply with institutional biosafety and chemical safety protocols (e.g., BSL-2). The agent must verify 'Safe Operating Ranges' before every experiment.
- **Scientific Integrity**: The agent must maintain a complete, immutable 'Electronic Lab Notebook' (ELN) of all experimental designs, execution logs, and data analysis.
- **Human-in-the-Loop**: Any decision to start a new 'High-Cost' or 'High-Risk' experiment must be confirmed by a human Principal Investigator (PI) via the `canvas` interface.
- **Data Privacy**: Ensure all research data is handled according to institutional data protection policies and relevant regulations (e.g., HIPAA).
