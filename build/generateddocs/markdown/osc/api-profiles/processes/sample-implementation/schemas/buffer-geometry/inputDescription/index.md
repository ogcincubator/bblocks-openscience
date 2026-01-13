
# Buffer geometry process input description (Schema)

`ogc.osc.api-profiles.processes.sample-implementation.schemas.buffer-geometry.inputDescription` *v1.0*

Description for the inputs of the buffer geometry process

[*Status*](http://www.opengis.net/def/status): Under development

## Schema

```yaml
allOf:
- $ref: https://ogcincubator.github.io/bblocks-ogcapi-processes/build/annotated/api/processes/v1/schemas/inputDescription/schema.yaml
type: object
properties:
  geometry:
    type: object
    properties:
      title:
        type: string
        const: Area for the buffer geometry
      minOccurs:
        type: integer
        const: 1
      maxOccurs:
        type: integer
        const: 1
      schema:
        $ref: https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/api-profiles/processes/sample-implementation/schemas/buffer-geometry/inputSchema/schema.yaml#/properties/geometry
  distance:
    type: object
    properties:
      title:
        type: string
        const: Buffer Distance
      description:
        type: string
        const: The distance from the geometry to create the buffer
      minOccurs:
        type: integer
        const: 1
      maxOccurs:
        type: integer
        const: 1
      schema:
        $ref: https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/api-profiles/processes/sample-implementation/schemas/buffer-geometry/inputSchema/schema.yaml#/properties/distance
  units:
    type: object
    properties:
      title:
        type: string
        example: Distance Units
      description:
        type: string
      minOccurs:
        type: integer
        const: 0
      maxOccurs:
        type: integer
        const: 1
      schema:
        $ref: https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/api-profiles/processes/sample-implementation/schemas/buffer-geometry/inputSchema/schema.yaml#/properties/units

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/api-profiles/processes/sample-implementation/schemas/buffer-geometry/inputDescription/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/api-profiles/processes/sample-implementation/schemas/buffer-geometry/inputDescription/schema.yaml)


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
    "dct": "http://purl.org/dc/terms/",
    "proc": "https://w3id.org/ogc/api/processes/",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/api-profiles/processes/sample-implementation/schemas/buffer-geometry/inputDescription/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-openscience](https://github.com/ogcincubator/bblocks-openscience)
* Path: `_sources/api-profiles/processes/sample-implementation/schemas/buffer-geometry/inputDescription`

