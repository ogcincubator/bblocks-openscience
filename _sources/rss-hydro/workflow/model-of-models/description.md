## Model of Models workflow

Provenance of three activities of the RSS-Hydro Model of Models (MoM) flood workflow.

| Activity | Activity type | Uses | Generates |
|---|---|---|---|
| Per-watershed aggregation | `pt:ZonalStatistics` | gridded source file, watershed shapefile, parameters | per-watershed aggregates |
| Hazard score accumulation | `pt:WeightedScoringAndClassification` | aggregates, previous summary, extra model inputs (optional), static tables, parameters | summary with duration, hazard score (`Final_Attributes`), `Attributes_Clean` |
| Final alert | `pt:ScoringAndProgressTracking` | hazard score of the accumulation, hazard scores of any other sources, previous final alert (optional), admin table | final alert with status per watershed |

Each activity is `dcterms:isPartOf` one `https://w3id.org/ogc/ospd/activity-type/workflow` activity. In the examples, GFMS is the aggregated source and GloFAS an extra model input.

Each watershed is masked from the raster in every run; nothing is reused between runs except the previous summary and the previous final alert, which point to the earlier run that made them. Parameters and static tables ship with the software version (`dcterms:hasVersion`, `dcterms:isPartOf`).

Source files state `mom:dataType`, `dcterms:format`, `mom:dataTime` (time the values refer to) and `generatedAtTime` (time the file was produced). Each `mom:HazardScore` also states the `mom:dataTime` of its cycle and `wasDerivedFrom` the data it was computed from, so the final alert shows which time of each source it combined. The schema enforces the entries; `rules.shacl` checks the links between activities and that every hazard score derives from dated model data.
