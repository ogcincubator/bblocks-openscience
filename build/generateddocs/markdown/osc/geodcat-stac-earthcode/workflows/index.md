
# EarthCODE Workflow (Schema)

`ogc.osc.geodcat-stac-earthcode.workflows` *v0.1*

EarthCODE metadata profile linked to semantic models

[*Status*](http://www.opengis.net/def/status): Under development

## Description

## ESA EarthCODE workflow 


Some constraints are not checked:

* All child links mst be to experiments.
* osc:project must be the ID of a Project in the EarthCODE Projects Catalog.
* 'related' links must be STAC or HTML. It's intended these point to the Workflow's Theme (a Catalog) and the Workflow's Project (a Collection).

## Examples

### Polar Warp
The polarwarp algorithm geolocates, aligns, and warps satellite SAR images using forecast drift and wind/tide fields in polar regions. It takes ice drift vectors from multiple data sources (SAR, TOPAZ4, ICON, tide models), translates them into pixel displacements, and applies thin-plate spline warping to generate temporally aligned and drift-corrected imagery. This enables monitoring of sea ice motion over forecast windows while preserving georeferencing.

#### json
```json
{
  "id": "polarwarp",
  "type": "Feature",
  "conformsTo": [
    "http://www.opengis.net/spec/ogcapi-records-1/1.0/req/record-core",
    "https://stac-extensions.github.io/application/v0.1.0/schema.json",
    "https://raw.githubusercontent.com/EOEPCA/metadata-profile/refs/heads/1.0/schemas/application-type-argo-workflow"
  ],
  "geometry": null,
  "properties": {
    "created": "2025-09-30T13:00:00Z",
    "updated": "2025-09-30T14:00:00Z",
    "type": "workflow",
    "title": "Polarwarp",
    "description": "The polarwarp algorithm geolocates, aligns, and warps satellite SAR images using forecast drift and wind/tide fields in polar regions.",
    "application:type": "argo-workflow",
    "application:container": true,
    "application:language": "Python",
    "keywords": [
      "sea ice",
      "polar"
    ],
    "contacts": [
      {
        "name": "David Arthurs",
        "roles": [
          "consortium_member"
        ],
        "emails": [
          {
            "value": "david.arthurs@polarview.org"
          }
        ]
      },
      {
        "name": "Týna Doležalová",
        "roles": [
          "consortium_member"
        ],
        "emails": [
          {
            "value": "tyna.dolezalova@eox.at"
          }
        ]
      }
    ],
    "themes": [
      {
        "scheme": "https://github.com/stac-extensions/osc#theme",
        "concepts": [
          {
            "id": "cryosphere"
          }
        ]
      },
      {
        "scheme": "https://github.com/stac-extensions/osc#theme",
        "concepts": [
          {
            "id": "oceans"
          }
        ]
      }
    ],
    "license": "CC-BY-SA-4.0",
    "osc:project": "cerulean-information-factory"
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
      "href": "https://esa-earthcode.github.io/open-science-catalog-metadata/workflows/polarwarp/record.json",
      "type": "application/json"
    },
    {
      "rel": "related",
      "href": "../../projects/cerulean-information-factory/collection.json",
      "type": "application/json",
      "title": "Project: Cerulean Information Factory"
    },
    {
      "rel": "related",
      "href": "../../themes/cryosphere/catalog.json",
      "type": "application/json",
      "title": "Theme: Cryosphere"
    },
    {
      "rel": "related",
      "href": "../../themes/oceans/catalog.json",
      "type": "application/json",
      "title": "Theme: Oceans"
    },
    {
      "rel": "child",
      "href": "../../experiments/polarwarp/record.json",
      "type": "application/json",
      "title": "Polarwarp"
    },
    {
      "rel": "vcs",
      "title": "Git source repository",
      "href": "https://github.com/gtif-cerulean/polarwarp.git",
      "vcs:type": "git",
      "vcs:branch": "main"
    },
    {
      "rel": "application",
      "title": "Polarwarp workflow",
      "href": "https://github.com/gtif-cerulean/polarwarp/blob/main/workflow.yml",
      "type": "application/x-argo-workflow-yaml",
      "application:type": "argo-workflow",
      "application:container": true,
      "application:language": "Python",
      "argo-workflow:": {
        "requirements": [
          {
            "temp_storage": "10GB"
        }
        ]
      }
    },
    {
      "rel": "application-originating-platform",
      "title": "EOxHub Workspaces",
      "href": "https://workspace.cif.hub-otc.eox.at/",
      "type": "text/html",
      "application:platform_supports": ["argo-workflow"],
      "application:preferred_app": "argo"
    },
    {
      "rel": "related",
      "href": "https://harshness-map.gtif.eox.at/processes/execute-polarwarp-gcps",
      "type": "text/html",
      "title": "Trigger workflow via API provided by pygeoapi"
    }

  ]
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/workflows/context.jsonld",
  "id": "polarwarp",
  "type": "Feature",
  "conformsTo": [
    "http://www.opengis.net/spec/ogcapi-records-1/1.0/req/record-core",
    "https://stac-extensions.github.io/application/v0.1.0/schema.json",
    "https://raw.githubusercontent.com/EOEPCA/metadata-profile/refs/heads/1.0/schemas/application-type-argo-workflow"
  ],
  "geometry": null,
  "properties": {
    "created": "2025-09-30T13:00:00Z",
    "updated": "2025-09-30T14:00:00Z",
    "type": "workflow",
    "title": "Polarwarp",
    "description": "The polarwarp algorithm geolocates, aligns, and warps satellite SAR images using forecast drift and wind/tide fields in polar regions.",
    "application:type": "argo-workflow",
    "application:container": true,
    "application:language": "Python",
    "keywords": [
      "sea ice",
      "polar"
    ],
    "contacts": [
      {
        "name": "David Arthurs",
        "roles": [
          "consortium_member"
        ],
        "emails": [
          {
            "value": "david.arthurs@polarview.org"
          }
        ]
      },
      {
        "name": "T\u00fdna Dole\u017ealov\u00e1",
        "roles": [
          "consortium_member"
        ],
        "emails": [
          {
            "value": "tyna.dolezalova@eox.at"
          }
        ]
      }
    ],
    "themes": [
      {
        "scheme": "https://github.com/stac-extensions/osc#theme",
        "concepts": [
          {
            "id": "cryosphere"
          }
        ]
      },
      {
        "scheme": "https://github.com/stac-extensions/osc#theme",
        "concepts": [
          {
            "id": "oceans"
          }
        ]
      }
    ],
    "license": "CC-BY-SA-4.0",
    "osc:project": "cerulean-information-factory"
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
      "href": "https://esa-earthcode.github.io/open-science-catalog-metadata/workflows/polarwarp/record.json",
      "type": "application/json"
    },
    {
      "rel": "related",
      "href": "../../projects/cerulean-information-factory/collection.json",
      "type": "application/json",
      "title": "Project: Cerulean Information Factory"
    },
    {
      "rel": "related",
      "href": "../../themes/cryosphere/catalog.json",
      "type": "application/json",
      "title": "Theme: Cryosphere"
    },
    {
      "rel": "related",
      "href": "../../themes/oceans/catalog.json",
      "type": "application/json",
      "title": "Theme: Oceans"
    },
    {
      "rel": "child",
      "href": "../../experiments/polarwarp/record.json",
      "type": "application/json",
      "title": "Polarwarp"
    },
    {
      "rel": "vcs",
      "title": "Git source repository",
      "href": "https://github.com/gtif-cerulean/polarwarp.git",
      "vcs:type": "git",
      "vcs:branch": "main"
    },
    {
      "rel": "application",
      "title": "Polarwarp workflow",
      "href": "https://github.com/gtif-cerulean/polarwarp/blob/main/workflow.yml",
      "type": "application/x-argo-workflow-yaml",
      "application:type": "argo-workflow",
      "application:container": true,
      "application:language": "Python",
      "argo-workflow:": {
        "requirements": [
          {
            "temp_storage": "10GB"
          }
        ]
      }
    },
    {
      "rel": "application-originating-platform",
      "title": "EOxHub Workspaces",
      "href": "https://workspace.cif.hub-otc.eox.at/",
      "type": "text/html",
      "application:platform_supports": [
        "argo-workflow"
      ],
      "application:preferred_app": "argo"
    },
    {
      "rel": "related",
      "href": "https://harshness-map.gtif.eox.at/processes/execute-polarwarp-gcps",
      "type": "text/html",
      "title": "Trigger workflow via API provided by pygeoapi"
    }
  ]
}
```

#### ttl
```ttl
@prefix dcterms: <http://purl.org/dc/terms/> .
@prefix geojson: <https://purl.org/geojson/vocab#> .
@prefix ns1: <http://www.iana.org/assignments/> .
@prefix ns2: <application:> .
@prefix ns3: <vcs:> .
@prefix oa: <http://www.w3.org/ns/oa#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

<https://ogc.org/demo/ospd/polarwarp> a geojson:Feature ;
    dcterms:conformsTo <http://www.opengis.net/spec/ogcapi-records-1/1.0/req/record-core>,
        <https://raw.githubusercontent.com/EOEPCA/metadata-profile/refs/heads/1.0/schemas/application-type-argo-workflow>,
        <https://stac-extensions.github.io/application/v0.1.0/schema.json> ;
    rdfs:seeAlso [ rdfs:label "EOxHub Workspaces" ;
            ns2:platform_supports "argo-workflow" ;
            ns2:preferred_app "argo" ;
            dcterms:type "text/html" ;
            ns1:relation <http://www.iana.org/assignments/relation/application-originating-platform> ;
            oa:hasTarget <https://workspace.cif.hub-otc.eox.at/> ],
        [ rdfs:label "Trigger workflow via API provided by pygeoapi" ;
            dcterms:type "text/html" ;
            ns1:relation <http://www.iana.org/assignments/relation/related> ;
            oa:hasTarget <https://harshness-map.gtif.eox.at/processes/execute-polarwarp-gcps> ],
        [ rdfs:label "Open Science Catalog" ;
            dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/root> ;
            oa:hasTarget <https://ogc.org/catalog.json> ],
        [ rdfs:label "Project: Cerulean Information Factory" ;
            dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/related> ;
            oa:hasTarget <https://ogc.org/projects/cerulean-information-factory/collection.json> ],
        [ rdfs:label "Theme: Cryosphere" ;
            dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/related> ;
            oa:hasTarget <https://ogc.org/themes/cryosphere/catalog.json> ],
        [ rdfs:label "Theme: Oceans" ;
            dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/related> ;
            oa:hasTarget <https://ogc.org/themes/oceans/catalog.json> ],
        [ rdfs:label "Polarwarp workflow" ;
            ns2:container true ;
            ns2:language "Python" ;
            ns2:type "argo-workflow" ;
            <argo-workflow:> [ ] ;
            dcterms:type "application/x-argo-workflow-yaml" ;
            ns1:relation <http://www.iana.org/assignments/relation/application> ;
            oa:hasTarget <https://github.com/gtif-cerulean/polarwarp/blob/main/workflow.yml> ],
        [ rdfs:label "Polarwarp" ;
            dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/child> ;
            oa:hasTarget <https://ogc.org/experiments/polarwarp/record.json> ],
        [ dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/self> ;
            oa:hasTarget <https://esa-earthcode.github.io/open-science-catalog-metadata/workflows/polarwarp/record.json> ],
        [ rdfs:label "Git source repository" ;
            ns1:relation <http://www.iana.org/assignments/relation/vcs> ;
            oa:hasTarget <https://github.com/gtif-cerulean/polarwarp.git> ;
            ns3:branch "main" ;
            ns3:type "git" ],
        [ rdfs:label "Workflows" ;
            dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/parent> ;
            oa:hasTarget <https://ogc.org/demo/catalog.json> ] .


```


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
@prefix dcterms: <http://purl.org/dc/terms/> .
@prefix geojson: <https://purl.org/geojson/vocab#> .
@prefix ns1: <http://www.iana.org/assignments/> .
@prefix oa: <http://www.w3.org/ns/oa#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .

<https://ogc.org/demo/ospd/polaris-workflow> a geojson:Feature ;
    dcterms:conformsTo <http://www.opengis.net/spec/ogcapi-records-1/1.0/req/record-core> ;
    rdfs:seeAlso [ rdfs:label "OGC Application Package" ;
            dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/application> ;
            oa:hasTarget <https://github.com/gtif-cerulean/cerulean-catalog.git> ],
        [ rdfs:label "Theme: Oceans" ;
            dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/related> ;
            oa:hasTarget <https://ogc.org/themes/oceans/catalog.json> ],
        [ rdfs:label "POLARIS" ;
            dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/child> ;
            oa:hasTarget <https://ogc.org/experiments/polaris-experiment/record.json> ],
        [ rdfs:label "Project: POLARIS" ;
            dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/related> ;
            oa:hasTarget <https://ogc.org/projects/polaris/collection.json> ],
        [ rdfs:label "Git source repository" ;
            dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/git> ;
            oa:hasTarget <https://github.com/gtif-cerulean/cerulean-catalog.git> ],
        [ rdfs:label "Workflows" ;
            dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/parent> ;
            oa:hasTarget <https://ogc.org/demo/catalog.json> ],
        [ dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/self> ;
            oa:hasTarget <https://esa-earthcode.github.io/open-science-catalog-metadata/workflows/polaris-workflow/record.json> ],
        [ rdfs:label "Open Science Catalog" ;
            dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/root> ;
            oa:hasTarget <https://ogc.org/catalog.json> ] .


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
@prefix dcterms: <http://purl.org/dc/terms/> .
@prefix geojson: <https://purl.org/geojson/vocab#> .
@prefix ns1: <http://www.iana.org/assignments/> .
@prefix oa: <http://www.w3.org/ns/oa#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .

<https://ogc.org/demo/ospd/waterbodies> a geojson:Feature ;
    dcterms:conformsTo <http://www.opengis.net/spec/ogcapi-records-1/1.0/req/record-core>,
        <https://raw.githubusercontent.com/EOEPCA/metadata-profile/refs/heads/1.0/schemas/application-type-ogc-application-package>,
        <https://stac-extensions.github.io/application/v0.1.0/schema.json> ;
    rdfs:seeAlso [ dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/self> ;
            oa:hasTarget <https://esa-earthcode.github.io/open-science-catalog-metadata/workflows/waterbodies/record.json> ],
        [ rdfs:label "Project: OSPD" ;
            dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/related> ;
            oa:hasTarget <https://ogc.org/projects/ospd/collection.json> ],
        [ rdfs:label "Open Science Catalog" ;
            dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/root> ;
            oa:hasTarget <https://ogc.org/catalog.json> ],
        [ rdfs:label "Workflows" ;
            dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/parent> ;
            oa:hasTarget <https://ogc.org/demo/catalog.json> ],
        [ rdfs:label "OGC Application Package" ;
            dcterms:language "" ;
            dcterms:type "application/clw+yaml" ;
            ns1:relation <http://www.iana.org/assignments/relation/application> ;
            oa:hasTarget <https://raw.githubusercontent.com/tjellicoe-tpzuk/eo-workflow-examples/refs/heads/main/water-bodies/water-bodies.cwl> ] .


```


### Water Bodies Detection With Provenance
The Water Bodies Detection workflow record with mocked-up provenance data added to it.

Some notes:
  - There is an `properties.id` field because the prov-entity schema requires it, but it duplicates the
    root `id`.
  - The link to the CWL is there twice but it's not clear to me which type of link is better.
  - wf4ever and PROV say little about how inputs are described. This is based on OGC API Processes.
  - There's potential ambiguity over whether it's describing what arrived at the Processes API,
    what arrived at the workflow engine or a mix. eg, processing mode may not reach the engine and
    links may have been dereferenced. Or perhaps this is unimportant. However, both a link to CWL and
    a link to a Processes API process could be given in one record.
#### json
```json
{
  "id": "waterbodies",
  "type": "Feature",
  "conformsTo": [
    "http://www.opengis.net/spec/ogcapi-records-1/1.0/req/record-core",
    "https://stac-extensions.github.io/application/v0.1.0/schema.json",
    "https://raw.githubusercontent.com/EOEPCA/metadata-profile/refs/heads/1.0/schemas/application-type-ogc-application-package"
  ],
  "geometry": null,

  "properties": {
    "id": "required-by-prov-Entity-schema",
    "provType": ["prov:Entity", "prov:Plan", "wfdesc:Workflow"],

    "wfdesc:hasInput": {
      "aoi": {
        "title": "area of interest",
        "description": "area of interest as a bounding box",
        "schema": {
          "type": "string",
          "default": "-121.399,39.834,-120.74,40.472",
          "pattern": "^-?\\d+(\\.\\d+)?,-?\\d+(\\.\\d+)?, -?\\d+(\\.\\d+)?,-?\\d+(\\.\\d+)?$"
        }
      },
      "epsg": {
        "title": "EPSG code",
        "description": "EPSG code",
        "schema": {
          "type": "string",
          "default": "EPSG:4326"
        }
      },
      "stac_items": {
        "title": "Sentinel-2 STAC items",
        "description": "list of Sentinel-2 COG STAC items",
        "schema": {
          "type": "array",
          "items": {
            "type": "string",
            "format": "uri"
          },
          "minItems": 1
        },
        "default": [
          "https://earth-search.aws.element84.com/v0/collections/sentinel-s2-l2a-cogs/items/S2B_10TFK_20210713_0_L2A",
          "https://earth-search.aws.element84.com/v0/collections/sentinel-s2-l2a-cogs/items/S2A_10TFK_20220524_0_L2A"
        ]
      },
      "bands": {
        "title": "bands used for the NDWI",
        "description": "bands used for the NDWI",
        "schema": {
          "type": "array",
          "items": {
            "type": "string"
          },
          "minItems": 2,
          "maxItems": 2,
          "default": ["green", "nir"]
        }
      }
    },
    "wfdesc:hasOutput": {
      "stac_catalog": {
        "title": "STAC Catalog",
        "description": "STAC Catalog containing the water bodies results",
        "provType": ["prov:Collection", "prov:Entity"],
        "schema": {
          "type": "string",
          "format": "uri"
        }
      }
    },

    "title": "Waterbodies",
    "created": "2025-10-03T09:20:36Z",
    "osc:project": "ospd",
    "description": "Waterbodies workflow",
    "type": "workflow",
    "resourceLanguages": [],
    "externalIds": [],
    "formats": [],
    "contacts": [
      {
        "name": "Tom Jellicoe",
        "positionName": "Software Developer",
        "organization": "Telespazio UK",
        "emails": [
            {
                "value": "thomas.jellicoe@telespazio.com"
            }
        ]
      }
    ],
    "keywords": [
      "water",
      "NDWI",
      "water bodies",
      "otsu",
      "eoepca"
    ],
    "language": {
      "code": ""
    },
    "languages": []
  },


  "links": [
    {
      "rel": "root",
      "href": "https://example.com/open-science-catalog-metadata/catalog.json",
      "type": "application/json",
      "title": "Open Science Catalog"
    },
    {
      "rel": "parent",
      "href": "https://example.com/open-science-catalog-metadata/workflows/catalog.json",
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
      "href": "https://example.com/open-science-catalog-metadata/projects/ospd/collection.json",
      "type": "application/json",
      "title": "Project: OSPD"
    },
    {
      "href": "https://raw.githubusercontent.com/tjellicoe-tpzuk/eo-workflow-examples/refs/heads/main/water-bodies/water-bodies.cwl",
      "rel": "wfdesc:WorkflowDefinition",
      "type": "application/cwl+yaml",
      "title": "OGC Application Package"
    },
    {
      "href": "https://raw.githubusercontent.com/tjellicoe-tpzuk/eo-workflow-examples/refs/heads/main/water-bodies/water-bodies.cwl",
      "rel": "application",
      "type": "application/cwl+yaml",
      "hreflang": "",
      "title": "OGC Application Package"
    },
    {
      "href": "https://github.com/Terradue/ogc-eo-application-package-hands-on/tree/master/water-bodies",
      "rel": "git",
      "title": "Source Code"
    }
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
  "conformsTo": [
    "http://www.opengis.net/spec/ogcapi-records-1/1.0/req/record-core",
    "https://stac-extensions.github.io/application/v0.1.0/schema.json",
    "https://raw.githubusercontent.com/EOEPCA/metadata-profile/refs/heads/1.0/schemas/application-type-ogc-application-package"
  ],
  "geometry": null,
  "properties": {
    "id": "required-by-prov-Entity-schema",
    "provType": [
      "prov:Entity",
      "prov:Plan",
      "wfdesc:Workflow"
    ],
    "wfdesc:hasInput": {
      "aoi": {
        "title": "area of interest",
        "description": "area of interest as a bounding box",
        "schema": {
          "type": "string",
          "default": "-121.399,39.834,-120.74,40.472",
          "pattern": "^-?\\d+(\\.\\d+)?,-?\\d+(\\.\\d+)?, -?\\d+(\\.\\d+)?,-?\\d+(\\.\\d+)?$"
        }
      },
      "epsg": {
        "title": "EPSG code",
        "description": "EPSG code",
        "schema": {
          "type": "string",
          "default": "EPSG:4326"
        }
      },
      "stac_items": {
        "title": "Sentinel-2 STAC items",
        "description": "list of Sentinel-2 COG STAC items",
        "schema": {
          "type": "array",
          "items": {
            "type": "string",
            "format": "uri"
          },
          "minItems": 1
        },
        "default": [
          "https://earth-search.aws.element84.com/v0/collections/sentinel-s2-l2a-cogs/items/S2B_10TFK_20210713_0_L2A",
          "https://earth-search.aws.element84.com/v0/collections/sentinel-s2-l2a-cogs/items/S2A_10TFK_20220524_0_L2A"
        ]
      },
      "bands": {
        "title": "bands used for the NDWI",
        "description": "bands used for the NDWI",
        "schema": {
          "type": "array",
          "items": {
            "type": "string"
          },
          "minItems": 2,
          "maxItems": 2,
          "default": [
            "green",
            "nir"
          ]
        }
      }
    },
    "wfdesc:hasOutput": {
      "stac_catalog": {
        "title": "STAC Catalog",
        "description": "STAC Catalog containing the water bodies results",
        "provType": [
          "prov:Collection",
          "prov:Entity"
        ],
        "schema": {
          "type": "string",
          "format": "uri"
        }
      }
    },
    "title": "Waterbodies",
    "created": "2025-10-03T09:20:36Z",
    "osc:project": "ospd",
    "description": "Waterbodies workflow",
    "type": "workflow",
    "resourceLanguages": [],
    "externalIds": [],
    "formats": [],
    "contacts": [
      {
        "name": "Tom Jellicoe",
        "positionName": "Software Developer",
        "organization": "Telespazio UK",
        "emails": [
          {
            "value": "thomas.jellicoe@telespazio.com"
          }
        ]
      }
    ],
    "keywords": [
      "water",
      "NDWI",
      "water bodies",
      "otsu",
      "eoepca"
    ],
    "language": {
      "code": ""
    },
    "languages": []
  },
  "links": [
    {
      "rel": "root",
      "href": "https://example.com/open-science-catalog-metadata/catalog.json",
      "type": "application/json",
      "title": "Open Science Catalog"
    },
    {
      "rel": "parent",
      "href": "https://example.com/open-science-catalog-metadata/workflows/catalog.json",
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
      "href": "https://example.com/open-science-catalog-metadata/projects/ospd/collection.json",
      "type": "application/json",
      "title": "Project: OSPD"
    },
    {
      "href": "https://raw.githubusercontent.com/tjellicoe-tpzuk/eo-workflow-examples/refs/heads/main/water-bodies/water-bodies.cwl",
      "rel": "wfdesc:WorkflowDefinition",
      "type": "application/cwl+yaml",
      "title": "OGC Application Package"
    },
    {
      "href": "https://raw.githubusercontent.com/tjellicoe-tpzuk/eo-workflow-examples/refs/heads/main/water-bodies/water-bodies.cwl",
      "rel": "application",
      "type": "application/cwl+yaml",
      "hreflang": "",
      "title": "OGC Application Package"
    },
    {
      "href": "https://github.com/Terradue/ogc-eo-application-package-hands-on/tree/master/water-bodies",
      "rel": "git",
      "title": "Source Code"
    }
  ],
  "linkTemplates": []
}
```

#### ttl
```ttl
@prefix dcterms: <http://purl.org/dc/terms/> .
@prefix geojson: <https://purl.org/geojson/vocab#> .
@prefix ns1: <http://www.iana.org/assignments/> .
@prefix oa: <http://www.w3.org/ns/oa#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .

<https://ogc.org/demo/ospd/waterbodies> a geojson:Feature ;
    dcterms:conformsTo <http://www.opengis.net/spec/ogcapi-records-1/1.0/req/record-core>,
        <https://raw.githubusercontent.com/EOEPCA/metadata-profile/refs/heads/1.0/schemas/application-type-ogc-application-package>,
        <https://stac-extensions.github.io/application/v0.1.0/schema.json> ;
    rdfs:seeAlso [ rdfs:label "OGC Application Package" ;
            dcterms:type "application/cwl+yaml" ;
            ns1:relation <wfdesc:WorkflowDefinition> ;
            oa:hasTarget <https://raw.githubusercontent.com/tjellicoe-tpzuk/eo-workflow-examples/refs/heads/main/water-bodies/water-bodies.cwl> ],
        [ rdfs:label "Workflows" ;
            dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/parent> ;
            oa:hasTarget <https://example.com/open-science-catalog-metadata/workflows/catalog.json> ],
        [ rdfs:label "Project: OSPD" ;
            dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/related> ;
            oa:hasTarget <https://example.com/open-science-catalog-metadata/projects/ospd/collection.json> ],
        [ rdfs:label "Source Code" ;
            ns1:relation <http://www.iana.org/assignments/relation/git> ;
            oa:hasTarget <https://github.com/Terradue/ogc-eo-application-package-hands-on/tree/master/water-bodies> ],
        [ rdfs:label "Open Science Catalog" ;
            dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/root> ;
            oa:hasTarget <https://example.com/open-science-catalog-metadata/catalog.json> ],
        [ dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/self> ;
            oa:hasTarget <https://esa-earthcode.github.io/open-science-catalog-metadata/workflows/waterbodies/record.json> ],
        [ rdfs:label "OGC Application Package" ;
            dcterms:language "" ;
            dcterms:type "application/cwl+yaml" ;
            ns1:relation <http://www.iana.org/assignments/relation/application> ;
            oa:hasTarget <https://raw.githubusercontent.com/tjellicoe-tpzuk/eo-workflow-examples/refs/heads/main/water-bodies/water-bodies.cwl> ] .


```


### Mangrove Detect
The mangrove biomass workflow demonstrates an initial approach to estimating above-ground biomass and carbon stocks using Sentinel-2 optical satellite imagery. This serves as a baseline workflow that can be augmented with complementary data sources depending on project needs. The current implementation queries the AWS STAC catalog for cloud-free scenes, calculates vegetation indices (NDVI, NDWI, SAVI), applies threshold-based classification to detect mangrove extent, and estimates biomass using a validated allometric equation from Myanmar field studies. Results include spatially explicit biomass maps, carbon stock totals, and CO2 equivalence calculations following IPCC Tier 2 methodology.
calculation.
#### json
```json
 {"id": "kindgrove-mangrove-biomass-workflow",
 "type": "Feature",
 "geometry": null,
 "conformsTo": ["http://www.opengis.net/spec/ogcapi-records-1/1.0/req/record-core"],
 "properties": {"title": "KindGrove: Mangrove Biomass Estimation",
  "description": "An interactive Jupyter notebook workflow for estimating mangrove forest biomass and carbon stocks using Sentinel-2 satellite imagery from AWS Open Data Registry. This demonstrates an initial baseline approach that can be augmented with complementary data sources (LiDAR, InSAR, thermal) or integrated with coastal vulnerability assessments depending on project needs.\n\n### Open Data Architecture\n- Sentinel-2 L2A imagery via AWS STAC catalog (no authentication)\n- Cloud-optimized GeoTIFF processing\n- STAC-compliant data discovery\n\n### Validated Scientific Methods\n- Biomass model R² = 0.72 (validated against 600+ field plots)\n- Detection accuracy: 85-90% (conservative threshold approach)\n- Uncertainty: ±30% (meets IPCC Tier 2 requirements)\n\n### Workflow Stages\n1. Study Area Definition - Interactive location selector\n2. STAC Data Discovery - Query AWS catalog for cloud-free scenes\n3. Vegetation Index Calculation - NDVI, NDWI, SAVI from spectral bands\n4. Mangrove Detection - Threshold-based classification\n5. Biomass Estimation - Allometric model (Biomass = 250.5 × NDVI - 75.2)\n6. Carbon Accounting - IPCC-compliant calculations",
  "osc:type": "workflow",
  "osc:project": "ospd",
  "osc:status": "development",
  "application:type": "cwl-workflow",
  "application:container": "True",
  "application:language": "Python",
  "updated": "2024-07-30T12:00:00Z",
  "created": "2024-07-30T12:00:00Z",
  "keywords": ["mangrove", "biomass", "carbon", "sentinel-2", "stac"],
  "license": "MIT",
  "version": "1",
  "themes": [{"scheme": "https://github.com/stac-extensions/osc#theme",
    "concepts": [{"id": "land"}]}],
  "contacts": [{"name": "Cameron Sajedi",
    "roles": ["developer"],
    "emails": []}],
  "extent": null},
 "linkTemplates": [],
 "links": [{"rel": "root",
   "href": "../../catalog.json",
   "type": "application/json",
   "title": "Open Science Catalog"},
  {"rel": "parent",
   "href": "../catalog.json",
   "type": "application/json",
   "title": "Workflows"},
  {"rel": "self",
   "href": "../kindgrove-mangrove-biomass-workflow/record.json",
   "type": "application/json"},
  {"rel": "related",
    "href": "../../projects/ospd/collection.json",
    "type": "application/json",
    "title": "Project: OSPD"},
  {"rel": "related",
   "href": "../../themes/land/catalog.json",
   "type": "application/json",
   "title": "Theme: Land"},
  {"rel": "vcs",
   "title": "Git source repository",
   "href": "https://github.com/starling-foundries/KindGrove",
   "vcs:type": "git",
   "vcs:branch": "main"},
  {"rel": "application",
   "title": "KindGrove Mangrove Biomass Workflow",
   "href": "https://github.com/starling-foundries/KindGrove/blob/main/mangrove_workflow.cwl",
   "type": "application/x-cwl",
   "application:type": "cwl-workflow",
   "application:container": "True",
   "application:language": "Python"}]}
```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/workflows/context.jsonld",
  "id": "kindgrove-mangrove-biomass-workflow",
  "type": "Feature",
  "geometry": null,
  "conformsTo": [
    "http://www.opengis.net/spec/ogcapi-records-1/1.0/req/record-core"
  ],
  "properties": {
    "title": "KindGrove: Mangrove Biomass Estimation",
    "description": "An interactive Jupyter notebook workflow for estimating mangrove forest biomass and carbon stocks using Sentinel-2 satellite imagery from AWS Open Data Registry. This demonstrates an initial baseline approach that can be augmented with complementary data sources (LiDAR, InSAR, thermal) or integrated with coastal vulnerability assessments depending on project needs.\n\n### Open Data Architecture\n- Sentinel-2 L2A imagery via AWS STAC catalog (no authentication)\n- Cloud-optimized GeoTIFF processing\n- STAC-compliant data discovery\n\n### Validated Scientific Methods\n- Biomass model R\u00b2 = 0.72 (validated against 600+ field plots)\n- Detection accuracy: 85-90% (conservative threshold approach)\n- Uncertainty: \u00b130% (meets IPCC Tier 2 requirements)\n\n### Workflow Stages\n1. Study Area Definition - Interactive location selector\n2. STAC Data Discovery - Query AWS catalog for cloud-free scenes\n3. Vegetation Index Calculation - NDVI, NDWI, SAVI from spectral bands\n4. Mangrove Detection - Threshold-based classification\n5. Biomass Estimation - Allometric model (Biomass = 250.5 \u00d7 NDVI - 75.2)\n6. Carbon Accounting - IPCC-compliant calculations",
    "osc:type": "workflow",
    "osc:project": "ospd",
    "osc:status": "development",
    "application:type": "cwl-workflow",
    "application:container": "True",
    "application:language": "Python",
    "updated": "2024-07-30T12:00:00Z",
    "created": "2024-07-30T12:00:00Z",
    "keywords": [
      "mangrove",
      "biomass",
      "carbon",
      "sentinel-2",
      "stac"
    ],
    "license": "MIT",
    "version": "1",
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
    "contacts": [
      {
        "name": "Cameron Sajedi",
        "roles": [
          "developer"
        ],
        "emails": []
      }
    ],
    "extent": null
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
      "href": "../kindgrove-mangrove-biomass-workflow/record.json",
      "type": "application/json"
    },
    {
      "rel": "related",
      "href": "../../projects/ospd/collection.json",
      "type": "application/json",
      "title": "Project: OSPD"
    },
    {
      "rel": "related",
      "href": "../../themes/land/catalog.json",
      "type": "application/json",
      "title": "Theme: Land"
    },
    {
      "rel": "vcs",
      "title": "Git source repository",
      "href": "https://github.com/starling-foundries/KindGrove",
      "vcs:type": "git",
      "vcs:branch": "main"
    },
    {
      "rel": "application",
      "title": "KindGrove Mangrove Biomass Workflow",
      "href": "https://github.com/starling-foundries/KindGrove/blob/main/mangrove_workflow.cwl",
      "type": "application/x-cwl",
      "application:type": "cwl-workflow",
      "application:container": "True",
      "application:language": "Python"
    }
  ]
}
```

#### ttl
```ttl
@prefix dcterms: <http://purl.org/dc/terms/> .
@prefix geojson: <https://purl.org/geojson/vocab#> .
@prefix ns1: <http://www.iana.org/assignments/> .
@prefix ns2: <vcs:> .
@prefix ns3: <application:> .
@prefix oa: <http://www.w3.org/ns/oa#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .

<https://ogc.org/demo/ospd/kindgrove-mangrove-biomass-workflow> a geojson:Feature ;
    dcterms:conformsTo <http://www.opengis.net/spec/ogcapi-records-1/1.0/req/record-core> ;
    rdfs:seeAlso [ rdfs:label "Open Science Catalog" ;
            dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/root> ;
            oa:hasTarget <https://ogc.org/catalog.json> ],
        [ rdfs:label "KindGrove Mangrove Biomass Workflow" ;
            ns3:container "True" ;
            ns3:language "Python" ;
            ns3:type "cwl-workflow" ;
            dcterms:type "application/x-cwl" ;
            ns1:relation <http://www.iana.org/assignments/relation/application> ;
            oa:hasTarget <https://github.com/starling-foundries/KindGrove/blob/main/mangrove_workflow.cwl> ],
        [ rdfs:label "Git source repository" ;
            ns1:relation <http://www.iana.org/assignments/relation/vcs> ;
            oa:hasTarget <https://github.com/starling-foundries/KindGrove> ;
            ns2:branch "main" ;
            ns2:type "git" ],
        [ rdfs:label "Project: OSPD" ;
            dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/related> ;
            oa:hasTarget <https://ogc.org/projects/ospd/collection.json> ],
        [ rdfs:label "Theme: Land" ;
            dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/related> ;
            oa:hasTarget <https://ogc.org/themes/land/catalog.json> ],
        [ rdfs:label "Workflows" ;
            dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/parent> ;
            oa:hasTarget <https://ogc.org/demo/catalog.json> ],
        [ dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/self> ;
            oa:hasTarget <https://ogc.org/demo/kindgrove-mangrove-biomass-workflow/record.json> ] .


```


### Coastal Vulnerability Index (CVI) Workflow
An automated, reproducible workflow for calculating the Coastal Vulnerability Index (CVI). This system generates coastal transects, fetches satellite data (DEM, Land Cover), computes physical parameters, and classifies coastal risk based on the USGS/NOAA methodology.\n\nThe workflow is implemented in Common Workflow Language (CWL) and runs inside a Docker container, ensuring it can be executed anywhere—from a local laptop to a High-Performance Computing (HPC) cluster or JupyterHub.
#### json
```json
 {"id": "cvi-workflow",
 "type": "Feature",
 "geometry": null,
 "conformsTo": ["http://www.opengis.net/spec/ogcapi-records-1/1.0/req/record-core",
  "https://stac-extensions.github.io/osc/v1.0.0/schema.json"],
 "properties": {"title": "Coastal Vulnerability Index (CVI) Workflow",
  "description": "An automated, reproducible workflow for calculating the Coastal Vulnerability Index (CVI). This system generates coastal transects, fetches satellite data (DEM, Land Cover), computes physical parameters, and classifies coastal risk based on the USGS/NOAA methodology.\n\nThe workflow is implemented in Common Workflow Language (CWL) and runs inside a Docker container, ensuring it can be executed anywhere—from a local laptop to a High-Performance Computing (HPC) cluster or JupyterHub.",
  "osc:type": "workflow",
  "osc:project": "ospd",
  "osc:status": "completed",
  "application:type": "cwl-workflow",
  "application:container": true,
  "application:language": "Python",
  "updated": "2024-07-30T12:00:00Z",
  "created": "2024-07-30T12:00:00Z",
  "keywords": ["coastal vulnerability",
   "CVI",
   "workflow",
   "CWL",
   "Earth observation"],
  "license": "MIT",
  "version": "1",
  "themes": [{"scheme": "https://github.com/stac-extensions/osc#theme",
    "concepts": [{"id": "oceans"}]}],
  "contacts": [{"name": "HARTIS Integrated Nautical Services",
    "roles": ["consortium_member"],
    "emails": [{"value": "info@hartis.org"}]}],
  "extent": null},
 "linkTemplates": [],
 "links": [{"rel": "root",
   "href": "../../catalog.json",
   "type": "application/json",
   "title": "Open Science Catalog"},
  {"rel": "parent",
   "href": "../catalog.json",
   "type": "application/json",
   "title": "Workflows"},
  {"rel": "self",
   "href": "./cvi-workflow/record.json",
   "type": "application/json"},
  {"rel": "related",
   "href": "../../projects/ospd/collection.json",
   "type": "application/json",
   "title": "Project: OSPD"},
  {"rel": "related",
   "href": "../../themes/oceans/catalog.json",
   "type": "application/json",
   "title": "Theme: Oceans"},
  {"rel": "vcs",
   "title": "Git source repository",
   "href": "https://github.com/hartis-org/cvi-workflow",
   "vcs:type": "git",
   "vcs:branch": "main"},
  {"rel": "application",
   "title": "Coastal Vulnerability Index (CVI) Workflow",
   "href": "https://github.com/hartis-org/cvi-workflow/blob/main/cvi_workflow.cwl",
   "type": "application/x-cwl",
   "application:type": "cwl-workflow",
   "application:container": true,
   "application:language": "Python"}]}
```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/workflows/context.jsonld",
  "id": "cvi-workflow",
  "type": "Feature",
  "geometry": null,
  "conformsTo": [
    "http://www.opengis.net/spec/ogcapi-records-1/1.0/req/record-core",
    "https://stac-extensions.github.io/osc/v1.0.0/schema.json"
  ],
  "properties": {
    "title": "Coastal Vulnerability Index (CVI) Workflow",
    "description": "An automated, reproducible workflow for calculating the Coastal Vulnerability Index (CVI). This system generates coastal transects, fetches satellite data (DEM, Land Cover), computes physical parameters, and classifies coastal risk based on the USGS/NOAA methodology.\n\nThe workflow is implemented in Common Workflow Language (CWL) and runs inside a Docker container, ensuring it can be executed anywhere\u2014from a local laptop to a High-Performance Computing (HPC) cluster or JupyterHub.",
    "osc:type": "workflow",
    "osc:project": "ospd",
    "osc:status": "completed",
    "application:type": "cwl-workflow",
    "application:container": true,
    "application:language": "Python",
    "updated": "2024-07-30T12:00:00Z",
    "created": "2024-07-30T12:00:00Z",
    "keywords": [
      "coastal vulnerability",
      "CVI",
      "workflow",
      "CWL",
      "Earth observation"
    ],
    "license": "MIT",
    "version": "1",
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
    "contacts": [
      {
        "name": "HARTIS Integrated Nautical Services",
        "roles": [
          "consortium_member"
        ],
        "emails": [
          {
            "value": "info@hartis.org"
          }
        ]
      }
    ],
    "extent": null
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
      "href": "./cvi-workflow/record.json",
      "type": "application/json"
    },
    {
      "rel": "related",
      "href": "../../projects/ospd/collection.json",
      "type": "application/json",
      "title": "Project: OSPD"
    },
    {
      "rel": "related",
      "href": "../../themes/oceans/catalog.json",
      "type": "application/json",
      "title": "Theme: Oceans"
    },
    {
      "rel": "vcs",
      "title": "Git source repository",
      "href": "https://github.com/hartis-org/cvi-workflow",
      "vcs:type": "git",
      "vcs:branch": "main"
    },
    {
      "rel": "application",
      "title": "Coastal Vulnerability Index (CVI) Workflow",
      "href": "https://github.com/hartis-org/cvi-workflow/blob/main/cvi_workflow.cwl",
      "type": "application/x-cwl",
      "application:type": "cwl-workflow",
      "application:container": true,
      "application:language": "Python"
    }
  ]
}
```

#### ttl
```ttl
@prefix dcterms: <http://purl.org/dc/terms/> .
@prefix geojson: <https://purl.org/geojson/vocab#> .
@prefix ns1: <application:> .
@prefix ns2: <http://www.iana.org/assignments/> .
@prefix ns3: <vcs:> .
@prefix oa: <http://www.w3.org/ns/oa#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

<https://ogc.org/demo/ospd/cvi-workflow> a geojson:Feature ;
    dcterms:conformsTo <http://www.opengis.net/spec/ogcapi-records-1/1.0/req/record-core>,
        <https://stac-extensions.github.io/osc/v1.0.0/schema.json> ;
    rdfs:seeAlso [ rdfs:label "Theme: Oceans" ;
            dcterms:type "application/json" ;
            ns2:relation <http://www.iana.org/assignments/relation/related> ;
            oa:hasTarget <https://ogc.org/themes/oceans/catalog.json> ],
        [ rdfs:label "Git source repository" ;
            ns2:relation <http://www.iana.org/assignments/relation/vcs> ;
            oa:hasTarget <https://github.com/hartis-org/cvi-workflow> ;
            ns3:branch "main" ;
            ns3:type "git" ],
        [ rdfs:label "Project: OSPD" ;
            dcterms:type "application/json" ;
            ns2:relation <http://www.iana.org/assignments/relation/related> ;
            oa:hasTarget <https://ogc.org/projects/ospd/collection.json> ],
        [ rdfs:label "Coastal Vulnerability Index (CVI) Workflow" ;
            ns1:container true ;
            ns1:language "Python" ;
            ns1:type "cwl-workflow" ;
            dcterms:type "application/x-cwl" ;
            ns2:relation <http://www.iana.org/assignments/relation/application> ;
            oa:hasTarget <https://github.com/hartis-org/cvi-workflow/blob/main/cvi_workflow.cwl> ],
        [ rdfs:label "Workflows" ;
            dcterms:type "application/json" ;
            ns2:relation <http://www.iana.org/assignments/relation/parent> ;
            oa:hasTarget <https://ogc.org/demo/catalog.json> ],
        [ rdfs:label "Open Science Catalog" ;
            dcterms:type "application/json" ;
            ns2:relation <http://www.iana.org/assignments/relation/root> ;
            oa:hasTarget <https://ogc.org/catalog.json> ],
        [ dcterms:type "application/json" ;
            ns2:relation <http://www.iana.org/assignments/relation/self> ;
            oa:hasTarget <https://ogc.org/demo/ospd/cvi-workflow/record.json> ] .


```


### ML4Floods Inference for Flood Extent Estimation
ML4Floods inference for flood extent estimation using a pre-trained model on Sentinel-2 or Landsat-9 data. This application is designed to process satellite imagery and delineate flood extents.
#### json
```json
{"id": "app-ml4floods",
 "type": "Feature",
 "geometry": null,
 "conformsTo": ["http://www.opengis.net/spec/ogcapi-records-1/1.0/req/record-core",
  "https://stacspec.org/STAC-api.html",
  "https://stac-extensions.github.io/osc/v1.0.0/schema.json",
  "https://stac-extensions.github.io/version/v1.0.0/schema.json",
  "https://stac-extensions.github.io/eo/v1.0.0/schema.json"],
 "properties": {"title": "ML4Floods Inference for Flood Extent Estimation",
  "description": "ML4Floods inference for flood extent estimation using a pre-trained model on Sentinel-2 or Landsat-9 data. This application is designed to process satellite imagery and delineate flood extents.",
  "osc:type": "workflow",
  "osc:project": "ospd",
  "osc:status": "completed",
  "application:type": "cwl-workflow",
  "application:container": true,
  "application:language": "Python",
  "updated": "2024-07-30T12:34:56Z",
  "created": "2024-07-30T12:34:56Z",
  "keywords": ["ML4Floods",
   "flood mapping",
   "Sentinel-2",
   "Landsat-9",
   "remote sensing"],
  "license": "MIT",
  "version": "1",
  "themes": [{"scheme": "https://github.com/stac-extensions/osc#theme",
    "concepts": [{"id": "land"}]}],
  "contacts": [{"name": "Fabrice Brito",
    "roles": ["developer"],
    "emails": [{"value": "fabrice.brito@terradue.com"}]}],
  "extent": null},
 "linkTemplates": [],
 "links": [{"rel": "root",
   "href": "../../catalog.json",
   "type": "application/json",
   "title": "Open Science Catalog"},
  {"rel": "parent",
   "href": "../catalog.json",
   "type": "application/json",
   "title": "Workflows"},
  {"rel": "self",
   "href": "../workflows/app-ml4floods/record.json",
   "type": "application/json"},
  {"rel": "related",
   "href": "../../projects/ospd/collection.json",
   "type": "application/json",
   "title": "Project: OSPD"},
  {"rel": "related",
   "href": "../../themes/land/catalog.json",
   "type": "application/json",
   "title": "Theme: Land"},
  {"rel": "vcs",
   "title": "Git source repository",
   "href": "https://github.com/eoap/app-ml4floods",
   "vcs:type": "git",
   "vcs:branch": "main"},
  {"rel": "application",
   "title": "ML4Floods Inference Workflow",
   "href": "https://github.com/eoap/app-ml4floods/blob/main/cwl-workflow/app-ml4floods.cwl",
   "type": "application/cwl",
   "application:type": "cwl-workflow",
   "application:container": true,
   "application:language": "Python"}]}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/workflows/context.jsonld",
  "id": "app-ml4floods",
  "type": "Feature",
  "geometry": null,
  "conformsTo": [
    "http://www.opengis.net/spec/ogcapi-records-1/1.0/req/record-core",
    "https://stacspec.org/STAC-api.html",
    "https://stac-extensions.github.io/osc/v1.0.0/schema.json",
    "https://stac-extensions.github.io/version/v1.0.0/schema.json",
    "https://stac-extensions.github.io/eo/v1.0.0/schema.json"
  ],
  "properties": {
    "title": "ML4Floods Inference for Flood Extent Estimation",
    "description": "ML4Floods inference for flood extent estimation using a pre-trained model on Sentinel-2 or Landsat-9 data. This application is designed to process satellite imagery and delineate flood extents.",
    "osc:type": "workflow",
    "osc:project": "ospd",
    "osc:status": "completed",
    "application:type": "cwl-workflow",
    "application:container": true,
    "application:language": "Python",
    "updated": "2024-07-30T12:34:56Z",
    "created": "2024-07-30T12:34:56Z",
    "keywords": [
      "ML4Floods",
      "flood mapping",
      "Sentinel-2",
      "Landsat-9",
      "remote sensing"
    ],
    "license": "MIT",
    "version": "1",
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
    "contacts": [
      {
        "name": "Fabrice Brito",
        "roles": [
          "developer"
        ],
        "emails": [
          {
            "value": "fabrice.brito@terradue.com"
          }
        ]
      }
    ],
    "extent": null
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
      "href": "../workflows/app-ml4floods/record.json",
      "type": "application/json"
    },
    {
      "rel": "related",
      "href": "../../projects/ospd/collection.json",
      "type": "application/json",
      "title": "Project: OSPD"
    },
    {
      "rel": "related",
      "href": "../../themes/land/catalog.json",
      "type": "application/json",
      "title": "Theme: Land"
    },
    {
      "rel": "vcs",
      "title": "Git source repository",
      "href": "https://github.com/eoap/app-ml4floods",
      "vcs:type": "git",
      "vcs:branch": "main"
    },
    {
      "rel": "application",
      "title": "ML4Floods Inference Workflow",
      "href": "https://github.com/eoap/app-ml4floods/blob/main/cwl-workflow/app-ml4floods.cwl",
      "type": "application/cwl",
      "application:type": "cwl-workflow",
      "application:container": true,
      "application:language": "Python"
    }
  ]
}
```

#### ttl
```ttl
@prefix dcterms: <http://purl.org/dc/terms/> .
@prefix geojson: <https://purl.org/geojson/vocab#> .
@prefix ns1: <http://www.iana.org/assignments/> .
@prefix ns2: <application:> .
@prefix ns3: <vcs:> .
@prefix oa: <http://www.w3.org/ns/oa#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

<https://ogc.org/demo/ospd/app-ml4floods> a geojson:Feature ;
    dcterms:conformsTo <http://www.opengis.net/spec/ogcapi-records-1/1.0/req/record-core>,
        <https://stac-extensions.github.io/eo/v1.0.0/schema.json>,
        <https://stac-extensions.github.io/osc/v1.0.0/schema.json>,
        <https://stac-extensions.github.io/version/v1.0.0/schema.json>,
        <https://stacspec.org/STAC-api.html> ;
    rdfs:seeAlso [ rdfs:label "Workflows" ;
            dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/parent> ;
            oa:hasTarget <https://ogc.org/demo/catalog.json> ],
        [ rdfs:label "Project: OSPD" ;
            dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/related> ;
            oa:hasTarget <https://ogc.org/projects/ospd/collection.json> ],
        [ rdfs:label "ML4Floods Inference Workflow" ;
            ns2:container true ;
            ns2:language "Python" ;
            ns2:type "cwl-workflow" ;
            dcterms:type "application/cwl" ;
            ns1:relation <http://www.iana.org/assignments/relation/application> ;
            oa:hasTarget <https://github.com/eoap/app-ml4floods/blob/main/cwl-workflow/app-ml4floods.cwl> ],
        [ dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/self> ;
            oa:hasTarget <https://ogc.org/demo/workflows/app-ml4floods/record.json> ],
        [ rdfs:label "Theme: Land" ;
            dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/related> ;
            oa:hasTarget <https://ogc.org/themes/land/catalog.json> ],
        [ rdfs:label "Open Science Catalog" ;
            dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/root> ;
            oa:hasTarget <https://ogc.org/catalog.json> ],
        [ rdfs:label "Git source repository" ;
            ns1:relation <http://www.iana.org/assignments/relation/vcs> ;
            oa:hasTarget <https://github.com/eoap/app-ml4floods> ;
            ns3:branch "main" ;
            ns3:type "git" ] .


```

## Schema

```yaml
$schema: https://json-schema.org/draft/2020-12/schema
description: Schema for EarthCODE Workflow
allOf:
- $ref: https://ogcincubator.github.io/geodcat-ogcapi-records/build/annotated/geo/geodcat/geodcat-records/schema.yaml
properties:
  properties:
    type: object
    anyOf:
    - $ref: https://ogcincubator.github.io/bblock-prov-schema/build/annotated/ogc-utils/prov-entity/schema.yaml
    - not:
        required:
        - provType
    required:
    - osc:project
    properties:
      osc:project:
        $ref: https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/common/schema.yaml#/$defs/osc:project
      wfdesc:hasInput:
        type: object
        additionalProperties:
          type: object
          $ref: https://ogcincubator.github.io/bblocks-ogcapi-processes/build/annotated/api/processes/v1/schemas/inputDescription/schema.yaml
      wfdesc:hasOutput:
        type: object
        additionalProperties:
          type: object
          $ref: https://ogcincubator.github.io/bblocks-ogcapi-processes/build/annotated/api/processes/v1/schemas/outputDescription/schema.yaml
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
      - $ref: https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/common/schema.yaml#/$defs/via_links

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
    "type": "@type",
    "id": "@id",
    "properties": {
      "@context": {
        "language": {
          "@context": {
            "code": {},
            "alternate": {},
            "dir": {}
          },
          "@id": "rec:language"
        },
        "languages": {
          "@context": {
            "code": {},
            "alternate": {},
            "dir": {}
          },
          "@container": "@set",
          "@id": "rec:languages"
        },
        "resourceLanguages": {
          "@context": {
            "code": {},
            "alternate": {},
            "dir": {}
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
            },
            "scheme": "thns:scheme"
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
            "identifier": {},
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
            "phones": {},
            "emails": {},
            "addresses": {
              "@context": {
                "deliveryPoint": {},
                "city": {},
                "administrativeArea": {},
                "postalCode": {},
                "country": {}
              }
            },
            "hoursOfService": {},
            "contactInstructions": {},
            "roles": {}
          },
          "@container": "@set",
          "@id": "dcat:contactPoint",
          "@type": "@id"
        },
        "license": "dcat:license",
        "rights": "dcat:rights"
      }
    },
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
        "type": "dct:type",
        "hreflang": "dct:language",
        "title": "rdfs:label",
        "length": "dct:extent",
        "anchor": {}
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
    "variables": {
      "@container": "@id",
      "@id": "rec:hasVariable",
      "@context": {
        "@base": "http://example.com/variables/",
        "@vocab": "https://www.opengis.net/def/ogc-api/records/"
      }
    },
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
        "anchor": {},
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
            "anchor": {},
            "hreflang": "dct:language",
            "title": "rdfs:label",
            "length": "dct:extent"
          },
          "@id": "prov:influencer",
          "@type": "@id"
        },
        "activity": {
          "@context": {
            "type": "dct:type",
            "wasAssociatedWith": {
              "@context": {
                "rel": {
                  "@context": {
                    "@base": "http://www.iana.org/assignments/relation/"
                  },
                  "@id": "http://www.iana.org/assignments/relation",
                  "@type": "@id"
                },
                "anchor": {},
                "hreflang": "dct:language",
                "title": "rdfs:label",
                "length": "dct:extent"
              },
              "@id": "prov:wasAssociatedWith",
              "@type": "@id"
            }
          },
          "@id": "prov:activity",
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
            "anchor": {},
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
    "prov:type": {},
    "hadMember": {
      "@id": "prov:hadMember",
      "@type": "@id"
    },
    "featureType": "@type",
    "entityType": "@type",
    "has_provenance": {
      "@context": {
        "type": "dct:type",
        "wasAssociatedWith": {
          "@id": "prov:wasAssociatedWith",
          "@type": "@id",
          "@context": {
            "rel": {
              "@context": {
                "@base": "http://www.iana.org/assignments/relation/"
              },
              "@id": "http://www.iana.org/assignments/relation",
              "@type": "@id"
            },
            "anchor": {},
            "hreflang": "dct:language",
            "title": "rdfs:label",
            "length": "dct:extent"
          }
        }
      },
      "@id": "dct:provenance",
      "@type": "@id"
    },
    "wasGeneratedBy": {
      "@context": {
        "type": "dct:type",
        "wasAssociatedWith": {
          "@context": {
            "rel": {
              "@context": {
                "@base": "http://www.iana.org/assignments/relation/"
              },
              "@id": "http://www.iana.org/assignments/relation",
              "@type": "@id"
            },
            "anchor": {},
            "hreflang": "dct:language",
            "title": "rdfs:label",
            "length": "dct:extent"
          },
          "@id": "prov:wasAssociatedWith",
          "@type": "@id"
        }
      },
      "@id": "prov:wasGeneratedBy",
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
        "anchor": {},
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
      "@context": {
        "type": "dct:type",
        "wasAssociatedWith": {
          "@context": {
            "rel": {
              "@context": {
                "@base": "http://www.iana.org/assignments/relation/"
              },
              "@id": "http://www.iana.org/assignments/relation",
              "@type": "@id"
            },
            "anchor": {},
            "hreflang": "dct:language",
            "title": "rdfs:label",
            "length": "dct:extent"
          },
          "@id": "prov:wasAssociatedWith",
          "@type": "@id"
        }
      },
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
    "qualifiedGeneration": {
      "@id": "prov:qualifiedGeneration",
      "@type": "@id"
    },
    "qualifiedInvalidation": {
      "@id": "prov:qualifiedInvalidation",
      "@type": "@id"
    },
    "qualifiedDerivation": {
      "@context": {
        "hadActivity": {
          "@context": {
            "type": "dct:type",
            "wasAssociatedWith": {
              "@context": {
                "rel": {
                  "@context": {
                    "@base": "http://www.iana.org/assignments/relation/"
                  },
                  "@id": "http://www.iana.org/assignments/relation",
                  "@type": "@id"
                },
                "anchor": {},
                "hreflang": "dct:language",
                "title": "rdfs:label",
                "length": "dct:extent"
              },
              "@id": "prov:wasAssociatedWith",
              "@type": "@id"
            }
          },
          "@id": "prov:hadActivity",
          "@type": "@id"
        }
      },
      "@id": "prov:qualifiedDerivation",
      "@type": "@id"
    },
    "qualifiedAttribution": {
      "@context": {
        "agent": {
          "@context": {
            "type": "dct:type"
          },
          "@id": "prov:agent",
          "@type": "@id"
        }
      },
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
    "osc:project": {},
    "additionalParameters": {
      "@context": {
        "role": {},
        "parameters": {}
      }
    },
    "metadata": {
      "@context": {
        "role": {}
      }
    },
    "maxOccurs": {},
    "minOccurs": {},
    "schema": {
      "@context": {
        "$ref": {},
        "additionalProperties": {},
        "allOf": {},
        "anyOf": {},
        "contentEncoding": {},
        "contentMediaType": {},
        "contentSchema": {},
        "default": {},
        "deprecated": {},
        "enum": {},
        "example": {},
        "exclusiveMaximum": {},
        "exclusiveMinimum": {},
        "format": {},
        "items": {},
        "maxItems": {},
        "maxLength": {},
        "maxProperties": {},
        "maximum": {},
        "minItems": {},
        "minLength": {},
        "minProperties": {},
        "minimum": {},
        "multipleOf": {},
        "not": {},
        "nullable": {},
        "oneOf": {},
        "pattern": {},
        "readOnly": {},
        "required": {},
        "uniqueItems": {},
        "writeOnly": {}
      }
    },
    "wfdesc:hasInput": {},
    "wfdesc:hasOutput": {},
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

