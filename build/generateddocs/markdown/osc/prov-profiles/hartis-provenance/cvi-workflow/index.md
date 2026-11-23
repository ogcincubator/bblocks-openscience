
# HARTIS CVI Workflow Provenance (Schema)

`ogc.osc.prov-profiles.hartis-provenance.cvi-workflow` *v0.1.0*

A provenance profile for the complete HARTIS Coastal Vulnerability Index workflow, from configuration and source data through coastline extraction, transect generation, indicator calculations and the final CVI result.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

# HARTIS CVI Workflow Provenance

This candidate Building Block describes provenance for the complete HARTIS
Coastal Vulnerability Index workflow. It is deliberately workflow-specific:
the profile connects the workflow definition and planned processing steps to
the runtime activities and their input and output entities.

The candidate covers the following chain:

1. configuration and source data preparation;
2. coastline extraction;
3. transect generation;
4. land-cover, slope, erosion and elevation calculations; and
5. final CVI calculation and GeoJSON result generation.

The profile is developed locally in the HARTIS repository first. It is not an
official OGC Register entry or a mature shared Building Block until reviewed
and accepted through the relevant OGC contribution process.

## Relationship to shared provenance

The candidate is intended to align with the common OGC PROV Building Block and
the shared processing-step profile. Its additional value is the explicit
representation of the complete CVI workflow, including design-time plans,
runtime activities, data entities and the links between them.

### Conformance to the Workflow Provenance Graph profile

This block profiles the [Workflow Provenance Graph](bblock://ogc.osc.prov-profiles.workflow-graph)
in its bundle form, so every activity in the bundle, including `runtime` and each of
`runtime.activities`, must be a
[Registered Processing Step](bblock://ogc.osc.prov-profiles.processing-step).
Every node states its PROV class in `provType` (`Entity` or `Activity`); the specific
types are IRIs or CURIEs in `entityType` (`prov:Bundle`, `prov:Plan`, `ospd:VectorDataset`)
or `activityType`. Each runtime activity carries its process type in `activityType`;
the design-time `plans` keep theirs in `processType` (`dct:type`).
Each node references its PROV building block (the bundle, workflow definition, plans and
entities are PROV entities; `runtime` is a PROV activity; each step is a Registered Processing
Step), so identifiers, `provType`, `entityType`/`activityType` and all PROV relations, together
with their JSON-LD mappings, are inherited. This block's schema and `context.jsonld` hold only
what HARTIS adds:

- the `ospd` and `hartis` prefixes;
- `processType` (`dct:type`) on plans;
- `workflowDefinition` and `plan` (`hartis:workflowDefinition`, `hartis:plan`), linking the
  bundle and run to the workflow plan, and each step to its design-time plan;
- `activities` (`dct:hasPart`), the steps of the run;
- `plans`, `runtime` and `entities` as `@included`, so the nested nodes are part of the graph.

The workflow definition is typed `acttype:WorkflowPlan` and `runtime` is typed `acttype:WorkflowRun`,
from the [activity type register profile](https://w3id.org/ogc/rim/activity-type/).
The workflow run reports its own inputs and output by reference only: it uses the inputs of
each step that no other step generated, and generates the output of the last step.
The example conforms to the JSON schema and the SHACL shapes.

## Examples

### HARTIS full CVI workflow provenance candidate
A complete design-time and runtime provenance representation for the HARTIS CVI workflow, including plans, activities, inputs and outputs.
#### json
```json
{
  "id": "hartis:cvi-run-example-001",
  "provType": "Entity",
  "entityType": "prov:Bundle",
  "label": "HARTIS CVI workflow design-time and runtime provenance skeleton",
  "status": "illustrative-candidate",
  "workflowDefinition": {
    "id": "hartis:cvi-workflow",
    "provType": "Entity",
    "entityType": [
      "prov:Plan",
      "ospd:WorkflowDefinition",
      "acttype:WorkflowPlan"
    ],
    "label": "HARTIS Coastal Vulnerability Index workflow",
    "sourceWorkflow": "cvi_workflow.cwl",
    "executionImage": "ghcr.io/hartis-org/cvi-workflow:latest"
  },
  "plans": [
    {
      "id": "hartis:cvi-workflow/step/setup-env",
      "provType": "Entity",
      "entityType": ["prov:Plan", "ospd:ProcessingStep"],
      "label": "Validate CVI configuration and initialize output workspace",
      "processType": "https://example.org/ospd/process-types/configuration-validation",
      "sourceCode": "steps/setup_env.py"
    },
    {
      "id": "hartis:cvi-workflow/step/extract-coastline",
      "provType": "Entity",
      "entityType": ["prov:Plan", "ospd:ProcessingStep"],
      "label": "Extract coastline geometry for selected AOI",
      "processType": "https://example.org/ospd/process-types/coastline-extraction",
      "sourceCode": "steps/extract_coastline.py"
    },
    {
      "id": "hartis:cvi-workflow/step/generate-transects",
      "provType": "Entity",
      "entityType": ["prov:Plan", "ospd:ProcessingStep"],
      "label": "Generate cross-shore transects from coastline",
      "processType": "https://example.org/ospd/process-types/transect-generation",
      "sourceCode": "steps/generate_transects.py"
    },
    {
      "id": "hartis:cvi-workflow/step/compute-landcover",
      "provType": "Entity",
      "entityType": ["prov:Plan", "ospd:ProcessingStep"],
      "label": "Compute land-cover vulnerability score per transect",
      "processType": "https://example.org/ospd/process-types/land-cover-analysis",
      "sourceCode": "steps/compute_landcover.py"
    },
    {
      "id": "hartis:cvi-workflow/step/compute-slope",
      "provType": "Entity",
      "entityType": ["prov:Plan", "ospd:ProcessingStep"],
      "label": "Compute slope vulnerability score per transect",
      "processType": "https://example.org/ospd/process-types/slope-derivation",
      "sourceCode": "steps/compute_slope.py"
    },
    {
      "id": "hartis:cvi-workflow/step/compute-erosion",
      "provType": "Entity",
      "entityType": ["prov:Plan", "ospd:ProcessingStep"],
      "label": "Compute erosion vulnerability score per transect",
      "processType": "https://example.org/ospd/process-types/erosion-data-integration",
      "sourceCode": "steps/compute_erosion.py"
    },
    {
      "id": "hartis:cvi-workflow/step/compute-elevation",
      "provType": "Entity",
      "entityType": ["prov:Plan", "ospd:ProcessingStep"],
      "label": "Compute coastal elevation vulnerability score per transect",
      "processType": "https://example.org/ospd/process-types/elevation-analysis",
      "sourceCode": "steps/compute_elevation.py"
    },
    {
      "id": "hartis:cvi-workflow/step/compute-cvi",
      "provType": "Entity",
      "entityType": ["prov:Plan", "ospd:ProcessingStep"],
      "label": "Compute final Coastal Vulnerability Index classification",
      "processType": "https://example.org/ospd/process-types/vulnerability-index-scoring",
      "sourceCode": "steps/compute_cvi.py"
    }
  ],
  "runtime": {
    "id": "hartis:cvi-run-example-001/runtime",
    "provType": "Activity",
    "activityType": "acttype:WorkflowRun",
    "label": "Illustrative CVI workflow execution",
    "workflowDefinition": "hartis:cvi-workflow",
    "used": [
      "hartis:cvi-run-example-001/entity/cvi-scoring-config",
      "hartis:cvi-run-example-001/entity/med-coastal-aois",
      "hartis:cvi-run-example-001/entity/nominatim-response",
      "hartis:cvi-run-example-001/entity/overpass-coastline-response",
      "hartis:cvi-run-example-001/entity/esa-worldcover-2021",
      "hartis:cvi-run-example-001/entity/copernicus-dem",
      "hartis:cvi-run-example-001/entity/deltares-chw-erosion-wfs"
    ],
    "generated": "hartis:cvi-run-example-001/entity/transects-with-cvi-equal",
    "wasAssociatedWith": [
      "hartis:cvi-workflow/container/cvi-workflow-latest"
    ],
    "activities": [
      {
        "id": "hartis:cvi-run-example-001/activity/setup-env",
        "provType": "Activity",
        "activityType": "https://example.org/ospd/process-types/configuration-validation",
        "plan": "hartis:cvi-workflow/step/setup-env",
        "used": ["hartis:cvi-run-example-001/entity/cvi-scoring-config"],
        "generated": ["hartis:cvi-run-example-001/entity/validated-config"],
        "qualifiedUsage": [{
          "entity": "hartis:cvi-run-example-001/entity/cvi-scoring-config",
          "hadRole": "hartis:role/workflowConfiguration"
        }],
        "wasAssociatedWith": [
          "hartis:cvi-workflow/software/setup-env-py",
          "hartis:cvi-workflow/container/cvi-workflow-latest"
        ],
        "parameters": {"outputDirectory": "output_data", "expectedConfigKeys": ["weights"]}
      },
      {
        "id": "hartis:cvi-run-example-001/activity/extract-coastline",
        "provType": "Activity",
        "activityType": "https://example.org/ospd/process-types/coastline-extraction",
        "plan": "hartis:cvi-workflow/step/extract-coastline",
        "used": [
          "hartis:cvi-run-example-001/entity/med-coastal-aois",
          "hartis:cvi-run-example-001/entity/nominatim-response",
          "hartis:cvi-run-example-001/entity/overpass-coastline-response"
        ],
        "generated": ["hartis:cvi-run-example-001/entity/coastline-gpkg"],
        "qualifiedUsage": [
          {"entity": "hartis:cvi-run-example-001/entity/med-coastal-aois", "hadRole": "hartis:role/aoiCandidateSource"},
          {"entity": "hartis:cvi-run-example-001/entity/nominatim-response", "hadRole": "hartis:role/aoiGeocodingResponse"},
          {"entity": "hartis:cvi-run-example-001/entity/overpass-coastline-response", "hadRole": "hartis:role/sourceCoastlineFeatures"}
        ],
        "wasAssociatedWith": [
          "hartis:cvi-workflow/software/extract-coastline-py",
          "hartis:cvi-workflow/container/cvi-workflow-latest"
        ],
        "wasInformedBy": ["hartis:cvi-run-example-001/activity/setup-env"],
        "parameters": {
          "osmFilter": "natural=coastline",
          "maxAoiAttempts": 5,
          "outputFormat": "GeoPackage"
        }
      },
      {
        "id": "hartis:cvi-run-example-001/activity/generate-transects",
        "provType": "Activity",
        "activityType": "https://example.org/ospd/process-types/transect-generation",
        "plan": "hartis:cvi-workflow/step/generate-transects",
        "used": ["hartis:cvi-run-example-001/entity/coastline-gpkg"],
        "generated": ["hartis:cvi-run-example-001/entity/transects-geojson"],
        "qualifiedUsage": [{
          "entity": "hartis:cvi-run-example-001/entity/coastline-gpkg",
          "hadRole": "hartis:role/sourceCoastline"
        }],
        "wasAssociatedWith": [
          "hartis:cvi-workflow/software/generate-transects-py",
          "hartis:cvi-workflow/container/cvi-workflow-latest"
        ],
        "wasInformedBy": ["hartis:cvi-run-example-001/activity/extract-coastline"],
        "parameters": {
          "spacingMeters": 50,
          "transectLengthMeters": 400,
          "maxProcessedCoastlineMeters": 15000,
          "processingCrs": "EPSG:3857",
          "outputCrs": "EPSG:4326"
        }
      },
      {
        "id": "hartis:cvi-run-example-001/activity/compute-landcover",
        "provType": "Activity",
        "activityType": "https://example.org/ospd/process-types/land-cover-analysis",
        "plan": "hartis:cvi-workflow/step/compute-landcover",
        "used": [
          "hartis:cvi-run-example-001/entity/transects-geojson",
          "hartis:cvi-run-example-001/entity/validated-config",
          "hartis:cvi-run-example-001/entity/esa-worldcover-2021"
        ],
        "generated": ["hartis:cvi-run-example-001/entity/transects-with-land-cover"],
        "qualifiedUsage": [
          {"entity": "hartis:cvi-run-example-001/entity/transects-geojson", "hadRole": "hartis:role/analysisUnits"},
          {"entity": "hartis:cvi-run-example-001/entity/validated-config", "hadRole": "hartis:role/classificationConfiguration"},
          {"entity": "hartis:cvi-run-example-001/entity/esa-worldcover-2021", "hadRole": "hartis:role/sourceLandCoverRaster"}
        ],
        "wasAssociatedWith": [
          "hartis:cvi-workflow/software/compute-landcover-py",
          "hartis:cvi-workflow/container/cvi-workflow-latest"
        ],
        "wasInformedBy": ["hartis:cvi-run-example-001/activity/generate-transects"],
        "parameters": {"derivedMeasure": "dominant land-cover class and CVI score"}
      },
      {
        "id": "hartis:cvi-run-example-001/activity/compute-slope",
        "provType": "Activity",
        "activityType": "https://example.org/ospd/process-types/slope-derivation",
        "plan": "hartis:cvi-workflow/step/compute-slope",
        "used": [
          "hartis:cvi-run-example-001/entity/transects-geojson",
          "hartis:cvi-run-example-001/entity/validated-config",
          "hartis:cvi-run-example-001/entity/copernicus-dem"
        ],
        "generated": ["hartis:cvi-run-example-001/entity/transects-with-slope"],
        "qualifiedUsage": [
          {"entity": "hartis:cvi-run-example-001/entity/transects-geojson", "hadRole": "hartis:role/analysisUnits"},
          {"entity": "hartis:cvi-run-example-001/entity/validated-config", "hadRole": "hartis:role/classificationConfiguration"},
          {"entity": "hartis:cvi-run-example-001/entity/copernicus-dem", "hadRole": "hartis:role/sourceElevationRaster"}
        ],
        "wasAssociatedWith": [
          "hartis:cvi-workflow/software/compute-slope-py",
          "hartis:cvi-workflow/container/cvi-workflow-latest"
        ],
        "wasInformedBy": ["hartis:cvi-run-example-001/activity/generate-transects"],
        "parameters": {"processingCrs": "EPSG:3035", "derivedMeasure": "slope percent"}
      },
      {
        "id": "hartis:cvi-run-example-001/activity/compute-erosion",
        "provType": "Activity",
        "activityType": "https://example.org/ospd/process-types/erosion-data-integration",
        "plan": "hartis:cvi-workflow/step/compute-erosion",
        "used": [
          "hartis:cvi-run-example-001/entity/transects-geojson",
          "hartis:cvi-run-example-001/entity/validated-config",
          "hartis:cvi-run-example-001/entity/deltares-chw-erosion-wfs"
        ],
        "generated": ["hartis:cvi-run-example-001/entity/transects-with-erosion"],
        "qualifiedUsage": [
          {"entity": "hartis:cvi-run-example-001/entity/transects-geojson", "hadRole": "hartis:role/analysisUnits"},
          {"entity": "hartis:cvi-run-example-001/entity/validated-config", "hadRole": "hartis:role/classificationConfiguration"},
          {"entity": "hartis:cvi-run-example-001/entity/deltares-chw-erosion-wfs", "hadRole": "hartis:role/sourceErosionClasses"}
        ],
        "wasAssociatedWith": [
          "hartis:cvi-workflow/software/compute-erosion-py",
          "hartis:cvi-workflow/container/cvi-workflow-latest"
        ],
        "wasInformedBy": ["hartis:cvi-run-example-001/activity/generate-transects"],
        "parameters": {"derivedMeasure": "erosion class and CVI score", "rescale": {"1": 1, "2": 3, "3": 5}}
      },
      {
        "id": "hartis:cvi-run-example-001/activity/compute-elevation",
        "provType": "Activity",
        "activityType": "https://example.org/ospd/process-types/elevation-analysis",
        "plan": "hartis:cvi-workflow/step/compute-elevation",
        "used": [
          "hartis:cvi-run-example-001/entity/transects-geojson",
          "hartis:cvi-run-example-001/entity/validated-config",
          "hartis:cvi-run-example-001/entity/copernicus-dem"
        ],
        "generated": ["hartis:cvi-run-example-001/entity/transects-with-elevation"],
        "qualifiedUsage": [
          {"entity": "hartis:cvi-run-example-001/entity/transects-geojson", "hadRole": "hartis:role/analysisUnits"},
          {"entity": "hartis:cvi-run-example-001/entity/validated-config", "hadRole": "hartis:role/classificationConfiguration"},
          {"entity": "hartis:cvi-run-example-001/entity/copernicus-dem", "hadRole": "hartis:role/sourceElevationRaster"}
        ],
        "wasAssociatedWith": [
          "hartis:cvi-workflow/software/compute-elevation-py",
          "hartis:cvi-workflow/container/cvi-workflow-latest"
        ],
        "wasInformedBy": ["hartis:cvi-run-example-001/activity/generate-transects"],
        "parameters": {"derivedMeasure": "maximum elevation per transect"}
      },
      {
        "id": "hartis:cvi-run-example-001/activity/compute-cvi",
        "provType": "Activity",
        "activityType": "https://example.org/ospd/process-types/vulnerability-index-scoring",
        "plan": "hartis:cvi-workflow/step/compute-cvi",
        "used": [
          "hartis:cvi-run-example-001/entity/transects-with-land-cover",
          "hartis:cvi-run-example-001/entity/transects-with-slope",
          "hartis:cvi-run-example-001/entity/transects-with-erosion",
          "hartis:cvi-run-example-001/entity/transects-with-elevation",
          "hartis:cvi-run-example-001/entity/validated-config"
        ],
        "generated": ["hartis:cvi-run-example-001/entity/transects-with-cvi-equal"],
        "qualifiedUsage": [
          {"entity": "hartis:cvi-run-example-001/entity/transects-with-land-cover", "hadRole": "hartis:role/landCoverScore"},
          {"entity": "hartis:cvi-run-example-001/entity/transects-with-slope", "hadRole": "hartis:role/slopeScore"},
          {"entity": "hartis:cvi-run-example-001/entity/transects-with-erosion", "hadRole": "hartis:role/erosionScore"},
          {"entity": "hartis:cvi-run-example-001/entity/transects-with-elevation", "hadRole": "hartis:role/elevationScore"},
          {"entity": "hartis:cvi-run-example-001/entity/validated-config", "hadRole": "hartis:role/classificationConfiguration"}
        ],
        "wasAssociatedWith": [
          "hartis:cvi-workflow/software/compute-cvi-py",
          "hartis:cvi-workflow/container/cvi-workflow-latest"
        ],
        "wasInformedBy": [
          "hartis:cvi-run-example-001/activity/compute-landcover",
          "hartis:cvi-run-example-001/activity/compute-slope",
          "hartis:cvi-run-example-001/activity/compute-erosion",
          "hartis:cvi-run-example-001/activity/compute-elevation"
        ],
        "parameters": {
          "indexMethod": "equal geometric CVI",
          "formula": "sqrt(product(scores) / number_of_scores)"
        }
      }
    ]
  },
  "entities": [
    {"id": "hartis:cvi-run-example-001/entity/cvi-scoring-config", "provType": "Entity", "label": "CVI scoring configuration", "path": "config/cvi_scoring_simple.json"},
    {"id": "hartis:cvi-run-example-001/entity/validated-config", "provType": "Entity", "label": "Validated CVI configuration", "path": "output_data/config_validated.json", "wasGeneratedBy": "hartis:cvi-run-example-001/activity/setup-env"},
    {"id": "hartis:cvi-run-example-001/entity/med-coastal-aois", "provType": "Entity", "label": "Mediterranean coastal AOI candidates", "format": "text/csv", "path": "input_data/med_coastal_aois.csv"},
    {"id": "hartis:cvi-run-example-001/entity/nominatim-response", "provType": "Entity", "label": "Nominatim AOI geocoding response", "source": "OpenStreetMap Nominatim"},
    {"id": "hartis:cvi-run-example-001/entity/overpass-coastline-response", "provType": "Entity", "label": "Overpass coastline feature response", "source": "OpenStreetMap Overpass API"},
    {"id": "hartis:cvi-run-example-001/entity/coastline-gpkg", "provType": "Entity", "entityType": "ospd:VectorDataset", "label": "Extracted coastline geometry", "format": "application/geopackage+sqlite3", "path": "output_data/coastline.gpkg", "wasGeneratedBy": "hartis:cvi-run-example-001/activity/extract-coastline"},
    {"id": "hartis:cvi-run-example-001/entity/transects-geojson", "provType": "Entity", "entityType": "ospd:VectorDataset", "label": "Generated CVI transects", "format": "application/geo+json", "path": "output_data/transects.geojson", "wasGeneratedBy": "hartis:cvi-run-example-001/activity/generate-transects"},
    {"id": "hartis:cvi-run-example-001/entity/esa-worldcover-2021", "provType": "Entity", "label": "ESA WorldCover 2021 source", "source": "Copernicus Dataspace"},
    {"id": "hartis:cvi-run-example-001/entity/copernicus-dem", "provType": "Entity", "label": "Copernicus DEM source", "source": "Copernicus Dataspace"},
    {"id": "hartis:cvi-run-example-001/entity/deltares-chw-erosion-wfs", "provType": "Entity", "label": "Deltares Coastal Hazard Wheel erosion response", "source": "Deltares WFS"},
    {"id": "hartis:cvi-run-example-001/entity/transects-with-land-cover", "provType": "Entity", "entityType": "ospd:VectorDataset", "label": "Transects with land-cover scores", "path": "output_data/transects_with_land_cover.geojson", "wasGeneratedBy": "hartis:cvi-run-example-001/activity/compute-landcover"},
    {"id": "hartis:cvi-run-example-001/entity/transects-with-slope", "provType": "Entity", "entityType": "ospd:VectorDataset", "label": "Transects with slope scores", "path": "output_data/transects_with_slope.geojson", "wasGeneratedBy": "hartis:cvi-run-example-001/activity/compute-slope"},
    {"id": "hartis:cvi-run-example-001/entity/transects-with-erosion", "provType": "Entity", "entityType": "ospd:VectorDataset", "label": "Transects with erosion scores", "path": "output_data/transects_with_erosion.geojson", "wasGeneratedBy": "hartis:cvi-run-example-001/activity/compute-erosion"},
    {"id": "hartis:cvi-run-example-001/entity/transects-with-elevation", "provType": "Entity", "entityType": "ospd:VectorDataset", "label": "Transects with elevation scores", "path": "output_data/transects_with_elevation.geojson", "wasGeneratedBy": "hartis:cvi-run-example-001/activity/compute-elevation"},
    {"id": "hartis:cvi-run-example-001/entity/transects-with-cvi-equal", "provType": "Entity", "entityType": "ospd:VectorDataset", "label": "Final CVI classification", "path": "output_data/transects_with_cvi_equal.geojson", "wasGeneratedBy": "hartis:cvi-run-example-001/activity/compute-cvi"}
  ],
  "notes": [
    "This is a normalized HARTIS workflow skeleton, not a final OSPD serialization.",
    "The runtime activities are linked to design-time plans through plan identifiers.",
    "External data sources are represented as entities; the exact representation of service calls remains open.",
    "All processType URIs are provisional and are not official Register identifiers.",
    "Credentials are intentionally not represented as values."
  ]
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/prov-profiles/hartis-provenance/cvi-workflow/context.jsonld",
  "id": "hartis:cvi-run-example-001",
  "provType": "Entity",
  "entityType": "prov:Bundle",
  "label": "HARTIS CVI workflow design-time and runtime provenance skeleton",
  "status": "illustrative-candidate",
  "workflowDefinition": {
    "id": "hartis:cvi-workflow",
    "provType": "Entity",
    "entityType": [
      "prov:Plan",
      "ospd:WorkflowDefinition",
      "acttype:WorkflowPlan"
    ],
    "label": "HARTIS Coastal Vulnerability Index workflow",
    "sourceWorkflow": "cvi_workflow.cwl",
    "executionImage": "ghcr.io/hartis-org/cvi-workflow:latest"
  },
  "plans": [
    {
      "id": "hartis:cvi-workflow/step/setup-env",
      "provType": "Entity",
      "entityType": [
        "prov:Plan",
        "ospd:ProcessingStep"
      ],
      "label": "Validate CVI configuration and initialize output workspace",
      "processType": "https://example.org/ospd/process-types/configuration-validation",
      "sourceCode": "steps/setup_env.py"
    },
    {
      "id": "hartis:cvi-workflow/step/extract-coastline",
      "provType": "Entity",
      "entityType": [
        "prov:Plan",
        "ospd:ProcessingStep"
      ],
      "label": "Extract coastline geometry for selected AOI",
      "processType": "https://example.org/ospd/process-types/coastline-extraction",
      "sourceCode": "steps/extract_coastline.py"
    },
    {
      "id": "hartis:cvi-workflow/step/generate-transects",
      "provType": "Entity",
      "entityType": [
        "prov:Plan",
        "ospd:ProcessingStep"
      ],
      "label": "Generate cross-shore transects from coastline",
      "processType": "https://example.org/ospd/process-types/transect-generation",
      "sourceCode": "steps/generate_transects.py"
    },
    {
      "id": "hartis:cvi-workflow/step/compute-landcover",
      "provType": "Entity",
      "entityType": [
        "prov:Plan",
        "ospd:ProcessingStep"
      ],
      "label": "Compute land-cover vulnerability score per transect",
      "processType": "https://example.org/ospd/process-types/land-cover-analysis",
      "sourceCode": "steps/compute_landcover.py"
    },
    {
      "id": "hartis:cvi-workflow/step/compute-slope",
      "provType": "Entity",
      "entityType": [
        "prov:Plan",
        "ospd:ProcessingStep"
      ],
      "label": "Compute slope vulnerability score per transect",
      "processType": "https://example.org/ospd/process-types/slope-derivation",
      "sourceCode": "steps/compute_slope.py"
    },
    {
      "id": "hartis:cvi-workflow/step/compute-erosion",
      "provType": "Entity",
      "entityType": [
        "prov:Plan",
        "ospd:ProcessingStep"
      ],
      "label": "Compute erosion vulnerability score per transect",
      "processType": "https://example.org/ospd/process-types/erosion-data-integration",
      "sourceCode": "steps/compute_erosion.py"
    },
    {
      "id": "hartis:cvi-workflow/step/compute-elevation",
      "provType": "Entity",
      "entityType": [
        "prov:Plan",
        "ospd:ProcessingStep"
      ],
      "label": "Compute coastal elevation vulnerability score per transect",
      "processType": "https://example.org/ospd/process-types/elevation-analysis",
      "sourceCode": "steps/compute_elevation.py"
    },
    {
      "id": "hartis:cvi-workflow/step/compute-cvi",
      "provType": "Entity",
      "entityType": [
        "prov:Plan",
        "ospd:ProcessingStep"
      ],
      "label": "Compute final Coastal Vulnerability Index classification",
      "processType": "https://example.org/ospd/process-types/vulnerability-index-scoring",
      "sourceCode": "steps/compute_cvi.py"
    }
  ],
  "runtime": {
    "id": "hartis:cvi-run-example-001/runtime",
    "provType": "Activity",
    "activityType": "acttype:WorkflowRun",
    "label": "Illustrative CVI workflow execution",
    "workflowDefinition": "hartis:cvi-workflow",
    "used": [
      "hartis:cvi-run-example-001/entity/cvi-scoring-config",
      "hartis:cvi-run-example-001/entity/med-coastal-aois",
      "hartis:cvi-run-example-001/entity/nominatim-response",
      "hartis:cvi-run-example-001/entity/overpass-coastline-response",
      "hartis:cvi-run-example-001/entity/esa-worldcover-2021",
      "hartis:cvi-run-example-001/entity/copernicus-dem",
      "hartis:cvi-run-example-001/entity/deltares-chw-erosion-wfs"
    ],
    "generated": "hartis:cvi-run-example-001/entity/transects-with-cvi-equal",
    "wasAssociatedWith": [
      "hartis:cvi-workflow/container/cvi-workflow-latest"
    ],
    "activities": [
      {
        "id": "hartis:cvi-run-example-001/activity/setup-env",
        "provType": "Activity",
        "activityType": "https://example.org/ospd/process-types/configuration-validation",
        "plan": "hartis:cvi-workflow/step/setup-env",
        "used": [
          "hartis:cvi-run-example-001/entity/cvi-scoring-config"
        ],
        "generated": [
          "hartis:cvi-run-example-001/entity/validated-config"
        ],
        "qualifiedUsage": [
          {
            "entity": "hartis:cvi-run-example-001/entity/cvi-scoring-config",
            "hadRole": "hartis:role/workflowConfiguration"
          }
        ],
        "wasAssociatedWith": [
          "hartis:cvi-workflow/software/setup-env-py",
          "hartis:cvi-workflow/container/cvi-workflow-latest"
        ],
        "parameters": {
          "outputDirectory": "output_data",
          "expectedConfigKeys": [
            "weights"
          ]
        }
      },
      {
        "id": "hartis:cvi-run-example-001/activity/extract-coastline",
        "provType": "Activity",
        "activityType": "https://example.org/ospd/process-types/coastline-extraction",
        "plan": "hartis:cvi-workflow/step/extract-coastline",
        "used": [
          "hartis:cvi-run-example-001/entity/med-coastal-aois",
          "hartis:cvi-run-example-001/entity/nominatim-response",
          "hartis:cvi-run-example-001/entity/overpass-coastline-response"
        ],
        "generated": [
          "hartis:cvi-run-example-001/entity/coastline-gpkg"
        ],
        "qualifiedUsage": [
          {
            "entity": "hartis:cvi-run-example-001/entity/med-coastal-aois",
            "hadRole": "hartis:role/aoiCandidateSource"
          },
          {
            "entity": "hartis:cvi-run-example-001/entity/nominatim-response",
            "hadRole": "hartis:role/aoiGeocodingResponse"
          },
          {
            "entity": "hartis:cvi-run-example-001/entity/overpass-coastline-response",
            "hadRole": "hartis:role/sourceCoastlineFeatures"
          }
        ],
        "wasAssociatedWith": [
          "hartis:cvi-workflow/software/extract-coastline-py",
          "hartis:cvi-workflow/container/cvi-workflow-latest"
        ],
        "wasInformedBy": [
          "hartis:cvi-run-example-001/activity/setup-env"
        ],
        "parameters": {
          "osmFilter": "natural=coastline",
          "maxAoiAttempts": 5,
          "outputFormat": "GeoPackage"
        }
      },
      {
        "id": "hartis:cvi-run-example-001/activity/generate-transects",
        "provType": "Activity",
        "activityType": "https://example.org/ospd/process-types/transect-generation",
        "plan": "hartis:cvi-workflow/step/generate-transects",
        "used": [
          "hartis:cvi-run-example-001/entity/coastline-gpkg"
        ],
        "generated": [
          "hartis:cvi-run-example-001/entity/transects-geojson"
        ],
        "qualifiedUsage": [
          {
            "entity": "hartis:cvi-run-example-001/entity/coastline-gpkg",
            "hadRole": "hartis:role/sourceCoastline"
          }
        ],
        "wasAssociatedWith": [
          "hartis:cvi-workflow/software/generate-transects-py",
          "hartis:cvi-workflow/container/cvi-workflow-latest"
        ],
        "wasInformedBy": [
          "hartis:cvi-run-example-001/activity/extract-coastline"
        ],
        "parameters": {
          "spacingMeters": 50,
          "transectLengthMeters": 400,
          "maxProcessedCoastlineMeters": 15000,
          "processingCrs": "EPSG:3857",
          "outputCrs": "EPSG:4326"
        }
      },
      {
        "id": "hartis:cvi-run-example-001/activity/compute-landcover",
        "provType": "Activity",
        "activityType": "https://example.org/ospd/process-types/land-cover-analysis",
        "plan": "hartis:cvi-workflow/step/compute-landcover",
        "used": [
          "hartis:cvi-run-example-001/entity/transects-geojson",
          "hartis:cvi-run-example-001/entity/validated-config",
          "hartis:cvi-run-example-001/entity/esa-worldcover-2021"
        ],
        "generated": [
          "hartis:cvi-run-example-001/entity/transects-with-land-cover"
        ],
        "qualifiedUsage": [
          {
            "entity": "hartis:cvi-run-example-001/entity/transects-geojson",
            "hadRole": "hartis:role/analysisUnits"
          },
          {
            "entity": "hartis:cvi-run-example-001/entity/validated-config",
            "hadRole": "hartis:role/classificationConfiguration"
          },
          {
            "entity": "hartis:cvi-run-example-001/entity/esa-worldcover-2021",
            "hadRole": "hartis:role/sourceLandCoverRaster"
          }
        ],
        "wasAssociatedWith": [
          "hartis:cvi-workflow/software/compute-landcover-py",
          "hartis:cvi-workflow/container/cvi-workflow-latest"
        ],
        "wasInformedBy": [
          "hartis:cvi-run-example-001/activity/generate-transects"
        ],
        "parameters": {
          "derivedMeasure": "dominant land-cover class and CVI score"
        }
      },
      {
        "id": "hartis:cvi-run-example-001/activity/compute-slope",
        "provType": "Activity",
        "activityType": "https://example.org/ospd/process-types/slope-derivation",
        "plan": "hartis:cvi-workflow/step/compute-slope",
        "used": [
          "hartis:cvi-run-example-001/entity/transects-geojson",
          "hartis:cvi-run-example-001/entity/validated-config",
          "hartis:cvi-run-example-001/entity/copernicus-dem"
        ],
        "generated": [
          "hartis:cvi-run-example-001/entity/transects-with-slope"
        ],
        "qualifiedUsage": [
          {
            "entity": "hartis:cvi-run-example-001/entity/transects-geojson",
            "hadRole": "hartis:role/analysisUnits"
          },
          {
            "entity": "hartis:cvi-run-example-001/entity/validated-config",
            "hadRole": "hartis:role/classificationConfiguration"
          },
          {
            "entity": "hartis:cvi-run-example-001/entity/copernicus-dem",
            "hadRole": "hartis:role/sourceElevationRaster"
          }
        ],
        "wasAssociatedWith": [
          "hartis:cvi-workflow/software/compute-slope-py",
          "hartis:cvi-workflow/container/cvi-workflow-latest"
        ],
        "wasInformedBy": [
          "hartis:cvi-run-example-001/activity/generate-transects"
        ],
        "parameters": {
          "processingCrs": "EPSG:3035",
          "derivedMeasure": "slope percent"
        }
      },
      {
        "id": "hartis:cvi-run-example-001/activity/compute-erosion",
        "provType": "Activity",
        "activityType": "https://example.org/ospd/process-types/erosion-data-integration",
        "plan": "hartis:cvi-workflow/step/compute-erosion",
        "used": [
          "hartis:cvi-run-example-001/entity/transects-geojson",
          "hartis:cvi-run-example-001/entity/validated-config",
          "hartis:cvi-run-example-001/entity/deltares-chw-erosion-wfs"
        ],
        "generated": [
          "hartis:cvi-run-example-001/entity/transects-with-erosion"
        ],
        "qualifiedUsage": [
          {
            "entity": "hartis:cvi-run-example-001/entity/transects-geojson",
            "hadRole": "hartis:role/analysisUnits"
          },
          {
            "entity": "hartis:cvi-run-example-001/entity/validated-config",
            "hadRole": "hartis:role/classificationConfiguration"
          },
          {
            "entity": "hartis:cvi-run-example-001/entity/deltares-chw-erosion-wfs",
            "hadRole": "hartis:role/sourceErosionClasses"
          }
        ],
        "wasAssociatedWith": [
          "hartis:cvi-workflow/software/compute-erosion-py",
          "hartis:cvi-workflow/container/cvi-workflow-latest"
        ],
        "wasInformedBy": [
          "hartis:cvi-run-example-001/activity/generate-transects"
        ],
        "parameters": {
          "derivedMeasure": "erosion class and CVI score",
          "rescale": {
            "1": 1,
            "2": 3,
            "3": 5
          }
        }
      },
      {
        "id": "hartis:cvi-run-example-001/activity/compute-elevation",
        "provType": "Activity",
        "activityType": "https://example.org/ospd/process-types/elevation-analysis",
        "plan": "hartis:cvi-workflow/step/compute-elevation",
        "used": [
          "hartis:cvi-run-example-001/entity/transects-geojson",
          "hartis:cvi-run-example-001/entity/validated-config",
          "hartis:cvi-run-example-001/entity/copernicus-dem"
        ],
        "generated": [
          "hartis:cvi-run-example-001/entity/transects-with-elevation"
        ],
        "qualifiedUsage": [
          {
            "entity": "hartis:cvi-run-example-001/entity/transects-geojson",
            "hadRole": "hartis:role/analysisUnits"
          },
          {
            "entity": "hartis:cvi-run-example-001/entity/validated-config",
            "hadRole": "hartis:role/classificationConfiguration"
          },
          {
            "entity": "hartis:cvi-run-example-001/entity/copernicus-dem",
            "hadRole": "hartis:role/sourceElevationRaster"
          }
        ],
        "wasAssociatedWith": [
          "hartis:cvi-workflow/software/compute-elevation-py",
          "hartis:cvi-workflow/container/cvi-workflow-latest"
        ],
        "wasInformedBy": [
          "hartis:cvi-run-example-001/activity/generate-transects"
        ],
        "parameters": {
          "derivedMeasure": "maximum elevation per transect"
        }
      },
      {
        "id": "hartis:cvi-run-example-001/activity/compute-cvi",
        "provType": "Activity",
        "activityType": "https://example.org/ospd/process-types/vulnerability-index-scoring",
        "plan": "hartis:cvi-workflow/step/compute-cvi",
        "used": [
          "hartis:cvi-run-example-001/entity/transects-with-land-cover",
          "hartis:cvi-run-example-001/entity/transects-with-slope",
          "hartis:cvi-run-example-001/entity/transects-with-erosion",
          "hartis:cvi-run-example-001/entity/transects-with-elevation",
          "hartis:cvi-run-example-001/entity/validated-config"
        ],
        "generated": [
          "hartis:cvi-run-example-001/entity/transects-with-cvi-equal"
        ],
        "qualifiedUsage": [
          {
            "entity": "hartis:cvi-run-example-001/entity/transects-with-land-cover",
            "hadRole": "hartis:role/landCoverScore"
          },
          {
            "entity": "hartis:cvi-run-example-001/entity/transects-with-slope",
            "hadRole": "hartis:role/slopeScore"
          },
          {
            "entity": "hartis:cvi-run-example-001/entity/transects-with-erosion",
            "hadRole": "hartis:role/erosionScore"
          },
          {
            "entity": "hartis:cvi-run-example-001/entity/transects-with-elevation",
            "hadRole": "hartis:role/elevationScore"
          },
          {
            "entity": "hartis:cvi-run-example-001/entity/validated-config",
            "hadRole": "hartis:role/classificationConfiguration"
          }
        ],
        "wasAssociatedWith": [
          "hartis:cvi-workflow/software/compute-cvi-py",
          "hartis:cvi-workflow/container/cvi-workflow-latest"
        ],
        "wasInformedBy": [
          "hartis:cvi-run-example-001/activity/compute-landcover",
          "hartis:cvi-run-example-001/activity/compute-slope",
          "hartis:cvi-run-example-001/activity/compute-erosion",
          "hartis:cvi-run-example-001/activity/compute-elevation"
        ],
        "parameters": {
          "indexMethod": "equal geometric CVI",
          "formula": "sqrt(product(scores) / number_of_scores)"
        }
      }
    ]
  },
  "entities": [
    {
      "id": "hartis:cvi-run-example-001/entity/cvi-scoring-config",
      "provType": "Entity",
      "label": "CVI scoring configuration",
      "path": "config/cvi_scoring_simple.json"
    },
    {
      "id": "hartis:cvi-run-example-001/entity/validated-config",
      "provType": "Entity",
      "label": "Validated CVI configuration",
      "path": "output_data/config_validated.json",
      "wasGeneratedBy": "hartis:cvi-run-example-001/activity/setup-env"
    },
    {
      "id": "hartis:cvi-run-example-001/entity/med-coastal-aois",
      "provType": "Entity",
      "label": "Mediterranean coastal AOI candidates",
      "format": "text/csv",
      "path": "input_data/med_coastal_aois.csv"
    },
    {
      "id": "hartis:cvi-run-example-001/entity/nominatim-response",
      "provType": "Entity",
      "label": "Nominatim AOI geocoding response",
      "source": "OpenStreetMap Nominatim"
    },
    {
      "id": "hartis:cvi-run-example-001/entity/overpass-coastline-response",
      "provType": "Entity",
      "label": "Overpass coastline feature response",
      "source": "OpenStreetMap Overpass API"
    },
    {
      "id": "hartis:cvi-run-example-001/entity/coastline-gpkg",
      "provType": "Entity",
      "entityType": "ospd:VectorDataset",
      "label": "Extracted coastline geometry",
      "format": "application/geopackage+sqlite3",
      "path": "output_data/coastline.gpkg",
      "wasGeneratedBy": "hartis:cvi-run-example-001/activity/extract-coastline"
    },
    {
      "id": "hartis:cvi-run-example-001/entity/transects-geojson",
      "provType": "Entity",
      "entityType": "ospd:VectorDataset",
      "label": "Generated CVI transects",
      "format": "application/geo+json",
      "path": "output_data/transects.geojson",
      "wasGeneratedBy": "hartis:cvi-run-example-001/activity/generate-transects"
    },
    {
      "id": "hartis:cvi-run-example-001/entity/esa-worldcover-2021",
      "provType": "Entity",
      "label": "ESA WorldCover 2021 source",
      "source": "Copernicus Dataspace"
    },
    {
      "id": "hartis:cvi-run-example-001/entity/copernicus-dem",
      "provType": "Entity",
      "label": "Copernicus DEM source",
      "source": "Copernicus Dataspace"
    },
    {
      "id": "hartis:cvi-run-example-001/entity/deltares-chw-erosion-wfs",
      "provType": "Entity",
      "label": "Deltares Coastal Hazard Wheel erosion response",
      "source": "Deltares WFS"
    },
    {
      "id": "hartis:cvi-run-example-001/entity/transects-with-land-cover",
      "provType": "Entity",
      "entityType": "ospd:VectorDataset",
      "label": "Transects with land-cover scores",
      "path": "output_data/transects_with_land_cover.geojson",
      "wasGeneratedBy": "hartis:cvi-run-example-001/activity/compute-landcover"
    },
    {
      "id": "hartis:cvi-run-example-001/entity/transects-with-slope",
      "provType": "Entity",
      "entityType": "ospd:VectorDataset",
      "label": "Transects with slope scores",
      "path": "output_data/transects_with_slope.geojson",
      "wasGeneratedBy": "hartis:cvi-run-example-001/activity/compute-slope"
    },
    {
      "id": "hartis:cvi-run-example-001/entity/transects-with-erosion",
      "provType": "Entity",
      "entityType": "ospd:VectorDataset",
      "label": "Transects with erosion scores",
      "path": "output_data/transects_with_erosion.geojson",
      "wasGeneratedBy": "hartis:cvi-run-example-001/activity/compute-erosion"
    },
    {
      "id": "hartis:cvi-run-example-001/entity/transects-with-elevation",
      "provType": "Entity",
      "entityType": "ospd:VectorDataset",
      "label": "Transects with elevation scores",
      "path": "output_data/transects_with_elevation.geojson",
      "wasGeneratedBy": "hartis:cvi-run-example-001/activity/compute-elevation"
    },
    {
      "id": "hartis:cvi-run-example-001/entity/transects-with-cvi-equal",
      "provType": "Entity",
      "entityType": "ospd:VectorDataset",
      "label": "Final CVI classification",
      "path": "output_data/transects_with_cvi_equal.geojson",
      "wasGeneratedBy": "hartis:cvi-run-example-001/activity/compute-cvi"
    }
  ],
  "notes": [
    "This is a normalized HARTIS workflow skeleton, not a final OSPD serialization.",
    "The runtime activities are linked to design-time plans through plan identifiers.",
    "External data sources are represented as entities; the exact representation of service calls remains open.",
    "All processType URIs are provisional and are not official Register identifiers.",
    "Credentials are intentionally not represented as values."
  ]
}
```

#### ttl
```ttl
@prefix acttype: <https://w3id.org/ogc/rim/activity-type/> .
@prefix hartis: <https://hartis.org/ospd2026/> .
@prefix ospd: <https://www.opengis.net/def/ospd/2026/> .
@prefix prov: <http://www.w3.org/ns/prov#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .

hartis:cvi-run-example-001 a prov:Bundle,
        prov:Entity ;
    rdfs:label "HARTIS CVI workflow design-time and runtime provenance skeleton" ;
    hartis:workflowDefinition hartis:cvi-workflow .

<https://hartis.org/ospd2026/cvi-run-example-001/entity/coastline-gpkg> a prov:Entity,
        ospd:VectorDataset ;
    rdfs:label "Extracted coastline geometry" ;
    prov:wasGeneratedBy <https://hartis.org/ospd2026/cvi-run-example-001/activity/extract-coastline> .

<https://hartis.org/ospd2026/cvi-run-example-001/entity/transects-geojson> a prov:Entity,
        ospd:VectorDataset ;
    rdfs:label "Generated CVI transects" ;
    prov:wasGeneratedBy <https://hartis.org/ospd2026/cvi-run-example-001/activity/generate-transects> .

<https://hartis.org/ospd2026/cvi-run-example-001/entity/transects-with-elevation> a prov:Entity,
        ospd:VectorDataset ;
    rdfs:label "Transects with elevation scores" ;
    prov:wasGeneratedBy <https://hartis.org/ospd2026/cvi-run-example-001/activity/compute-elevation> .

<https://hartis.org/ospd2026/cvi-run-example-001/entity/transects-with-erosion> a prov:Entity,
        ospd:VectorDataset ;
    rdfs:label "Transects with erosion scores" ;
    prov:wasGeneratedBy <https://hartis.org/ospd2026/cvi-run-example-001/activity/compute-erosion> .

<https://hartis.org/ospd2026/cvi-run-example-001/entity/transects-with-land-cover> a prov:Entity,
        ospd:VectorDataset ;
    rdfs:label "Transects with land-cover scores" ;
    prov:wasGeneratedBy <https://hartis.org/ospd2026/cvi-run-example-001/activity/compute-landcover> .

<https://hartis.org/ospd2026/cvi-run-example-001/entity/transects-with-slope> a prov:Entity,
        ospd:VectorDataset ;
    rdfs:label "Transects with slope scores" ;
    prov:wasGeneratedBy <https://hartis.org/ospd2026/cvi-run-example-001/activity/compute-slope> .

<https://hartis.org/ospd2026/cvi-run-example-001/entity/validated-config> a prov:Entity ;
    rdfs:label "Validated CVI configuration" ;
    prov:wasGeneratedBy <https://hartis.org/ospd2026/cvi-run-example-001/activity/setup-env> .

<https://hartis.org/ospd2026/cvi-run-example-001/runtime> a prov:Activity,
        acttype:WorkflowRun ;
    rdfs:label "Illustrative CVI workflow execution" ;
    prov:generated <https://hartis.org/ospd2026/cvi-run-example-001/entity/transects-with-cvi-equal> ;
    prov:used <https://hartis.org/ospd2026/cvi-run-example-001/entity/copernicus-dem>,
        <https://hartis.org/ospd2026/cvi-run-example-001/entity/cvi-scoring-config>,
        <https://hartis.org/ospd2026/cvi-run-example-001/entity/deltares-chw-erosion-wfs>,
        <https://hartis.org/ospd2026/cvi-run-example-001/entity/esa-worldcover-2021>,
        <https://hartis.org/ospd2026/cvi-run-example-001/entity/med-coastal-aois>,
        <https://hartis.org/ospd2026/cvi-run-example-001/entity/nominatim-response>,
        <https://hartis.org/ospd2026/cvi-run-example-001/entity/overpass-coastline-response> ;
    prov:wasAssociatedWith <https://hartis.org/ospd2026/cvi-workflow/container/cvi-workflow-latest> ;
    hartis:workflowDefinition hartis:cvi-workflow .

<https://hartis.org/ospd2026/cvi-workflow/step/compute-cvi> a prov:Entity,
        prov:Plan,
        ospd:ProcessingStep ;
    rdfs:label "Compute final Coastal Vulnerability Index classification" .

<https://hartis.org/ospd2026/cvi-workflow/step/compute-elevation> a prov:Entity,
        prov:Plan,
        ospd:ProcessingStep ;
    rdfs:label "Compute coastal elevation vulnerability score per transect" .

<https://hartis.org/ospd2026/cvi-workflow/step/compute-erosion> a prov:Entity,
        prov:Plan,
        ospd:ProcessingStep ;
    rdfs:label "Compute erosion vulnerability score per transect" .

<https://hartis.org/ospd2026/cvi-workflow/step/compute-landcover> a prov:Entity,
        prov:Plan,
        ospd:ProcessingStep ;
    rdfs:label "Compute land-cover vulnerability score per transect" .

<https://hartis.org/ospd2026/cvi-workflow/step/compute-slope> a prov:Entity,
        prov:Plan,
        ospd:ProcessingStep ;
    rdfs:label "Compute slope vulnerability score per transect" .

<https://hartis.org/ospd2026/cvi-workflow/step/extract-coastline> a prov:Entity,
        prov:Plan,
        ospd:ProcessingStep ;
    rdfs:label "Extract coastline geometry for selected AOI" .

<https://hartis.org/ospd2026/cvi-workflow/step/generate-transects> a prov:Entity,
        prov:Plan,
        ospd:ProcessingStep ;
    rdfs:label "Generate cross-shore transects from coastline" .

<https://hartis.org/ospd2026/cvi-workflow/step/setup-env> a prov:Entity,
        prov:Plan,
        ospd:ProcessingStep ;
    rdfs:label "Validate CVI configuration and initialize output workspace" .

<https://hartis.org/ospd2026/cvi-run-example-001/entity/copernicus-dem> a prov:Entity ;
    rdfs:label "Copernicus DEM source" .

<https://hartis.org/ospd2026/cvi-run-example-001/entity/cvi-scoring-config> a prov:Entity ;
    rdfs:label "CVI scoring configuration" .

<https://hartis.org/ospd2026/cvi-run-example-001/entity/deltares-chw-erosion-wfs> a prov:Entity ;
    rdfs:label "Deltares Coastal Hazard Wheel erosion response" .

<https://hartis.org/ospd2026/cvi-run-example-001/entity/esa-worldcover-2021> a prov:Entity ;
    rdfs:label "ESA WorldCover 2021 source" .

<https://hartis.org/ospd2026/cvi-run-example-001/entity/med-coastal-aois> a prov:Entity ;
    rdfs:label "Mediterranean coastal AOI candidates" .

<https://hartis.org/ospd2026/cvi-run-example-001/entity/nominatim-response> a prov:Entity ;
    rdfs:label "Nominatim AOI geocoding response" .

<https://hartis.org/ospd2026/cvi-run-example-001/entity/overpass-coastline-response> a prov:Entity ;
    rdfs:label "Overpass coastline feature response" .

<https://hartis.org/ospd2026/cvi-run-example-001/entity/transects-with-cvi-equal> a prov:Entity,
        ospd:VectorDataset ;
    rdfs:label "Final CVI classification" ;
    prov:wasGeneratedBy <https://hartis.org/ospd2026/cvi-run-example-001/activity/compute-cvi> .

hartis:cvi-workflow a prov:Entity,
        prov:Plan,
        acttype:WorkflowPlan,
        ospd:WorkflowDefinition ;
    rdfs:label "HARTIS Coastal Vulnerability Index workflow" .


```

## Schema

```yaml
$schema: https://json-schema.org/draft/2020-12/schema
$id: https://github.com/hartis-org/cvi-workflow/tree/ospd2026-d100/ospd2026/building-block/_sources/hartis-provenance/cvi-workflow/schema.yaml
title: HARTIS CVI Workflow Provenance
description: 'HARTIS profile of the Workflow Provenance Graph (bundle form) for the
  complete CVI workflow. PROV structure, identifiers, provType and entityType/activityType
  come from the PROV building blocks; this schema only adds what HARTIS requires:
  a workflow definition, design-time plans with process types, a runtime activity
  whose steps link to their plans, and the entities they use and generate.'
allOf:
- $ref: https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/prov-profiles/workflow-graph/schema.yaml
- $ref: https://ogcincubator.github.io/bblock-prov-schema/build/annotated/ogc-utils/prov-entity/schema.yaml
type: object
required:
- id
- provType
- entityType
- workflowDefinition
- plans
- runtime
- entities
properties:
  entityType:
    description: The bundle's entityType must include prov:Bundle.
    anyOf:
    - const: prov:Bundle
    - type: array
      contains:
        const: prov:Bundle
  status:
    type: string
  workflowDefinition:
    description: The workflow as a whole, as a PROV Plan.
    allOf:
    - $ref: https://ogcincubator.github.io/bblock-prov-schema/build/annotated/ogc-utils/prov-entity/schema.yaml
    required:
    - id
    - provType
    - entityType
    properties:
      sourceWorkflow:
        type: string
      executionImage:
        type: string
    x-jsonld-id: https://hartis.org/ospd2026/workflowDefinition
    x-jsonld-type: '@id'
  plans:
    description: Design-time plans, one per processing step.
    type: array
    minItems: 1
    items:
      allOf:
      - $ref: https://ogcincubator.github.io/bblock-prov-schema/build/annotated/ogc-utils/prov-entity/schema.yaml
      required:
      - id
      - provType
      - entityType
      - processType
      properties:
        processType:
          description: The process type this plan describes.
          $ref: https://opengeospatial.github.io/bblocks/annotated-schemas/ogc-utils/iri-or-curie/schema.yaml#/$defs/Single
          x-jsonld-id: dct:type
          x-jsonld-type: '@id'
        sourceCode:
          type: string
    x-jsonld-id: '@included'
  runtime:
    description: The workflow execution as a whole, containing the step activities.
    allOf:
    - $ref: https://ogcincubator.github.io/bblock-prov-schema/build/annotated/ogc-utils/prov-activity/schema.yaml
    required:
    - id
    - provType
    - workflowDefinition
    - activities
    properties:
      workflowDefinition:
        description: Reference to the workflow definition this run executes.
        type: string
        x-jsonld-id: https://hartis.org/ospd2026/workflowDefinition
        x-jsonld-type: '@id'
      activities:
        type: array
        minItems: 1
        items:
          $ref: '#/$defs/activity'
        x-jsonld-id: dct:hasPart
        x-jsonld-type: '@id'
    x-jsonld-id: '@included'
  entities:
    description: Data used and generated by the run.
    type: array
    minItems: 1
    items:
      allOf:
      - $ref: https://ogcincubator.github.io/bblock-prov-schema/build/annotated/ogc-utils/prov-entity/schema.yaml
      required:
      - id
      - provType
    x-jsonld-id: '@included'
$defs:
  activity:
    description: 'A runtime step: a Registered Processing Step that names its design-time
      plan and lists its inputs and outputs explicitly.'
    allOf:
    - $ref: https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/prov-profiles/processing-step/schema.yaml
    required:
    - provType
    - plan
    - used
    - generated
    properties:
      plan:
        description: Reference to the design-time plan this step executes.
        type: string
        x-jsonld-id: https://hartis.org/ospd2026/plan
        x-jsonld-type: '@id'
      used:
        type: array
        minItems: 1
      generated:
        type: array
        minItems: 1
      qualifiedUsage:
        type: array
      wasAssociatedWith:
        type: array
x-jsonld-prefixes:
  hartis: https://hartis.org/ospd2026/
  ospd: https://www.opengis.net/def/ospd/2026/
x-bblocks-metadata:
  itemIdentifier: ogc.osc.prov-profiles.hartis-provenance.cvi-workflow
  register: https://ogcincubator.github.io/bblocks-openscience/build/register.json
  version: 0.1.0
  dateOfLastChange: '2026-10-13'

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/prov-profiles/hartis-provenance/cvi-workflow/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/prov-profiles/hartis-provenance/cvi-workflow/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "wasInfluencedBy": {
      "@id": "prov:wasInfluencedBy",
      "@type": "@id"
    },
    "qualifiedInfluence": {
      "@id": "prov:qualifiedInfluence",
      "@type": "@id"
    },
    "hadMember": {
      "@id": "prov:hadMember",
      "@type": "@id"
    },
    "id": "@id",
    "provType": "@type",
    "featureType": "@type",
    "entityType": "@type",
    "has_provenance": {
      "@id": "dct:provenance",
      "@type": "@id"
    },
    "wasGeneratedBy": {
      "@id": "prov:wasGeneratedBy",
      "@type": "@id"
    },
    "wasAttributedTo": {
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
    "activityType": "@type",
    "agentType": "@type",
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
    "endedAtTime": {
      "@id": "prov:endedAtTime",
      "@type": "xsd:dateTime"
    },
    "startedAtTime": {
      "@id": "prov:startedAtTime",
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
    "actedOnBehalfOf": {
      "@id": "prov:actedOnBehalfOf",
      "@type": "@id"
    },
    "agent": {
      "@id": "prov:agent",
      "@type": "@id"
    },
    "entity": {
      "@id": "prov:entity",
      "@type": "@id"
    },
    "generated": {
      "@id": "prov:generated",
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
    "invalidated": {
      "@id": "prov:invalidated",
      "@type": "@id"
    },
    "qualifiedAssociation": {
      "@id": "prov:qualifiedAssociation",
      "@type": "@id"
    },
    "qualifiedCommunication": {
      "@id": "prov:qualifiedCommunication",
      "@type": "@id"
    },
    "qualifiedDelegation": {
      "@id": "prov:qualifiedDelegation",
      "@type": "@id"
    },
    "qualifiedEnd": {
      "@id": "prov:qualifiedEnd",
      "@type": "@id"
    },
    "qualifiedStart": {
      "@id": "prov:qualifiedStart",
      "@type": "@id"
    },
    "qualifiedUsage": {
      "@id": "prov:qualifiedUsage",
      "@type": "@id"
    },
    "used": {
      "@id": "prov:used",
      "@type": "@id"
    },
    "wasAssociatedWith": {
      "@id": "prov:wasAssociatedWith",
      "@type": "@id"
    },
    "wasEndedBy": {
      "@id": "prov:wasEndedBy",
      "@type": "@id"
    },
    "wasInformedBy": {
      "@id": "prov:wasInformedBy",
      "@type": "@id"
    },
    "wasStartedBy": {
      "@id": "prov:wasStartedBy",
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
    "name": "rdfs:label",
    "label": "rdfs:label",
    "workflowDefinition": {
      "@id": "hartis:workflowDefinition",
      "@type": "@id"
    },
    "plans": {
      "@context": {
        "processType": {
          "@id": "dct:type",
          "@type": "@id"
        }
      },
      "@id": "@included"
    },
    "runtime": {
      "@context": {
        "activities": {
          "@context": {
            "plan": {
              "@id": "hartis:plan",
              "@type": "@id"
            }
          },
          "@id": "dct:hasPart",
          "@type": "@id"
        }
      },
      "@id": "@included"
    },
    "entities": "@included",
    "prov": "http://www.w3.org/ns/prov#",
    "xsd": "http://www.w3.org/2001/XMLSchema#",
    "rdfs": "http://www.w3.org/2000/01/rdf-schema#",
    "dct": "http://purl.org/dc/terms/",
    "rdf": "http://www.w3.org/1999/02/22-rdf-syntax-ns#",
    "oa": "http://www.w3.org/ns/oa#",
    "dcterms": "http://purl.org/dc/terms/",
    "skos": "http://www.w3.org/2004/02/skos/core#",
    "acttype": "https://w3id.org/ogc/rim/activity-type/",
    "hartis": "https://hartis.org/ospd2026/",
    "ospd": "https://www.opengis.net/def/ospd/2026/",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/prov-profiles/hartis-provenance/cvi-workflow/context.jsonld)

## Sources

* [HARTIS CVI workflow repository](https://github.com/hartis-org/cvi-workflow)
* [HARTIS OSPD-2026 D001 contribution](https://github.com/hartis-org/cvi-workflow/blob/ospd2026-d100/ospd2026/report/d001-hartis-contribution.md)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-openscience](https://github.com/ogcincubator/bblocks-openscience)
* Path: `_sources/prov-profiles/hartis-provenance/cvi-workflow`

