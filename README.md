# runcrate-analysis

This repository documents the analysis of Workflow Run RO-Crate objects converted from CWL ROs using [runcrate](https://github.com/ResearchObject/runcrate). 

Here I perform the same analysis as for CWL ROs, described [here](https://doi.org/10.5281/zenodo.7014948). 

## Scenario 1: Analyze representation of CWL metadata fields, human agent, file characteristics, execution details

Commit [7c77b0dabe45e60a2cb87d8320a5c1df592fb477](https://github.com/ResearchObject/runcrate/commit/7c77b0dabe45e60a2cb87d8320a5c1df592fb477). 

RO of workflow with metadata fields for the following workflow elements:

- `label`: Workflow, WorkflowInputParameter, WorkflowOutputParameter, CommandLineTool, CommandInputParameter, CommandOutputParameter, WorkflowStep
- `doc`: Workflow, WorkflowInputParameter, WorkflowOutputParameter, CommandLineTool, CommandInputParameter, CommandOutputParameter, WorkflowStep
- `intent`: Workflow, CommandLineTool
- `format`: WorkflowInputParameter, WorkflowOutputParameter, CommandInputParameter, CommandOutputParameter, WorkflowInputParameter value (File)

Workflow executed with full name and ORCID of human agent.

Results:

- [Human agent](https://github.com/RenskeW/runcrate-analysis/blob/774a2b3c6f00ebe5c68244fa39a660b45618ca25/scenario1/rocrate/ro-crate-metadata.json#L203): represented with name and ORCID in RDF
- Metadata annotations: 
    - `doc`: Only `doc` field of `CommandLineTool` documents is included in `ro-crate-metadata.json`. 
    - `format`: Included for Workflow and CommandLineTool input/output parameters, but not for the actual files used as inputs or generated as outputs.
    - `intent`: Not included in `ro-crate-metadata.json`.
    - `label`: Not included in `ro-crate-metadata.json`.
- File characteristics:
    - basename: Not included in `ro-crate-metadata.json`. 
    - checksum: In CWLProv RO, file ID corresponds to the checksum of the file. In RO-Crate, ID is inherited from CWLProv RO, but not explicitly mentioned as checksum. 
    - creation/modification timestamps: Not included.
    - file size: Not included.
- Start/end timestamps of workflow execution: Represented in `ro-crate-metadata.json` at workflow and step level. 
- Workflow engine: Represented in `ro-crate-metadata.json` with name and version. 
- Workflow description:
    - Workflow: Linked to steps and to CommandLineTools executed in the steps. Programming language is specified. 
    - Parameters: An improvement compared to CWLProv, workflow and CommandLineTool parameters are described as independent entities (`FormalParameter`) in `ro-crate-metadata.json`. 

## Scenario 2: Analyze representation of `SoftwareRequirement`

Commit [7c77b0dabe45e60a2cb87d8320a5c1df592fb477](https://github.com/ResearchObject/runcrate/commit/7c77b0dabe45e60a2cb87d8320a5c1df592fb477). 

RO of workflow containing `SoftwareRequirement` in CommandLineTool description.

- Scenario 2A: Defining default values for WorkflowStepInputParameters gives an error.
- Scenario 2B: Instead of defining default value at WorkflowStep level, defined at CommandInputParameter level. 

Results of analysis of Scenario 2B:

- SoftwareRequirement is not part of `ro-crate-metadata.json`. 

## Scenario 3: Analyze representation of `DockerRequirement`

Commit [7c77b0dabe45e60a2cb87d8320a5c1df592fb477](https://github.com/ResearchObject/runcrate/commit/7c77b0dabe45e60a2cb87d8320a5c1df592fb477). 

RO of workflow containing `DockerRequirement` in CommandLineTool description.

Results of analysis: 

- In contrast to CWLProv RDF provenance graph, the name/tag of the container image is not included in `ro-crate-metadata.json`.

