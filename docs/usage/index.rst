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
   * - **Project / Replication**
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

   - **Restricted Data path**
     This is the central directory where your restricted input data is stored.  
     The data files are *not* copied into the replication directory.  
     Instead, this path is recorded in the replication configuration file ``rerun_config.json``. 
     At runtime, the automatically generated configuration files read this value to define the 
     data location (e.g., ``global path_source ...`` in **Stata**).  
     The data directory may contain subfolders, as long as your scripts reference them correctly.

   - **Non-restricted data path**  
     Shareable data path for the replication. The data files under this path are copied to the
     output directory, under '...Replications/Rep###/data/public'. The configuration files set this
     path and assign it to a variable/global (e.g., ``global path_source_public ...`` in Stata) 


2. **Define Steps**

   - Each Step represents a major stage in your analysis.  
   - ReRun creates a dedicated folder for each Step.
   - Users may write documentation for the Step in the Step Text Field; this text is stored in the Step’s
     ``rerun_readme.md`` file.  
   - Steps can be added, deleted or configured using the controls in the Left Panel.  

3. **Define Jobs within a Step**

   - Each Job represents an independent task that can be run in parallel with other jobs in the same Step.  
   - ReRun creates a dedicated folder for each Job.  
   - A Job consists of one **main script** and optionally additional **dependencies**.  
   - Users may write documentation for each Job; this text is added to the Job’s ``rerun_readme.md`` file.  
   - Click the **Configure Job** button to open the Job Configuration View.

4. **Configure Job settings**

   - **Main Path**  
     Select the directory containing the files needed for the Job.  
     ReRun copies this folder (and its internal structure) into the Job directory.

   - **Main Script**  
     Choose the primary script that controls the Job’s execution.  
     This script may call additional dependencies.

   - **Executable / Interpreter**  
     Executable or interpreter used to run the main script. Provide only the binary path/name, for example:  

     - ``stata-mp`` (Linux, Docker, Singularity)  
     - ``python`` 
     - ``Rscript``
     - ``C:\Program Files\StataNow19\StataMP-64.exe`` (Windows Local Mode)

   - **Dependencies**  
     Provide any scripts that the main script relies on.

   - **Tools Path**  
     Select a directory containing user-supplied tools (e.g., Stata ``PLUS`` packages, Python modules, or R libraries).  
     This directory is copied into a ``tools`` folder under the Job directory.  
     During execution, the runtime will load **only** the tools in this directory (or those available inside the container, if used).

   - **Container**  
     Choose between:  

     - a **Docker image** (e.g., ``stata:18``),  
     - a **Singularity/Apptainer .sif** file, or  
     - leave empty for **Local Mode** (direct use of the host’s Stata/Python/R installation).

   - **Container Definition (optional)**  
     Provide the build script used to create the container.  
     If specified, this file is copied into the Job directory.

   - **Container Bindings (optional)**
     Optional host-to-container bind mounts used when a Container Image is set.
     Fill one row per mount:

     - Host path: existing path on your machine/server.
     - Container path: destination path inside the container.
     - Read-only: enable when scripts only need to read files.

     Example:
    
     - ``/opt/licenses/stata.lic`` -> ``/opt/stata/stata.lic`` 


   - Save the configurations for the **Job**. 


5. **Run the replication**   

   - Execute the project by clicking the **Run Project** button.
   - Follow the progress and logs in real time in the **Execution Panel**.

6. **Review results**

   When a replication finishes, all outputs are written into the appropriate directories within the replication folder.  
   In addition to the files produced by your own code, ReRun automatically generates several metadata and documentation files that support transparency and reproducibility:

   - ``rerun_config.json``  
     Describes the structure of the replication: steps, jobs, paths, and job settings.

   - ``rerun_log.txt`` 
     Contains execution logs from the **Execution Panel**, showing step and job progress.

   - ``rerun_readme.md`` 
     A consolidated documentation file containing system information and user-provided notes from the project, steps, and jobs.

   - ``rerun_replication_tree.txt``  
     A tree-style representation of the replication folder structure (generated before execution).

   - **Job-level configuration files**  
     Created for each job depending on the runtime used:
     
    - ``profile.do`` (Stata)   
    - ``config.R`` (R)   
    - ``config.py`` (Python)   

     These files define the environment and paths used during job execution (see :doc:`Configuration Files <configuration_files>`).


7. **Re-run**

   You can repeat an analysis by loading an existing replication. Start the app; in the **Load Replication** panel, provide the following paths:

   - **Input Path**  
     The directory of the replication you want to re-run.  
     This must be a numbered folder (e.g., ``Rep001``, ``Rep002``) containing ``rerun_config.json``.  
     If ``rerun_config.json`` is missing, ReRun cannot restore the replication and will display an error.

   - **Output Path**  
     Optional.  
     If **left empty**, ReRun will create a new directory inside the **Input Path** following the same structure used when creating a new replication:

     .. code-block:: text

        InputPath/
            Replications/
                Rep00X/

     where ``Rep00X`` is the next available replication number.  
     If you prefer the outputs to be written elsewhere, you must explicitly provide a different **Output Path**.

   - **Restricted Data Path**  
     If not specified, ReRun will use the restricted data path stored in ``rerun_config.json``.  
     If you want to run the replication with a different dataset or a relocated data directory, you must provide the new path here.

   - **Non-restricted Data Path**  
     If not specified, ReRun will use the shareable data path stored in ``rerun_config.json``.  


  Please note that the user can add, remove, or adjust any component of the loaded replication.


Directory Structure
-------------------

A typical project managed by ReRun has the following layout:

.. code-block:: text

   Replications/Rep001/
   ├── rerun_config.json
   ├── rerun_log.txt
   ├── rerun_replication_tree.txt
   ├── rerun_readme.md
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
   two_step_example
   certification
   interface_reference


Next Steps
----------

Continue to the next page to see :doc:`A Small Example in Stata <stata_small_example>`.
