Troubleshooting
===============

ReRun includes built-in logging to help diagnose application-level errors.  
If something unexpected happens while using the app, ReRun automatically writes diagnostic logs to:

``~/.rerun/logs`` 


(where ``~`` refers to the user’s home directory).


Log Contents
------------

Inside the ``.rerun/logs`` directory, you will find timestamped log files such as:

- ``log_2025-11-28_15-32-10.log``

These files may contain:

- stack traces for internal errors,
- issues with file paths or permissions,
- UI or filesystem-related exceptions,
- unexpected failures loading or saving replications.


Reporting Issues
----------------

If you encounter a bug or suspect unexpected behavior:

1. Locate the latest log file inside:

``~/.rerun/logs`` 


2. Open a new issue on GitHub:

https://github.com/BPLIM/rerun/issues

3. Attach:   

- the error message shown inside ReRun (if any),
- the relevant log file(s),
- a short description of what you were trying to do,
- your OS, backend mode (Local/Docker/Singularity), and version of ReRun.

Providing logs allows developers to diagnose and resolve issues more quickly.


Common Sources of Errors
------------------------

Although most issues will be self-explanatory inside the logs, the following are frequent causes:

- **Missing Stata license in Docker/Singularity:** if running Stata inside a container, ``stata.lic`` must exist in the container or be provided as a container binding.

- **File-permission issues:** ReRun must be able to read/write inside the output directory and replication folder.

If none of the above applies, please report the issue with logs attached.
