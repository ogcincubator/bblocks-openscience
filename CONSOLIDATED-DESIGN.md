# Consolidated Workflow Provenance Design

This note describes the consolidated design for workflow and processing-step provenance in this
register, and how each contributed building block now fits it. Per-contributor review actions
are in [REVIEW-TASK.md](REVIEW-TASK.md).

Status: proposed, for contributor review. Validation results are from local JSON Schema and SHACL
checks; a full `bblocks-postprocess` build has not yet been run.

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
    geodcat-stac-earthcode/{common,experiments,products,workflows}/
```

Identifiers follow the paths with the prefix `ogc.osc.`, e.g.
`ogc.osc.prov-profiles.processing-step`.

## 3. Layered profiles

| Layer | Block | Provides |
|---|---|---|
| PROV | `ogc.ogc-utils.prov`, `prov-entity`, `prov-activity`, `prov-agent` | PROV structure; `provType` / `entityType` / `activityType` / `agentType` mapped to `@type`; all PROV terms; prefixes `prov`, `rdfs`, `dct`, `xsd`, `rdf` |
| Step | `prov-profiles.processing-step` | every step has an `id` and an `activityType` naming a specific (registered) process type; `label` → `rdfs:label`; SHACL: a step must have an output, should have an input |
| Workflow | `prov-profiles.workflow-graph` | a run as a graph (array) or a `prov:Bundle`; every activity, at any depth, is a processing step; labels on plans and agents (SHACL warning); label-generation uplift rule; prefixes `dcterms`, `skos`, `acttype` |
| Contributor | `aganitha-ndvi`, `hartis-provenance/cvi-workflow`, `52n-provenance/*`, `geodcat-stac-earthcode/*` | only contributor-specific properties, constraints and prefixes |

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
- **Process types**: a step's `activityType` includes a type more specific than `prov:Activity`,
  normally a register item IRI (e.g. an OSPD GeoACS item). Local CURIEs (`ex:...`) are accepted as
  an interim measure; register membership will be checked by a separate validator once the
  activity-type register is live.

```json
{
  "id": "ex:act3_reproject",
  "provType": "Activity",
  "activityType": "https://catalog.ospd.dev.kurrawong.ai/catalogs/demo:geoacs/collections/demo:ospd-geoacs/items/demo:GA018",
  "used": "ex:rawOsmData"
}
```

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
| Plans and agents are labelled (warning) | SHACL, workflow-graph, after the label uplift rule |
| The process type is a member of the register | future validator, against the activity-type register |

## 9. Validation status (local checks)

| Block | JSON Schema | SHACL |
|---|---|---|
| processing-step | pass | pass |
| workflow-graph | pass | pass (the unlabelled-plan and unlabelled-agent tests give the intended warnings) |
| aganitha-ndvi | pass | pass |
| HARTIS cvi-workflow | pass | pass |
| 52n cool-spots | pass | pass, 1 warning (`ex:act1_defineInputs` uses no entity) |
| 52n vegetation-productivity | pass | pass, after the label uplift rule |
| GeoDCAT/STAC | PROV parts pass the PROV schemas; full blocks not checked locally | not checked |

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
- **Uplift**: `semantic-uplift.yaml` → `uplift/labels.shacl` (label generation).

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

### EarthCODE GeoDCAT/STAC

- **Schemas**: they reference `prov-entity` and `wfprov.WorkflowRun` for their PROV parts.
- **Context**: `acttype` prefix in experiments and workflows. These blocks do not build on
  workflow-graph, so they don't inherit it from there.
- **Examples**: `provType` plus specific types; the run, the workflow plan and the engine are
  typed with `acttype:` classes. The product tests use the CF extension v1.0.0 (`bands` with
  `cf:standard_name`).

### Activity-type register

- **Ontology**: `acttype:WorkflowPlan`, `acttype:WorkflowRun` and `acttype:WorkflowRunner`.

## 11. Open questions

1. Is a referenced block's `semantic-uplift.yaml` applied to dependent blocks, before SHACL
   validation? If not, each dependent block must list the label rule itself.
2. Is a referenced block's `context.jsonld` included when the reference is only inside `$defs`
   (workflow-graph → processing-step)? If not, `label` must also be mapped in workflow-graph.
3. Does the postprocessor treat SHACL warnings as passing?
4. Should HARTIS's own predicates (`hartis:workflowDefinition`, `hartis:plan`) be replaced by
   standard ones, e.g. `prov:hadPlan` via a qualified association?
5. Which predicates should HARTIS use for the literals currently not mapped to RDF: `status`, `notes`,
   `path`, `format`, `source`, `sourceWorkflow`, `executionImage`, `sourceCode`?
6. How should the interim `ex:` process types be mapped to registered types?
7. How should step parameters (Aganitha `parameters`) be typed?
8. Who publishes the `acttype:` namespace, so that the workflow classes resolve?
