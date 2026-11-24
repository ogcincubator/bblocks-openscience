# Review Task: Consolidated Workflow Provenance

The provenance building blocks contributed to this register now build on shared PROV profiles.
The design is described in [CONSOLIDATED-DESIGN.md](CONSOLIDATED-DESIGN.md).

**What we ask of each contributor**

1. Review your block(s) as described below. Confirm they still represent your provenance
   correctly, or say what is wrong.
2. Answer the questions addressed to you.
3. Ideally, update the code that generates your provenance to emit these patterns directly.

Please reply on the pull request, or open an issue that references this file.

**Patterns common to everyone**

- `provType` gives the PROV class (`Entity`, `Activity`, `Agent`). `entityType`, `activityType`
  and `agentType` hold only the specific types, as IRIs or CURIEs.
- Every activity has an `activityType` more specific than `prov:Activity`, ideally a registered
  process type IRI (we will be publishing the register of supplied descriptions and updating examples to point to these in the next step).
- A whole workflow execution is an `acttype:WorkflowRun`, its reusable description an
  `acttype:WorkflowPlan`, and the engine running it an `acttype:WorkflowRunner`.
- A run lists, by ID only, the inputs that no step generated (`used`) and the last step's output
  (`generated`).
- Labels are optional on activities and entities. Plans and agents should have one (a warning
  only). `dcterms:title` and `skos:prefLabel` are turned into `rdfs:label` during uplift.
- **Deduplication**: a block's schema and context hold only what it adds. PROV structure, the
  type properties, PROV terms and common prefixes are inherited from the PROV building blocks
  and the shared profiles. Examples carry no inline `@context`.

---

## (52°North): `prov-examples/52n-provenance/cool-spots`, `vegetation-productivity`

**Your blocks now**

| Aspect | Design | Rationale |
|---|---|---|
| Profile | `isProfileOf` workflow-graph; the schema is a single `$ref` to it | Step and graph rules are shared with the other contributors |
| Context | only `ex` and `schema` (plus `openeo` and `spdx` in vegetation-productivity) | `prov`, `rdfs`, `xsd`, `dcterms` are inherited; `geojson` and `stac` were unused |
| Typing | `provType` plus specific `entityType` / `activityType` / `agentType`; one type is a plain string | Common convention |
| cool-spots process types | register IRIs for steps 3–7; interim local types `ex:defineInputs`, `ex:geocodeCity`, `ex:acquireData`, `ex:exportOutputs` for steps 1, 2a, 2 and 8 | Every step needs a specific process type |
| Workflow classes | cool-spots: `ex:workflowRun` is an `acttype:WorkflowRun`, `ex:coolSpotsScript` an `acttype:WorkflowPlan`, `ex:gisPipelineEngine` an `acttype:WorkflowRunner`. vegetation-productivity: `ex:bap_process_graph` is an `acttype:WorkflowPlan`, `ex:openeo_backend` an `acttype:WorkflowRunner` | Shared classes for runs, plans and runners |
| Run inputs and output | the cool-spots run `used` `ex:nominatimApi` and `ex:overpassApi`, and `generated` `ex:finalOutputPackage` | A run reports the inputs no step generated and the last step's output, by ID |
| Labels | `rdfs:label` and `dcterms:title` both accepted | `dcterms:title` becomes `rdfs:label` during uplift |
| References | related nodes are referenced by plain IRI or CURIE strings (`"wasGeneratedBy": "ex:act1_defineInputs"`), not `{"id": …}` objects | The PROV schemas accept a reference string or a full node with `provType`; an object holding only `id` is neither |
| Uplift | `semantic-uplift.yaml` inherits workflow-graph's type and label rules (`inheritedPostSteps`) | Uplift rules are not applied to dependent blocks unless they opt in |

**Questions**

- Should the interim `ex:` process types be mapped to GeoACS items, or proposed as new register
  items? This covers the 4 cool-spots step types, and `ex:PostProcessing`, `ex:CogConversion` and
  `ex:StacMetadataCreation` in vegetation-productivity.
- Is `ex:finalOutputPackage` alone the right run output, or should its nine member files be listed
  too?
- `ex:act1_defineInputs` uses no entity, so SHACL gives a warning. Should the parameters it reads
  be modelled as an input entity?
- vegetation-productivity has no run-level activity. Do you want to add one?

**Code updates suggested**: emit `provType` with specific `*Type` values; type the run, plan
and engine with the `acttype:` classes; emit run-level `used` and `generated` by ID; drop the
prefixes that are now inherited; emit references as IRI or CURIE strings, not `{"id": …}` objects.

---

## (HARTIS): `prov-profiles/hartis-provenance/cvi-workflow`

**Your block now**

| Aspect | Design | Rationale |
|---|---|---|
| Profile | `isProfileOf` workflow-graph (bundle form) | Shares the step rules with the other contributors |
| Schema | each node references `prov-entity`, `prov-activity` or `processing-step`. HARTIS adds only the bundle's required parts (`workflowDefinition`, `plans` with `processType`, `runtime` with `activities`, `entities`) and, on each step, `plan`, `used` and `generated` | `id`, `provType`, the type properties and their enums are inherited |
| Context | `ospd` and `hartis` prefixes; `processType` → `dct:type`; `workflowDefinition` → `hartis:workflowDefinition`; `plan` → `hartis:plan`; `activities` → `dct:hasPart`; `plans`, `runtime`, `entities` → `@included` | Only HARTIS terms; PROV terms, `label` and `dct` are inherited. `@included` makes the nested nodes part of the graph (261 triples) |
| Example | no inline `@context` | The block context applies |
| Typing | `provType` plus `entityType` / `activityType`; step process types in `activityType` | Common convention |
| Workflow classes | the workflow definition is an `acttype:WorkflowPlan`; `runtime` an `acttype:WorkflowRun` | Shared classes; this gives `runtime` its required type |
| Run inputs and output | `runtime` `used` the 7 external inputs and `generated` `transects-with-cvi-equal`, by ID | A run reports its external inputs and final output |
| Uplift | `semantic-uplift.yaml` inherits workflow-graph's type and label rules (`inheritedPostSteps`) | Uplift rules are not applied to dependent blocks unless they opt in |

**Questions**

- `hartis:workflowDefinition` and `hartis:plan` are new predicates in your namespace. Keep them,
  or use PROV (`prov:qualifiedAssociation` / `prov:hadPlan`)?
- Which predicates should be used for `status`, `notes`, `path`, `format`, `source`,
  `sourceWorkflow`, `executionImage` and `sourceCode`? They are not mapped to RDF yet.
  Suggestions: `dct:format`, `dct:source`.
- The step process types are `https://example.org/ospd/process-types/...`. We aim to have descriptions for these registered. 
- The container agent `hartis:cvi-workflow/container/cvi-workflow-latest` is referenced but not
  described. Should it be described as an `acttype:WorkflowRunner`?

**Code updates suggested**: omit the inline `@context`; emit `provType` with `entityType` or
`activityType`; type the runtime and the workflow definition with the `acttype:` classes; emit
run-level `used` and `generated` by ID.

---

## (Aganitha): `prov-profiles/aganitha-drought`

**Your block now**

| Aspect | Design | Rationale |
|---|---|---|
| Profile | `isProfileOf` processing-step (identifier `ogc.osc.prov-profiles.aganitha-drought`) | The generic step rules are shared with the other contributors |
| Schema | `$ref` to processing-step, plus `used` / `generated` as required non-empty arrays of IDs, `qualifiedUsage` with `entity` and `hadRole`, and `parameters` | `id`, `label`, timestamps, `wasAssociatedWith` and the type binding are inherited |
| Context | none of its own | `label` comes from processing-step, and the PROV terms and `@type` binding from the PROV context |
| Typing | `provType: "Activity"` with `activityType` (the process type IRI) | Common convention |
| Examples | 10 files under `examples/` (nine steps plus a whole-run record), referenced from `examples.yaml` | Easier to maintain and reuse |

**Questions**

- Does anything external reference this block by an earlier identifier?
- `parameters` is not mapped in the context. Do you prefer coarse process types with parameters,
  or parameterised subtypes?
- Block name: renamed from `aganitha-ndvi` to `aganitha-drought` (resolved).

**Code updates suggested**: emit `provType` with `activityType` for each step.

---

## (Telespazio / EarthCODE): `ogc.esa.earthcode.*` in [bblocks-esa-earthcode](https://github.com/ogcincubator/bblocks-esa-earthcode)

**Your blocks now**

| Aspect | Design | Rationale |
|---|---|---|
| Schemas | PROV parts reference `prov-entity` (products, workflows) and `prov-activity` (experiments), applied when `provType` is given | PROV structure is inherited; no dependency on the deprecated wf4ever blocks |
| SHACL | `experiments/shapes.shacl` checks wf4ever traces (ProcessRun described by a Process and part of a WorkflowRun; outputs linked to a ProcessRun) | Keeps existing wf4ever traces consistent |
| Context | `acttype` in experiments and workflows; `wfprov`, `wfdesc`, `wf4ever` where the examples use them | These blocks don't build on workflow-graph, so they need `acttype` themselves; wf4ever terms in existing data still expand to IRIs |
| experiments | the run has `provType: "Activity"` and `activityType: ["wfprov:WorkflowRun", "acttype:WorkflowRun"]`; the engine has `provType: "Agent"` and `agentType: ["wfprov:WorkfowEngine", "prov:SoftwareAgent", "acttype:WorkflowRunner"]` | Common convention; shared run and runner classes |
| products | `provType: "Entity"`, `entityType: ["wfprov:Artifact", "wf4ever:Dataset"]` | Common convention |
| workflows | `provType: "Entity"`, `entityType: ["prov:Plan", "wfdesc:Workflow", "acttype:WorkflowPlan"]`; the nested catalog output has `entityType: "prov:Collection"` | Common convention; shared plan class |
| Product tests | CF extension v1.0.0: `bands` with `cf:standard_name` | Matches the current CF schema |

**Note: wf4ever (deprecated).** OSPD 2025 identified the wf4ever vocabularies (`wfprov`, `wfdesc`, `wf4ever`) as a useful level of abstraction for workflow provenance, between generic PROV and platform-specific records. wf4ever is no longer maintained, so it is deprecated here: these building blocks no longer depend on the wf4ever building blocks, and the focus has moved to the simpler task of defining activity types in a governed register (the activity-type register), which are used to type PROV activities. wf4ever terms already used in the examples are kept, with their prefixes declared, but are not required.

**Questions and possible fixes**

- `wfprov:WorkfowEngine` looks like a typo for `wfprov:WorkflowEngine`. Fix it?
- The engine node uses `prov:label`, which is not a PROV term. Change it to `rdfs:label` or
  `name`?
- The full blocks could not be validated locally, because their imported GeoDCAT schemas did not
  resolve. Please check the build report for these blocks.
- The water-bodies run has no step activities. Should its steps be described, so it can be
  compared with the other platforms?

**Code updates suggested**: emit `provType` with specific `*Type` values; type the run, plan
and engine with the `acttype:` classes.

---

## (RSS-Hydro): `rss-hydro/processing-activity`, `ontology/activities`, `workflow/model-of-models`

**Your blocks now**

| Aspect | Design | Rationale |
|---|---|---|
| Typing | every node has `provType` (`Activity`, `Entity` or `Agent`) | Required by the PROV building blocks |
| Process types | `activityType` values are CURIEs with the `pt:` prefix (`pt:ZonalStatistics`, `pt:WeightedScoringAndClassification`, `pt:ScoringAndProgressTracking`); the schema also accepts the full IRIs | The PROV context maps `activityType` as an IRI (`"@type": "@id"`), so a bare term such as `ZonalStatistics` is read as a relative IRI and never expands |
| Context | `ontology/activities` declares `mom`, `dcterms` and the `pt` prefix | One prefix instead of a term per process type |
| SHACL | `model-of-models/rules.shacl` selects activities and hazard scores by their `prov:type` value | `activityType` / `entityType` map to `prov:type`, not `rdf:type`, so `sh:targetClass` / `sh:class` would never match |

**Questions**

- This brings back the `pt:` prefix that was replaced by full IRIs in an earlier commit, now as
  CURIEs in the data rather than as context terms. Is that acceptable?
- Should the process types move from the placeholder `https://example.org/ospd/process-types/`
  namespace to the activity-type register once it is live?

**Code updates suggested**: emit `provType` on every node; emit process types as `pt:` CURIEs
(or full IRIs).

---

## Register maintainers (OGC)

- Confirm the `acttype:WorkflowPlan`, `acttype:WorkflowRun` and `acttype:WorkflowRunner` classes
  in `activity-type-register/_sources/activity-types/ontology.ttl`, and publish the namespace.
- Plan the register-membership validator for process types.
