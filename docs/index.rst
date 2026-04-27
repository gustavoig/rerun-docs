ReRun Documentation
====================

.. image:: _static/rerun_logo.png
   :alt: ReRun Logo
   :width: 100px
   :align: center

**ReRun** is a desktop application that helps researchers design and execute reproducible scientific analyses using **Stata**, **Python**, or **R**.  
It provides a structured workflow system that promotes best practices in **replicability**, **transparency**, and **computational reproducibility**.

ReRun allows analyses to be organized into **Steps** and **Jobs**:

- **Steps** are executed sequentially, representing major stages of the workflow.
- **Jobs** within each step run in parallel, enabling efficient execution of independent tasks.

The application supports both **local** execution (using installed software) and **containerized** execution via **Docker** or **Singularity**, ensuring that analyses can be reproduced across different environments.

ReRun is cross-platform and runs on **Windows** , **MacOS** and **Linux**.  


Contents
--------

.. toctree::
   :maxdepth: 3

   introduction
   installation
   usage/index
   troubleshooting

