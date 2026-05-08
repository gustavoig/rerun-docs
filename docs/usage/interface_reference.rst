Interface Reference
===================

This page is a complete UI inventory for ReRun, based strictly on current UI components in ``src/rerun/ui``.


Welcome View
------------

Initial landing screen (`WelcomeView`) with entry points to start or load a project, plus an About toggle.

**Start View**

Overview of the welcome screen before choosing a workflow.

.. image:: ../_static/ui_reference/01_welcome_view/01_start_view.png
   :alt: Start View
   :width: 900

**Start Project**

Starts a new project and opens the start-path workflow.

.. image:: ../_static/ui_reference/01_welcome_view/02_start_project.png
   :alt: Start Project
   :width: 900

**Load Project**

Opens the load-project workflow for an existing replication.

.. image:: ../_static/ui_reference/01_welcome_view/03_load_project.png
   :alt: Load Project
   :width: 900

**About**

Switches to the About panel from the welcome screen.

.. image:: ../_static/ui_reference/01_welcome_view/04_about.png
   :alt: About
   :width: 900

About View
----------

About panel content from the welcome screen, including repository and documentation links.

**About View**

Overview of the About panel with app description and metadata.

.. image:: ../_static/ui_reference/02_about_view/01_about_view.png
   :alt: About View
   :width: 900

**Back**

Returns from the About panel to the welcome options.

.. image:: ../_static/ui_reference/02_about_view/02_back.png
   :alt: Back
   :width: 900

**Github**

Opens the project repository link from the About panel.

.. image:: ../_static/ui_reference/02_about_view/03_github.png
   :alt: Github
   :width: 900

**Documentation**

Opens the documentation link from the About panel.

.. image:: ../_static/ui_reference/02_about_view/04_documentation.png
   :alt: Documentation
   :width: 900

Start New Project View
----------------------

`StartProjectView` path form used to create a new replication context.

**Start View**

Overview of the welcome screen before choosing a workflow.

.. image:: ../_static/ui_reference/03_start_view/01_start_view.png
   :alt: Start View
   :width: 900

**Output Path**

Output path field for selecting where replication artifacts are written.

.. image:: ../_static/ui_reference/03_start_view/02_output_path.png
   :alt: Output Path
   :width: 900

**Browse**

Opens file/directory chooser for the current path input.

.. image:: ../_static/ui_reference/03_start_view/03_browse.png
   :alt: Browse
   :width: 900

**Remove**

Clears the selected path from the current path input.

.. image:: ../_static/ui_reference/03_start_view/04_remove.png
   :alt: Remove
   :width: 900

**Restricted Data Path**

Restricted data path field used by runtime configuration.

.. image:: ../_static/ui_reference/03_start_view/05_restricted_data_path.png
   :alt: Restricted Data Path
   :width: 900

**Non Restricted Data Path**

Non-restricted/shareable data path field copied into outputs.

.. image:: ../_static/ui_reference/03_start_view/06_non_restricted_data_path.png
   :alt: Non Restricted Data Path
   :width: 900

**Back**

Navigates back to the previous workflow screen.

.. image:: ../_static/ui_reference/03_start_view/07_back.png
   :alt: Back
   :width: 900

**Proceed**

Validates selected paths and proceeds to the project configuration.

.. image:: ../_static/ui_reference/03_start_view/08_proceed.png
   :alt: Proceed
   :width: 900

Load Existing Project View
--------------------------

`LoadProjectView` form used to restore an existing replication and optionally override paths.

**Load Project View**

Overview of the load-project form and required/optional path fields.

.. image:: ../_static/ui_reference/04_load_project_view/01_load_project_view.png
   :alt: Load Project View
   :width: 900

**Input Path**

Input path selector for an existing replication folder.

.. image:: ../_static/ui_reference/04_load_project_view/02_input_path.png
   :alt: Input Path
   :width: 900

**Browse**

Opens file/directory chooser for the current path input.

.. image:: ../_static/ui_reference/04_load_project_view/03_browse.png
   :alt: Browse
   :width: 900

**Remove**

Clears the selected path from the current path input.

.. image:: ../_static/ui_reference/04_load_project_view/04_remove.png
   :alt: Remove
   :width: 900

**Output Path**

Output path field for selecting where replication artifacts are written.

.. image:: ../_static/ui_reference/04_load_project_view/05_output_path.png
   :alt: Output Path
   :width: 900

**Restricted Data Path**

Optional restricted-data override for the loaded replication.

.. image:: ../_static/ui_reference/04_load_project_view/06_restricted_data_path.png
   :alt: Restricted Data Path
   :width: 900

**Non-Restricted Data Path**

Optional non-restricted data override for the loaded replication.

.. image:: ../_static/ui_reference/04_load_project_view/07_non_restricted-data-path.png
   :alt: Non-RestrictedRestricted Data Path
   :width: 900

**Back**

Navigates back to the previous workflow screen.

.. image:: ../_static/ui_reference/04_load_project_view/08_back.png
   :alt: Back
   :width: 900

**Proceed**

Validates selected paths and attempts to load the saved project configuration.

.. image:: ../_static/ui_reference/04_load_project_view/09_proceed.png
   :alt: Proceed
   :width: 900

Project Node (Left Panel)
-------------------------

Top-level project controls in the tree header (`ProjectNode`).

**Project Node**

Project header row in the left tree with global project actions.

.. image:: ../_static/ui_reference/05_project_node/01_project_node.png
   :alt: Project Node
   :width: 900

**Add Step**

Adds a new step node to the project tree.

.. image:: ../_static/ui_reference/05_project_node/02_add_step.png
   :alt: Add Step
   :width: 900

**Configure Certification**

Opens certification settings for the current project.

.. image:: ../_static/ui_reference/05_project_node/03_configure_certification.png
   :alt: Configure Certification
   :width: 900

**Add Project Notes**

Opens project notes editor for project-level markdown documentation.

.. image:: ../_static/ui_reference/05_project_node/04_add_project_notes.png
   :alt: Add Project Notes
   :width: 900

**Reset Replication Paths**

Opens the path-reset view to update replication path settings.

.. image:: ../_static/ui_reference/05_project_node/05_reset_replication_paths.png
   :alt: Reset Replication Paths
   :width: 900

**Restart Project**

Restarts the project session from the tree header action.

.. image:: ../_static/ui_reference/05_project_node/06_restart_project.png
   :alt: Restart Project
   :width: 900

Certification Settings View
---------------------------

`CertificationView` controls for TRO/TRACE certification settings.

**Certification View**

Overview of certification settings sections and controls.

.. image:: ../_static/ui_reference/06_certification_view/01_certification_view.png
   :alt: Certification View
   :width: 900

**Enable Certification**

Toggles certification settings on/off and enables related fields.

.. image:: ../_static/ui_reference/06_certification_view/02_enable_certification.png
   :alt: Enable Certification
   :width: 900

**Trs File Path**

Selects the TRS profile path used for certification.

.. image:: ../_static/ui_reference/06_certification_view/03_trs_file_path.png
   :alt: Trs File Path
   :width: 900

**Browse**

Opens file/directory chooser for the current path input.

.. image:: ../_static/ui_reference/06_certification_view/04_browse.png
   :alt: Browse
   :width: 900

**Remove**

Clears the selected path from the current path input.

.. image:: ../_static/ui_reference/06_certification_view/05_remove.png
   :alt: Remove
   :width: 900

**GPG Directory Path**

Sets the GPG directory path used for signing operations.

.. image:: ../_static/ui_reference/06_certification_view/06_gpl_directory_path.png
   :alt: GPG Directory Path
   :width: 900

**GPG Fingerprint**

GPG fingerprint field used for signature identity.

.. image:: ../_static/ui_reference/06_certification_view/07_gpl_fingerprint.png
   :alt: GPG Fingerprint
   :width: 900

**GPG Passphrase**

GPG passphrase field (masked input).

.. image:: ../_static/ui_reference/06_certification_view/08_gpl_passphrase.png
   :alt: GPG Passphrase
   :width: 900

**Enable Signing**

Enables or disables signing behavior for certification.

.. image:: ../_static/ui_reference/06_certification_view/09_enable_signing.png
   :alt: Enable Signing
   :width: 900

**Enable Timestamp Request**

Enables or disables trusted timestamp requests.

.. image:: ../_static/ui_reference/06_certification_view/10_enable_timestamp_request.png
   :alt: Enable Timestamp Request
   :width: 900

**Http Proxy**

HTTP proxy setting used during certification network calls.

.. image:: ../_static/ui_reference/06_certification_view/11_http_proxy.png
   :alt: Http Proxy
   :width: 900

**Https Proxy**

HTTPS proxy setting used during certification network calls.

.. image:: ../_static/ui_reference/06_certification_view/12_https_proxy.png
   :alt: Https Proxy
   :width: 900

**Import Settings**

Imports certification settings from a JSON file.

.. image:: ../_static/ui_reference/06_certification_view/13_import_settings.png
   :alt: Import Settings
   :width: 900

**Export Settings**

Exports current certification settings to a JSON file.

.. image:: ../_static/ui_reference/06_certification_view/14_export_settings.png
   :alt: Export Settings
   :width: 900

**Save**

Saves certification settings to the current project state.

.. image:: ../_static/ui_reference/06_certification_view/15_save.png
   :alt: Save
   :width: 900

Project Notes View
------------------

`ProjectConfigView` markdown editor for project-level notes.

**Project Notes Views**

Overview of the project notes editor view.

.. image:: ../_static/ui_reference/07_project_notes_view/01_project_notes_views.png
   :alt: Project Notes Views
   :width: 900

**Write**

Write mode for project notes markdown content.

.. image:: ../_static/ui_reference/07_project_notes_view/02_write.png
   :alt: Write
   :width: 900

**Preview**

Preview mode rendering project notes markdown.

.. image:: ../_static/ui_reference/07_project_notes_view/03_preview.png
   :alt: Preview
   :width: 900

Reset Replication Paths View
----------------------------

`ResetReplicationPathsView` for editing saved replication paths in active mode.

**Reset Replication Paths View**

Overview of path reset form for active projects.

.. image:: ../_static/ui_reference/08_reset_replication_paths_view/01_reset_replication_paths_view.png
   :alt: Reset Replication Paths View
   :width: 900

**Output Path**

Output path field for selecting where replication artifacts are written.

.. image:: ../_static/ui_reference/08_reset_replication_paths_view/02_output_path.png
   :alt: Output Path
   :width: 900

**Browse**

Opens file/directory chooser for the current path input.

.. image:: ../_static/ui_reference/08_reset_replication_paths_view/03_browse.png
   :alt: Browse
   :width: 900

**Remove**

Clears the selected path from the current path input.

.. image:: ../_static/ui_reference/08_reset_replication_paths_view/04_remove.png
   :alt: Remove
   :width: 900

**Restricted Data Path**

Restricted data path field used by runtime configuration.

.. image:: ../_static/ui_reference/08_reset_replication_paths_view/05_restricted_data_path.png
   :alt: Restricted Data Path
   :width: 900

**Non Restricted Data Path**

Non-restricted/shareable data path field copied into outputs.

.. image:: ../_static/ui_reference/08_reset_replication_paths_view/06_non_restricted_data_path.png
   :alt: Non Restricted Data Path
   :width: 900

**Save**

Validates and saves updated replication paths.

.. image:: ../_static/ui_reference/08_reset_replication_paths_view/07_save.png
   :alt: Save
   :width: 900

Step Node (Left Panel)
----------------------

Per-step controls in the left tree (`StepNode`).

**Step Node**

Overview of one step row and its inline controls.

.. image:: ../_static/ui_reference/09_step_node/01_step_node.png
   :alt: Step Node
   :width: 900

**Configure Step**

Opens step configuration editor for description and skip flag.

.. image:: ../_static/ui_reference/09_step_node/02_configure_step.png
   :alt: Configure Step
   :width: 900

**Add Job**

Adds a new job under the selected step.

.. image:: ../_static/ui_reference/09_step_node/03_add_job.png
   :alt: Add Job
   :width: 900

**Duplicate Step**

Duplicates a configured step (enabled when rules permit).

.. image:: ../_static/ui_reference/09_step_node/04_duplicate_step.png
   :alt: Duplicate Step
   :width: 900

**Delete Step**

Deletes the selected step node.

.. image:: ../_static/ui_reference/09_step_node/05_delete_step.png
   :alt: Delete Step
   :width: 900

**Checkboxes**

Step/job selection checkboxes for bulk actions.

.. image:: ../_static/ui_reference/09_step_node/06_checkboxes.png
   :alt: Checkboxes
   :width: 900

**Delete Multiple Nodes**

Deletes multiple selected step nodes.

.. image:: ../_static/ui_reference/09_step_node/07_delete_multiple_nodes.png
   :alt: Delete Multiple Nodes
   :width: 900

Step Configuration View
-----------------------

`StepConfigView` for step description and skip behavior.

**Step Config View**

Overview of step description editor and skip checkbox.

.. image:: ../_static/ui_reference/10_step_config_view/01_step_config_view.png
   :alt: Step Config View
   :width: 900

**Write**

Write mode for step markdown description.

.. image:: ../_static/ui_reference/10_step_config_view/03_write.png
   :alt: Write
   :width: 900

**Preview**

Preview mode for step markdown description.

.. image:: ../_static/ui_reference/10_step_config_view/04_preview.png
   :alt: Preview
   :width: 900

**Skip Step**

Toggles whether the step should be skipped during execution. In this case, the contents of the step are copied 
to the output directory but not run.

.. image:: ../_static/ui_reference/10_step_config_view/05_skip_step.png
   :alt: Skip Step
   :width: 900

Job Node (Left Panel)
---------------------

Per-job controls in the left tree (`JobNode`).

**Job Node**

Overview of one job row and its inline controls.

.. image:: ../_static/ui_reference/11_job_node/01_job_node.png
   :alt: Job Node
   :width: 900

**Configure Job**

Opens job configuration editor for the selected job.

.. image:: ../_static/ui_reference/11_job_node/02_configure_job.png
   :alt: Configure Job
   :width: 900

**Duplicate Job**

Duplicates a configured job under the same step.

.. image:: ../_static/ui_reference/11_job_node/03_duplicate_job.png
   :alt: Duplicate Job
   :width: 900

**Delete Job**

Deletes the selected job node.

.. image:: ../_static/ui_reference/11_job_node/04_delete_job.png
   :alt: Delete Job
   :width: 900

**Checkboxes**

Job selection checkboxes for bulk actions.

.. image:: ../_static/ui_reference/11_job_node/05_checkboxes.png
   :alt: Checkboxes
   :width: 900

**Delete Multiple Nodes**

Deletes multiple selected job nodes.

.. image:: ../_static/ui_reference/11_job_node/06_delete_multiple_nodes.png
   :alt: Delete Multiple Nodes
   :width: 900

Job Configuration View (Configurations)
---------------------------------------

Configuration controls from `JobConfigView` (paths, runtime, container, dependencies).

**Job Config View Configurations**

Overview of job configuration fields and validation status.

.. image:: ../_static/ui_reference/12_job_config_view_configurations/01_job_config_view_configurations.png
   :alt: Job Config View Configurations
   :width: 900


**Main Path**

Directory path containing files required by the job.

.. image:: ../_static/ui_reference/12_job_config_view_configurations/03_main_path.png
   :alt: Main Path
   :width: 900

**Browse**

Opens file/directory chooser for the current path input.

.. image:: ../_static/ui_reference/12_job_config_view_configurations/04_browse.png
   :alt: Browse
   :width: 900

**Remove**

Clears the selected path from the current path input.

.. image:: ../_static/ui_reference/12_job_config_view_configurations/05_remove.png
   :alt: Remove
   :width: 900

**Main Script**

Main script path for the job.

.. image:: ../_static/ui_reference/12_job_config_view_configurations/06_main_script.png
   :alt: Main Script
   :width: 900

**Executable**

Executable/interpreter used to run the main script.

.. image:: ../_static/ui_reference/12_job_config_view_configurations/07_executable.png
   :alt: Executable
   :width: 900

**Dependencies**

Optional dependencies that are copied/registered with the job.

.. image:: ../_static/ui_reference/12_job_config_view_configurations/08_dependencies.png
   :alt: Dependencies
   :width: 900

**Tools Path**

Optional tools directory copied into the job runtime context.

.. image:: ../_static/ui_reference/12_job_config_view_configurations/09_tools_path.png
   :alt: Tools Path
   :width: 900

**Container Image**

Optional Docker image or Singularity/Apptainer artifact.

.. image:: ../_static/ui_reference/12_job_config_view_configurations/10_container_image.png
   :alt: Container Image
   :width: 900

**Container Definition**

Optional container definition/build script path.

.. image:: ../_static/ui_reference/12_job_config_view_configurations/11_container_definition.png
   :alt: Container Definition
   :width: 900

**Container Bindings**

Container bindings table for host->container mounts.

.. image:: ../_static/ui_reference/12_job_config_view_configurations/12_container_bindings.png
   :alt: Container Bindings
   :width: 900

**Save**

Saves job configuration changes for the selected job.

.. image:: ../_static/ui_reference/12_job_config_view_configurations/13_save.png
   :alt: Save
   :width: 900

**Kill All Jobs If This Job Fails**

Failure policy toggle to stop all jobs if this job fails.

.. image:: ../_static/ui_reference/12_job_config_view_configurations/14_kill_all_jobs_if_this_job_fails.png
   :alt: Kill All Jobs If This Job Fails
   :width: 900

Job Configuration View (Notes)
------------------------------

Notes/editor mode of `JobConfigView`, including write/preview and save/navigation actions.

**Job Config View Notes**

Overview of the job notes editor mode.

.. image:: ../_static/ui_reference/13_job_config_view_notes/01_job_config_view_notes.png
   :alt: Job Config View Notes
   :width: 900

**Write**

Write mode for job notes markdown.

.. image:: ../_static/ui_reference/13_job_config_view_notes/02_write.png
   :alt: Write
   :width: 900

**Preview**

Preview mode for job notes markdown.

.. image:: ../_static/ui_reference/13_job_config_view_notes/03_preview.png
   :alt: Preview
   :width: 900

**Back to Configuration**

Returns to configuration mode from notes or navigates back as shown.

.. image:: ../_static/ui_reference/13_job_config_view_notes/05_configuration_or_back.png
   :alt: Configuration Or Back
   :width: 900


Run Project Action
------------------

`Run Project` trigger in the left tree footer (`LeftTreeView`).

**Run Project**

Runs the configured project from the left panel footer.

.. image:: ../_static/ui_reference/14_run_project_button/01_run_project.png
   :alt: Run Project
   :width: 900

Run & Log Panel View
--------------------

Execution-time log panel from `RunView`, including start/stop/completion states.

**Start Replication**

Run view just after execution starts; logs begin streaming.

.. image:: ../_static/ui_reference/15_log_panel_view/01_start_replication.png
   :alt: Start Replication
   :width: 900

**Stop Replication**

Stop button and confirmation flow while a run is in progress.

.. image:: ../_static/ui_reference/15_log_panel_view/02_stop_replication.png
   :alt: Stop Replication
   :width: 900

**Replication Completed**

Completed-state run view after replication finishes.

.. image:: ../_static/ui_reference/15_log_panel_view/03_replication_completed.png
   :alt: Replication Completed
   :width: 900