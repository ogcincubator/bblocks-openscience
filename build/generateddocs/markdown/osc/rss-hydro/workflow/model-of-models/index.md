
# Model of Models workflow (Schema)

`ogc.osc.rss-hydro.workflow.model-of-models` *v0.1*

Tested provenance example of a slice of the RSS-Hydro Model of Models flood workflow: per-watershed aggregation of a gridded source, hazard score accumulation with extra model inputs, and the final alert from the hazard scores of all sources. GFMS and GloFAS are example sources.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

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

## Examples

### Run of 2026-03-02 00:00 UTC
Usual run; the final alert compares with the alert of the 2026-03-01 18:00 run. All values are illustrative.
#### json
```json
[
  {
    "id": "run:mom",
    "provType": "Agent",
    "agentType": "prov:SoftwareAgent",
    "name": "MoMProduction",
    "dcterms:hasVersion": "0.0.1-alpha"
  },
  {
    "id": "run:rss-hydro",
    "provType": "Agent",
    "agentType": "prov:Organization",
    "name": "RSS-Hydro"
  },
  {
    "id": "run:server",
    "provType": "Agent",
    "agentType": "prov:Agent",
    "name": "mom-prod-01 (illustrative server)"
  },
  {
    "id": "run:workflow-run",
    "provType": "Activity",
    "activityType": "https://w3id.org/ogc/ospd/activity-type/workflow",
    "name": "MoM workflow run, 2026-03-02 00:00",
    "startedAtTime": "2026-03-02T01:05:33Z",
    "endedAtTime": "2026-03-02T01:12:52Z",
    "wasAssociatedWith": [
      "run:mom",
      "run:rss-hydro",
      "run:server"
    ]
  },
  {
    "id": "run:umd",
    "provType": "Agent",
    "agentType": "prov:Organization",
    "name": "University of Maryland (GFMS)"
  },
  {
    "id": "run:ecmwf",
    "provType": "Agent",
    "agentType": "prov:Organization",
    "name": "ECMWF / CEMS (GloFAS)"
  },
  {
    "id": "run:provider-1",
    "provType": "Agent",
    "agentType": "prov:Organization",
    "name": "Provider of sources 1 and 2"
  },
  {
    "id": "run:noaa",
    "provType": "Agent",
    "agentType": "prov:Organization",
    "name": "NOAA (VIIRS)"
  },
  {
    "id": "run:watersheds",
    "provType": "Entity",
    "entityType": "prov:Entity",
    "name": "Watershed_pfaf_id.shp",
    "dcterms:hasVersion": "0.0.0",
    "dcterms:format": "ESRI Shapefile",
    "mom:watershedFingerprint": "a09161ac707ef1d0355e92e730c8fe31e127149b803321bc988b3232058eea17",
    "generatedAtTime": "2026-01-15T00:00:00Z"
  },
  {
    "id": "run:gfms-bin",
    "provType": "Entity",
    "entityType": "prov:Entity",
    "name": "Flood_byStor_2026030200.bin",
    "dcat:downloadURL": "https://example.org/gfms/Flood_byStor_2026030200.bin",
    "mom:dataType": "GFMS",
    "dcterms:format": "GFMS Flood_byStor binary grid (float32)",
    "mom:gfmsNodataValue": -9999,
    "mom:dataTime": "2026-03-02T00:00:00Z",
    "generatedAtTime": "2026-03-02T01:05:32Z",
    "wasAttributedTo": "run:umd"
  },
  {
    "id": "run:aggregation-parameters",
    "provType": "Entity",
    "entityType": "prov:Entity",
    "name": "GFMS per-watershed aggregation parameters",
    "dcterms:hasVersion": "0.0.1-alpha",
    "dcterms:isPartOf": "run:mom",
    "mom:gfmsDurationAreaThresholdKm2": 50,
    "mom:gfmsMinFileSizeBytes": 1000000
  },
  {
    "id": "run:aggregation",
    "provType": "Activity",
    "activityType": "pt:ZonalStatistics",
    "processType": "https://w3id.org/ogc/ospd/activity-type/ZonalStatistics",
    "name": "GFMS per-watershed aggregation",
    "startedAtTime": "2026-03-02T01:05:33Z",
    "endedAtTime": "2026-03-02T01:05:41Z",
    "used": [
      "run:gfms-bin",
      "run:watersheds",
      "run:aggregation-parameters"
    ],
    "generated": "run:gfms-aggregates",
    "wasAssociatedWith": [
      "run:mom",
      "run:rss-hydro",
      "run:server"
    ],
    "dcterms:isPartOf": "run:workflow-run"
  },
  {
    "id": "run:gfms-aggregates",
    "provType": "Entity",
    "entityType": "prov:Entity",
    "name": "Processing/gfms/Flood_byStor_2026030200.csv (per-watershed aggregates, duration not yet recalculated)",
    "mom:dataType": "GFMS",
    "dcterms:format": "text/csv",
    "mom:dataTime": "2026-03-02T00:00:00Z",
    "generatedAtTime": "2026-03-02T01:05:41Z",
    "wasGeneratedBy": "run:aggregation",
    "wasDerivedFrom": [
      "run:gfms-bin",
      "run:watersheds"
    ]
  },
  {
    "id": "run:gfms-summary-prev",
    "provType": "Entity",
    "entityType": "prov:Entity",
    "name": "GFMS_summary/Flood_byStor_2026030121.csv",
    "mom:dataType": "GFMS",
    "dcterms:format": "text/csv",
    "mom:dataTime": "2026-03-01T21:00:00Z",
    "generatedAtTime": "2026-03-01T01:07:12Z"
  },
  {
    "id": "run:glofas-txt",
    "provType": "Entity",
    "entityType": "prov:Entity",
    "name": "threspoints_2026030200.txt",
    "dcat:downloadURL": "https://example.org/glofas/threspoints_2026030200.txt",
    "mom:dataType": "GloFAS",
    "dcterms:format": "GloFAS threspoints station table (comma-separated text)",
    "mom:glofasNodataValue": -9999,
    "mom:dataTime": "2026-03-02T00:00:00Z",
    "generatedAtTime": "2026-03-02T00:58:10Z",
    "wasAttributedTo": "run:ecmwf"
  },
  {
    "id": "run:glofas-points",
    "provType": "Entity",
    "entityType": "prov:Entity",
    "name": "GLOFAS/threspoints_2026030200.csv",
    "mom:dataType": "GloFAS",
    "dcterms:format": "text/csv",
    "mom:glofasNodataValue": -9999,
    "mom:dataTime": "2026-03-02T00:00:00Z",
    "generatedAtTime": "2026-03-02T00:58:12Z",
    "wasDerivedFrom": "run:glofas-txt"
  },
  {
    "id": "run:attributes",
    "provType": "Entity",
    "entityType": "prov:Entity",
    "name": "data/Attributes.csv",
    "dcterms:format": "text/csv",
    "dcterms:hasVersion": "0.0.1-alpha",
    "dcterms:isPartOf": "run:mom"
  },
  {
    "id": "run:resilience",
    "provType": "Entity",
    "entityType": "prov:Entity",
    "name": "data/Resilience_Index.csv",
    "dcterms:format": "text/csv",
    "dcterms:hasVersion": "0.0.1-alpha",
    "dcterms:isPartOf": "run:mom"
  },
  {
    "id": "run:weights",
    "provType": "Entity",
    "entityType": "prov:Entity",
    "name": "data/GFMS_Weightage.csv",
    "dcterms:format": "text/csv",
    "dcterms:hasVersion": "0.0.1-alpha",
    "dcterms:isPartOf": "run:mom"
  },
  {
    "id": "run:hazard-parameters",
    "provType": "Entity",
    "entityType": "prov:Entity",
    "name": "GloFAS + GFMS hazard score accumulation parameters",
    "dcterms:hasVersion": "0.0.1-alpha",
    "dcterms:isPartOf": "run:mom",
    "mom:gfmsDurationAreaThresholdKm2": 50
  },
  {
    "id": "run:hazard",
    "provType": "Activity",
    "activityType": "pt:WeightedScoringAndClassification",
    "processType": "https://w3id.org/ogc/ospd/activity-type/WeightedScoringAndClassification",
    "name": "GloFAS + GFMS hazard score accumulation",
    "startedAtTime": "2026-03-02T01:12:40Z",
    "endedAtTime": "2026-03-02T01:12:47Z",
    "used": [
      "run:gfms-aggregates",
      "run:gfms-summary-prev",
      "run:glofas-points",
      "run:attributes",
      "run:resilience",
      "run:weights",
      "run:hazard-parameters"
    ],
    "generated": [
      "run:gfms-summary",
      "run:final-attributes",
      "run:attributes-clean"
    ],
    "wasAssociatedWith": [
      "run:mom",
      "run:rss-hydro",
      "run:server"
    ],
    "dcterms:isPartOf": "run:workflow-run"
  },
  {
    "id": "run:gfms-summary",
    "provType": "Entity",
    "entityType": "prov:Entity",
    "name": "GFMS_summary/Flood_byStor_2026030200.csv (duration recalculated)",
    "mom:dataType": "GFMS",
    "dcterms:format": "text/csv",
    "mom:dataTime": "2026-03-02T00:00:00Z",
    "generatedAtTime": "2026-03-02T01:12:41Z",
    "wasGeneratedBy": "run:hazard",
    "wasDerivedFrom": [
      "run:gfms-aggregates",
      "run:gfms-summary-prev"
    ]
  },
  {
    "id": "run:final-attributes",
    "provType": "Entity",
    "entityType": "mom:HazardScore",
    "name": "GFMS_MoM/Final_Attributes_20260302.csv",
    "mom:dataType": [
      "GloFAS",
      "GFMS"
    ],
    "dcterms:format": "text/csv",
    "mom:dataTime": "2026-03-02T00:00:00Z",
    "generatedAtTime": "2026-03-02T01:12:47Z",
    "wasGeneratedBy": "run:hazard",
    "wasDerivedFrom": [
      "run:gfms-summary",
      "run:glofas-points",
      "run:attributes",
      "run:resilience",
      "run:weights"
    ]
  },
  {
    "id": "run:attributes-clean",
    "provType": "Entity",
    "entityType": "prov:Entity",
    "name": "GFMS_MoM/Attributes_Clean_20260302.csv",
    "dcterms:format": "text/csv",
    "generatedAtTime": "2026-03-02T01:12:47Z",
    "wasGeneratedBy": "run:hazard",
    "wasDerivedFrom": "run:final-attributes"
  },
  {
    "id": "run:source-1-data",
    "provType": "Entity",
    "entityType": "prov:Entity",
    "name": "Source 1 grid, cycle 2026030118",
    "dcat:downloadURL": "https://example.org/source-1/2026030118.grb2",
    "mom:dataType": "Source 1",
    "dcterms:format": "GRIB2",
    "mom:dataTime": "2026-03-01T18:00:00Z",
    "generatedAtTime": "2026-03-01T23:47:05Z",
    "wasAttributedTo": "run:provider-1"
  },
  {
    "id": "run:source-1-score",
    "provType": "Entity",
    "entityType": "mom:HazardScore",
    "name": "Source 1 hazard scores, cycle 2026030118",
    "mom:dataType": "Source 1",
    "dcterms:format": "text/csv",
    "mom:dataTime": "2026-03-01T18:00:00Z",
    "generatedAtTime": "2026-03-02T00:52:19Z",
    "wasDerivedFrom": "run:source-1-data"
  },
  {
    "id": "run:source-2-data",
    "provType": "Entity",
    "entityType": "prov:Entity",
    "name": "Source 2 grid 20260228",
    "dcat:downloadURL": "https://example.org/source-2/20260228.tif",
    "mom:dataType": "Source 2",
    "dcterms:format": "GeoTIFF",
    "mom:dataTime": "2026-02-28T00:00:00Z",
    "generatedAtTime": "2026-03-01T02:10:44Z",
    "wasAttributedTo": "run:provider-1"
  },
  {
    "id": "run:source-2-score",
    "provType": "Entity",
    "entityType": "mom:HazardScore",
    "name": "Source 2 hazard scores 20260228",
    "mom:dataType": "Source 2",
    "dcterms:format": "text/csv",
    "mom:dataTime": "2026-02-28T00:00:00Z",
    "generatedAtTime": "2026-03-01T04:12:30Z",
    "wasDerivedFrom": "run:source-2-data"
  },
  {
    "id": "run:viirs-data",
    "provType": "Entity",
    "entityType": "prov:Entity",
    "name": "VIIRS flood extent 20260228",
    "dcat:downloadURL": "https://example.org/viirs/VIIRS_20260228.tif",
    "mom:dataType": "VIIRS",
    "dcterms:format": "GeoTIFF",
    "mom:dataTime": "2026-02-28T00:00:00Z",
    "generatedAtTime": "2026-03-01T09:02:13Z",
    "wasAttributedTo": "run:noaa"
  },
  {
    "id": "run:viirs-score",
    "provType": "Entity",
    "entityType": "mom:HazardScore",
    "name": "VIIRS hazard scores 20260228",
    "mom:dataType": "VIIRS",
    "dcterms:format": "text/csv",
    "mom:dataTime": "2026-02-28T00:00:00Z",
    "generatedAtTime": "2026-03-01T11:41:08Z",
    "wasDerivedFrom": "run:viirs-data"
  },
  {
    "id": "run:final-alert-prev",
    "provType": "Entity",
    "entityType": "prov:Entity",
    "name": "Final_Alert/Final_Alert_2026030118.csv",
    "dcterms:format": "text/csv",
    "generatedAtTime": "2026-03-01T19:13:02Z",
    "wasGeneratedBy": "https://example.org/mom/run/2026030118/final-alert"
  },
  {
    "id": "run:admin-centroids",
    "provType": "Entity",
    "entityType": "prov:Entity",
    "name": "data/Admin0_1_union_centroid.csv",
    "dcterms:format": "text/csv",
    "dcterms:hasVersion": "0.0.1-alpha",
    "dcterms:isPartOf": "run:mom"
  },
  {
    "id": "run:final-alert",
    "provType": "Activity",
    "activityType": "pt:ScoringAndProgressTracking",
    "processType": "https://w3id.org/ogc/ospd/activity-type/ScoringAndProgressTracking",
    "name": "Final alert",
    "startedAtTime": "2026-03-02T01:12:48Z",
    "endedAtTime": "2026-03-02T01:12:52Z",
    "used": [
      "run:final-attributes",
      "run:source-1-score",
      "run:source-2-score",
      "run:viirs-score",
      "run:final-alert-prev",
      "run:admin-centroids"
    ],
    "generated": "run:final-alert-output",
    "wasAssociatedWith": [
      "run:mom",
      "run:rss-hydro",
      "run:server"
    ],
    "dcterms:isPartOf": "run:workflow-run"
  },
  {
    "id": "run:final-alert-output",
    "provType": "Entity",
    "entityType": "prov:Entity",
    "name": "Final_Alert/Final_Alert_2026030200.csv",
    "dcterms:format": "text/csv",
    "generatedAtTime": "2026-03-02T01:12:52Z",
    "wasGeneratedBy": "run:final-alert",
    "wasDerivedFrom": [
      "run:final-attributes",
      "run:source-1-score",
      "run:source-2-score",
      "run:viirs-score",
      "run:final-alert-prev",
      "run:admin-centroids"
    ]
  }
]

```

#### jsonld
```jsonld
{
  "@context": [
    {
      "run": "https://example.org/mom/run/2026030200/"
    },
    "https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/rss-hydro/workflow/model-of-models/context.jsonld"
  ],
  "@graph": [
    {
      "id": "run:mom",
      "provType": "Agent",
      "agentType": "prov:SoftwareAgent",
      "name": "MoMProduction",
      "dcterms:hasVersion": "0.0.1-alpha"
    },
    {
      "id": "run:rss-hydro",
      "provType": "Agent",
      "agentType": "prov:Organization",
      "name": "RSS-Hydro"
    },
    {
      "id": "run:server",
      "provType": "Agent",
      "agentType": "prov:Agent",
      "name": "mom-prod-01 (illustrative server)"
    },
    {
      "id": "run:workflow-run",
      "provType": "Activity",
      "activityType": "https://w3id.org/ogc/ospd/activity-type/workflow",
      "name": "MoM workflow run, 2026-03-02 00:00",
      "startedAtTime": "2026-03-02T01:05:33Z",
      "endedAtTime": "2026-03-02T01:12:52Z",
      "wasAssociatedWith": [
        "run:mom",
        "run:rss-hydro",
        "run:server"
      ]
    },
    {
      "id": "run:umd",
      "provType": "Agent",
      "agentType": "prov:Organization",
      "name": "University of Maryland (GFMS)"
    },
    {
      "id": "run:ecmwf",
      "provType": "Agent",
      "agentType": "prov:Organization",
      "name": "ECMWF / CEMS (GloFAS)"
    },
    {
      "id": "run:provider-1",
      "provType": "Agent",
      "agentType": "prov:Organization",
      "name": "Provider of sources 1 and 2"
    },
    {
      "id": "run:noaa",
      "provType": "Agent",
      "agentType": "prov:Organization",
      "name": "NOAA (VIIRS)"
    },
    {
      "id": "run:watersheds",
      "provType": "Entity",
      "entityType": "prov:Entity",
      "name": "Watershed_pfaf_id.shp",
      "dcterms:hasVersion": "0.0.0",
      "dcterms:format": "ESRI Shapefile",
      "mom:watershedFingerprint": "a09161ac707ef1d0355e92e730c8fe31e127149b803321bc988b3232058eea17",
      "generatedAtTime": "2026-01-15T00:00:00Z"
    },
    {
      "id": "run:gfms-bin",
      "provType": "Entity",
      "entityType": "prov:Entity",
      "name": "Flood_byStor_2026030200.bin",
      "dcat:downloadURL": "https://example.org/gfms/Flood_byStor_2026030200.bin",
      "mom:dataType": "GFMS",
      "dcterms:format": "GFMS Flood_byStor binary grid (float32)",
      "mom:gfmsNodataValue": -9999,
      "mom:dataTime": "2026-03-02T00:00:00Z",
      "generatedAtTime": "2026-03-02T01:05:32Z",
      "wasAttributedTo": "run:umd"
    },
    {
      "id": "run:aggregation-parameters",
      "provType": "Entity",
      "entityType": "prov:Entity",
      "name": "GFMS per-watershed aggregation parameters",
      "dcterms:hasVersion": "0.0.1-alpha",
      "dcterms:isPartOf": "run:mom",
      "mom:gfmsDurationAreaThresholdKm2": 50,
      "mom:gfmsMinFileSizeBytes": 1000000
    },
    {
      "id": "run:aggregation",
      "provType": "Activity",
      "activityType": "pt:ZonalStatistics",
      "processType": "https://w3id.org/ogc/ospd/activity-type/ZonalStatistics",
      "name": "GFMS per-watershed aggregation",
      "startedAtTime": "2026-03-02T01:05:33Z",
      "endedAtTime": "2026-03-02T01:05:41Z",
      "used": [
        "run:gfms-bin",
        "run:watersheds",
        "run:aggregation-parameters"
      ],
      "generated": "run:gfms-aggregates",
      "wasAssociatedWith": [
        "run:mom",
        "run:rss-hydro",
        "run:server"
      ],
      "dcterms:isPartOf": "run:workflow-run"
    },
    {
      "id": "run:gfms-aggregates",
      "provType": "Entity",
      "entityType": "prov:Entity",
      "name": "Processing/gfms/Flood_byStor_2026030200.csv (per-watershed aggregates, duration not yet recalculated)",
      "mom:dataType": "GFMS",
      "dcterms:format": "text/csv",
      "mom:dataTime": "2026-03-02T00:00:00Z",
      "generatedAtTime": "2026-03-02T01:05:41Z",
      "wasGeneratedBy": "run:aggregation",
      "wasDerivedFrom": [
        "run:gfms-bin",
        "run:watersheds"
      ]
    },
    {
      "id": "run:gfms-summary-prev",
      "provType": "Entity",
      "entityType": "prov:Entity",
      "name": "GFMS_summary/Flood_byStor_2026030121.csv",
      "mom:dataType": "GFMS",
      "dcterms:format": "text/csv",
      "mom:dataTime": "2026-03-01T21:00:00Z",
      "generatedAtTime": "2026-03-01T01:07:12Z"
    },
    {
      "id": "run:glofas-txt",
      "provType": "Entity",
      "entityType": "prov:Entity",
      "name": "threspoints_2026030200.txt",
      "dcat:downloadURL": "https://example.org/glofas/threspoints_2026030200.txt",
      "mom:dataType": "GloFAS",
      "dcterms:format": "GloFAS threspoints station table (comma-separated text)",
      "mom:glofasNodataValue": -9999,
      "mom:dataTime": "2026-03-02T00:00:00Z",
      "generatedAtTime": "2026-03-02T00:58:10Z",
      "wasAttributedTo": "run:ecmwf"
    },
    {
      "id": "run:glofas-points",
      "provType": "Entity",
      "entityType": "prov:Entity",
      "name": "GLOFAS/threspoints_2026030200.csv",
      "mom:dataType": "GloFAS",
      "dcterms:format": "text/csv",
      "mom:glofasNodataValue": -9999,
      "mom:dataTime": "2026-03-02T00:00:00Z",
      "generatedAtTime": "2026-03-02T00:58:12Z",
      "wasDerivedFrom": "run:glofas-txt"
    },
    {
      "id": "run:attributes",
      "provType": "Entity",
      "entityType": "prov:Entity",
      "name": "data/Attributes.csv",
      "dcterms:format": "text/csv",
      "dcterms:hasVersion": "0.0.1-alpha",
      "dcterms:isPartOf": "run:mom"
    },
    {
      "id": "run:resilience",
      "provType": "Entity",
      "entityType": "prov:Entity",
      "name": "data/Resilience_Index.csv",
      "dcterms:format": "text/csv",
      "dcterms:hasVersion": "0.0.1-alpha",
      "dcterms:isPartOf": "run:mom"
    },
    {
      "id": "run:weights",
      "provType": "Entity",
      "entityType": "prov:Entity",
      "name": "data/GFMS_Weightage.csv",
      "dcterms:format": "text/csv",
      "dcterms:hasVersion": "0.0.1-alpha",
      "dcterms:isPartOf": "run:mom"
    },
    {
      "id": "run:hazard-parameters",
      "provType": "Entity",
      "entityType": "prov:Entity",
      "name": "GloFAS + GFMS hazard score accumulation parameters",
      "dcterms:hasVersion": "0.0.1-alpha",
      "dcterms:isPartOf": "run:mom",
      "mom:gfmsDurationAreaThresholdKm2": 50
    },
    {
      "id": "run:hazard",
      "provType": "Activity",
      "activityType": "pt:WeightedScoringAndClassification",
      "processType": "https://w3id.org/ogc/ospd/activity-type/WeightedScoringAndClassification",
      "name": "GloFAS + GFMS hazard score accumulation",
      "startedAtTime": "2026-03-02T01:12:40Z",
      "endedAtTime": "2026-03-02T01:12:47Z",
      "used": [
        "run:gfms-aggregates",
        "run:gfms-summary-prev",
        "run:glofas-points",
        "run:attributes",
        "run:resilience",
        "run:weights",
        "run:hazard-parameters"
      ],
      "generated": [
        "run:gfms-summary",
        "run:final-attributes",
        "run:attributes-clean"
      ],
      "wasAssociatedWith": [
        "run:mom",
        "run:rss-hydro",
        "run:server"
      ],
      "dcterms:isPartOf": "run:workflow-run"
    },
    {
      "id": "run:gfms-summary",
      "provType": "Entity",
      "entityType": "prov:Entity",
      "name": "GFMS_summary/Flood_byStor_2026030200.csv (duration recalculated)",
      "mom:dataType": "GFMS",
      "dcterms:format": "text/csv",
      "mom:dataTime": "2026-03-02T00:00:00Z",
      "generatedAtTime": "2026-03-02T01:12:41Z",
      "wasGeneratedBy": "run:hazard",
      "wasDerivedFrom": [
        "run:gfms-aggregates",
        "run:gfms-summary-prev"
      ]
    },
    {
      "id": "run:final-attributes",
      "provType": "Entity",
      "entityType": "mom:HazardScore",
      "name": "GFMS_MoM/Final_Attributes_20260302.csv",
      "mom:dataType": [
        "GloFAS",
        "GFMS"
      ],
      "dcterms:format": "text/csv",
      "mom:dataTime": "2026-03-02T00:00:00Z",
      "generatedAtTime": "2026-03-02T01:12:47Z",
      "wasGeneratedBy": "run:hazard",
      "wasDerivedFrom": [
        "run:gfms-summary",
        "run:glofas-points",
        "run:attributes",
        "run:resilience",
        "run:weights"
      ]
    },
    {
      "id": "run:attributes-clean",
      "provType": "Entity",
      "entityType": "prov:Entity",
      "name": "GFMS_MoM/Attributes_Clean_20260302.csv",
      "dcterms:format": "text/csv",
      "generatedAtTime": "2026-03-02T01:12:47Z",
      "wasGeneratedBy": "run:hazard",
      "wasDerivedFrom": "run:final-attributes"
    },
    {
      "id": "run:source-1-data",
      "provType": "Entity",
      "entityType": "prov:Entity",
      "name": "Source 1 grid, cycle 2026030118",
      "dcat:downloadURL": "https://example.org/source-1/2026030118.grb2",
      "mom:dataType": "Source 1",
      "dcterms:format": "GRIB2",
      "mom:dataTime": "2026-03-01T18:00:00Z",
      "generatedAtTime": "2026-03-01T23:47:05Z",
      "wasAttributedTo": "run:provider-1"
    },
    {
      "id": "run:source-1-score",
      "provType": "Entity",
      "entityType": "mom:HazardScore",
      "name": "Source 1 hazard scores, cycle 2026030118",
      "mom:dataType": "Source 1",
      "dcterms:format": "text/csv",
      "mom:dataTime": "2026-03-01T18:00:00Z",
      "generatedAtTime": "2026-03-02T00:52:19Z",
      "wasDerivedFrom": "run:source-1-data"
    },
    {
      "id": "run:source-2-data",
      "provType": "Entity",
      "entityType": "prov:Entity",
      "name": "Source 2 grid 20260228",
      "dcat:downloadURL": "https://example.org/source-2/20260228.tif",
      "mom:dataType": "Source 2",
      "dcterms:format": "GeoTIFF",
      "mom:dataTime": "2026-02-28T00:00:00Z",
      "generatedAtTime": "2026-03-01T02:10:44Z",
      "wasAttributedTo": "run:provider-1"
    },
    {
      "id": "run:source-2-score",
      "provType": "Entity",
      "entityType": "mom:HazardScore",
      "name": "Source 2 hazard scores 20260228",
      "mom:dataType": "Source 2",
      "dcterms:format": "text/csv",
      "mom:dataTime": "2026-02-28T00:00:00Z",
      "generatedAtTime": "2026-03-01T04:12:30Z",
      "wasDerivedFrom": "run:source-2-data"
    },
    {
      "id": "run:viirs-data",
      "provType": "Entity",
      "entityType": "prov:Entity",
      "name": "VIIRS flood extent 20260228",
      "dcat:downloadURL": "https://example.org/viirs/VIIRS_20260228.tif",
      "mom:dataType": "VIIRS",
      "dcterms:format": "GeoTIFF",
      "mom:dataTime": "2026-02-28T00:00:00Z",
      "generatedAtTime": "2026-03-01T09:02:13Z",
      "wasAttributedTo": "run:noaa"
    },
    {
      "id": "run:viirs-score",
      "provType": "Entity",
      "entityType": "mom:HazardScore",
      "name": "VIIRS hazard scores 20260228",
      "mom:dataType": "VIIRS",
      "dcterms:format": "text/csv",
      "mom:dataTime": "2026-02-28T00:00:00Z",
      "generatedAtTime": "2026-03-01T11:41:08Z",
      "wasDerivedFrom": "run:viirs-data"
    },
    {
      "id": "run:final-alert-prev",
      "provType": "Entity",
      "entityType": "prov:Entity",
      "name": "Final_Alert/Final_Alert_2026030118.csv",
      "dcterms:format": "text/csv",
      "generatedAtTime": "2026-03-01T19:13:02Z",
      "wasGeneratedBy": "https://example.org/mom/run/2026030118/final-alert"
    },
    {
      "id": "run:admin-centroids",
      "provType": "Entity",
      "entityType": "prov:Entity",
      "name": "data/Admin0_1_union_centroid.csv",
      "dcterms:format": "text/csv",
      "dcterms:hasVersion": "0.0.1-alpha",
      "dcterms:isPartOf": "run:mom"
    },
    {
      "id": "run:final-alert",
      "provType": "Activity",
      "activityType": "pt:ScoringAndProgressTracking",
      "processType": "https://w3id.org/ogc/ospd/activity-type/ScoringAndProgressTracking",
      "name": "Final alert",
      "startedAtTime": "2026-03-02T01:12:48Z",
      "endedAtTime": "2026-03-02T01:12:52Z",
      "used": [
        "run:final-attributes",
        "run:source-1-score",
        "run:source-2-score",
        "run:viirs-score",
        "run:final-alert-prev",
        "run:admin-centroids"
      ],
      "generated": "run:final-alert-output",
      "wasAssociatedWith": [
        "run:mom",
        "run:rss-hydro",
        "run:server"
      ],
      "dcterms:isPartOf": "run:workflow-run"
    },
    {
      "id": "run:final-alert-output",
      "provType": "Entity",
      "entityType": "prov:Entity",
      "name": "Final_Alert/Final_Alert_2026030200.csv",
      "dcterms:format": "text/csv",
      "generatedAtTime": "2026-03-02T01:12:52Z",
      "wasGeneratedBy": "run:final-alert",
      "wasDerivedFrom": [
        "run:final-attributes",
        "run:source-1-score",
        "run:source-2-score",
        "run:viirs-score",
        "run:final-alert-prev",
        "run:admin-centroids"
      ]
    }
  ]
}
```

#### ttl
```ttl
@prefix dcat: <http://www.w3.org/ns/dcat#> .
@prefix dcterms: <http://purl.org/dc/terms/> .
@prefix mom: <https://rss-hydro.lu/ns/mom/> .
@prefix prov: <http://www.w3.org/ns/prov#> .
@prefix pt: <https://w3id.org/ogc/ospd/activity-type/> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix run: <https://example.org/mom/run/2026030200/> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

run:aggregation a prov:Activity ;
    rdfs:label "GFMS per-watershed aggregation" ;
    dcterms:isPartOf run:workflow-run ;
    dcterms:type pt:ZonalStatistics ;
    prov:endedAtTime "2026-03-02T01:05:41+00:00"^^xsd:dateTime ;
    prov:generated run:gfms-aggregates ;
    prov:startedAtTime "2026-03-02T01:05:33+00:00"^^xsd:dateTime ;
    prov:type pt:ZonalStatistics ;
    prov:used run:aggregation-parameters,
        run:gfms-bin,
        run:watersheds ;
    prov:wasAssociatedWith run:mom,
        run:rss-hydro,
        run:server .

run:aggregation-parameters a prov:Entity ;
    rdfs:label "GFMS per-watershed aggregation parameters" ;
    dcterms:hasVersion "0.0.1-alpha" ;
    dcterms:isPartOf run:mom ;
    prov:type prov:Entity ;
    mom:gfmsDurationAreaThresholdKm2 50 ;
    mom:gfmsMinFileSizeBytes 1000000 .

run:attributes-clean a prov:Entity ;
    rdfs:label "GFMS_MoM/Attributes_Clean_20260302.csv" ;
    dcterms:format "text/csv" ;
    prov:generatedAtTime "2026-03-02T01:12:47+00:00"^^xsd:dateTime ;
    prov:type prov:Entity ;
    prov:wasDerivedFrom run:final-attributes ;
    prov:wasGeneratedBy run:hazard .

run:ecmwf a prov:Agent ;
    rdfs:label "ECMWF / CEMS (GloFAS)" ;
    prov:type prov:Organization .

run:final-alert a prov:Activity ;
    rdfs:label "Final alert" ;
    dcterms:isPartOf run:workflow-run ;
    dcterms:type pt:ScoringAndProgressTracking ;
    prov:endedAtTime "2026-03-02T01:12:52+00:00"^^xsd:dateTime ;
    prov:generated run:final-alert-output ;
    prov:startedAtTime "2026-03-02T01:12:48+00:00"^^xsd:dateTime ;
    prov:type pt:ScoringAndProgressTracking ;
    prov:used run:admin-centroids,
        run:final-alert-prev,
        run:final-attributes,
        run:source-1-score,
        run:source-2-score,
        run:viirs-score ;
    prov:wasAssociatedWith run:mom,
        run:rss-hydro,
        run:server .

run:final-alert-output a prov:Entity ;
    rdfs:label "Final_Alert/Final_Alert_2026030200.csv" ;
    dcterms:format "text/csv" ;
    prov:generatedAtTime "2026-03-02T01:12:52+00:00"^^xsd:dateTime ;
    prov:type prov:Entity ;
    prov:wasDerivedFrom run:admin-centroids,
        run:final-alert-prev,
        run:final-attributes,
        run:source-1-score,
        run:source-2-score,
        run:viirs-score ;
    prov:wasGeneratedBy run:final-alert .

run:glofas-txt a prov:Entity ;
    rdfs:label "threspoints_2026030200.txt" ;
    dcterms:format "GloFAS threspoints station table (comma-separated text)" ;
    dcat:downloadURL <https://example.org/glofas/threspoints_2026030200.txt> ;
    prov:generatedAtTime "2026-03-02T00:58:10+00:00"^^xsd:dateTime ;
    prov:type prov:Entity ;
    prov:wasAttributedTo run:ecmwf ;
    mom:dataTime "2026-03-02T00:00:00+00:00"^^xsd:dateTime ;
    mom:dataType "GloFAS" ;
    mom:glofasNodataValue -9999 .

run:hazard-parameters a prov:Entity ;
    rdfs:label "GloFAS + GFMS hazard score accumulation parameters" ;
    dcterms:hasVersion "0.0.1-alpha" ;
    dcterms:isPartOf run:mom ;
    prov:type prov:Entity ;
    mom:gfmsDurationAreaThresholdKm2 50 .

run:noaa a prov:Agent ;
    rdfs:label "NOAA (VIIRS)" ;
    prov:type prov:Organization .

run:source-1-data a prov:Entity ;
    rdfs:label "Source 1 grid, cycle 2026030118" ;
    dcterms:format "GRIB2" ;
    dcat:downloadURL <https://example.org/source-1/2026030118.grb2> ;
    prov:generatedAtTime "2026-03-01T23:47:05+00:00"^^xsd:dateTime ;
    prov:type prov:Entity ;
    prov:wasAttributedTo run:provider-1 ;
    mom:dataTime "2026-03-01T18:00:00+00:00"^^xsd:dateTime ;
    mom:dataType "Source 1" .

run:source-2-data a prov:Entity ;
    rdfs:label "Source 2 grid 20260228" ;
    dcterms:format "GeoTIFF" ;
    dcat:downloadURL <https://example.org/source-2/20260228.tif> ;
    prov:generatedAtTime "2026-03-01T02:10:44+00:00"^^xsd:dateTime ;
    prov:type prov:Entity ;
    prov:wasAttributedTo run:provider-1 ;
    mom:dataTime "2026-02-28T00:00:00+00:00"^^xsd:dateTime ;
    mom:dataType "Source 2" .

run:umd a prov:Agent ;
    rdfs:label "University of Maryland (GFMS)" ;
    prov:type prov:Organization .

run:viirs-data a prov:Entity ;
    rdfs:label "VIIRS flood extent 20260228" ;
    dcterms:format "GeoTIFF" ;
    dcat:downloadURL <https://example.org/viirs/VIIRS_20260228.tif> ;
    prov:generatedAtTime "2026-03-01T09:02:13+00:00"^^xsd:dateTime ;
    prov:type prov:Entity ;
    prov:wasAttributedTo run:noaa ;
    mom:dataTime "2026-02-28T00:00:00+00:00"^^xsd:dateTime ;
    mom:dataType "VIIRS" .

run:admin-centroids a prov:Entity ;
    rdfs:label "data/Admin0_1_union_centroid.csv" ;
    dcterms:format "text/csv" ;
    dcterms:hasVersion "0.0.1-alpha" ;
    dcterms:isPartOf run:mom ;
    prov:type prov:Entity .

run:attributes a prov:Entity ;
    rdfs:label "data/Attributes.csv" ;
    dcterms:format "text/csv" ;
    dcterms:hasVersion "0.0.1-alpha" ;
    dcterms:isPartOf run:mom ;
    prov:type prov:Entity .

run:final-alert-prev a prov:Entity ;
    rdfs:label "Final_Alert/Final_Alert_2026030118.csv" ;
    dcterms:format "text/csv" ;
    prov:generatedAtTime "2026-03-01T19:13:02+00:00"^^xsd:dateTime ;
    prov:type prov:Entity ;
    prov:wasGeneratedBy <https://example.org/mom/run/2026030118/final-alert> .

run:gfms-bin a prov:Entity ;
    rdfs:label "Flood_byStor_2026030200.bin" ;
    dcterms:format "GFMS Flood_byStor binary grid (float32)" ;
    dcat:downloadURL <https://example.org/gfms/Flood_byStor_2026030200.bin> ;
    prov:generatedAtTime "2026-03-02T01:05:32+00:00"^^xsd:dateTime ;
    prov:type prov:Entity ;
    prov:wasAttributedTo run:umd ;
    mom:dataTime "2026-03-02T00:00:00+00:00"^^xsd:dateTime ;
    mom:dataType "GFMS" ;
    mom:gfmsNodataValue -9999 .

run:gfms-summary a prov:Entity ;
    rdfs:label "GFMS_summary/Flood_byStor_2026030200.csv (duration recalculated)" ;
    dcterms:format "text/csv" ;
    prov:generatedAtTime "2026-03-02T01:12:41+00:00"^^xsd:dateTime ;
    prov:type prov:Entity ;
    prov:wasDerivedFrom run:gfms-aggregates,
        run:gfms-summary-prev ;
    prov:wasGeneratedBy run:hazard ;
    mom:dataTime "2026-03-02T00:00:00+00:00"^^xsd:dateTime ;
    mom:dataType "GFMS" .

run:gfms-summary-prev a prov:Entity ;
    rdfs:label "GFMS_summary/Flood_byStor_2026030121.csv" ;
    dcterms:format "text/csv" ;
    prov:generatedAtTime "2026-03-01T01:07:12+00:00"^^xsd:dateTime ;
    prov:type prov:Entity ;
    mom:dataTime "2026-03-01T21:00:00+00:00"^^xsd:dateTime ;
    mom:dataType "GFMS" .

run:glofas-points a prov:Entity ;
    rdfs:label "GLOFAS/threspoints_2026030200.csv" ;
    dcterms:format "text/csv" ;
    prov:generatedAtTime "2026-03-02T00:58:12+00:00"^^xsd:dateTime ;
    prov:type prov:Entity ;
    prov:wasDerivedFrom run:glofas-txt ;
    mom:dataTime "2026-03-02T00:00:00+00:00"^^xsd:dateTime ;
    mom:dataType "GloFAS" ;
    mom:glofasNodataValue -9999 .

run:provider-1 a prov:Agent ;
    rdfs:label "Provider of sources 1 and 2" ;
    prov:type prov:Organization .

run:resilience a prov:Entity ;
    rdfs:label "data/Resilience_Index.csv" ;
    dcterms:format "text/csv" ;
    dcterms:hasVersion "0.0.1-alpha" ;
    dcterms:isPartOf run:mom ;
    prov:type prov:Entity .

run:source-1-score a prov:Entity ;
    rdfs:label "Source 1 hazard scores, cycle 2026030118" ;
    dcterms:format "text/csv" ;
    prov:generatedAtTime "2026-03-02T00:52:19+00:00"^^xsd:dateTime ;
    prov:type mom:HazardScore ;
    prov:wasDerivedFrom run:source-1-data ;
    mom:dataTime "2026-03-01T18:00:00+00:00"^^xsd:dateTime ;
    mom:dataType "Source 1" .

run:source-2-score a prov:Entity ;
    rdfs:label "Source 2 hazard scores 20260228" ;
    dcterms:format "text/csv" ;
    prov:generatedAtTime "2026-03-01T04:12:30+00:00"^^xsd:dateTime ;
    prov:type mom:HazardScore ;
    prov:wasDerivedFrom run:source-2-data ;
    mom:dataTime "2026-02-28T00:00:00+00:00"^^xsd:dateTime ;
    mom:dataType "Source 2" .

run:viirs-score a prov:Entity ;
    rdfs:label "VIIRS hazard scores 20260228" ;
    dcterms:format "text/csv" ;
    prov:generatedAtTime "2026-03-01T11:41:08+00:00"^^xsd:dateTime ;
    prov:type mom:HazardScore ;
    prov:wasDerivedFrom run:viirs-data ;
    mom:dataTime "2026-02-28T00:00:00+00:00"^^xsd:dateTime ;
    mom:dataType "VIIRS" .

run:watersheds a prov:Entity ;
    rdfs:label "Watershed_pfaf_id.shp" ;
    dcterms:format "ESRI Shapefile" ;
    dcterms:hasVersion "0.0.0" ;
    prov:generatedAtTime "2026-01-15T00:00:00+00:00"^^xsd:dateTime ;
    prov:type prov:Entity ;
    mom:watershedFingerprint "a09161ac707ef1d0355e92e730c8fe31e127149b803321bc988b3232058eea17" .

run:weights a prov:Entity ;
    rdfs:label "data/GFMS_Weightage.csv" ;
    dcterms:format "text/csv" ;
    dcterms:hasVersion "0.0.1-alpha" ;
    dcterms:isPartOf run:mom ;
    prov:type prov:Entity .

run:gfms-aggregates a prov:Entity ;
    rdfs:label "Processing/gfms/Flood_byStor_2026030200.csv (per-watershed aggregates, duration not yet recalculated)" ;
    dcterms:format "text/csv" ;
    prov:generatedAtTime "2026-03-02T01:05:41+00:00"^^xsd:dateTime ;
    prov:type prov:Entity ;
    prov:wasDerivedFrom run:gfms-bin,
        run:watersheds ;
    prov:wasGeneratedBy run:aggregation ;
    mom:dataTime "2026-03-02T00:00:00+00:00"^^xsd:dateTime ;
    mom:dataType "GFMS" .

run:hazard a prov:Activity ;
    rdfs:label "GloFAS + GFMS hazard score accumulation" ;
    dcterms:isPartOf run:workflow-run ;
    dcterms:type pt:WeightedScoringAndClassification ;
    prov:endedAtTime "2026-03-02T01:12:47+00:00"^^xsd:dateTime ;
    prov:generated run:attributes-clean,
        run:final-attributes,
        run:gfms-summary ;
    prov:startedAtTime "2026-03-02T01:12:40+00:00"^^xsd:dateTime ;
    prov:type pt:WeightedScoringAndClassification ;
    prov:used run:attributes,
        run:gfms-aggregates,
        run:gfms-summary-prev,
        run:glofas-points,
        run:hazard-parameters,
        run:resilience,
        run:weights ;
    prov:wasAssociatedWith run:mom,
        run:rss-hydro,
        run:server .

run:workflow-run a prov:Activity ;
    rdfs:label "MoM workflow run, 2026-03-02 00:00" ;
    prov:endedAtTime "2026-03-02T01:12:52+00:00"^^xsd:dateTime ;
    prov:startedAtTime "2026-03-02T01:05:33+00:00"^^xsd:dateTime ;
    prov:type pt:workflow ;
    prov:wasAssociatedWith run:mom,
        run:rss-hydro,
        run:server .

run:final-attributes a prov:Entity ;
    rdfs:label "GFMS_MoM/Final_Attributes_20260302.csv" ;
    dcterms:format "text/csv" ;
    prov:generatedAtTime "2026-03-02T01:12:47+00:00"^^xsd:dateTime ;
    prov:type mom:HazardScore ;
    prov:wasDerivedFrom run:attributes,
        run:gfms-summary,
        run:glofas-points,
        run:resilience,
        run:weights ;
    prov:wasGeneratedBy run:hazard ;
    mom:dataTime "2026-03-02T00:00:00+00:00"^^xsd:dateTime ;
    mom:dataType "GFMS",
        "GloFAS" .

run:rss-hydro a prov:Agent ;
    rdfs:label "RSS-Hydro" ;
    prov:type prov:Organization .

run:server a prov:Agent ;
    rdfs:label "mom-prod-01 (illustrative server)" ;
    prov:type prov:Agent .

run:mom a prov:Agent ;
    rdfs:label "MoMProduction" ;
    dcterms:hasVersion "0.0.1-alpha" ;
    prov:type prov:SoftwareAgent .


```


### Run of 2026-03-02 00:00 UTC, no previous final alert
Same run without an earlier alert; every watershed is New. All values are illustrative.
#### json
```json
[
  {
    "id": "run:mom",
    "provType": "Agent",
    "agentType": "prov:SoftwareAgent",
    "name": "MoMProduction",
    "dcterms:hasVersion": "0.0.1-alpha"
  },
  {
    "id": "run:rss-hydro",
    "provType": "Agent",
    "agentType": "prov:Organization",
    "name": "RSS-Hydro"
  },
  {
    "id": "run:server",
    "provType": "Agent",
    "agentType": "prov:Agent",
    "name": "mom-prod-01 (illustrative server)"
  },
  {
    "id": "run:workflow-run",
    "provType": "Activity",
    "activityType": "https://w3id.org/ogc/ospd/activity-type/workflow",
    "name": "MoM workflow run, 2026-03-02 00:00",
    "startedAtTime": "2026-03-02T01:05:33Z",
    "endedAtTime": "2026-03-02T01:12:52Z",
    "wasAssociatedWith": [
      "run:mom",
      "run:rss-hydro",
      "run:server"
    ]
  },
  {
    "id": "run:umd",
    "provType": "Agent",
    "agentType": "prov:Organization",
    "name": "University of Maryland (GFMS)"
  },
  {
    "id": "run:ecmwf",
    "provType": "Agent",
    "agentType": "prov:Organization",
    "name": "ECMWF / CEMS (GloFAS)"
  },
  {
    "id": "run:provider-1",
    "provType": "Agent",
    "agentType": "prov:Organization",
    "name": "Provider of sources 1 and 2"
  },
  {
    "id": "run:watersheds",
    "provType": "Entity",
    "entityType": "prov:Entity",
    "name": "Watershed_pfaf_id.shp",
    "dcterms:hasVersion": "0.0.0",
    "dcterms:format": "ESRI Shapefile",
    "mom:watershedFingerprint": "a09161ac707ef1d0355e92e730c8fe31e127149b803321bc988b3232058eea17",
    "generatedAtTime": "2026-01-15T00:00:00Z"
  },
  {
    "id": "run:gfms-bin",
    "provType": "Entity",
    "entityType": "prov:Entity",
    "name": "Flood_byStor_2026030200.bin",
    "dcat:downloadURL": "https://example.org/gfms/Flood_byStor_2026030200.bin",
    "mom:dataType": "GFMS",
    "dcterms:format": "GFMS Flood_byStor binary grid (float32)",
    "mom:gfmsNodataValue": -9999,
    "mom:dataTime": "2026-03-02T00:00:00Z",
    "generatedAtTime": "2026-03-02T01:05:32Z",
    "wasAttributedTo": "run:umd"
  },
  {
    "id": "run:aggregation-parameters",
    "provType": "Entity",
    "entityType": "prov:Entity",
    "name": "GFMS per-watershed aggregation parameters",
    "dcterms:hasVersion": "0.0.1-alpha",
    "dcterms:isPartOf": "run:mom",
    "mom:gfmsDurationAreaThresholdKm2": 50,
    "mom:gfmsMinFileSizeBytes": 1000000
  },
  {
    "id": "run:aggregation",
    "provType": "Activity",
    "activityType": "pt:ZonalStatistics",
    "processType": "https://w3id.org/ogc/ospd/activity-type/ZonalStatistics",
    "name": "GFMS per-watershed aggregation",
    "startedAtTime": "2026-03-02T01:05:33Z",
    "endedAtTime": "2026-03-02T01:05:41Z",
    "used": [
      "run:gfms-bin",
      "run:watersheds",
      "run:aggregation-parameters"
    ],
    "generated": "run:gfms-aggregates",
    "wasAssociatedWith": [
      "run:mom",
      "run:rss-hydro",
      "run:server"
    ],
    "dcterms:isPartOf": "run:workflow-run"
  },
  {
    "id": "run:gfms-aggregates",
    "provType": "Entity",
    "entityType": "prov:Entity",
    "name": "Processing/gfms/Flood_byStor_2026030200.csv (per-watershed aggregates, duration not yet recalculated)",
    "mom:dataType": "GFMS",
    "dcterms:format": "text/csv",
    "mom:dataTime": "2026-03-02T00:00:00Z",
    "generatedAtTime": "2026-03-02T01:05:41Z",
    "wasGeneratedBy": "run:aggregation",
    "wasDerivedFrom": [
      "run:gfms-bin",
      "run:watersheds"
    ]
  },
  {
    "id": "run:gfms-summary-prev",
    "provType": "Entity",
    "entityType": "prov:Entity",
    "name": "GFMS_summary/Flood_byStor_2026030121.csv",
    "mom:dataType": "GFMS",
    "dcterms:format": "text/csv",
    "mom:dataTime": "2026-03-01T21:00:00Z",
    "generatedAtTime": "2026-03-01T01:07:12Z"
  },
  {
    "id": "run:glofas-txt",
    "provType": "Entity",
    "entityType": "prov:Entity",
    "name": "threspoints_2026030200.txt",
    "dcat:downloadURL": "https://example.org/glofas/threspoints_2026030200.txt",
    "mom:dataType": "GloFAS",
    "dcterms:format": "GloFAS threspoints station table (comma-separated text)",
    "mom:glofasNodataValue": -9999,
    "mom:dataTime": "2026-03-02T00:00:00Z",
    "generatedAtTime": "2026-03-02T00:58:10Z",
    "wasAttributedTo": "run:ecmwf"
  },
  {
    "id": "run:glofas-points",
    "provType": "Entity",
    "entityType": "prov:Entity",
    "name": "GLOFAS/threspoints_2026030200.csv",
    "mom:dataType": "GloFAS",
    "dcterms:format": "text/csv",
    "mom:glofasNodataValue": -9999,
    "mom:dataTime": "2026-03-02T00:00:00Z",
    "generatedAtTime": "2026-03-02T00:58:12Z",
    "wasDerivedFrom": "run:glofas-txt"
  },
  {
    "id": "run:attributes",
    "provType": "Entity",
    "entityType": "prov:Entity",
    "name": "data/Attributes.csv",
    "dcterms:format": "text/csv",
    "dcterms:hasVersion": "0.0.1-alpha",
    "dcterms:isPartOf": "run:mom"
  },
  {
    "id": "run:resilience",
    "provType": "Entity",
    "entityType": "prov:Entity",
    "name": "data/Resilience_Index.csv",
    "dcterms:format": "text/csv",
    "dcterms:hasVersion": "0.0.1-alpha",
    "dcterms:isPartOf": "run:mom"
  },
  {
    "id": "run:weights",
    "provType": "Entity",
    "entityType": "prov:Entity",
    "name": "data/GFMS_Weightage.csv",
    "dcterms:format": "text/csv",
    "dcterms:hasVersion": "0.0.1-alpha",
    "dcterms:isPartOf": "run:mom"
  },
  {
    "id": "run:hazard-parameters",
    "provType": "Entity",
    "entityType": "prov:Entity",
    "name": "GloFAS + GFMS hazard score accumulation parameters",
    "dcterms:hasVersion": "0.0.1-alpha",
    "dcterms:isPartOf": "run:mom",
    "mom:gfmsDurationAreaThresholdKm2": 50
  },
  {
    "id": "run:hazard",
    "provType": "Activity",
    "activityType": "pt:WeightedScoringAndClassification",
    "processType": "https://w3id.org/ogc/ospd/activity-type/WeightedScoringAndClassification",
    "name": "GloFAS + GFMS hazard score accumulation",
    "startedAtTime": "2026-03-02T01:12:40Z",
    "endedAtTime": "2026-03-02T01:12:47Z",
    "used": [
      "run:gfms-aggregates",
      "run:gfms-summary-prev",
      "run:glofas-points",
      "run:attributes",
      "run:resilience",
      "run:weights",
      "run:hazard-parameters"
    ],
    "generated": [
      "run:gfms-summary",
      "run:final-attributes",
      "run:attributes-clean"
    ],
    "wasAssociatedWith": [
      "run:mom",
      "run:rss-hydro",
      "run:server"
    ],
    "dcterms:isPartOf": "run:workflow-run"
  },
  {
    "id": "run:gfms-summary",
    "provType": "Entity",
    "entityType": "prov:Entity",
    "name": "GFMS_summary/Flood_byStor_2026030200.csv (duration recalculated)",
    "mom:dataType": "GFMS",
    "dcterms:format": "text/csv",
    "mom:dataTime": "2026-03-02T00:00:00Z",
    "generatedAtTime": "2026-03-02T01:12:41Z",
    "wasGeneratedBy": "run:hazard",
    "wasDerivedFrom": [
      "run:gfms-aggregates",
      "run:gfms-summary-prev"
    ]
  },
  {
    "id": "run:final-attributes",
    "provType": "Entity",
    "entityType": "mom:HazardScore",
    "name": "GFMS_MoM/Final_Attributes_20260302.csv",
    "mom:dataType": [
      "GloFAS",
      "GFMS"
    ],
    "dcterms:format": "text/csv",
    "mom:dataTime": "2026-03-02T00:00:00Z",
    "generatedAtTime": "2026-03-02T01:12:47Z",
    "wasGeneratedBy": "run:hazard",
    "wasDerivedFrom": [
      "run:gfms-summary",
      "run:glofas-points",
      "run:attributes",
      "run:resilience",
      "run:weights"
    ]
  },
  {
    "id": "run:attributes-clean",
    "provType": "Entity",
    "entityType": "prov:Entity",
    "name": "GFMS_MoM/Attributes_Clean_20260302.csv",
    "dcterms:format": "text/csv",
    "generatedAtTime": "2026-03-02T01:12:47Z",
    "wasGeneratedBy": "run:hazard",
    "wasDerivedFrom": "run:final-attributes"
  },
  {
    "id": "run:source-1-data",
    "provType": "Entity",
    "entityType": "prov:Entity",
    "name": "Source 1 grid, cycle 2026030118",
    "dcat:downloadURL": "https://example.org/source-1/2026030118.grb2",
    "mom:dataType": "Source 1",
    "dcterms:format": "GRIB2",
    "mom:dataTime": "2026-03-01T18:00:00Z",
    "generatedAtTime": "2026-03-01T23:47:05Z",
    "wasAttributedTo": "run:provider-1"
  },
  {
    "id": "run:source-1-score",
    "provType": "Entity",
    "entityType": "mom:HazardScore",
    "name": "Source 1 hazard scores, cycle 2026030118",
    "mom:dataType": "Source 1",
    "dcterms:format": "text/csv",
    "mom:dataTime": "2026-03-01T18:00:00Z",
    "generatedAtTime": "2026-03-02T00:52:19Z",
    "wasDerivedFrom": "run:source-1-data"
  },
  {
    "id": "run:source-2-data",
    "provType": "Entity",
    "entityType": "prov:Entity",
    "name": "Source 2 grid 20260228",
    "dcat:downloadURL": "https://example.org/source-2/20260228.tif",
    "mom:dataType": "Source 2",
    "dcterms:format": "GeoTIFF",
    "mom:dataTime": "2026-02-28T00:00:00Z",
    "generatedAtTime": "2026-03-01T02:10:44Z",
    "wasAttributedTo": "run:provider-1"
  },
  {
    "id": "run:source-2-score",
    "provType": "Entity",
    "entityType": "mom:HazardScore",
    "name": "Source 2 hazard scores 20260228",
    "mom:dataType": "Source 2",
    "dcterms:format": "text/csv",
    "mom:dataTime": "2026-02-28T00:00:00Z",
    "generatedAtTime": "2026-03-01T04:12:30Z",
    "wasDerivedFrom": "run:source-2-data"
  },
  {
    "id": "run:admin-centroids",
    "provType": "Entity",
    "entityType": "prov:Entity",
    "name": "data/Admin0_1_union_centroid.csv",
    "dcterms:format": "text/csv",
    "dcterms:hasVersion": "0.0.1-alpha",
    "dcterms:isPartOf": "run:mom"
  },
  {
    "id": "run:final-alert",
    "provType": "Activity",
    "activityType": "pt:ScoringAndProgressTracking",
    "processType": "https://w3id.org/ogc/ospd/activity-type/ScoringAndProgressTracking",
    "name": "Final alert",
    "startedAtTime": "2026-03-02T01:12:48Z",
    "endedAtTime": "2026-03-02T01:12:52Z",
    "used": [
      "run:final-attributes",
      "run:source-1-score",
      "run:source-2-score",
      "run:admin-centroids"
    ],
    "generated": "run:final-alert-output",
    "wasAssociatedWith": [
      "run:mom",
      "run:rss-hydro",
      "run:server"
    ],
    "dcterms:isPartOf": "run:workflow-run"
  },
  {
    "id": "run:final-alert-output",
    "provType": "Entity",
    "entityType": "prov:Entity",
    "name": "Final_Alert/Final_Alert_2026030200.csv",
    "dcterms:format": "text/csv",
    "generatedAtTime": "2026-03-02T01:12:52Z",
    "wasGeneratedBy": "run:final-alert",
    "wasDerivedFrom": [
      "run:final-attributes",
      "run:source-1-score",
      "run:source-2-score",
      "run:admin-centroids"
    ]
  }
]

```

#### jsonld
```jsonld
{
  "@context": [
    {
      "run": "https://example.org/mom/run/2026030200/"
    },
    "https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/rss-hydro/workflow/model-of-models/context.jsonld"
  ],
  "@graph": [
    {
      "id": "run:mom",
      "provType": "Agent",
      "agentType": "prov:SoftwareAgent",
      "name": "MoMProduction",
      "dcterms:hasVersion": "0.0.1-alpha"
    },
    {
      "id": "run:rss-hydro",
      "provType": "Agent",
      "agentType": "prov:Organization",
      "name": "RSS-Hydro"
    },
    {
      "id": "run:server",
      "provType": "Agent",
      "agentType": "prov:Agent",
      "name": "mom-prod-01 (illustrative server)"
    },
    {
      "id": "run:workflow-run",
      "provType": "Activity",
      "activityType": "https://w3id.org/ogc/ospd/activity-type/workflow",
      "name": "MoM workflow run, 2026-03-02 00:00",
      "startedAtTime": "2026-03-02T01:05:33Z",
      "endedAtTime": "2026-03-02T01:12:52Z",
      "wasAssociatedWith": [
        "run:mom",
        "run:rss-hydro",
        "run:server"
      ]
    },
    {
      "id": "run:umd",
      "provType": "Agent",
      "agentType": "prov:Organization",
      "name": "University of Maryland (GFMS)"
    },
    {
      "id": "run:ecmwf",
      "provType": "Agent",
      "agentType": "prov:Organization",
      "name": "ECMWF / CEMS (GloFAS)"
    },
    {
      "id": "run:provider-1",
      "provType": "Agent",
      "agentType": "prov:Organization",
      "name": "Provider of sources 1 and 2"
    },
    {
      "id": "run:watersheds",
      "provType": "Entity",
      "entityType": "prov:Entity",
      "name": "Watershed_pfaf_id.shp",
      "dcterms:hasVersion": "0.0.0",
      "dcterms:format": "ESRI Shapefile",
      "mom:watershedFingerprint": "a09161ac707ef1d0355e92e730c8fe31e127149b803321bc988b3232058eea17",
      "generatedAtTime": "2026-01-15T00:00:00Z"
    },
    {
      "id": "run:gfms-bin",
      "provType": "Entity",
      "entityType": "prov:Entity",
      "name": "Flood_byStor_2026030200.bin",
      "dcat:downloadURL": "https://example.org/gfms/Flood_byStor_2026030200.bin",
      "mom:dataType": "GFMS",
      "dcterms:format": "GFMS Flood_byStor binary grid (float32)",
      "mom:gfmsNodataValue": -9999,
      "mom:dataTime": "2026-03-02T00:00:00Z",
      "generatedAtTime": "2026-03-02T01:05:32Z",
      "wasAttributedTo": "run:umd"
    },
    {
      "id": "run:aggregation-parameters",
      "provType": "Entity",
      "entityType": "prov:Entity",
      "name": "GFMS per-watershed aggregation parameters",
      "dcterms:hasVersion": "0.0.1-alpha",
      "dcterms:isPartOf": "run:mom",
      "mom:gfmsDurationAreaThresholdKm2": 50,
      "mom:gfmsMinFileSizeBytes": 1000000
    },
    {
      "id": "run:aggregation",
      "provType": "Activity",
      "activityType": "pt:ZonalStatistics",
      "processType": "https://w3id.org/ogc/ospd/activity-type/ZonalStatistics",
      "name": "GFMS per-watershed aggregation",
      "startedAtTime": "2026-03-02T01:05:33Z",
      "endedAtTime": "2026-03-02T01:05:41Z",
      "used": [
        "run:gfms-bin",
        "run:watersheds",
        "run:aggregation-parameters"
      ],
      "generated": "run:gfms-aggregates",
      "wasAssociatedWith": [
        "run:mom",
        "run:rss-hydro",
        "run:server"
      ],
      "dcterms:isPartOf": "run:workflow-run"
    },
    {
      "id": "run:gfms-aggregates",
      "provType": "Entity",
      "entityType": "prov:Entity",
      "name": "Processing/gfms/Flood_byStor_2026030200.csv (per-watershed aggregates, duration not yet recalculated)",
      "mom:dataType": "GFMS",
      "dcterms:format": "text/csv",
      "mom:dataTime": "2026-03-02T00:00:00Z",
      "generatedAtTime": "2026-03-02T01:05:41Z",
      "wasGeneratedBy": "run:aggregation",
      "wasDerivedFrom": [
        "run:gfms-bin",
        "run:watersheds"
      ]
    },
    {
      "id": "run:gfms-summary-prev",
      "provType": "Entity",
      "entityType": "prov:Entity",
      "name": "GFMS_summary/Flood_byStor_2026030121.csv",
      "mom:dataType": "GFMS",
      "dcterms:format": "text/csv",
      "mom:dataTime": "2026-03-01T21:00:00Z",
      "generatedAtTime": "2026-03-01T01:07:12Z"
    },
    {
      "id": "run:glofas-txt",
      "provType": "Entity",
      "entityType": "prov:Entity",
      "name": "threspoints_2026030200.txt",
      "dcat:downloadURL": "https://example.org/glofas/threspoints_2026030200.txt",
      "mom:dataType": "GloFAS",
      "dcterms:format": "GloFAS threspoints station table (comma-separated text)",
      "mom:glofasNodataValue": -9999,
      "mom:dataTime": "2026-03-02T00:00:00Z",
      "generatedAtTime": "2026-03-02T00:58:10Z",
      "wasAttributedTo": "run:ecmwf"
    },
    {
      "id": "run:glofas-points",
      "provType": "Entity",
      "entityType": "prov:Entity",
      "name": "GLOFAS/threspoints_2026030200.csv",
      "mom:dataType": "GloFAS",
      "dcterms:format": "text/csv",
      "mom:glofasNodataValue": -9999,
      "mom:dataTime": "2026-03-02T00:00:00Z",
      "generatedAtTime": "2026-03-02T00:58:12Z",
      "wasDerivedFrom": "run:glofas-txt"
    },
    {
      "id": "run:attributes",
      "provType": "Entity",
      "entityType": "prov:Entity",
      "name": "data/Attributes.csv",
      "dcterms:format": "text/csv",
      "dcterms:hasVersion": "0.0.1-alpha",
      "dcterms:isPartOf": "run:mom"
    },
    {
      "id": "run:resilience",
      "provType": "Entity",
      "entityType": "prov:Entity",
      "name": "data/Resilience_Index.csv",
      "dcterms:format": "text/csv",
      "dcterms:hasVersion": "0.0.1-alpha",
      "dcterms:isPartOf": "run:mom"
    },
    {
      "id": "run:weights",
      "provType": "Entity",
      "entityType": "prov:Entity",
      "name": "data/GFMS_Weightage.csv",
      "dcterms:format": "text/csv",
      "dcterms:hasVersion": "0.0.1-alpha",
      "dcterms:isPartOf": "run:mom"
    },
    {
      "id": "run:hazard-parameters",
      "provType": "Entity",
      "entityType": "prov:Entity",
      "name": "GloFAS + GFMS hazard score accumulation parameters",
      "dcterms:hasVersion": "0.0.1-alpha",
      "dcterms:isPartOf": "run:mom",
      "mom:gfmsDurationAreaThresholdKm2": 50
    },
    {
      "id": "run:hazard",
      "provType": "Activity",
      "activityType": "pt:WeightedScoringAndClassification",
      "processType": "https://w3id.org/ogc/ospd/activity-type/WeightedScoringAndClassification",
      "name": "GloFAS + GFMS hazard score accumulation",
      "startedAtTime": "2026-03-02T01:12:40Z",
      "endedAtTime": "2026-03-02T01:12:47Z",
      "used": [
        "run:gfms-aggregates",
        "run:gfms-summary-prev",
        "run:glofas-points",
        "run:attributes",
        "run:resilience",
        "run:weights",
        "run:hazard-parameters"
      ],
      "generated": [
        "run:gfms-summary",
        "run:final-attributes",
        "run:attributes-clean"
      ],
      "wasAssociatedWith": [
        "run:mom",
        "run:rss-hydro",
        "run:server"
      ],
      "dcterms:isPartOf": "run:workflow-run"
    },
    {
      "id": "run:gfms-summary",
      "provType": "Entity",
      "entityType": "prov:Entity",
      "name": "GFMS_summary/Flood_byStor_2026030200.csv (duration recalculated)",
      "mom:dataType": "GFMS",
      "dcterms:format": "text/csv",
      "mom:dataTime": "2026-03-02T00:00:00Z",
      "generatedAtTime": "2026-03-02T01:12:41Z",
      "wasGeneratedBy": "run:hazard",
      "wasDerivedFrom": [
        "run:gfms-aggregates",
        "run:gfms-summary-prev"
      ]
    },
    {
      "id": "run:final-attributes",
      "provType": "Entity",
      "entityType": "mom:HazardScore",
      "name": "GFMS_MoM/Final_Attributes_20260302.csv",
      "mom:dataType": [
        "GloFAS",
        "GFMS"
      ],
      "dcterms:format": "text/csv",
      "mom:dataTime": "2026-03-02T00:00:00Z",
      "generatedAtTime": "2026-03-02T01:12:47Z",
      "wasGeneratedBy": "run:hazard",
      "wasDerivedFrom": [
        "run:gfms-summary",
        "run:glofas-points",
        "run:attributes",
        "run:resilience",
        "run:weights"
      ]
    },
    {
      "id": "run:attributes-clean",
      "provType": "Entity",
      "entityType": "prov:Entity",
      "name": "GFMS_MoM/Attributes_Clean_20260302.csv",
      "dcterms:format": "text/csv",
      "generatedAtTime": "2026-03-02T01:12:47Z",
      "wasGeneratedBy": "run:hazard",
      "wasDerivedFrom": "run:final-attributes"
    },
    {
      "id": "run:source-1-data",
      "provType": "Entity",
      "entityType": "prov:Entity",
      "name": "Source 1 grid, cycle 2026030118",
      "dcat:downloadURL": "https://example.org/source-1/2026030118.grb2",
      "mom:dataType": "Source 1",
      "dcterms:format": "GRIB2",
      "mom:dataTime": "2026-03-01T18:00:00Z",
      "generatedAtTime": "2026-03-01T23:47:05Z",
      "wasAttributedTo": "run:provider-1"
    },
    {
      "id": "run:source-1-score",
      "provType": "Entity",
      "entityType": "mom:HazardScore",
      "name": "Source 1 hazard scores, cycle 2026030118",
      "mom:dataType": "Source 1",
      "dcterms:format": "text/csv",
      "mom:dataTime": "2026-03-01T18:00:00Z",
      "generatedAtTime": "2026-03-02T00:52:19Z",
      "wasDerivedFrom": "run:source-1-data"
    },
    {
      "id": "run:source-2-data",
      "provType": "Entity",
      "entityType": "prov:Entity",
      "name": "Source 2 grid 20260228",
      "dcat:downloadURL": "https://example.org/source-2/20260228.tif",
      "mom:dataType": "Source 2",
      "dcterms:format": "GeoTIFF",
      "mom:dataTime": "2026-02-28T00:00:00Z",
      "generatedAtTime": "2026-03-01T02:10:44Z",
      "wasAttributedTo": "run:provider-1"
    },
    {
      "id": "run:source-2-score",
      "provType": "Entity",
      "entityType": "mom:HazardScore",
      "name": "Source 2 hazard scores 20260228",
      "mom:dataType": "Source 2",
      "dcterms:format": "text/csv",
      "mom:dataTime": "2026-02-28T00:00:00Z",
      "generatedAtTime": "2026-03-01T04:12:30Z",
      "wasDerivedFrom": "run:source-2-data"
    },
    {
      "id": "run:admin-centroids",
      "provType": "Entity",
      "entityType": "prov:Entity",
      "name": "data/Admin0_1_union_centroid.csv",
      "dcterms:format": "text/csv",
      "dcterms:hasVersion": "0.0.1-alpha",
      "dcterms:isPartOf": "run:mom"
    },
    {
      "id": "run:final-alert",
      "provType": "Activity",
      "activityType": "pt:ScoringAndProgressTracking",
      "processType": "https://w3id.org/ogc/ospd/activity-type/ScoringAndProgressTracking",
      "name": "Final alert",
      "startedAtTime": "2026-03-02T01:12:48Z",
      "endedAtTime": "2026-03-02T01:12:52Z",
      "used": [
        "run:final-attributes",
        "run:source-1-score",
        "run:source-2-score",
        "run:admin-centroids"
      ],
      "generated": "run:final-alert-output",
      "wasAssociatedWith": [
        "run:mom",
        "run:rss-hydro",
        "run:server"
      ],
      "dcterms:isPartOf": "run:workflow-run"
    },
    {
      "id": "run:final-alert-output",
      "provType": "Entity",
      "entityType": "prov:Entity",
      "name": "Final_Alert/Final_Alert_2026030200.csv",
      "dcterms:format": "text/csv",
      "generatedAtTime": "2026-03-02T01:12:52Z",
      "wasGeneratedBy": "run:final-alert",
      "wasDerivedFrom": [
        "run:final-attributes",
        "run:source-1-score",
        "run:source-2-score",
        "run:admin-centroids"
      ]
    }
  ]
}
```

#### ttl
```ttl
@prefix dcat: <http://www.w3.org/ns/dcat#> .
@prefix dcterms: <http://purl.org/dc/terms/> .
@prefix mom: <https://rss-hydro.lu/ns/mom/> .
@prefix prov: <http://www.w3.org/ns/prov#> .
@prefix pt: <https://w3id.org/ogc/ospd/activity-type/> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix run: <https://example.org/mom/run/2026030200/> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

run:aggregation a prov:Activity ;
    rdfs:label "GFMS per-watershed aggregation" ;
    dcterms:isPartOf run:workflow-run ;
    dcterms:type pt:ZonalStatistics ;
    prov:endedAtTime "2026-03-02T01:05:41+00:00"^^xsd:dateTime ;
    prov:generated run:gfms-aggregates ;
    prov:startedAtTime "2026-03-02T01:05:33+00:00"^^xsd:dateTime ;
    prov:type pt:ZonalStatistics ;
    prov:used run:aggregation-parameters,
        run:gfms-bin,
        run:watersheds ;
    prov:wasAssociatedWith run:mom,
        run:rss-hydro,
        run:server .

run:aggregation-parameters a prov:Entity ;
    rdfs:label "GFMS per-watershed aggregation parameters" ;
    dcterms:hasVersion "0.0.1-alpha" ;
    dcterms:isPartOf run:mom ;
    prov:type prov:Entity ;
    mom:gfmsDurationAreaThresholdKm2 50 ;
    mom:gfmsMinFileSizeBytes 1000000 .

run:attributes-clean a prov:Entity ;
    rdfs:label "GFMS_MoM/Attributes_Clean_20260302.csv" ;
    dcterms:format "text/csv" ;
    prov:generatedAtTime "2026-03-02T01:12:47+00:00"^^xsd:dateTime ;
    prov:type prov:Entity ;
    prov:wasDerivedFrom run:final-attributes ;
    prov:wasGeneratedBy run:hazard .

run:ecmwf a prov:Agent ;
    rdfs:label "ECMWF / CEMS (GloFAS)" ;
    prov:type prov:Organization .

run:final-alert a prov:Activity ;
    rdfs:label "Final alert" ;
    dcterms:isPartOf run:workflow-run ;
    dcterms:type pt:ScoringAndProgressTracking ;
    prov:endedAtTime "2026-03-02T01:12:52+00:00"^^xsd:dateTime ;
    prov:generated run:final-alert-output ;
    prov:startedAtTime "2026-03-02T01:12:48+00:00"^^xsd:dateTime ;
    prov:type pt:ScoringAndProgressTracking ;
    prov:used run:admin-centroids,
        run:final-attributes,
        run:source-1-score,
        run:source-2-score ;
    prov:wasAssociatedWith run:mom,
        run:rss-hydro,
        run:server .

run:final-alert-output a prov:Entity ;
    rdfs:label "Final_Alert/Final_Alert_2026030200.csv" ;
    dcterms:format "text/csv" ;
    prov:generatedAtTime "2026-03-02T01:12:52+00:00"^^xsd:dateTime ;
    prov:type prov:Entity ;
    prov:wasDerivedFrom run:admin-centroids,
        run:final-attributes,
        run:source-1-score,
        run:source-2-score ;
    prov:wasGeneratedBy run:final-alert .

run:glofas-txt a prov:Entity ;
    rdfs:label "threspoints_2026030200.txt" ;
    dcterms:format "GloFAS threspoints station table (comma-separated text)" ;
    dcat:downloadURL <https://example.org/glofas/threspoints_2026030200.txt> ;
    prov:generatedAtTime "2026-03-02T00:58:10+00:00"^^xsd:dateTime ;
    prov:type prov:Entity ;
    prov:wasAttributedTo run:ecmwf ;
    mom:dataTime "2026-03-02T00:00:00+00:00"^^xsd:dateTime ;
    mom:dataType "GloFAS" ;
    mom:glofasNodataValue -9999 .

run:hazard-parameters a prov:Entity ;
    rdfs:label "GloFAS + GFMS hazard score accumulation parameters" ;
    dcterms:hasVersion "0.0.1-alpha" ;
    dcterms:isPartOf run:mom ;
    prov:type prov:Entity ;
    mom:gfmsDurationAreaThresholdKm2 50 .

run:source-1-data a prov:Entity ;
    rdfs:label "Source 1 grid, cycle 2026030118" ;
    dcterms:format "GRIB2" ;
    dcat:downloadURL <https://example.org/source-1/2026030118.grb2> ;
    prov:generatedAtTime "2026-03-01T23:47:05+00:00"^^xsd:dateTime ;
    prov:type prov:Entity ;
    prov:wasAttributedTo run:provider-1 ;
    mom:dataTime "2026-03-01T18:00:00+00:00"^^xsd:dateTime ;
    mom:dataType "Source 1" .

run:source-2-data a prov:Entity ;
    rdfs:label "Source 2 grid 20260228" ;
    dcterms:format "GeoTIFF" ;
    dcat:downloadURL <https://example.org/source-2/20260228.tif> ;
    prov:generatedAtTime "2026-03-01T02:10:44+00:00"^^xsd:dateTime ;
    prov:type prov:Entity ;
    prov:wasAttributedTo run:provider-1 ;
    mom:dataTime "2026-02-28T00:00:00+00:00"^^xsd:dateTime ;
    mom:dataType "Source 2" .

run:umd a prov:Agent ;
    rdfs:label "University of Maryland (GFMS)" ;
    prov:type prov:Organization .

run:admin-centroids a prov:Entity ;
    rdfs:label "data/Admin0_1_union_centroid.csv" ;
    dcterms:format "text/csv" ;
    dcterms:hasVersion "0.0.1-alpha" ;
    dcterms:isPartOf run:mom ;
    prov:type prov:Entity .

run:attributes a prov:Entity ;
    rdfs:label "data/Attributes.csv" ;
    dcterms:format "text/csv" ;
    dcterms:hasVersion "0.0.1-alpha" ;
    dcterms:isPartOf run:mom ;
    prov:type prov:Entity .

run:gfms-bin a prov:Entity ;
    rdfs:label "Flood_byStor_2026030200.bin" ;
    dcterms:format "GFMS Flood_byStor binary grid (float32)" ;
    dcat:downloadURL <https://example.org/gfms/Flood_byStor_2026030200.bin> ;
    prov:generatedAtTime "2026-03-02T01:05:32+00:00"^^xsd:dateTime ;
    prov:type prov:Entity ;
    prov:wasAttributedTo run:umd ;
    mom:dataTime "2026-03-02T00:00:00+00:00"^^xsd:dateTime ;
    mom:dataType "GFMS" ;
    mom:gfmsNodataValue -9999 .

run:gfms-summary a prov:Entity ;
    rdfs:label "GFMS_summary/Flood_byStor_2026030200.csv (duration recalculated)" ;
    dcterms:format "text/csv" ;
    prov:generatedAtTime "2026-03-02T01:12:41+00:00"^^xsd:dateTime ;
    prov:type prov:Entity ;
    prov:wasDerivedFrom run:gfms-aggregates,
        run:gfms-summary-prev ;
    prov:wasGeneratedBy run:hazard ;
    mom:dataTime "2026-03-02T00:00:00+00:00"^^xsd:dateTime ;
    mom:dataType "GFMS" .

run:gfms-summary-prev a prov:Entity ;
    rdfs:label "GFMS_summary/Flood_byStor_2026030121.csv" ;
    dcterms:format "text/csv" ;
    prov:generatedAtTime "2026-03-01T01:07:12+00:00"^^xsd:dateTime ;
    prov:type prov:Entity ;
    mom:dataTime "2026-03-01T21:00:00+00:00"^^xsd:dateTime ;
    mom:dataType "GFMS" .

run:glofas-points a prov:Entity ;
    rdfs:label "GLOFAS/threspoints_2026030200.csv" ;
    dcterms:format "text/csv" ;
    prov:generatedAtTime "2026-03-02T00:58:12+00:00"^^xsd:dateTime ;
    prov:type prov:Entity ;
    prov:wasDerivedFrom run:glofas-txt ;
    mom:dataTime "2026-03-02T00:00:00+00:00"^^xsd:dateTime ;
    mom:dataType "GloFAS" ;
    mom:glofasNodataValue -9999 .

run:provider-1 a prov:Agent ;
    rdfs:label "Provider of sources 1 and 2" ;
    prov:type prov:Organization .

run:resilience a prov:Entity ;
    rdfs:label "data/Resilience_Index.csv" ;
    dcterms:format "text/csv" ;
    dcterms:hasVersion "0.0.1-alpha" ;
    dcterms:isPartOf run:mom ;
    prov:type prov:Entity .

run:source-1-score a prov:Entity ;
    rdfs:label "Source 1 hazard scores, cycle 2026030118" ;
    dcterms:format "text/csv" ;
    prov:generatedAtTime "2026-03-02T00:52:19+00:00"^^xsd:dateTime ;
    prov:type mom:HazardScore ;
    prov:wasDerivedFrom run:source-1-data ;
    mom:dataTime "2026-03-01T18:00:00+00:00"^^xsd:dateTime ;
    mom:dataType "Source 1" .

run:source-2-score a prov:Entity ;
    rdfs:label "Source 2 hazard scores 20260228" ;
    dcterms:format "text/csv" ;
    prov:generatedAtTime "2026-03-01T04:12:30+00:00"^^xsd:dateTime ;
    prov:type mom:HazardScore ;
    prov:wasDerivedFrom run:source-2-data ;
    mom:dataTime "2026-02-28T00:00:00+00:00"^^xsd:dateTime ;
    mom:dataType "Source 2" .

run:watersheds a prov:Entity ;
    rdfs:label "Watershed_pfaf_id.shp" ;
    dcterms:format "ESRI Shapefile" ;
    dcterms:hasVersion "0.0.0" ;
    prov:generatedAtTime "2026-01-15T00:00:00+00:00"^^xsd:dateTime ;
    prov:type prov:Entity ;
    mom:watershedFingerprint "a09161ac707ef1d0355e92e730c8fe31e127149b803321bc988b3232058eea17" .

run:weights a prov:Entity ;
    rdfs:label "data/GFMS_Weightage.csv" ;
    dcterms:format "text/csv" ;
    dcterms:hasVersion "0.0.1-alpha" ;
    dcterms:isPartOf run:mom ;
    prov:type prov:Entity .

run:gfms-aggregates a prov:Entity ;
    rdfs:label "Processing/gfms/Flood_byStor_2026030200.csv (per-watershed aggregates, duration not yet recalculated)" ;
    dcterms:format "text/csv" ;
    prov:generatedAtTime "2026-03-02T01:05:41+00:00"^^xsd:dateTime ;
    prov:type prov:Entity ;
    prov:wasDerivedFrom run:gfms-bin,
        run:watersheds ;
    prov:wasGeneratedBy run:aggregation ;
    mom:dataTime "2026-03-02T00:00:00+00:00"^^xsd:dateTime ;
    mom:dataType "GFMS" .

run:hazard a prov:Activity ;
    rdfs:label "GloFAS + GFMS hazard score accumulation" ;
    dcterms:isPartOf run:workflow-run ;
    dcterms:type pt:WeightedScoringAndClassification ;
    prov:endedAtTime "2026-03-02T01:12:47+00:00"^^xsd:dateTime ;
    prov:generated run:attributes-clean,
        run:final-attributes,
        run:gfms-summary ;
    prov:startedAtTime "2026-03-02T01:12:40+00:00"^^xsd:dateTime ;
    prov:type pt:WeightedScoringAndClassification ;
    prov:used run:attributes,
        run:gfms-aggregates,
        run:gfms-summary-prev,
        run:glofas-points,
        run:hazard-parameters,
        run:resilience,
        run:weights ;
    prov:wasAssociatedWith run:mom,
        run:rss-hydro,
        run:server .

run:workflow-run a prov:Activity ;
    rdfs:label "MoM workflow run, 2026-03-02 00:00" ;
    prov:endedAtTime "2026-03-02T01:12:52+00:00"^^xsd:dateTime ;
    prov:startedAtTime "2026-03-02T01:05:33+00:00"^^xsd:dateTime ;
    prov:type pt:workflow ;
    prov:wasAssociatedWith run:mom,
        run:rss-hydro,
        run:server .

run:final-attributes a prov:Entity ;
    rdfs:label "GFMS_MoM/Final_Attributes_20260302.csv" ;
    dcterms:format "text/csv" ;
    prov:generatedAtTime "2026-03-02T01:12:47+00:00"^^xsd:dateTime ;
    prov:type mom:HazardScore ;
    prov:wasDerivedFrom run:attributes,
        run:gfms-summary,
        run:glofas-points,
        run:resilience,
        run:weights ;
    prov:wasGeneratedBy run:hazard ;
    mom:dataTime "2026-03-02T00:00:00+00:00"^^xsd:dateTime ;
    mom:dataType "GFMS",
        "GloFAS" .

run:rss-hydro a prov:Agent ;
    rdfs:label "RSS-Hydro" ;
    prov:type prov:Organization .

run:server a prov:Agent ;
    rdfs:label "mom-prod-01 (illustrative server)" ;
    prov:type prov:Agent .

run:mom a prov:Agent ;
    rdfs:label "MoMProduction" ;
    dcterms:hasVersion "0.0.1-alpha" ;
    prov:type prov:SoftwareAgent .


```

## Schema

```yaml
$schema: https://json-schema.org/draft/2020-12/schema
description: 'Provenance chain of one MoM run: per-watershed aggregation, hazard score
  accumulation and final alert, each always present.'
allOf:
- $ref: https://ogcincubator.github.io/bblock-prov-schema/build/annotated/ogc-utils/prov/schema.yaml
contains:
  $ref: '#/$defs/isProcessingActivity'
minContains: 3
items:
  allOf:
  - if:
      $ref: '#/$defs/isProcessingActivity'
    then:
      allOf:
      - $ref: https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/rss-hydro/ontology/activities/schema.yaml
      - required:
        - dcterms:isPartOf
  - if:
      required:
      - activityType
      properties:
        activityType:
          const: https://w3id.org/ogc/ospd/activity-type/workflow
    then:
      required:
      - id
      - name
      - startedAtTime
      - endedAtTime
      - wasAssociatedWith
  - if:
      required:
      - entityType
    then:
      $ref: https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/rss-hydro/processing-activity/schema.yaml#/$defs/datedOrVersioned
  - $ref: https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/rss-hydro/processing-activity/schema.yaml#/$defs/softwareVersioned
  - if:
      $ref: '#/$defs/isHazardScore'
    then:
      required:
      - mom:dataType
      - mom:dataTime
      - generatedAtTime
      - wasDerivedFrom
  - if:
      required:
      - mom:dataType
    then:
      required:
      - dcterms:format
      anyOf:
      - required:
        - dcterms:hasVersion
      - required:
        - generatedAtTime
        - mom:dataTime
$defs:
  isProcessingActivity:
    $ref: https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/rss-hydro/ontology/activities/schema.yaml#/$defs/isMomActivity
  isHazardScore:
    required:
    - entityType
    properties:
      entityType:
        const: mom:HazardScore
x-jsonld-extra-terms:
  mom:dataTime:
    x-jsonld-type: http://www.w3.org/2001/XMLSchema#dateTime
  dcat:downloadURL:
    x-jsonld-type: '@id'
  dcterms:isPartOf:
    x-jsonld-type: '@id'
x-jsonld-prefixes:
  xsd: http://www.w3.org/2001/XMLSchema#
  mom: https://rss-hydro.lu/ns/mom/
  dcat: http://www.w3.org/ns/dcat#
  dcterms: http://purl.org/dc/terms/
x-bblocks-metadata:
  itemIdentifier: ogc.osc.rss-hydro.workflow.model-of-models
  register: https://ogcincubator.github.io/bblocks-openscience/build/register.json
  version: '0.1'
  dateOfLastChange: '2026-10-14'

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/rss-hydro/workflow/model-of-models/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/rss-hydro/workflow/model-of-models/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "wasInfluencedBy": {
      "@context": {
        "href": {
          "@type": "@id",
          "@id": "oa:hasTarget"
        },
        "rel": {
          "@context": {
            "@base": "http://www.iana.org/assignments/relation/"
          },
          "@id": "http://www.iana.org/assignments/relation",
          "@type": "@id"
        },
        "type": "dct:type",
        "hreflang": "dct:language",
        "title": "rdfs:label",
        "length": "dct:extent"
      },
      "@id": "prov:wasInfluencedBy",
      "@type": "@id"
    },
    "qualifiedInfluence": {
      "@context": {
        "influencer": {
          "@context": {
            "href": {
              "@type": "@id",
              "@id": "oa:hasTarget"
            },
            "rel": {
              "@context": {
                "@base": "http://www.iana.org/assignments/relation/"
              },
              "@id": "http://www.iana.org/assignments/relation",
              "@type": "@id"
            },
            "type": "dct:type",
            "hreflang": "dct:language",
            "title": "rdfs:label",
            "length": "dct:extent"
          },
          "@id": "prov:influencer",
          "@type": "@id"
        },
        "agent": {
          "@context": {
            "href": {
              "@type": "@id",
              "@id": "oa:hasTarget"
            },
            "rel": {
              "@context": {
                "@base": "http://www.iana.org/assignments/relation/"
              },
              "@id": "http://www.iana.org/assignments/relation",
              "@type": "@id"
            },
            "type": "dct:type",
            "hreflang": "dct:language",
            "title": "rdfs:label",
            "length": "dct:extent"
          },
          "@id": "prov:agent",
          "@type": "@id"
        }
      },
      "@id": "prov:qualifiedInfluence",
      "@type": "@id"
    },
    "hadMember": {
      "@id": "prov:hadMember",
      "@type": "@id"
    },
    "id": "@id",
    "provType": "@type",
    "entityType": {
      "@id": "prov:type",
      "@type": "@id"
    },
    "name": "rdfs:label",
    "wasGeneratedBy": {
      "@id": "prov:wasGeneratedBy",
      "@type": "@id"
    },
    "wasAttributedTo": {
      "@context": {
        "href": {
          "@type": "@id",
          "@id": "oa:hasTarget"
        },
        "rel": {
          "@context": {
            "@base": "http://www.iana.org/assignments/relation/"
          },
          "@id": "http://www.iana.org/assignments/relation",
          "@type": "@id"
        },
        "type": "dct:type",
        "hreflang": "dct:language",
        "title": "rdfs:label",
        "length": "dct:extent"
      },
      "@id": "prov:wasAttributedTo",
      "@type": "@id"
    },
    "wasDerivedFrom": {
      "@id": "prov:wasDerivedFrom",
      "@type": "@id"
    },
    "alternateOf": {
      "@id": "prov:alternateOf",
      "@type": "@id"
    },
    "hadPrimarySource": {
      "@id": "prov:hadPrimarySource",
      "@type": "@id"
    },
    "specializationOf": {
      "@id": "prov:specializationOf",
      "@type": "@id"
    },
    "wasInvalidatedBy": {
      "@id": "prov:wasInvalidatedBy",
      "@type": "@id"
    },
    "wasQuotedFrom": {
      "@id": "prov:wasQuotedFrom",
      "@type": "@id"
    },
    "wasRevisionOf": {
      "@id": "prov:wasRevisionOf",
      "@type": "@id"
    },
    "atLocation": {
      "@id": "prov:atLocation",
      "@type": "@id"
    },
    "links": {
      "@context": {
        "href": {
          "@type": "@id",
          "@id": "oa:hasTarget"
        },
        "rel": {
          "@context": {
            "@base": "http://www.iana.org/assignments/relation/"
          },
          "@id": "http://www.iana.org/assignments/relation",
          "@type": "@id"
        },
        "type": "dct:type",
        "hreflang": "dct:language",
        "title": "rdfs:label",
        "length": "dct:extent"
      },
      "@id": "rdfs:seeAlso"
    },
    "generatedAtTime": {
      "@id": "prov:generatedAtTime",
      "@type": "xsd:dateTime"
    },
    "invalidatedAtTime": {
      "@id": "prov:invalidatedAtTime",
      "@type": "xsd:dateTime"
    },
    "value": "prov:value",
    "qualifiedPrimarySource": {
      "@id": "prov:qualifiedPrimarySource",
      "@type": "@id"
    },
    "qualifiedQuotation": {
      "@id": "prov:qualifiedQuotation",
      "@type": "@id"
    },
    "qualifiedRevision": {
      "@id": "prov:qualifiedRevision",
      "@type": "@id"
    },
    "qualifiedGeneration": {
      "@id": "prov:qualifiedGeneration",
      "@type": "@id"
    },
    "qualifiedInvalidation": {
      "@id": "prov:qualifiedInvalidation",
      "@type": "@id"
    },
    "qualifiedDerivation": {
      "@id": "prov:qualifiedDerivation",
      "@type": "@id"
    },
    "qualifiedAttribution": {
      "@id": "prov:qualifiedAttribution",
      "@type": "@id"
    },
    "activityType": {
      "@id": "prov:type",
      "@type": "@id"
    },
    "startedAtTime": {
      "@id": "prov:startedAtTime",
      "@type": "xsd:dateTime"
    },
    "endedAtTime": {
      "@id": "prov:endedAtTime",
      "@type": "xsd:dateTime"
    },
    "wasAssociatedWith": {
      "@context": {
        "href": {
          "@type": "@id",
          "@id": "oa:hasTarget"
        },
        "rel": {
          "@context": {
            "@base": "http://www.iana.org/assignments/relation/"
          },
          "@id": "http://www.iana.org/assignments/relation",
          "@type": "@id"
        },
        "type": "dct:type",
        "hreflang": "dct:language",
        "title": "rdfs:label",
        "length": "dct:extent"
      },
      "@id": "prov:wasAssociatedWith",
      "@type": "@id"
    },
    "wasInformedBy": {
      "@id": "prov:wasInformedBy",
      "@type": "@id"
    },
    "used": {
      "@id": "prov:used",
      "@type": "@id"
    },
    "wasStartedBy": {
      "@id": "prov:wasStartedBy",
      "@type": "@id"
    },
    "wasEndedBy": {
      "@id": "prov:wasEndedBy",
      "@type": "@id"
    },
    "invalidated": {
      "@id": "prov:invalidated",
      "@type": "@id"
    },
    "generated": {
      "@id": "prov:generated",
      "@type": "@id"
    },
    "qualifiedUsage": {
      "@id": "prov:qualifiedUsage",
      "@type": "@id"
    },
    "qualifiedCommunication": {
      "@id": "prov:qualifiedCommunication",
      "@type": "@id"
    },
    "qualifiedStart": {
      "@id": "prov:qualifiedStart",
      "@type": "@id"
    },
    "qualifiedEnd": {
      "@id": "prov:qualifiedEnd",
      "@type": "@id"
    },
    "qualifiedAssociation": {
      "@id": "prov:qualifiedAssociation",
      "@type": "@id"
    },
    "agentType": {
      "@id": "prov:type",
      "@type": "@id"
    },
    "actedOnBehalfOf": {
      "@id": "prov:actedOnBehalfOf",
      "@type": "@id"
    },
    "qualifiedDelegation": {
      "@id": "prov:qualifiedDelegation",
      "@type": "@id"
    },
    "Activity": "prov:Activity",
    "ActivityInfluence": "prov:ActivityInfluence",
    "Agent": "prov:Agent",
    "AgentInfluence": "prov:AgentInfluence",
    "Association": "prov:Association",
    "Attribution": "prov:Attribution",
    "Bundle": "prov:Bundle",
    "Collection": "prov:Collection",
    "Communication": "prov:Communication",
    "Delegation": "prov:Delegation",
    "Derivation": "prov:Derivation",
    "EmptyCollection": "prov:EmptyCollection",
    "End": "prov:End",
    "Entity": "prov:Entity",
    "EntityInfluence": "prov:EntityInfluence",
    "Generation": "prov:Generation",
    "Influence": "prov:Influence",
    "InstantaneousEvent": "prov:InstantaneousEvent",
    "Invalidation": "prov:Invalidation",
    "Location": "prov:Location",
    "Organization": "prov:Organization",
    "Person": "prov:Person",
    "Plan": "prov:Plan",
    "PrimarySource": "prov:PrimarySource",
    "Quotation": "prov:Quotation",
    "Revision": "prov:Revision",
    "Role": "prov:Role",
    "SoftwareAgent": "prov:SoftwareAgent",
    "Start": "prov:Start",
    "Usage": "prov:Usage",
    "ServiceDescription": "prov:ServiceDescription",
    "DirectQueryService": "prov:DirectQueryService",
    "Accept": "prov:Accept",
    "Contribute": "prov:Contribute",
    "Contributor": "prov:Contributor",
    "Copyright": "prov:Copyright",
    "Create": "prov:Create",
    "Creator": "prov:Creator",
    "Modify": "prov:Modify",
    "Publish": "prov:Publish",
    "Publisher": "prov:Publisher",
    "Replace": "prov:Replace",
    "RightsAssignment": "prov:RightsAssignment",
    "RightsHolder": "prov:RightsHolder",
    "Submit": "prov:Submit",
    "Dictionary": "prov:Dictionary",
    "EmptyDictionary": "prov:EmptyDictionary",
    "KeyEntityPair": "prov:KeyEntityPair",
    "Insertion": "prov:Insertion",
    "Removal": "prov:Removal",
    "atTime": {
      "@id": "prov:atTime",
      "@type": "xsd:dateTime"
    },
    "provenanceUriTemplate": "prov:provenanceUriTemplate",
    "pairKey": {
      "@id": "prov:pairKey",
      "@type": "rdfs:Literal"
    },
    "removedKey": {
      "@id": "prov:removedKey",
      "@type": "rdfs:Literal"
    },
    "agent": {
      "@id": "prov:agent",
      "@type": "@id"
    },
    "entity": {
      "@id": "prov:entity",
      "@type": "@id"
    },
    "hadActivity": {
      "@id": "prov:hadActivity",
      "@type": "@id"
    },
    "activity": {
      "@id": "prov:activity",
      "@type": "@id"
    },
    "hadGeneration": {
      "@id": "prov:hadGeneration",
      "@type": "@id"
    },
    "hadPlan": {
      "@id": "prov:hadPlan",
      "@type": "@id"
    },
    "hadRole": {
      "@id": "prov:hadRole",
      "@type": "@id"
    },
    "hadUsage": {
      "@id": "prov:hadUsage",
      "@type": "@id"
    },
    "influenced": {
      "@id": "prov:influenced",
      "@type": "@id"
    },
    "influencer": {
      "@id": "prov:influencer",
      "@type": "@id"
    },
    "has_anchor": {
      "@id": "prov:has_anchor",
      "@type": "@id"
    },
    "has_query_service": {
      "@id": "prov:has_query_service",
      "@type": "@id"
    },
    "describesService": {
      "@id": "prov:describesService",
      "@type": "@id"
    },
    "pingback": {
      "@id": "prov:pingback",
      "@type": "@id"
    },
    "dictionary": {
      "@id": "prov:dictionary",
      "@type": "@id"
    },
    "derivedByInsertionFrom": {
      "@id": "prov:derivedByInsertionFrom",
      "@type": "@id"
    },
    "derivedByRemovalFrom": {
      "@id": "prov:derivedByRemovalFrom",
      "@type": "@id"
    },
    "insertedKeyEntityPair": {
      "@id": "prov:insertedKeyEntityPair",
      "@type": "@id"
    },
    "hadDictionaryMember": {
      "@id": "prov:hadDictionaryMember",
      "@type": "@id"
    },
    "pairEntity": {
      "@id": "prov:pairEntity",
      "@type": "@id"
    },
    "qualifiedInsertion": {
      "@id": "prov:qualifiedInsertion",
      "@type": "@id"
    },
    "qualifiedRemoval": {
      "@id": "prov:qualifiedRemoval",
      "@type": "@id"
    },
    "asInBundle": {
      "@id": "prov:asInBundle",
      "@type": "@id"
    },
    "mentionOf": {
      "@id": "prov:mentionOf",
      "@type": "@id"
    },
    "influenceType": {
      "@id": "prov:type",
      "@type": "@id"
    },
    "processType": {
      "@id": "dct:type",
      "@type": "@id"
    },
    "mom:dataTime": {
      "@type": "xsd:dateTime"
    },
    "dcat:downloadURL": {
      "@type": "@id"
    },
    "dcterms:isPartOf": {
      "@type": "@id"
    },
    "prov": "http://www.w3.org/ns/prov#",
    "xsd": "http://www.w3.org/2001/XMLSchema#",
    "rdfs": "http://www.w3.org/2000/01/rdf-schema#",
    "dct": "http://purl.org/dc/terms/",
    "rdf": "http://www.w3.org/1999/02/22-rdf-syntax-ns#",
    "foaf": "http://xmlns.com/foaf/0.1/",
    "schema": "https://schema.org/",
    "wfprov": "http://purl.org/wf4ever/wfprov#",
    "wfdesc": "http://purl.org/wf4ever/wfdesc#",
    "wf4ever": "http://purl.org/wf4ever/wf4ever#",
    "oa": "http://www.w3.org/ns/oa#",
    "mom": "https://rss-hydro.lu/ns/mom/",
    "dcat": "http://www.w3.org/ns/dcat#",
    "dcterms": "http://purl.org/dc/terms/",
    "pt": "https://w3id.org/ogc/ospd/activity-type/",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/rss-hydro/workflow/model-of-models/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-openscience](https://github.com/ogcincubator/bblocks-openscience)
* Path: `_sources/rss-hydro/workflow/model-of-models`

