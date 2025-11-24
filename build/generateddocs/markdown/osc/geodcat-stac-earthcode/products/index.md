
# EarthCODE Product (Schema)

`ogc.osc.geodcat-stac-earthcode.products` *v0.1*

EarthCODE metadata profile linked to semantic models

[*Status*](http://www.opengis.net/def/status): Under development

## Description

## ESA EarthCODE Products as GeoDCAT and STAC profile 

This building block represents the outputs of an EarthCODE Experiment.

This is a STAC Collection using the themes, osc and cf extensions with some additional EarthCODE-specific fields.

The EarthCODE OSC has requirements which are not captured here

  - A list of conceps following the OSC theme scheme must be present using the themes extension
  - Each theme ID must match the ID of a Catalog at /themes/theme-id/catalog.json
  - A 'related' link must exists in `links` also pointing to the theme Catalog
  - The osc:project, osc:variables, osc:missions and osc:experiment fields should contain the IDs of catalogue entries found at /projects/{id}/collection.json, /variables/{id}/catalog.json, /missions/{id}/catalog.json or /experiments/{id}/record.json repsectively.

## Examples

### Polarwarp
#### json
```json
{
  "id": "polarwarp",
  "title": "Polarwarp",
  "created": "2025-10-13T16:54:34Z",
  "osc:status": "completed",
  "type": "Collection",
  "osc:type": "product",
  "stac_version": "1.0.0",
  "description": "Polarwarp product\n\nForecast rasters (+1h … +6h) produced by the Polarwarp workflow using NEXTSIM model and S1 scenes.",
  "license": "various",
  "extent": {
    "spatial": {
      "bbox": [
        [
          -0.0018099989187332413,
          0.00043814539682784925,
          0.001347252506956414,
          0.0007574196581714432
        ]
      ]
    },
    "temporal": {
      "interval": [
        [
          "2025-02-25T00:00:00Z",
          null
        ]
      ]
    }
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
      "title": "Products"
    },
    {
      "href": "../../projects/cerulean-information-factory/collection.json",
      "rel": "related",
      "type": "application/json",
      "title": "Project: Cerulean Information Factory"
    },
    {
      "href": "../../themes/cryosphere/catalog.json",
      "rel": "related",
      "type": "application/json",
      "title": "Theme: Cryosphere"
    },
    {
      "rel": "related",
      "href": "../../experiments/polarwarp/record.json",
      "type": "application/json",
      "title": "Experiment: Polarwarp"
    },
    {
      "href": "./item.json",
      "rel": "item"
    },
    {
      "href": "https://github.com/gtif-cerulean/polarwarp",
      "rel": "via"
    }
  ],
  "stac_extensions": [
    "https://stac-extensions.github.io/osc/v1.0.0/schema.json",
    "https://stac-extensions.github.io/themes/v1.0.0/schema.json"
  ],
  "osc:project": "cerulean-information-factory",
  "themes": [
    {
      "scheme": "https://github.com/stac-extensions/osc#theme",
      "concepts": [
        {
          "id": "cryosphere"
        }
      ]
    }
  ]
}

```

#### jsonld
```jsonld
{
  "@context": "https://ahaywardtvuk.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/products/context.jsonld",
  "id": "polarwarp",
  "title": "Polarwarp",
  "created": "2025-10-13T16:54:34Z",
  "osc:status": "completed",
  "type": "Collection",
  "osc:type": "product",
  "stac_version": "1.0.0",
  "description": "Polarwarp product\n\nForecast rasters (+1h \u2026 +6h) produced by the Polarwarp workflow using NEXTSIM model and S1 scenes.",
  "license": "various",
  "extent": {
    "spatial": {
      "bbox": [
        [
          -0.0018099989187332413,
          0.00043814539682784925,
          0.001347252506956414,
          0.0007574196581714432
        ]
      ]
    },
    "temporal": {
      "interval": [
        [
          "2025-02-25T00:00:00Z",
          null
        ]
      ]
    }
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
      "title": "Products"
    },
    {
      "href": "../../projects/cerulean-information-factory/collection.json",
      "rel": "related",
      "type": "application/json",
      "title": "Project: Cerulean Information Factory"
    },
    {
      "href": "../../themes/cryosphere/catalog.json",
      "rel": "related",
      "type": "application/json",
      "title": "Theme: Cryosphere"
    },
    {
      "rel": "related",
      "href": "../../experiments/polarwarp/record.json",
      "type": "application/json",
      "title": "Experiment: Polarwarp"
    },
    {
      "href": "./item.json",
      "rel": "item"
    },
    {
      "href": "https://github.com/gtif-cerulean/polarwarp",
      "rel": "via"
    }
  ],
  "stac_extensions": [
    "https://stac-extensions.github.io/osc/v1.0.0/schema.json",
    "https://stac-extensions.github.io/themes/v1.0.0/schema.json"
  ],
  "osc:project": "cerulean-information-factory",
  "themes": [
    {
      "scheme": "https://github.com/stac-extensions/osc#theme",
      "concepts": [
        {
          "id": "cryosphere"
        }
      ]
    }
  ]
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
@prefix stac: <https://w3id.org/ogc/stac/core/> .
@prefix thns: <https://w3id.org/ogc/stac/themes/> .

<https://ogc.org/demo/ospd/polarwarp> a <https://ogc.org/demo/ospd/Collection> ;
    dcterms:created "2025-10-13T16:54:34Z" ;
    dcterms:description """Polarwarp product

Forecast rasters (+1h … +6h) produced by the Polarwarp workflow using NEXTSIM model and S1 scenes.""" ;
    dcterms:extent [ ] ;
    dcterms:title "Polarwarp" ;
    rdfs:seeAlso [ rdfs:label "Products" ;
            dcterms:format "application/json" ;
            ns2:relation <http://www.iana.org/assignments/relation/parent> ;
            oa:hasTarget <https://ogc.org/demo/catalog.json> ],
        [ ns2:relation <http://www.iana.org/assignments/relation/item> ;
            oa:hasTarget <https://ogc.org/demo/ospd/item.json> ],
        [ ns2:relation <http://www.iana.org/assignments/relation/via> ;
            oa:hasTarget <https://github.com/gtif-cerulean/polarwarp> ],
        [ rdfs:label "Project: Cerulean Information Factory" ;
            dcterms:format "application/json" ;
            ns2:relation <http://www.iana.org/assignments/relation/related> ;
            oa:hasTarget <https://ogc.org/projects/cerulean-information-factory/collection.json> ],
        [ rdfs:label "Experiment: Polarwarp" ;
            dcterms:format "application/json" ;
            ns2:relation <http://www.iana.org/assignments/relation/related> ;
            oa:hasTarget <https://ogc.org/experiments/polarwarp/record.json> ],
        [ rdfs:label "Theme: Cryosphere" ;
            dcterms:format "application/json" ;
            ns2:relation <http://www.iana.org/assignments/relation/related> ;
            oa:hasTarget <https://ogc.org/themes/cryosphere/catalog.json> ],
        [ rdfs:label "Open Science Catalog" ;
            dcterms:format "application/json" ;
            ns2:relation <http://www.iana.org/assignments/relation/root> ;
            oa:hasTarget <https://ogc.org/catalog.json> ] ;
    dcat:license "various" ;
    stac:hasExtension "https://stac-extensions.github.io/osc/v1.0.0/schema.json",
        "https://stac-extensions.github.io/themes/v1.0.0/schema.json" ;
    stac:version "1.0.0" ;
    rec:themes [ thns:concepts [ thns:id "cryosphere" ] ;
            thns:scheme "https://github.com/stac-extensions/osc#theme" ] ;
    ns1:project "cerulean-information-factory" ;
    ns1:status "completed" ;
    ns1:type "product" .


```

## Schema

```yaml
$schema: https://json-schema.org/draft/2020-12/schema
description: EarthCode Product
allOf:
- $ref: https://ahaywardtvuk.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/common/schema.yaml
- anyOf:
  - $ref: https://ogcincubator.github.io/bblocks-stac/build/annotated/contrib/stac/extensions/cf/schema.yaml
  - not:
      properties:
        stac_extensions:
          type: array
          contains:
            const: https://stac-extensions.github.io/cf/v0.2.0/schema.json
properties:
  osc:type:
    type: string
    enum:
    - product
  type:
    const: Collection

```

Links to the schema:

* YAML version: [schema.yaml](https://ahaywardtvuk.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/products/schema.json)
* JSON version: [schema.json](https://ahaywardtvuk.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/products/schema.yaml)


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
    "links": {
      "@context": {
        "type": "dct:format",
        "title": "rdfs:label"
      },
      "@id": "rdfs:seeAlso"
    },
    "conformsTo": {
      "@container": "@set",
      "@id": "dct:conformsTo",
      "@type": "@id"
    },
    "time": "dct:temporal",
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
        "type": "dct:type",
        "title": "rdfs:label"
      },
      "@container": "@set",
      "@id": "dcat:contactPoint",
      "@type": "@id"
    },
    "license": "dcat:license",
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
    "accessrights": "dct:accessRights",
    "variables": {
      "@container": "@id",
      "@id": "rec:hasVariable",
      "@context": {
        "@base": "http://example.com/variables/",
        "@vocab": "https://www.opengis.net/def/ogc-api/records/"
      }
    },
    "stac_version": "stac:version",
    "stac_extensions": "stac:hasExtension",
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
    "datetime": {
      "@id": "dct:date",
      "@type": "xsd:dateTime"
    },
    "extent": "dct:extent",
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
    "name": "cf:name",
    "unit": {
      "@id": "qudt:hasUnit",
      "@context": {
        "@base": "http://qudt.org/vocab/unit/"
      }
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
    "stac": "https://w3id.org/ogc/stac/core/",
    "thns": "https://w3id.org/ogc/stac/themes/",
    "cf": "https://w3id.org/ogc/stac/cf/",
    "qudt": "http://qudt.org/schema/qudt/",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ahaywardtvuk.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/products/context.jsonld)

## Sources

* [GeoDCAT Specification](http://www.opengis.net/def/metamodel/profiles/geodcat)
* [EarthCODE]({
      "title": "GeoDCAT Specification",
      "link": "http://www.opengis.net/def/metamodel/profiles/geodcat"
    },)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ahaywardtvuk/bblocks-openscience](https://github.com/ahaywardtvuk/bblocks-openscience)
* Path: `_sources/geodcat-stac-earthcode/products`

