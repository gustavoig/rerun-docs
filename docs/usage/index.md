# Usage Overview

The **Usage** section explains how to operate ReRun once it has been installed.  
It describes how to create, configure, and execute workflows using **Steps** and **Jobs**, and how to monitor execution through logs and status panels.

ReRun workflows follow a simple structure:

- **Steps** are executed **sequentially**, representing ordered stages of analysis.  
- **Jobs** within a step are executed **in parallel**, allowing independent tasks to run simultaneously.  

This structure allows researchers to reproduce analyses efficiently and maintain clarity across complex computational pipelines.

---

## Basic Concepts

| Concept | Description |
|----------|--------------|
| **Workflow** | A collection of steps defining the full analytical process. |
| **Step** | A logical stage in the workflow (e.g., data preparation, estimation, reporting). Steps run sequentially. |
| **Job** | An individual execution unit inside a step (e.g., a Stata do-file, Python script, or R script). Jobs within a step run in parallel. |
| **Execution Backend** | Defines whether a job is executed locally, in Docker, or in Singularity. |
| **Log Panel** | Displays job progress, timestamps, and messages during execution. |

---

## Typical Workflow

1. **Create a new project or load an existing one.**  
   Projects contain all configuration files, scripts, and workflow definitions.

2. **Define Steps and Jobs.**  
   - Each Step represents a stage in your analysis.  
   - Each Job specifies a single executable script and its parameters.

3. **Configure execution settings.**  
   Choose between:
   - **Local** execution using installed software (Stata, Python, R).  
   - **Docker** or **Singularity** for containerized, reproducible runs.

4. **Run the workflow.**  
   ReRun will:
   - Execute Steps sequentially.  
   - Launch Jobs within each Step in parallel.  
   - Display progress and logs in real time.

5. **Review results.**  
   Once complete, outputs and logs are stored in designated directories for documentation and verification.

---

## Interface Overview

ReRun’s interface is divided into several main components:

| Section | Purpose |
|----------|----------|
| **Menu Bar** | Access project operations, settings, and help resources. |
| **Workflow Panel** | Displays all Steps and Jobs. Allows adding, editing, or removing items. |
| **Execution Panel** | Shows progress, elapsed time, and provides controls to start or stop runs. |
| **Log Panel** | Displays output from each running job for traceability. |
| **Status Bar** | Indicates current backend mode (Local, Docker, Singularity) and overall workflow status. |

---

## Directory Structure

A typical project managed by ReRun has the following layout:

```
project_name/
├── config.yaml
├── steps/
│   ├── 01_prepare_data/
│   │   ├── job1_stata.do
│   │   ├── job2_python.py
│   │   └── job3_rscript.R
│   ├── 02_analysis/
│   │   ├── job1_stata.do
│   │   └── job2_python.py
│   └── 03_report/
│       └── job1_rscript.R
└── logs/
    ├── 01_prepare_data/
    ├── 02_analysis/
    └── 03_report/
```

---

## Usage Sections

The following subsections describe each aspect of ReRun in detail.

```{toctree}
:maxdepth: 2
:caption: Usage Sections

stata_small_example.md
```

---

## Next Steps

Continue to the next page to see a [A Small Example in Stata](stata_small_example.md).
