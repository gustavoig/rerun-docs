Usage Overview
==============

The **Usage** section explains how to operate ReRun once it has been installed. It describes how to create, configure, 
and execute replications using **Steps** and **Jobs**, and how to monitor execution through logs and status panels.

ReRun replications follow a simple structure:

- **Steps** are executed **sequentially**, representing ordered stages of analysis.
- **Jobs** within a step are executed **in parallel**, allowing independent tasks to run simultaneously.

This structure allows researchers to reproduce analyses efficiently and maintain clarity across complex 
computational pipelines.


Basic Concepts
--------------

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Concept
     - Description
   * - **Replication**
     - A collection of steps defining the full analytical process.
   * - **Step**
     - A logical stage in the workflow (e.g., data preparation, estimation, reporting). Steps run sequentially.
   * - **Job**
     - An individual execution unit inside a step (e.g., a Stata do-file, Python script, or R script, with dependencies or not). Jobs within a step run in parallel.
   * - **Execution Backend**
     - Defines whether a job is executed locally, in Docker, or in Singularity.
   * - **Log Panel**
     - Displays job progress, timestamps, and messages during execution.


Typical Workflow
----------------

1. **Create a new replication or load an existing one.** 

 - Replications contain all configuration files, scripts, and workflow definitions. 

2. **Define Steps.**

 - Each Step represents a stage in your analysis.

3. **Define Jobs.**

 - Each Job specifies an executable script and its dependencies.

4. **Configure job settings**  

 - Set the main path for the job
 - Set the main script 
 - Choose the container (or instead local mode)
 - Provide dependencies if your main script calls any
 - Choose the command (e.g. ``stata-mp -b do``)

5. **Run the replication.**  

 - Execute Steps sequentially.
 - Launch Jobs within each Step in parallel.- Display progress and logs in real time.

6. **Review results.** 

 - Once complete, outputs and logs are stored in designated directories for documentation and verification.


Interface Overview
------------------

ReRun’s interface is divided into several main components:

.. list-table::
   :header-rows: 1
   :widths: 40 70

   * - Section
     - Purpose
   * - **App Panel**
     - Start new replication or load a new one.
   * - **Start/Load Replication Panel**
     - Provide the input, output, and data paths.
   * - **Steps Manager Panel**
     - Define steps and edit project notes.
   * - **Jobs Manager Panel**
     - Define jobs within a step.
   * - **Job Configuration Panel**
     - Configure a single job: main script, dependencies, container, command, etc.
   * - **Log Panel**
     - Tracks running jobs, display status messages.


Directory Structure
-------------------

A typical project managed by ReRun has the following layout:

.. code-block:: text

   Replications/Rep001/
   ├── config.json
   ├── manifest.json
   ├── datafiles.txt
   ├── log.txt
   ├── replication_tree.txt
   ├── readme.md
   ├── Step01/
   │   ├── Job01/
   │   │   ├── main.do
   │   │   └── profile.do
   │   └── Job02/
   │       └── ...
   └── Step02/
       └── ...


Usage Sections
--------------

The following subsections describe each aspect of ReRun in detail.

.. toctree::
   :maxdepth: 2

   stata_small_example
   configuration_files
   containerized_example
   interface_reference


Next Steps
----------

Continue to the next page to see :doc:`A Small Example in Stata <stata_small_example>`.
