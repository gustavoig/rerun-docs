A Small Example in Stata (Windows, Local Execution)
===================================================

This example demonstrates how to run a minimal **Stata replication** using **ReRun** in **local mode** on **Windows**.  
The replication consists of a single **Step** and a single **Job**, showing the essential workflow for executing a 
Stata analysis through ReRun without containers.

Example Structure
-----------------

In this example, the project is located in:

``C:\Users\bpu060275\Desktop\rerun_examples\stata_local``

It contains two folders:

.. code-block:: text

   C:\Users\bpu060275\Desktop\rerun_examples\stata_local
   ├── data\
   │   └── auto.dta
   └── scripts\
       └── main.do

- The **data** folder holds the dataset ``auto.dta`` (the built-in Stata automobile dataset).
- The **scripts** folder contains a single script ``main.do``.
- No ``profile.do`` is needed — ReRun automatically generates one with the correct path variables when you launch a job.

The main script
---------------

The ``main.do`` file performs a small analysis using the dataset in the global ``path_source`` (set automatically by ReRun when the user sets the restricted data path in the app).  
It then summarizes the data, runs a simple regression, and writes the results to a log file.

Example content:

.. code-block:: stata

   ***************************************************
   * main.do - Small ReRun Example (Windows Local)
   ***************************************************
   version 18.0
   clear all
   set more off

   include profile.do 
   
   * Change to the main script directory 
   cd "${path_main}"

   log using "auto_example.log", replace

   * Load dataset from ReRun-provided global path
   use "${path_source}/auto.dta", clear

   * Basic inspection
   describe
   summarize

   * Simple regression
   regress price mpg weight

   * Save output log
   log close

Execution Overview
------------------

This example will:

1. **Create one Step** named ``Step01``.
2. **Add one Job** named ``Job01`` that runs the ``main.do`` script.
3. **Select Local backend** and choose the system Stata executable (e.g., ``StataMP-64.exe``).
4. **Run the job** directly from ReRun.
5. **Verify output** in the generated log file ``auto_example.log``.

Expected Output
---------------

After running the job:

- A log file named ``auto_example.log`` will appear in the job directory.
- It contains the ``describe``, ``summarize``, and regression output for the ``auto.dta`` dataset.
- The ReRun log panel will show the job start, completion time, and a success message.

Running the Example in ReRun
----------------------------

This section illustrates, step-by-step, how to launch the ReRun application, create a new replication project for the Stata example, define the step and job, and execute it locally on Windows.  
Each stage is accompanied by screenshots from the ReRun interface.

Launching ReRun
---------------

Open **ReRun** from your desktop or terminal environment.  
The main application window appears, offering options to **Start a new Project** or **Load an existing project**.

.. image:: ../_static/stata_small_example/01_app_window/01_app_window.png
   :alt: ReRun application main window
   :width: 820

To start from scratch, click **Start new project**.

.. image:: ../_static/stata_small_example/01_app_window/03_start_new_replication.png
   :alt: Start new replication button
   :width: 820

Creating a New Replication
--------------------------

After selecting **Start New Replication**, the configuration window appears.  
Here you define the base paths for your project.

.. image:: ../_static/stata_small_example/02_start_load_window/01_start_window.png
   :alt: Start new replication window
   :width: 820

Specify the following paths:

- **Output path** → In this case, ``C:\Users\bpu060275\Desktop\rerun_examples\stata_local``
- **Restricted Data path** → The folder containing your dataset (in this case, ``...stata_local\data``). 

Once all paths are filled, click **Proceed**.

.. image:: ../_static/stata_small_example/02_start_load_window/02_start_window_proceed.png
   :alt: Start button for new replication
   :width: 820

ReRun uses these paths for configuration files that your scripts need.  
These configuration files are created automatically by the app.

Managing Steps
--------------

After initialization, ReRun opens the **Project Explorer View** where you define the main stages of your replication.  
At this point, no steps or jobs are defined:

.. image:: ../_static/stata_small_example/03_project_view/00_blank_project.png
   :alt: Project explorer view
   :width: 820

Click the **Add Step** button to add one step to the project explorer:

.. image:: ../_static/stata_small_example/03_project_view/01_add_step.png
   :alt: Add Step Button
   :width: 820

Click the **Configure Step** button to configure the step.  

.. image:: ../_static/stata_small_example/03_project_view/02_step_configure_button.png
   :alt: Step text field
   :width: 820

You may add a small description to the step.  

.. image:: ../_static/stata_small_example/03_project_view/03_step_input_text.png
   :alt: Step text field
   :width: 820

This text renders as markdown in the **Preview** tab and is saved to a file named ``rerun_readme.md`` in the step directory (e.g. ``Step01``).  
The full replication readme will also include the contents provided in this field.

.. image:: ../_static/stata_small_example/03_project_view/04_step_input_text_md.png
   :alt: Step text field
   :width: 820

To add global notes to the replication, click the **Add Project Notes** button.

.. image:: ../_static/stata_small_example/03_project_view/05_project_notes_button.png
   :alt: Opening project notes
   :width: 820

Provide some general information about your project.  
The text is rendered as markdown in the **Preview** tab:

.. image:: ../_static/stata_small_example/03_project_view/06_project_notes_input_text.png
   :alt: Project notes input text
   :width: 820

.. image:: ../_static/stata_small_example/03_project_view/07_project_notes_input_text_md.png
   :alt: Project notes markdown
   :width: 820

Defining Jobs
-------------

Inside each step, we define one or more jobs by clicking the **Add Job** button:

.. image:: ../_static/stata_small_example/03_project_view/08_add_job_button.png
   :alt: Add job button
   :width: 820


To configure the job, click the button **Configure Job**.

.. image:: ../_static/stata_small_example/03_project_view/09_configure_job_button.png
   :alt: Configure job button
   :width: 820

The Job Configuration panel has two views, one for setting paths, configurations and files for the job and other to document 
the job. To add documentation to one job, click **Toggle description editor**:

.. image:: ../_static/stata_small_example/04_job_config_view/01_toggle_description_editor.png
   :alt: Toggle description editor
   :width: 820


Add a small description for your job.  
This text renders as markdown in the **Preview** tab and is saved to a file named ``rerun_readme.md`` in the job directory (e.g. ``Job01``).  
The full replication readme will also include the contents provided in this field.

.. image:: ../_static/stata_small_example/04_job_config_view/02_job_input_text.png
   :alt: Job description
   :width: 820

.. image:: ../_static/stata_small_example/04_job_config_view/03_job_input_text_md.png
   :alt: Job markdown
   :width: 820

To go back to the configuration view, click **Toggle configuration view**.

.. image:: ../_static/stata_small_example/04_job_config_view/04_toggle_config_view.png
   :alt: Job markdown
   :width: 820

Configuring the Job
-------------------

In the **Job Configuration View**, provide the inputs for the local run example using **Stata**.  

Key settings for this example:

- **Language/Runner** → Stata  
- **Main Path** → ``C:\Users\bpu060275\Desktop\rerun_examples\stata_local\scripts``  
- **Main Script** → ``main.do`` (located in the ``scripts`` folder)  
- **Interpreter/Executable** → Full path to Stata:  
  ``C:\Program Files\StataNow19\StataMP-64.exe``  

.. note::

   The **Main Path** defines the folder that ReRun uses as the source when creating the **Job Path**.  
   All files needed by the job — including the main script and any dependencies — must be located inside this folder or its subdirectories.

   Before execution, ReRun copies the selected contents inside the Main Path into the Job Path.  
   This means:

   - If your main script or dependencies are outside the Main Path, ReRun will not find them and an error will occur.  
   - If your script is inside a subfolder (for example, ``scripts\stata\main.do``), that same subfolder structure will be preserved inside the Job Path.  
   - In this example, since ``main.do`` is directly inside the Main Path (``...\scripts``), it will be copied automatically to the Job Path.


Save your configurations.

.. image:: ../_static/stata_small_example/04_job_config_view/05_job_config_save.png
   :alt: Job config save
   :width: 820

If there are no configuration errors, a message is displayed at bottom of the app and the **Run Project** button in the left panel is enabled.

.. image:: ../_static/stata_small_example/04_job_config_view/06_job_config_save_success.png
   :alt: Job config save success
   :width: 820

.. warning::
   Job configurations are not saved unless you explicitly click the button to save them.

Running the Project
-----------------------

Once your job is defined and saved, click **Run Project** in the left panel.

.. image:: ../_static/stata_small_example/05_project_run/01_run_project_button.png
   :alt: Run workflow button
   :width: 820

ReRun opens the **Execution View**, where you can monitor job progress and logs in real time.

.. image:: ../_static/stata_small_example/05_project_run/02_log_panel.png
   :alt: Log Panel
   :width: 820

If necessary, you can stop the run using the **Stop replication** button.

.. image:: ../_static/stata_small_example/05_project_run/03_stop_project.png
   :alt: Log Panel Stop button
   :width: 820

When the project finishes, ReRun displays a completion message.

.. image:: ../_static/stata_small_example/05_project_run/04_job_completed.png
   :alt: Replication completed message
   :width: 820


Output
------

After the job completes successfully, ReRun automatically creates a structured and versioned output folder under the specified **Output Path**.  
A parent directory named ``Replications`` is created (if it does not already exist), and each new replication receives a numbered subfolder (``Rep001``, ``Rep002``, etc.) to ensure previous runs are preserved.

Example output structure:

.. code-block:: text

   └─── Rep001
       ├── rerun_version
       ├── rerun_config.json
       ├── rerun_log.txt
       ├── rerun_readme.md
       ├── rerun_replication_tree.txt
       │
       └─── Step01
           ├── rerun_readme.md
           │
           └─── Job01
               ├── auto_example.log
               ├── main.do
               ├── main.log
               ├── profile.do
               ├── rerun_readme.md
               └── stata_requirements.txt


Configuration and Log Files
---------------------------

**rerun_version** Text file with **ReRun**'s version.

**rerun_config.json** Defines the structure and parameters of the current replication — including output paths, data paths, and step/job definitions.

.. code-block:: json
   :caption: config.json (excerpt)

   {
      "input_path": "",
      "output_path": "C:/Users/bpu060275/Desktop/rerun_examples/stata_local/Replications/Rep001",
      "data_path": "C:/Users/bpu060275/Desktop/rerun_examples/stata_local/data",
      "replication_data_path": "",
      "steps": [
         {
            "index": 1,
            "description": "My first step",
            "skip_step": false,
            "jobs": [
               {
                  "description": "My first job",
                  "index": 1,
                  "configurations": {
                     "main_path": "Step01/Job01",
                     "main_script": "main.do",
                     "container_definition": "",
                     "container": "",
                     "command": "C:\\Program Files\\StataNow19\\StataMP-64.exe",
                     "tools_path": "",
                     "container_bindings": [],
                     "kill_all": true
                  }
               }
            ]
         }
      ]
   }

This file captures all configuration metadata required to reproduce the run, including container 
images, files, paths, and commands.


**rerun_log.txt** Chronological execution log that records every action performed by ReRun during setup and execution.

.. code-block:: text
   :caption: log.txt (excerpt)

   [2025-10-23 14:32:14]  Execution started...
   [2025-10-23 14:32:14]  'Step 1' starting...
   [2025-10-23 14:32:14]  [ Step 1 ] 'Job 1' starting...
   [2025-10-23 14:32:14]  [ Step 1 ] [ Job 1 ] PID: 14480
   [2025-10-23 14:32:16]  [ Step 1 ] 'Job 1' completed successfully in 0:00:02
   [2025-10-23 14:32:17]  Replication completed.

This file provides full traceability of the execution process.


**rerun_readme.md** Automatically generated documentation that consolidates information from the replication, steps, and jobs.

.. code-block:: markdown
   :caption: readme.md (excerpt)

   <!-- From: rerun_readme.md -->

   My first project

   **Run time:** 0:00:37
   **Storage space used:**
   - **C:/Users/bpu060275/Desktop/rerun_examples/stata_local/Replications/Rep001:** 24.43 KB
   - **C:/Users/bpu060275/Desktop/rerun_examples/stata_local/data:** 12.47 KB

   **System info:**
   - **OS:** Windows
   - **OS Version:** 10.0.26100
   - **OS Release:** 11
   - **Machine:** AMD64
   - **Processor:** Intel64 Family 6 Model 140 Stepping 1, GenuineIntel
   - **CPU Cores (Physical):** 4
   - **CPU Cores (Logical):** 8
   - **RAM Total (GB):** 15.71
   - **Disk Total (GB):** 474.25
   - **Disk Used (GB):** 274.68
   - **Disk Free (GB):** 199.57


   <!-- From: Step01/rerun_readme.md -->

   My first step

   <!-- From: Step01/Job01/rerun_readme.md -->

   My first job

This serves as a self-contained human-readable summary of the replication.


**rerun_replication_tree.txt** Provides a tree-like representation of the project structure (pre-run).

.. code-block:: text
   :caption: replication_tree.txt

   Root: C:/Users/bpu060275/Desktop/rerun_examples/stata_local/Replications/Rep001
   ├── rerun_config.json
   └── Step01/
      ├── rerun_readme.md
      └── Job01/
         ├── main.do
         ├── profile.do
         └── rerun_readme.md

   2 directories, 5 files

This lightweight index helps users quickly inspect the structure of a replication from the command line or within version control.


Within each **Step** folder:

- Each step has its own ``rerun_readme.md`` summarizing its content.  
- The **Job** folder (e.g., ``Job01``) contains all the files required to run and reproduce that job:
- ``auto_example.log`` – The Stata output log generated by the main script.  
- ``main.do`` – The job’s main Stata script.  
- ``main.log`` – Execution log capturing command-level details (automatically created by Stata in batch mode).  
- ``profile.do`` – Automatically generated by ReRun; defines path variables like ``path_main`` and ``path_source``.  
- ``stata_requirements.txt`` – A record of required Stata packages and its version (requires the installation of the Stata package `stata-require <https://github.com/sergiocorreia/stata-require>`_).



Reproducibility and Versioning
------------------------------

Each replication run receives a unique **Rep###** identifier. Combined with configuration metadata, this guarantees 
that analyses can be reproduced even across different systems.

.. note::

   The ``Replications`` folder acts as a permanent record of analytical runs.  
   Each numbered replication contains all the information needed to repeat or audit the analysis later.

.. note::

   The ``Rep###`` numbering ensures that each replication run is kept separate and never overwrites a previous one.  
   You can safely run new replications without manually managing output directories.
