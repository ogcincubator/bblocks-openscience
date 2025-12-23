
# EarthCODE Experiment (Schema)

`ogc.osc.geodcat-stac-earthcode.experiments` *v0.1*

EarthCODE metadata profile linked to semantic models

[*Status*](http://www.opengis.net/def/status): Under development

## Description

## ESA EarthCODE experiments as GeoDCAT and STAC profile 

This building block shows a possible profile of GeoDCAT supporting semantic annotation and inclusion of the three STAC extensions used by EarthCODE:

- themes
- osc
- cf

## Examples

### An example demonstrating a basic EarthCODE Experiment
#### json
```json
{
  "id": "polaris-experiment",
  "type": "Feature",
  "conformsTo": [
    "http://www.opengis.net/spec/ogcapi-records-1/1.0/req/record-core"
  ],
  "geometry": null,
  "properties": {
    "created": "2025-02-19T23:00:00Z",
    "updated": "2025-02-19T23:00:00Z",
    "type": "experiment",
    "title": "POLARIS",
    "description": "Polar Operational Limit Assessment Risk Index System (POLARIS)",
    "keywords": [
      "sea ice",
      "polar"
    ],
    "contacts": [
      {
        "name": "EarthCODE Demo",
        "organization": "EarthCODE",
        "links": [
          {
            "rel": "about",
            "type": "text/html",
            "href": "https://opensciencedata.esa.int/"
          }
        ],
        "contactInstructions": "Contact via EarthCODE",
        "roles": [
          "host"
        ]
      }
    ],
    "themes": [
      {
        "scheme": "https://github.com/stac-extensions/osc#theme",
        "concepts": [
          {
            "id": "oceans"
          }
        ]
      }
    ],
    "formats": [
      {
        "name": "GeoTIFF"
      }
    ],
    "license": "CC-BY-SA-4.0",
    "osc:workflow": "polaris-workflow",
    "version": "2"
  },
  "linkTemplates": [],
  "links": [
    {
      "rel": "root",
      "href": "../../catalog.json",
      "type": "application/json",
      "title": "Open Science Catalog"
    },
    {
      "rel": "parent",
      "href": "../catalog.json",
      "type": "application/json",
      "title": "Experiments"
    },
    {
      "rel": "child",
      "href": "../../products/polaris/collection.json",
      "type": "application/json",
      "title": "POLARIS"
    },
    {
      "rel": "related",
      "href": "../../themes/oceans/catalog.json",
      "type": "application/json",
      "title": "Theme: Oceans"
    },
    {
      "rel": "related",
      "href": "../../workflows/polaris-workflow/record.json",
      "type": "application/json",
      "title": "Workflow: POLARIS"
    },
    {
      "rel": "input",
      "href": "./input.yaml",
      "type": "application/yaml",
      "title": "Input parameters"
    },
    {
      "rel": "environment",
      "href": "./environment.yaml",
      "type": "application/yaml",
      "title": "Execution environment"
    },
    {
      "rel": "self",
      "href": "https://esa-earthcode.github.io/open-science-catalog-metadata/experiments/polaris-experiment/item.json",
      "type": "application/json"
    }
  ]
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/experiments/context.jsonld",
  "id": "polaris-experiment",
  "type": "Feature",
  "conformsTo": [
    "http://www.opengis.net/spec/ogcapi-records-1/1.0/req/record-core"
  ],
  "geometry": null,
  "properties": {
    "created": "2025-02-19T23:00:00Z",
    "updated": "2025-02-19T23:00:00Z",
    "type": "experiment",
    "title": "POLARIS",
    "description": "Polar Operational Limit Assessment Risk Index System (POLARIS)",
    "keywords": [
      "sea ice",
      "polar"
    ],
    "contacts": [
      {
        "name": "EarthCODE Demo",
        "organization": "EarthCODE",
        "links": [
          {
            "rel": "about",
            "type": "text/html",
            "href": "https://opensciencedata.esa.int/"
          }
        ],
        "contactInstructions": "Contact via EarthCODE",
        "roles": [
          "host"
        ]
      }
    ],
    "themes": [
      {
        "scheme": "https://github.com/stac-extensions/osc#theme",
        "concepts": [
          {
            "id": "oceans"
          }
        ]
      }
    ],
    "formats": [
      {
        "name": "GeoTIFF"
      }
    ],
    "license": "CC-BY-SA-4.0",
    "osc:workflow": "polaris-workflow",
    "version": "2"
  },
  "linkTemplates": [],
  "links": [
    {
      "rel": "root",
      "href": "../../catalog.json",
      "type": "application/json",
      "title": "Open Science Catalog"
    },
    {
      "rel": "parent",
      "href": "../catalog.json",
      "type": "application/json",
      "title": "Experiments"
    },
    {
      "rel": "child",
      "href": "../../products/polaris/collection.json",
      "type": "application/json",
      "title": "POLARIS"
    },
    {
      "rel": "related",
      "href": "../../themes/oceans/catalog.json",
      "type": "application/json",
      "title": "Theme: Oceans"
    },
    {
      "rel": "related",
      "href": "../../workflows/polaris-workflow/record.json",
      "type": "application/json",
      "title": "Workflow: POLARIS"
    },
    {
      "rel": "input",
      "href": "./input.yaml",
      "type": "application/yaml",
      "title": "Input parameters"
    },
    {
      "rel": "environment",
      "href": "./environment.yaml",
      "type": "application/yaml",
      "title": "Execution environment"
    },
    {
      "rel": "self",
      "href": "https://esa-earthcode.github.io/open-science-catalog-metadata/experiments/polaris-experiment/item.json",
      "type": "application/json"
    }
  ]
}
```

#### ttl
```ttl
@prefix dcat: <http://www.w3.org/ns/dcat#> .
@prefix dcterms: <http://purl.org/dc/terms/> .
@prefix geojson: <https://purl.org/geojson/vocab#> .
@prefix ns1: <http://www.iana.org/assignments/> .
@prefix ns2: <osc:> .
@prefix oa: <http://www.w3.org/ns/oa#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix rec: <https://www.opengis.net/def/ogc-api/records/> .
@prefix thns: <https://w3id.org/ogc/stac/themes/> .
@prefix wfprov: <http://purl.org/wf4ever/wfprov#> .

<https://ogc.org/demo/ospd/polaris-experiment> a geojson:Feature ;
    dcterms:conformsTo <http://www.opengis.net/spec/ogcapi-records-1/1.0/req/record-core> ;
    wfprov:properties [ a wfprov:experiment ;
            dcterms:created "2025-02-19T23:00:00Z" ;
            dcterms:description "Polar Operational Limit Assessment Risk Index System (POLARIS)" ;
            dcterms:modified "2025-02-19T23:00:00Z" ;
            dcterms:title "POLARIS" ;
            wfprov:version "2" ;
            dcat:contactPoint [ rdfs:label "EarthCODE Demo" ;
                    wfprov:contactInstructions "Contact via EarthCODE" ;
                    wfprov:links [ dcterms:type "text/html" ;
                            ns1:relation <http://www.iana.org/assignments/relation/about> ;
                            oa:hasTarget <https://opensciencedata.esa.int/> ] ;
                    wfprov:organization "EarthCODE" ;
                    wfprov:roles "host" ] ;
            dcat:keyword "polar",
                "sea ice" ;
            dcat:license "CC-BY-SA-4.0" ;
            rec:format [ rec:name "GeoTIFF" ] ;
            rec:themes [ thns:concepts [ thns:id "oceans" ] ;
                    thns:scheme "https://github.com/stac-extensions/osc#theme" ] ;
            ns2:workflow "polaris-workflow" ] ;
    rdfs:seeAlso [ a <http://purl.org/wf4ever/wfprov#application/json> ;
            dcterms:title "POLARIS" ;
            wfprov:rel "child" ;
            oa:hasTarget <https://ogc.org/products/polaris/collection.json> ],
        [ a <http://purl.org/wf4ever/wfprov#application/json> ;
            dcterms:title "Workflow: POLARIS" ;
            wfprov:rel "related" ;
            oa:hasTarget <https://ogc.org/workflows/polaris-workflow/record.json> ],
        [ a <http://purl.org/wf4ever/wfprov#application/yaml> ;
            dcterms:title "Execution environment" ;
            wfprov:rel "environment" ;
            oa:hasTarget <https://ogc.org/demo/ospd/environment.yaml> ],
        [ a <http://purl.org/wf4ever/wfprov#application/json> ;
            wfprov:rel "self" ;
            oa:hasTarget <https://esa-earthcode.github.io/open-science-catalog-metadata/experiments/polaris-experiment/item.json> ],
        [ a <http://purl.org/wf4ever/wfprov#application/json> ;
            dcterms:title "Theme: Oceans" ;
            wfprov:rel "related" ;
            oa:hasTarget <https://ogc.org/themes/oceans/catalog.json> ],
        [ a <http://purl.org/wf4ever/wfprov#application/json> ;
            dcterms:title "Open Science Catalog" ;
            wfprov:rel "root" ;
            oa:hasTarget <https://ogc.org/catalog.json> ],
        [ a <http://purl.org/wf4ever/wfprov#application/yaml> ;
            dcterms:title "Input parameters" ;
            wfprov:rel "input" ;
            oa:hasTarget <https://ogc.org/demo/ospd/input.yaml> ],
        [ a <http://purl.org/wf4ever/wfprov#application/json> ;
            dcterms:title "Experiments" ;
            wfprov:rel "parent" ;
            oa:hasTarget <https://ogc.org/demo/catalog.json> ] .


```


### An example of Kind Grove workflow provenance wf4ever
Kind Grove workflow example and its provenance trace with main steps involved for its execution. 

#### turtle
```turtle
PREFIX prov: <http://www.w3.org/ns/prov#>
PREFIX schema: <https://schema.org/>
PREFIX stac: <https://w3id.org/ogc/stac/core/>
PREFIX wfdesc: <http://purl.org/wf4ever/wfdesc#>
PREFIX wfkg: <https://example.org/kindgrove/>
PREFIX wfprov: <http://purl.org/wf4ever/wfprov#>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>

wfkg:DefineStudyAreaRun
    a wfprov:ProcessRun ;
    wfprov:describedByProcess wfkg:DefineStudyAreaProcess ;
    wfprov:hasSubProcessRun
        wfkg:AddCenterPointRun ,
        wfkg:AddInfoAnnotationRun ,
        wfkg:AddStudyAreaBoundaryRun ,
        wfkg:CreateBoundingBoxRun ,
        wfkg:CreateLocationSelectorWidgetRun ,
        wfkg:CreateMapRun ,
        wfkg:DisplayStudyAreaRun ,
        wfkg:GetSelectedSiteRun ;
    wfprov:usedInput
        wfkg:DateRange ,
        wfkg:StudyArea ;
    wfprov:wasEnactedBy wfkg:JupyterNotebookEngine ;
    wfprov:wasPartOfWorkflowRun wfkg:KindGroveWorkflowRun ;
.

wfkg:InteractiveVisualisation
    a wfprov:Artifact ;
    wfprov:wasOutputFrom wfkg:DisplaySummaryReportRun ;
    schema:encodingFormat "text/html" ;
    schema:name "HTML Summary Report" ;
.

wfkg:AWSSTACCatalog
    a
        wfprov:Artifact ,
        stac:Catalog ;
    schema:name "AWS STAC Catalog" ;
    schema:url "https://earth-search.aws.element84.com/v1" ;
.

wfkg:AllometricEquationDesc
    a wfdesc:Process ;
.

wfkg:AllometricEquationRun
    a wfprov:ProcessRun ;
    wfprov:describedByProcess wfkg:AllometricEquationDesc ;
    wfprov:usedInput
        wfkg:MangroveMask ,
        wfkg:NDVI ;
    wfprov:wasEnactedBy wfkg:JupyterNotebookEngine ;
    wfprov:wasPartOfWorkflowRun wfkg:KindGroveWorkflowRun ;
.

wfkg:BiomassEstimate
    a wfprov:Artifact ;
    wfdesc:wasOutputFrom wfkg:AllometricEquationRun ;
.

wfkg:CO2EquivalentDesc
    a wfdesc:Process ;
.

wfkg:CO2EquivalentEstimate
    a wfprov:Artifact ;
    wfdesc:wasOutputFrom wfkg:CO2EquivalentRun ;
.

wfkg:CO2EquivalentRun
    a wfprov:ProcessRun ;
    wfprov:describedByProcess wfkg:CO2EquivalentDesc ;
    wfprov:usedInput wfkg:CarbonStockEstimate ;
    wfprov:wasEnactedBy wfkg:JupyterNotebookEngine ;
    wfprov:wasPartOfWorkflowRun wfkg:KindGroveWorkflowRun ;
.

wfkg:CSVSummary
    a wfprov:Artifact ;
    wfdesc:wasOutputFrom wfkg:ExportResultsRun ;
    schema:encodingFormat "text/csv" ;
.

wfkg:CalculateIndicesProcessDesc
    a wfdesc:Process ;
.

wfkg:CarbonStockDesc
    a wfdesc:Process ;
.

wfkg:CarbonStockEstimate
    a wfprov:Artifact ;
    wfdesc:wasOutputFrom wfkg:CarbonStockRun ;
.

wfkg:CarbonStockRun
    a wfprov:ProcessRun ;
    wfprov:describedByProcess wfkg:CarbonStockDesc ;
    wfprov:usedInput wfkg:BiomassEstimate ;
    wfprov:wasEnactedBy wfkg:JupyterNotebookEngine ;
    wfprov:wasPartOfWorkflowRun wfkg:KindGroveWorkflowRun ;
.

wfkg:DefineStudyAreaProcess
    a wfdesc:Process ;

.

wfkg:DisplaySummaryReportRun
    a wfdesc:Process ;
.

wfkg:DisplaySummaryReportRun
    a wfprov:ProcessRun ;
    wfprov:describedByProcess wfkg:DisplaySummaryReportRun ;
    wfprov:usedInput
        wfkg:CSVSummary ,
        wfkg:GeoTIFFRaster ;
    wfprov:wasPartOfWorkflowRun wfkg:KindGroveWorkflowRun ;
    prov:endedAtTime "2024-06-01T10:46:00+00:00"^^xsd:dateTime ;
.

wfkg:DownloadBandsProcessDesc
    a wfdesc:Process ;
.

wfkg:ExportResultsDesc
    a wfdesc:Process ;
.

wfkg:GeoTIFFRaster
    a wfprov:Artifact ;
    wfdesc:wasOutputFrom wfkg:ExportResultsRun ;
    schema:encodingFormat "image/tiff" ;
.

wfkg:GreenBand
    a wfprov:Artifact ;
    wfdesc:wasOutputFrom wfkg:DownloadBandsRun ;
.

wfkg:KindGroveWorkflow
    a
        wfdesc:Workflow ,
        schema:ComputationalWorkflow ;
    schema:name "KindGrove Mangrove Carbon Assessment Workflow" ;
    schema:version "1.0" ;
.

wfkg:Myanmar
    a schema:Country ;
    schema:name "Myanmar" ;
.

wfkg:NDWI
    a wfprov:Artifact ;
    wfdesc:wasOutputFrom wfkg:CalculateIndicesRun ;
.

wfkg:NIRBand
    a wfprov:Artifact ;
    wfdesc:wasOutputFrom wfkg:DownloadBandsRun ;
.

wfkg:RedBand
    a wfprov:Artifact ;
    wfdesc:wasOutputFrom wfkg:DownloadBandsRun ;
.

wfkg:SAVI
    a wfprov:Artifact ;
    wfdesc:wasOutputFrom wfkg:CalculateIndicesRun ;
.

wfkg:SelectScenesProcessDesc
    a wfdesc:Process ;
.

wfkg:SelectScenesRun
    a wfprov:ProcessRun ;
    wfprov:describedByProcess wfkg:SelectScenesProcessDesc ;
    wfprov:usedInput
        wfkg:DateRange ,
        wfkg:Sentinel2L2A ,
        wfkg:StudyArea ;
    wfprov:wasEnactedBy wfkg:JupyterNotebookEngine ;
    wfprov:wasPartOfWorkflowRun wfkg:KindGroveWorkflowRun ;
.

wfkg:SelectedScene
    a wfprov:Artifact ;
    wfdesc:wasOutputFrom wfkg:SelectScenesRun ;
    schema:description "Lowest cloud cover Sentinel-2 scene" ;
.

wfkg:Sentinel2L2A
    a
        wfprov:Artifact ,
        stac:Collection ;
    schema:distribution wfkg:Sentinel2L2A_AWSS3Distribution ;
    schema:isPartOf wfkg:AWSSTACCatalog ;
    schema:name "Sentinel-2 L2A Multispectral Optical Imagery" ;
.

wfkg:Sentinel2L2A_AWSS3Distribution
    a schema:DataDownload ;
    schema:contentUrl "s3://sentinel-inventory/sentinel-s2-l2a/" ;
    schema:isAccessibleForFree true ;
    schema:name "Sentinel-2 L2A AWS Open Data Registry (S3)" ;
    schema:provider "AWS Open Data Registry" ;
.

wfkg:StarlingFoundries
    a prov:Organization ;
    schema:name "Starling Foundries" ;
.

wfkg:StudyAreaGeometry
    a schema:GeoShape ;
    schema:box "95.15 15.9 95.35 16.1" ;
    schema:center "95.25 16.0" ;
    schema:polygon "95.15 15.9 95.35 15.9 95.35 16.1 95.15 16.1 95.15 15.9" ;
.

wfkg:ThresholdClassificationDesc
    a wfdesc:Process ;
.

wfkg:ThresholdClassificationRun
    a wfprov:ProcessRun ;
    wfprov:describedByProcess wfkg:ThresholdClassificationDesc ;
    wfprov:usedInput
        wfkg:NDVI ,
        wfkg:NDWI ,
        wfkg:SAVI ;
    wfprov:wasEnactedBy wfkg:JupyterNotebookEngine ;
    wfprov:wasPartOfWorkflowRun wfkg:KindGroveWorkflowRun ;
.

wfkg:CameronSajedi
    a prov:Person ;
    schema:affiliation wfkg:StarlingFoundries ;
    schema:name "Cameron Sajedi" ;
.

wfkg:DateRange
    a wfprov:Artifact ;
    schema:description "Temporal range for satellite query" ;
.

wfkg:ExportResultsRun
    a wfprov:ProcessRun ;
    wfprov:describedByProcess wfkg:ExportResultsDesc ;
    wfprov:usedInput
        wfkg:CO2EquivalentEstimate ,
        wfkg:MangroveMask ;
    wfprov:wasEnactedBy wfkg:JupyterNotebookEngine ;
    wfprov:wasPartOfWorkflowRun wfkg:KindGroveWorkflowRun ;
.

wfkg:MangroveMask
    a wfprov:Artifact ;
    wfdesc:wasOutputFrom wfkg:ThresholdClassificationRun ;
.

wfkg:NDVI
    a wfprov:Artifact ;
    wfdesc:wasOutputFrom wfkg:CalculateIndicesRun ;
.

wfkg:StudyArea
    a wfprov:Artifact ;
    schema:containedInPlace wfkg:Myanmar ;
    schema:description "1,800 acres of mangrove restoration in Ayeyarwady Delta" ;
    schema:geo wfkg:StudyAreaGeometry ;
    schema:name "Thor Heyerdahl Climate Park" ;
.

wfkg:CalculateIndicesRun
    a wfprov:ProcessRun ;
    wfprov:describedByProcess wfkg:CalculateIndicesProcessDesc ;
    wfprov:usedInput
        wfkg:GreenBand ,
        wfkg:NIRBand ,
        wfkg:RedBand ;
    wfprov:wasEnactedBy wfkg:JupyterNotebookEngine ;
    wfprov:wasPartOfWorkflowRun wfkg:KindGroveWorkflowRun ;
.

wfkg:DownloadBandsRun
    a wfprov:ProcessRun ;
    wfprov:describedByProcess wfkg:DownloadBandsProcessDesc ;
    wfprov:usedInput wfkg:SelectedScene ;
    wfprov:wasEnactedBy wfkg:JupyterNotebookEngine ;
    wfprov:wasPartOfWorkflowRun wfkg:KindGroveWorkflowRun ;
.

wfkg:JupyterNotebookEngine
    a wfprov:WorkflowEngine ;
    prov:actedOnBehalfOf wfkg:CameronSajedi ;
    schema:name "Jupyter Notebook" ;
.

wfkg:KindGroveWorkflowRun
    a wfprov:WorkflowRun ;
    wfprov:describedByWorkflow wfkg:KindGroveWorkflow ;
    wfprov:wasInitiatedBy wfkg:CameronSajedi ;
    prov:endedAtTime "2024-06-01T10:45:00+00:00"^^xsd:dateTime ;
    prov:startedAtTime "2024-06-01T10:00:00+00:00"^^xsd:dateTime ;
.

```


### An example of Kind Grove workflow provenance wf4ever
Kind Grove workflow example and its provenance trace with main steps involved for its execution. 

#### jsonld
```jsonld
{
  "@context": "https://nenadradosevic.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/experiments/context.jsonld",
  "id": "kindgrove-experiment",
  "type": "Feature",
  "conformsTo": [
    "http://www.opengis.net/spec/ogcapi-records-1/1.0/req/record-core"
  ],
  "geometry": null,
  "properties": {
    "created": "2024-06-01T10:00:00Z",
    "updated": "2024-06-01T10:45:00Z",
    "type": "experiment",
    "title": "KindGrove Mangrove Carbon Assessment",
    "description": "An Earth observation workflow for mangrove detection and carbon stock estimation using Sentinel-2 imagery.",
    "keywords": [
      "mangroves",
      "carbon",
      "Sentinel-2",
      "remote sensing",
      "climate"
    ],
    "contacts": [
      {
        "name": "Cameron Sajedi",
        "organization": "Starling Foundries",
        "roles": ["author", "operator"]
      }
    ],
    "themes": [
      {
        "scheme": "https://github.com/stac-extensions/osc#theme",
        "concepts": [
          { "id": "ecosystems" },
          { "id": "climate" }
        ]
      }
    ],
    "formats": [
      { "name": "GeoTIFF" },
      { "name": "CSV" }
    ],
    "license": "CC-BY-4.0",
    "osc:workflow": "kindgrove-workflow",
    "version": "1.0"
  },
  "links": [
    {
      "rel": "related",
      "href": "../workflows/kindgrove-workflow/record.json",
      "type": "application/json",
      "title": "Workflow description"
    },
    {
      "rel": "related",
      "href": "../provenance/kindgrove-run.jsonld",
      "type": "application/ld+json",
      "title": "Execution provenance"
    }
  ]
}

```

#### ttl
```ttl
@prefix dcterms: <http://purl.org/dc/terms/> .
@prefix geojson: <https://purl.org/geojson/vocab#> .
@prefix ns1: <http://www.iana.org/assignments/> .
@prefix oa: <http://www.w3.org/ns/oa#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .

<https://ogc.org/demo/ospd/kindgrove/kindgrove-experiment> a geojson:Feature ;
    dcterms:conformsTo <http://www.opengis.net/spec/ogcapi-records-1/1.0/req/record-core> ;
    rdfs:seeAlso [ rdfs:label "Execution provenance" ;
            dcterms:format "application/ld+json" ;
            ns1:relation <http://www.iana.org/assignments/relation/related> ;
            oa:hasTarget <https://ogc.org/demo/ospd/provenance/kindgrove-run.jsonld> ],
        [ rdfs:label "Workflow description" ;
            dcterms:format "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/related> ;
            oa:hasTarget <https://ogc.org/demo/ospd/workflows/kindgrove-workflow/record.json> ] .


```


### An example Experiment for the OSPD experiment taking the water bodies workflow and running it on another platform.
#### json
```json
{
  "id": "water-bodies-execution",
  "type": "Feature",
  "conformsTo": [
    "http://www.opengis.net/spec/ogcapi-records-1/1.0/req/record-core"
  ],
  "geometry": null,
  "properties": {
    "created": "2025-01-21T18:00:00Z",
    "updated": "2025-01-21T18:40:00Z",
    "type": "experiment",
    "title": "ESA WorldCereal Experiment",
    "description": "Experiment using the water bodies workflow.",
    "contacts": [
      {
        "name": "A person",
        "position": "Researcher",
        "organization": "An Org",
        "contactInstructions": "Contact via website",
        "roles": [
          "principal investigator"
        ]
      },
      {
        "name": "An Org",
        "links": [
          {
            "href": "https://example.com/",
            "rel": "about",
            "type": "text/html"
          }
        ],
        "contactInstructions": "SEE WEBSITE",
        "roles": [
          "processor"
        ]
      }
    ],
    "themes": [
      {
        "scheme": "https://github.com/stac-extensions/osc#theme",
        "concepts": [
          {
            "id": "land"
          }
        ]
      }
    ],
    "formats": [
      {
        "name": "GeoTIFF"
      }
    ],
    "license": "proprietary",
    "osc:workflow": "waterbodies",
    "version": "2"
  },
  "linkTemplates": [],
  "links": [
    {
      "rel": "root",
      "href": "https://example.com/open-science-catalog-metadata/catalog.json",
      "type": "application/json",
      "title": "Open Science Catalog"
    },
    {
      "rel": "parent",
      "href": "https://example.com/open-science-catalog-metadata/experiments/catalog.json",
      "type": "application/json",
      "title": "Experiments"
    },
    {
      "rel": "child",
      "href": "https://example.com/open-science-catalog-metadata/products/water-bodies-execution-outputs/collection.json",
      "type": "application/json",
      "title": "Water Bodies Execution Outputs"
    },
    {
      "rel": "service",
      "type": "application/json",
      "title": "An EO data exploitation platform",
      "href": "https://example.com"
    },
    {
      "rel": "related",
      "href": "https://example.com/open-science-catalog-metadata/themes/land/catalog.json",
      "type": "application/json",
      "title": "Theme: Land"
    },
    {
      "rel": "related",
      "href": "../../workflows/waterbodies/record.json",
      "type": "application/json",
      "title": "Workflow: Water Bodies"
    },
    {
      "rel": "self",
      "href": "https://example.com/open-science-catalog-metadata/experiments/water-bodies-execution/record.json",
      "type": "application/json"
    }
  ]
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/experiments/context.jsonld",
  "id": "water-bodies-execution",
  "type": "Feature",
  "conformsTo": [
    "http://www.opengis.net/spec/ogcapi-records-1/1.0/req/record-core"
  ],
  "geometry": null,
  "properties": {
    "created": "2025-01-21T18:00:00Z",
    "updated": "2025-01-21T18:40:00Z",
    "type": "experiment",
    "title": "ESA WorldCereal Experiment",
    "description": "Experiment using the water bodies workflow.",
    "contacts": [
      {
        "name": "A person",
        "position": "Researcher",
        "organization": "An Org",
        "contactInstructions": "Contact via website",
        "roles": [
          "principal investigator"
        ]
      },
      {
        "name": "An Org",
        "links": [
          {
            "href": "https://example.com/",
            "rel": "about",
            "type": "text/html"
          }
        ],
        "contactInstructions": "SEE WEBSITE",
        "roles": [
          "processor"
        ]
      }
    ],
    "themes": [
      {
        "scheme": "https://github.com/stac-extensions/osc#theme",
        "concepts": [
          {
            "id": "land"
          }
        ]
      }
    ],
    "formats": [
      {
        "name": "GeoTIFF"
      }
    ],
    "license": "proprietary",
    "osc:workflow": "waterbodies",
    "version": "2"
  },
  "linkTemplates": [],
  "links": [
    {
      "rel": "root",
      "href": "https://example.com/open-science-catalog-metadata/catalog.json",
      "type": "application/json",
      "title": "Open Science Catalog"
    },
    {
      "rel": "parent",
      "href": "https://example.com/open-science-catalog-metadata/experiments/catalog.json",
      "type": "application/json",
      "title": "Experiments"
    },
    {
      "rel": "child",
      "href": "https://example.com/open-science-catalog-metadata/products/water-bodies-execution-outputs/collection.json",
      "type": "application/json",
      "title": "Water Bodies Execution Outputs"
    },
    {
      "rel": "service",
      "type": "application/json",
      "title": "An EO data exploitation platform",
      "href": "https://example.com"
    },
    {
      "rel": "related",
      "href": "https://example.com/open-science-catalog-metadata/themes/land/catalog.json",
      "type": "application/json",
      "title": "Theme: Land"
    },
    {
      "rel": "related",
      "href": "../../workflows/waterbodies/record.json",
      "type": "application/json",
      "title": "Workflow: Water Bodies"
    },
    {
      "rel": "self",
      "href": "https://example.com/open-science-catalog-metadata/experiments/water-bodies-execution/record.json",
      "type": "application/json"
    }
  ]
}
```

#### ttl
```ttl
@prefix dcat: <http://www.w3.org/ns/dcat#> .
@prefix dcterms: <http://purl.org/dc/terms/> .
@prefix geojson: <https://purl.org/geojson/vocab#> .
@prefix ns1: <osc:> .
@prefix ns2: <http://www.iana.org/assignments/> .
@prefix oa: <http://www.w3.org/ns/oa#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix rec: <https://www.opengis.net/def/ogc-api/records/> .
@prefix thns: <https://w3id.org/ogc/stac/themes/> .
@prefix wfprov: <http://purl.org/wf4ever/wfprov#> .

<https://ogc.org/demo/ospd/water-bodies-execution> a geojson:Feature ;
    dcterms:conformsTo <http://www.opengis.net/spec/ogcapi-records-1/1.0/req/record-core> ;
    wfprov:properties [ a wfprov:experiment ;
            dcterms:created "2025-01-21T18:00:00Z" ;
            dcterms:description "Experiment using the water bodies workflow." ;
            dcterms:modified "2025-01-21T18:40:00Z" ;
            dcterms:title "ESA WorldCereal Experiment" ;
            wfprov:version "2" ;
            dcat:contactPoint [ rdfs:label "An Org" ;
                    wfprov:contactInstructions "SEE WEBSITE" ;
                    wfprov:links [ dcterms:type "text/html" ;
                            ns2:relation <http://www.iana.org/assignments/relation/about> ;
                            oa:hasTarget <https://example.com/> ] ;
                    wfprov:roles "processor" ],
                [ rdfs:label "A person" ;
                    wfprov:contactInstructions "Contact via website" ;
                    wfprov:organization "An Org" ;
                    wfprov:position "Researcher" ;
                    wfprov:roles "principal investigator" ] ;
            dcat:license "proprietary" ;
            rec:format [ rec:name "GeoTIFF" ] ;
            rec:themes [ thns:concepts [ thns:id "land" ] ;
                    thns:scheme "https://github.com/stac-extensions/osc#theme" ] ;
            ns1:workflow "waterbodies" ] ;
    rdfs:seeAlso [ a <http://purl.org/wf4ever/wfprov#application/json> ;
            dcterms:title "Water Bodies Execution Outputs" ;
            wfprov:rel "child" ;
            oa:hasTarget <https://example.com/open-science-catalog-metadata/products/water-bodies-execution-outputs/collection.json> ],
        [ a <http://purl.org/wf4ever/wfprov#application/json> ;
            dcterms:title "Experiments" ;
            wfprov:rel "parent" ;
            oa:hasTarget <https://example.com/open-science-catalog-metadata/experiments/catalog.json> ],
        [ a <http://purl.org/wf4ever/wfprov#application/json> ;
            wfprov:rel "self" ;
            oa:hasTarget <https://example.com/open-science-catalog-metadata/experiments/water-bodies-execution/record.json> ],
        [ a <http://purl.org/wf4ever/wfprov#application/json> ;
            dcterms:title "An EO data exploitation platform" ;
            wfprov:rel "service" ;
            oa:hasTarget <https://example.com> ],
        [ a <http://purl.org/wf4ever/wfprov#application/json> ;
            dcterms:title "Open Science Catalog" ;
            wfprov:rel "root" ;
            oa:hasTarget <https://example.com/open-science-catalog-metadata/catalog.json> ],
        [ a <http://purl.org/wf4ever/wfprov#application/json> ;
            dcterms:title "Theme: Land" ;
            wfprov:rel "related" ;
            oa:hasTarget <https://example.com/open-science-catalog-metadata/themes/land/catalog.json> ],
        [ a <http://purl.org/wf4ever/wfprov#application/json> ;
            dcterms:title "Workflow: Water Bodies" ;
            wfprov:rel "related" ;
            oa:hasTarget <https://ogc.org/workflows/waterbodies/record.json> ] .


```


### The water bodies experiment with some provenance data attached
This describes an execution of the water bodies example workflow included in the workflows EarthCODE
bblock.

Some notes:
  - Validation fails because 1) OGC Records requires properties.type to be a string, 2) prov-activity
    requires properties.type to be 'Activity' or 'prov:Activity' or an array containing this,
    and 3) EarthCODE requires properties.type to be 'experiment'.
  - The wfprov:usedInput is nearer to a natural representation of the inputs than plain PROV's
    qualifiedUsage. However, there is no equivalent wfprov:generatedOutput, which makes it difficult
    to say that the output is a STAC Collection and that it was the stac_catalog output parameter.
    If you wish to track quality/fit metrics as you develop a workflow or product then a
    wfprov:producedOutput with a describedByParameter might have been useful.
  - hadMember for the stac_items parameter indicates that this is not a string literal input but an
    array of URIs for input entities.
  - The outputs being a child is required in EarthCODE but this constrains catalogue structure
    and results in STAC entities with multiple parents. It doesn't seem fundamentally necessary.
  - Very little runtime information is given, cwltool --provenance emits very little and wf4ever
    doesn't provide a way to represent it. eg, OS, total memory, etc, that are relevant to knowing
    if an experiment can feasibly be repeated.
#### json
```json
{
  "id": "water-bodies-execution",
  "type": "Feature",
  "conformsTo": [
    "http://www.opengis.net/spec/ogcapi-records-1/1.0/req/record-core"
  ],
  "geometry": null,

  "properties": {
    "id": "water-bodies-execution",
    "provType": [
      "Activity",
      "wfprov:WorkflowRun"
    ],
    "startedAtTime": "2025-01-21T17:40:50Z",
    "endedAtTime": "2025-01-21T17:59:50Z",
    "wasAssociatedWith": [
      {
        "agentType": "Person",
        "name": "A Person",
        "actedOnBehalfOf": {
          "agentType": "Organization",
          "name": "An Org"
        }
      }
    ],

    "generated": "https://example.com/open-science-catalog-metadata/products/water-bodies-execution-outputs/collection.json",

    
    "wfprov:describedByWorkflow": "https://example.com/workflows/waterbodies/record.json",
    "wfprov:wasEnactedBy": { 
      "id": "eo-data-platform",
      "type": ["wfprov:WorkfowEngine", "prov:SoftwareAgent", "prov:Agent"],
      "prov:label": "cwltool 3.1.20251031082601"
    },
    "wfprov:usedInput": [
      {
        "type": "wfprov:Artifact",
        "hadMember": [
          "https://earth-search.aws.element84.com/v0/collections/sentinel-s2-l2a-cogs/items/S2B_10TFK_20210713_0_L2A",
          "https://earth-search.aws.element84.com/v0/collections/sentinel-s2-l2a-cogs/items/S2A_10TFK_20220524_0_L2A"
        ],
        "describedByParameter": "stac_items"
      },
      {
        "type": "wfprov:Artifact",
        "data": "-121.399,39.834,-120.74,40.472",
        "describedByParameter": "aoi"
      },
      {
        "type": "wfprov:Artifact",
        "data": "EPSG:4326",
        "describedByParameter": "epsg"
      },
      {
        "type": "wfprov:Artifact",
        "data": [
            "green",
            "nir"
        ],
        "describedByParameter": "bands"
      }
    ],


    "created": "2025-01-21T18:00:00Z",
    "updated": "2025-01-21T18:40:00Z",
    "type": "experiment",
    "title": "Water Bodies Experiment",
    "description": "Experiment using the water bodies workflow.",
    "contacts": [
      {
        "name": "A person",
        "position": "Researcher",
        "organization": "An Org",
        "contactInstructions": "Contact via website",
        "roles": [
          "principal investigator"
        ]
      },
      {
        "name": "An Org",
        "links": [
          {
            "href": "https://example.com/",
            "rel": "about",
            "type": "text/html"
          }
        ],
        "contactInstructions": "SEE WEBSITE",
        "roles": [
          "processor"
        ]
      }
    ],
    "themes": [
      {
        "scheme": "https://github.com/stac-extensions/osc#theme",
        "concepts": [
          {
            "id": "land"
          }
        ]
      }
    ],
    "formats": [
      {
        "name": "GeoTIFF"
      }
    ],
    "license": "proprietary",
    "osc:workflow": "waterbodies",
    "version": "2"
  },
  "linkTemplates": [],
  "links": [
    {
      "rel": "root",
      "href": "https://example.com/open-science-catalog-metadata/catalog.json",
      "type": "application/json",
      "title": "Open Science Catalog"
    },
    {
      "rel": "parent",
      "href": "https://example.com/open-science-catalog-metadata/experiments/catalog.json",
      "type": "application/json",
      "title": "Experiments"
    },
    {
      "rel": "child",
      "href": "https://example.com/open-science-catalog-metadata/products/water-bodies-execution-outputs/collection.json",
      "type": "application/json",
      "title": "Water Bodies Execution Outputs"
    },
    {
      "rel": "service",
      "type": "application/json",
      "title": "An EO data exploitation platform",
      "href": "https://example.com"
    },
    {
      "rel": "related",
      "href": "https://example.com/open-science-catalog-metadata/themes/land/catalog.json",
      "type": "application/json",
      "title": "Theme: Land"
    },
    {
      "rel": "related",
      "href": "https://example.com/open-science-catalog-metadata/workflows/waterbodies/record.json",
      "type": "application/json",
      "title": "Workflow: Water Bodies"
    },
    {
      "rel": "self",
      "href": "https://example.com/open-science-catalog-metadata/experiments/water-bodies-execution/record.json",
      "type": "application/json"
    }
  ]
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/experiments/context.jsonld",
  "id": "water-bodies-execution",
  "type": "Feature",
  "conformsTo": [
    "http://www.opengis.net/spec/ogcapi-records-1/1.0/req/record-core"
  ],
  "geometry": null,
  "properties": {
    "id": "water-bodies-execution",
    "provType": [
      "Activity",
      "wfprov:WorkflowRun"
    ],
    "startedAtTime": "2025-01-21T17:40:50Z",
    "endedAtTime": "2025-01-21T17:59:50Z",
    "wasAssociatedWith": [
      {
        "agentType": "Person",
        "name": "A Person",
        "actedOnBehalfOf": {
          "agentType": "Organization",
          "name": "An Org"
        }
      }
    ],
    "generated": "https://example.com/open-science-catalog-metadata/products/water-bodies-execution-outputs/collection.json",
    "wfprov:describedByWorkflow": "https://example.com/workflows/waterbodies/record.json",
    "wfprov:wasEnactedBy": {
      "id": "eo-data-platform",
      "type": [
        "wfprov:WorkfowEngine",
        "prov:SoftwareAgent",
        "prov:Agent"
      ],
      "prov:label": "cwltool 3.1.20251031082601"
    },
    "wfprov:usedInput": [
      {
        "type": "wfprov:Artifact",
        "hadMember": [
          "https://earth-search.aws.element84.com/v0/collections/sentinel-s2-l2a-cogs/items/S2B_10TFK_20210713_0_L2A",
          "https://earth-search.aws.element84.com/v0/collections/sentinel-s2-l2a-cogs/items/S2A_10TFK_20220524_0_L2A"
        ],
        "describedByParameter": "stac_items"
      },
      {
        "type": "wfprov:Artifact",
        "data": "-121.399,39.834,-120.74,40.472",
        "describedByParameter": "aoi"
      },
      {
        "type": "wfprov:Artifact",
        "data": "EPSG:4326",
        "describedByParameter": "epsg"
      },
      {
        "type": "wfprov:Artifact",
        "data": [
          "green",
          "nir"
        ],
        "describedByParameter": "bands"
      }
    ],
    "created": "2025-01-21T18:00:00Z",
    "updated": "2025-01-21T18:40:00Z",
    "type": "experiment",
    "title": "Water Bodies Experiment",
    "description": "Experiment using the water bodies workflow.",
    "contacts": [
      {
        "name": "A person",
        "position": "Researcher",
        "organization": "An Org",
        "contactInstructions": "Contact via website",
        "roles": [
          "principal investigator"
        ]
      },
      {
        "name": "An Org",
        "links": [
          {
            "href": "https://example.com/",
            "rel": "about",
            "type": "text/html"
          }
        ],
        "contactInstructions": "SEE WEBSITE",
        "roles": [
          "processor"
        ]
      }
    ],
    "themes": [
      {
        "scheme": "https://github.com/stac-extensions/osc#theme",
        "concepts": [
          {
            "id": "land"
          }
        ]
      }
    ],
    "formats": [
      {
        "name": "GeoTIFF"
      }
    ],
    "license": "proprietary",
    "osc:workflow": "waterbodies",
    "version": "2"
  },
  "linkTemplates": [],
  "links": [
    {
      "rel": "root",
      "href": "https://example.com/open-science-catalog-metadata/catalog.json",
      "type": "application/json",
      "title": "Open Science Catalog"
    },
    {
      "rel": "parent",
      "href": "https://example.com/open-science-catalog-metadata/experiments/catalog.json",
      "type": "application/json",
      "title": "Experiments"
    },
    {
      "rel": "child",
      "href": "https://example.com/open-science-catalog-metadata/products/water-bodies-execution-outputs/collection.json",
      "type": "application/json",
      "title": "Water Bodies Execution Outputs"
    },
    {
      "rel": "service",
      "type": "application/json",
      "title": "An EO data exploitation platform",
      "href": "https://example.com"
    },
    {
      "rel": "related",
      "href": "https://example.com/open-science-catalog-metadata/themes/land/catalog.json",
      "type": "application/json",
      "title": "Theme: Land"
    },
    {
      "rel": "related",
      "href": "https://example.com/open-science-catalog-metadata/workflows/waterbodies/record.json",
      "type": "application/json",
      "title": "Workflow: Water Bodies"
    },
    {
      "rel": "self",
      "href": "https://example.com/open-science-catalog-metadata/experiments/water-bodies-execution/record.json",
      "type": "application/json"
    }
  ]
}
```

#### ttl
```ttl
@prefix dcat: <http://www.w3.org/ns/dcat#> .
@prefix dcterms: <http://purl.org/dc/terms/> .
@prefix geojson: <https://purl.org/geojson/vocab#> .
@prefix ns1: <http://www.iana.org/assignments/> .
@prefix ns2: <osc:> .
@prefix oa: <http://www.w3.org/ns/oa#> .
@prefix prov: <http://www.w3.org/ns/prov#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix rec: <https://www.opengis.net/def/ogc-api/records/> .
@prefix thns: <https://w3id.org/ogc/stac/themes/> .
@prefix wfprov: <http://purl.org/wf4ever/wfprov#> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

<https://ogc.org/demo/ospd/eo-data-platform> a wfprov:WorkfowEngine,
        prov:Agent,
        prov:SoftwareAgent ;
    prov:label "cwltool 3.1.20251031082601" .

<https://ogc.org/demo/ospd/water-bodies-execution> a wfprov:WorkflowRun,
        wfprov:experiment,
        prov:Activity,
        geojson:Feature ;
    dcterms:conformsTo <http://www.opengis.net/spec/ogcapi-records-1/1.0/req/record-core> ;
    dcterms:created "2025-01-21T18:00:00Z" ;
    dcterms:description "Experiment using the water bodies workflow." ;
    dcterms:modified "2025-01-21T18:40:00Z" ;
    dcterms:title "Water Bodies Experiment" ;
    wfprov:describedByWorkflow "https://example.com/workflows/waterbodies/record.json" ;
    wfprov:properties <https://ogc.org/demo/ospd/water-bodies-execution> ;
    wfprov:usedInput [ a wfprov:Artifact ;
            wfprov:data "green",
                "nir" ;
            wfprov:describedByParameter "bands" ],
        [ a wfprov:Artifact ;
            wfprov:data "-121.399,39.834,-120.74,40.472" ;
            wfprov:describedByParameter "aoi" ],
        [ a wfprov:Artifact ;
            wfprov:describedByParameter "stac_items" ;
            prov:hadMember <https://earth-search.aws.element84.com/v0/collections/sentinel-s2-l2a-cogs/items/S2A_10TFK_20220524_0_L2A>,
                <https://earth-search.aws.element84.com/v0/collections/sentinel-s2-l2a-cogs/items/S2B_10TFK_20210713_0_L2A> ],
        [ a wfprov:Artifact ;
            wfprov:data "EPSG:4326" ;
            wfprov:describedByParameter "epsg" ] ;
    wfprov:version "2" ;
    wfprov:wasEnactedBy <https://ogc.org/demo/ospd/eo-data-platform> ;
    rdfs:seeAlso [ a <http://purl.org/wf4ever/wfprov#application/json> ;
            dcterms:title "Workflow: Water Bodies" ;
            wfprov:rel "related" ;
            oa:hasTarget <https://example.com/open-science-catalog-metadata/workflows/waterbodies/record.json> ],
        [ a <http://purl.org/wf4ever/wfprov#application/json> ;
            dcterms:title "Theme: Land" ;
            wfprov:rel "related" ;
            oa:hasTarget <https://example.com/open-science-catalog-metadata/themes/land/catalog.json> ],
        [ a <http://purl.org/wf4ever/wfprov#application/json> ;
            dcterms:title "Open Science Catalog" ;
            wfprov:rel "root" ;
            oa:hasTarget <https://example.com/open-science-catalog-metadata/catalog.json> ],
        [ a <http://purl.org/wf4ever/wfprov#application/json> ;
            dcterms:title "An EO data exploitation platform" ;
            wfprov:rel "service" ;
            oa:hasTarget <https://example.com> ],
        [ a <http://purl.org/wf4ever/wfprov#application/json> ;
            wfprov:rel "self" ;
            oa:hasTarget <https://example.com/open-science-catalog-metadata/experiments/water-bodies-execution/record.json> ],
        [ a <http://purl.org/wf4ever/wfprov#application/json> ;
            dcterms:title "Water Bodies Execution Outputs" ;
            wfprov:rel "child" ;
            oa:hasTarget <https://example.com/open-science-catalog-metadata/products/water-bodies-execution-outputs/collection.json> ],
        [ a <http://purl.org/wf4ever/wfprov#application/json> ;
            dcterms:title "Experiments" ;
            wfprov:rel "parent" ;
            oa:hasTarget <https://example.com/open-science-catalog-metadata/experiments/catalog.json> ] ;
    dcat:contactPoint [ rdfs:label "A person" ;
            wfprov:contactInstructions "Contact via website" ;
            wfprov:organization "An Org" ;
            wfprov:position "Researcher" ;
            wfprov:roles "principal investigator" ],
        [ rdfs:label "An Org" ;
            wfprov:contactInstructions "SEE WEBSITE" ;
            wfprov:links [ dcterms:type "text/html" ;
                    ns1:relation <http://www.iana.org/assignments/relation/about> ;
                    oa:hasTarget <https://example.com/> ] ;
            wfprov:roles "processor" ] ;
    dcat:license "proprietary" ;
    prov:endedAtTime "2025-01-21T17:59:50+00:00"^^xsd:dateTime ;
    prov:generated <https://example.com/open-science-catalog-metadata/products/water-bodies-execution-outputs/collection.json> ;
    prov:startedAtTime "2025-01-21T17:40:50+00:00"^^xsd:dateTime ;
    prov:wasAssociatedWith [ a prov:Person ;
            rdfs:label "A Person" ;
            prov:actedOnBehalfOf [ a prov:Organization ;
                    rdfs:label "An Org" ] ] ;
    rec:format [ rec:name "GeoTIFF" ] ;
    rec:themes [ thns:concepts [ thns:id "land" ] ;
            thns:scheme "https://github.com/stac-extensions/osc#theme" ] ;
    ns2:workflow "waterbodies" .


```

## Schema

```yaml
$schema: https://json-schema.org/draft/2020-12/schema
description: EarthCode Experiment
allOf:
- $ref: https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/common/schema.yaml
- $ref: https://ogcincubator.github.io/geodcat-ogcapi-records/build/annotated/geo/geodcat/geodcat-records/schema.yaml
properties:
  properties:
    allOf:
    - $ref: https://ogcincubator.github.io/bblocks-wf4ever/build/annotated/bbr/wf4ever/wfprov/WorkflowRun/schema.yaml
    type: object
    required:
    - osc:workflow
    properties:
      osc:workflow:
        $ref: https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/common/schema.yaml#/$defs/osc:workflow
  links:
    type: array
    items:
      oneOf:
      - title: Other Link
        properties:
          rel:
            not:
              enum:
              - via
              - input
              - environment
      - title: Link to Input Parameter
        properties:
          rel:
            const: input
      - title: Link to Execution Environment
        properties:
          rel:
            const: environment
      - $ref: https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/common/schema.yaml#/$defs/via_links

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/experiments/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/experiments/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "Feature": "geojson:Feature",
    "FeatureCollection": "geojson:FeatureCollection",
    "GeometryCollection": "geojson:GeometryCollection",
    "LineString": "geojson:LineString",
    "MultiLineString": "geojson:MultiLineString",
    "MultiPoint": "geojson:MultiPoint",
    "MultiPolygon": "geojson:MultiPolygon",
    "Point": "geojson:Point",
    "Polygon": "geojson:Polygon",
    "features": {
      "@container": "@set",
      "@id": "geojson:features"
    },
    "type": "@type",
    "id": "@id",
    "geometry": {
      "@context": {
        "coordinates": {
          "@container": "@list",
          "@id": "geojson:coordinates"
        },
        "bbox": {
          "@container": "@list",
          "@id": "geojson:bbox"
        }
      },
      "@id": "geojson:geometry"
    },
    "bbox": "geojson:bbox",
    "links": "rdfs:seeAlso",
    "conformsTo": {
      "@container": "@set",
      "@id": "dct:conformsTo",
      "@type": "@id"
    },
    "time": "dct:temporal",
    "linkTemplates": {
      "@context": {
        "rel": {
          "@context": {
            "@base": "http://www.iana.org/assignments/relation/"
          },
          "@id": "http://www.iana.org/assignments/relation",
          "@type": "@id"
        },
        "type": "dct:format",
        "hreflang": "dct:language",
        "title": "rdfs:label",
        "length": "dct:extent",
        "uriTemplate": {
          "@type": "xsd:string",
          "@id": "rec:uriTemplate"
        },
        "varBase": "rec:varBase",
        "variables": {
          "@id": "rec:hasVariable",
          "@container": "@index",
          "@index": "dct:identifier"
        }
      },
      "@id": "rec:hasLinkTemplate"
    },
    "created": "dct:created",
    "updated": "dct:modified",
    "title": {
      "@container": "@set",
      "@id": "dct:title"
    },
    "description": {
      "@container": "@set",
      "@id": "dct:description"
    },
    "keywords": {
      "@container": "@set",
      "@id": "dcat:keyword"
    },
    "language": {
      "@context": {
        "code": "rec:languageCode",
        "name": "skos:prefLabel"
      },
      "@id": "rec:language"
    },
    "languages": {
      "@context": {
        "code": "rec:languageCode",
        "name": "skos:prefLabel"
      },
      "@container": "@set",
      "@id": "rec:languages"
    },
    "resourceLanguages": {
      "@context": {
        "code": "rec:languageCode",
        "name": "skos:prefLabel"
      },
      "@container": "@set",
      "@id": "rec:resourceLanguages"
    },
    "externalIds": {
      "@context": {
        "scheme": "rec:scheme",
        "value": "rec:id"
      },
      "@container": "@set",
      "@id": "rec:scopedIdentifier"
    },
    "themes": {
      "@context": {
        "concepts": {
          "@context": {
            "id": "thns:id",
            "url": "@id"
          },
          "@id": "thns:concepts",
          "@container": "@set"
        }
      },
      "@container": "@set",
      "@id": "rec:themes"
    },
    "formats": {
      "@context": {
        "name": "rec:name",
        "mediaType": "rec:mediaType"
      },
      "@container": "@set",
      "@id": "rec:format",
      "@type": "@id"
    },
    "contacts": {
      "@context": {
        "logo": {
          "@context": {
            "rel": "http://www.iana.org/assignments/relation",
            "type": "dct:type",
            "hreflang": "dct:language",
            "title": "rdfs:label",
            "length": "dct:extent"
          }
        },
        "links": {
          "@context": {
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
          }
        }
      },
      "@container": "@set",
      "@id": "dcat:contactPoint",
      "@type": "@id"
    },
    "license": "dcat:license",
    "accessrights": "dct:accessRights",
    "variables": {
      "@container": "@id",
      "@id": "rec:hasVariable",
      "@context": {
        "@base": "http://example.com/variables/",
        "@vocab": "https://www.opengis.net/def/ogc-api/records/"
      }
    },
    "stac_extensions": "stac:hasExtension",
    "datetime": "dct:date",
    "start_datetime": "stac:start_datetime",
    "end_datetime": "stac:end_datetime",
    "providers": "stac:hasProvider",
    "assets": {
      "@context": {
        "type": "dct:format",
        "roles": "stac:roles"
      },
      "@id": "stac:hasAsset",
      "@container": "@set"
    },
    "stac_version": "stac:version",
    "media_type": "dct:format",
    "rights": "dcat:rights",
    "extent": "dct:extent",
    "concepts": {
      "@id": "thns:concepts",
      "@container": "@set",
      "@context": {
        "name": "thns:name",
        "id": "thns:id",
        "url": "@id"
      }
    },
    "scheme": "thns:scheme",
    "@vocab": "http://purl.org/wf4ever/wfprov#",
    "wasInfluencedBy": {
      "@context": {
        "type": "dct:type",
        "rel": {
          "@context": {
            "@base": "http://www.iana.org/assignments/relation/"
          },
          "@id": "http://www.iana.org/assignments/relation",
          "@type": "@id"
        },
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
            "type": "dct:type",
            "rel": {
              "@context": {
                "@base": "http://www.iana.org/assignments/relation/"
              },
              "@id": "http://www.iana.org/assignments/relation",
              "@type": "@id"
            },
            "hreflang": "dct:language",
            "title": "rdfs:label",
            "length": "dct:extent"
          },
          "@id": "prov:influencer",
          "@type": "@id"
        },
        "entity": {
          "@context": {
            "has_provenance": {
              "@context": {
                "actedOnBehalfOf": {
                  "@context": {
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
                  "@id": "prov:actedOnBehalfOf",
                  "@type": "@id"
                }
              },
              "@id": "dct:provenance",
              "@type": "@id"
            },
            "wasAttributedTo": {
              "@context": {
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
            "links": {
              "@context": {
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
            }
          },
          "@id": "prov:entity",
          "@type": "@id"
        },
        "agent": {
          "@context": {
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
    "provType": "@type",
    "activityType": "@type",
    "endedAtTime": {
      "@id": "prov:endedAtTime",
      "@type": "xsd:dateTime"
    },
    "wasAssociatedWith": {
      "@context": {
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
      "@context": {
        "has_provenance": {
          "@context": {
            "actedOnBehalfOf": {
              "@context": {
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
              "@id": "prov:actedOnBehalfOf",
              "@type": "@id"
            }
          },
          "@id": "dct:provenance",
          "@type": "@id"
        },
        "wasAttributedTo": {
          "@context": {
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
        "links": {
          "@context": {
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
        "qualifiedAttribution": {
          "@context": {
            "agent": {
              "@context": {
                "actedOnBehalfOf": {
                  "@context": {
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
                  "@id": "prov:actedOnBehalfOf",
                  "@type": "@id"
                }
              },
              "@id": "prov:agent",
              "@type": "@id"
            }
          },
          "@id": "prov:qualifiedAttribution",
          "@type": "@id"
        }
      },
      "@id": "prov:used",
      "@type": "@id"
    },
    "wasStartedBy": {
      "@context": {
        "has_provenance": {
          "@context": {
            "actedOnBehalfOf": {
              "@context": {
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
              "@id": "prov:actedOnBehalfOf",
              "@type": "@id"
            }
          },
          "@id": "dct:provenance",
          "@type": "@id"
        },
        "wasAttributedTo": {
          "@context": {
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
        "links": {
          "@context": {
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
        "qualifiedAttribution": {
          "@context": {
            "agent": {
              "@context": {
                "actedOnBehalfOf": {
                  "@context": {
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
                  "@id": "prov:actedOnBehalfOf",
                  "@type": "@id"
                }
              },
              "@id": "prov:agent",
              "@type": "@id"
            }
          },
          "@id": "prov:qualifiedAttribution",
          "@type": "@id"
        }
      },
      "@id": "prov:wasStartedBy",
      "@type": "@id"
    },
    "wasEndedBy": {
      "@context": {
        "has_provenance": {
          "@context": {
            "actedOnBehalfOf": {
              "@context": {
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
              "@id": "prov:actedOnBehalfOf",
              "@type": "@id"
            }
          },
          "@id": "dct:provenance",
          "@type": "@id"
        },
        "wasAttributedTo": {
          "@context": {
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
        "links": {
          "@context": {
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
        "qualifiedAttribution": {
          "@context": {
            "agent": {
              "@context": {
                "actedOnBehalfOf": {
                  "@context": {
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
                  "@id": "prov:actedOnBehalfOf",
                  "@type": "@id"
                }
              },
              "@id": "prov:agent",
              "@type": "@id"
            }
          },
          "@id": "prov:qualifiedAttribution",
          "@type": "@id"
        }
      },
      "@id": "prov:wasEndedBy",
      "@type": "@id"
    },
    "invalidated": {
      "@context": {
        "has_provenance": {
          "@context": {
            "actedOnBehalfOf": {
              "@context": {
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
              "@id": "prov:actedOnBehalfOf",
              "@type": "@id"
            }
          },
          "@id": "dct:provenance",
          "@type": "@id"
        },
        "wasAttributedTo": {
          "@context": {
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
        "links": {
          "@context": {
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
        "qualifiedAttribution": {
          "@context": {
            "agent": {
              "@context": {
                "actedOnBehalfOf": {
                  "@context": {
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
                  "@id": "prov:actedOnBehalfOf",
                  "@type": "@id"
                }
              },
              "@id": "prov:agent",
              "@type": "@id"
            }
          },
          "@id": "prov:qualifiedAttribution",
          "@type": "@id"
        }
      },
      "@id": "prov:invalidated",
      "@type": "@id"
    },
    "generated": {
      "@context": {
        "has_provenance": {
          "@context": {
            "actedOnBehalfOf": {
              "@context": {
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
              "@id": "prov:actedOnBehalfOf",
              "@type": "@id"
            }
          },
          "@id": "dct:provenance",
          "@type": "@id"
        },
        "wasAttributedTo": {
          "@context": {
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
        "links": {
          "@context": {
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
        "qualifiedAttribution": {
          "@context": {
            "agent": {
              "@context": {
                "actedOnBehalfOf": {
                  "@context": {
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
                  "@id": "prov:actedOnBehalfOf",
                  "@type": "@id"
                }
              },
              "@id": "prov:agent",
              "@type": "@id"
            }
          },
          "@id": "prov:qualifiedAttribution",
          "@type": "@id"
        }
      },
      "@id": "prov:generated",
      "@type": "@id"
    },
    "atLocation": {
      "@id": "prov:atLocation",
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
      "@context": {
        "entity": {
          "@context": {
            "has_provenance": {
              "@context": {
                "actedOnBehalfOf": {
                  "@context": {
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
                  "@id": "prov:actedOnBehalfOf",
                  "@type": "@id"
                }
              },
              "@id": "dct:provenance",
              "@type": "@id"
            },
            "wasAttributedTo": {
              "@context": {
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
            "links": {
              "@context": {
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
            "qualifiedAttribution": {
              "@context": {
                "agent": {
                  "@context": {
                    "actedOnBehalfOf": {
                      "@context": {
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
                      "@id": "prov:actedOnBehalfOf",
                      "@type": "@id"
                    }
                  },
                  "@id": "prov:agent",
                  "@type": "@id"
                }
              },
              "@id": "prov:qualifiedAttribution",
              "@type": "@id"
            }
          },
          "@id": "prov:entity",
          "@type": "@id"
        }
      },
      "@id": "prov:qualifiedStart",
      "@type": "@id"
    },
    "qualifiedEnd": {
      "@context": {
        "entity": {
          "@context": {
            "has_provenance": {
              "@context": {
                "actedOnBehalfOf": {
                  "@context": {
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
                  "@id": "prov:actedOnBehalfOf",
                  "@type": "@id"
                }
              },
              "@id": "dct:provenance",
              "@type": "@id"
            },
            "wasAttributedTo": {
              "@context": {
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
            "links": {
              "@context": {
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
            "qualifiedAttribution": {
              "@context": {
                "agent": {
                  "@context": {
                    "actedOnBehalfOf": {
                      "@context": {
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
                      "@id": "prov:actedOnBehalfOf",
                      "@type": "@id"
                    }
                  },
                  "@id": "prov:agent",
                  "@type": "@id"
                }
              },
              "@id": "prov:qualifiedAttribution",
              "@type": "@id"
            }
          },
          "@id": "prov:entity",
          "@type": "@id"
        }
      },
      "@id": "prov:qualifiedEnd",
      "@type": "@id"
    },
    "qualifiedAssociation": {
      "@context": {
        "agent": {
          "@context": {
            "actedOnBehalfOf": {
              "@context": {
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
              "@id": "prov:actedOnBehalfOf",
              "@type": "@id"
            }
          },
          "@id": "prov:agent",
          "@type": "@id"
        }
      },
      "@id": "prov:qualifiedAssociation",
      "@type": "@id"
    },
    "agentType": "@type",
    "entityType": "@type",
    "featureType": "@type",
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
    "generatedAtTime": {
      "@id": "prov:generatedAtTime",
      "@type": "xsd:dateTime"
    },
    "invalidatedAtTime": {
      "@id": "prov:invalidatedAtTime",
      "@type": "xsd:dateTime"
    },
    "startedAtTime": {
      "@id": "prov:startedAtTime",
      "@type": "xsd:dateTime"
    },
    "value": "prov:value",
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
    "alternateOf": {
      "@id": "prov:alternateOf",
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
    "hadMember": {
      "@id": "prov:hadMember",
      "@type": "@id"
    },
    "hadPlan": {
      "@id": "prov:hadPlan",
      "@type": "@id"
    },
    "hadPrimarySource": {
      "@id": "prov:hadPrimarySource",
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
    "qualifiedAttribution": {
      "@id": "prov:qualifiedAttribution",
      "@type": "@id"
    },
    "qualifiedDelegation": {
      "@id": "prov:qualifiedDelegation",
      "@type": "@id"
    },
    "qualifiedDerivation": {
      "@id": "prov:qualifiedDerivation",
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
    "specializationOf": {
      "@id": "prov:specializationOf",
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
    "wasGeneratedBy": {
      "@id": "prov:wasGeneratedBy",
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
    "has_anchor": {
      "@id": "prov:has_anchor",
      "@type": "@id"
    },
    "has_provenance": {
      "@id": "dct:provenance",
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
    "ProcessRun": "wfprov:ProcessRun",
    "WorkflowRun": "wfprov:WorkflowRun",
    "wasOutputFrom": {
      "@id": "prov:generated",
      "@type": "@id",
      "@container": "@set"
    },
    "describedByProcess": {
      "@id": "wfprov:describedByProcess",
      "@type": "@id"
    },
    "usedInput": {
      "@id": "wfprov:usedInput",
      "@type": "@id",
      "@container": "@set"
    },
    "wasPartOfWorkflowRun": {
      "@id": "wfprov:wasPartOfWorkflowRun",
      "@type": "@id"
    },
    "wasEnactedBy": {
      "@id": "prov:wasAssociatedWith",
      "@type": "@id"
    },
    "describedByWorkflow": {
      "@id": "wfprov:describedByWorkflow",
      "@type": "@id"
    },
    "hadSubProcessRun": {
      "@reverse": "wfprov:wasPartOfWorkflowRun",
      "@type": "@id",
      "@container": "@set"
    },
    "href": {
      "@type": "@id",
      "@id": "oa:hasTarget"
    },
    "geojson": "https://purl.org/geojson/vocab#",
    "rdfs": "http://www.w3.org/2000/01/rdf-schema#",
    "oa": "http://www.w3.org/ns/oa#",
    "dct": "http://purl.org/dc/terms/",
    "dcat": "http://www.w3.org/ns/dcat#",
    "rec": "https://www.opengis.net/def/ogc-api/records/",
    "skos": "http://www.w3.org/2004/02/skos/core#",
    "xsd": "http://www.w3.org/2001/XMLSchema#",
    "owl": "http://www.w3.org/2002/07/owl#",
    "rdf": "http://www.w3.org/1999/02/22-rdf-syntax-ns#",
    "w3ctime": "http://www.w3.org/2006/time#",
    "dctype": "http://purl.org/dc/dcmitype/",
    "vcard": "http://www.w3.org/2006/vcard/ns#",
    "prov": "http://www.w3.org/ns/prov#",
    "foaf": "http://xmlns.com/foaf/0.1/",
    "thns": "https://w3id.org/ogc/stac/themes/",
    "stac": "https://w3id.org/ogc/stac/core/",
    "wfprov": "http://purl.org/wf4ever/wfprov#",
    "wfdesc": "http://purl.org/wf4ever/wfdesc#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/experiments/context.jsonld)

## Sources

* [GeoDCAT Specification](http://www.opengis.net/def/metamodel/profiles/geodcat)
* [EarthCODE](https://earthcode.esa.int/)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-openscience](https://github.com/ogcincubator/bblocks-openscience)
* Path: `_sources/geodcat-stac-earthcode/experiments`

