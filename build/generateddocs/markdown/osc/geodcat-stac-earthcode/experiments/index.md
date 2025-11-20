
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

<https://ogc.org/demo/ospd/polaris-experiment> a <https://ogc.org/demo/ospd/experiment>,
        geojson:Feature ;
    dcterms:conformsTo <http://www.opengis.net/spec/ogcapi-records-1/1.0/req/record-core> ;
    dcterms:created "2025-02-19T23:00:00Z" ;
    dcterms:description "Polar Operational Limit Assessment Risk Index System (POLARIS)" ;
    dcterms:modified "2025-02-19T23:00:00Z" ;
    dcterms:title "POLARIS" ;
    rdfs:seeAlso [ rdfs:label "Open Science Catalog" ;
            dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/root> ;
            oa:hasTarget <https://ogc.org/catalog.json> ],
        [ rdfs:label "Input parameters" ;
            dcterms:type "application/yaml" ;
            ns1:relation <http://www.iana.org/assignments/relation/input> ;
            oa:hasTarget <https://ogc.org/demo/ospd/input.yaml> ],
        [ rdfs:label "Workflow: POLARIS" ;
            dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/related> ;
            oa:hasTarget <https://ogc.org/workflows/polaris-workflow/record.json> ],
        [ rdfs:label "Theme: Oceans" ;
            dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/related> ;
            oa:hasTarget <https://ogc.org/themes/oceans/catalog.json> ],
        [ rdfs:label "Experiments" ;
            dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/parent> ;
            oa:hasTarget <https://ogc.org/demo/catalog.json> ],
        [ rdfs:label "Execution environment" ;
            dcterms:type "application/yaml" ;
            ns1:relation <http://www.iana.org/assignments/relation/environment> ;
            oa:hasTarget <https://ogc.org/demo/ospd/environment.yaml> ],
        [ rdfs:label "POLARIS" ;
            dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/child> ;
            oa:hasTarget <https://ogc.org/products/polaris/collection.json> ],
        [ dcterms:type "application/json" ;
            ns1:relation <http://www.iana.org/assignments/relation/self> ;
            oa:hasTarget <https://esa-earthcode.github.io/open-science-catalog-metadata/experiments/polaris-experiment/item.json> ] ;
    dcat:contactPoint [ rdfs:label "EarthCODE Demo" ;
            rdfs:seeAlso [ dcterms:type "text/html" ;
                    ns1:relation <http://www.iana.org/assignments/relation/about> ;
                    oa:hasTarget <https://opensciencedata.esa.int/> ] ] ;
    dcat:keyword "polar",
        "sea ice" ;
    dcat:license "CC-BY-SA-4.0" ;
    rec:format [ rdfs:label "GeoTIFF" ] ;
    rec:themes [ thns:concepts [ thns:id "oceans" ] ;
            thns:scheme "https://github.com/stac-extensions/osc#theme" ] ;
    ns2:workflow "polaris-workflow" .


```

## Schema

```yaml
$schema: https://json-schema.org/draft/2020-12/schema
description: EarthCode Experiment
allOf:
- $ref: https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/common/schema.yaml

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/experiments/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/experiments/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "stac_version": "stac:version",
    "stac_extensions": "stac:hasExtension",
    "type": "@type",
    "id": "@id",
    "extent": "dct:extent",
    "assets": {
      "@context": {
        "type": "dct:format",
        "roles": {
          "@id": "stac:roles",
          "@container": "@set"
        },
        "thumbnail": "stac:thumbnail",
        "overview": "stac:overview",
        "data": "stac:data",
        "metadata": "stac:metadata"
      },
      "@id": "stac:assets",
      "@container": "@id"
    },
    "title": {
      "@id": "dct:title",
      "@container": "@set"
    },
    "description": {
      "@id": "dct:description",
      "@container": "@set"
    },
    "links": {
      "@context": {
        "type": "dct:type",
        "title": "rdfs:label"
      },
      "@id": "rdfs:seeAlso"
    },
    "keywords": {
      "@id": "dcat:keyword",
      "@container": "@set"
    },
    "license": "dcat:license",
    "datetime": {
      "@id": "dct:date",
      "@type": "xsd:dateTime"
    },
    "start_datetime": {
      "@id": "stac:start_datetime",
      "@type": "xsd:dateTime"
    },
    "end_datetime": {
      "@id": "stac:end_datetime",
      "@type": "xsd:dateTime"
    },
    "providers": "stac:hasProvider",
    "media_type": "dct:format",
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
    "properties": "@nest",
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
    "conformsTo": {
      "@container": "@set",
      "@id": "dct:conformsTo",
      "@type": "@id"
    },
    "time": "dct:temporal",
    "created": "dct:created",
    "updated": "dct:modified",
    "language": "rec:language",
    "languages": {
      "@container": "@set",
      "@id": "rec:languages"
    },
    "resourceLanguages": {
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
      "@container": "@set",
      "@id": "rec:themes"
    },
    "formats": {
      "@container": "@set",
      "@id": "rec:format",
      "@type": "@id"
    },
    "contacts": {
      "@context": {
        "type": "dct:type",
        "title": "rdfs:label"
      },
      "@container": "@set",
      "@id": "dcat:contactPoint",
      "@type": "@id"
    },
    "rights": "dcat:rights",
    "linkTemplates": {
      "@context": {
        "type": "dct:format",
        "title": "rdfs:label",
        "uriTemplate": {
          "@type": "xsd:string",
          "@id": "rec:uriTemplate"
        },
        "varBase": "rec:varBase",
        "variables": {
          "@id": "rec:hasVariable",
          "@container": "@index",
          "@index": "dct:identifier",
          "@type": "@json"
        }
      },
      "@id": "rec:hasLinkTemplate"
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
    "length": "dct:extent",
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
    "name": "rdfs:label",
    "unit": {
      "@id": "qudt:hasUnit",
      "@context": {
        "@base": "http://qudt.org/vocab/unit/"
      }
    },
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
        "title": "rdfs:label"
      },
      "@id": "prov:wasInfluencedBy",
      "@type": "@id"
    },
    "qualifiedInfluence": {
      "@context": {
        "influencer": {
          "@context": {
            "type": "dct:type",
            "title": "rdfs:label"
          },
          "@id": "prov:influencer",
          "@type": "@id"
        },
        "activity": {
          "@context": {
            "wasAssociatedWith": {
              "@context": {
                "type": "dct:type",
                "title": "rdfs:label"
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
            "type": "dct:type",
            "title": "rdfs:label"
          },
          "@id": "prov:agent",
          "@type": "@id"
        }
      },
      "@id": "prov:qualifiedInfluence",
      "@type": "@id"
    },
    "provType": "@type",
    "hadMember": {
      "@id": "prov:hadMember",
      "@type": "@id"
    },
    "featureType": "@type",
    "entityType": "@type",
    "has_provenance": {
      "@context": {
        "wasAssociatedWith": {
          "@id": "prov:wasAssociatedWith",
          "@type": "@id",
          "@context": {
            "type": "dct:type",
            "title": "rdfs:label"
          }
        }
      },
      "@id": "dct:provenance",
      "@type": "@id"
    },
    "wasGeneratedBy": {
      "@context": {
        "wasAssociatedWith": {
          "@context": {
            "type": "dct:type",
            "title": "rdfs:label"
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
        "type": "dct:type",
        "title": "rdfs:label"
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
        "wasAssociatedWith": {
          "@context": {
            "type": "dct:type",
            "title": "rdfs:label"
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
            "wasAssociatedWith": {
              "@context": {
                "type": "dct:type",
                "title": "rdfs:label"
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
    "stac": "https://w3id.org/ogc/stac/core/",
    "dct": "http://purl.org/dc/terms/",
    "rdfs": "http://www.w3.org/2000/01/rdf-schema#",
    "oa": "http://www.w3.org/ns/oa#",
    "thns": "https://w3id.org/ogc/stac/themes/",
    "geojson": "https://purl.org/geojson/vocab#",
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
    "cf": "https://w3id.org/ogc/stac/cf/",
    "qudt": "http://qudt.org/schema/qudt/",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/experiments/context.jsonld)

## Sources

* [GeoDCAT Specification](http://www.opengis.net/def/metamodel/profiles/geodcat)
* [EarthCODE]({
      "title": "GeoDCAT Specification",
      "link": "http://www.opengis.net/def/metamodel/profiles/geodcat"
    },)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-openscience](https://github.com/ogcincubator/bblocks-openscience)
* Path: `_sources/geodcat-stac-earthcode/experiments`

