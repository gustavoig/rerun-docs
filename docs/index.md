# ReRun Documentation ![ReRun Logo](_static/rerun_logo.png){width="100px"} 


**ReRun** is a desktop application that helps researchers design and execute reproducible scientific analyses using **Stata**, **Python**, or **R**. It provides a structured workflow system that promotes best practices in **replicability**, **transparency**, and **computational reproducibility**.

ReRun allows analyses to be organized into **Steps** and **Jobs**:
- **Steps** are executed sequentially, representing major stages of the workflow.
- **Jobs** within each step run in parallel, enabling efficient execution of independent tasks.

The application supports both **local** execution (using installed software) and **containerized** execution via **Docker** or **Singularity**, ensuring that analyses can be reproduced across different environments.

ReRun is cross-platform and runs on **Windows** and **Linux**. *(Note: macOS support is limited due to a [FilePicker issue in Flet v0.28.3](https://github.com/flet-dev/flet/issues/5334).)*

```{toctree}
:maxdepth: 2
:caption: Table of Contents

introduction.md
installation.md
usage/index.md
advanced.md
troubleshooting.md
