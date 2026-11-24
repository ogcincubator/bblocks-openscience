# Workflow Provenance Graph

Provenance of one workflow run, in either of two forms:

- **Graph form**: a JSON array of PROV entities, activities and agents (the
  pattern used by the 52°North workflow provenance examples).
- **Bundle form**: a single entity whose `entityType` (or `@type`) includes
  `prov:Bundle`, with its nodes nested inside it, at any depth and under any
  property names (the pattern used by the HARTIS CVI workflow).

In both forms, every object that is a PROV Activity (its `provType` or
`@type` includes `Activity`, or it has an `activityType`) must conform to the
[Registered Processing Step](bblock://ogc.osc.prov-profiles.processing-step)
profile, wherever it sits in the document (`@context` is skipped). Each step
in the run is therefore typed by a process type from a governed register,
which is what makes two runs of a workflow, on different platforms,
comparable step by step.

Reusable descriptions should have a human-readable label: plans (including
workflow definitions) and agents. A missing label is reported as a warning. Other entities need not be labelled, as
they may be temporary artefacts passed between activities; nor need the
records of an individual run, the activities and the bundle that holds a
run. The process types that `activityType` points to are labelled in their
register.

The label requirement is checked by SHACL on the uplifted graph
(`rdfs:label`), not by the JSON schema, so a label can be generated during
semantic uplift. This block's uplift rule (`uplift/labels.shacl`) derives
`rdfs:label` from `dcterms:title` or `skos:prefLabel` when no label is given;
profiles can add their own label-generation rules.

`provType` identifies the PROV class of each node (`Entity`, `Activity` or
`Agent`); `entityType`, `activityType` and `agentType` then only carry the
specific types, as IRIs or CURIEs.

Outputs are commonly stated from the entity side (`wasGeneratedBy`); the
processing-step SHACL shapes accept either direction.

### Type uplift

The PROV building blocks map `entityType`, `activityType` and `agentType` to `prov:type`; only
`provType` gives `rdf:type`. Before validation, this block's uplift rule (`uplift/types.shacl`)
also asserts `rdf:type` for an allow-list of classes: the PROV subclasses (`prov:Plan`,
`prov:Bundle`, `prov:Collection`, `prov:EmptyCollection`, `prov:Person`, `prov:Organization`,
`prov:SoftwareAgent`) and the activity-type register's `acttype:WorkflowPlan`,
`acttype:WorkflowRun` and `acttype:WorkflowRunner`. This lets the label shapes target plans and
agents by class.

Process types are not copied: they remain `prov:type` values, so that a run does not become an
instance of a register item class. Shapes about process types should select nodes by their
`prov:type` value.
