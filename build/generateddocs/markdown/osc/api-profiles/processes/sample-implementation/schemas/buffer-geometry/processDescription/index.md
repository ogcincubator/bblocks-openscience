
# Buffer geometry process description (Schema)

`ogc.osc.api-profiles.processes.sample-implementation.schemas.buffer-geometry.processDescription` *v1.0*

Description of the buffer geometry process

[*Status*](http://www.opengis.net/def/status): Under development

## Schema

```yaml
allOf:
- $ref: https://ogcincubator.github.io/bblocks-ogcapi-processes/build/annotated/api/processes/v1/schemas/process/schema.yaml
- properties:
    inputs:
      $ref: https://raw.githubusercontent.com/nsnarayanam/bblocks-openscience/undefined/build/annotated/osc/api-profiles/processes/sample-implementation/schemas/buffer-geometry/inputDescription/schema.yaml
      additionalProperties: false
    outputs:
      $ref: https://raw.githubusercontent.com/nsnarayanam/bblocks-openscience/undefined/build/annotated/osc/api-profiles/processes/sample-implementation/schemas/buffer-geometry/outputDescription/schema.yaml
      additionalProperties: false

```

Links to the schema:

* YAML version: [schema.yaml](https://raw.githubusercontent.com/nsnarayanam/bblocks-openscience/undefined/build/annotated/osc/api-profiles/processes/sample-implementation/schemas/buffer-geometry/processDescription/schema.json)
* JSON version: [schema.json](https://raw.githubusercontent.com/nsnarayanam/bblocks-openscience/undefined/build/annotated/osc/api-profiles/processes/sample-implementation/schemas/buffer-geometry/processDescription/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
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
    "minOccurs": "proc:minOccurs",
    "maxOccurs": "proc:maxOccurs",
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
[context.jsonld](https://raw.githubusercontent.com/nsnarayanam/bblocks-openscience/undefined/build/annotated/osc/api-profiles/processes/sample-implementation/schemas/buffer-geometry/processDescription/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/nsnarayanam/bblocks-openscience](https://github.com/nsnarayanam/bblocks-openscience)
* Path: `_sources/api-profiles/processes/sample-implementation/schemas/buffer-geometry/processDescription`

