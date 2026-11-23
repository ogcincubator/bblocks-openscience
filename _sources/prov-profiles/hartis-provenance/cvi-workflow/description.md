# HARTIS CVI Workflow Provenance

This candidate Building Block describes provenance for the complete HARTIS
Coastal Vulnerability Index workflow. It is deliberately workflow-specific:
the profile connects the workflow definition and planned processing steps to
the runtime activities and their input and output entities.

The candidate covers the following chain:

1. configuration and source data preparation;
2. coastline extraction;
3. transect generation;
4. land-cover, slope, erosion and elevation calculations; and
5. final CVI calculation and GeoJSON result generation.

The profile is developed locally in the HARTIS repository first. It is not an
official OGC Register entry or a mature shared Building Block until reviewed
and accepted through the relevant OGC contribution process.

## Relationship to shared provenance

The candidate is intended to align with the common OGC PROV Building Block and
the shared processing-step profile. Its additional value is the explicit
representation of the complete CVI workflow, including design-time plans,
runtime activities, data entities and the links between them.

### Conformance to the Workflow Provenance Graph profile

This block profiles the [Workflow Provenance Graph](bblock://ogc.osc.prov-profiles.workflow-graph)
in its bundle form, so every activity in the bundle, including `runtime` and each of
`runtime.activities`, must be a
[Registered Processing Step](bblock://ogc.osc.prov-profiles.processing-step).
Every node states its PROV class in `provType` (`Entity` or `Activity`); the specific
types are IRIs or CURIEs in `entityType` (`prov:Bundle`, `prov:Plan`, `ospd:VectorDataset`)
or `activityType`. Each runtime activity carries its process type in `activityType`;
the design-time `plans` keep theirs in `processType` (`dct:type`).
Each node references its PROV building block (the bundle, workflow definition, plans and
entities are PROV entities; `runtime` is a PROV activity; each step is a Registered Processing
Step), so identifiers, `provType`, `entityType`/`activityType` and all PROV relations, together
with their JSON-LD mappings, are inherited. This block's schema and `context.jsonld` hold only
what HARTIS adds:

- the `ospd` and `hartis` prefixes;
- `processType` (`dct:type`) on plans;
- `workflowDefinition` and `plan` (`hartis:workflowDefinition`, `hartis:plan`), linking the
  bundle and run to the workflow plan, and each step to its design-time plan;
- `activities` (`dct:hasPart`), the steps of the run;
- `plans`, `runtime` and `entities` as `@included`, so the nested nodes are part of the graph.

The workflow definition is typed `acttype:WorkflowPlan` and `runtime` is typed `acttype:WorkflowRun`,
from the [activity type register profile](https://w3id.org/ogc/rim/activity-type/).
The workflow run reports its own inputs and output by reference only: it uses the inputs of
each step that no other step generated, and generates the output of the last step.
The example conforms to the JSON schema and the SHACL shapes.
