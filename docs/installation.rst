Installation
============

This page explains how to install and configure **ReRun**.  
ReRun runs on **Windows** and **Linux**, and can execute analyses with **locally installed software** (Stata, Python, R) or inside **containers** (Docker or Singularity) for reproducibility.


1. System Requirements
----------------------

**Operating Systems**

- Windows 10 or later
- Linux
- macOS: currently limited (FilePicker bug in Flet v0.28.3)

.. note::

   In Linux, **ReRun** depends on **Zenity**. To install Zenity on Ubuntu/Debian run the following command:

   .. code-block:: bash

      sudo apt-get install zenity



**Runtime**

- Python 3.10+

**Requirements**

- ``flet-cli>=0.28.3``
- ``flet-desktop>=0.28.3``
- ``psutil``

**Analysis Runtimes (as needed)**

- Stata
- Python
- R

**Optional (for containerized execution)**

- Docker
- Apptainer (Singularity)


2. Get the Source
-----------------

Clone the repository:

.. code-block:: bash

   git clone https://github.com/your-org/rerun.git
   cd rerun

Or download the ZIP from your repository hosting and extract it to a folder.


3. Create and Activate a Virtual Environment
--------------------------------------------

It is recommended to isolate ReRun’s dependencies.

.. code-block:: bash

   python -m venv .venv

**Windows (PowerShell):**

.. code-block:: powershell

   .venv\Scripts\Activate.ps1

**Linux:**

.. code-block:: bash

   source .venv/bin/activate


4. Install Dependencies
-----------------------

.. code-block:: bash

   pip install -r requirements.txt



5. Launch ReRun
---------------

From the project root (with the virtual environment active):

.. code-block:: bash

   python main.py

A desktop window should open with the ReRun interface.  
If you see errors in the terminal, check the messages and consult the Troubleshooting section.



6. Verifying Your Installation
------------------------------

After launching ReRun:

1. **Interface check:** The main window should load without errors.
2. **Workflow check:** Create a minimal workflow with one Step and one Job.
3. **Execution check:** Run the job using your chosen backend (Local, Docker, or Singularity).
4. **Logs check:** Confirm that logs show start/end timestamps and exit status.

If anything fails, capture the logs in your home path and review the :doc:`Troubleshooting <troubleshooting>` page.


7. Next Steps
-------------

- Read the :doc:`Usage <usage/index>` section to create Steps and Jobs and to run workflows.
- Consult :doc:`Troubleshooting <troubleshooting>` for common issues and diagnostics.
