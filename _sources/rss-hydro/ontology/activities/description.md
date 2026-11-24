## MoM workflow activity types

Process types used by the MoM flood workflow (subclasses of `Geoprocessing`, itself a `prov:Activity`), candidate entries for the OSPD process-type register in a placeholder namespace (`https://example.org/ospd/process-types/`, prefix `pt`), plus the entity type, properties, workflow run type (`mom:WorkflowRun`) and alert levels (`mom:AlertLevels`) the MoM profile uses.

| `activityType` (CURIE) | Register term (`processType`) | Generic operation |
|---|---|---|
| `pt:ZonalStatistics` | `https://example.org/ospd/process-types/zonal-statistics` | zonal statistics |
| `pt:WeightedScoringAndClassification` | `https://example.org/ospd/process-types/weighted-scoring-and-classification` | index composition and classification |
| `pt:ScoringAndProgressTracking` | `https://example.org/ospd/process-types/scoring-and-progress-tracking` | multi-source scoring and progress tracking |

The schema checks that a record of one of these types states the matching `processType` and is a valid processing activity (`ogc.osc.rss-hydro.processing-activity`).
