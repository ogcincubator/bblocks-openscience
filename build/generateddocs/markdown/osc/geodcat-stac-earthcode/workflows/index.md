
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
  "@context": "https://nsnarayanam.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/workflows/context.jsonld",
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
@prefix dcat: <http://www.w3.org/ns/dcat#> .
@prefix dcterms: <http://purl.org/dc/terms/> .
@prefix ns1: <http://www.iana.org/assignments/> .
@prefix ns2: <application:> .
@prefix ns3: <vcs:> .
@prefix ns4: <osc:> .
@prefix oa: <http://www.w3.org/ns/oa#> .
@prefix proc: <https://w3id.org/ogc/api/processes/> .
@prefix prov: <http://www.w3.org/ns/prov#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix rec: <https://www.opengis.net/def/ogc-api/records/> .
@prefix thns: <https://w3id.org/ogc/stac/themes/> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

<https://ogc.org/demo/ospd/polarwarp> ns2:container true ;
    ns2:language "Python" ;
    ns2:type "argo-workflow" ;
    dcterms:conformsTo <http://www.opengis.net/spec/ogcapi-records-1/1.0/req/record-core>,
        <https://raw.githubusercontent.com/EOEPCA/metadata-profile/refs/heads/1.0/schemas/application-type-argo-workflow>,
        <https://stac-extensions.github.io/application/v0.1.0/schema.json> ;
    dcterms:created "2025-09-30T13:00:00Z" ;
    dcterms:description "The polarwarp algorithm geolocates, aligns, and warps satellite SAR images using forecast drift and wind/tide fields in polar regions." ;
    dcterms:modified "2025-09-30T14:00:00Z" ;
    dcterms:title "Polarwarp" ;
    rdfs:seeAlso [ rdfs:label "Project: Cerulean Information Factory" ;
            dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/related> ;
            oa:hasTarget <https://ogc.org/projects/cerulean-information-factory/collection.json> ],
        [ rdfs:label "Polarwarp" ;
            dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/child> ;
            oa:hasTarget <https://ogc.org/experiments/polarwarp/record.json> ],
        [ rdfs:label "Polarwarp workflow" ;
            ns2:container true ;
            ns2:language "Python" ;
            ns2:type "argo-workflow" ;
            <argo-workflow:> [ proc:requirements [ proc:temp_storage "10GB" ] ] ;
            dcterms:type "application/x-argo-workflow-yaml" ;
            ns1:relation <http://www.iana.org/assignments/relation/application> ;
            oa:hasTarget <https://github.com/gtif-cerulean/polarwarp/blob/main/workflow.yml> ],
        [ rdfs:label "Trigger workflow via API provided by pygeoapi" ;
            dcterms:type "text/html" ;
            ns1:relation <http://www.iana.org/assignments/relation/related> ;
            oa:hasTarget <https://harshness-map.gtif.eox.at/processes/execute-polarwarp-gcps> ],
        [ rdfs:label "Theme: Oceans" ;
            dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/related> ;
            oa:hasTarget <https://ogc.org/themes/oceans/catalog.json> ],
        [ rdfs:label "Workflows" ;
            dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/parent> ;
            oa:hasTarget <https://ogc.org/demo/catalog.json> ],
        [ dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/self> ;
            oa:hasTarget <https://esa-earthcode.github.io/open-science-catalog-metadata/workflows/polarwarp/record.json> ],
        [ rdfs:label "Open Science Catalog" ;
            dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/root> ;
            oa:hasTarget <https://ogc.org/catalog.json> ],
        [ rdfs:label "EOxHub Workspaces" ;
            ns2:platform_supports "argo-workflow" ;
            ns2:preferred_app "argo" ;
            dcterms:type "text/html" ;
            ns1:relation <http://www.iana.org/assignments/relation/application-originating-platform> ;
            oa:hasTarget <https://workspace.cif.hub-otc.eox.at/> ],
        [ rdfs:label "Theme: Cryosphere" ;
            dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/related> ;
            oa:hasTarget <https://ogc.org/themes/cryosphere/catalog.json> ],
        [ rdfs:label "Git source repository" ;
            ns1:relation <http://www.iana.org/assignments/relation/vcs> ;
            oa:hasTarget <https://github.com/gtif-cerulean/polarwarp.git> ;
            ns3:branch "main" ;
            ns3:type "git" ] ;
    dcat:contactPoint [ rdfs:label "David Arthurs" ;
            proc:emails [ prov:value "david.arthurs@polarview.org" ] ;
            proc:roles "consortium_member" ],
        [ rdfs:label "Týna Doležalová" ;
            proc:emails [ prov:value "tyna.dolezalova@eox.at" ] ;
            proc:roles "consortium_member" ] ;
    dcat:keyword "polar",
        "sea ice" ;
    dcat:license "CC-BY-SA-4.0" ;
    proc:type "Feature",
        "workflow" ;
    rec:themes [ thns:concepts [ thns:id "oceans"^^xsd:string ] ;
            thns:scheme "https://github.com/stac-extensions/osc#theme" ],
        [ thns:concepts [ thns:id "cryosphere"^^xsd:string ] ;
            thns:scheme "https://github.com/stac-extensions/osc#theme" ] ;
    ns4:project "cerulean-information-factory" .


```


### Polaris
The Polar Operational Limit Assessment Risk Indexing System (POLARIS) is a methodology to assess the risk posed to a ship by ice conditions in relation to the ship's assigned ice class. It uses the WMO standard sea ice charts as the basis for the calculation.
#### json
```json
{
  "id": "polaris-workflow",
  "type": "Feature",
  "conformsTo": [
    "http://www.opengis.net/spec/ogcapi-records-1/1.0/req/record-core",
    "https://stac-extensions.github.io/application/v0.1.0/schema.json",
    "https://raw.githubusercontent.com/EOEPCA/metadata-profile/refs/heads/1.0/schemas/application-type-argo-workflow"
  ],
  "geometry": null,
  "properties": {
    "created": "2025-02-19T23:00:00Z",
    "updated": "2025-03-03T22:00:00Z",
    "type": "workflow",
    "title": "POLARIS",
    "description": "Polar Operational Limit Assessment Risk Index System (POLARIS) algorithm.",
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
      "href": "https://esa-earthcode.github.io/open-science-catalog-metadata/workflows/polaris-workflow/record.json",
      "type": "application/json"
    },
    {
      "rel": "related",
      "href": "../../projects/cerulean-information-factory/collection.json",
      "type": "application/json",
      "title": "Project: Cerulean Information Factory"
    },
    {
      "rel": "child",
      "href": "../../experiments/polaris/record.json",
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
      "rel": "vcs",
      "title": "Git source repository",
      "href": "https://github.com/gtif-cerulean/polaris.git",
      "vcs:type": "git",
      "vcs:branch": "main"
    },
    {
      "rel": "application",
      "title": "POLARIS workflow",
      "href": "https://github.com/gtif-cerulean/polaris/blob/main/workflow.yml",
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
      "href": "https://harshness-map.gtif.eox.at/processes/execute-polaris",
      "type": "text/html",
      "title": "Trigger workflow via API provided by pygeoapi"
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
  "@context": "https://nsnarayanam.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/workflows/context.jsonld",
  "id": "polaris-workflow",
  "type": "Feature",
  "conformsTo": [
    "http://www.opengis.net/spec/ogcapi-records-1/1.0/req/record-core",
    "https://stac-extensions.github.io/application/v0.1.0/schema.json",
    "https://raw.githubusercontent.com/EOEPCA/metadata-profile/refs/heads/1.0/schemas/application-type-argo-workflow"
  ],
  "geometry": null,
  "properties": {
    "created": "2025-02-19T23:00:00Z",
    "updated": "2025-03-03T22:00:00Z",
    "type": "workflow",
    "title": "POLARIS",
    "description": "Polar Operational Limit Assessment Risk Index System (POLARIS) algorithm.",
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
      "href": "https://esa-earthcode.github.io/open-science-catalog-metadata/workflows/polaris-workflow/record.json",
      "type": "application/json"
    },
    {
      "rel": "related",
      "href": "../../projects/cerulean-information-factory/collection.json",
      "type": "application/json",
      "title": "Project: Cerulean Information Factory"
    },
    {
      "rel": "child",
      "href": "../../experiments/polaris/record.json",
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
      "rel": "vcs",
      "title": "Git source repository",
      "href": "https://github.com/gtif-cerulean/polaris.git",
      "vcs:type": "git",
      "vcs:branch": "main"
    },
    {
      "rel": "application",
      "title": "POLARIS workflow",
      "href": "https://github.com/gtif-cerulean/polaris/blob/main/workflow.yml",
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
      "href": "https://harshness-map.gtif.eox.at/processes/execute-polaris",
      "type": "text/html",
      "title": "Trigger workflow via API provided by pygeoapi"
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
@prefix ns1: <application:> .
@prefix ns2: <http://www.iana.org/assignments/> .
@prefix ns3: <vcs:> .
@prefix ns4: <osc:> .
@prefix oa: <http://www.w3.org/ns/oa#> .
@prefix proc: <https://w3id.org/ogc/api/processes/> .
@prefix prov: <http://www.w3.org/ns/prov#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix rec: <https://www.opengis.net/def/ogc-api/records/> .
@prefix thns: <https://w3id.org/ogc/stac/themes/> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

<https://ogc.org/demo/ospd/polaris-workflow> ns1:container true ;
    ns1:language "Python" ;
    ns1:type "argo-workflow" ;
    dcterms:conformsTo <http://www.opengis.net/spec/ogcapi-records-1/1.0/req/record-core>,
        <https://raw.githubusercontent.com/EOEPCA/metadata-profile/refs/heads/1.0/schemas/application-type-argo-workflow>,
        <https://stac-extensions.github.io/application/v0.1.0/schema.json> ;
    dcterms:created "2025-02-19T23:00:00Z" ;
    dcterms:description "Polar Operational Limit Assessment Risk Index System (POLARIS) algorithm." ;
    dcterms:modified "2025-03-03T22:00:00Z" ;
    dcterms:title "POLARIS" ;
    rdfs:seeAlso [ rdfs:label "Git source repository" ;
            dcterms:type "application/json" ;
            ns2:relation <http://www.iana.org/assignments/relation/git> ;
            oa:hasTarget <https://github.com/gtif-cerulean/cerulean-catalog.git> ],
        [ rdfs:label "POLARIS workflow" ;
            ns1:container true ;
            ns1:language "Python" ;
            ns1:type "argo-workflow" ;
            <argo-workflow:> [ proc:requirements [ proc:temp_storage "10GB" ] ] ;
            dcterms:type "application/x-argo-workflow-yaml" ;
            ns2:relation <http://www.iana.org/assignments/relation/application> ;
            oa:hasTarget <https://github.com/gtif-cerulean/polaris/blob/main/workflow.yml> ],
        [ rdfs:label "Project: Cerulean Information Factory" ;
            dcterms:type "application/json" ;
            ns2:relation <http://www.iana.org/assignments/relation/related> ;
            oa:hasTarget <https://ogc.org/projects/cerulean-information-factory/collection.json> ],
        [ rdfs:label "Git source repository" ;
            ns2:relation <http://www.iana.org/assignments/relation/vcs> ;
            oa:hasTarget <https://github.com/gtif-cerulean/polaris.git> ;
            ns3:branch "main" ;
            ns3:type "git" ],
        [ rdfs:label "Open Science Catalog" ;
            dcterms:type "application/json" ;
            ns2:relation <http://www.iana.org/assignments/relation/root> ;
            oa:hasTarget <https://ogc.org/catalog.json> ],
        [ rdfs:label "Trigger workflow via API provided by pygeoapi" ;
            dcterms:type "text/html" ;
            ns2:relation <http://www.iana.org/assignments/relation/related> ;
            oa:hasTarget <https://harshness-map.gtif.eox.at/processes/execute-polaris> ],
        [ rdfs:label "OGC Application Package" ;
            dcterms:type "application/json" ;
            ns2:relation <http://www.iana.org/assignments/relation/application> ;
            oa:hasTarget <https://github.com/gtif-cerulean/cerulean-catalog.git> ],
        [ rdfs:label "Workflows" ;
            dcterms:type "application/json" ;
            ns2:relation <http://www.iana.org/assignments/relation/parent> ;
            oa:hasTarget <https://ogc.org/demo/catalog.json> ],
        [ rdfs:label "Theme: Oceans" ;
            dcterms:type "application/json" ;
            ns2:relation <http://www.iana.org/assignments/relation/related> ;
            oa:hasTarget <https://ogc.org/themes/oceans/catalog.json> ],
        [ rdfs:label "EOxHub Workspaces" ;
            ns1:platform_supports "argo-workflow" ;
            ns1:preferred_app "argo" ;
            dcterms:type "text/html" ;
            ns2:relation <http://www.iana.org/assignments/relation/application-originating-platform> ;
            oa:hasTarget <https://workspace.cif.hub-otc.eox.at/> ],
        [ dcterms:type "application/json" ;
            ns2:relation <http://www.iana.org/assignments/relation/self> ;
            oa:hasTarget <https://esa-earthcode.github.io/open-science-catalog-metadata/workflows/polaris-workflow/record.json> ],
        [ rdfs:label "POLARIS" ;
            dcterms:type "application/json" ;
            ns2:relation <http://www.iana.org/assignments/relation/child> ;
            oa:hasTarget <https://ogc.org/experiments/polaris/record.json> ] ;
    dcat:contactPoint [ rdfs:label "David Arthurs" ;
            proc:emails [ prov:value "david.arthurs@polarview.org" ] ;
            proc:roles "consortium_member" ],
        [ rdfs:label "Týna Doležalová" ;
            proc:emails [ prov:value "tyna.dolezalova@eox.at" ] ;
            proc:roles "consortium_member" ] ;
    dcat:keyword "polar",
        "sea ice" ;
    dcat:license "CC-BY-SA-4.0" ;
    proc:type "Feature",
        "workflow" ;
    rec:format [ rec:name "GeoTIFF" ] ;
    rec:themes [ thns:concepts [ thns:id "oceans"^^xsd:string ] ;
            thns:scheme "https://github.com/stac-extensions/osc#theme" ] ;
    ns4:project "cerulean-information-factory" .


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
        $ref: https://nsnarayanam.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/common/schema.yaml#/$defs/osc:project
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
      - $ref: https://nsnarayanam.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/common/schema.yaml#/$defs/via_links

```

Links to the schema:

* YAML version: [schema.yaml](https://nsnarayanam.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/workflows/schema.json)
* JSON version: [schema.json](https://nsnarayanam.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/workflows/schema.yaml)


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
    "type": "proc:type",
    "id": "@id",
    "properties": "@nest",
    "geometry": {
      "@context": {
        "type": "@type",
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
        "type": "dct:type",
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
        },
        "scheme": "thns:scheme"
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
        }
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
    "@vocab": "https://w3id.org/ogc/api/processes/",
    "maxOccurs": "proc:maxOccurs",
    "minOccurs": "proc:minOccurs",
    "schema": {
      "@context": {
        "@vocab": "https://w3id.org/ogc/api/schema/"
      },
      "@id": "proc:schema"
    },
    "nullable": "proc:nullable",
    "$ref": {
      "@id": "proc:ref",
      "@type": "@id"
    },
    "default": {
      "@id": "proc:default",
      "@type": "@json"
    },
    "enum": {
      "@id": "proc:enum",
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
    "proc": "https://w3id.org/ogc/api/processes/",
    "rights": "dcat:rights",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://nsnarayanam.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/workflows/context.jsonld)

## Sources

* [GeoDCAT Specification](http://www.opengis.net/def/metamodel/profiles/geodcat)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/nsnarayanam/bblocks-openscience](https://github.com/nsnarayanam/bblocks-openscience)
* Path: `_sources/geodcat-stac-earthcode/workflows`

