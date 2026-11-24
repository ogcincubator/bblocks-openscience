# Registered Processing Step

PROV-O is deliberately general: any valid PROV document is a valid description
of a processing step, which makes validation weak and cross-platform
comparison hard. This profile narrows a `prov:Activity` to one processing step
that is **typed by a registered process type**.

## Binding the process type

`provType` identifies the PROV class (`Activity`). `activityType` (which maps
to `@type` / `rdf:type`) then carries only the specific type: the process type
the step is an instance of. Both use the
[IRI or CURIE](bblock://ogc.ogc-utils.iri-or-curie) building block.

```json
"provType": "Activity",
"activityType": "https://register.ospd.dev.kurrawong.ai/catalogs/reg:top/collections/reg:52north/items/demo:GA016"
```

Data that does not set `provType` can still identify the step by including
`prov:Activity` in `activityType`, but it must also give a more specific type.

The step is then an instance of the governed concept, with no new property.
OGC API - Processes Part 5 (draft 26-038) does not link a process to a
registered process type; this profile makes that link required. It is where
the OSPD 2026 profile-plus-register pattern closes: the profile gives the
structure, the register gives the controlled term.

JSON Schema checks that `activityType` gives a type more specific than
`prov:Activity`, as an IRI or CURIE. Whether that type is a member of the
register is for SHACL with a closure of the register, or for the register
itself, to check.

## Inputs and outputs

Inputs and outputs may be stated from either side of the relation, so the
JSON schema does not require `used` or `generated`. The SHACL shapes check:

- **output** (violation): `prov:generated`, or some entity `prov:wasGeneratedBy` the step;
- **input** (warning): `prov:used`, or `prov:qualifiedUsage` / `prov:entity`.

The role an input plays is expressed with `qualifiedUsage` and `hadRole`.

## Specialisations

- [Workflow Provenance Graph](bblock://ogc.osc.prov-profiles.workflow-graph): a whole workflow run
  whose activities are all registered processing steps.
- Platform-specific profiles add stricter rules, e.g.
  [Geospatial Processing Step Provenance](bblock://ogc.osc.prov-profiles.aganitha-ndvi).

Labels are optional on the step itself: an activity records one run. The
process type is a reusable description and is labelled in its register.
