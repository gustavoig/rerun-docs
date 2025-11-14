A Containerized Example (Stata, Parallel Jobs)
==============================================

This example demonstrates how to run **two Stata jobs in parallel** inside the **same Step**, using a **Docker container** as the execution backend in ReRun.  
Both jobs read from the same dataset, perform independent analyses, and write their outputs to separate job folders.

This example illustrates:

- How to configure Stata jobs to run inside a Docker container.
- How parallelization works inside a single Step.
- How ReRun isolates job environments and organizes outputs.


Example Input Structure
-----------------------

Your project directory should contain:

.. code-block:: text

   C:\Users\bpu060275\Desktop\work_container
   ├── data\
   │   └── auto.dta
   └── scripts\
       ├── job1.do
       └── job2.do

- ``data`` contains the dataset.  
- ``scripts`` contains the two Stata jobs.  
- The container will be a **Docker** image with Stata installed named **stata:18**.


Launching the Replication
-------------------------

Starting a New Replication
~~~~~~~~~~~~~~~~~~~~~~~~~~

Click **Start New Replication** in the main application window:

.. image:: ../_static/container_example/01_start_new_replication.png
   :alt: Start new replication
   :width: 640

Provide Input Paths
~~~~~~~~~~~~~~~~~~~

Specify the **Output Path** and **Data Path**, then click **Start**:

.. image:: ../_static/container_example/02_input_paths_and_start.png
   :alt: Input paths and Start button
   :width: 640


Configuring the Step
--------------------

After initialization, the Steps Window opens.  
Click **Configure** on Step 1:

.. image:: ../_static/container_example/03_configure_step.png
   :alt: Configure the step
   :width: 640


Adding the Two Jobs
-------------------

Click **Add Job** in the Jobs Window:

.. image:: ../_static/container_example/04_add_job.png
   :alt: Add Job button
   :width: 640

You may add descriptive text to document this job:

.. image:: ../_static/container_example/05_jobs_text_field.png
   :alt: Job description text field
   :width: 640

Configuring Job 1
~~~~~~~~~~~~~~~~~

Select the job and click **Configure**:

.. image:: ../_static/container_example/06_configure_job1.png
   :alt: Configure Job 1
   :width: 640

Set the container execution parameters:
 
- **Main Path**: your ``scripts`` folder  
- **Main Script**: ``job1.do``  
- **Container Image**: your Docker image with Stata installed ``stata:18`` 
- **Command**: the Stata executable inside the container (e.g., ``stata-mp -b do``)

Then save:

.. image:: ../_static/container_example/07_job1_configurations_and_save.png
   :alt: Job 1 configuration and save
   :width: 640

Do the same for **Job 2**, changing only the script to ``job2.do``.

Finally, save all jobs and return to the Steps Window:

.. image:: ../_static/container_example/08_save_jobs.png
   :alt: Save Jobs button
   :width: 640


Running the Parallel Jobs
-------------------------

Back in the Steps Window, click **Run Steps**:

.. image:: ../_static/container_example/09_run_steps.png
   :alt: Run Steps button
   :width: 640

ReRun opens the **Execution Window**, where both jobs start in parallel using Docker:

Jobs starting:

.. image:: ../_static/container_example/10_running_window_01.png
   :alt: Execution window showing Job 1 starting
   :width: 640

Both jobs executing:

.. image:: ../_static/container_example/10_running_window_02.png
   :alt: Running both jobs
   :width: 640

Job progress and completion:

.. image:: ../_static/container_example/10_running_window_03.png
   :alt: Execution window with progress
   :width: 640


Stata Job Scripts
-----------------

Below are the full contents of the two Stata scripts used in this example.

Job 1 — ``job1.do``
~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: stata
   :caption: job1.do

    ***************************************************
    * Parallel Job 1 (container/local)
    * - Reads data from ${path_source}\auto.dta
    * - EDA, correlation, regression, margins
    * - Writes: job1_example.log
    * - Approx. runtime: 30 seconds
    ***************************************************
    version 18.0
    clear all
    set more off

    include profile.do
    cd "${path_main}"

    log using "job1_example.log", replace

    use "${path_source}\auto.dta", clear

    describe
    summarize price mpg weight, detail
    corr price mpg weight

    regress price mpg weight i.foreign, vce(robust)
    margins foreign
    marginsplot, name(m1, replace) nodraw

    preserve
    collapse (mean) price mpg weight, by(foreign)
    export delimited using "${path_main}\job1_means_by_foreign.csv", replace
    restore

    forvalues t = 1/6 {
        di as txt "Job1 progress: " `t' " / 6"
        sleep 5000
    }

    log close
    exit 0


Job 2 — ``main_job2.do``
~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: stata
   :caption: main_job2.do

    ***************************************************
    * Parallel Job 2 (container/local)
    * - Reads data from ${path_source}\auto.dta
    * - Weight binning, ANOVA, grouped means
    * - Writes: job2_example.log
    * - Approx. runtime: 30 seconds
    ***************************************************
    version 18.0
    clear all
    set more off

    include profile.do
    cd "${path_main}"

    log using "job2_example.log", replace

    use "${path_source}\auto.dta", clear

    generate ln_price = ln(price)
    xtile weight_bin = weight, nq(5)
    label var weight_bin "Weight quintile (1 = lightest, 5 = heaviest)"

    bys weight_bin: summarize price mpg weight

    anova price i.weight_bin

    preserve
    collapse (mean) price mpg weight ln_price, by(weight_bin)
    export delimited using "${path_main}\job2_means_by_weightbin.csv", replace
    restore

    forvalues t = 1/6 {
        di as txt "Job2 progress: " `t' " / 6"
        sleep 5000
    }

    log close
    exit 0


Output Structure
----------------

After the run completes, the replication folder looks like:

.. code-block:: text

   Replications/Rep002/
   ├── config.json
   ├── manifest.json
   ├── log.txt
   ├── readme.md
   ├── Step01/
   │   ├── readme.md
   │   ├── Job01/
   │   │   ├── job1.do
   │   │   ├── job1_example.log
   │   │   ├── job1_means_by_foreign.csv
   │   │   ├── profile.do
   │   │   └── stata_requirements.txt
   │   └── Job02/
   │       ├── job2.do
   │       ├── job2_example.log
   │       ├── job2_means_by_weightbin.csv
   │       ├── profile.do
   │       └── stata_requirements.txt

Each job has its own independent logs, CSVs, and configuration.

Summary
-------

This example shows how to:

1. Configure ReRun to use a **Docker container** for execution.  
2. Create a step with **two parallel Stata jobs**.  
3. Run those jobs simultaneously.  
4. Inspect separate logs and outputs for each job.

This pattern scales to more complex workflows and to other runtimes such as Python and R.
