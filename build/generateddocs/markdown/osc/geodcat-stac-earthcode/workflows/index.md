
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
  "@context": "https://nenadradosevic.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/workflows/context.jsonld",
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
    rdfs:seeAlso [ rdfs:label "Theme: Cryosphere" ;
            dcterms:format "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/related> ;
            oa:hasTarget <https://ogc.org/themes/cryosphere/catalog.json> ],
        [ rdfs:label "Trigger workflow via API provided by pygeoapi" ;
            dcterms:format "text/html" ;
            ns1:relation <http://www.iana.org/assignments/relation/related> ;
            oa:hasTarget <https://harshness-map.gtif.eox.at/processes/execute-polarwarp-gcps> ],
        [ rdfs:label "Project: Cerulean Information Factory" ;
            dcterms:format "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/related> ;
            oa:hasTarget <https://ogc.org/projects/cerulean-information-factory/collection.json> ],
        [ rdfs:label "Theme: Oceans" ;
            dcterms:format "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/related> ;
            oa:hasTarget <https://ogc.org/themes/oceans/catalog.json> ],
        [ rdfs:label "Polarwarp" ;
            dcterms:format "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/child> ;
            oa:hasTarget <https://ogc.org/experiments/polarwarp/record.json> ],
        [ rdfs:label "Polarwarp workflow" ;
            ns2:container true ;
            ns2:language "Python" ;
            ns2:type "argo-workflow" ;
            <argo-workflow:> [ ] ;
            dcterms:format "application/x-argo-workflow-yaml" ;
            ns1:relation <http://www.iana.org/assignments/relation/application> ;
            oa:hasTarget <https://github.com/gtif-cerulean/polarwarp/blob/main/workflow.yml> ],
        [ rdfs:label "Workflows" ;
            dcterms:format "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/parent> ;
            oa:hasTarget <https://ogc.org/demo/catalog.json> ],
        [ rdfs:label "Open Science Catalog" ;
            dcterms:format "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/root> ;
            oa:hasTarget <https://ogc.org/catalog.json> ],
        [ rdfs:label "EOxHub Workspaces" ;
            ns2:platform_supports "argo-workflow" ;
            ns2:preferred_app "argo" ;
            dcterms:format "text/html" ;
            ns1:relation <http://www.iana.org/assignments/relation/application-originating-platform> ;
            oa:hasTarget <https://workspace.cif.hub-otc.eox.at/> ],
        [ rdfs:label "Git source repository" ;
            ns1:relation <http://www.iana.org/assignments/relation/vcs> ;
            oa:hasTarget <https://github.com/gtif-cerulean/polarwarp.git> ;
            ns3:branch "main" ;
            ns3:type "git" ],
        [ dcterms:format "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/self> ;
            oa:hasTarget <https://esa-earthcode.github.io/open-science-catalog-metadata/workflows/polarwarp/record.json> ] .


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
  "@context": "https://nenadradosevic.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/workflows/context.jsonld",
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
    rdfs:seeAlso [ rdfs:label "Workflows" ;
            dcterms:format "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/parent> ;
            oa:hasTarget <https://ogc.org/demo/catalog.json> ],
        [ rdfs:label "POLARIS" ;
            dcterms:format "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/child> ;
            oa:hasTarget <https://ogc.org/experiments/polaris-experiment/record.json> ],
        [ rdfs:label "Project: POLARIS" ;
            dcterms:format "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/related> ;
            oa:hasTarget <https://ogc.org/projects/polaris/collection.json> ],
        [ rdfs:label "Theme: Oceans" ;
            dcterms:format "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/related> ;
            oa:hasTarget <https://ogc.org/themes/oceans/catalog.json> ],
        [ dcterms:format "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/self> ;
            oa:hasTarget <https://esa-earthcode.github.io/open-science-catalog-metadata/workflows/polaris-workflow/record.json> ],
        [ rdfs:label "Git source repository" ;
            dcterms:format "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/git> ;
            oa:hasTarget <https://github.com/gtif-cerulean/cerulean-catalog.git> ],
        [ rdfs:label "OGC Application Package" ;
            dcterms:format "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/application> ;
            oa:hasTarget <https://github.com/gtif-cerulean/cerulean-catalog.git> ],
        [ rdfs:label "Open Science Catalog" ;
            dcterms:format "application/json" ;
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
  "@context": "https://nenadradosevic.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/workflows/context.jsonld",
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
    rdfs:seeAlso [ rdfs:label "Workflows" ;
            dcterms:format "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/parent> ;
            oa:hasTarget <https://ogc.org/demo/catalog.json> ],
        [ rdfs:label "OGC Application Package" ;
            dcterms:format "application/clw+yaml" ;
            dcterms:language "" ;
            ns1:relation <http://www.iana.org/assignments/relation/application> ;
            oa:hasTarget <https://raw.githubusercontent.com/tjellicoe-tpzuk/eo-workflow-examples/refs/heads/main/water-bodies/water-bodies.cwl> ],
        [ rdfs:label "Project: OSPD" ;
            dcterms:format "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/related> ;
            oa:hasTarget <https://ogc.org/projects/ospd/collection.json> ],
        [ dcterms:format "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/self> ;
            oa:hasTarget <https://esa-earthcode.github.io/open-science-catalog-metadata/workflows/waterbodies/record.json> ],
        [ rdfs:label "Open Science Catalog" ;
            dcterms:format "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/root> ;
            oa:hasTarget <https://ogc.org/catalog.json> ] .


```


### Mangrove Detect
The mangrove biomass workflow demonstrates an initial approach to estimating above-ground biomass and carbon stocks using Sentinel-2 optical satellite imagery. This serves as a baseline workflow that can be augmented with complementary data sources depending on project needs. The current implementation queries the AWS STAC catalog for cloud-free scenes, calculates vegetation indices (NDVI, NDWI, SAVI), applies threshold-based classification to detect mangrove extent, and estimates biomass using a validated allometric equation from Myanmar field studies. Results include spatially explicit biomass maps, carbon stock totals, and CO2 equivalence calculations following IPCC Tier 2 methodology.
calculation.
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
  "@context": "https://nenadradosevic.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/workflows/context.jsonld",
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
    rdfs:seeAlso [ dcterms:format "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/self> ;
            oa:hasTarget <https://esa-earthcode.github.io/open-science-catalog-metadata/workflows/polaris-workflow/record.json> ],
        [ rdfs:label "POLARIS" ;
            dcterms:format "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/child> ;
            oa:hasTarget <https://ogc.org/experiments/polaris-experiment/record.json> ],
        [ rdfs:label "Open Science Catalog" ;
            dcterms:format "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/root> ;
            oa:hasTarget <https://ogc.org/catalog.json> ],
        [ rdfs:label "Git source repository" ;
            dcterms:format "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/git> ;
            oa:hasTarget <https://github.com/gtif-cerulean/cerulean-catalog.git> ],
        [ rdfs:label "Project: POLARIS" ;
            dcterms:format "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/related> ;
            oa:hasTarget <https://ogc.org/projects/polaris/collection.json> ],
        [ rdfs:label "Workflows" ;
            dcterms:format "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/parent> ;
            oa:hasTarget <https://ogc.org/demo/catalog.json> ],
        [ rdfs:label "OGC Application Package" ;
            dcterms:format "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/application> ;
            oa:hasTarget <https://github.com/gtif-cerulean/cerulean-catalog.git> ],
        [ rdfs:label "Theme: Oceans" ;
            dcterms:format "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/related> ;
            oa:hasTarget <https://ogc.org/themes/oceans/catalog.json> ] .


```

## Schema

```yaml
$schema: https://json-schema.org/draft/2020-12/schema
description: Schema for EarthCODE Workflow
allOf:
- anyOf:
  - $ref: https://ogcincubator.github.io/geodcat-ogcapi-records/build/annotated/geo/geodcat/geodcat-records/schema.yaml
properties:
  properties:
    type: object
    required:
    - osc:project
    properties:
      osc:project:
        $ref: https://nenadradosevic.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/common/schema.yaml#/$defs/osc:project
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
      - $ref: https://nenadradosevic.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/common/schema.yaml#/$defs/via_links

```

Links to the schema:

* YAML version: [schema.yaml](https://nenadradosevic.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/workflows/schema.json)
* JSON version: [schema.json](https://nenadradosevic.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/workflows/schema.yaml)


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
            "logo": {
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
        "rights": "dcat:rights"
      }
    },
    "geometry": {
      "@context": {
        "coordinates": {
          "@container": "@list",
          "@id": "geojson:coordinates"
        }
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
        "length": "dct:extent"
      },
      "@id": "rdfs:seeAlso"
    },
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
[context.jsonld](https://nenadradosevic.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/workflows/context.jsonld)

## Sources

* [GeoDCAT Specification](http://www.opengis.net/def/metamodel/profiles/geodcat)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/nenadradosevic/bblocks-openscience](https://github.com/nenadradosevic/bblocks-openscience)
* Path: `_sources/geodcat-stac-earthcode/workflows`

