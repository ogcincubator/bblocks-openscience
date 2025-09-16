
# EarthCODE Product (Schema)

`ogc.osc.geodcat-stac-earthcode.products` *v0.1*

EarthCODE metadata profile linked to semantic models

[*Status*](http://www.opengis.net/def/status): Under development

## Description

## ESA EarthCODE experiments as GeoDCAT and STAC profile 

This building block shows a possible profile of GeoDCAT supporting semantic annotation and inclusion of the three STAC extensions used by EarthCODE:

- themes
- osc
- cf

## Examples

### An example demonstrating EarthCode Product as a STAC Collection.
#### json
```json
{
  "type": "Collection",
  "id": "ice-shelf-antarctica-cryosmos",
  "stac_version": "1.0.0",
  "description": "The ice shelf product consists of two types of NETCDF-4 files, one containing yearly mean quantities and one containing differential quantities as well as static surface type masks. Names of the first file type are \"SMOS_TB_for_Origin_yyyy_vvv.nc\", where \"yyyy\" is the respective year and \"vvv\" the dataset version. Names of the second file type are \"SMOS_Origin_yyyy_yyyy_vvv.nc\" where the first \"yyyy\" indicates the first year, the second \"yyyy\" the second year and \"vvv\" the dataset version. All differential quantities are based on the yearly mean of the second year minus the yearly mean of first year. Product details are available at: http://www.ifac.cnr.it/cryosmos/products/CryoSMOS_D8_EDUM_V2.0.pdf.",
  "links": [
    {
      "rel": "root",
      "href": "../../catalog.json",
      "type": "application/json",
      "title": "Open Science Catalog"
    },
    {
      "rel": "via",
      "href": "http://www.ifac.cnr.it/cryosmos/products/CRYOSMOS_shelf.tgz",
      "title": "Access"
    },
    {
      "rel": "parent",
      "href": "../catalog.json",
      "type": "application/json",
      "title": "Products"
    },
    {
      "rel": "related",
      "href": "../../projects/cryosmos/collection.json",
      "type": "application/json",
      "title": "Project: CryoSMOS"
    },
    {
      "rel": "related",
      "href": "../../themes/cryosphere/catalog.json",
      "type": "application/json",
      "title": "Theme: Cryosphere"
    },
    {
      "rel": "related",
      "href": "../../variables/ice-sheets-and-ice-shelves/catalog.json",
      "type": "application/json",
      "title": "Variable: Ice Sheets and Ice Shelves"
    },
    {
      "rel": "related",
      "href": "../../eo-missions/smos/catalog.json",
      "type": "application/json",
      "title": "EO Mission: SMOS"
    },
    {
      "rel": "self",
      "href": "https://esa-earthcode.github.io/open-science-catalog-metadata/products/ice-shelf-antarctica-cryosmos/collection.json",
      "type": "application/json"
    }
  ],
  "stac_extensions": [
    "https://stac-extensions.github.io/osc/v1.0.0/schema.json",
    "https://stac-extensions.github.io/themes/v1.0.0/schema.json",
    "https://stac-extensions.github.io/cf/v0.2.0/schema.json"
  ],
  "osc:project": "cryosmos",
  "osc:status": "ongoing",
  "osc:region": "Antarctica",
  "osc:type": "product",
  "created": "2020-03-19T00:00:00Z",
  "cf:parameter": [
    {
      "name": "ice_shelves"
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
    }
  ],
  "osc:variables": [
    "ice-sheets-and-ice-shelves"
  ],
  "osc:missions": [
    "smos"
  ],
  "updated": "2024-09-12T20:32:06.219108Z",
  "title": "Ice shelf product_Antarctica_SMOS",
  "extent": {
    "spatial": {
      "bbox": [
        [
          -180.0,
          -83.0,
          180.0,
          -60.0
        ]
      ]
    },
    "temporal": {
      "interval": [
        [
          "2013-01-01T00:00:00Z",
          "2014-12-31T23:59:59Z"
        ]
      ]
    }
  },
  "license": "proprietary",
  "keywords": [
    "Glaciers/Ice Sheets",
    "Ice Sheets and Ice Shelves",
    "Sea Ice"
  ]
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/products/context.jsonld",
  "type": "Collection",
  "id": "ice-shelf-antarctica-cryosmos",
  "stac_version": "1.0.0",
  "description": "The ice shelf product consists of two types of NETCDF-4 files, one containing yearly mean quantities and one containing differential quantities as well as static surface type masks. Names of the first file type are \"SMOS_TB_for_Origin_yyyy_vvv.nc\", where \"yyyy\" is the respective year and \"vvv\" the dataset version. Names of the second file type are \"SMOS_Origin_yyyy_yyyy_vvv.nc\" where the first \"yyyy\" indicates the first year, the second \"yyyy\" the second year and \"vvv\" the dataset version. All differential quantities are based on the yearly mean of the second year minus the yearly mean of first year. Product details are available at: http://www.ifac.cnr.it/cryosmos/products/CryoSMOS_D8_EDUM_V2.0.pdf.",
  "links": [
    {
      "rel": "root",
      "href": "../../catalog.json",
      "type": "application/json",
      "title": "Open Science Catalog"
    },
    {
      "rel": "via",
      "href": "http://www.ifac.cnr.it/cryosmos/products/CRYOSMOS_shelf.tgz",
      "title": "Access"
    },
    {
      "rel": "parent",
      "href": "../catalog.json",
      "type": "application/json",
      "title": "Products"
    },
    {
      "rel": "related",
      "href": "../../projects/cryosmos/collection.json",
      "type": "application/json",
      "title": "Project: CryoSMOS"
    },
    {
      "rel": "related",
      "href": "../../themes/cryosphere/catalog.json",
      "type": "application/json",
      "title": "Theme: Cryosphere"
    },
    {
      "rel": "related",
      "href": "../../variables/ice-sheets-and-ice-shelves/catalog.json",
      "type": "application/json",
      "title": "Variable: Ice Sheets and Ice Shelves"
    },
    {
      "rel": "related",
      "href": "../../eo-missions/smos/catalog.json",
      "type": "application/json",
      "title": "EO Mission: SMOS"
    },
    {
      "rel": "self",
      "href": "https://esa-earthcode.github.io/open-science-catalog-metadata/products/ice-shelf-antarctica-cryosmos/collection.json",
      "type": "application/json"
    }
  ],
  "stac_extensions": [
    "https://stac-extensions.github.io/osc/v1.0.0/schema.json",
    "https://stac-extensions.github.io/themes/v1.0.0/schema.json",
    "https://stac-extensions.github.io/cf/v0.2.0/schema.json"
  ],
  "osc:project": "cryosmos",
  "osc:status": "ongoing",
  "osc:region": "Antarctica",
  "osc:type": "product",
  "created": "2020-03-19T00:00:00Z",
  "cf:parameter": [
    {
      "name": "ice_shelves"
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
    }
  ],
  "osc:variables": [
    "ice-sheets-and-ice-shelves"
  ],
  "osc:missions": [
    "smos"
  ],
  "updated": "2024-09-12T20:32:06.219108Z",
  "title": "Ice shelf product_Antarctica_SMOS",
  "extent": {
    "spatial": {
      "bbox": [
        [
          -180.0,
          -83.0,
          180.0,
          -60.0
        ]
      ]
    },
    "temporal": {
      "interval": [
        [
          "2013-01-01T00:00:00Z",
          "2014-12-31T23:59:59Z"
        ]
      ]
    }
  },
  "license": "proprietary",
  "keywords": [
    "Glaciers/Ice Sheets",
    "Ice Sheets and Ice Shelves",
    "Sea Ice"
  ]
}
```

#### ttl
```ttl
@prefix dcterms: <http://purl.org/dc/terms/> .
@prefix ns1: <osc:> .
@prefix ns2: <http://www.iana.org/assignments/> .
@prefix ns3: <urn:stac:vocab#> .
@prefix ns4: <cf:> .
@prefix oa: <http://www.w3.org/ns/oa#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix thns: <https://w3id.org/ogc/stac/themes/> .

<https://ogc.org/demo/ospd/ice-shelf-antarctica-cryosmos> rdfs:label "Ice shelf product_Antarctica_SMOS" ;
    ns4:parameter [ ] ;
    dcterms:created "2020-03-19T00:00:00Z" ;
    dcterms:description "The ice shelf product consists of two types of NETCDF-4 files, one containing yearly mean quantities and one containing differential quantities as well as static surface type masks. Names of the first file type are \"SMOS_TB_for_Origin_yyyy_vvv.nc\", where \"yyyy\" is the respective year and \"vvv\" the dataset version. Names of the second file type are \"SMOS_Origin_yyyy_yyyy_vvv.nc\" where the first \"yyyy\" indicates the first year, the second \"yyyy\" the second year and \"vvv\" the dataset version. All differential quantities are based on the yearly mean of the second year minus the yearly mean of first year. Product details are available at: http://www.ifac.cnr.it/cryosmos/products/CryoSMOS_D8_EDUM_V2.0.pdf." ;
    dcterms:extent [ ] ;
    dcterms:license "proprietary" ;
    dcterms:modified "2024-09-12T20:32:06.219108Z" ;
    dcterms:subject "Glaciers/Ice Sheets",
        "Ice Sheets and Ice Shelves",
        "Sea Ice" ;
    dcterms:type "Collection" ;
    rdfs:seeAlso [ rdfs:label "Theme: Cryosphere" ;
            dcterms:type "application/json" ;
            ns2:relation <http://www.iana.org/assignments/relation/related> ;
            oa:hasTarget <https://ogc.org/themes/cryosphere/catalog.json> ],
        [ rdfs:label "Access" ;
            ns2:relation <http://www.iana.org/assignments/relation/via> ;
            oa:hasTarget <http://www.ifac.cnr.it/cryosmos/products/CRYOSMOS_shelf.tgz> ],
        [ rdfs:label "Variable: Ice Sheets and Ice Shelves" ;
            dcterms:type "application/json" ;
            ns2:relation <http://www.iana.org/assignments/relation/related> ;
            oa:hasTarget <https://ogc.org/variables/ice-sheets-and-ice-shelves/catalog.json> ],
        [ rdfs:label "Products" ;
            dcterms:type "application/json" ;
            ns2:relation <http://www.iana.org/assignments/relation/parent> ;
            oa:hasTarget <https://ogc.org/demo/catalog.json> ],
        [ rdfs:label "EO Mission: SMOS" ;
            dcterms:type "application/json" ;
            ns2:relation <http://www.iana.org/assignments/relation/related> ;
            oa:hasTarget <https://ogc.org/eo-missions/smos/catalog.json> ],
        [ rdfs:label "Open Science Catalog" ;
            dcterms:type "application/json" ;
            ns2:relation <http://www.iana.org/assignments/relation/root> ;
            oa:hasTarget <https://ogc.org/catalog.json> ],
        [ rdfs:label "Project: CryoSMOS" ;
            dcterms:type "application/json" ;
            ns2:relation <http://www.iana.org/assignments/relation/related> ;
            oa:hasTarget <https://ogc.org/projects/cryosmos/collection.json> ],
        [ dcterms:type "application/json" ;
            ns2:relation <http://www.iana.org/assignments/relation/self> ;
            oa:hasTarget <https://esa-earthcode.github.io/open-science-catalog-metadata/products/ice-shelf-antarctica-cryosmos/collection.json> ] ;
    thns:schemes [ thns:concepts [ thns:id "cryosphere" ] ;
            thns:scheme "https://github.com/stac-extensions/osc#theme" ] ;
    ns1:missions "smos" ;
    ns1:project "cryosmos" ;
    ns1:region "Antarctica" ;
    ns1:status "ongoing" ;
    ns1:type "product" ;
    ns1:variables "ice-sheets-and-ice-shelves" ;
    ns3:extensions "https://stac-extensions.github.io/cf/v0.2.0/schema.json",
        "https://stac-extensions.github.io/osc/v1.0.0/schema.json",
        "https://stac-extensions.github.io/themes/v1.0.0/schema.json" ;
    ns3:version "1.0.0" .


```

## Schema

```yaml
$schema: https://json-schema.org/draft/2020-12/schema
description: Schema for OGCAPI records profile for GeoDCAT - defines all extra elements
  defined by GeoDCAT so that the JSON-LD context can map to GeoDCAT RDF
allOf:
- $ref: https://ogcincubator.github.io/bblocks-stac/build/annotated/contrib/stac/extensions/themes/schema.yaml
- $ref: https://ogcincubator.github.io/bblocks-stac/build/annotated/contrib/stac/extensions/osc/schema.yaml
- $ref: https://ogcincubator.github.io/bblocks-stac/build/annotated/contrib/stac/extensions/cf/schema.yaml
- anyOf:
  - $ref: https://ogcincubator.github.io/geodcat-ogcapi-records/build/annotated/geo/geodcat/stac/geodcat-stac-collection/schema.yaml

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/products/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/products/schema.yaml)


# JSON-LD Context

```jsonld
{
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
    "length": "dct:extent",
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
    "links": "rdfs:seeAlso",
    "coordinates": {
      "@container": "@list",
      "@id": "geojson:coordinates"
    },
    "created": "dct:created",
    "updated": "dct:modified",
    "uriTemplate": {
      "@type": "xsd:string",
      "@id": "oa:hasTarget"
    },
    "description": "dct:description",
    "license": "dct:license",
    "extent": "dct:extent",
    "datetime": {
      "@id": "stac:datetime",
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
    "assets": {
      "@id": "urn:stac:vocab#hasAsset",
      "@container": "@id",
      "@context": {
        "href": {
          "@id": "dcat:downloadURL",
          "@type": "@id"
        },
        "title": "dct:title",
        "type": "dct:format"
      }
    },
    "media_type": "stac:mediaType",
    "themes": {
      "@id": "thns:schemes",
      "@container": "@set"
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
    "stac_version": "urn:stac:vocab#version",
    "stac_extensions": "urn:stac:vocab#extensions",
    "keywords": "dct:subject",
    "oa": "http://www.w3.org/ns/oa#",
    "rdfs": "http://www.w3.org/2000/01/rdf-schema#",
    "dct": "http://purl.org/dc/terms/",
    "thns": "https://w3id.org/ogc/stac/themes/",
    "geojson": "https://purl.org/geojson/vocab#",
    "stac": "http://stacspec.org/ontology/core#",
    "geo": "http://www.opengis.net/ont/geosparql#",
    "prov": "http://www.w3.org/ns/prov#",
    "xsd": "http://www.w3.org/2001/XMLSchema#",
    "dcat": "http://www.w3.org/ns/dcat#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/geodcat-stac-earthcode/products/context.jsonld)

## Sources

* [GeoDCAT Specification](http://www.opengis.net/def/metamodel/profiles/geodcat)
* [EarthCODE]({
      "title": "GeoDCAT Specification",
      "link": "http://www.opengis.net/def/metamodel/profiles/geodcat"
    },)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-openscience](https://github.com/ogcincubator/bblocks-openscience)
* Path: `_sources/geodcat-stac-earthcode/products`

