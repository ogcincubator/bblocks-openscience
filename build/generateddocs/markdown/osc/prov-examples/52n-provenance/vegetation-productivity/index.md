
# Vegetation Productivity Trend Workflow Provenance Profile (Schema)

`ogc.osc.prov-examples.52n-provenance.vegetation-productivity` *v0.1*

Vegetation Productivity Trend Workflow Provenance Profile.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

## Vegetation Productivity Trend Workflow Provenance Profile

This Building Block contains the provenance description of a vegetation productivity trend workflow developed as part of the [PEOPLE-ECCO](https://www.people-ecco.eu/) project and profiled within the [Open Science Persitent Demonstrator 2026](https://www.ogc.org/de/initiatives/open-science-persistent-demonstrator-2026/) initiative.

The provenance representation follows [W3C PROV](https://www.w3.org/TR/prov-overview/), to be more specific its JSON schema as defined in the [Provenance Chain](https://ogcincubator.github.io/bblock-prov-schema/bblock/ogc.ogc-utils.prov) Building Block.

### Conformance to the Workflow Provenance Graph profile

This block profiles the [Workflow Provenance Graph](bblock://ogc.osc.prov-profiles.workflow-graph),
so every activity must be a [Registered Processing Step](bblock://ogc.osc.prov-profiles.processing-step):
its `activityType` must give a process type, from a governed register, more specific than `prov:Activity`, and it must have an output.
Each node gives its PROV class in `provType`, and `entityType`, `activityType` and `agentType`
carry only the specific types.
The example conforms. Its post-processing steps are typed with the registered activity types
`ospd:cog-conversion` and `ospd:catalog-export` (which replaced the local CURIEs `ex:CogConversion` and
`ex:StacMetadataCreation`, 26 Nov 2026).

The workflow is orchestrated by [Prefect](https://www.prefect.io/). The run, its plan and its runner
are typed with the generic workflow classes of the
[activity type register profile](https://w3id.org/ogc/rim/activity-type/):
`ex:vegetation_productivity_run` is an `acttype:WorkflowRun`, the Prefect flow
`ex:vegetation_productivity_flow` an `acttype:WorkflowPlan` and `ex:prefect` an `acttype:WorkflowRunner`.
The run uses the inputs that no step generated (the Sentinel-2 collection and the workflow
parameters `ex:workflow_parameters`, which steps 1 and 2 share) and generates the output of the last step (the Seasonal Sen Slope STAC collection),
by reference only.
The analyst is responsible for the run through Prefect, which acts on their behalf.
Each step points to the run it belongs to with `isPartOf`.

## Examples

### Example from a vegetation productivity trend workflow run from the PEOPLE-ECCO project
#### json
```json
[
  {
    "id": "https://openeo.example.org/collections/SENTINEL2_L2",
    "provType": "Entity",
    "entityType": "prov:Collection",
    "dct:title": "Sentinel-2 L2A surface reflectance",
    "dct:description": "Copernicus Sentinel-2 MSI Level-2A bottom-of-atmosphere reflectance, atmospherically corrected with Sen2Cor and including the scene classification layer (SCL), as offered by the openEO backend.",
    "dct:identifier": "SENTINEL2_L2",
    "dct:publisher": "European Space Agency (ESA), Copernicus Programme",
    "license": "https://sentinels.copernicus.eu/documents/247904/690755/Sentinel_Data_Legal_Notice",
    "ex:mission": "Sentinel-2",
    "ex:instrument": "MSI",
    "ex:processingLevel": "L2A",
    "ex:spatialResolution": "10 m (B02, B03, B04, B08), 20 m (B05-B07, B8A, B11, B12, SCL), 60 m (B01, B09)",
    "ex:revisitTime": "5 days",
    "seeAlso": "https://documentation.dataspace.copernicus.eu/Data/SentinelMissions/Sentinel2.html"
  },

  {
    "id": "ex:bap_results",
    "provType": "Entity",
    "entityType": "prov:Collection",
    "dct:title": "Best available pixel composites (plain GeoTIFF)",
    "dct:format": "image/tiff; application=geotiff",
    "ex:crs": "EPSG:32635",
    "hadMember": [
      "Sakar_complete_months_2021_2025_2021_01_indices_savi.tif",
      "Sakar_complete_months_2021_2025_2021_02_indices_savi.tif"
    ],
    "wasGeneratedBy": "ex:step1_bap",
    "generatedAtTime": "2026-08-21T10:42:00Z",
    "wasDerivedFrom": "https://openeo.example.org/collections/SENTINEL2_L2",
    "wasAttributedTo": "https://orcid.org/0000-0003-4718-2959"
  },

  {
    "id": "ex:bap_cogs",
    "provType": "Entity",
    "entityType": "prov:Collection",
    "dct:title": "Best available pixel composites (Cloud Optimized GeoTIFF, EPSG:3857)",
    "dct:format": "image/tiff; application=geotiff; profile=cloud-optimized",
    "ex:crs": "EPSG:3857",
    "hadMember": [
      "https://example.org/data/bap/Sakar_complete_months_2021_2025_2021_01_indices_savi.tif",
      "https://example.org/data/bap/Sakar_complete_months_2021_2025_2021_02_indices_savi.tif"
    ],
    "wasGeneratedBy": "ex:step1_post_a_bap_reprojection_and_cog_conversion",
    "generatedAtTime": "2026-08-21T10:46:00Z",
    "wasDerivedFrom": "ex:bap_results",
    "wasAttributedTo": "https://orcid.org/0000-0003-4718-2959"
  },

  {
    "id": "https://example.org/stac/collections/bap",
    "provType": "Entity",
    "entityType": "prov:Collection",
    "dct:title": "Best available pixels from Sentinel-2 scenes over AOI",
    "conformsTo": "https://schemas.stacspec.org/v1.0.0/collection-spec/json-schema/collection.json",
    "hadMember": [
      "https://example.org/stac/collections/bap/items/Sakar_complete_months_2021_2025_2021_01_indices_savi",
      "https://example.org/stac/collections/bap/items/Sakar_complete_months_2021_2025_2021_02_indices_savi"
    ],
    "wasGeneratedBy": "ex:step1_post_b_bap_stac_metadata",
    "generatedAtTime": "2026-08-21T10:49:00Z",
    "wasDerivedFrom": "ex:bap_cogs",
    "wasAttributedTo": "https://orcid.org/0000-0003-4718-2959",
    "spdx:checksum": {
      "spdx:algorithm": "spdx:checksumAlgorithm_sha256",
      "spdx:checksumValue": "3f1c9a0e7b2d4c6f8a1e5b7d9c0f2a4e6b8d0c1e3f5a7b9d2c4e6f8a0b1c3d5e"
    }
  },

  {
    "id": "ex:vegetation_productivity_flow",
    "provType": "Entity",
    "entityType": ["prov:Plan", "schema:SoftwareSourceCode", "acttype:WorkflowPlan"],
    "dct:title": "Vegetation productivity trend workflow (Prefect flow)",
    "ex:flowName": "vegetation-productivity-trend",
    "schema:codeRepository": "https://github.com/example-org/people-ecco-workflows",
    "schema:version": "0.4.0",
    "schema:programmingLanguage": "Python",
    "wasAttributedTo": "https://orcid.org/0000-0003-4718-2959"
  },

  {
    "id": "ex:bap_process_graph",
    "provType": "Entity",
    "entityType": "prov:Plan",
    "dct:title": "Best available pixel in timeseries over AOI",
    "openeo:processId": "bap"
  },

  {
    "id": "ex:sen_slope_algorithm",
    "provType": "Entity",
    "entityType": ["prov:Plan", "schema:SoftwareSourceCode"],
    "dct:title": "Seasonal Sen slope trend estimator",
    "schema:codeRepository": "https://github.com/example-org/seasonal-sen-slope",
    "schema:version": "1.2.0",
    "schema:programmingLanguage": "Python",
    "seeAlso": "https://en.wikipedia.org/wiki/Theil%E2%80%93Sen_estimator"
  },

  {
    "id": "ex:postprocessing_code",
    "provType": "Entity",
    "entityType": ["prov:Plan", "schema:SoftwareSourceCode"],
    "dct:title": "Post-processing: reprojection, COG conversion and STAC metadata creation",
    "schema:codeRepository": "https://github.com/example-org/ecco-postprocessing",
    "schema:version": "0.6.1",
    "schema:programmingLanguage": "Python"
  },

  {
    "id": "ex:workflow_parameters",
    "provType": "Entity",
    "entityType": "ex:ProcessInputs",
    "dct:title": "Input parameters of the vegetation productivity trend workflow",
    "ex:bbox": { "@list": [26.45329, 41.8569712, 26.5792884, 41.9825977] },
    "ex:startDate": "2021-01-01",
    "ex:endDate": "2025-12-31",
    "ex:bands": ["B04", "B08", "SCL"],
    "ex:vegetationIndex": "SAVI",
    "ex:seasonLength": 12,
    "ex:significanceLevel": 0.05
  },

  {
    "id": "ex:sen_slope_results",
    "provType": "Entity",
    "entityType": "prov:Collection",
    "dct:title": "Seasonal Sen slope results (Cloud Optimized GeoTIFF)",
    "dct:format": "image/tiff; application=geotiff; profile=cloud-optimized",
    "hadMember": [
      "https://example.org/data/sen/DeltaIR_SAVI.tif",
      "https://example.org/data/sen/PercentChange_SAVI.tif"
    ],
    "wasGeneratedBy": "ex:step2_seasonal_sen_slope",
    "generatedAtTime": "2026-08-21T11:02:00Z",
    "wasDerivedFrom": "https://example.org/stac/collections/bap",
    "wasAttributedTo": "https://orcid.org/0000-0003-4718-2959"
  },

  {
    "id": "https://example.org/stac/collections/sen",
    "provType": "Entity",
    "entityType": "prov:Collection",
    "dct:title": "Seasonal Sen Slope",
    "conformsTo": "https://schemas.stacspec.org/v1.0.0/collection-spec/json-schema/collection.json",
    "hadMember": [
      "https://example.org/stac/collections/sen/items/DeltaIR_SAVI",
      "https://example.org/stac/collections/sen/items/PercentChange_SAVI"
    ],
    "wasGeneratedBy": "ex:step2_post_sen_stac_metadata",
    "generatedAtTime": "2026-08-21T11:06:00Z",
    "wasDerivedFrom": "ex:sen_slope_results",
    "wasAttributedTo": "https://orcid.org/0000-0003-4718-2959",
    "spdx:checksum": {
      "spdx:algorithm": "spdx:checksumAlgorithm_sha256",
      "spdx:checksumValue": "a7d2e4f6081b3c5d7e9f0a2b4c6d8e0f1a3b5c7d9e1f2a4b6c8d0e2f4a6b8c0d"
    }
  },

  {
    "id": "ex:vegetation_productivity_run",
    "provType": "Activity",
    "activityType": "acttype:WorkflowRun",
    "rdfs:label": "Vegetation productivity trend workflow run",
    "startedAtTime": "2026-08-21T10:00:00Z",
    "endedAtTime": "2026-08-21T11:07:00Z",
    "ex:prefectFlowRunId": "3f6a1c2e-8b4d-4e7a-9c1f-5d2b7e8a9f01",
    "used": [
      "https://openeo.example.org/collections/SENTINEL2_L2",
      "ex:workflow_parameters"
    ],
    "generated": "https://example.org/stac/collections/sen",
    "qualifiedAssociation": {
      "agent": "ex:prefect",
      "hadPlan": "ex:vegetation_productivity_flow"
    }
  },

  {
    "id": "ex:step1_bap",
    "provType": "Activity",
    "activityType": [
      "openeo:BatchJob",
      "https://w3id.org/ogc/ospd/activity-type/GA016"
    ],
    "rdfs:label": "Step 1: Best available pixel composites",
    "startedAtTime": "2026-08-21T10:00:10Z",
    "endedAtTime": "2026-08-21T10:42:00Z",
    "isPartOf": "ex:vegetation_productivity_run",
    "openeo:jobId": "j-2608251100",
    "used": ["https://openeo.example.org/collections/SENTINEL2_L2", "ex:workflow_parameters"],
    "qualifiedAssociation": [
      { "agent": "ex:prefect" },
      { "agent": "ex:openeo_client", "hadPlan": "ex:bap_process_graph" },
      { "agent": "ex:openeo_backend", "hadPlan": "ex:bap_process_graph" }
    ]
  },

  {
    "id": "ex:step1_post_a_bap_reprojection_and_cog_conversion",
    "provType": "Activity",
    "activityType": [
      "https://w3id.org/ogc/ospd/activity-type/GA018",
      "https://w3id.org/ogc/ospd/activity-type/cog-conversion"
    ],
    "rdfs:label": "Step 1 post-processing a: reproject best available pixel composites to EPSG:3857 and convert them to Cloud Optimized GeoTIFFs",
    "ex:targetCrs": "EPSG:3857",
    "startedAtTime": "2026-08-21T10:42:00Z",
    "endedAtTime": "2026-08-21T10:46:00Z",
    "isPartOf": "ex:vegetation_productivity_run",
    "used": "ex:bap_results",
    "wasInformedBy": "ex:step1_bap",
    "qualifiedAssociation": [
      { "agent": "ex:prefect" },
      { "agent": "ex:postprocessing_container", "hadPlan": "ex:postprocessing_code" },
      { "agent": "ex:gdal" }
    ]
  },

  {
    "id": "ex:step1_post_b_bap_stac_metadata",
    "provType": "Activity",
    "activityType": ["https://w3id.org/ogc/ospd/activity-type/catalog-export"],
    "rdfs:label": "Step 1 post-processing b: create STAC metadata for the best available pixel composites",
    "rdfs:comment": "Creates STAC collection and items for the COGs and embeds the available provenance information: openEO process graph, processing backend and input parameters.",
    "startedAtTime": "2026-08-21T10:46:00Z",
    "endedAtTime": "2026-08-21T10:49:00Z",
    "isPartOf": "ex:vegetation_productivity_run",
    "used": [
      "ex:bap_cogs",
      "ex:bap_process_graph",
      "ex:workflow_parameters"
    ],
    "wasInformedBy": ["ex:step1_bap", "ex:step1_post_a_bap_reprojection_and_cog_conversion"],
    "qualifiedAssociation": [
      { "agent": "ex:prefect" },
      { "agent": "ex:postprocessing_container", "hadPlan": "ex:postprocessing_code" },
      { "agent": "ex:pystac" }
    ]
  },

  {
    "id": "ex:step2_seasonal_sen_slope",
    "provType": "Activity",
    "activityType": "https://w3id.org/ogc/ospd/activity-type/GA017",
    "rdfs:label": "Step 2: Seasonal Sen slope trend analysis",
    "startedAtTime": "2026-08-21T10:50:00Z",
    "endedAtTime": "2026-08-21T11:02:00Z",
    "isPartOf": "ex:vegetation_productivity_run",
    "used": ["https://example.org/stac/collections/bap", "ex:workflow_parameters"],
    "wasInformedBy": "ex:step1_post_b_bap_stac_metadata",
    "qualifiedAssociation": [
      { "agent": "ex:prefect" },
      { "agent": "ex:sen_slope_container", "hadPlan": "ex:sen_slope_algorithm" }
    ]
  },

  {
    "id": "ex:step2_post_sen_stac_metadata",
    "provType": "Activity",
    "activityType": ["https://w3id.org/ogc/ospd/activity-type/catalog-export"],
    "rdfs:label": "Step 2 post-processing: create STAC metadata for the Sen slope results",
    "rdfs:comment": "Creates STAC collection and items for the COGs and embeds the available provenance information: algorithm repository and version, processing backend and input parameters.",
    "startedAtTime": "2026-08-21T11:02:00Z",
    "endedAtTime": "2026-08-21T11:06:00Z",
    "isPartOf": "ex:vegetation_productivity_run",
    "used": [
      "ex:sen_slope_results",
      "ex:sen_slope_algorithm",
      "ex:workflow_parameters",
      "ex:bap_process_graph"
    ],
    "wasInformedBy": "ex:step2_seasonal_sen_slope",
    "qualifiedAssociation": [
      { "agent": "ex:prefect" },
      { "agent": "ex:postprocessing_container", "hadPlan": "ex:postprocessing_code" },
      { "agent": "ex:pystac" }
    ]
  },

  {
    "id": "https://orcid.org/0000-0003-4718-2959",
    "provType": "Agent",
    "agentType": "prov:Person",
    "rdfs:label": "GIS Analyst",
    "schema:identifier": "https://orcid.org/0000-0003-4718-2959"
  },

  {
    "id": "ex:prefect",
    "provType": "Agent",
    "agentType": ["prov:SoftwareAgent", "schema:SoftwareApplication", "acttype:WorkflowRunner"],
    "rdfs:label": "Prefect",
    "schema:softwareVersion": "3.9.4",
    "seeAlso": "https://www.prefect.io/",
    "actedOnBehalfOf": "https://orcid.org/0000-0003-4718-2959"
  },

  {
    "id": "ex:openeo_client",
    "provType": "Agent",
    "agentType": ["prov:SoftwareAgent", "schema:SoftwareApplication"],
    "rdfs:label": "openeo-python-client",
    "schema:softwareVersion": "0.31.0",
    "qualifiedDelegation": { "agent": "ex:prefect", "hadActivity": "ex:step1_bap" }
  },

  {
    "id": "ex:openeo_backend",
    "provType": "Agent",
    "agentType": ["prov:SoftwareAgent", "openeo:Backend"],
    "rdfs:label": "openEO backend",
    "ex:backendUrl": "https://openeo.example.org",
    "qualifiedDelegation": { "agent": "ex:openeo_client", "hadActivity": "ex:step1_bap" }
  },

  {
    "id": "ex:sen_slope_container",
    "provType": "Agent",
    "agentType": ["prov:SoftwareAgent", "ex:Container"],
    "rdfs:label": "Seasonal Sen slope container",
    "ex:containerImage": "ghcr.io/example-org/ecco-sen-slope:1.2.0",
    "ex:baseImage": "ecco-algorithm-base:1.1.0",
    "qualifiedDelegation": { "agent": "ex:prefect", "hadActivity": "ex:step2_seasonal_sen_slope" }
  },

  {
    "id": "ex:postprocessing_container",
    "provType": "Agent",
    "agentType": ["prov:SoftwareAgent", "ex:Container"],
    "rdfs:label": "Post-processing container",
    "ex:containerImage": "ghcr.io/example-org/ecco-postprocessing:0.6.1",
    "ex:baseImage": "ecco-algorithm-base:1.1.0",
    "actedOnBehalfOf": "ex:prefect"
  },

  {
    "id": "ex:gdal",
    "provType": "Agent",
    "agentType": ["prov:SoftwareAgent", "schema:SoftwareApplication"],
    "rdfs:label": "GDAL (gdalwarp, COG driver)",
    "schema:softwareVersion": "3.9.2",
    "actedOnBehalfOf": "ex:postprocessing_container"
  },

  {
    "id": "ex:pystac",
    "provType": "Agent",
    "agentType": ["prov:SoftwareAgent", "schema:SoftwareApplication"],
    "rdfs:label": "PySTAC",
    "schema:softwareVersion": "1.10.1",
    "actedOnBehalfOf": "ex:postprocessing_container"
  }
]

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/prov-examples/52n-provenance/vegetation-productivity/context.jsonld",
  "@graph": [
    {
      "id": "https://openeo.example.org/collections/SENTINEL2_L2",
      "provType": "Entity",
      "entityType": "prov:Collection",
      "dct:title": "Sentinel-2 L2A surface reflectance",
      "dct:description": "Copernicus Sentinel-2 MSI Level-2A bottom-of-atmosphere reflectance, atmospherically corrected with Sen2Cor and including the scene classification layer (SCL), as offered by the openEO backend.",
      "dct:identifier": "SENTINEL2_L2",
      "dct:publisher": "European Space Agency (ESA), Copernicus Programme",
      "license": "https://sentinels.copernicus.eu/documents/247904/690755/Sentinel_Data_Legal_Notice",
      "ex:mission": "Sentinel-2",
      "ex:instrument": "MSI",
      "ex:processingLevel": "L2A",
      "ex:spatialResolution": "10 m (B02, B03, B04, B08), 20 m (B05-B07, B8A, B11, B12, SCL), 60 m (B01, B09)",
      "ex:revisitTime": "5 days",
      "seeAlso": "https://documentation.dataspace.copernicus.eu/Data/SentinelMissions/Sentinel2.html"
    },
    {
      "id": "ex:bap_results",
      "provType": "Entity",
      "entityType": "prov:Collection",
      "dct:title": "Best available pixel composites (plain GeoTIFF)",
      "dct:format": "image/tiff; application=geotiff",
      "ex:crs": "EPSG:32635",
      "hadMember": [
        "Sakar_complete_months_2021_2025_2021_01_indices_savi.tif",
        "Sakar_complete_months_2021_2025_2021_02_indices_savi.tif"
      ],
      "wasGeneratedBy": "ex:step1_bap",
      "generatedAtTime": "2026-08-21T10:42:00Z",
      "wasDerivedFrom": "https://openeo.example.org/collections/SENTINEL2_L2",
      "wasAttributedTo": "https://orcid.org/0000-0003-4718-2959"
    },
    {
      "id": "ex:bap_cogs",
      "provType": "Entity",
      "entityType": "prov:Collection",
      "dct:title": "Best available pixel composites (Cloud Optimized GeoTIFF, EPSG:3857)",
      "dct:format": "image/tiff; application=geotiff; profile=cloud-optimized",
      "ex:crs": "EPSG:3857",
      "hadMember": [
        "https://example.org/data/bap/Sakar_complete_months_2021_2025_2021_01_indices_savi.tif",
        "https://example.org/data/bap/Sakar_complete_months_2021_2025_2021_02_indices_savi.tif"
      ],
      "wasGeneratedBy": "ex:step1_post_a_bap_reprojection_and_cog_conversion",
      "generatedAtTime": "2026-08-21T10:46:00Z",
      "wasDerivedFrom": "ex:bap_results",
      "wasAttributedTo": "https://orcid.org/0000-0003-4718-2959"
    },
    {
      "id": "https://example.org/stac/collections/bap",
      "provType": "Entity",
      "entityType": "prov:Collection",
      "dct:title": "Best available pixels from Sentinel-2 scenes over AOI",
      "conformsTo": "https://schemas.stacspec.org/v1.0.0/collection-spec/json-schema/collection.json",
      "hadMember": [
        "https://example.org/stac/collections/bap/items/Sakar_complete_months_2021_2025_2021_01_indices_savi",
        "https://example.org/stac/collections/bap/items/Sakar_complete_months_2021_2025_2021_02_indices_savi"
      ],
      "wasGeneratedBy": "ex:step1_post_b_bap_stac_metadata",
      "generatedAtTime": "2026-08-21T10:49:00Z",
      "wasDerivedFrom": "ex:bap_cogs",
      "wasAttributedTo": "https://orcid.org/0000-0003-4718-2959",
      "spdx:checksum": {
        "spdx:algorithm": "spdx:checksumAlgorithm_sha256",
        "spdx:checksumValue": "3f1c9a0e7b2d4c6f8a1e5b7d9c0f2a4e6b8d0c1e3f5a7b9d2c4e6f8a0b1c3d5e"
      }
    },
    {
      "id": "ex:vegetation_productivity_flow",
      "provType": "Entity",
      "entityType": [
        "prov:Plan",
        "schema:SoftwareSourceCode",
        "acttype:WorkflowPlan"
      ],
      "dct:title": "Vegetation productivity trend workflow (Prefect flow)",
      "ex:flowName": "vegetation-productivity-trend",
      "schema:codeRepository": "https://github.com/example-org/people-ecco-workflows",
      "schema:version": "0.4.0",
      "schema:programmingLanguage": "Python",
      "wasAttributedTo": "https://orcid.org/0000-0003-4718-2959"
    },
    {
      "id": "ex:bap_process_graph",
      "provType": "Entity",
      "entityType": "prov:Plan",
      "dct:title": "Best available pixel in timeseries over AOI",
      "openeo:processId": "bap"
    },
    {
      "id": "ex:sen_slope_algorithm",
      "provType": "Entity",
      "entityType": [
        "prov:Plan",
        "schema:SoftwareSourceCode"
      ],
      "dct:title": "Seasonal Sen slope trend estimator",
      "schema:codeRepository": "https://github.com/example-org/seasonal-sen-slope",
      "schema:version": "1.2.0",
      "schema:programmingLanguage": "Python",
      "seeAlso": "https://en.wikipedia.org/wiki/Theil%E2%80%93Sen_estimator"
    },
    {
      "id": "ex:postprocessing_code",
      "provType": "Entity",
      "entityType": [
        "prov:Plan",
        "schema:SoftwareSourceCode"
      ],
      "dct:title": "Post-processing: reprojection, COG conversion and STAC metadata creation",
      "schema:codeRepository": "https://github.com/example-org/ecco-postprocessing",
      "schema:version": "0.6.1",
      "schema:programmingLanguage": "Python"
    },
    {
      "id": "ex:workflow_parameters",
      "provType": "Entity",
      "entityType": "ex:ProcessInputs",
      "dct:title": "Input parameters of the vegetation productivity trend workflow",
      "ex:bbox": {
        "@list": [
          26.45329,
          41.8569712,
          26.5792884,
          41.9825977
        ]
      },
      "ex:startDate": "2021-01-01",
      "ex:endDate": "2025-12-31",
      "ex:bands": [
        "B04",
        "B08",
        "SCL"
      ],
      "ex:vegetationIndex": "SAVI",
      "ex:seasonLength": 12,
      "ex:significanceLevel": 0.05
    },
    {
      "id": "ex:sen_slope_results",
      "provType": "Entity",
      "entityType": "prov:Collection",
      "dct:title": "Seasonal Sen slope results (Cloud Optimized GeoTIFF)",
      "dct:format": "image/tiff; application=geotiff; profile=cloud-optimized",
      "hadMember": [
        "https://example.org/data/sen/DeltaIR_SAVI.tif",
        "https://example.org/data/sen/PercentChange_SAVI.tif"
      ],
      "wasGeneratedBy": "ex:step2_seasonal_sen_slope",
      "generatedAtTime": "2026-08-21T11:02:00Z",
      "wasDerivedFrom": "https://example.org/stac/collections/bap",
      "wasAttributedTo": "https://orcid.org/0000-0003-4718-2959"
    },
    {
      "id": "https://example.org/stac/collections/sen",
      "provType": "Entity",
      "entityType": "prov:Collection",
      "dct:title": "Seasonal Sen Slope",
      "conformsTo": "https://schemas.stacspec.org/v1.0.0/collection-spec/json-schema/collection.json",
      "hadMember": [
        "https://example.org/stac/collections/sen/items/DeltaIR_SAVI",
        "https://example.org/stac/collections/sen/items/PercentChange_SAVI"
      ],
      "wasGeneratedBy": "ex:step2_post_sen_stac_metadata",
      "generatedAtTime": "2026-08-21T11:06:00Z",
      "wasDerivedFrom": "ex:sen_slope_results",
      "wasAttributedTo": "https://orcid.org/0000-0003-4718-2959",
      "spdx:checksum": {
        "spdx:algorithm": "spdx:checksumAlgorithm_sha256",
        "spdx:checksumValue": "a7d2e4f6081b3c5d7e9f0a2b4c6d8e0f1a3b5c7d9e1f2a4b6c8d0e2f4a6b8c0d"
      }
    },
    {
      "id": "ex:vegetation_productivity_run",
      "provType": "Activity",
      "activityType": "acttype:WorkflowRun",
      "rdfs:label": "Vegetation productivity trend workflow run",
      "startedAtTime": "2026-08-21T10:00:00Z",
      "endedAtTime": "2026-08-21T11:07:00Z",
      "ex:prefectFlowRunId": "3f6a1c2e-8b4d-4e7a-9c1f-5d2b7e8a9f01",
      "used": [
        "https://openeo.example.org/collections/SENTINEL2_L2",
        "ex:workflow_parameters"
      ],
      "generated": "https://example.org/stac/collections/sen",
      "qualifiedAssociation": {
        "agent": "ex:prefect",
        "hadPlan": "ex:vegetation_productivity_flow"
      }
    },
    {
      "id": "ex:step1_bap",
      "provType": "Activity",
      "activityType": [
        "openeo:BatchJob",
        "https://w3id.org/ogc/ospd/activity-type/GA016"
      ],
      "rdfs:label": "Step 1: Best available pixel composites",
      "startedAtTime": "2026-08-21T10:00:10Z",
      "endedAtTime": "2026-08-21T10:42:00Z",
      "isPartOf": "ex:vegetation_productivity_run",
      "openeo:jobId": "j-2608251100",
      "used": [
        "https://openeo.example.org/collections/SENTINEL2_L2",
        "ex:workflow_parameters"
      ],
      "qualifiedAssociation": [
        {
          "agent": "ex:prefect"
        },
        {
          "agent": "ex:openeo_client",
          "hadPlan": "ex:bap_process_graph"
        },
        {
          "agent": "ex:openeo_backend",
          "hadPlan": "ex:bap_process_graph"
        }
      ]
    },
    {
      "id": "ex:step1_post_a_bap_reprojection_and_cog_conversion",
      "provType": "Activity",
      "activityType": [
        "https://w3id.org/ogc/ospd/activity-type/GA018",
        "https://w3id.org/ogc/ospd/activity-type/cog-conversion"
      ],
      "rdfs:label": "Step 1 post-processing a: reproject best available pixel composites to EPSG:3857 and convert them to Cloud Optimized GeoTIFFs",
      "ex:targetCrs": "EPSG:3857",
      "startedAtTime": "2026-08-21T10:42:00Z",
      "endedAtTime": "2026-08-21T10:46:00Z",
      "isPartOf": "ex:vegetation_productivity_run",
      "used": "ex:bap_results",
      "wasInformedBy": "ex:step1_bap",
      "qualifiedAssociation": [
        {
          "agent": "ex:prefect"
        },
        {
          "agent": "ex:postprocessing_container",
          "hadPlan": "ex:postprocessing_code"
        },
        {
          "agent": "ex:gdal"
        }
      ]
    },
    {
      "id": "ex:step1_post_b_bap_stac_metadata",
      "provType": "Activity",
      "activityType": [
        "https://w3id.org/ogc/ospd/activity-type/catalog-export"
      ],
      "rdfs:label": "Step 1 post-processing b: create STAC metadata for the best available pixel composites",
      "rdfs:comment": "Creates STAC collection and items for the COGs and embeds the available provenance information: openEO process graph, processing backend and input parameters.",
      "startedAtTime": "2026-08-21T10:46:00Z",
      "endedAtTime": "2026-08-21T10:49:00Z",
      "isPartOf": "ex:vegetation_productivity_run",
      "used": [
        "ex:bap_cogs",
        "ex:bap_process_graph",
        "ex:workflow_parameters"
      ],
      "wasInformedBy": [
        "ex:step1_bap",
        "ex:step1_post_a_bap_reprojection_and_cog_conversion"
      ],
      "qualifiedAssociation": [
        {
          "agent": "ex:prefect"
        },
        {
          "agent": "ex:postprocessing_container",
          "hadPlan": "ex:postprocessing_code"
        },
        {
          "agent": "ex:pystac"
        }
      ]
    },
    {
      "id": "ex:step2_seasonal_sen_slope",
      "provType": "Activity",
      "activityType": "https://w3id.org/ogc/ospd/activity-type/GA017",
      "rdfs:label": "Step 2: Seasonal Sen slope trend analysis",
      "startedAtTime": "2026-08-21T10:50:00Z",
      "endedAtTime": "2026-08-21T11:02:00Z",
      "isPartOf": "ex:vegetation_productivity_run",
      "used": [
        "https://example.org/stac/collections/bap",
        "ex:workflow_parameters"
      ],
      "wasInformedBy": "ex:step1_post_b_bap_stac_metadata",
      "qualifiedAssociation": [
        {
          "agent": "ex:prefect"
        },
        {
          "agent": "ex:sen_slope_container",
          "hadPlan": "ex:sen_slope_algorithm"
        }
      ]
    },
    {
      "id": "ex:step2_post_sen_stac_metadata",
      "provType": "Activity",
      "activityType": [
        "https://w3id.org/ogc/ospd/activity-type/catalog-export"
      ],
      "rdfs:label": "Step 2 post-processing: create STAC metadata for the Sen slope results",
      "rdfs:comment": "Creates STAC collection and items for the COGs and embeds the available provenance information: algorithm repository and version, processing backend and input parameters.",
      "startedAtTime": "2026-08-21T11:02:00Z",
      "endedAtTime": "2026-08-21T11:06:00Z",
      "isPartOf": "ex:vegetation_productivity_run",
      "used": [
        "ex:sen_slope_results",
        "ex:sen_slope_algorithm",
        "ex:workflow_parameters",
        "ex:bap_process_graph"
      ],
      "wasInformedBy": "ex:step2_seasonal_sen_slope",
      "qualifiedAssociation": [
        {
          "agent": "ex:prefect"
        },
        {
          "agent": "ex:postprocessing_container",
          "hadPlan": "ex:postprocessing_code"
        },
        {
          "agent": "ex:pystac"
        }
      ]
    },
    {
      "id": "https://orcid.org/0000-0003-4718-2959",
      "provType": "Agent",
      "agentType": "prov:Person",
      "rdfs:label": "GIS Analyst",
      "schema:identifier": "https://orcid.org/0000-0003-4718-2959"
    },
    {
      "id": "ex:prefect",
      "provType": "Agent",
      "agentType": [
        "prov:SoftwareAgent",
        "schema:SoftwareApplication",
        "acttype:WorkflowRunner"
      ],
      "rdfs:label": "Prefect",
      "schema:softwareVersion": "3.9.4",
      "seeAlso": "https://www.prefect.io/",
      "actedOnBehalfOf": "https://orcid.org/0000-0003-4718-2959"
    },
    {
      "id": "ex:openeo_client",
      "provType": "Agent",
      "agentType": [
        "prov:SoftwareAgent",
        "schema:SoftwareApplication"
      ],
      "rdfs:label": "openeo-python-client",
      "schema:softwareVersion": "0.31.0",
      "qualifiedDelegation": {
        "agent": "ex:prefect",
        "hadActivity": "ex:step1_bap"
      }
    },
    {
      "id": "ex:openeo_backend",
      "provType": "Agent",
      "agentType": [
        "prov:SoftwareAgent",
        "openeo:Backend"
      ],
      "rdfs:label": "openEO backend",
      "ex:backendUrl": "https://openeo.example.org",
      "qualifiedDelegation": {
        "agent": "ex:openeo_client",
        "hadActivity": "ex:step1_bap"
      }
    },
    {
      "id": "ex:sen_slope_container",
      "provType": "Agent",
      "agentType": [
        "prov:SoftwareAgent",
        "ex:Container"
      ],
      "rdfs:label": "Seasonal Sen slope container",
      "ex:containerImage": "ghcr.io/example-org/ecco-sen-slope:1.2.0",
      "ex:baseImage": "ecco-algorithm-base:1.1.0",
      "qualifiedDelegation": {
        "agent": "ex:prefect",
        "hadActivity": "ex:step2_seasonal_sen_slope"
      }
    },
    {
      "id": "ex:postprocessing_container",
      "provType": "Agent",
      "agentType": [
        "prov:SoftwareAgent",
        "ex:Container"
      ],
      "rdfs:label": "Post-processing container",
      "ex:containerImage": "ghcr.io/example-org/ecco-postprocessing:0.6.1",
      "ex:baseImage": "ecco-algorithm-base:1.1.0",
      "actedOnBehalfOf": "ex:prefect"
    },
    {
      "id": "ex:gdal",
      "provType": "Agent",
      "agentType": [
        "prov:SoftwareAgent",
        "schema:SoftwareApplication"
      ],
      "rdfs:label": "GDAL (gdalwarp, COG driver)",
      "schema:softwareVersion": "3.9.2",
      "actedOnBehalfOf": "ex:postprocessing_container"
    },
    {
      "id": "ex:pystac",
      "provType": "Agent",
      "agentType": [
        "prov:SoftwareAgent",
        "schema:SoftwareApplication"
      ],
      "rdfs:label": "PySTAC",
      "schema:softwareVersion": "1.10.1",
      "actedOnBehalfOf": "ex:postprocessing_container"
    }
  ]
}
```

#### ttl
```ttl
@prefix acttype: <https://w3id.org/ogc/rim/activity-type/> .
@prefix dcterms: <http://purl.org/dc/terms/> .
@prefix ex: <https://example.org/vegetation-productivity#> .
@prefix openeo: <https://example.org/openeo#> .
@prefix prov: <http://www.w3.org/ns/prov#> .
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix schema: <https://schema.org/> .
@prefix spdx: <http://spdx.org/rdf/terms#> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

<https://example.org/stac/collections/sen> a prov:Collection,
        prov:Entity ;
    rdfs:label "Seasonal Sen Slope" ;
    dcterms:conformsTo <https://schemas.stacspec.org/v1.0.0/collection-spec/json-schema/collection.json> ;
    dcterms:title "Seasonal Sen Slope" ;
    spdx:checksum [ spdx:algorithm spdx:checksumAlgorithm_sha256 ;
            spdx:checksumValue "a7d2e4f6081b3c5d7e9f0a2b4c6d8e0f1a3b5c7d9e1f2a4b6c8d0e2f4a6b8c0d" ] ;
    prov:generatedAtTime "2026-08-21T11:06:00+00:00"^^xsd:dateTime ;
    prov:hadMember <https://example.org/stac/collections/sen/items/DeltaIR_SAVI>,
        <https://example.org/stac/collections/sen/items/PercentChange_SAVI> ;
    prov:type prov:Collection ;
    prov:wasAttributedTo <https://orcid.org/0000-0003-4718-2959> ;
    prov:wasDerivedFrom ex:sen_slope_results ;
    prov:wasGeneratedBy ex:step2_post_sen_stac_metadata .

ex:gdal a prov:Agent,
        prov:SoftwareAgent ;
    rdfs:label "GDAL (gdalwarp, COG driver)" ;
    prov:actedOnBehalfOf ex:postprocessing_container ;
    prov:type prov:SoftwareAgent,
        schema:SoftwareApplication ;
    schema:softwareVersion "3.9.2" .

ex:openeo_backend a prov:Agent,
        prov:SoftwareAgent ;
    rdfs:label "openEO backend" ;
    prov:qualifiedDelegation [ prov:agent ex:openeo_client ;
            prov:hadActivity ex:step1_bap ] ;
    prov:type prov:SoftwareAgent,
        openeo:Backend ;
    ex:backendUrl "https://openeo.example.org" .

ex:sen_slope_container a prov:Agent,
        prov:SoftwareAgent ;
    rdfs:label "Seasonal Sen slope container" ;
    prov:qualifiedDelegation [ prov:agent ex:prefect ;
            prov:hadActivity ex:step2_seasonal_sen_slope ] ;
    prov:type prov:SoftwareAgent,
        ex:Container ;
    ex:baseImage "ecco-algorithm-base:1.1.0" ;
    ex:containerImage "ghcr.io/example-org/ecco-sen-slope:1.2.0" .

ex:step2_post_sen_stac_metadata a prov:Activity ;
    rdfs:label "Step 2 post-processing: create STAC metadata for the Sen slope results" ;
    dcterms:isPartOf ex:vegetation_productivity_run ;
    rdfs:comment "Creates STAC collection and items for the COGs and embeds the available provenance information: algorithm repository and version, processing backend and input parameters." ;
    prov:endedAtTime "2026-08-21T11:06:00+00:00"^^xsd:dateTime ;
    prov:qualifiedAssociation [ prov:agent ex:pystac ],
        [ prov:agent ex:postprocessing_container ;
            prov:hadPlan ex:postprocessing_code ],
        [ prov:agent ex:prefect ] ;
    prov:startedAtTime "2026-08-21T11:02:00+00:00"^^xsd:dateTime ;
    prov:type <https://w3id.org/ogc/ospd/activity-type/catalog-export> ;
    prov:used ex:bap_process_graph,
        ex:sen_slope_algorithm,
        ex:sen_slope_results,
        ex:workflow_parameters ;
    prov:wasInformedBy ex:step2_seasonal_sen_slope .

ex:vegetation_productivity_flow a prov:Entity,
        prov:Plan,
        acttype:WorkflowPlan ;
    rdfs:label "Vegetation productivity trend workflow (Prefect flow)" ;
    dcterms:title "Vegetation productivity trend workflow (Prefect flow)" ;
    prov:type prov:Plan,
        schema:SoftwareSourceCode,
        acttype:WorkflowPlan ;
    prov:wasAttributedTo <https://orcid.org/0000-0003-4718-2959> ;
    ex:flowName "vegetation-productivity-trend" ;
    schema:codeRepository "https://github.com/example-org/people-ecco-workflows" ;
    schema:programmingLanguage "Python" ;
    schema:version "0.4.0" .

<https://example.org/stac/collections/bap> a prov:Collection,
        prov:Entity ;
    rdfs:label "Best available pixels from Sentinel-2 scenes over AOI" ;
    dcterms:conformsTo <https://schemas.stacspec.org/v1.0.0/collection-spec/json-schema/collection.json> ;
    dcterms:title "Best available pixels from Sentinel-2 scenes over AOI" ;
    spdx:checksum [ spdx:algorithm spdx:checksumAlgorithm_sha256 ;
            spdx:checksumValue "3f1c9a0e7b2d4c6f8a1e5b7d9c0f2a4e6b8d0c1e3f5a7b9d2c4e6f8a0b1c3d5e" ] ;
    prov:generatedAtTime "2026-08-21T10:49:00+00:00"^^xsd:dateTime ;
    prov:hadMember <https://example.org/stac/collections/bap/items/Sakar_complete_months_2021_2025_2021_01_indices_savi>,
        <https://example.org/stac/collections/bap/items/Sakar_complete_months_2021_2025_2021_02_indices_savi> ;
    prov:type prov:Collection ;
    prov:wasAttributedTo <https://orcid.org/0000-0003-4718-2959> ;
    prov:wasDerivedFrom ex:bap_cogs ;
    prov:wasGeneratedBy ex:step1_post_b_bap_stac_metadata .

ex:bap_cogs a prov:Collection,
        prov:Entity ;
    rdfs:label "Best available pixel composites (Cloud Optimized GeoTIFF, EPSG:3857)" ;
    dcterms:format "image/tiff; application=geotiff; profile=cloud-optimized" ;
    dcterms:title "Best available pixel composites (Cloud Optimized GeoTIFF, EPSG:3857)" ;
    prov:generatedAtTime "2026-08-21T10:46:00+00:00"^^xsd:dateTime ;
    prov:hadMember <https://example.org/data/bap/Sakar_complete_months_2021_2025_2021_01_indices_savi.tif>,
        <https://example.org/data/bap/Sakar_complete_months_2021_2025_2021_02_indices_savi.tif> ;
    prov:type prov:Collection ;
    prov:wasAttributedTo <https://orcid.org/0000-0003-4718-2959> ;
    prov:wasDerivedFrom ex:bap_results ;
    prov:wasGeneratedBy ex:step1_post_a_bap_reprojection_and_cog_conversion ;
    ex:crs "EPSG:3857" .

ex:bap_results a prov:Collection,
        prov:Entity ;
    rdfs:label "Best available pixel composites (plain GeoTIFF)" ;
    dcterms:format "image/tiff; application=geotiff" ;
    dcterms:title "Best available pixel composites (plain GeoTIFF)" ;
    prov:generatedAtTime "2026-08-21T10:42:00+00:00"^^xsd:dateTime ;
    prov:hadMember <file:///github/workspace/Sakar_complete_months_2021_2025_2021_01_indices_savi.tif>,
        <file:///github/workspace/Sakar_complete_months_2021_2025_2021_02_indices_savi.tif> ;
    prov:type prov:Collection ;
    prov:wasAttributedTo <https://orcid.org/0000-0003-4718-2959> ;
    prov:wasDerivedFrom <https://openeo.example.org/collections/SENTINEL2_L2> ;
    prov:wasGeneratedBy ex:step1_bap ;
    ex:crs "EPSG:32635" .

ex:openeo_client a prov:Agent,
        prov:SoftwareAgent ;
    rdfs:label "openeo-python-client" ;
    prov:qualifiedDelegation [ prov:agent ex:prefect ;
            prov:hadActivity ex:step1_bap ] ;
    prov:type prov:SoftwareAgent,
        schema:SoftwareApplication ;
    schema:softwareVersion "0.31.0" .

ex:pystac a prov:Agent,
        prov:SoftwareAgent ;
    rdfs:label "PySTAC" ;
    prov:actedOnBehalfOf ex:postprocessing_container ;
    prov:type prov:SoftwareAgent,
        schema:SoftwareApplication ;
    schema:softwareVersion "1.10.1" .

ex:sen_slope_algorithm a prov:Entity,
        prov:Plan ;
    rdfs:label "Seasonal Sen slope trend estimator" ;
    dcterms:title "Seasonal Sen slope trend estimator" ;
    rdfs:seeAlso <https://en.wikipedia.org/wiki/Theil%E2%80%93Sen_estimator> ;
    prov:type prov:Plan,
        schema:SoftwareSourceCode ;
    schema:codeRepository "https://github.com/example-org/seasonal-sen-slope" ;
    schema:programmingLanguage "Python" ;
    schema:version "1.2.0" .

ex:sen_slope_results a prov:Collection,
        prov:Entity ;
    rdfs:label "Seasonal Sen slope results (Cloud Optimized GeoTIFF)" ;
    dcterms:format "image/tiff; application=geotiff; profile=cloud-optimized" ;
    dcterms:title "Seasonal Sen slope results (Cloud Optimized GeoTIFF)" ;
    prov:generatedAtTime "2026-08-21T11:02:00+00:00"^^xsd:dateTime ;
    prov:hadMember <https://example.org/data/sen/DeltaIR_SAVI.tif>,
        <https://example.org/data/sen/PercentChange_SAVI.tif> ;
    prov:type prov:Collection ;
    prov:wasAttributedTo <https://orcid.org/0000-0003-4718-2959> ;
    prov:wasDerivedFrom <https://example.org/stac/collections/bap> ;
    prov:wasGeneratedBy ex:step2_seasonal_sen_slope .

ex:step1_post_a_bap_reprojection_and_cog_conversion a prov:Activity ;
    rdfs:label "Step 1 post-processing a: reproject best available pixel composites to EPSG:3857 and convert them to Cloud Optimized GeoTIFFs" ;
    dcterms:isPartOf ex:vegetation_productivity_run ;
    prov:endedAtTime "2026-08-21T10:46:00+00:00"^^xsd:dateTime ;
    prov:qualifiedAssociation [ prov:agent ex:gdal ],
        [ prov:agent ex:postprocessing_container ;
            prov:hadPlan ex:postprocessing_code ],
        [ prov:agent ex:prefect ] ;
    prov:startedAtTime "2026-08-21T10:42:00+00:00"^^xsd:dateTime ;
    prov:type <https://w3id.org/ogc/ospd/activity-type/GA018>,
        <https://w3id.org/ogc/ospd/activity-type/cog-conversion> ;
    prov:used ex:bap_results ;
    prov:wasInformedBy ex:step1_bap ;
    ex:targetCrs "EPSG:3857" .

ex:step1_post_b_bap_stac_metadata a prov:Activity ;
    rdfs:label "Step 1 post-processing b: create STAC metadata for the best available pixel composites" ;
    dcterms:isPartOf ex:vegetation_productivity_run ;
    rdfs:comment "Creates STAC collection and items for the COGs and embeds the available provenance information: openEO process graph, processing backend and input parameters." ;
    prov:endedAtTime "2026-08-21T10:49:00+00:00"^^xsd:dateTime ;
    prov:qualifiedAssociation [ prov:agent ex:postprocessing_container ;
            prov:hadPlan ex:postprocessing_code ],
        [ prov:agent ex:prefect ],
        [ prov:agent ex:pystac ] ;
    prov:startedAtTime "2026-08-21T10:46:00+00:00"^^xsd:dateTime ;
    prov:type <https://w3id.org/ogc/ospd/activity-type/catalog-export> ;
    prov:used ex:bap_cogs,
        ex:bap_process_graph,
        ex:workflow_parameters ;
    prov:wasInformedBy ex:step1_bap,
        ex:step1_post_a_bap_reprojection_and_cog_conversion .

ex:postprocessing_code a prov:Entity,
        prov:Plan ;
    rdfs:label "Post-processing: reprojection, COG conversion and STAC metadata creation" ;
    dcterms:title "Post-processing: reprojection, COG conversion and STAC metadata creation" ;
    prov:type prov:Plan,
        schema:SoftwareSourceCode ;
    schema:codeRepository "https://github.com/example-org/ecco-postprocessing" ;
    schema:programmingLanguage "Python" ;
    schema:version "0.6.1" .

ex:step2_seasonal_sen_slope a prov:Activity ;
    rdfs:label "Step 2: Seasonal Sen slope trend analysis" ;
    dcterms:isPartOf ex:vegetation_productivity_run ;
    prov:endedAtTime "2026-08-21T11:02:00+00:00"^^xsd:dateTime ;
    prov:qualifiedAssociation [ prov:agent ex:sen_slope_container ;
            prov:hadPlan ex:sen_slope_algorithm ],
        [ prov:agent ex:prefect ] ;
    prov:startedAtTime "2026-08-21T10:50:00+00:00"^^xsd:dateTime ;
    prov:type <https://w3id.org/ogc/ospd/activity-type/GA017> ;
    prov:used <https://example.org/stac/collections/bap>,
        ex:workflow_parameters ;
    prov:wasInformedBy ex:step1_post_b_bap_stac_metadata .

<https://openeo.example.org/collections/SENTINEL2_L2> a prov:Collection,
        prov:Entity ;
    rdfs:label "Sentinel-2 L2A surface reflectance" ;
    dcterms:description "Copernicus Sentinel-2 MSI Level-2A bottom-of-atmosphere reflectance, atmospherically corrected with Sen2Cor and including the scene classification layer (SCL), as offered by the openEO backend." ;
    dcterms:identifier "SENTINEL2_L2" ;
    dcterms:license <https://sentinels.copernicus.eu/documents/247904/690755/Sentinel_Data_Legal_Notice> ;
    dcterms:publisher "European Space Agency (ESA), Copernicus Programme" ;
    dcterms:title "Sentinel-2 L2A surface reflectance" ;
    rdfs:seeAlso <https://documentation.dataspace.copernicus.eu/Data/SentinelMissions/Sentinel2.html> ;
    prov:type prov:Collection ;
    ex:instrument "MSI" ;
    ex:mission "Sentinel-2" ;
    ex:processingLevel "L2A" ;
    ex:revisitTime "5 days" ;
    ex:spatialResolution "10 m (B02, B03, B04, B08), 20 m (B05-B07, B8A, B11, B12, SCL), 60 m (B01, B09)" .

ex:bap_process_graph a prov:Entity,
        prov:Plan ;
    rdfs:label "Best available pixel in timeseries over AOI" ;
    dcterms:title "Best available pixel in timeseries over AOI" ;
    prov:type prov:Plan ;
    openeo:processId "bap" .

ex:postprocessing_container a prov:Agent,
        prov:SoftwareAgent ;
    rdfs:label "Post-processing container" ;
    prov:actedOnBehalfOf ex:prefect ;
    prov:type prov:SoftwareAgent,
        ex:Container ;
    ex:baseImage "ecco-algorithm-base:1.1.0" ;
    ex:containerImage "ghcr.io/example-org/ecco-postprocessing:0.6.1" .

ex:step1_bap a prov:Activity ;
    rdfs:label "Step 1: Best available pixel composites" ;
    dcterms:isPartOf ex:vegetation_productivity_run ;
    prov:endedAtTime "2026-08-21T10:42:00+00:00"^^xsd:dateTime ;
    prov:qualifiedAssociation [ prov:agent ex:openeo_client ;
            prov:hadPlan ex:bap_process_graph ],
        [ prov:agent ex:openeo_backend ;
            prov:hadPlan ex:bap_process_graph ],
        [ prov:agent ex:prefect ] ;
    prov:startedAtTime "2026-08-21T10:00:10+00:00"^^xsd:dateTime ;
    prov:type openeo:BatchJob,
        <https://w3id.org/ogc/ospd/activity-type/GA016> ;
    prov:used ex:workflow_parameters,
        <https://openeo.example.org/collections/SENTINEL2_L2> ;
    openeo:jobId "j-2608251100" .

ex:vegetation_productivity_run a prov:Activity,
        acttype:WorkflowRun ;
    rdfs:label "Vegetation productivity trend workflow run" ;
    prov:endedAtTime "2026-08-21T11:07:00+00:00"^^xsd:dateTime ;
    prov:generated <https://example.org/stac/collections/sen> ;
    prov:qualifiedAssociation [ prov:agent ex:prefect ;
            prov:hadPlan ex:vegetation_productivity_flow ] ;
    prov:startedAtTime "2026-08-21T10:00:00+00:00"^^xsd:dateTime ;
    prov:type acttype:WorkflowRun ;
    prov:used ex:workflow_parameters,
        <https://openeo.example.org/collections/SENTINEL2_L2> ;
    ex:prefectFlowRunId "3f6a1c2e-8b4d-4e7a-9c1f-5d2b7e8a9f01" .

ex:workflow_parameters a prov:Entity ;
    rdfs:label "Input parameters of the vegetation productivity trend workflow" ;
    dcterms:title "Input parameters of the vegetation productivity trend workflow" ;
    prov:type ex:ProcessInputs ;
    ex:bands "B04",
        "B08",
        "SCL" ;
    ex:bbox ( 2.645329e+01 4.185697e+01 2.657929e+01 4.19826e+01 ) ;
    ex:endDate "2025-12-31" ;
    ex:seasonLength 12 ;
    ex:significanceLevel 5e-02 ;
    ex:startDate "2021-01-01" ;
    ex:vegetationIndex "SAVI" .

<https://orcid.org/0000-0003-4718-2959> a prov:Agent,
        prov:Person ;
    rdfs:label "GIS Analyst" ;
    prov:type prov:Person ;
    schema:identifier "https://orcid.org/0000-0003-4718-2959" .

ex:prefect a prov:Agent,
        prov:SoftwareAgent,
        acttype:WorkflowRunner ;
    rdfs:label "Prefect" ;
    rdfs:seeAlso <https://www.prefect.io/> ;
    prov:actedOnBehalfOf <https://orcid.org/0000-0003-4718-2959> ;
    prov:type prov:SoftwareAgent,
        schema:SoftwareApplication,
        acttype:WorkflowRunner ;
    schema:softwareVersion "3.9.4" .


```

## Schema

```yaml
$schema: https://json-schema.org/draft/2020-12/schema
$ref: https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/prov-profiles/workflow-graph/schema.yaml
x-jsonld-extra-terms:
  spdx:algorithm:
    x-jsonld-type: '@id'
  isPartOf:
    x-jsonld-id: dct:isPartOf
    x-jsonld-type: '@id'
  license:
    x-jsonld-id: dct:license
    x-jsonld-type: '@id'
  conformsTo:
    x-jsonld-id: dct:conformsTo
    x-jsonld-type: '@id'
  seeAlso:
    x-jsonld-id: rdfs:seeAlso
    x-jsonld-type: '@id'
x-jsonld-prefixes:
  ex: https://example.org/vegetation-productivity#
  openeo: https://example.org/openeo#
  schema: https://schema.org/
  spdx: http://spdx.org/rdf/terms#
x-bblocks-metadata:
  itemIdentifier: ogc.osc.prov-examples.52n-provenance.vegetation-productivity
  register: https://ogcincubator.github.io/bblocks-openscience/build/register.json
  version: '0.1'
  dateOfLastChange: '2026-11-26'

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/prov-examples/52n-provenance/vegetation-productivity/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/prov-examples/52n-provenance/vegetation-productivity/schema.yaml)


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
    "label": "rdfs:label",
    "spdx:algorithm": {
      "@type": "@id"
    },
    "isPartOf": {
      "@id": "dct:isPartOf",
      "@type": "@id"
    },
    "license": {
      "@id": "dct:license",
      "@type": "@id"
    },
    "conformsTo": {
      "@id": "dct:conformsTo",
      "@type": "@id"
    },
    "seeAlso": {
      "@id": "rdfs:seeAlso",
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
    "dcterms": "http://purl.org/dc/terms/",
    "skos": "http://www.w3.org/2004/02/skos/core#",
    "acttype": "https://w3id.org/ogc/rim/activity-type/",
    "ex": "https://example.org/vegetation-productivity#",
    "openeo": "https://example.org/openeo#",
    "spdx": "http://spdx.org/rdf/terms#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/prov-examples/52n-provenance/vegetation-productivity/context.jsonld)

## Sources

* [PEOPLE-ECCO](https://www.people-ecco.eu/)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-openscience](https://github.com/ogcincubator/bblocks-openscience)
* Path: `_sources/prov-examples/52n-provenance/vegetation-productivity`

