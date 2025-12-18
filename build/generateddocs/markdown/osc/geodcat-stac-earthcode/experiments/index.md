
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

### An example demonstrating EO extension fields in a STAC item.
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
  "@context": "https://nenadradosevic.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/experiments/context.jsonld",
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
@prefix : <https://w3id.org/ogc/stac/assets/> .
@prefix dcat: <http://www.w3.org/ns/dcat#> .
@prefix dcterms: <http://purl.org/dc/terms/> .
@prefix geojson: <https://purl.org/geojson/vocab#> .
@prefix ns1: <http://www.iana.org/assignments/> .
@prefix ns2: <osc:> .
@prefix oa: <http://www.w3.org/ns/oa#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix rec: <https://www.opengis.net/def/ogc-api/records/> .
@prefix stac: <https://w3id.org/ogc/stac/core/> .
@prefix thns: <https://w3id.org/ogc/stac/themes/> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

<https://ogc.org/demo/ospd/polaris-experiment> a geojson:Feature ;
    dcterms:conformsTo <http://www.opengis.net/spec/ogcapi-records-1/1.0/req/record-core> ;
    rdfs:seeAlso [ dcterms:format "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/self> ;
            oa:hasTarget <https://esa-earthcode.github.io/open-science-catalog-metadata/experiments/polaris-experiment/item.json> ],
        [ rdfs:label "Open Science Catalog" ;
            dcterms:format "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/root> ;
            oa:hasTarget <https://ogc.org/catalog.json> ],
        [ rdfs:label "Input parameters" ;
            dcterms:format "application/yaml" ;
            ns1:relation <http://www.iana.org/assignments/relation/input> ;
            oa:hasTarget <https://ogc.org/demo/ospd/input.yaml> ],
        [ rdfs:label "Experiments" ;
            dcterms:format "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/parent> ;
            oa:hasTarget <https://ogc.org/demo/catalog.json> ],
        [ rdfs:label "Theme: Oceans" ;
            dcterms:format "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/related> ;
            oa:hasTarget <https://ogc.org/themes/oceans/catalog.json> ],
        [ rdfs:label "Execution environment" ;
            dcterms:format "application/yaml" ;
            ns1:relation <http://www.iana.org/assignments/relation/environment> ;
            oa:hasTarget <https://ogc.org/demo/ospd/environment.yaml> ],
        [ rdfs:label "Workflow: POLARIS" ;
            dcterms:format "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/related> ;
            oa:hasTarget <https://ogc.org/workflows/polaris-workflow/record.json> ],
        [ rdfs:label "POLARIS" ;
            dcterms:format "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/child> ;
            oa:hasTarget <https://ogc.org/products/polaris/collection.json> ] ;
    :properties [ a :experiment ;
            dcterms:created "2025-02-19T23:00:00Z" ;
            dcterms:description "Polar Operational Limit Assessment Risk Index System (POLARIS)" ;
            dcterms:modified "2025-02-19T23:00:00Z" ;
            dcterms:title "POLARIS" ;
            dcat:contactPoint [ :contactInstructions "Contact via EarthCODE" ;
                    :links [ dcterms:type "text/html" ;
                            ns1:relation <http://www.iana.org/assignments/relation/about> ;
                            oa:hasTarget <https://opensciencedata.esa.int/> ] ;
                    :name "EarthCODE Demo" ;
                    :organization "EarthCODE" ;
                    stac:roles "host" ] ;
            dcat:keyword "polar",
                "sea ice" ;
            dcat:license "CC-BY-SA-4.0" ;
            :version "2" ;
            rec:format [ rec:name "GeoTIFF" ] ;
            rec:themes [ thns:concepts [ thns:id "oceans"^^xsd:string ] ;
                    thns:scheme "https://github.com/stac-extensions/osc#theme" ] ;
            ns2:workflow "polaris-workflow" ] .


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
    a wfprov:ProcessRun ;
    wfprov:usedInput
        wfkg:CSVSummary ,
        wfkg:GeoTIFFRaster ;
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
@prefix : <https://w3id.org/ogc/stac/assets/> .
@prefix dcat: <http://www.w3.org/ns/dcat#> .
@prefix dcterms: <http://purl.org/dc/terms/> .
@prefix geojson: <https://purl.org/geojson/vocab#> .
@prefix ns1: <http://www.iana.org/assignments/> .
@prefix ns2: <osc:> .
@prefix oa: <http://www.w3.org/ns/oa#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix rec: <https://www.opengis.net/def/ogc-api/records/> .
@prefix stac: <https://w3id.org/ogc/stac/core/> .
@prefix thns: <https://w3id.org/ogc/stac/themes/> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

<https://ogc.org/demo/ospd/kindgrove/kindgrove-experiment> a geojson:Feature ;
    dcterms:conformsTo <http://www.opengis.net/spec/ogcapi-records-1/1.0/req/record-core> ;
    rdfs:seeAlso [ rdfs:label "Execution provenance" ;
            dcterms:format "application/ld+json" ;
            ns1:relation <http://www.iana.org/assignments/relation/related> ;
            oa:hasTarget <https://ogc.org/demo/ospd/provenance/kindgrove-run.jsonld> ],
        [ rdfs:label "Workflow description" ;
            dcterms:format "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/related> ;
            oa:hasTarget <https://ogc.org/demo/ospd/workflows/kindgrove-workflow/record.json> ] ;
    :properties [ a :experiment ;
            dcterms:created "2024-06-01T10:00:00Z" ;
            dcterms:description "An Earth observation workflow for mangrove detection and carbon stock estimation using Sentinel-2 imagery." ;
            dcterms:modified "2024-06-01T10:45:00Z" ;
            dcterms:title "KindGrove Mangrove Carbon Assessment" ;
            dcat:contactPoint [ :name "Cameron Sajedi" ;
                    :organization "Starling Foundries" ;
                    stac:roles "author",
                        "operator" ] ;
            dcat:keyword "Sentinel-2",
                "carbon",
                "climate",
                "mangroves",
                "remote sensing" ;
            dcat:license "CC-BY-4.0" ;
            :version "1.0" ;
            rec:format [ rec:name "CSV" ],
                [ rec:name "GeoTIFF" ] ;
            rec:themes [ thns:concepts [ thns:id "ecosystems"^^xsd:string ],
                        [ thns:id "climate"^^xsd:string ] ;
                    thns:scheme "https://github.com/stac-extensions/osc#theme" ] ;
            ns2:workflow "kindgrove-workflow" ] .


```

## Schema

```yaml
$schema: https://json-schema.org/draft/2020-12/schema
description: EarthCode Experiment
allOf:
- $ref: https://nenadradosevic.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/common/schema.yaml
- $ref: https://ogcincubator.github.io/geodcat-ogcapi-records/build/annotated/geo/geodcat/geodcat-records/schema.yaml
properties:
  properties:
    type: object
    required:
    - osc:workflow
    properties:
      osc:workflow:
        $ref: https://nenadradosevic.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/common/schema.yaml#/$defs/osc:workflow
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
      - $ref: https://nenadradosevic.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/common/schema.yaml#/$defs/via_links

```

Links to the schema:

* YAML version: [schema.yaml](https://nenadradosevic.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/experiments/schema.json)
* JSON version: [schema.json](https://nenadradosevic.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/experiments/schema.yaml)


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
    "properties": {},
    "geometry": {
      "@context": {
        "coordinates": {
          "@container": "@list",
          "@id": "geojson:coordinates"
        },
        "geometries": {}
      },
      "@id": "geojson:geometry"
    },
    "bbox": {
      "@container": "@list",
      "@id": "geojson:bbox"
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
        "type": "dct:format",
        "hreflang": "dct:language",
        "title": "rdfs:label",
        "length": "dct:extent",
        "anchor": {},
        "method": {},
        "headers": {},
        "body": {}
      },
      "@id": "rdfs:seeAlso"
    },
    "conformsTo": {
      "@container": "@set",
      "@id": "dct:conformsTo",
      "@type": "@id"
    },
    "time": {
      "@context": {
        "date": {},
        "timestamp": {},
        "interval": {},
        "resolution": {}
      },
      "@id": "dct:temporal"
    },
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
      "@id": "rec:language",
      "@context": {
        "code": "rec:languageCode",
        "name": "skos:prefLabel",
        "alternate": {},
        "dir": {}
      }
    },
    "languages": {
      "@container": "@set",
      "@id": "rec:languages",
      "@context": {
        "code": "rec:languageCode",
        "name": "skos:prefLabel",
        "alternate": {},
        "dir": {}
      }
    },
    "resourceLanguages": {
      "@container": "@set",
      "@id": "rec:resourceLanguages",
      "@context": {
        "code": "rec:languageCode",
        "name": "skos:prefLabel",
        "alternate": {},
        "dir": {}
      }
    },
    "externalIds": {
      "@container": "@set",
      "@id": "rec:scopedIdentifier",
      "@context": {
        "scheme": "rec:scheme",
        "value": "rec:id"
      }
    },
    "themes": {
      "@container": "@set",
      "@id": "rec:themes",
      "@context": {
        "concepts": {
          "@id": "thns:concepts",
          "@context": {
            "id": {
              "@type": "xsd:string",
              "@id": "thns:id"
            },
            "url": {
              "@type": "@id",
              "@id": "@id"
            }
          },
          "@container": "@set"
        }
      }
    },
    "formats": {
      "@id": "rec:format",
      "@context": {
        "name": "rec:name",
        "mediaType": "rec:mediaType"
      },
      "@container": "@set",
      "@type": "@id"
    },
    "contacts": {
      "@container": "@set",
      "@id": "dcat:contactPoint",
      "@type": "@id",
      "@context": {
        "identifier": {},
        "name": {},
        "position": {},
        "organization": {},
        "logo": {
          "@context": {
            "rel": {
              "@context": {
                "@base": "http://www.iana.org/assignments/relation/"
              },
              "@id": "http://www.iana.org/assignments/relation",
              "@type": "@id"
            },
            "anchor": {},
            "type": "dct:type",
            "hreflang": "dct:language",
            "title": "rdfs:label",
            "length": "dct:extent"
          }
        },
        "phones": {
          "@context": {
            "value": {}
          }
        },
        "emails": {
          "@context": {
            "value": {}
          }
        },
        "addresses": {
          "@context": {
            "deliveryPoint": {},
            "city": {},
            "administrativeArea": {},
            "postalCode": {},
            "country": {}
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
            "anchor": {},
            "type": "dct:type",
            "hreflang": "dct:language",
            "title": "rdfs:label",
            "length": "dct:extent"
          }
        },
        "hoursOfService": {},
        "contactInstructions": {}
      }
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
    "collection": {},
    "stac_extensions": "stac:hasExtension",
    "roles": {
      "@id": "stac:roles",
      "@container": "@set"
    },
    "bands": {
      "@context": {
        "name": {}
      }
    },
    "datetime": {
      "@id": "dct:date",
      "@type": "xsd:dateTime"
    },
    "start_datetime": {},
    "end_datetime": {},
    "data_type": {},
    "nodata": {},
    "statistics": {
      "@context": {
        "minimum": {},
        "maximum": {},
        "mean": {},
        "stddev": {},
        "count": {},
        "valid_percent": {}
      }
    },
    "unit": {},
    "platform": {},
    "instruments": {},
    "constellation": {},
    "mission": {},
    "gsd": {},
    "providers": {
      "@context": {
        "name": {},
        "url": {}
      }
    },
    "rights": "dcat:rights",
    "@vocab": "https://w3id.org/ogc/stac/assets/",
    "assets": {
      "@context": {
        "type": "dct:format"
      },
      "@id": "stac:hasAsset",
      "@container": "@set"
    },
    "stac_version": "stac:version",
    "media_type": "dct:format",
    "extent": {
      "@id": "dct:extent",
      "@context": {
        "spatial": {},
        "temporal": {
          "@context": {
            "interval": {}
          }
        }
      }
    },
    "item_assets": {},
    "summaries": {
      "@context": {
        "minimum": {},
        "maximum": {}
      }
    },
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
    "osc:type": {},
    "osc:status": {},
    "osc:project": {},
    "osc:region": {},
    "osc:variables": {},
    "osc:missions": {},
    "osc:experiment": {},
    "osc:workflows": {},
    "osc:workflow": {},
    "rel": {},
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
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://nenadradosevic.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/experiments/context.jsonld)

## Sources

* [GeoDCAT Specification](http://www.opengis.net/def/metamodel/profiles/geodcat)
* [EarthCODE]({
      "title": "GeoDCAT Specification",
      "link": "http://www.opengis.net/def/metamodel/profiles/geodcat"
    },)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/nenadradosevic/bblocks-openscience](https://github.com/nenadradosevic/bblocks-openscience)
* Path: `_sources/geodcat-stac-earthcode/experiments`

