
# EarthCODE Workflow (Schema)

`ogc.osc.geodcat-stac-earthcode.workflows` *v0.1*

EarthCODE metadata profile linked to semantic models

[*Status*](http://www.opengis.net/def/status): Under development

## Description

## ESA EarthCODE workflow 



## Examples

### Polar Warp
The polarwarp algorithm geolocates, aligns, and warps satellite SAR images using forecast drift and wind/tide fields in polar regions. It takes ice drift vectors from multiple data sources (SAR, TOPAZ4, ICON, tide models), translates them into pixel displacements, and applies thin-plate spline warping to generate temporally aligned and drift-corrected imagery. This enables monitoring of sea ice motion over forecast windows while preserving georeferencing.


### Polaris
The Polar Operational Limit Assessment Risk Indexing System (POLARIS) is a methodology to assess the risk posed to a ship by ice conditions in relation to the ship's assigned ice class. It uses the WMO standard sea ice charts as the basis for the calculation.
#### json
```json
{
  "id": "polaris-workflow",
  "type": "Feature",
  "conformsTo": [
    "http://www.opengis.net/spec/ogcapi-records-1/1.0/req/record-core"
  ],
  "geometry": null,
  "properties": {
    "created": "2025-02-19T23:00:00Z",
    "updated": "2025-03-03T22:00:00Z",
    "type": "workflow",
    "title": "POLARIS",
    "description": "Polar Operational Limit Assessment Risk Index System (POLARIS) algorithm.",
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
        "concepts": [
          {
            "id": "oceans"
          }
        ],
        "scheme": "https://github.com/stac-extensions/osc#theme"
      }
    ],
    "formats": [
      {
        "name": "GeoTIFF"
      }
    ],
    "license": "CC-BY-SA-4.0",
    "osc:project": "polaris"
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
      "title": "Workflows"
    },
    {
      "rel": "self",
      "href": "https://esa-earthcode.github.io/open-science-catalog-metadata/workflows/polaris-workflow/record.json",
      "type": "application/json"
    },
    {
      "rel": "related",
      "href": "../../projects/polaris/collection.json",
      "type": "application/json",
      "title": "Project: POLARIS"
    },
    {
      "rel": "child",
      "href": "../../experiments/polaris-experiment/record.json",
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
      "rel": "application",
      "type": "application/json",
      "title": "OGC Application Package",
      "href": "https://github.com/gtif-cerulean/cerulean-catalog.git"
    },
    {
      "rel": "git",
      "type": "application/json",
      "title": "Git source repository",
      "href": "https://github.com/gtif-cerulean/cerulean-catalog.git"
    }
  ]
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/workflows/context.jsonld",
  "id": "polaris-workflow",
  "type": "Feature",
  "conformsTo": [
    "http://www.opengis.net/spec/ogcapi-records-1/1.0/req/record-core"
  ],
  "geometry": null,
  "properties": {
    "created": "2025-02-19T23:00:00Z",
    "updated": "2025-03-03T22:00:00Z",
    "type": "workflow",
    "title": "POLARIS",
    "description": "Polar Operational Limit Assessment Risk Index System (POLARIS) algorithm.",
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
        "concepts": [
          {
            "id": "oceans"
          }
        ],
        "scheme": "https://github.com/stac-extensions/osc#theme"
      }
    ],
    "formats": [
      {
        "name": "GeoTIFF"
      }
    ],
    "license": "CC-BY-SA-4.0",
    "osc:project": "polaris"
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
      "title": "Workflows"
    },
    {
      "rel": "self",
      "href": "https://esa-earthcode.github.io/open-science-catalog-metadata/workflows/polaris-workflow/record.json",
      "type": "application/json"
    },
    {
      "rel": "related",
      "href": "../../projects/polaris/collection.json",
      "type": "application/json",
      "title": "Project: POLARIS"
    },
    {
      "rel": "child",
      "href": "../../experiments/polaris-experiment/record.json",
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
      "rel": "application",
      "type": "application/json",
      "title": "OGC Application Package",
      "href": "https://github.com/gtif-cerulean/cerulean-catalog.git"
    },
    {
      "rel": "git",
      "type": "application/json",
      "title": "Git source repository",
      "href": "https://github.com/gtif-cerulean/cerulean-catalog.git"
    }
  ]
}
```

#### ttl
```ttl
@prefix dcat: <http://www.w3.org/ns/dcat#> .
@prefix dcterms: <http://purl.org/dc/terms/> .
@prefix ns1: <http://www.iana.org/assignments/> .
@prefix ns2: <osc:> .
@prefix oa: <http://www.w3.org/ns/oa#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix rec: <https://www.opengis.net/def/ogc-api/records/> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

<https://ogc.org/demo/ospd/polaris-workflow> rdfs:label "POLARIS" ;
    dcterms:conformsTo <http://www.opengis.net/spec/ogcapi-records-1/1.0/req/record-core> ;
    dcterms:created "2025-02-19T23:00:00Z" ;
    dcterms:description "Polar Operational Limit Assessment Risk Index System (POLARIS) algorithm." ;
    dcterms:format "Feature",
        "workflow" ;
    dcterms:license "CC-BY-SA-4.0" ;
    dcterms:modified "2025-03-03T22:00:00Z" ;
    rdfs:seeAlso [ rdfs:label "Git source repository" ;
            dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/git> ;
            oa:hasTarget <https://github.com/gtif-cerulean/cerulean-catalog.git> ],
        [ rdfs:label "Open Science Catalog" ;
            dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/root> ;
            oa:hasTarget <https://ogc.org/catalog.json> ],
        [ rdfs:label "Theme: Oceans" ;
            dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/related> ;
            oa:hasTarget <https://ogc.org/themes/oceans/catalog.json> ],
        [ rdfs:label "OGC Application Package" ;
            dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/application> ;
            oa:hasTarget <https://github.com/gtif-cerulean/cerulean-catalog.git> ],
        [ dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/self> ;
            oa:hasTarget <https://esa-earthcode.github.io/open-science-catalog-metadata/workflows/polaris-workflow/record.json> ],
        [ rdfs:label "Workflows" ;
            dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/parent> ;
            oa:hasTarget <https://ogc.org/demo/catalog.json> ],
        [ rdfs:label "Project: POLARIS" ;
            dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/related> ;
            oa:hasTarget <https://ogc.org/projects/polaris/collection.json> ],
        [ rdfs:label "POLARIS" ;
            dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/child> ;
            oa:hasTarget <https://ogc.org/experiments/polaris-experiment/record.json> ] ;
    dcat:contactPoint [ rdfs:seeAlso [ dcterms:type "text/html" ;
                    ns1:relation <http://www.iana.org/assignments/relation/about> ;
                    oa:hasTarget <https://opensciencedata.esa.int/> ] ] ;
    dcat:keyword "polar",
        "sea ice" ;
    rec:format [ rec:name "GeoTIFF" ] ;
    rec:themes [ rec:concept [ rec:conceptID "oceans"^^xsd:string ] ;
            rec:scheme "https://github.com/stac-extensions/osc#theme" ] ;
    ns2:project "polaris" .


```


### Water Bodies Detection
The water-bodies workflow determines possible areas of water within a given region using NDWI and Otsu threshold. These regions are marked on the generated GeoTIFF(s) and can then be viewed using an appropriate application.
The primary workflow, water_bodies, returns a STAC Catalog containing the generated items and each output will have it's own STAC item. Multiple images can be processed at once as the workflow uses scatter functionality for parallel processing, if supported by the executing service.
This workflow is borrowed from the EOEPCA examples
There are two workflows defined in this CWL file, the first, detect_water_body, computes the output TIFF for a single input STAC item, and the second, water_bodies, calls the first workflow for any number of STAC items and also wraps the output in a STAC Catalog, to improve integration with other OGC services.
The primary workflow accept the same parameters:


stac_items - links to the Sentinel-2 COG STAC items containing GeoTIFF data you wish to process

aoi - coordinates defining the area of interest we wish to crop the inputs to

epsg - the coordinate system for the input data, to be used when cropping the input

bands - the band names to use in the NDWI calculations
The sub-workflow swaps stac_items for a single item input.
The expected output from this workflow is a STAC Catalog of GeoTIFF items containing GeoTIFF files highlighting the regions of water in the input images, you will get a single image for each STAC item input.

not accessible at https://osc-staging.earthcode.eox.at/workflows/waterbodies/record
#### json
```json
{
  "id": "waterbodies",
  "type": "Feature",
  "geometry": null,
  "properties": {
    "title": "Waterbodies",
    "created": "2025-10-03T09:20:36Z",
    "osc:project": "ospd",
    "description": "Waterbodies workflow",
    "type": "dataset",
    "resourceLanguages": [],
    "externalIds": [],
    "formats": [],
    "contacts": [
      {
        "name": "Garin Smith",
        "organization": "Telespazio UK LTD"
      }
    ],
    "keywords": [],
    "language": {
      "code": ""
    },
    "languages": []
  },
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
      "title": "Workflows"
    },
    {
      "rel": "self",
      "href": "https://esa-earthcode.github.io/open-science-catalog-metadata/workflows/waterbodies/record.json",
      "type": "application/json"
    },
    {
      "rel": "related",
      "href": "../../projects/ospd/collection.json",
      "type": "application/json",
      "title": "Project: OSPD"
    },
    {
      "href": "https://raw.githubusercontent.com/tjellicoe-tpzuk/eo-workflow-examples/refs/heads/main/water-bodies/water-bodies.cwl",
      "rel": "application",
      "type": "application/clw+yaml",
      "hreflang": "",
      "title": "OGC Application Package"
    }
  ],
  "conformsTo": [
    "http://www.opengis.net/spec/ogcapi-records-1/1.0/req/record-core",
    "https://stac-extensions.github.io/application/v0.1.0/schema.json",
    "https://raw.githubusercontent.com/EOEPCA/metadata-profile/refs/heads/1.0/schemas/application-type-ogc-application-package"
  ],
  "linkTemplates": []
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/workflows/context.jsonld",
  "id": "waterbodies",
  "type": "Feature",
  "geometry": null,
  "properties": {
    "title": "Waterbodies",
    "created": "2025-10-03T09:20:36Z",
    "osc:project": "ospd",
    "description": "Waterbodies workflow",
    "type": "dataset",
    "resourceLanguages": [],
    "externalIds": [],
    "formats": [],
    "contacts": [
      {
        "name": "Garin Smith",
        "organization": "Telespazio UK LTD"
      }
    ],
    "keywords": [],
    "language": {
      "code": ""
    },
    "languages": []
  },
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
      "title": "Workflows"
    },
    {
      "rel": "self",
      "href": "https://esa-earthcode.github.io/open-science-catalog-metadata/workflows/waterbodies/record.json",
      "type": "application/json"
    },
    {
      "rel": "related",
      "href": "../../projects/ospd/collection.json",
      "type": "application/json",
      "title": "Project: OSPD"
    },
    {
      "href": "https://raw.githubusercontent.com/tjellicoe-tpzuk/eo-workflow-examples/refs/heads/main/water-bodies/water-bodies.cwl",
      "rel": "application",
      "type": "application/clw+yaml",
      "hreflang": "",
      "title": "OGC Application Package"
    }
  ],
  "conformsTo": [
    "http://www.opengis.net/spec/ogcapi-records-1/1.0/req/record-core",
    "https://stac-extensions.github.io/application/v0.1.0/schema.json",
    "https://raw.githubusercontent.com/EOEPCA/metadata-profile/refs/heads/1.0/schemas/application-type-ogc-application-package"
  ],
  "linkTemplates": []
}
```

#### ttl
```ttl
@prefix dcat: <http://www.w3.org/ns/dcat#> .
@prefix dcterms: <http://purl.org/dc/terms/> .
@prefix ns1: <osc:> .
@prefix ns2: <http://www.iana.org/assignments/> .
@prefix oa: <http://www.w3.org/ns/oa#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix rec: <https://www.opengis.net/def/ogc-api/records/> .

<https://ogc.org/demo/ospd/waterbodies> rdfs:label "Waterbodies" ;
    dcterms:conformsTo <http://www.opengis.net/spec/ogcapi-records-1/1.0/req/record-core>,
        <https://raw.githubusercontent.com/EOEPCA/metadata-profile/refs/heads/1.0/schemas/application-type-ogc-application-package>,
        <https://stac-extensions.github.io/application/v0.1.0/schema.json> ;
    dcterms:created "2025-10-03T09:20:36Z" ;
    dcterms:description "Waterbodies workflow" ;
    dcterms:format "Feature",
        "dataset" ;
    rdfs:seeAlso [ rdfs:label "OGC Application Package" ;
            dcterms:language "" ;
            dcterms:type "application/clw+yaml" ;
            ns2:relation <http://www.iana.org/assignments/relation/application> ;
            oa:hasTarget <https://raw.githubusercontent.com/tjellicoe-tpzuk/eo-workflow-examples/refs/heads/main/water-bodies/water-bodies.cwl> ],
        [ rdfs:label "Open Science Catalog" ;
            dcterms:type "application/json" ;
            ns2:relation <http://www.iana.org/assignments/relation/root> ;
            oa:hasTarget <https://ogc.org/catalog.json> ],
        [ dcterms:type "application/json" ;
            ns2:relation <http://www.iana.org/assignments/relation/self> ;
            oa:hasTarget <https://esa-earthcode.github.io/open-science-catalog-metadata/workflows/waterbodies/record.json> ],
        [ rdfs:label "Project: OSPD" ;
            dcterms:type "application/json" ;
            ns2:relation <http://www.iana.org/assignments/relation/related> ;
            oa:hasTarget <https://ogc.org/projects/ospd/collection.json> ],
        [ rdfs:label "Workflows" ;
            dcterms:type "application/json" ;
            ns2:relation <http://www.iana.org/assignments/relation/parent> ;
            oa:hasTarget <https://ogc.org/demo/catalog.json> ] ;
    dcat:contactPoint [ ] ;
    rec:language [ rec:languageCode "" ] ;
    ns1:project "ospd" .


```


### Mangrove Detect
The mangrove biomass workflow demonstrates an initial approach to estimating above-ground biomass and carbon stocks using Sentinel-2 optical satellite imagery. This serves as a baseline workflow that can be augmented with complementary data sources depending on project needs. The current implementation queries the AWS STAC catalog for cloud-free scenes, calculates vegetation indices (NDVI, NDWI, SAVI), applies threshold-based classification to detect mangrove extent, and estimates biomass using a validated allometric equation from Myanmar field studies. Results include spatially explicit biomass maps, carbon stock totals, and CO2 equivalence calculations following IPCC Tier 2 methodology.
calculation.
## Schema

```yaml
$schema: https://json-schema.org/draft/2020-12/schema
description: Schema for OGCAPI records profile for GeoDCAT - defines all extra elements
  defined by GeoDCAT so that the JSON-LD context can map to GeoDCAT RDF
allOf:
- anyOf:
  - $ref: https://ogcincubator.github.io/geodcat-ogcapi-records/build/annotated/geo/geodcat/geodcat-records/schema.yaml

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/workflows/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/workflows/schema.yaml)


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
    "type": "dct:format",
    "id": "@id",
    "properties": "@nest",
    "geometry": {
      "@context": {
        "type": "@type"
      },
      "@id": "geojson:geometry"
    },
    "bbox": {
      "@container": "@list",
      "@id": "geojson:bbox"
    },
    "links": {
      "@context": {
        "type": "dct:type"
      },
      "@id": "rdfs:seeAlso"
    },
    "coordinates": {
      "@container": "@list",
      "@id": "geojson:coordinates"
    },
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
    "hreflang": "dct:language",
    "title": "rdfs:label",
    "length": "dct:extent",
    "created": "dct:created",
    "updated": "dct:modified",
    "uriTemplate": {
      "@type": "xsd:string",
      "@id": "oa:hasTarget"
    },
    "time": {
      "@id": "dct:temporal",
      "@context": {
        "interval": {
          "@id": "w3ctime:hasTime",
          "@container": "@list"
        },
        "resolution": "rec:iso8601period"
      }
    },
    "description": {
      "@container": "@set",
      "@id": "dct:description"
    },
    "keywords": {
      "@container": "@set",
      "@id": "dcat:keyword"
    },
    "conformsTo": {
      "@container": "@set",
      "@id": "dct:conformsTo",
      "@type": "@id"
    },
    "language": {
      "@id": "rec:language",
      "@context": {
        "code": "rec:languageCode",
        "name": "skos:prefLabel"
      }
    },
    "languages": {
      "@container": "@set",
      "@id": "rec:languages",
      "@context": {
        "code": "rec:languageCode",
        "name": "skos:prefLabel"
      }
    },
    "resourceLanguages": {
      "@container": "@set",
      "@id": "rec:resourceLanguages",
      "@context": {
        "code": "rec:languageCode",
        "name": "skos:prefLabel"
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
          "@id": "rec:concept",
          "@context": {
            "id": {
              "@type": "xsd:string",
              "@id": "rec:conceptID"
            },
            "url": {
              "@type": "@id",
              "@id": "dcat:theme"
            }
          }
        },
        "scheme": "rec:scheme"
      }
    },
    "formats": {
      "@id": "rec:format",
      "@context": {
        "name": "rec:name"
      }
    },
    "contacts": {
      "@container": "@set",
      "@id": "dcat:contactPoint",
      "@type": "@id"
    },
    "license": "dct:license",
    "accessrights": "dct:accessRights",
    "linkTemplates": "rec:hasLinkTemplate",
    "variables": {
      "@container": "@id",
      "@id": "rec:hasVariable",
      "@context": {
        "@base": "http://example.com/variables/",
        "@vocab": "https://www.opengis.net/def/ogc-api/records/"
      }
    },
    "geojson": "https://purl.org/geojson/vocab#",
    "rdfs": "http://www.w3.org/2000/01/rdf-schema#",
    "oa": "http://www.w3.org/ns/oa#",
    "dct": "http://purl.org/dc/terms/",
    "xsd": "http://www.w3.org/2001/XMLSchema#",
    "w3ctime": "http://www.w3.org/2006/time#",
    "rec": "https://www.opengis.net/def/ogc-api/records/",
    "dcat": "http://www.w3.org/ns/dcat#",
    "skos": "http://www.w3.org/2004/02/skos/core#",
    "owl": "http://www.w3.org/2002/07/owl#",
    "rdf": "http://www.w3.org/1999/02/22-rdf-syntax-ns#",
    "dctype": "http://purl.org/dc/dcmitype/",
    "vcard": "http://www.w3.org/2006/vcard/ns#",
    "prov": "http://www.w3.org/ns/prov#",
    "foaf": "http://xmlns.com/foaf/0.1/",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/workflows/context.jsonld)

## Sources

* [GeoDCAT Specification](http://www.opengis.net/def/metamodel/profiles/geodcat)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-openscience](https://github.com/ogcincubator/bblocks-openscience)
* Path: `_sources/geodcat-stac-earthcode/workflows`

