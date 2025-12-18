
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
    rdfs:seeAlso [ rdfs:label "Input parameters" ;
            dcterms:format "application/yaml" ;
            ns1:relation <http://www.iana.org/assignments/relation/input> ;
            oa:hasTarget <https://ogc.org/demo/ospd/input.yaml> ],
        [ rdfs:label "Experiments" ;
            dcterms:format "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/parent> ;
            oa:hasTarget <https://ogc.org/demo/catalog.json> ],
        [ rdfs:label "Execution environment" ;
            dcterms:format "application/yaml" ;
            ns1:relation <http://www.iana.org/assignments/relation/environment> ;
            oa:hasTarget <https://ogc.org/demo/ospd/environment.yaml> ],
        [ dcterms:format "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/self> ;
            oa:hasTarget <https://esa-earthcode.github.io/open-science-catalog-metadata/experiments/polaris-experiment/item.json> ],
        [ rdfs:label "POLARIS" ;
            dcterms:format "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/child> ;
            oa:hasTarget <https://ogc.org/products/polaris/collection.json> ],
        [ rdfs:label "Open Science Catalog" ;
            dcterms:format "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/root> ;
            oa:hasTarget <https://ogc.org/catalog.json> ],
        [ rdfs:label "Theme: Oceans" ;
            dcterms:format "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/related> ;
            oa:hasTarget <https://ogc.org/themes/oceans/catalog.json> ],
        [ rdfs:label "Workflow: POLARIS" ;
            dcterms:format "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/related> ;
            oa:hasTarget <https://ogc.org/workflows/polaris-workflow/record.json> ] ;
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
@prefix kg: <https://example.org/kindgrove/> .
@prefix prov: <http://www.w3.org/ns/prov#> .
@prefix wfprov: <http://purl.org/wf4ever/wfprov#> .
@prefix wfdesc: <http://purl.org/wf4ever/wfdesc#> .
@prefix foaf: <http://xmlns.com/foaf/0.1/> .
@prefix schema: <https://schema.org/> .
@prefix stac: <https://stacspec.org/ontology#> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

#################################################################
# 1. WORKFLOW INPUTS
#################################################################

kg:Sentinel2L2A
    a wfprov:Artifact , stac:Item ;
    schema:name "Sentinel-2 L2A Multispectral Optical Imagery" ;
    stac:resolution "10m" ;
    stac:collection "sentinel-2-l2a" .

kg:AWSSTACCatalog
    a wfprov:Artifact , stac:Catalog ;
    schema:name "AWS STAC Catalog (element84)" ;
    schema:url "https://earth-search.aws.element84.com/v1" .

#################################################################
# 2. WORKFLOW PROCESSES (PROCESS RUNS)
#################################################################

kg:KindGroveWorkflow
    a wfdesc:Workflow , schema:ComputationalWorkflow ;
    schema:name "KindGrove Mangrove Carbon Assessment Workflow" ;
    schema:version "1.0" .

kg:KindGroveWorkflowRun
    a wfprov:WorkflowRun , schema:CreateAction ;
    wfprov:describedByWorkflow kg:KindGroveWorkflow ;
    wfprov:wasInitiatedBy kg:CameronSajedi ;
    prov:startedAtTime "2024-06-01T10:00:00Z"^^xsd:dateTime ;
    prov:endedAtTime "2024-06-01T10:45:00Z"^^xsd:dateTime .

kg:SelectScenesProcess
    a wfprov:ProcessRun ;
    wfprov:usedInput kg:AWSSTACCatalog ;
    wfprov:usedInput kg:Sentinel2L2A ;
    wfprov:wasPartOfWorkflowRun kg:KindGroveWorkflowRun ;
    wfprov:wasEnactedBy kg:JupyterNotebookEngine .

kg:DownloadBandsProcess
    a wfprov:ProcessRun ;
    wfprov:usedInput kg:Sentinel2L2A ;
    wfprov:wasPartOfWorkflowRun kg:KindGroveWorkflowRun ;
    wfprov:wasEnactedBy kg:JupyterNotebookEngine .

kg:CalculateVegetationIndicesProcess
    a wfprov:ProcessRun ;
    wfprov:usedInput kg:Sentinel2L2A ;
    wfprov:wasPartOfWorkflowRun kg:KindGroveWorkflowRun ;
    wfprov:wasEnactedBy kg:JupyterNotebookEngine .

kg:ApplyThresholdClassificationProcess
    a wfprov:ProcessRun ;
    wfprov:wasPartOfWorkflowRun kg:KindGroveWorkflowRun ;
    wfprov:wasEnactedBy kg:JupyterNotebookEngine .

kg:DetectedMangroveMaskProcess
    a wfprov:ProcessRun ;
    wfprov:wasPartOfWorkflowRun kg:KindGroveWorkflowRun ;
    wfprov:wasEnactedBy kg:JupyterNotebookEngine .

kg:ApplyAllometricEquationProcess
    a wfprov:ProcessRun ;
    wfprov:wasPartOfWorkflowRun kg:KindGroveWorkflowRun ;
    wfprov:wasEnactedBy kg:JupyterNotebookEngine .

kg:CalculateCarbonStockProcess
    a wfprov:ProcessRun ;
    wfprov:wasPartOfWorkflowRun kg:KindGroveWorkflowRun ;
    wfprov:wasEnactedBy kg:JupyterNotebookEngine .

kg:CalculateCO2EquivalentProcess
    a wfprov:ProcessRun ;
    wfprov:wasPartOfWorkflowRun kg:KindGroveWorkflowRun ;
    wfprov:wasEnactedBy kg:JupyterNotebookEngine .

kg:ExportResultsProcess
    a wfprov:ProcessRun ;
    wfprov:wasPartOfWorkflowRun kg:KindGroveWorkflowRun ;
    wfprov:wasEnactedBy kg:JupyterNotebookEngine .

#################################################################
# 3. WORKFLOW OUTPUTS
#################################################################

kg:MangroveMask
    a wfprov:Artifact ;
    schema:name "Detected Mangrove Mask" ;
    prov:wasGeneratedBy kg:DetectedMangroveMaskProcess ;
    prov:wasDerivedFrom kg:Sentinel2L2A .

kg:CarbonStockEstimate
    a wfprov:Artifact ;
    schema:name "Estimated Mangrove Carbon Stock" ;
    prov:wasGeneratedBy kg:CalculateCarbonStockProcess ;
    prov:wasDerivedFrom kg:MangroveMask .

kg:CO2EquivalentEstimate
    a wfprov:Artifact ;
    schema:name "CO2 Equivalent Estimate" ;
    prov:wasGeneratedBy kg:CalculateCO2EquivalentProcess ;
    prov:wasDerivedFrom kg:CarbonStockEstimate .

kg:GeoTIFFRaster
    a wfprov:Artifact , stac:Asset ;
    schema:encodingFormat "image/tiff" ;
    prov:wasGeneratedBy kg:ExportResultsProcess .

kg:CSVSummary
    a wfprov:Artifact , schema:Dataset ;
    schema:encodingFormat "text/csv" ;
    prov:wasGeneratedBy kg:ExportResultsProcess .

kg:InteractiveVisualisation
    a wfprov:Artifact ;
    schema:name "Interactive Visualisation Outputs" ;
    prov:wasGeneratedBy kg:ExportResultsProcess .

#################################################################
# 4. WORKFLOW AGENT (PERSON, ORGANISATION, ENGINE)
#################################################################

kg:CameronSajedi
    a prov:Person , foaf:Person , schema:Person ;
    schema:name "Cameron Sajedi" ;
    schema:affiliation kg:StarlingFoundries .

kg:StarlingFoundries
    a prov:Organization , foaf:Organization , schema:Organization ;
    schema:name "Starling Foundries" .

kg:JupyterNotebookEngine
    a wfprov:WorkflowEngine , prov:SoftwareAgent , schema:SoftwareApplication ;
    schema:name "Jupyter Notebook" ;
    prov:actedOnBehalfOf kg:CameronSajedi .

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
@prefix ns1: <osc:> .
@prefix ns2: <http://www.iana.org/assignments/> .
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
            ns2:relation <http://www.iana.org/assignments/relation/related> ;
            oa:hasTarget <https://ogc.org/demo/ospd/provenance/kindgrove-run.jsonld> ],
        [ rdfs:label "Workflow description" ;
            dcterms:format "application/json" ;
            ns2:relation <http://www.iana.org/assignments/relation/related> ;
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
            rec:themes [ thns:concepts [ thns:id "climate"^^xsd:string ],
                        [ thns:id "ecosystems"^^xsd:string ] ;
                    thns:scheme "https://github.com/stac-extensions/osc#theme" ] ;
            ns1:workflow "kindgrove-workflow" ] .


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

