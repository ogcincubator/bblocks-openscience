## Vegetation Productivity Trend Workflow Provenance Profile

This Building Block contains the provenance description of a vegetation productivity trend workflow developed as part of the [PEOPLE-ECCO](https://www.people-ecco.eu/) project and profiled within the [Open Science Persitent Demonstrator 2026](https://www.ogc.org/de/initiatives/open-science-persistent-demonstrator-2026/) initiative.

The provenance representation follows [W3C PROV](https://www.w3.org/TR/prov-overview/), to be more specific its JSON schema as defined in the [Provenance Chain](https://ogcincubator.github.io/bblock-prov-schema/bblock/ogc.ogc-utils.prov) Building Block.

### Conformance to the Workflow Provenance Graph profile

This block profiles the [Workflow Provenance Graph](bblock://ogc.osc.prov-profiles.workflow-graph),
so every activity must be a [Registered Processing Step](bblock://ogc.osc.prov-profiles.processing-step):
its `activityType` must give a process type, from a governed register, more specific than `prov:Activity`, and it must have an output.
Each node gives its PROV class in `provType`, and `entityType`, `activityType` and `agentType`
carry only the specific types.
The example conforms. Its post-processing steps are typed with local CURIEs (`ex:CogConversion`,
`ex:StacMetadataCreation`), which the schema accepts as specific types; mapping them to registered
process types is still to be done, and can only be checked against the register.

The workflow is orchestrated by [Prefect](https://www.prefect.io/). The run, its plan and its runner
are typed with the generic workflow classes of the
[activity type register profile](https://w3id.org/ogc/rim/activity-type/):
`ex:vegetation_productivity_run` is an `acttype:WorkflowRun`, the Prefect flow
`ex:vegetation_productivity_flow` an `acttype:WorkflowPlan` and `ex:prefect` an `acttype:WorkflowRunner`.
The run uses the inputs that no step generated (the Sentinel-2 collection and the workflow
parameters `ex:workflow_parameters`, which steps 1 and 2 share) and generates the output of the last step (the Seasonal Sen Slope STAC collection),
by reference only.
The analyst is responsible for the run through Prefect, which acts on their behalf.
Each step points to the run it belongs to with `isPartOf`.
