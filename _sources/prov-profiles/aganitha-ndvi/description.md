# Geospatial Processing Step Provenance

This building block profiles the
[Registered Processing Step](bblock://ogc.osc.prov-profiles.processing-step)
for one geospatial processing step.

PROV-O is deliberately general. Any valid PROV document is a valid description
of a processing step, which makes validation weak and cross-platform comparison
hard.

OGC API - Processes Part 5 (draft 26-038) narrows this for job provenance: a
job entity, a process entity, an activity joining them, and input/output
artifacts carrying roles. This profile follows that shape.

Part 5 does not define any link from a process to a registered process type.
The base profile makes that link required: `provType` is `Activity`, and
`activityType` gives the registered process type. On top of that, this profile adds:

- `used` and `generated` on the activity, as non-empty arrays of entity references;
- a `hadRole` on every `qualifiedUsage`, naming the input slot of the process type;
- step parameters, when given, in a single `parameters` object keyed by the process type's parameter terms.

Under development as part of OSPD 2026, deliverable D104 (Aganitha Space
Technologies, Workflow Profiler).
