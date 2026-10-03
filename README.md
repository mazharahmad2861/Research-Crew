# Research Crew

A **multi-agent AI project built with CrewAI** to understand the core concepts of agent orchestration, task management, and sequential execution.

## Overview

**Research Crew** uses multiple specialized AI agents that collaborate to research a given topic and produce a structured report.

The project demonstrates how CrewAI organizes agents into a **Crew**, assigns them specific **Tasks**, and executes those tasks through a defined **Process**.

### Workflow

```text
                    Research Crew
                         │
                    User Topic
                         │
                         ↓
                 ┌───────────────┐
                 │   Researcher  │
                 │     Agent     │
                 └───────┬───────┘
                         │
                   Research Task
                         │
                         ↓
              ┌─────────────────────┐
              │  Reporting Analyst  │
              │        Agent        │
              └──────────┬──────────┘
                         │
                   Reporting Task
                         │
                         ↓
                     report.md
```

## How CrewAI Works

CrewAI provides an opinionated framework for building applications using teams of AI agents.

The core architecture used in this project is:

```text
Agent
  ↓
Task
  ↓
Crew
  ↓
Process
  ↓
Final Output
```

## Core CrewAI Concepts

### 1. Agent

An **Agent** is an AI worker responsible for performing a specific role.

Key parameters:

| Parameter | Description |
|---|---|
| `role` | Defines the agent's purpose or responsibility |
| `goal` | Defines what the agent is trying to achieve |
| `backstory` | Provides relevant background/context for the agent |
| `llm` | Specifies the language model used by the agent |

Example:

```yaml
researcher:
  role: Research Researcher
  goal: Research the given topic
  backstory: Experienced technology researcher
  llm: openai/gpt-4o-mini
```

---

### 2. Task

A **Task** represents a specific piece of work assigned to an agent.

Key parameters:

| Parameter | Description |
|---|---|
| `description` | Explains what the agent needs to do |
| `expected_output` | Defines the desired result |
| `agent` | Specifies which agent performs the task |
| `output_file` | Optional file where the result is saved |

Example:

```yaml
research_task:
  description: Research the given topic
  expected_output: A detailed research report
  agent: researcher
```

---

### 3. Crew

A **Crew** brings multiple agents and tasks together into one collaborative workflow.

```text
Agents + Tasks
      ↓
     Crew
```

The Crew is responsible for coordinating the execution of the defined tasks.

In this project:

```text
Researcher
     +
Reporting Analyst
     +
Research Task
     +
Reporting Task
     ↓
    Crew
```

---

### 4. Process

A **Process** determines how the tasks inside a Crew are executed.

The two important process types are:

| Process | Description |
|---|---|
| `sequential` | Tasks execute in a defined order |
| `hierarchical` | A manager/LLM determines how tasks are orchestrated |

This project uses a **sequential process**:

```text
Research Task
      ↓
Reporting Task
      ↓
Final Report
```

So the overall relationship is:

```text
Agent  →  Who does the work?
Task   →  What work needs to be done?
Crew   →  Who + What are organized together?
Process → How are the tasks executed?
```

## Configuration

CrewAI separates much of the agent and task configuration from the Python code using YAML files.

```text
config/
├── agents.yaml
└── tasks.yaml
```

### `agents.yaml`

Contains agent definitions:

```text
Role
Goal
Backstory
LLM
```

### `tasks.yaml`

Contains task definitions:

```text
Description
Expected Output
Agent
Output File
```

This separation keeps the **agent/task configuration** independent from the application logic.

## Project Structure

```text
research_crew/
│
├── src/
│   └── research_crew/
│       │
│       ├── config/
│       │   ├── agents.yaml
│       │   └── tasks.yaml
│       │
│       ├── crew.py
│       └── main.py
│
├── report.md
├── pyproject.toml
└── README.md
```

## Tech Stack

- **Python**
- **CrewAI 1.14.4**
- **UV** — Python project and dependency management
- **YAML** — Agent and task configuration
- **LLM** — Used by CrewAI agents

## Installation

Install the specified CrewAI version:

```bash
uv tool install crewai==1.14.4
```

Create a CrewAI project:

```bash
crewai create crew research_crew
```

Configure your API key in `.env`:

```env
OPENAI_API_KEY=your_api_key
```

Run the project:

```bash
cd research_crew
crewai run
```

The final report is generated as:

```text
report.md
```

## Key Concepts Demonstrated

- Multi-agent architecture
- Agent roles, goals, and backstories
- Task definition and assignment
- Crew creation
- Sequential process
- YAML-based configuration
- LLM configuration
- File-based output

## Learning Goal

This project is intentionally simple. Its purpose is to establish a strong understanding of the fundamental CrewAI architecture:

```text
Agent → Task → Crew → Process
```

It serves as a foundation for more advanced CrewAI applications involving **custom tools, memory, hierarchical processes, Flows, external APIs, and more complex multi-agent workflows**.
