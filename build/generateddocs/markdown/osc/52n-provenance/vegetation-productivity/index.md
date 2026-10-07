
# Vegetation Productivity Trend Workflow Provenance Profile (Schema)

`ogc.osc.52n-provenance.vegetation-productivity` *v0.1*

Vegetation Productivity Trend Workflow Provenance Profile.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

## Vegetation Productivity Trend Workflow Provenance Profile

This Building Block contains the provenance description of a vegetation productivity trend workflow developed as part of the [PEOPLE-ECCO](https://www.people-ecco.eu/) project and profiled within the [Open Science Persitent Demonstrator 2026](https://www.ogc.org/de/initiatives/open-science-persistent-demonstrator-2026/) initiative.

The provenance representation follows [W3C PROV](https://www.w3.org/TR/prov-overview/), to be more specific its JSON schema as defined in the [Provenance Chain](https://ogcincubator.github.io/bblock-prov-schema/bblock/ogc.ogc-utils.prov) Building Block.


## Examples

### Example from a vegetation productivity trend workflow run from the PEOPLE-ECCO project
#### json
```json
[
  {
    "id": "https://openeo.example.org/collections/SENTINEL2_L2",
    "entityType": ["prov:Entity", "prov:Collection"],
    "dcterms:title": "Sentinel-2 L2A surface reflectance",
    "dcterms:description": "Copernicus Sentinel-2 MSI Level-2A bottom-of-atmosphere reflectance, atmospherically corrected with Sen2Cor and including the scene classification layer (SCL), as offered by the openEO backend.",
    "dcterms:identifier": "SENTINEL2_L2",
    "dcterms:publisher": "European Space Agency (ESA), Copernicus Programme",
    "dcterms:license": "https://sentinels.copernicus.eu/documents/247904/690755/Sentinel_Data_Legal_Notice",
    "ex:mission": "Sentinel-2",
    "ex:instrument": "MSI",
    "ex:processingLevel": "L2A",
    "ex:spatialResolution": "10 m (B02, B03, B04, B08), 20 m (B05-B07, B8A, B11, B12, SCL), 60 m (B01, B09)",
    "ex:revisitTime": "5 days",
    "rdfs:seeAlso": "https://documentation.dataspace.copernicus.eu/Data/SentinelMissions/Sentinel2.html"
  },

  {
    "id": "https://example.org/stac/collections/bap",
    "entityType": ["prov:Entity", "prov:Collection"],
    "dcterms:title": "Best available pixels from Sentinel-2 scenes over AOI",
    "dcterms:conformsTo": "https://schemas.stacspec.org/v1.0.0/collection-spec/json-schema/collection.json",
    "hadMember": [
      "https://example.org/stac/collections/bap/items/Sakar_complete_months_2021_2025_2021_01_indices_savi",
      "https://example.org/stac/collections/bap/items/Sakar_complete_months_2021_2025_2021_02_indices_savi"
    ],
    "wasGeneratedBy": "ex:step1_bap",
    "generatedAtTime": "2026-08-21T10:05:00Z",
    "wasDerivedFrom": "https://openeo.example.org/collections/SENTINEL2_L2",
    "wasAttributedTo": "https://orcid.org/0000-0003-4718-2959",
    "spdx:checksum": {
      "spdx:algorithm": { "@id": "spdx:checksumAlgorithm_sha256" },
      "spdx:checksumValue": "3f1c9a0e7b2d4c6f8a1e5b7d9c0f2a4e6b8d0c1e3f5a7b9d2c4e6f8a0b1c3d5e"
    }
  },

  {
    "id": "ex:bap_process_graph",
    "entityType": ["prov:Entity", "prov:Plan"],
    "dcterms:title": "Best available pixel in timeseries over AOI",
    "openeo:processId": "bap"
  },

  {
    "id": "ex:sen_slope_algorithm",
    "entityType": ["prov:Entity", "prov:Plan", "schema:SoftwareSourceCode"],
    "dcterms:title": "Seasonal Sen slope trend estimator",
    "schema:codeRepository": "https://github.com/example-org/seasonal-sen-slope",
    "schema:version": "1.2.0",
    "schema:programmingLanguage": "Python",
    "rdfs:seeAlso": "https://en.wikipedia.org/wiki/Theil%E2%80%93Sen_estimator"
  },

  {
    "id": "ex:sen_slope_parameters",
    "entityType": ["prov:Entity", "ex:ProcessInputs"],
    "dcterms:title": "Input parameters of the seasonal Sen slope analysis",
    "ex:vegetationIndex": "SAVI",
    "ex:saviSoilFactor": 0.5,
    "ex:startDate": "2021-01-01",
    "ex:endDate": "2025-12-31",
    "ex:seasonLength": 12,
    "ex:significanceLevel": 0.05
  },

  {
    "id": "ex:sen_slope_results",
    "entityType": ["prov:Entity", "prov:Collection"],
    "dcterms:title": "Seasonal Sen slope results (plain GeoTIFF)",
    "dcterms:format": "image/tiff; application=geotiff",
    "hadMember": ["ex:DeltaIR_SAVI_tif", "ex:PercentChange_SAVI_tif"],
    "wasGeneratedBy": "ex:step2_seasonal_sen_slope",
    "generatedAtTime": "2026-08-21T10:12:00Z",
    "wasDerivedFrom": "https://example.org/stac/collections/bap",
    "wasAttributedTo": "https://orcid.org/0000-0003-4718-2959"
  },

  {
    "id": "ex:sen_slope_cogs",
    "entityType": ["prov:Entity", "prov:Collection"],
    "dcterms:title": "Seasonal Sen slope results (Cloud Optimized GeoTIFF)",
    "dcterms:format": "image/tiff; application=geotiff; profile=cloud-optimized",
    "hadMember": [
      "https://example.org/data/sen/DeltaIR_SAVI.tif",
      "https://example.org/data/sen/PercentChange_SAVI.tif"
    ],
    "wasGeneratedBy": "ex:step3a_cog_conversion",
    "generatedAtTime": "2026-08-21T10:28:00Z",
    "wasDerivedFrom": "ex:sen_slope_results",
    "wasAttributedTo": "https://orcid.org/0000-0003-4718-2959"
  },

  {
    "id": "https://example.org/stac/collections/sen",
    "entityType": ["prov:Entity", "prov:Collection"],
    "dcterms:title": "Seasonal Sen Slope",
    "dcterms:conformsTo": "https://schemas.stacspec.org/v1.0.0/collection-spec/json-schema/collection.json",
    "hadMember": [
      "https://example.org/stac/collections/sen/items/DeltaIR_SAVI",
      "https://example.org/stac/collections/sen/items/PercentChange_SAVI"
    ],
    "wasGeneratedBy": "ex:step3b_stac_metadata",
    "generatedAtTime": "2026-08-21T10:45:00Z",
    "wasDerivedFrom": "ex:sen_slope_cogs",
    "wasAttributedTo": "https://orcid.org/0000-0003-4718-2959",
    "spdx:checksum": {
      "spdx:algorithm": { "@id": "spdx:checksumAlgorithm_sha256" },
      "spdx:checksumValue": "a7d2e4f6081b3c5d7e9f0a2b4c6d8e0f1a3b5c7d9e1f2a4b6c8d0e2f4a6b8c0d"
    }
  },

  {
    "id": "ex:step1_bap",
    "activityType": [
      "prov:Activity",
      "openeo:BatchJob",
      "https://catalog.ospd.dev.kurrawong.ai/catalogs/demo:geoacs/collections/demo:ospd-geoacs/items/demo:GA016"
    ],
    "rdfs:label": "Step 1: Best available pixel composites",
    "startedAtTime": "2026-08-21T10:00:00Z",
    "endedAtTime": "2026-08-21T18:05:00Z",
    "openeo:jobId": "j-2608251100",
    "used": "https://openeo.example.org/collections/SENTINEL2_L2",
    "qualifiedUsage": {
      "entity": "https://openeo.example.org/collections/SENTINEL2_L2",
      "ex:bbox": { "@list": [26.45329, 41.8569712, 26.5792884, 41.9825977] },
      "ex:startDate": "2021-01-01",
      "ex:endDate": "2025-12-31",
      "ex:bands": ["B04", "B08", "SCL"]
    },
    "qualifiedAssociation": [
      { "agent": "https://orcid.org/0000-0003-4718-2959", "hadPlan": "ex:bap_process_graph" },
      { "agent": "ex:openeo_client", "hadPlan": "ex:bap_process_graph" },
      { "agent": "ex:openeo_backend", "hadPlan": "ex:bap_process_graph" }
    ]
  },

  {
    "id": "ex:step2_seasonal_sen_slope",
    "activityType": [
      "prov:Activity",
      "https://catalog.ospd.dev.kurrawong.ai/catalogs/demo:geoacs/collections/demo:ospd-geoacs/items/demo:GA017"
    ],
    "rdfs:label": "Step 2: Seasonal Sen slope trend analysis",
    "startedAtTime": "2026-08-21T10:06:00Z",
    "endedAtTime": "2026-08-21T10:12:00Z",
    "used": ["https://example.org/stac/collections/bap", "ex:sen_slope_parameters"],
    "wasInformedBy": "ex:step1_bap",
    "qualifiedAssociation": [
      { "agent": "https://orcid.org/0000-0003-4718-2959", "hadPlan": "ex:sen_slope_algorithm" }
    ]
  },

  {
    "id": "ex:step3a_cog_conversion",
    "activityType": ["prov:Activity", "ex:PostProcessing", "ex:CogConversion"],
    "rdfs:label": "Step 3a: Post-processing - convert results to Cloud Optimized GeoTIFFs",
    "startedAtTime": "2026-08-21T10:15:00Z",
    "endedAtTime": "2026-08-21T10:28:00Z",
    "used": "ex:sen_slope_results",
    "wasInformedBy": "ex:step2_seasonal_sen_slope",
    "wasAssociatedWith": ["https://orcid.org/0000-0003-4718-2959", "ex:gdal"]
  },

  {
    "id": "ex:step3b_stac_metadata",
    "activityType": ["prov:Activity", "ex:PostProcessing", "ex:StacMetadataCreation"],
    "rdfs:label": "Step 3b: Post-processing - create STAC metadata",
    "rdfs:comment": "Creates STAC collection and items for the COGs and embeds the available provenance information: algorithm repository and version, processing backend and input parameters.",
    "startedAtTime": "2026-08-21T10:28:00Z",
    "endedAtTime": "2026-08-21T10:45:00Z",
    "used": [
      "ex:sen_slope_cogs",
      "ex:sen_slope_algorithm",
      "ex:sen_slope_parameters",
      "ex:bap_process_graph"
    ],
    "wasInformedBy": ["ex:step1_bap", "ex:step2_seasonal_sen_slope", "ex:step3a_cog_conversion"],
    "wasAssociatedWith": ["https://orcid.org/0000-0003-4718-2959", "ex:pystac"]
  },

  {
    "id": "https://orcid.org/0000-0003-4718-2959",
    "agentType": ["prov:Agent", "prov:Person"],
    "rdfs:label": "GIS Analyst",
    "schema:identifier": "https://orcid.org/0000-0003-4718-2959"
  },

  {
    "id": "ex:openeo_client",
    "agentType": ["prov:Agent", "prov:SoftwareAgent", "schema:SoftwareApplication"],
    "dcterms:title": "openeo-python-client",
    "schema:softwareVersion": "0.31.0",
    "qualifiedDelegation": { "agent": "https://orcid.org/0000-0003-4718-2959", "hadActivity": "ex:step1_bap" }
  },

  {
    "id": "ex:openeo_backend",
    "agentType": ["prov:Agent", "prov:SoftwareAgent", "openeo:Backend"],
    "dcterms:title": "openEO backend",
    "ex:backendUrl": "https://openeo.example.org",
    "qualifiedDelegation": { "agent": "ex:openeo_client", "hadActivity": "ex:step1_bap" }
  },

  {
    "id": "ex:gdal",
    "agentType": ["prov:Agent", "prov:SoftwareAgent", "schema:SoftwareApplication"],
    "dcterms:title": "GDAL (COG driver)",
    "schema:softwareVersion": "3.9.2",
    "actedOnBehalfOf": "https://orcid.org/0000-0003-4718-2959"
  },

  {
    "id": "ex:pystac",
    "agentType": ["prov:Agent", "prov:SoftwareAgent", "schema:SoftwareApplication"],
    "dcterms:title": "PySTAC",
    "schema:softwareVersion": "1.10.1",
    "actedOnBehalfOf": "https://orcid.org/0000-0003-4718-2959"
  }
]

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/52n-provenance/vegetation-productivity/context.jsonld",
  "@graph": [
    {
      "id": "https://openeo.example.org/collections/SENTINEL2_L2",
      "entityType": [
        "prov:Entity",
        "prov:Collection"
      ],
      "dcterms:title": "Sentinel-2 L2A surface reflectance",
      "dcterms:description": "Copernicus Sentinel-2 MSI Level-2A bottom-of-atmosphere reflectance, atmospherically corrected with Sen2Cor and including the scene classification layer (SCL), as offered by the openEO backend.",
      "dcterms:identifier": "SENTINEL2_L2",
      "dcterms:publisher": "European Space Agency (ESA), Copernicus Programme",
      "dcterms:license": "https://sentinels.copernicus.eu/documents/247904/690755/Sentinel_Data_Legal_Notice",
      "ex:mission": "Sentinel-2",
      "ex:instrument": "MSI",
      "ex:processingLevel": "L2A",
      "ex:spatialResolution": "10 m (B02, B03, B04, B08), 20 m (B05-B07, B8A, B11, B12, SCL), 60 m (B01, B09)",
      "ex:revisitTime": "5 days",
      "rdfs:seeAlso": "https://documentation.dataspace.copernicus.eu/Data/SentinelMissions/Sentinel2.html"
    },
    {
      "id": "https://example.org/stac/collections/bap",
      "entityType": [
        "prov:Entity",
        "prov:Collection"
      ],
      "dcterms:title": "Best available pixels from Sentinel-2 scenes over AOI",
      "dcterms:conformsTo": "https://schemas.stacspec.org/v1.0.0/collection-spec/json-schema/collection.json",
      "hadMember": [
        "https://example.org/stac/collections/bap/items/Sakar_complete_months_2021_2025_2021_01_indices_savi",
        "https://example.org/stac/collections/bap/items/Sakar_complete_months_2021_2025_2021_02_indices_savi"
      ],
      "wasGeneratedBy": "ex:step1_bap",
      "generatedAtTime": "2026-08-21T10:05:00Z",
      "wasDerivedFrom": "https://openeo.example.org/collections/SENTINEL2_L2",
      "wasAttributedTo": "https://orcid.org/0000-0003-4718-2959",
      "spdx:checksum": {
        "spdx:algorithm": {
          "@id": "spdx:checksumAlgorithm_sha256"
        },
        "spdx:checksumValue": "3f1c9a0e7b2d4c6f8a1e5b7d9c0f2a4e6b8d0c1e3f5a7b9d2c4e6f8a0b1c3d5e"
      }
    },
    {
      "id": "ex:bap_process_graph",
      "entityType": [
        "prov:Entity",
        "prov:Plan"
      ],
      "dcterms:title": "Best available pixel in timeseries over AOI",
      "openeo:processId": "bap"
    },
    {
      "id": "ex:sen_slope_algorithm",
      "entityType": [
        "prov:Entity",
        "prov:Plan",
        "schema:SoftwareSourceCode"
      ],
      "dcterms:title": "Seasonal Sen slope trend estimator",
      "schema:codeRepository": "https://github.com/example-org/seasonal-sen-slope",
      "schema:version": "1.2.0",
      "schema:programmingLanguage": "Python",
      "rdfs:seeAlso": "https://en.wikipedia.org/wiki/Theil%E2%80%93Sen_estimator"
    },
    {
      "id": "ex:sen_slope_parameters",
      "entityType": [
        "prov:Entity",
        "ex:ProcessInputs"
      ],
      "dcterms:title": "Input parameters of the seasonal Sen slope analysis",
      "ex:vegetationIndex": "SAVI",
      "ex:saviSoilFactor": 0.5,
      "ex:startDate": "2021-01-01",
      "ex:endDate": "2025-12-31",
      "ex:seasonLength": 12,
      "ex:significanceLevel": 0.05
    },
    {
      "id": "ex:sen_slope_results",
      "entityType": [
        "prov:Entity",
        "prov:Collection"
      ],
      "dcterms:title": "Seasonal Sen slope results (plain GeoTIFF)",
      "dcterms:format": "image/tiff; application=geotiff",
      "hadMember": [
        "ex:DeltaIR_SAVI_tif",
        "ex:PercentChange_SAVI_tif"
      ],
      "wasGeneratedBy": "ex:step2_seasonal_sen_slope",
      "generatedAtTime": "2026-08-21T10:12:00Z",
      "wasDerivedFrom": "https://example.org/stac/collections/bap",
      "wasAttributedTo": "https://orcid.org/0000-0003-4718-2959"
    },
    {
      "id": "ex:sen_slope_cogs",
      "entityType": [
        "prov:Entity",
        "prov:Collection"
      ],
      "dcterms:title": "Seasonal Sen slope results (Cloud Optimized GeoTIFF)",
      "dcterms:format": "image/tiff; application=geotiff; profile=cloud-optimized",
      "hadMember": [
        "https://example.org/data/sen/DeltaIR_SAVI.tif",
        "https://example.org/data/sen/PercentChange_SAVI.tif"
      ],
      "wasGeneratedBy": "ex:step3a_cog_conversion",
      "generatedAtTime": "2026-08-21T10:28:00Z",
      "wasDerivedFrom": "ex:sen_slope_results",
      "wasAttributedTo": "https://orcid.org/0000-0003-4718-2959"
    },
    {
      "id": "https://example.org/stac/collections/sen",
      "entityType": [
        "prov:Entity",
        "prov:Collection"
      ],
      "dcterms:title": "Seasonal Sen Slope",
      "dcterms:conformsTo": "https://schemas.stacspec.org/v1.0.0/collection-spec/json-schema/collection.json",
      "hadMember": [
        "https://example.org/stac/collections/sen/items/DeltaIR_SAVI",
        "https://example.org/stac/collections/sen/items/PercentChange_SAVI"
      ],
      "wasGeneratedBy": "ex:step3b_stac_metadata",
      "generatedAtTime": "2026-08-21T10:45:00Z",
      "wasDerivedFrom": "ex:sen_slope_cogs",
      "wasAttributedTo": "https://orcid.org/0000-0003-4718-2959",
      "spdx:checksum": {
        "spdx:algorithm": {
          "@id": "spdx:checksumAlgorithm_sha256"
        },
        "spdx:checksumValue": "a7d2e4f6081b3c5d7e9f0a2b4c6d8e0f1a3b5c7d9e1f2a4b6c8d0e2f4a6b8c0d"
      }
    },
    {
      "id": "ex:step1_bap",
      "activityType": [
        "prov:Activity",
        "openeo:BatchJob",
        "https://catalog.ospd.dev.kurrawong.ai/catalogs/demo:geoacs/collections/demo:ospd-geoacs/items/demo:GA016"
      ],
      "rdfs:label": "Step 1: Best available pixel composites",
      "startedAtTime": "2026-08-21T10:00:00Z",
      "endedAtTime": "2026-08-21T18:05:00Z",
      "openeo:jobId": "j-2608251100",
      "used": "https://openeo.example.org/collections/SENTINEL2_L2",
      "qualifiedUsage": {
        "entity": "https://openeo.example.org/collections/SENTINEL2_L2",
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
        ]
      },
      "qualifiedAssociation": [
        {
          "agent": "https://orcid.org/0000-0003-4718-2959",
          "hadPlan": "ex:bap_process_graph"
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
      "id": "ex:step2_seasonal_sen_slope",
      "activityType": [
        "prov:Activity",
        "https://catalog.ospd.dev.kurrawong.ai/catalogs/demo:geoacs/collections/demo:ospd-geoacs/items/demo:GA017"
      ],
      "rdfs:label": "Step 2: Seasonal Sen slope trend analysis",
      "startedAtTime": "2026-08-21T10:06:00Z",
      "endedAtTime": "2026-08-21T10:12:00Z",
      "used": [
        "https://example.org/stac/collections/bap",
        "ex:sen_slope_parameters"
      ],
      "wasInformedBy": "ex:step1_bap",
      "qualifiedAssociation": [
        {
          "agent": "https://orcid.org/0000-0003-4718-2959",
          "hadPlan": "ex:sen_slope_algorithm"
        }
      ]
    },
    {
      "id": "ex:step3a_cog_conversion",
      "activityType": [
        "prov:Activity",
        "ex:PostProcessing",
        "ex:CogConversion"
      ],
      "rdfs:label": "Step 3a: Post-processing - convert results to Cloud Optimized GeoTIFFs",
      "startedAtTime": "2026-08-21T10:15:00Z",
      "endedAtTime": "2026-08-21T10:28:00Z",
      "used": "ex:sen_slope_results",
      "wasInformedBy": "ex:step2_seasonal_sen_slope",
      "wasAssociatedWith": [
        "https://orcid.org/0000-0003-4718-2959",
        "ex:gdal"
      ]
    },
    {
      "id": "ex:step3b_stac_metadata",
      "activityType": [
        "prov:Activity",
        "ex:PostProcessing",
        "ex:StacMetadataCreation"
      ],
      "rdfs:label": "Step 3b: Post-processing - create STAC metadata",
      "rdfs:comment": "Creates STAC collection and items for the COGs and embeds the available provenance information: algorithm repository and version, processing backend and input parameters.",
      "startedAtTime": "2026-08-21T10:28:00Z",
      "endedAtTime": "2026-08-21T10:45:00Z",
      "used": [
        "ex:sen_slope_cogs",
        "ex:sen_slope_algorithm",
        "ex:sen_slope_parameters",
        "ex:bap_process_graph"
      ],
      "wasInformedBy": [
        "ex:step1_bap",
        "ex:step2_seasonal_sen_slope",
        "ex:step3a_cog_conversion"
      ],
      "wasAssociatedWith": [
        "https://orcid.org/0000-0003-4718-2959",
        "ex:pystac"
      ]
    },
    {
      "id": "https://orcid.org/0000-0003-4718-2959",
      "agentType": [
        "prov:Agent",
        "prov:Person"
      ],
      "rdfs:label": "GIS Analyst",
      "schema:identifier": "https://orcid.org/0000-0003-4718-2959"
    },
    {
      "id": "ex:openeo_client",
      "agentType": [
        "prov:Agent",
        "prov:SoftwareAgent",
        "schema:SoftwareApplication"
      ],
      "dcterms:title": "openeo-python-client",
      "schema:softwareVersion": "0.31.0",
      "qualifiedDelegation": {
        "agent": "https://orcid.org/0000-0003-4718-2959",
        "hadActivity": "ex:step1_bap"
      }
    },
    {
      "id": "ex:openeo_backend",
      "agentType": [
        "prov:Agent",
        "prov:SoftwareAgent",
        "openeo:Backend"
      ],
      "dcterms:title": "openEO backend",
      "ex:backendUrl": "https://openeo.example.org",
      "qualifiedDelegation": {
        "agent": "ex:openeo_client",
        "hadActivity": "ex:step1_bap"
      }
    },
    {
      "id": "ex:gdal",
      "agentType": [
        "prov:Agent",
        "prov:SoftwareAgent",
        "schema:SoftwareApplication"
      ],
      "dcterms:title": "GDAL (COG driver)",
      "schema:softwareVersion": "3.9.2",
      "actedOnBehalfOf": "https://orcid.org/0000-0003-4718-2959"
    },
    {
      "id": "ex:pystac",
      "agentType": [
        "prov:Agent",
        "prov:SoftwareAgent",
        "schema:SoftwareApplication"
      ],
      "dcterms:title": "PySTAC",
      "schema:softwareVersion": "1.10.1",
      "actedOnBehalfOf": "https://orcid.org/0000-0003-4718-2959"
    }
  ]
}
```

#### ttl
```ttl
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
    dcterms:conformsTo "https://schemas.stacspec.org/v1.0.0/collection-spec/json-schema/collection.json" ;
    dcterms:title "Seasonal Sen Slope" ;
    spdx:checksum [ spdx:algorithm spdx:checksumAlgorithm_sha256 ;
            spdx:checksumValue "a7d2e4f6081b3c5d7e9f0a2b4c6d8e0f1a3b5c7d9e1f2a4b6c8d0e2f4a6b8c0d" ] ;
    prov:generatedAtTime "2026-08-21T10:45:00+00:00"^^xsd:dateTime ;
    prov:hadMember <https://example.org/stac/collections/sen/items/DeltaIR_SAVI>,
        <https://example.org/stac/collections/sen/items/PercentChange_SAVI> ;
    prov:wasAttributedTo <https://orcid.org/0000-0003-4718-2959> ;
    prov:wasDerivedFrom ex:sen_slope_cogs ;
    prov:wasGeneratedBy ex:step3b_stac_metadata .

ex:gdal a prov:Agent,
        prov:SoftwareAgent,
        schema:SoftwareApplication ;
    dcterms:title "GDAL (COG driver)" ;
    prov:actedOnBehalfOf <https://orcid.org/0000-0003-4718-2959> ;
    schema:softwareVersion "3.9.2" .

ex:openeo_backend a prov:Agent,
        prov:SoftwareAgent,
        openeo:Backend ;
    dcterms:title "openEO backend" ;
    prov:qualifiedDelegation [ prov:agent ex:openeo_client ;
            prov:hadActivity ex:step1_bap ] ;
    ex:backendUrl "https://openeo.example.org" .

ex:pystac a prov:Agent,
        prov:SoftwareAgent,
        schema:SoftwareApplication ;
    dcterms:title "PySTAC" ;
    prov:actedOnBehalfOf <https://orcid.org/0000-0003-4718-2959> ;
    schema:softwareVersion "1.10.1" .

ex:step3b_stac_metadata a prov:Activity,
        ex:PostProcessing,
        ex:StacMetadataCreation ;
    rdfs:label "Step 3b: Post-processing - create STAC metadata" ;
    rdfs:comment "Creates STAC collection and items for the COGs and embeds the available provenance information: algorithm repository and version, processing backend and input parameters." ;
    prov:endedAtTime "2026-08-21T10:45:00+00:00"^^xsd:dateTime ;
    prov:startedAtTime "2026-08-21T10:28:00+00:00"^^xsd:dateTime ;
    prov:used ex:bap_process_graph,
        ex:sen_slope_algorithm,
        ex:sen_slope_cogs,
        ex:sen_slope_parameters ;
    prov:wasAssociatedWith ex:pystac,
        <https://orcid.org/0000-0003-4718-2959> ;
    prov:wasInformedBy ex:step1_bap,
        ex:step2_seasonal_sen_slope,
        ex:step3a_cog_conversion .

<https://example.org/stac/collections/bap> a prov:Collection,
        prov:Entity ;
    dcterms:conformsTo "https://schemas.stacspec.org/v1.0.0/collection-spec/json-schema/collection.json" ;
    dcterms:title "Best available pixels from Sentinel-2 scenes over AOI" ;
    spdx:checksum [ spdx:algorithm spdx:checksumAlgorithm_sha256 ;
            spdx:checksumValue "3f1c9a0e7b2d4c6f8a1e5b7d9c0f2a4e6b8d0c1e3f5a7b9d2c4e6f8a0b1c3d5e" ] ;
    prov:generatedAtTime "2026-08-21T10:05:00+00:00"^^xsd:dateTime ;
    prov:hadMember <https://example.org/stac/collections/bap/items/Sakar_complete_months_2021_2025_2021_01_indices_savi>,
        <https://example.org/stac/collections/bap/items/Sakar_complete_months_2021_2025_2021_02_indices_savi> ;
    prov:wasAttributedTo <https://orcid.org/0000-0003-4718-2959> ;
    prov:wasDerivedFrom <https://openeo.example.org/collections/SENTINEL2_L2> ;
    prov:wasGeneratedBy ex:step1_bap .

ex:openeo_client a prov:Agent,
        prov:SoftwareAgent,
        schema:SoftwareApplication ;
    dcterms:title "openeo-python-client" ;
    prov:qualifiedDelegation [ prov:agent <https://orcid.org/0000-0003-4718-2959> ;
            prov:hadActivity ex:step1_bap ] ;
    schema:softwareVersion "0.31.0" .

ex:sen_slope_algorithm a prov:Entity,
        prov:Plan,
        schema:SoftwareSourceCode ;
    dcterms:title "Seasonal Sen slope trend estimator" ;
    rdfs:seeAlso "https://en.wikipedia.org/wiki/Theil%E2%80%93Sen_estimator" ;
    schema:codeRepository "https://github.com/example-org/seasonal-sen-slope" ;
    schema:programmingLanguage "Python" ;
    schema:version "1.2.0" .

ex:sen_slope_cogs a prov:Collection,
        prov:Entity ;
    dcterms:format "image/tiff; application=geotiff; profile=cloud-optimized" ;
    dcterms:title "Seasonal Sen slope results (Cloud Optimized GeoTIFF)" ;
    prov:generatedAtTime "2026-08-21T10:28:00+00:00"^^xsd:dateTime ;
    prov:hadMember <https://example.org/data/sen/DeltaIR_SAVI.tif>,
        <https://example.org/data/sen/PercentChange_SAVI.tif> ;
    prov:wasAttributedTo <https://orcid.org/0000-0003-4718-2959> ;
    prov:wasDerivedFrom ex:sen_slope_results ;
    prov:wasGeneratedBy ex:step3a_cog_conversion .

ex:sen_slope_parameters a prov:Entity,
        ex:ProcessInputs ;
    dcterms:title "Input parameters of the seasonal Sen slope analysis" ;
    ex:endDate "2025-12-31" ;
    ex:saviSoilFactor 5e-01 ;
    ex:seasonLength 12 ;
    ex:significanceLevel 5e-02 ;
    ex:startDate "2021-01-01" ;
    ex:vegetationIndex "SAVI" .

ex:sen_slope_results a prov:Collection,
        prov:Entity ;
    dcterms:format "image/tiff; application=geotiff" ;
    dcterms:title "Seasonal Sen slope results (plain GeoTIFF)" ;
    prov:generatedAtTime "2026-08-21T10:12:00+00:00"^^xsd:dateTime ;
    prov:hadMember ex:DeltaIR_SAVI_tif,
        ex:PercentChange_SAVI_tif ;
    prov:wasAttributedTo <https://orcid.org/0000-0003-4718-2959> ;
    prov:wasDerivedFrom <https://example.org/stac/collections/bap> ;
    prov:wasGeneratedBy ex:step2_seasonal_sen_slope .

ex:step3a_cog_conversion a prov:Activity,
        ex:CogConversion,
        ex:PostProcessing ;
    rdfs:label "Step 3a: Post-processing - convert results to Cloud Optimized GeoTIFFs" ;
    prov:endedAtTime "2026-08-21T10:28:00+00:00"^^xsd:dateTime ;
    prov:startedAtTime "2026-08-21T10:15:00+00:00"^^xsd:dateTime ;
    prov:used ex:sen_slope_results ;
    prov:wasAssociatedWith ex:gdal,
        <https://orcid.org/0000-0003-4718-2959> ;
    prov:wasInformedBy ex:step2_seasonal_sen_slope .

ex:step2_seasonal_sen_slope a prov:Activity,
        <https://catalog.ospd.dev.kurrawong.ai/catalogs/demo:geoacs/collections/demo:ospd-geoacs/items/demo:GA017> ;
    rdfs:label "Step 2: Seasonal Sen slope trend analysis" ;
    prov:endedAtTime "2026-08-21T10:12:00+00:00"^^xsd:dateTime ;
    prov:qualifiedAssociation [ prov:agent <https://orcid.org/0000-0003-4718-2959> ;
            prov:hadPlan ex:sen_slope_algorithm ] ;
    prov:startedAtTime "2026-08-21T10:06:00+00:00"^^xsd:dateTime ;
    prov:used <https://example.org/stac/collections/bap>,
        ex:sen_slope_parameters ;
    prov:wasInformedBy ex:step1_bap .

<https://openeo.example.org/collections/SENTINEL2_L2> a prov:Collection,
        prov:Entity ;
    dcterms:description "Copernicus Sentinel-2 MSI Level-2A bottom-of-atmosphere reflectance, atmospherically corrected with Sen2Cor and including the scene classification layer (SCL), as offered by the openEO backend." ;
    dcterms:identifier "SENTINEL2_L2" ;
    dcterms:license "https://sentinels.copernicus.eu/documents/247904/690755/Sentinel_Data_Legal_Notice" ;
    dcterms:publisher "European Space Agency (ESA), Copernicus Programme" ;
    dcterms:title "Sentinel-2 L2A surface reflectance" ;
    rdfs:seeAlso "https://documentation.dataspace.copernicus.eu/Data/SentinelMissions/Sentinel2.html" ;
    ex:instrument "MSI" ;
    ex:mission "Sentinel-2" ;
    ex:processingLevel "L2A" ;
    ex:revisitTime "5 days" ;
    ex:spatialResolution "10 m (B02, B03, B04, B08), 20 m (B05-B07, B8A, B11, B12, SCL), 60 m (B01, B09)" .

ex:bap_process_graph a prov:Entity,
        prov:Plan ;
    dcterms:title "Best available pixel in timeseries over AOI" ;
    openeo:processId "bap" .

ex:step1_bap a prov:Activity,
        <https://catalog.ospd.dev.kurrawong.ai/catalogs/demo:geoacs/collections/demo:ospd-geoacs/items/demo:GA016>,
        openeo:BatchJob ;
    rdfs:label "Step 1: Best available pixel composites" ;
    prov:endedAtTime "2026-08-21T18:05:00+00:00"^^xsd:dateTime ;
    prov:qualifiedAssociation [ prov:agent <https://orcid.org/0000-0003-4718-2959> ;
            prov:hadPlan ex:bap_process_graph ],
        [ prov:agent ex:openeo_backend ;
            prov:hadPlan ex:bap_process_graph ],
        [ prov:agent ex:openeo_client ;
            prov:hadPlan ex:bap_process_graph ] ;
    prov:qualifiedUsage [ prov:entity <https://openeo.example.org/collections/SENTINEL2_L2> ;
            ex:bands "B04",
                "B08",
                "SCL" ;
            ex:bbox ( 2.645329e+01 4.185697e+01 2.657929e+01 4.19826e+01 ) ;
            ex:endDate "2025-12-31" ;
            ex:startDate "2021-01-01" ] ;
    prov:startedAtTime "2026-08-21T10:00:00+00:00"^^xsd:dateTime ;
    prov:used <https://openeo.example.org/collections/SENTINEL2_L2> ;
    openeo:jobId "j-2608251100" .

<https://orcid.org/0000-0003-4718-2959> a prov:Agent,
        prov:Person ;
    rdfs:label "GIS Analyst" ;
    schema:identifier "https://orcid.org/0000-0003-4718-2959" .


```

## Schema

```yaml
$schema: https://json-schema.org/draft/2020-12/schema
$ref: https://ogcincubator.github.io/bblock-prov-schema/build/annotated/ogc-utils/prov/schema.yaml
x-jsonld-prefixes:
  dcterms: http://purl.org/dc/terms/
  ex: https://example.org/vegetation-productivity#
  geojson: https://purl.org/geojson/vocab#
  openeo: https://example.org/openeo#
  prov: http://www.w3.org/ns/prov#
  rdfs: http://www.w3.org/2000/01/rdf-schema#
  schema: https://schema.org/
  spdx: http://spdx.org/rdf/terms#
  xsd: http://www.w3.org/2001/XMLSchema#

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/52n-provenance/vegetation-productivity/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/52n-provenance/vegetation-productivity/schema.yaml)


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
    "prov": "http://www.w3.org/ns/prov#",
    "xsd": "http://www.w3.org/2001/XMLSchema#",
    "rdfs": "http://www.w3.org/2000/01/rdf-schema#",
    "dct": "http://purl.org/dc/terms/",
    "rdf": "http://www.w3.org/1999/02/22-rdf-syntax-ns#",
    "oa": "http://www.w3.org/ns/oa#",
    "dcterms": "http://purl.org/dc/terms/",
    "ex": "https://example.org/vegetation-productivity#",
    "geojson": "https://purl.org/geojson/vocab#",
    "openeo": "https://example.org/openeo#",
    "schema": "https://schema.org/",
    "spdx": "http://spdx.org/rdf/terms#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/52n-provenance/vegetation-productivity/context.jsonld)

## Sources

* [PEOPLE-ECCO](https://www.people-ecco.eu/)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-openscience](https://github.com/ogcincubator/bblocks-openscience)
* Path: `_sources/52n-provenance/vegetation-productivity`

