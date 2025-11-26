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
   * - **Execution Panel**
     - Displays job progress, timestamps, and messages during execution.


Typical Workflow
----------------

1. **Create a new replication**

   In the **Start Replication** panel, specify the following:

   - **Output path**  
     This is the directory where the replication structure will be created.  
     ReRun will generate a folder named **Replications** inside this directory, and each run will be
     placed in a numbered subfolder (e.g., ``Rep001``, ``Rep002``).

   - **Data path**  
     This is the central directory where your input data is stored.  
     The data files are *not* copied into the replication directory.  
     Instead, this path is recorded in the automatically generated configuration files  
     (e.g., ``global path_source ...`` in **Stata**).  
     The data directory may contain subfolders, as long as your scripts reference them correctly.


2. **Define Steps**

   - Each Step represents a major stage in your analysis.  
   - Users may write documentation for the Step in the Step Text Field; this text is stored in the Step’s
     ``readme.md`` file.  
   - Steps can be added or deleted using the controls in the Steps Panel.  
   - To configure a Step - i.e., to define its Jobs and their settings - click the **Configure** button.

3. **Define Jobs within a Step**

   - Each Job represents an independent task that can be run in parallel with other jobs in the same Step.  
   - ReRun creates a dedicated folder for each Job.  
   - A Job consists of one **main script** and optionally additional **dependencies**.  
   - Users may write documentation for each Job; this text is added to the Job’s ``readme.md`` file.  
   - Click **Configure** to open the Job Configuration window.

4. **Configure Job settings**

   - **Main Path**  
     Select the directory containing the files needed for the Job.  
     ReRun copies this folder (and its internal structure) into the Job directory.

   - **Main Script**  
     Choose the primary script that controls the Job’s execution.  
     This script may call additional dependencies.

   - **Container**  
     Choose between:  

     - a **Docker image** (e.g., ``stata:18``),  
     - a **Singularity/Apptainer .sif** file, or  
     - leave empty for **Local Mode** (direct use of the host’s Stata/Python/R installation).

   - **Container Definition (optional)**  
     Provide the build script used to create the container.  
     If specified, this file is copied into the Job directory.

   - **Command**  
     Specify the command used to run the main script - for example:  

     - ``stata-mp -b do`` (Linux, Docker, Singularity)  
     - ``C:\Program Files\StataNow19\StataMP-64.exe /e do`` (Windows Local Mode)

   - **Dependencies**  
     Provide any scripts that the main script relies on.

   - **Tools Path**  
     Select a directory containing user-supplied tools (e.g., Stata ``PLUS`` packages, Python modules, or R libraries).  
     This directory is copied into a ``tools`` folder under the Job directory.  
     During execution, the runtime will load **only** the tools in this directory (or those available inside the container, if used).

   - Save the configurations for the **Job**. 


5. **Run the replication**   

   - Save the Jobs. 
   - Execute the Steps by clicking the **Run Steps** button.
   - Follow the progress and logs in real time in the **Execution Panel**.

6. **Review results**

   When a replication finishes, all outputs are written into the appropriate directories within the replication folder.  
   In addition to the files produced by your own code, ReRun automatically generates several metadata and documentation files that support transparency and reproducibility:

   - ``config.json``  
     Describes the structure of the replication: steps, jobs, paths, and job settings.

   - ``log.txt`` 
     Contains execution logs from the **Execution Panel**, showing step and job progress.

   - ``datafiles.txt`` 
     Lists all input data files referenced by the replication, including modification timestamps and file hashes.

   - ``manifest.json``  
     Records inputs and outputs for each job, including file sizes, hashes, and timestamps, enabling verification and reproducibility.

   - ``readme.md`` 
     A consolidated documentation file containing system information and user-provided notes from the project, steps, and jobs.

   - ``replication_tree.txt``  
     A tree-style representation of the replication folder structure (generated before execution).

   - **Job-level configuration files**  
     Created for each job depending on the runtime used:
     
    - ``profile.do`` (Stata)   
    - ``config.R`` (R)   
    - ``config.py`` (Python)   

     These files define the environment and paths used during job execution (see :doc:`Configuration Files <configuration_files>`).


7. **Re-run**

   You can repeat an analysis by loading an existing replication. In the **Load Replication** panel, provide the following paths:

   - **Input Path**  
     The directory of the replication you want to re-run.  
     This must be a numbered folder (e.g., ``Rep001``, ``Rep002``) containing ``config.json``.  
     If ``config.json`` is missing, ReRun cannot restore the replication and will display an error.

   - **Output Path**  
     Optional.  
     If **left empty**, ReRun will create a new directory inside the **Input Path** following the same structure used when creating a new replication:

     .. code-block:: text

        InputPath/
            Replications/
                Rep00X/

     where ``Rep00X`` is the next available replication number.  
     If you prefer the outputs to be written elsewhere, you must explicitly provide a different **Output Path**.

   - **Data Path**  
     If not specified, ReRun will use the data path stored in ``config.json``.  
     If you want to run the replication with a different dataset or a relocated data directory, you must provide the new path here.


  Please note that the user can add to, remove, or adjust any component of the loaded replication.


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
