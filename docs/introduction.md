# Introduction

<img src="_static/rerun_logo.png" alt="ReRun Logo" width="120">

## Overview

**ReRun** is a desktop application that helps researchers execute and replicate scientific analyses using **Stata**, **Python**, or **R**. It provides a consistent framework to design workflows, organize analyses, and ensure best practices in **replicability**, **transparency**, and **computational reproducibility**.

ReRun allows workflows to be built from **Steps** and **Jobs**:
- **Steps** represent major stages of an analysis and run **sequentially**.
- **Jobs** represent individual execution units within a step and run **in parallel**.

This structure enables researchers to define complex workflows that are both modular and efficient.

---

## Key Features

- **Multi-language support** – Run code written in Stata, Python, or R.  
- **Workflow structure** – Combine sequential and parallel execution through Steps and Jobs.  
- **Containerized execution** – Run analyses in Docker or Singularity containers for full reproducibility.  
- **Local or container mode** – Choose between your local runtime or isolated environments.  
- **Transparent execution** – Each job produces logs, timestamps, and status information.  
- **Cross-platform compatibility** – Works on Windows and Linux systems.  
  - *(Note: macOS support limited due to a FilePicker issue in Flet v0.28.3.)*

---

## Who Uses ReRun

ReRun is designed for:

- Researchers conducting reproducible empirical analyses.  
- Researchers managing large or multi-language pipelines.  
- Computational social scientists who need transparent, replicable workflows.  
- Academic teams maintaining shared analytical environments.

---

## Why ReRun

Scientific analyses often depend on multiple tools, custom scripts, and manual steps that are difficult to reproduce. ReRun addresses this by providing:

- A standardized workflow structure that documents each stage of execution.  
- Support for containers, ensuring environments are consistent across systems.  
- Automated and transparent job management.  
- Simplified re-execution of complete analytical pipelines.

The result is a streamlined, reproducible research workflow that can be shared and validated easily.

---

## Supported Platforms

| Platform | Status | Notes |
|-----------|---------|-------|
| **Windows** | Supported | Fully tested |
| **Linux** | Supported | Fully tested |
| **macOS** | Limited | FilePicker bug in Flet v0.28.3 |

---

## Next Steps

- Proceed to the [Installation](installation.md) section to set up ReRun.  
- Then explore the [Usage](usage/index.md) section to learn how to create and run workflows.
