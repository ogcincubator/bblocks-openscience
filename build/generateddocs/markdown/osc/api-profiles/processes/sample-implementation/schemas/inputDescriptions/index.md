
# Example OGC API Processes instance input descriptions (Schema)

`ogc.osc.api-profiles.processes.sample-implementation.schemas.inputDescriptions` *v1.0*

Collection of input descriptions

[*Status*](http://www.opengis.net/def/status): Under development

## Schema

```yaml
anyOf:
- $ref: https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/api-profiles/processes/sample-implementation/schemas/buffer-geometry/inputDescription/schema.yaml

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/api-profiles/processes/sample-implementation/schemas/inputDescriptions/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/api-profiles/processes/sample-implementation/schemas/inputDescriptions/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "@vocab": "https://w3id.org/ogc/api/processes/",
    "maxOccurs": "proc:maxOccurs",
    "minOccurs": "proc:minOccurs",
    "schema": {
      "@context": {
        "@vocab": "https://w3id.org/ogc/api/schema/"
      },
      "@id": "proc:schema"
    },
    "title": "dct:title",
    "description": "dct:description",
    "keywords": "proc:keywords",
    "nullable": "proc:nullable",
    "type": "proc:type",
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
    "geometry": {
      "@context": {
        "schema": {
          "@context": {
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
            }
          }
        }
      }
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
    "dct": "http://purl.org/dc/terms/",
    "proc": "https://w3id.org/ogc/api/processes/",
    "geojson": "https://purl.org/geojson/vocab#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/api-profiles/processes/sample-implementation/schemas/inputDescriptions/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-openscience](https://github.com/ogcincubator/bblocks-openscience)
* Path: `_sources/api-profiles/processes/sample-implementation/schemas/inputDescriptions`

