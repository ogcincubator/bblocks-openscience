
# HARTIS CVI Workflow Provenance (Schema)

`ogc.osc.hartis-provenance.cvi-workflow` *v0.1.0*

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

## Examples

### HARTIS full CVI workflow provenance candidate
A complete design-time and runtime provenance representation for the HARTIS CVI workflow, including plans, activities, inputs and outputs.
#### json
```json
{
  "@context": {
    "prov": "http://www.w3.org/ns/prov#",
    "dct": "http://purl.org/dc/terms/",
    "ospd": "https://www.opengis.net/def/ospd/2026/",
    "hartis": "https://hartis.org/ospd2026/",
    "processType": "dct:type",
    "used": "prov:used",
    "generated": "prov:generated",
    "qualifiedUsage": "prov:qualifiedUsage",
    "entity": "prov:entity",
    "hadRole": "prov:hadRole",
    "wasGeneratedBy": "prov:wasGeneratedBy",
    "wasInformedBy": "prov:wasInformedBy",
    "wasAssociatedWith": "prov:wasAssociatedWith",
    "qualifiedAssociation": "prov:qualifiedAssociation",
    "agent": "prov:agent",
    "hadPlan": "prov:hadPlan"
  },
  "id": "hartis:cvi-run-example-001",
  "type": "prov:Bundle",
  "label": "HARTIS CVI workflow design-time and runtime provenance skeleton",
  "status": "illustrative-candidate",
  "workflowDefinition": {
    "id": "hartis:cvi-workflow",
    "type": [
      "prov:Plan",
      "ospd:WorkflowDefinition"
    ],
    "label": "HARTIS Coastal Vulnerability Index workflow",
    "sourceWorkflow": "cvi_workflow.cwl",
    "executionImage": "ghcr.io/hartis-org/cvi-workflow:latest"
  },
  "plans": [
    {
      "id": "hartis:cvi-workflow/step/setup-env",
      "type": ["prov:Plan", "ospd:ProcessingStep"],
      "label": "Validate CVI configuration and initialize output workspace",
      "processType": "https://example.org/ospd/process-types/configuration-validation",
      "sourceCode": "steps/setup_env.py"
    },
    {
      "id": "hartis:cvi-workflow/step/extract-coastline",
      "type": ["prov:Plan", "ospd:ProcessingStep"],
      "label": "Extract coastline geometry for selected AOI",
      "processType": "https://example.org/ospd/process-types/coastline-extraction",
      "sourceCode": "steps/extract_coastline.py"
    },
    {
      "id": "hartis:cvi-workflow/step/generate-transects",
      "type": ["prov:Plan", "ospd:ProcessingStep"],
      "label": "Generate cross-shore transects from coastline",
      "processType": "https://example.org/ospd/process-types/transect-generation",
      "sourceCode": "steps/generate_transects.py"
    },
    {
      "id": "hartis:cvi-workflow/step/compute-landcover",
      "type": ["prov:Plan", "ospd:ProcessingStep"],
      "label": "Compute land-cover vulnerability score per transect",
      "processType": "https://example.org/ospd/process-types/land-cover-analysis",
      "sourceCode": "steps/compute_landcover.py"
    },
    {
      "id": "hartis:cvi-workflow/step/compute-slope",
      "type": ["prov:Plan", "ospd:ProcessingStep"],
      "label": "Compute slope vulnerability score per transect",
      "processType": "https://example.org/ospd/process-types/slope-derivation",
      "sourceCode": "steps/compute_slope.py"
    },
    {
      "id": "hartis:cvi-workflow/step/compute-erosion",
      "type": ["prov:Plan", "ospd:ProcessingStep"],
      "label": "Compute erosion vulnerability score per transect",
      "processType": "https://example.org/ospd/process-types/erosion-data-integration",
      "sourceCode": "steps/compute_erosion.py"
    },
    {
      "id": "hartis:cvi-workflow/step/compute-elevation",
      "type": ["prov:Plan", "ospd:ProcessingStep"],
      "label": "Compute coastal elevation vulnerability score per transect",
      "processType": "https://example.org/ospd/process-types/elevation-analysis",
      "sourceCode": "steps/compute_elevation.py"
    },
    {
      "id": "hartis:cvi-workflow/step/compute-cvi",
      "type": ["prov:Plan", "ospd:ProcessingStep"],
      "label": "Compute final Coastal Vulnerability Index classification",
      "processType": "https://example.org/ospd/process-types/vulnerability-index-scoring",
      "sourceCode": "steps/compute_cvi.py"
    }
  ],
  "runtime": {
    "id": "hartis:cvi-run-example-001/runtime",
    "type": "prov:Activity",
    "label": "Illustrative CVI workflow execution",
    "workflowDefinition": "hartis:cvi-workflow",
    "wasAssociatedWith": [
      "hartis:cvi-workflow/container/cvi-workflow-latest"
    ],
    "activities": [
      {
        "id": "hartis:cvi-run-example-001/activity/setup-env",
        "type": "prov:Activity",
        "plan": "hartis:cvi-workflow/step/setup-env",
        "processType": "https://example.org/ospd/process-types/configuration-validation",
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
        "type": "prov:Activity",
        "plan": "hartis:cvi-workflow/step/extract-coastline",
        "processType": "https://example.org/ospd/process-types/coastline-extraction",
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
        "type": "prov:Activity",
        "plan": "hartis:cvi-workflow/step/generate-transects",
        "processType": "https://example.org/ospd/process-types/transect-generation",
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
        "type": "prov:Activity",
        "plan": "hartis:cvi-workflow/step/compute-landcover",
        "processType": "https://example.org/ospd/process-types/land-cover-analysis",
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
        "type": "prov:Activity",
        "plan": "hartis:cvi-workflow/step/compute-slope",
        "processType": "https://example.org/ospd/process-types/slope-derivation",
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
        "type": "prov:Activity",
        "plan": "hartis:cvi-workflow/step/compute-erosion",
        "processType": "https://example.org/ospd/process-types/erosion-data-integration",
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
        "type": "prov:Activity",
        "plan": "hartis:cvi-workflow/step/compute-elevation",
        "processType": "https://example.org/ospd/process-types/elevation-analysis",
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
        "type": "prov:Activity",
        "plan": "hartis:cvi-workflow/step/compute-cvi",
        "processType": "https://example.org/ospd/process-types/vulnerability-index-scoring",
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
    {"id": "hartis:cvi-run-example-001/entity/cvi-scoring-config", "type": "prov:Entity", "label": "CVI scoring configuration", "path": "config/cvi_scoring_simple.json"},
    {"id": "hartis:cvi-run-example-001/entity/validated-config", "type": "prov:Entity", "label": "Validated CVI configuration", "path": "output_data/config_validated.json", "wasGeneratedBy": "hartis:cvi-run-example-001/activity/setup-env"},
    {"id": "hartis:cvi-run-example-001/entity/med-coastal-aois", "type": "prov:Entity", "label": "Mediterranean coastal AOI candidates", "format": "text/csv", "path": "input_data/med_coastal_aois.csv"},
    {"id": "hartis:cvi-run-example-001/entity/nominatim-response", "type": "prov:Entity", "label": "Nominatim AOI geocoding response", "source": "OpenStreetMap Nominatim"},
    {"id": "hartis:cvi-run-example-001/entity/overpass-coastline-response", "type": "prov:Entity", "label": "Overpass coastline feature response", "source": "OpenStreetMap Overpass API"},
    {"id": "hartis:cvi-run-example-001/entity/coastline-gpkg", "type": ["prov:Entity", "ospd:VectorDataset"], "label": "Extracted coastline geometry", "format": "application/geopackage+sqlite3", "path": "output_data/coastline.gpkg", "wasGeneratedBy": "hartis:cvi-run-example-001/activity/extract-coastline"},
    {"id": "hartis:cvi-run-example-001/entity/transects-geojson", "type": ["prov:Entity", "ospd:VectorDataset"], "label": "Generated CVI transects", "format": "application/geo+json", "path": "output_data/transects.geojson", "wasGeneratedBy": "hartis:cvi-run-example-001/activity/generate-transects"},
    {"id": "hartis:cvi-run-example-001/entity/esa-worldcover-2021", "type": "prov:Entity", "label": "ESA WorldCover 2021 source", "source": "Copernicus Dataspace"},
    {"id": "hartis:cvi-run-example-001/entity/copernicus-dem", "type": "prov:Entity", "label": "Copernicus DEM source", "source": "Copernicus Dataspace"},
    {"id": "hartis:cvi-run-example-001/entity/deltares-chw-erosion-wfs", "type": "prov:Entity", "label": "Deltares Coastal Hazard Wheel erosion response", "source": "Deltares WFS"},
    {"id": "hartis:cvi-run-example-001/entity/transects-with-land-cover", "type": ["prov:Entity", "ospd:VectorDataset"], "label": "Transects with land-cover scores", "path": "output_data/transects_with_land_cover.geojson", "wasGeneratedBy": "hartis:cvi-run-example-001/activity/compute-landcover"},
    {"id": "hartis:cvi-run-example-001/entity/transects-with-slope", "type": ["prov:Entity", "ospd:VectorDataset"], "label": "Transects with slope scores", "path": "output_data/transects_with_slope.geojson", "wasGeneratedBy": "hartis:cvi-run-example-001/activity/compute-slope"},
    {"id": "hartis:cvi-run-example-001/entity/transects-with-erosion", "type": ["prov:Entity", "ospd:VectorDataset"], "label": "Transects with erosion scores", "path": "output_data/transects_with_erosion.geojson", "wasGeneratedBy": "hartis:cvi-run-example-001/activity/compute-erosion"},
    {"id": "hartis:cvi-run-example-001/entity/transects-with-elevation", "type": ["prov:Entity", "ospd:VectorDataset"], "label": "Transects with elevation scores", "path": "output_data/transects_with_elevation.geojson", "wasGeneratedBy": "hartis:cvi-run-example-001/activity/compute-elevation"},
    {"id": "hartis:cvi-run-example-001/entity/transects-with-cvi-equal", "type": ["prov:Entity", "ospd:VectorDataset"], "label": "Final CVI classification", "path": "output_data/transects_with_cvi_equal.geojson", "wasGeneratedBy": "hartis:cvi-run-example-001/activity/compute-cvi"}
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

## Schema

```yaml
$schema: https://json-schema.org/draft/2020-12/schema
$id: https://github.com/hartis-org/cvi-workflow/tree/ospd2026-d100/ospd2026/building-block/_sources/hartis-provenance/cvi-workflow/schema.yaml
title: HARTIS CVI Workflow Provenance
description: Candidate schema for the complete HARTIS CVI workflow provenance bundle.
type: object
required:
- id
- type
- workflowDefinition
- plans
- runtime
- entities
properties:
  id:
    type: string
  type:
    anyOf:
    - const: prov:Bundle
    - type: array
      contains:
        const: prov:Bundle
  label:
    type: string
  status:
    type: string
  workflowDefinition:
    type: object
    required:
    - id
    - type
    - label
    properties:
      id:
        type: string
      type:
        anyOf:
        - type: string
        - type: array
          minItems: 1
      label:
        type: string
      sourceWorkflow:
        type: string
      executionImage:
        type: string
    additionalProperties: true
  plans:
    type: array
    minItems: 1
    items:
      type: object
      required:
      - id
      - type
      - label
      - processType
      properties:
        id:
          type: string
        type:
          type: array
          minItems: 1
        label:
          type: string
        processType:
          type: string
        sourceCode:
          type: string
      additionalProperties: true
  runtime:
    type: object
    required:
    - id
    - type
    - workflowDefinition
    - activities
    properties:
      id:
        type: string
      type:
        anyOf:
        - type: string
        - type: array
          minItems: 1
      workflowDefinition:
        type: string
      activities:
        type: array
        minItems: 1
        items:
          $ref: '#/$defs/activity'
    additionalProperties: true
  entities:
    type: array
    minItems: 1
    items:
      type: object
      required:
      - id
      - type
      properties:
        id:
          type: string
        type:
          anyOf:
          - type: string
          - type: array
            minItems: 1
        label:
          type: string
      additionalProperties: true
additionalProperties: true
$defs:
  activity:
    type: object
    required:
    - id
    - type
    - plan
    - processType
    - used
    - generated
    properties:
      id:
        type: string
      type:
        anyOf:
        - type: string
        - type: array
          minItems: 1
      plan:
        type: string
      processType:
        type: string
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
    additionalProperties: true

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/hartis-provenance/cvi-workflow/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/hartis-provenance/cvi-workflow/schema.yaml)

## Sources

* [HARTIS CVI workflow repository](https://github.com/hartis-org/cvi-workflow)
* [HARTIS OSPD-2026 D001 contribution](https://github.com/hartis-org/cvi-workflow/blob/ospd2026-d100/ospd2026/report/d001-hartis-contribution.md)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-openscience](https://github.com/ogcincubator/bblocks-openscience)
* Path: `_sources/hartis-provenance/cvi-workflow`

