# Geospatial Processing Step Provenance

This building block profiles `ogc-utils.prov` down to a single unit: one
geospatial processing step.

PROV-O is deliberately general. Any valid PROV document is a valid description
of a processing step, which makes validation weak and cross-platform comparison
hard.

OGC API - Processes Part 5 (draft 26-038) narrows this for job provenance: a
job entity, a process entity, an activity joining them, and input/output
artifacts carrying roles. This profile follows that shape.

Part 5 does not define any link from a process to a registered process type.
This profile makes that link required, via the processType property. It is the
point at which the OSPD 2026 profile-plus-register pattern closes: the profile
gives the structure, the register gives the controlled term.

Under development as part of OSPD 2026, deliverable D104 (Aganitha Space
Technologies, Workflow Profiler).
