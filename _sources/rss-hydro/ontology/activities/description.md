## MoM workflow activity types

Process types used by the MoM flood workflow (subclasses of `Geoprocessing`, itself a `prov:Activity`), defined by the OSPD activity types register (`https://w3id.org/ogc/ospd/activity-type/`, prefix `pt`; until 26 Nov 2026 a placeholder namespace), plus the entity type, properties, workflow run type (`https://w3id.org/ogc/ospd/activity-type/workflow`) and alert levels (`mom:AlertLevels`) the MoM profile uses.

| `activityType` (CURIE) | Register term (`processType`) | Generic operation |
|---|---|---|
| `pt:ZonalStatistics` | `https://w3id.org/ogc/ospd/activity-type/ZonalStatistics` | zonal statistics |
| `pt:WeightedScoringAndClassification` | `https://w3id.org/ogc/ospd/activity-type/WeightedScoringAndClassification` | index composition and classification |
| `pt:ScoringAndProgressTracking` | `https://w3id.org/ogc/ospd/activity-type/ScoringAndProgressTracking` | multi-source scoring and progress tracking |

The schema checks that a record of one of these types states the matching `processType` and is a valid processing activity (`ogc.osc.rss-hydro.processing-activity`).
