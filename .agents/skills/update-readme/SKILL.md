---
name: update-readme
description: Keep the project's replication README.md in sync with the codebase — updates data file manifests, installed package versions, computational requirements, and the table/figure program-to-output mapping, and removes any claim that no longer matches what ships. Use whenever new datasets, packages, analysis scripts, tables, or figures are added or modified.
---

# Updating Replication README

Keep `README.md` consistent with the codebase and outputs at all times following the Social Science Data Editors standard.

## When to Update the README

Update `README.md` immediately whenever any of the following change:
1. **Data files**: New raw datasets downloaded or derived datasets created.
2. **Software & packages**: New packages added to `programs/00_setup.do`.
3. **Exhibits & programs**: New tables or figures produced in `programs/02_analysis/` or `programs/03_appendix/`.
4. **Computational details**: Random seeds set, hardware environment changed, or significant changes in pipeline runtime.

## Key Sections to Maintain

### 1. Dataset List
Ensure every file in `data/raw/` and `data/derived/` appears in the **Dataset List** table:
- **Data file**: Exact relative path (e.g. `data/raw/ted/export_CAN_2023.csv`).
- **Source**: Name of the issuing agency or origin.
- **Notes**: Format, uncompressed size, observation/variable count, or confidentiality restrictions.
- **Provided**: `Yes` (redistributed in package) or `No` (instructions to obtain given in DAS).

### 2. Software & Package Dependencies
Under **Computational Requirements > Software Requirements**:
- Record the exact Stata version used.
- For each package in `programs/00_setup.do`, record its name, version, and release date (obtain via `which <package>` in Stata).

### 3. Controlled Randomness
- If estimation or sampling sets a random seed, check the box and specify the exact program name and line number where the seed is set.

### 4. List of Tables and Programs
Maintain the **List of Tables and Programs** mapping table:
- **Figure/Table #**: Exact exhibit number in the manuscript (e.g. `Table 1`, `Figure 3`).
- **Program**: Exact relative path to the producing do-file (e.g. `programs/02_analysis/table1.do`).
- **Line Number**: Line number where the exhibit is exported (if the script produces multiple exhibits).
- **Output file**: Exact filename written to `output/` (e.g. `table1.tex`, `figure2.png`).
- **Note**: Mark `n.a. (no data)` for conceptual diagrams without underlying data.

### 5. Statements must match the artifact

- The **Provided** column must reflect what actually ships in the repository or
  package, not what could be obtained. If a dataset is gitignored, mark it `No`
  and point to the download instructions.
- Do not reference programs, directories, or files that do not exist (e.g. a
  `programs/03_appendix/` never created, a `programs/ado/` with no ado files, or a
  bundled data archive that is not included).
- When unsure whether a claim is still true, remove it. No information is better
  than incorrect information.
