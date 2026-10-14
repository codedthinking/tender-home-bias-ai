---
name: stata
description: Write clean, reproducible Stata code following project conventions — no command/variable abbreviations, top-level working directory discipline, centralized package setup, and no chatty displays or unnecessary comments. Use when creating or editing Stata do-files (.do) or organizing Stata data pipelines.
---

# Stata Code Conventions

## Core Rules

### 1. No Command or Variable Abbreviations
- Spell out every command completely (e.g. `generate` not `gen`, `replace` not `rep`, `compress` not `comp`, `import delimited` not `import delim`, `display` not `di`).
- Spell out every variable name in full. Never rely on Stata's minimum unique prefix resolution.

### 2. Fixed Project Working Directory
- Always run code from the project root (`tenders/`).
- **Never change working directory (`cd`) inside do-files.**
- Reference paths relative to root or via global macros defined in a central `config.do` (e.g. `$raw`, `$derived`, `$output`).
- If a command operates on the working directory by default (such as `unzipfile`), extract and move/copy files explicitly to the target subdirectory without `cd`.

### 3. Minimal Comments and No Chatty Displays
- Do not write decorative banner comments, section headers, or step-by-step narration.
- Do not add `display` messages to report progress or status.
- The only reason for a comment is if a step is very unintuitive for future agents; in that case, explain only **why** it is done that way.

### 4. Centralized Package Management
- Never put `ssc install` or package installations inside data prep or analysis scripts.
- Declare all required packages in `local packages` inside `programs/00_setup.do`.

## Pipeline Structure
- `main.do` in the project root executes the sequence: `00_setup.do` -> `01_dataprep/main.do` -> `02_analysis/main.do`.
- `programs/config.do` sets global paths (`$root`, `$raw`, `$derived`, `$output`, `$programs`).
- Sub-pipelines (e.g. `01_dataprep/main.do`) sequentially invoke their component do-files (`download.do`, `unpack.do`).
