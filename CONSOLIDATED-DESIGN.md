# Consolidated Workflow Provenance Design

This note describes the consolidated design for workflow and processing-step provenance in this
register, and how each contributed building block now fits it. Per-contributor review actions
are in [REVIEW-TASK.md](REVIEW-TASK.md).

Status: proposed, for contributor review. Validation results are from a full local
`bblocks-postprocess` build of this register (all 25 tests pass).

---

## 1. Goals

- Make provenance from different platforms (52°North, HARTIS, Aganitha, EarthCODE) **comparable
  step by step**, by typing each processing step with a process type from a governed register.
- Keep **shared requirements in shared profiles**, so each contributor's block holds only its own
  requirements.
- **Reuse** the PROV building blocks (`ogc.ogc-utils.prov`, `prov-entity`, `prov-activity`,
  `prov-agent`) and the IRI-or-CURIE building block for structure, typing and JSON-LD mappings.
- Check structure with JSON Schema, and graph-level rules with SHACL on the uplifted RDF.

## 2. Block structure

```
_sources/
  prov-profiles/                     shared profiles and contributor profiles
    processing-step/                 Registered Processing Step   (profile of prov-activity)
    workflow-graph/                  Workflow Provenance Graph    (profile of prov)
    aganitha-ndvi/                   Aganitha drought pipeline    (profile of processing-step)
    hartis-provenance/cvi-workflow/  HARTIS CVI workflow          (profile of workflow-graph)
  prov-examples/                     contributed examples built on the profiles
    52n-provenance/cool-spots/                 (profile of workflow-graph)
    52n-provenance/vegetation-productivity/    (profile of workflow-graph)
```

The EarthCODE blocks are in a separate register,
[bblocks-esa-earthcode](https://github.com/ogcincubator/bblocks-esa-earthcode)
(`ogc.esa.earthcode.{common,experiments,products,workflows}`), which imports this one.

Identifiers follow the paths with the prefix `ogc.osc.`, e.g.
`ogc.osc.prov-profiles.processing-step`.

## 3. Layered profiles

| Layer | Block | Provides |
|---|---|---|
| PROV | `ogc.ogc-utils.prov`, `prov-entity`, `prov-activity`, `prov-agent` | PROV structure; `provType` / `entityType` / `activityType` / `agentType` mapped to `@type`; all PROV terms; prefixes `prov`, `rdfs`, `dct`, `xsd`, `rdf` |
| Step | `prov-profiles.processing-step` | every step has an `id` and an `activityType` naming a specific (registered) process type; `label` → `rdfs:label`; SHACL: a step must have an output, should have an input |
| Workflow | `prov-profiles.workflow-graph` | a run as a graph (array) or a `prov:Bundle`; every activity, at any depth, is a processing step; labels on plans and agents (SHACL warning); label-generation uplift rule; prefixes `dcterms`, `skos`, `acttype` |
| Contributor | `aganitha-ndvi`, `hartis-provenance/cvi-workflow`, `52n-provenance/*`, EarthCODE (`ogc.esa.earthcode.*`) | only contributor-specific properties, constraints and prefixes |

## 4. Systematic deduplication

Every block declares only what it adds. Anything a block inherits from a building block it
references (by `$ref` in its schema, or as the block it profiles) is not repeated.

**Schemas**

- A profile references its base block (`$ref`) and adds constraints only; it does not redefine
  inherited properties (`id`, `provType`, the `*Type` properties, timestamps, PROV relations).
- Each nested node references the PROV building block for its kind (`prov-entity`,
  `prov-activity`, `processing-step`), instead of restating PROV structure.
- Types use the IRI-or-CURIE building block (`#/$defs/Single`, `#/$defs/Multiple`), not local
  patterns or enums.
- Generic requirements are stated once, in the layer that owns them: "a step has a specific
  process type" in processing-step, "every activity is a step" in workflow-graph, labels in the
  workflow-graph SHACL shapes.

**JSON-LD contexts**

- Contexts compose: a block's assembled context includes the contexts of the blocks it
  references, so `context.jsonld` holds only new terms and prefixes.
- PROV terms and the `prov`, `rdfs`, `dct`, `xsd` and `rdf` prefixes come from the PROV
  context; `label` from processing-step; `dcterms`, `skos` and `acttype` from workflow-graph.
- Inherited prefixes are used in mappings (e.g. `dct:type`) instead of repeating full IRIs, and
  unused prefixes are not declared.
- Examples carry no inline `@context`; the block context applies.

**Examples**

- Example code lives in files (`examples/*.json` or `example.json`) referenced from
  `examples.yaml`.
- A workflow run references its inputs and output by ID; entity details appear once, on the
  entity node.

What each block now declares is listed in §10.

## 5. Typing conventions

- **`provType`** gives the PROV class: `Entity`, `Activity` or `Agent`.
- **`entityType` / `activityType` / `agentType`** give only the specific types, as IRIs or CURIEs
  (a single value or an array). They do not repeat `prov:Entity`, `prov:Activity` or `prov:Agent`.
  Values are full IRIs or CURIEs (`prov:Person`, `pt:ZonalStatistics`), not bare terms: the PROV
  context maps these properties with `"@type": "@id"`, so a bare term such as `ZonalStatistics`
  would be read as a relative IRI rather than looked up in the context. (A profile could switch to
  `"@type": "@vocab"`, but CURIEs keep the meaning visible in the data.)
- **Process types**: a step's `activityType` includes a type more specific than `prov:Activity`,
  normally a register item IRI (e.g. an OSPD GeoACS item). Local CURIEs (`ex:...`) are accepted as
  an interim measure; register membership will be checked by a separate validator once the
  activity-type register is live.
- **RDF mapping**: `provType` maps to `rdf:type`; `entityType`, `activityType` and `agentType` map to
  `prov:type` (as in the PROV building blocks). The workflow-graph uplift rule
  (`uplift/types.shacl`) also asserts `rdf:type` for an allow-list of classes: the PROV subclasses
  (`prov:Plan`, `prov:Bundle`, `prov:Collection`, `prov:EmptyCollection`, `prov:Person`,
  `prov:Organization`, `prov:SoftwareAgent`) and `acttype:WorkflowPlan` / `WorkflowRun` /
  `WorkflowRunner`, so shapes can use `sh:targetClass` for them.
- **Process types stay `prov:type` values.** Registered activity types are subclasses of
  `acttype:ActivityType`, itself a `rim:RegisterItem`; asserting them as `rdf:type` would make every
  run a register item. Shapes about process types select nodes by `prov:type` value (as in the
  RSS-Hydro rules).

```json
{
  "id": "ex:act3_reproject",
  "provType": "Activity",
  "activityType": "https://register.ospd.dev.kurrawong.ai/catalogs/reg:top/collections/reg:52north/items/demo:GA018",
  "used": "ex:rawOsmData"
}
```

Register item IRIs in the examples use the demonstration register
(`https://register.ospd.dev.kurrawong.ai/catalogs/reg:top/collections/<register>/items/<item>`), for
example `reg:52north` for GA016–GA020 and `reg:ogcactivites` for GA001. They will be replaced if the
register is deployed to its final location.

## 6. Workflow plans, runs and runners

The activity-type register profile (`activity-type-register/_sources/activity-types/ontology.ttl`,
namespace `acttype: <https://w3id.org/ogc/rim/activity-type/>`) defines three generic classes:

| Class | Subclass of | Meaning |
|---|---|---|
| `acttype:WorkflowPlan` | `prov:Plan` (so `prov:Entity`) | the reusable description of a workflow |
| `acttype:WorkflowRun` | `prov:Activity` | one execution of a workflow, as a whole |
| `acttype:WorkflowRunner` | `prov:Agent` | the engine or platform that executes runs |

A workflow run reports its own inputs and output by ID only. `used` lists the inputs of each step
that no other step generated, and `generated` lists the output of the last step.

### wf4ever (deprecated)

OSPD 2025 identified the wf4ever vocabularies (`wfprov`, `wfdesc`, `wf4ever`) as a useful level of abstraction for workflow provenance, between generic PROV and platform-specific records. wf4ever is no longer maintained, so it is deprecated here: these building blocks no longer depend on the wf4ever building blocks, and the focus has moved to the simpler task of defining activity types in a governed register (the activity-type register), which are used to type PROV activities. wf4ever terms already used in the examples are kept, with their prefixes declared, but are not required.

## 7. Labels

- Labels are optional on activities and on the bundle that holds a run: these record one run.
- Labels are not required on entities in general: an entity may be a temporary artefact passed
  between activities.
- Plans (including workflow definitions) and agents are reusable descriptions and should have an
  `rdfs:label`. A missing label is a SHACL warning, checked after uplift.
- A label may be given as `label`, `rdfs:label` or `name`. It may also be generated during uplift:
  the workflow-graph rule (`uplift/labels.shacl`) derives `rdfs:label` from `dcterms:title` or
  `skos:prefLabel` when no label is given. Profiles may add their own label-generation rules.

## 8. Validation

| Check | Where |
|---|---|
| Structure, required properties, a specific process type on every activity | JSON Schema |
| A step has an output (violation) and an input (warning) | SHACL, processing-step |
| Plans and agents are labelled (warning) | SHACL, workflow-graph, after the type and label uplift rules (inherited by its profiles) |
| The process type is a member of the register | future validator, against the activity-type register |

## 9. Validation status (local postprocessor build)

| Block | Result | Notes |
|---|---|---|
| processing-step | pass (4/4) | |
| workflow-graph | pass (8/8) | the unlabelled-plan and unlabelled-agent tests give the intended warnings |
| aganitha-ndvi | pass (9/9) | |
| HARTIS cvi-workflow | pass (3/3) | inherited type and label rules applied |
| 52n cool-spots | pass (1/1) | 1 warning: `ex:act1_defineInputs` uses no entity; inherited rules applied |
| 52n vegetation-productivity | pass (1/1) | agent labels generated from `dcterms:title` by the inherited label rule |
| rss-hydro processing-activity, ontology/activities, model-of-models | pass (3/3, 2/2, 6/6) | negative tests fail for their intended reasons |
| EarthCODE (separate register) | not built yet | PROV parts pass the PROV schemas locally |

## 10. What each block declares

### processing-step

- **Schema**: `$ref` to `prov-activity`; requires `id` and `activityType`; requires the activity
  to be identified as a PROV Activity (by `provType`, or `prov:Activity` in `activityType`);
  `activityType` is IRI-or-CURIE `Multiple` and must include a specific type.
- **Context**: `label` → `rdfs:label`.
- **SHACL**: output required (violation); input expected (warning).

### workflow-graph

- **Schema**: `$ref` to `prov`; graph form (an array containing an activity) or bundle form (an
  entity typed `prov:Bundle`); a recursive walk applying processing-step to every activity.
- **Context**: prefixes `dcterms`, `skos`, `acttype`.
- **SHACL**: `rdfs:label` on plans and agents (warning).
- **Uplift**: `semantic-uplift.yaml` → `uplift/types.shacl` (`rdf:type` for allow-listed
  `prov:type` classes), then `uplift/labels.shacl` (label generation). Both are `inheritable`;
  profiles opt in with `inheritedPostSteps: [ogc.osc.prov-profiles.workflow-graph]`.

### aganitha-ndvi

- **Schema**: `$ref` to processing-step, plus `used` / `generated` as required non-empty arrays of
  IDs, `qualifiedUsage` with `entity` and `hadRole`, and `parameters`.
- **Context**: none of its own.
- **Examples**: 9 files under `examples/`; steps use `provType: "Activity"` and `activityType`.

### HARTIS cvi-workflow

- **Schema**: `$ref` to workflow-graph and `prov-entity`. It adds the bundle's required parts:
  `workflowDefinition`, `plans` (each with a `processType`), `runtime` (with `workflowDefinition`
  and `activities`), and `entities`. Each step requires `plan`, `used` and `generated`.
- **Context**: prefixes `ospd`, `hartis`; `processType` → `dct:type`; `workflowDefinition` →
  `hartis:workflowDefinition`; `plan` → `hartis:plan`; `activities` → `dct:hasPart`; `plans`,
  `runtime`, `entities` → `@included`.
- **Example**: the workflow definition is an `acttype:WorkflowPlan`; `runtime` is an
  `acttype:WorkflowRun` with its external inputs and final output. It uplifts to 261 triples.

### 52°North cool-spots and vegetation-productivity

- **Schema**: `$ref` to workflow-graph only.
- **Context**: prefixes not otherwise inherited: `ex` and `schema`, plus `openeo` and `spdx` for
  vegetation-productivity.
- **Examples**: `provType` plus specific types; the run, the plan and the runner are typed with
  `acttype:` classes; the cool-spots run reports its external inputs and final output.

### EarthCODE GeoDCAT/STAC (`bblocks-esa-earthcode`)

- **Schemas**: they reference `prov-entity` (products, workflows) and `prov-activity` (experiments) for
  their PROV parts, applied only when `provType` is given.
- **Context**: `acttype` prefix in experiments and workflows. These blocks do not build on
  workflow-graph, so they don't inherit it from there.
- **Examples**: `provType` plus specific types; the run, the workflow plan and the engine are
  typed with `acttype:` classes. The product tests use the CF extension v1.0.0 (`bands` with
  `cf:standard_name`).

### Activity-type register

- **Ontology**: `acttype:WorkflowPlan`, `acttype:WorkflowRun` and `acttype:WorkflowRunner`.

## 11. Open questions

1. Should HARTIS's own predicates (`hartis:workflowDefinition`, `hartis:plan`) be replaced by
   standard ones, e.g. `prov:hadPlan` via a qualified association?
2. Which predicates should HARTIS use for the literals currently not mapped to RDF: `status`, `notes`,
   `path`, `format`, `source`, `sourceWorkflow`, `executionImage`, `sourceCode`?
3. How should the interim `ex:` process types be mapped to registered types?
4. How should step parameters (Aganitha `parameters`) be typed?
5. Who publishes the `acttype:` namespace, so that the workflow classes resolve?

### Settled by a full build

- **Uplift steps are not applied to dependent blocks by default.** A block's uplift steps run for its
  own examples only. workflow-graph therefore marks its type and label rules `inheritable: true`, and
  each block that profiles it opts in with `inheritedPostSteps` in its own `semantic-uplift.yaml`.
  The inherited steps run before the block's own steps and before SHACL validation.
- **Contexts are inherited through nested schema references**, including references inside `$defs`
  (e.g. `label` from processing-step reaches workflow-graph; the rss-hydro `pt` prefix reaches
  model-of-models).
- **SHACL warnings do not fail validation**: blocks with only warnings pass.
