## Processing activity provenance

Profile of `ogc.ogc-utils.prov-activity`. Requires `activityType`, `name`, `startedAtTime`, `endedAtTime`, `used`, `generated` and `wasAssociatedWith`.

Optional `processType` links the activity to a registered process type (`dcterms:type`).

Inline inputs need `generatedAtTime` or `dcterms:hasVersion`; inline software agents need `dcterms:hasVersion`.
