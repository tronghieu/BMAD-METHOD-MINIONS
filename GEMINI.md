# BMAD (Build-My-Agent-Director) Expansion Packs

## Directory Overview

This repository is a framework for creating and managing unofficial "BMAD" (Build-My-Agent-Director) expansion packs. These packs are collections of AI agents, tasks, and workflows designed to accomplish specific goals. The entire system is defined through a series of Markdown and YAML files.

## Key Files and Structure

The repository is organized into several key directories:

*   **`expansion-packs/`**: This is the core directory containing the different agent packs. Each subdirectory represents a specific expansion pack (e.g., `bmad-design-thinking-facilitator`, `bmad-bug-management`).
*   **`docs/`**: Contains high-level documentation about the BMAD framework, including guiding principles and design philosophies.

Within each expansion pack, the structure is consistent:

*   **`agents/`**: Contains Markdown files that define the personas, capabilities, and instructions for individual AI agents.
*   **`tasks/`**: Contains Markdown files that define specific, granular tasks that agents can be assigned to perform.
*   **`workflows/`**: Contains YAML files that orchestrate a sequence of tasks and assign them to different agents to accomplish a larger goal.
*   **`templates/`**: Holds template files (usually YAML or Markdown) that are used by tasks to generate documents, plans, or other artifacts.
*   **`checklists/`**: Provides Markdown-based checklists that agents can use to ensure tasks are completed to a certain standard.
*   **`data/`**: Stores supplementary data and guides that agents can reference.
*   **`config.yaml`**: A configuration file that defines the metadata and settings for the expansion pack.

## Usage

The contents of this directory are intended to be used by the BMAD system. The files are not executed directly but are read and interpreted by the system to assemble and direct teams of AI agents.

*   To **create a new expansion pack**, you would create a new subdirectory in `expansion-packs/` and populate it with the required `agents`, `tasks`, `workflows`, and a `config.yaml`.
*   To **customize an existing pack**, you would modify the Markdown and YAML files within that pack's directory. For example, you could edit an agent's persona in the `agents/` directory or change the sequence of a process in the `workflows/` directory.
