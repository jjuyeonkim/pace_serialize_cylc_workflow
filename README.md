# Cylc Workflow Exploration

This document details an initial effort to automate SerialBox savepoint generation on Gaea C5. Given the complexity of the build process—involving numerous dependencies, specific tool versions, and distinct codebases—the goal was to create a reliable, "push-button" solution for generating reference data. 

Cylc was selected for this workflow due to its prevalence within the lab, though the process is adaptable to other workflow engines. 

> ⚠️ **Work-In-Progress Notice:** This document outlines configurations explored during an initial phase. It is not fully complete due to time constraints.

---

## 1. Prerequisites (Conda Setup)

Set up the environment using Conda and install the necessary Cylc components. 

> 📌 **Note:** The Cylc UI server currently requires Python 3.8–3.9.

```bash
module load cylc

# Create and activate environment
conda create -y --name serial_cylc python=3.9
conda activate serial_cylc

# Install Cylc components
conda install -c conda-forge cylc-flow
conda install -c conda-forge cylc-uiserver
```

## 2. Running the Workflow
To execute the workflow, you must first validate the syntax, install the workflow into the Cylc run directory, and then start the execution.

```bash
(serial_cylc) ~/cylc-src/pace-serialize-workflow> cylc validate .
(serial_cylc) ~/cylc-src/pace-serialize-workflow> cylc install .
(serial_cylc) ~/cylc-src/pace-serialize-workflow> cylc play pace_serialize_cylc_workflow
```

## 3. Output
When running pace_serialize_cylc_workflow, the final run script in the run-aquaplanet-collection step outputs data directly into the following directories:

You can grep the log output for the WORKDIR: 
```bash
grep WORKDIR ~/cylc-run/pace_serialize_cylc_workflow/run1/share/SHiELD_dev/SHiELD_build/RTS/GAEA_RTS/serialbox/stdout/C12_res_aquaplanet.*
```

Serialized Reference Data will be within the WORKDIR, located in rundir/test_data/.
