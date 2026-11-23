## Cool Spot Workflow Provenance Profile

This Building Block contains the provenance description of a cool spot analysis workflow developed as part of the [VelocityAdapt](https://velocityadapt.de/) project and profiled within the [Open Science Persitent Demonstrator 2026](https://www.ogc.org/de/initiatives/open-science-persistent-demonstrator-2026/) initiative.

The provenance representation follows [W3C PROV](https://www.w3.org/TR/prov-overview/), to be more specific its JSON schema as defined in the [Provenance Chain](https://ogcincubator.github.io/bblock-prov-schema/bblock/ogc.ogc-utils.prov) Building Block.

### Conformance to the Workflow Provenance Graph profile

This block profiles the [Workflow Provenance Graph](bblock://ogc.osc.prov-profiles.workflow-graph),
so every activity must be a [Registered Processing Step](bblock://ogc.osc.prov-profiles.processing-step):
its `activityType` must give a process type, from a governed register, more specific than `prov:Activity`, and it must have an output.
Each node gives its PROV class in `provType` (`Entity`, `Activity`, `Agent`), and `entityType`,
`activityType` and `agentType` carry only the specific types. Steps not yet mapped to a registered
process type use local CURIEs derived from their names (`ex:defineInputs`, `ex:geocodeCity`,
`ex:acquireData`, `ex:exportOutputs`); the schema accepts these, but mapping them to registered
process types is still to be done.

The workflow run, its plan and its runner are typed with the generic workflow classes of the
[activity type register profile](https://w3id.org/ogc/rim/activity-type/): `ex:workflowRun` is an
`acttype:WorkflowRun`, `ex:coolSpotsScript` an `acttype:WorkflowPlan` and `ex:gisPipelineEngine` an
`acttype:WorkflowRunner`.

The workflow run reports its own inputs and output by reference only: it uses the inputs of
each step that no other step generated, and generates the output of the last step (`ex:finalOutputPackage`, whose members are the exported files).
The example conforms; the SHACL shapes warn only that `ex:act1_defineInputs`, which creates the
process inputs from parameters, uses no entity.
