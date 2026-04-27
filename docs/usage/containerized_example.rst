A Containerized Example (Stata, Parallel Jobs)
==============================================

This example demonstrates how to run **two Stata jobs in parallel** inside the **same Step**, using a **Docker container** as the execution backend in ReRun.  
Both jobs read from the same dataset, perform independent analyses, and write their outputs to separate job folders.

This example illustrates:

- How to configure Stata jobs to run inside a Docker container.
- How parallelization works inside a single Step.
- How ReRun isolates job environments and organizes outputs.

.. warning::
   To run this example, you must have **Docker** installed and running.

   Additionally, ensure that any host directories you bind mount into the container
   are accessible via Docker's *file sharing settings* (for example, on Windows or macOS).

   You are responsible for specifying the bind mounts in the **Job Configuration View**.

   All project files (replication folder, data, scripts, etc.) must be located within
   the directories you mount, and those directories must be permitted in Docker’s
   file sharing configuration.

Example Input Structure
-----------------------

Your project directory should contain:

.. code-block:: text

   C:\Users\bpu060275\Desktop\rerun_examples\stata_docker
   ├── data\
   │   └── auto.dta
   └── scripts\
       ├── job1.do
       └── job2.do

- ``data`` contains the dataset.  
- ``scripts`` contains the two Stata jobs.  
- The container will be a **Docker** image with Stata installed named **stata:18**.


Stata Job Scripts
-----------------

Below are the full contents of the two Stata scripts used in this example.

Job 1 — ``job1.do``
~~~~~~~~~~~~~~~~~~~~

.. code-block:: stata
   :caption: job1.do

    ***************************************************
    * Parallel Job 1 (container/local)
    * - Approx. runtime: 30 seconds
    ***************************************************
    version 18.0
    clear all
    set more off

    include profile.do
    cd "${path_main}"

    log using "job1_example.log", replace

    use "${path_source}/auto.dta", clear

    describe
    summarize price mpg weight, detail
    corr price mpg weight

    regress price mpg weight i.foreign, vce(robust)
    margins foreign
    marginsplot, name(m1, replace) nodraw

    preserve
    collapse (mean) price mpg weight, by(foreign)
    export delimited using "${path_main}/job1_means_by_foreign.csv", replace
    restore

    forvalues t = 1/6 {
        di as txt "Job1 progress: " `t' " / 6"
        sleep 5000
    }

    log close
    exit 0

Job 2 — ``job2.do``
~~~~~~~~~~~~~~~~~~~~

.. code-block:: stata
   :caption: job2.do

    ***************************************************
    * Parallel Job 2 (container/local)
    * - Approx. runtime: 30 seconds
    ***************************************************
    version 18.0
    clear all
    set more off

    include profile.do
    cd "${path_main}"

    log using "job2_example.log", replace

    use "${path_source}/auto.dta", clear

    generate ln_price = ln(price)
    xtile weight_bin = weight, nq(5)
    label var weight_bin "Weight quintile (1 = lightest, 5 = heaviest)"

    bys weight_bin: summarize price mpg weight

    anova price i.weight_bin

    preserve
    collapse (mean) price mpg weight ln_price, by(weight_bin)
    export delimited using "${path_main}/job2_means_by_weightbin.csv", replace
    restore

    forvalues t = 1/6 {
        di as txt "Job2 progress: " `t' " / 6"
        sleep 5000
    }

    log close
    exit 0

Launching the Replication
-------------------------

Starting a New Replication
~~~~~~~~~~~~~~~~~~~~~~~~~~

Click **Start New Replication** in the main application window:

.. image:: ../_static/container_example/01_start_new_replication.png
   :alt: Start new replication
   :width: 820

Provide Input Paths
~~~~~~~~~~~~~~~~~~~

Specify the **Output Path** and **Data Path**, then click **Proceed**:

.. image:: ../_static/container_example/02_input_paths_and_start.png
   :alt: Input paths and Start button
   :width: 820

Configuring the Step
--------------------

After initialization, in the project explorer, click the **Add Step** button to add one step.

.. image:: ../_static/container_example/03_add_step.png
   :alt: Configure the step
   :width: 820

Then click the **Configure Step** button and add a small description.

.. image:: ../_static/container_example/04_configure_step.png
   :alt: Configure the step
   :width: 820

.. image:: ../_static/container_example/05_step_input_text.png
   :alt: Configure the step
   :width: 820

Adding the Two Jobs
-------------------

To add the first job, click **Add Job** in the first step:

.. image:: ../_static/container_example/06_add_job.png
   :alt: Add Job button
   :width: 820


Configuring Job 1
~~~~~~~~~~~~~~~~~

Click the  **Configure Job** button to configure the first job:

.. image:: ../_static/container_example/07_configure_job_button.png
   :alt: Configure Job 1
   :width: 820

Set the container execution parameters:
 
- **Main Path**: your ``scripts`` folder  
- **Main Script**: ``job1.do``  
- **Interpreter**: the Stata executable inside the container (e.g., ``stata-mp``)

- **Container Image**: your Docker image with Stata installed ``stata:18``  
- **Container Bindings**: ``C:\Users\bpu060275`` -> ``/mnt/c/Users/bpu060275``

.. image:: ../_static/container_example/08_job1_configuration_paths.png
   :alt: Job 1 configuration path inputs
   :width: 820

.. image:: ../_static/container_example/09_job1_configuration_container.png
   :alt: Job 1 configuration container inputs
   :width: 820

Save the configurations. The app validates the container and ensures that the specified interpreter / executable exists in the container. 

.. image:: ../_static/container_example/10_job1_validation.png
   :alt: Job 1 configuration validation
   :width: 820

Given that the configurations for **Job 2** will be the same as in **Job 1**, except for the name of the script, we can duplicate 
**Job 2** by clicking the **Duplicate Job** button.

.. image:: ../_static/container_example/11_job1_duplicate.png
   :alt: Job 1 duplication
   :width: 820

Click **Configure Job** in **Job 2**, change the script to ``job2.do``, and save.


.. image:: ../_static/container_example/12_job2_script_path.png
   :alt: Job 2 change script name
   :width: 820

.. image:: ../_static/container_example/13_job2_save.png
   :alt: Job 2 save
   :width: 820

Running the Parallel Jobs
-------------------------

In the left panel, click the **Run Project** button.

.. image:: ../_static/container_example/14_run_project.png
   :alt: Run Project
   :width: 820

ReRun opens the **Execution View**.  
Each job starts its **own Docker container instance**, and because both jobs are launched for the same step, they run **in parallel** as independent processes. 
Since the jobs run in container mode, ReRun first inspects the container metadata and writes it to ``Job##/container_info.json``.


.. image:: ../_static/container_example/15_inspecting_container_metadata.png
   :alt: Inspecting container metadata
   :width: 820

Then the jobs run.


Jobs starting:

.. image:: ../_static/container_example/16_jobs_starting.png
   :alt: Jobs starting
   :width: 820

Both jobs executing:

.. image:: ../_static/container_example/17_jobs_running.png
   :alt: Jobs running
   :width: 820

Job progress and completion:

.. image:: ../_static/container_example/18_jobs_finished.png
   :alt: Jobs finished
   :width: 820

In this example, the entire step finished in **41 seconds** because both jobs were executed
at the same time.  
If the same two jobs were run one after the other, the total runtime would be **over one minute**.

Running jobs in parallel makes the overall process faster, but it comes with trade-offs:
it increases **CPU usage** (because multiple jobs run at once) and may increase **memory (RAM)
usage**, depending on the amount of data each job loads and the operations it performs.  
Users running several jobs in parallel should make sure their system has enough CPU cores
and available memory.



Output Structure
----------------

After the run completes, the replication folder looks like:

.. code-block:: text

   Replications/Rep001
   ├── rerun_version
   ├── rerun_config.json
   ├── rerun_log.txt
   ├── rerun_readme.md
   ├── rerun_replication_tree.txt
   ├── Step01/
   │   ├── rerun_readme.md
   │   ├── Job01/
   │   │   ├── container_info.json   
   │   │   ├── job1.do
   │   │   ├── job1_example.log
   │   │   ├── job1_means_by_foreign.csv
   │   │   ├── profile.do
   │   │   └── job1.log
   │   └── Job02/
   │   │   ├── container_info.json 
   │       ├── job2.do
   │       ├── job2_example.log
   │       ├── job2_means_by_weightbin.csv
   │       ├── profile.do
   │       └── job2.log

Each job has its own independent logs, CSVs, and configuration.


Differences Between Local and Containerized Execution
-----------------------------------------------------

When running locally or inside a Docker/Singularity container, ReRun produces the same replication structure,  
but certain configuration details differ. This section describes the main differences, focusing on:

- Path handling in ``rerun_config.json``  
- How ReRun maps host directories into Docker  
- Differences in the execution command  
- Stata license handling in a container

Path Differences
~~~~~~~~~~~~~~~~

In **local execution**, paths in ``rerun_config.json`` correspond directly to the file system of the host.  
For example:

.. code-block:: json
   :caption: Local ``rerun_config.json`` (excerpt)

   {
       "data_path": "C:/Users/bpu060275/Desktop/rerun_examples/stata_docker/data"
   }

However, during **containerized execution**, ReRun replaces host paths with **container-mounted paths**,  
so that the runtime inside Docker can correctly access the data:

.. code-block:: json
   :caption: Containerized ``rerun_config.json`` (excerpt)

   {
       "data_path": "/mnt/c/Users/bpu060275/Desktop/rerun_examples/stata_docker/data"
   }

These paths only exist **inside the container**, not on the host.

ReRun performs this mapping by mounting the directories specified by the user in the **Container bindings** field into Docker and rewriting paths accordingly, guaranteeing that scripts using the ``path_source`` global can access  
data using the container’s file-system layout.

.. warning::
   When **loading an existing replication** from a containerized execution, 
   the ``data_path`` stored in ``rerun_config.json`` refers to   
   the **container path**, not the host path.  
   Therefore, users **must re-enter the correct Data Path** in the restricted data path field, so ReRun can  
   regenerate the correct host → container path mapping.  

Command Differences
~~~~~~~~~~~~~~~~~~~

Local jobs execute the Stata command directly, for example:

.. code-block:: text
   :caption: Local execution command

   C:\Program Files\StataNow19\StataMP-64.exe /e do main.do

Containerized jobs require executing the runtime inside the Docker container, which is why the command generated by ReRun differs from the local execution command.
These additional Docker arguments are handled automatically by the application, so users do not need to manage them manually.
Below is the full command that ReRun produces for a Stata job:

.. code-block:: text
   :caption: Containerized execution command

   docker run --rm ^
      -w /mnt/c/Users/bpu060275/Desktop/rerun_examples/stata_docker/Replications/Rep001/Step01/Job01 
      -v C:\Users\bpu060275:/mnt/c/Users/bpu060275 ^
      stata:18 ^
      stata-mp -b do job1.do

Below is an explanation of each part:

#. ``-w /mnt/c/Users/bpu060275/Desktop/rerun_examples/stata_docker/Replications/Rep001/Step01/Job01``  

   Sets the **working directory** of the container to the Job Path inside the container,  
   ensuring Stata loads the correct ``profile.do`` and writes logs to the job folder.

#. ``-v C:\Users\bpu060275:/mnt/c/Users/bpu060275``

   ReRun mounts host directories into the container according to the values provided in **Job Config Bindings**. 
   This ensures that all replication files, steps, jobs, and tools remain accessible.  
   All paths inside the job are rewritten using these mounts (e.g., ``/mnt/c/Users/...``).

#. ``stata:18``

   The Docker image used. Users must ensure this image exists locally.

#. ``stata-mp -b do job1.do``  

   Actual execution command inside the container.

Summary of Key Differences
~~~~~~~~~~~~~~~~~~~~~~~~~~
.. list-table::
   :header-rows: 1
   :widths: 25 35 40

   * - Aspect
     - Local Execution
     - Containerized Execution
   * - ``data_path`` in config
     - Host path
     - Container-mounted path
   * - Command used
     - Direct Stata executable
     - ``docker run … stata-mp -b do``
   * - License handling
     - Uses local installation
     - *stata.lic* inside container / Bindings field
   * - Directory handling
     - Normal filesystem
     - Home directory mounted into container
   * - Requirements
     - Stata installed locally
     - Docker + container image + license


These differences ensure that containerized execution provides a fully reproducible, controlled  
environment while still allowing scripts to refer to familiar paths via ReRun’s automatic mappings. 
This pattern scales to more complex workflows and to other runtimes such as Python and R.

.. note::
   This example would be almost identical when using **Apptainer/Singularity** instead of Docker.  
   The only change is that, in the Job Configuration window, you must provide the path to the
   ``.sif`` image for the job.

   Note that Apptainer does **not** run natively on Windows.  
   If you have **WSL** installed and Apptainer available inside it, ReRun will automatically:

   - detect that the backend is Apptainer,
   - run the container inside WSL, and
   - map your replication directory into the WSL environment.

   No additional configuration is required from the user.

   Keep in mind that the execution command differs between Docker and Apptainer.  
   Docker requires explicit directory mounts (e.g., ``-v host_path:container_path``), while  
   Apptainer automatically **binds** several host directories (such as your home folder)  
   into the container.  
   Because of these auto-binds, Apptainer jobs often require fewer arguments in the command
   line, and the file paths inside the container will typically match the host paths more closely.



