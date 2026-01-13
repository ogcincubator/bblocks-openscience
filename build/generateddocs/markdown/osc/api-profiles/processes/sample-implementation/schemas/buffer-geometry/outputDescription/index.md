
# Buffer geometry process output description (Schema)

`ogc.osc.api-profiles.processes.sample-implementation.schemas.buffer-geometry.outputDescription` *v1.0*

Description for the output of the buffer geometry process

[*Status*](http://www.opengis.net/def/status): Under development

## Schema

```yaml
allOf:
- $ref: https://ogcincubator.github.io/bblocks-ogcapi-processes/build/annotated/api/processes/v1/schemas/outputDescription/schema.yaml
properties:
  schema:
    type: object
    properties:
      bufferedGeometry:
        type: object
        properties:
          title:
            type: string
            const: Buffered Geometry
          description:
            type: string
          schema:
            $ref: https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/api-profiles/processes/sample-implementation/schemas/buffer-geometry/outputSchema/schema.yaml#/properties/bufferedGeometry
      area:
        type: object
        properties:
          title:
            type: string
            const: Buffer Area
          description:
            type: string
          schema:
            $ref: https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/api-profiles/processes/sample-implementation/schemas/buffer-geometry/outputSchema/schema.yaml#/properties/area

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/api-profiles/processes/sample-implementation/schemas/buffer-geometry/outputDescription/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/api-profiles/processes/sample-implementation/schemas/buffer-geometry/outputDescription/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "@vocab": "https://w3id.org/ogc/api/processes/",
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
    "minOccurs": "proc:minOccurs",
    "maxOccurs": "proc:maxOccurs",
    "enum": {
      "@id": "proc:enum",
      "@container": "@set"
    },
    "dct": "http://purl.org/dc/terms/",
    "proc": "https://w3id.org/ogc/api/processes/",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/api-profiles/processes/sample-implementation/schemas/buffer-geometry/outputDescription/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-openscience](https://github.com/ogcincubator/bblocks-openscience)
* Path: `_sources/api-profiles/processes/sample-implementation/schemas/buffer-geometry/outputDescription`

