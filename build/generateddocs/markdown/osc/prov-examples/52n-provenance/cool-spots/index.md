
# Cool Spot Workflow Provenance Profile (Schema)

`ogc.osc.prov-examples.52n-provenance.cool-spots` *v0.1*

Cool Spot Workflow Provenance Profile.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

## Cool Spot Workflow Provenance Profile

This Building Block contains the provenance description of a cool spot analysis workflow developed as part of the [VelocityAdapt](https://velocityadapt.de/) project and profiled within the [Open Science Persitent Demonstrator 2026](https://www.ogc.org/de/initiatives/open-science-persistent-demonstrator-2026/) initiative.

The provenance representation follows [W3C PROV](https://www.w3.org/TR/prov-overview/), to be more specific its JSON schema as defined in the [Provenance Chain](https://ogcincubator.github.io/bblock-prov-schema/bblock/ogc.ogc-utils.prov) Building Block.

### Conformance to the Workflow Provenance Graph profile

This block profiles the [Workflow Provenance Graph](bblock://ogc.osc.prov-profiles.workflow-graph),
so every activity must be a [Registered Processing Step](bblock://ogc.osc.prov-profiles.processing-step):
its `activityType` must give a process type, from a governed register, more specific than `prov:Activity`, and it must have an output.
Each node gives its PROV class in `provType` (`Entity`, `Activity`, `Agent`), and `entityType`,
`activityType` and `agentType` carry only the specific types. Steps not yet mapped to a registered
process type use local CURIEs derived from their names (`ex:defineInputs`, `ex:geocodeCity`,
`ex:acquireData`, `ex:exportOutputs`); the schema accepts these, but mapping them to registered
process types is still to be done.

The workflow run, its plan and its runner are typed with the generic workflow classes of the
[activity type register profile](https://w3id.org/ogc/rim/activity-type/): `ex:workflowRun` is an
`acttype:WorkflowRun`, `ex:coolSpotsScript` an `acttype:WorkflowPlan` and `ex:gisPipelineEngine` an
`acttype:WorkflowRunner`.

The workflow run reports its own inputs and output by reference only: it uses the inputs of
each step that no other step generated, and generates the output of the last step (`ex:finalOutputPackage`, whose members are the exported files).
The example conforms; the SHACL shapes warn only that `ex:act1_defineInputs`, which creates the
process inputs from parameters, uses no entity.

## Examples

### Example from a cool spot workflow run from the VelocityAdapt project
#### json
```json
[
  {
    "id": "ex:processInputs",
    "provType": "Entity",
    "entityType": "ex:WorkflowInputs",
    "rdfs:label": "Workflow Parameters",
    "ex:location": "Münster, Germany",
    "ex:osmTags": "landuse=forest, natural=wood, leisure=park",
    "ex:minArea": 200,
    "ex:distance": 300,
    "ex:bufferIntervals": [
      0,
      75,
      150,
      225,
      300
    ],
    "generatedAtTime": "2026-07-13T17:43:40+02:00",
    "wasGeneratedBy": "ex:act1_defineInputs",
    "wasAttributedTo": "https://orcid.org/0000-0003-4718-2959"
  },
  {
    "id": "ex:openStreetMap",
    "provType": "Entity",
    "entityType": "prov:PrimarySource",
    "rdfs:label": "OpenStreetMap",
    "schema:url": "https://www.openstreetmap.org",
    "dcterms:license": "https://opendatacommons.org/licenses/odbl/1-0/"
  },
  {
    "id": "ex:nominatimApi",
    "provType": "Entity",
    "entityType": "schema:WebAPI",
    "rdfs:label": "Nominatim geocoding API",
    "schema:url": "https://nominatim.openstreetmap.org/"
  },
  {
    "id": "ex:overpassApi",
    "provType": "Entity",
    "entityType": "schema:WebAPI",
    "rdfs:label": "Overpass API",
    "schema:url": "https://overpass-api.de/api",
    "schema:softwareVersion": "0.7.62.11 87bfad18"
  },
  {
    "id": "ex:cityBoundary",
    "provType": "Entity",
    "entityType": "ex:VectorDataset",
    "rdfs:label": "Münster city boundary (EPSG:4326)",
    "ex:crs": "EPSG:4326",
    "hadPrimarySource": "ex:openStreetMap",
    "generatedAtTime": "2026-07-13T17:43:41.9+02:00",
    "wasGeneratedBy": "ex:act2a_geocodeCity"
  },
  {
    "id": "ex:rawOsmData",
    "provType": "Entity",
    "entityType": "ex:OsmDataset",
    "rdfs:label": "Raw OSM vector data (EPSG:4326)",
    "ex:crs": "EPSG:4326",
    "ex:osmBaseTimestamp": "2026-07-13T13:54:30Z",
    "dcterms:license": "https://opendatacommons.org/licenses/odbl/1-0/",
    "hadPrimarySource": "ex:openStreetMap",
    "generatedAtTime": "2026-07-13T17:44:05.8+02:00",
    "wasGeneratedBy": "ex:act2_acquireData"
  },
  {
    "id": "ex:reprojectedData",
    "provType": "Entity",
    "entityType": "ex:VectorDataset",
    "rdfs:label": "UTM Projected OSM data",
    "ex:crs": "EPSG:32632",
    "wasDerivedFrom": "ex:rawOsmData",
    "generatedAtTime": "2026-07-13T17:44:06.4+02:00",
    "wasGeneratedBy": "ex:act3_reproject"
  },
  {
    "id": "ex:filteredCoolSpots",
    "provType": "Entity",
    "entityType": "ex:VectorDataset",
    "rdfs:label": "Cool spots filtered by min area (>=200m²)",
    "wasDerivedFrom": "ex:reprojectedData",
    "generatedAtTime": "2026-07-13T17:44:06.7+02:00",
    "wasGeneratedBy": "ex:act4_filterAreas"
  },
  {
    "id": "ex:primaryBuffers",
    "provType": "Entity",
    "entityType": "ex:VectorDataset",
    "rdfs:label": "300m buffers around cool spots",
    "wasDerivedFrom": "ex:filteredCoolSpots",
    "generatedAtTime": "2026-07-13T17:44:09.1+02:00",
    "wasGeneratedBy": "ex:act5_buffer300m"
  },
  {
    "id": "ex:multiLevelBuffers",
    "provType": "Entity",
    "entityType": "ex:VectorDataset",
    "rdfs:label": "Multi-level buffer zones",
    "wasDerivedFrom": "ex:filteredCoolSpots",
    "generatedAtTime": "2026-07-13T17:44:15.9+02:00",
    "wasGeneratedBy": "ex:act6_bufferMultiLevel"
  },
  {
    "id": "ex:unservedAreas",
    "provType": "Entity",
    "entityType": "ex:VectorDataset",
    "rdfs:label": "Areas outside defined cool spot range",
    "wasDerivedFrom": [
      "ex:primaryBuffers",
      "ex:multiLevelBuffers",
      "ex:cityBoundary"
    ],
    "generatedAtTime": "2026-07-13T17:44:16.9+02:00",
    "wasGeneratedBy": "ex:act7_calcDifferences"
  },
  {
    "id": "ex:finalOutputPackage",
    "provType": "Entity",
    "entityType": [
      "prov:Collection",
      "ex:OutputPackage"
    ],
    "rdfs:label": "Exported spatial outputs",
    "hadMember": [
      "ex:file_city",
      "ex:file_coolSpots",
      "ex:file_coolSpotsFiltered",
      "ex:file_buffer",
      "ex:file_diff",
      "ex:file_ring0_75",
      "ex:file_ring75_150",
      "ex:file_ring150_225",
      "ex:file_ring225_300"
    ],
    "generatedAtTime": "2026-07-13T17:44:17.3+02:00",
    "wasGeneratedBy": "ex:act8_exportOutputs"
  },
  {
    "id": "ex:file_city",
    "provType": "Entity",
    "entityType": "ex:GeoPackageFile",
    "rdfs:label": "City boundary (UTM)",
    "schema:contentUrl": "outputs/city.gpkg",
    "schema:encodingFormat": "application/geopackage+sqlite3",
    "schema:sha256": "f7aacae91ba5791b0c06fee9ac022a49c48a8e4b58bff1cebba2e50760f46edf",
    "wasDerivedFrom": "ex:cityBoundary",
    "generatedAtTime": "2026-07-13T17:44:17.240+02:00",
    "wasGeneratedBy": "ex:act8_exportOutputs"
  },
  {
    "id": "ex:file_coolSpots",
    "provType": "Entity",
    "entityType": "ex:GeoPackageFile",
    "rdfs:label": "Cool spots (UTM)",
    "schema:contentUrl": "outputs/cool_spots.gpkg",
    "schema:encodingFormat": "application/geopackage+sqlite3",
    "schema:sha256": "fd7dbb6bed299cfed22e90f2057305f27dda8572163a58d6022739c34cdcb860",
    "wasDerivedFrom": "ex:reprojectedData",
    "generatedAtTime": "2026-07-13T17:44:17.245+02:00",
    "wasGeneratedBy": "ex:act8_exportOutputs"
  },
  {
    "id": "ex:file_coolSpotsFiltered",
    "provType": "Entity",
    "entityType": "ex:GeoPackageFile",
    "rdfs:label": "Cool spots filtered by min area",
    "schema:contentUrl": "outputs/cool_spots_filtered.gpkg",
    "schema:encodingFormat": "application/geopackage+sqlite3",
    "schema:sha256": "c232b9ce525709270edd3be1d1bb709602505e64265bc72d054e0a25c38e2cc4",
    "wasDerivedFrom": "ex:filteredCoolSpots",
    "generatedAtTime": "2026-07-13T17:44:17.250+02:00",
    "wasGeneratedBy": "ex:act8_exportOutputs"
  },
  {
    "id": "ex:file_buffer",
    "provType": "Entity",
    "entityType": "ex:GeoPackageFile",
    "rdfs:label": "300m buffers",
    "schema:contentUrl": "outputs/buffer.gpkg",
    "schema:encodingFormat": "application/geopackage+sqlite3",
    "schema:sha256": "0242d5216981cc52cd912352a9540fca63af47bd39fe02b53cb4db39d11a9fcf",
    "wasDerivedFrom": "ex:primaryBuffers",
    "generatedAtTime": "2026-07-13T17:44:17.233+02:00",
    "wasGeneratedBy": "ex:act8_exportOutputs"
  },
  {
    "id": "ex:file_diff",
    "provType": "Entity",
    "entityType": "ex:GeoPackageFile",
    "rdfs:label": "Unserved areas (>300m)",
    "schema:contentUrl": "outputs/diff.gpkg",
    "schema:encodingFormat": "application/geopackage+sqlite3",
    "schema:sha256": "918e75738a37bb2cb8e24f260bbc6c42017906121710ac5e86fe968e9d8e62fa",
    "wasDerivedFrom": "ex:unservedAreas",
    "generatedAtTime": "2026-07-13T17:44:17.271+02:00",
    "wasGeneratedBy": "ex:act8_exportOutputs"
  },
  {
    "id": "ex:file_ring0_75",
    "provType": "Entity",
    "entityType": "ex:GeoPackageFile",
    "rdfs:label": "Buffer ring 0-75m",
    "schema:contentUrl": "outputs/diff_0m-75m.gpkg",
    "schema:encodingFormat": "application/geopackage+sqlite3",
    "schema:sha256": "e16e0980138b3cdc25fd53d837b6f0dc5948d318a017dfab695f60e275fba501",
    "wasDerivedFrom": "ex:multiLevelBuffers",
    "generatedAtTime": "2026-07-13T17:44:17.255+02:00",
    "wasGeneratedBy": "ex:act8_exportOutputs"
  },
  {
    "id": "ex:file_ring75_150",
    "provType": "Entity",
    "entityType": "ex:GeoPackageFile",
    "rdfs:label": "Buffer ring 75-150m",
    "schema:contentUrl": "outputs/diff_75m-150m.gpkg",
    "schema:encodingFormat": "application/geopackage+sqlite3",
    "schema:sha256": "04f4bf3280175f9b1aa6189bc54cc78f9e07f2ed5bbbdc862dcaf58512c6d14b",
    "wasDerivedFrom": "ex:multiLevelBuffers",
    "generatedAtTime": "2026-07-13T17:44:17.265+02:00",
    "wasGeneratedBy": "ex:act8_exportOutputs"
  },
  {
    "id": "ex:file_ring150_225",
    "provType": "Entity",
    "entityType": "ex:GeoPackageFile",
    "rdfs:label": "Buffer ring 150-225m",
    "schema:contentUrl": "outputs/diff_150m-225m.gpkg",
    "schema:encodingFormat": "application/geopackage+sqlite3",
    "schema:sha256": "521b637211efbf3d0e44cab6950d44d4f144ab1c0c94f34e24c257b93b4f680c",
    "wasDerivedFrom": "ex:multiLevelBuffers",
    "generatedAtTime": "2026-07-13T17:44:17.275+02:00",
    "wasGeneratedBy": "ex:act8_exportOutputs"
  },
  {
    "id": "ex:file_ring225_300",
    "provType": "Entity",
    "entityType": "ex:GeoPackageFile",
    "rdfs:label": "Buffer ring 225-300m",
    "schema:contentUrl": "outputs/diff_225m-300m.gpkg",
    "schema:encodingFormat": "application/geopackage+sqlite3",
    "schema:sha256": "f88ac1fae96fba33c9702834eb19e762ac0213c57d2b3a4bdc1b89a85982e2f8",
    "wasDerivedFrom": "ex:multiLevelBuffers",
    "generatedAtTime": "2026-07-13T17:44:17.261+02:00",
    "wasGeneratedBy": "ex:act8_exportOutputs"
  },
  {
    "id": "ex:coolSpotsScript",
    "provType": "Entity",
    "entityType": [
      "prov:Plan",
      "schema:SoftwareSourceCode",
      "acttype:WorkflowPlan"
    ],
    "rdfs:label": "Cool spots workflow script",
    "schema:name": "cool_spots.py",
    "schema:programmingLanguage": "Python",
    "schema:sha256": "42abb24daf03e809f2f4d4dbbd1fa443508d243ba9f00a87ef3b47065fe2af43",
    "wasAttributedTo": "https://orcid.org/0000-0003-4718-2959"
  },

  {
    "id": "ex:act1_defineInputs",
    "provType": "Activity",
    "activityType": "ex:defineInputs",
    "rdfs:label": "Step 1: Define Process Inputs",
    "startedAtTime": "2026-07-13T17:35:00+02:00",
    "endedAtTime": "2026-07-13T17:43:40+02:00",
    "wasAssociatedWith": "https://orcid.org/0000-0003-4718-2959"
  },
  {
    "id": "ex:workflowRun",
    "provType": "Activity",
    "activityType": "acttype:WorkflowRun",
    "rdfs:label": "Cool spots workflow run",
    "startedAtTime": "2026-07-13T17:43:41.2+02:00",
    "endedAtTime": "2026-07-13T17:44:17.3+02:00",
    "used": [
      "ex:nominatimApi",
      "ex:overpassApi"
    ],
    "generated": "ex:finalOutputPackage",
    "wasAssociatedWith": "ex:gisPipelineEngine",
    "qualifiedAssociation": {
      "type": "Association",
      "agent": "ex:gisPipelineEngine",
      "hadRole": "ex:workflowExecutor",
      "hadPlan": "ex:coolSpotsScript"
    }
  },
  {
    "id": "ex:act2a_geocodeCity",
    "provType": "Activity",
    "activityType": "ex:geocodeCity",
    "rdfs:label": "Step 2a: Geocode city boundary",
    "startedAtTime": "2026-07-13T17:43:41.2+02:00",
    "endedAtTime": "2026-07-13T17:43:41.9+02:00",
    "used": [
      "ex:processInputs",
      "ex:nominatimApi"
    ],
    "wasAssociatedWith": "ex:gisPipelineEngine",
    "dcterms:isPartOf": "ex:workflowRun"
  },
  {
    "id": "ex:act2_acquireData",
    "provType": "Activity",
    "activityType": "ex:acquireData",
    "rdfs:label": "Step 2: Acquire relevant OSM data",
    "startedAtTime": "2026-07-13T17:43:42.0+02:00",
    "endedAtTime": "2026-07-13T17:44:05.8+02:00",
    "used": [
      "ex:processInputs",
      "ex:cityBoundary",
      "ex:overpassApi"
    ],
    "wasAssociatedWith": "ex:gisPipelineEngine",
    "dcterms:isPartOf": "ex:workflowRun"
  },
  {
    "id": "ex:act3_reproject",
    "provType": "Activity",
    "activityType": "https://register.ospd.dev.kurrawong.ai/catalogs/reg:top/collections/reg:52north/items/demo:GA018",
    "rdfs:label": "Step 3: Reproject EPSG:4326 to UTM",
    "startedAtTime": "2026-07-13T17:44:05.9+02:00",
    "endedAtTime": "2026-07-13T17:44:06.4+02:00",
    "used": "ex:rawOsmData",
    "wasAssociatedWith": "ex:gisPipelineEngine",
    "dcterms:isPartOf": "ex:workflowRun"
  },
  {
    "id": "ex:act4_filterAreas",
    "provType": "Activity",
    "activityType": "https://register.ospd.dev.kurrawong.ai/catalogs/reg:top/collections/reg:52north/items/demo:GA020",
    "rdfs:label": "Step 4: Filter areas by size",
    "startedAtTime": "2026-07-13T17:44:06.5+02:00",
    "endedAtTime": "2026-07-13T17:44:06.7+02:00",
    "used": [
      "ex:reprojectedData",
      "ex:processInputs"
    ],
    "wasAssociatedWith": "ex:gisPipelineEngine",
    "dcterms:isPartOf": "ex:workflowRun"
  },
  {
    "id": "ex:act5_buffer300m",
    "provType": "Activity",
    "activityType": "https://register.ospd.dev.kurrawong.ai/catalogs/reg:top/collections/reg:ogcactivites/items/demo:GA001",
    "rdfs:label": "Step 5: Create 300m buffer (or walking distance)",
    "startedAtTime": "2026-07-13T17:44:06.8+02:00",
    "endedAtTime": "2026-07-13T17:44:09.1+02:00",
    "used": [
      "ex:filteredCoolSpots",
      "ex:processInputs"
    ],
    "wasAssociatedWith": "ex:gisPipelineEngine",
    "dcterms:isPartOf": "ex:workflowRun"
  },
  {
    "id": "ex:act6_bufferMultiLevel",
    "provType": "Activity",
    "activityType": "https://register.ospd.dev.kurrawong.ai/catalogs/reg:top/collections/reg:ogcactivites/items/demo:GA001",
    "rdfs:label": "Step 6: Create additional level buffers",
    "startedAtTime": "2026-07-13T17:44:09.2+02:00",
    "endedAtTime": "2026-07-13T17:44:15.9+02:00",
    "used": [
      "ex:filteredCoolSpots",
      "ex:processInputs"
    ],
    "wasAssociatedWith": "ex:gisPipelineEngine",
    "dcterms:isPartOf": "ex:workflowRun"
  },
  {
    "id": "ex:act7_calcDifferences",
    "provType": "Activity",
    "activityType": "https://register.ospd.dev.kurrawong.ai/catalogs/reg:top/collections/reg:52north/items/demo:GA019",
    "rdfs:label": "Step 7: Identify unserved city areas",
    "startedAtTime": "2026-07-13T17:44:16.0+02:00",
    "endedAtTime": "2026-07-13T17:44:16.9+02:00",
    "used": [
      "ex:primaryBuffers",
      "ex:multiLevelBuffers",
      "ex:cityBoundary"
    ],
    "wasAssociatedWith": "ex:gisPipelineEngine",
    "dcterms:isPartOf": "ex:workflowRun"
  },
  {
    "id": "ex:act8_exportOutputs",
    "provType": "Activity",
    "activityType": "ex:exportOutputs",
    "rdfs:label": "Step 8: Export process outputs",
    "startedAtTime": "2026-07-13T17:44:17.0+02:00",
    "endedAtTime": "2026-07-13T17:44:17.3+02:00",
    "used": [
      "ex:cityBoundary",
      "ex:reprojectedData",
      "ex:filteredCoolSpots",
      "ex:primaryBuffers",
      "ex:unservedAreas",
      "ex:multiLevelBuffers"
    ],
    "wasAssociatedWith": "ex:gisPipelineEngine",
    "dcterms:isPartOf": "ex:workflowRun"
  },

  {
    "id": "https://orcid.org/0000-0003-4718-2959",
    "provType": "Agent",
    "agentType": "prov:Person",
    "rdfs:label": "GIS Analyst",
    "schema:identifier": "https://orcid.org/0000-0003-4718-2959"
  },
  {
    "id": "ex:gisPipelineEngine",
    "provType": "Agent",
    "agentType": ["prov:SoftwareAgent", "acttype:WorkflowRunner"],
    "rdfs:label": "Automated Spatial Workflow Runner",
    "schema:softwareRequirements": [
      "Python 3.13.3",
      "osmnx 2.1.0",
      "geopandas 1.1.4",
      "shapely 2.1.2"
    ],
    "actedOnBehalfOf": "https://orcid.org/0000-0003-4718-2959"
  }
]

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/prov-examples/52n-provenance/cool-spots/context.jsonld",
  "@graph": [
    {
      "id": "ex:processInputs",
      "provType": "Entity",
      "entityType": "ex:WorkflowInputs",
      "rdfs:label": "Workflow Parameters",
      "ex:location": "M\u00fcnster, Germany",
      "ex:osmTags": "landuse=forest, natural=wood, leisure=park",
      "ex:minArea": 200,
      "ex:distance": 300,
      "ex:bufferIntervals": [
        0,
        75,
        150,
        225,
        300
      ],
      "generatedAtTime": "2026-07-13T17:43:40+02:00",
      "wasGeneratedBy": "ex:act1_defineInputs",
      "wasAttributedTo": "https://orcid.org/0000-0003-4718-2959"
    },
    {
      "id": "ex:openStreetMap",
      "provType": "Entity",
      "entityType": "prov:PrimarySource",
      "rdfs:label": "OpenStreetMap",
      "schema:url": "https://www.openstreetmap.org",
      "dcterms:license": "https://opendatacommons.org/licenses/odbl/1-0/"
    },
    {
      "id": "ex:nominatimApi",
      "provType": "Entity",
      "entityType": "schema:WebAPI",
      "rdfs:label": "Nominatim geocoding API",
      "schema:url": "https://nominatim.openstreetmap.org/"
    },
    {
      "id": "ex:overpassApi",
      "provType": "Entity",
      "entityType": "schema:WebAPI",
      "rdfs:label": "Overpass API",
      "schema:url": "https://overpass-api.de/api",
      "schema:softwareVersion": "0.7.62.11 87bfad18"
    },
    {
      "id": "ex:cityBoundary",
      "provType": "Entity",
      "entityType": "ex:VectorDataset",
      "rdfs:label": "M\u00fcnster city boundary (EPSG:4326)",
      "ex:crs": "EPSG:4326",
      "hadPrimarySource": "ex:openStreetMap",
      "generatedAtTime": "2026-07-13T17:43:41.9+02:00",
      "wasGeneratedBy": "ex:act2a_geocodeCity"
    },
    {
      "id": "ex:rawOsmData",
      "provType": "Entity",
      "entityType": "ex:OsmDataset",
      "rdfs:label": "Raw OSM vector data (EPSG:4326)",
      "ex:crs": "EPSG:4326",
      "ex:osmBaseTimestamp": "2026-07-13T13:54:30Z",
      "dcterms:license": "https://opendatacommons.org/licenses/odbl/1-0/",
      "hadPrimarySource": "ex:openStreetMap",
      "generatedAtTime": "2026-07-13T17:44:05.8+02:00",
      "wasGeneratedBy": "ex:act2_acquireData"
    },
    {
      "id": "ex:reprojectedData",
      "provType": "Entity",
      "entityType": "ex:VectorDataset",
      "rdfs:label": "UTM Projected OSM data",
      "ex:crs": "EPSG:32632",
      "wasDerivedFrom": "ex:rawOsmData",
      "generatedAtTime": "2026-07-13T17:44:06.4+02:00",
      "wasGeneratedBy": "ex:act3_reproject"
    },
    {
      "id": "ex:filteredCoolSpots",
      "provType": "Entity",
      "entityType": "ex:VectorDataset",
      "rdfs:label": "Cool spots filtered by min area (>=200m\u00b2)",
      "wasDerivedFrom": "ex:reprojectedData",
      "generatedAtTime": "2026-07-13T17:44:06.7+02:00",
      "wasGeneratedBy": "ex:act4_filterAreas"
    },
    {
      "id": "ex:primaryBuffers",
      "provType": "Entity",
      "entityType": "ex:VectorDataset",
      "rdfs:label": "300m buffers around cool spots",
      "wasDerivedFrom": "ex:filteredCoolSpots",
      "generatedAtTime": "2026-07-13T17:44:09.1+02:00",
      "wasGeneratedBy": "ex:act5_buffer300m"
    },
    {
      "id": "ex:multiLevelBuffers",
      "provType": "Entity",
      "entityType": "ex:VectorDataset",
      "rdfs:label": "Multi-level buffer zones",
      "wasDerivedFrom": "ex:filteredCoolSpots",
      "generatedAtTime": "2026-07-13T17:44:15.9+02:00",
      "wasGeneratedBy": "ex:act6_bufferMultiLevel"
    },
    {
      "id": "ex:unservedAreas",
      "provType": "Entity",
      "entityType": "ex:VectorDataset",
      "rdfs:label": "Areas outside defined cool spot range",
      "wasDerivedFrom": [
        "ex:primaryBuffers",
        "ex:multiLevelBuffers",
        "ex:cityBoundary"
      ],
      "generatedAtTime": "2026-07-13T17:44:16.9+02:00",
      "wasGeneratedBy": "ex:act7_calcDifferences"
    },
    {
      "id": "ex:finalOutputPackage",
      "provType": "Entity",
      "entityType": [
        "prov:Collection",
        "ex:OutputPackage"
      ],
      "rdfs:label": "Exported spatial outputs",
      "hadMember": [
        "ex:file_city",
        "ex:file_coolSpots",
        "ex:file_coolSpotsFiltered",
        "ex:file_buffer",
        "ex:file_diff",
        "ex:file_ring0_75",
        "ex:file_ring75_150",
        "ex:file_ring150_225",
        "ex:file_ring225_300"
      ],
      "generatedAtTime": "2026-07-13T17:44:17.3+02:00",
      "wasGeneratedBy": "ex:act8_exportOutputs"
    },
    {
      "id": "ex:file_city",
      "provType": "Entity",
      "entityType": "ex:GeoPackageFile",
      "rdfs:label": "City boundary (UTM)",
      "schema:contentUrl": "outputs/city.gpkg",
      "schema:encodingFormat": "application/geopackage+sqlite3",
      "schema:sha256": "f7aacae91ba5791b0c06fee9ac022a49c48a8e4b58bff1cebba2e50760f46edf",
      "wasDerivedFrom": "ex:cityBoundary",
      "generatedAtTime": "2026-07-13T17:44:17.240+02:00",
      "wasGeneratedBy": "ex:act8_exportOutputs"
    },
    {
      "id": "ex:file_coolSpots",
      "provType": "Entity",
      "entityType": "ex:GeoPackageFile",
      "rdfs:label": "Cool spots (UTM)",
      "schema:contentUrl": "outputs/cool_spots.gpkg",
      "schema:encodingFormat": "application/geopackage+sqlite3",
      "schema:sha256": "fd7dbb6bed299cfed22e90f2057305f27dda8572163a58d6022739c34cdcb860",
      "wasDerivedFrom": "ex:reprojectedData",
      "generatedAtTime": "2026-07-13T17:44:17.245+02:00",
      "wasGeneratedBy": "ex:act8_exportOutputs"
    },
    {
      "id": "ex:file_coolSpotsFiltered",
      "provType": "Entity",
      "entityType": "ex:GeoPackageFile",
      "rdfs:label": "Cool spots filtered by min area",
      "schema:contentUrl": "outputs/cool_spots_filtered.gpkg",
      "schema:encodingFormat": "application/geopackage+sqlite3",
      "schema:sha256": "c232b9ce525709270edd3be1d1bb709602505e64265bc72d054e0a25c38e2cc4",
      "wasDerivedFrom": "ex:filteredCoolSpots",
      "generatedAtTime": "2026-07-13T17:44:17.250+02:00",
      "wasGeneratedBy": "ex:act8_exportOutputs"
    },
    {
      "id": "ex:file_buffer",
      "provType": "Entity",
      "entityType": "ex:GeoPackageFile",
      "rdfs:label": "300m buffers",
      "schema:contentUrl": "outputs/buffer.gpkg",
      "schema:encodingFormat": "application/geopackage+sqlite3",
      "schema:sha256": "0242d5216981cc52cd912352a9540fca63af47bd39fe02b53cb4db39d11a9fcf",
      "wasDerivedFrom": "ex:primaryBuffers",
      "generatedAtTime": "2026-07-13T17:44:17.233+02:00",
      "wasGeneratedBy": "ex:act8_exportOutputs"
    },
    {
      "id": "ex:file_diff",
      "provType": "Entity",
      "entityType": "ex:GeoPackageFile",
      "rdfs:label": "Unserved areas (>300m)",
      "schema:contentUrl": "outputs/diff.gpkg",
      "schema:encodingFormat": "application/geopackage+sqlite3",
      "schema:sha256": "918e75738a37bb2cb8e24f260bbc6c42017906121710ac5e86fe968e9d8e62fa",
      "wasDerivedFrom": "ex:unservedAreas",
      "generatedAtTime": "2026-07-13T17:44:17.271+02:00",
      "wasGeneratedBy": "ex:act8_exportOutputs"
    },
    {
      "id": "ex:file_ring0_75",
      "provType": "Entity",
      "entityType": "ex:GeoPackageFile",
      "rdfs:label": "Buffer ring 0-75m",
      "schema:contentUrl": "outputs/diff_0m-75m.gpkg",
      "schema:encodingFormat": "application/geopackage+sqlite3",
      "schema:sha256": "e16e0980138b3cdc25fd53d837b6f0dc5948d318a017dfab695f60e275fba501",
      "wasDerivedFrom": "ex:multiLevelBuffers",
      "generatedAtTime": "2026-07-13T17:44:17.255+02:00",
      "wasGeneratedBy": "ex:act8_exportOutputs"
    },
    {
      "id": "ex:file_ring75_150",
      "provType": "Entity",
      "entityType": "ex:GeoPackageFile",
      "rdfs:label": "Buffer ring 75-150m",
      "schema:contentUrl": "outputs/diff_75m-150m.gpkg",
      "schema:encodingFormat": "application/geopackage+sqlite3",
      "schema:sha256": "04f4bf3280175f9b1aa6189bc54cc78f9e07f2ed5bbbdc862dcaf58512c6d14b",
      "wasDerivedFrom": "ex:multiLevelBuffers",
      "generatedAtTime": "2026-07-13T17:44:17.265+02:00",
      "wasGeneratedBy": "ex:act8_exportOutputs"
    },
    {
      "id": "ex:file_ring150_225",
      "provType": "Entity",
      "entityType": "ex:GeoPackageFile",
      "rdfs:label": "Buffer ring 150-225m",
      "schema:contentUrl": "outputs/diff_150m-225m.gpkg",
      "schema:encodingFormat": "application/geopackage+sqlite3",
      "schema:sha256": "521b637211efbf3d0e44cab6950d44d4f144ab1c0c94f34e24c257b93b4f680c",
      "wasDerivedFrom": "ex:multiLevelBuffers",
      "generatedAtTime": "2026-07-13T17:44:17.275+02:00",
      "wasGeneratedBy": "ex:act8_exportOutputs"
    },
    {
      "id": "ex:file_ring225_300",
      "provType": "Entity",
      "entityType": "ex:GeoPackageFile",
      "rdfs:label": "Buffer ring 225-300m",
      "schema:contentUrl": "outputs/diff_225m-300m.gpkg",
      "schema:encodingFormat": "application/geopackage+sqlite3",
      "schema:sha256": "f88ac1fae96fba33c9702834eb19e762ac0213c57d2b3a4bdc1b89a85982e2f8",
      "wasDerivedFrom": "ex:multiLevelBuffers",
      "generatedAtTime": "2026-07-13T17:44:17.261+02:00",
      "wasGeneratedBy": "ex:act8_exportOutputs"
    },
    {
      "id": "ex:coolSpotsScript",
      "provType": "Entity",
      "entityType": [
        "prov:Plan",
        "schema:SoftwareSourceCode",
        "acttype:WorkflowPlan"
      ],
      "rdfs:label": "Cool spots workflow script",
      "schema:name": "cool_spots.py",
      "schema:programmingLanguage": "Python",
      "schema:sha256": "42abb24daf03e809f2f4d4dbbd1fa443508d243ba9f00a87ef3b47065fe2af43",
      "wasAttributedTo": "https://orcid.org/0000-0003-4718-2959"
    },
    {
      "id": "ex:act1_defineInputs",
      "provType": "Activity",
      "activityType": "ex:defineInputs",
      "rdfs:label": "Step 1: Define Process Inputs",
      "startedAtTime": "2026-07-13T17:35:00+02:00",
      "endedAtTime": "2026-07-13T17:43:40+02:00",
      "wasAssociatedWith": "https://orcid.org/0000-0003-4718-2959"
    },
    {
      "id": "ex:workflowRun",
      "provType": "Activity",
      "activityType": "acttype:WorkflowRun",
      "rdfs:label": "Cool spots workflow run",
      "startedAtTime": "2026-07-13T17:43:41.2+02:00",
      "endedAtTime": "2026-07-13T17:44:17.3+02:00",
      "used": [
        "ex:nominatimApi",
        "ex:overpassApi"
      ],
      "generated": "ex:finalOutputPackage",
      "wasAssociatedWith": "ex:gisPipelineEngine",
      "qualifiedAssociation": {
        "type": "Association",
        "agent": "ex:gisPipelineEngine",
        "hadRole": "ex:workflowExecutor",
        "hadPlan": "ex:coolSpotsScript"
      }
    },
    {
      "id": "ex:act2a_geocodeCity",
      "provType": "Activity",
      "activityType": "ex:geocodeCity",
      "rdfs:label": "Step 2a: Geocode city boundary",
      "startedAtTime": "2026-07-13T17:43:41.2+02:00",
      "endedAtTime": "2026-07-13T17:43:41.9+02:00",
      "used": [
        "ex:processInputs",
        "ex:nominatimApi"
      ],
      "wasAssociatedWith": "ex:gisPipelineEngine",
      "dcterms:isPartOf": "ex:workflowRun"
    },
    {
      "id": "ex:act2_acquireData",
      "provType": "Activity",
      "activityType": "ex:acquireData",
      "rdfs:label": "Step 2: Acquire relevant OSM data",
      "startedAtTime": "2026-07-13T17:43:42.0+02:00",
      "endedAtTime": "2026-07-13T17:44:05.8+02:00",
      "used": [
        "ex:processInputs",
        "ex:cityBoundary",
        "ex:overpassApi"
      ],
      "wasAssociatedWith": "ex:gisPipelineEngine",
      "dcterms:isPartOf": "ex:workflowRun"
    },
    {
      "id": "ex:act3_reproject",
      "provType": "Activity",
      "activityType": "https://register.ospd.dev.kurrawong.ai/catalogs/reg:top/collections/reg:52north/items/demo:GA018",
      "rdfs:label": "Step 3: Reproject EPSG:4326 to UTM",
      "startedAtTime": "2026-07-13T17:44:05.9+02:00",
      "endedAtTime": "2026-07-13T17:44:06.4+02:00",
      "used": "ex:rawOsmData",
      "wasAssociatedWith": "ex:gisPipelineEngine",
      "dcterms:isPartOf": "ex:workflowRun"
    },
    {
      "id": "ex:act4_filterAreas",
      "provType": "Activity",
      "activityType": "https://register.ospd.dev.kurrawong.ai/catalogs/reg:top/collections/reg:52north/items/demo:GA020",
      "rdfs:label": "Step 4: Filter areas by size",
      "startedAtTime": "2026-07-13T17:44:06.5+02:00",
      "endedAtTime": "2026-07-13T17:44:06.7+02:00",
      "used": [
        "ex:reprojectedData",
        "ex:processInputs"
      ],
      "wasAssociatedWith": "ex:gisPipelineEngine",
      "dcterms:isPartOf": "ex:workflowRun"
    },
    {
      "id": "ex:act5_buffer300m",
      "provType": "Activity",
      "activityType": "https://register.ospd.dev.kurrawong.ai/catalogs/reg:top/collections/reg:ogcactivites/items/demo:GA001",
      "rdfs:label": "Step 5: Create 300m buffer (or walking distance)",
      "startedAtTime": "2026-07-13T17:44:06.8+02:00",
      "endedAtTime": "2026-07-13T17:44:09.1+02:00",
      "used": [
        "ex:filteredCoolSpots",
        "ex:processInputs"
      ],
      "wasAssociatedWith": "ex:gisPipelineEngine",
      "dcterms:isPartOf": "ex:workflowRun"
    },
    {
      "id": "ex:act6_bufferMultiLevel",
      "provType": "Activity",
      "activityType": "https://register.ospd.dev.kurrawong.ai/catalogs/reg:top/collections/reg:ogcactivites/items/demo:GA001",
      "rdfs:label": "Step 6: Create additional level buffers",
      "startedAtTime": "2026-07-13T17:44:09.2+02:00",
      "endedAtTime": "2026-07-13T17:44:15.9+02:00",
      "used": [
        "ex:filteredCoolSpots",
        "ex:processInputs"
      ],
      "wasAssociatedWith": "ex:gisPipelineEngine",
      "dcterms:isPartOf": "ex:workflowRun"
    },
    {
      "id": "ex:act7_calcDifferences",
      "provType": "Activity",
      "activityType": "https://register.ospd.dev.kurrawong.ai/catalogs/reg:top/collections/reg:52north/items/demo:GA019",
      "rdfs:label": "Step 7: Identify unserved city areas",
      "startedAtTime": "2026-07-13T17:44:16.0+02:00",
      "endedAtTime": "2026-07-13T17:44:16.9+02:00",
      "used": [
        "ex:primaryBuffers",
        "ex:multiLevelBuffers",
        "ex:cityBoundary"
      ],
      "wasAssociatedWith": "ex:gisPipelineEngine",
      "dcterms:isPartOf": "ex:workflowRun"
    },
    {
      "id": "ex:act8_exportOutputs",
      "provType": "Activity",
      "activityType": "ex:exportOutputs",
      "rdfs:label": "Step 8: Export process outputs",
      "startedAtTime": "2026-07-13T17:44:17.0+02:00",
      "endedAtTime": "2026-07-13T17:44:17.3+02:00",
      "used": [
        "ex:cityBoundary",
        "ex:reprojectedData",
        "ex:filteredCoolSpots",
        "ex:primaryBuffers",
        "ex:unservedAreas",
        "ex:multiLevelBuffers"
      ],
      "wasAssociatedWith": "ex:gisPipelineEngine",
      "dcterms:isPartOf": "ex:workflowRun"
    },
    {
      "id": "https://orcid.org/0000-0003-4718-2959",
      "provType": "Agent",
      "agentType": "prov:Person",
      "rdfs:label": "GIS Analyst",
      "schema:identifier": "https://orcid.org/0000-0003-4718-2959"
    },
    {
      "id": "ex:gisPipelineEngine",
      "provType": "Agent",
      "agentType": [
        "prov:SoftwareAgent",
        "acttype:WorkflowRunner"
      ],
      "rdfs:label": "Automated Spatial Workflow Runner",
      "schema:softwareRequirements": [
        "Python 3.13.3",
        "osmnx 2.1.0",
        "geopandas 1.1.4",
        "shapely 2.1.2"
      ],
      "actedOnBehalfOf": "https://orcid.org/0000-0003-4718-2959"
    }
  ]
}
```

#### ttl
```ttl
@prefix acttype: <https://w3id.org/ogc/rim/activity-type/> .
@prefix dcterms: <http://purl.org/dc/terms/> .
@prefix ex: <https://example.org/cool-spots#> .
@prefix prov: <http://www.w3.org/ns/prov#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix schema: <https://schema.org/> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

ex:workflowRun a prov:Activity,
        acttype:WorkflowRun ;
    rdfs:label "Cool spots workflow run" ;
    prov:endedAtTime "2026-07-13T17:44:17.300000+02:00"^^xsd:dateTime ;
    prov:generated ex:finalOutputPackage ;
    prov:qualifiedAssociation [ prov:agent ex:gisPipelineEngine ;
            prov:hadPlan ex:coolSpotsScript ;
            prov:hadRole ex:workflowExecutor ] ;
    prov:startedAtTime "2026-07-13T17:43:41.200000+02:00"^^xsd:dateTime ;
    prov:type acttype:WorkflowRun ;
    prov:used ex:nominatimApi,
        ex:overpassApi ;
    prov:wasAssociatedWith ex:gisPipelineEngine .

ex:act1_defineInputs a prov:Activity ;
    rdfs:label "Step 1: Define Process Inputs" ;
    prov:endedAtTime "2026-07-13T17:43:40+02:00"^^xsd:dateTime ;
    prov:startedAtTime "2026-07-13T17:35:00+02:00"^^xsd:dateTime ;
    prov:type ex:defineInputs ;
    prov:wasAssociatedWith <https://orcid.org/0000-0003-4718-2959> .

ex:act2_acquireData a prov:Activity ;
    rdfs:label "Step 2: Acquire relevant OSM data" ;
    dcterms:isPartOf "ex:workflowRun" ;
    prov:endedAtTime "2026-07-13T17:44:05.800000+02:00"^^xsd:dateTime ;
    prov:startedAtTime "2026-07-13T17:43:42+02:00"^^xsd:dateTime ;
    prov:type ex:acquireData ;
    prov:used ex:cityBoundary,
        ex:overpassApi,
        ex:processInputs ;
    prov:wasAssociatedWith ex:gisPipelineEngine .

ex:act2a_geocodeCity a prov:Activity ;
    rdfs:label "Step 2a: Geocode city boundary" ;
    dcterms:isPartOf "ex:workflowRun" ;
    prov:endedAtTime "2026-07-13T17:43:41.900000+02:00"^^xsd:dateTime ;
    prov:startedAtTime "2026-07-13T17:43:41.200000+02:00"^^xsd:dateTime ;
    prov:type ex:geocodeCity ;
    prov:used ex:nominatimApi,
        ex:processInputs ;
    prov:wasAssociatedWith ex:gisPipelineEngine .

ex:act3_reproject a prov:Activity ;
    rdfs:label "Step 3: Reproject EPSG:4326 to UTM" ;
    dcterms:isPartOf "ex:workflowRun" ;
    prov:endedAtTime "2026-07-13T17:44:06.400000+02:00"^^xsd:dateTime ;
    prov:startedAtTime "2026-07-13T17:44:05.900000+02:00"^^xsd:dateTime ;
    prov:type <https://register.ospd.dev.kurrawong.ai/catalogs/reg:top/collections/reg:52north/items/demo:GA018> ;
    prov:used ex:rawOsmData ;
    prov:wasAssociatedWith ex:gisPipelineEngine .

ex:act4_filterAreas a prov:Activity ;
    rdfs:label "Step 4: Filter areas by size" ;
    dcterms:isPartOf "ex:workflowRun" ;
    prov:endedAtTime "2026-07-13T17:44:06.700000+02:00"^^xsd:dateTime ;
    prov:startedAtTime "2026-07-13T17:44:06.500000+02:00"^^xsd:dateTime ;
    prov:type <https://register.ospd.dev.kurrawong.ai/catalogs/reg:top/collections/reg:52north/items/demo:GA020> ;
    prov:used ex:processInputs,
        ex:reprojectedData ;
    prov:wasAssociatedWith ex:gisPipelineEngine .

ex:act5_buffer300m a prov:Activity ;
    rdfs:label "Step 5: Create 300m buffer (or walking distance)" ;
    dcterms:isPartOf "ex:workflowRun" ;
    prov:endedAtTime "2026-07-13T17:44:09.100000+02:00"^^xsd:dateTime ;
    prov:startedAtTime "2026-07-13T17:44:06.800000+02:00"^^xsd:dateTime ;
    prov:type <https://register.ospd.dev.kurrawong.ai/catalogs/reg:top/collections/reg:ogcactivites/items/demo:GA001> ;
    prov:used ex:filteredCoolSpots,
        ex:processInputs ;
    prov:wasAssociatedWith ex:gisPipelineEngine .

ex:act6_bufferMultiLevel a prov:Activity ;
    rdfs:label "Step 6: Create additional level buffers" ;
    dcterms:isPartOf "ex:workflowRun" ;
    prov:endedAtTime "2026-07-13T17:44:15.900000+02:00"^^xsd:dateTime ;
    prov:startedAtTime "2026-07-13T17:44:09.200000+02:00"^^xsd:dateTime ;
    prov:type <https://register.ospd.dev.kurrawong.ai/catalogs/reg:top/collections/reg:ogcactivites/items/demo:GA001> ;
    prov:used ex:filteredCoolSpots,
        ex:processInputs ;
    prov:wasAssociatedWith ex:gisPipelineEngine .

ex:act7_calcDifferences a prov:Activity ;
    rdfs:label "Step 7: Identify unserved city areas" ;
    dcterms:isPartOf "ex:workflowRun" ;
    prov:endedAtTime "2026-07-13T17:44:16.900000+02:00"^^xsd:dateTime ;
    prov:startedAtTime "2026-07-13T17:44:16+02:00"^^xsd:dateTime ;
    prov:type <https://register.ospd.dev.kurrawong.ai/catalogs/reg:top/collections/reg:52north/items/demo:GA019> ;
    prov:used ex:cityBoundary,
        ex:multiLevelBuffers,
        ex:primaryBuffers ;
    prov:wasAssociatedWith ex:gisPipelineEngine .

ex:coolSpotsScript a prov:Entity,
        prov:Plan,
        acttype:WorkflowPlan ;
    rdfs:label "Cool spots workflow script" ;
    prov:type prov:Plan,
        schema:SoftwareSourceCode,
        acttype:WorkflowPlan ;
    prov:wasAttributedTo <https://orcid.org/0000-0003-4718-2959> ;
    schema:name "cool_spots.py" ;
    schema:programmingLanguage "Python" ;
    schema:sha256 "42abb24daf03e809f2f4d4dbbd1fa443508d243ba9f00a87ef3b47065fe2af43" .

ex:file_buffer a prov:Entity ;
    rdfs:label "300m buffers" ;
    prov:generatedAtTime "2026-07-13T17:44:17.233000+02:00"^^xsd:dateTime ;
    prov:type ex:GeoPackageFile ;
    prov:wasDerivedFrom ex:primaryBuffers ;
    prov:wasGeneratedBy ex:act8_exportOutputs ;
    schema:contentUrl "outputs/buffer.gpkg" ;
    schema:encodingFormat "application/geopackage+sqlite3" ;
    schema:sha256 "0242d5216981cc52cd912352a9540fca63af47bd39fe02b53cb4db39d11a9fcf" .

ex:file_city a prov:Entity ;
    rdfs:label "City boundary (UTM)" ;
    prov:generatedAtTime "2026-07-13T17:44:17.240000+02:00"^^xsd:dateTime ;
    prov:type ex:GeoPackageFile ;
    prov:wasDerivedFrom ex:cityBoundary ;
    prov:wasGeneratedBy ex:act8_exportOutputs ;
    schema:contentUrl "outputs/city.gpkg" ;
    schema:encodingFormat "application/geopackage+sqlite3" ;
    schema:sha256 "f7aacae91ba5791b0c06fee9ac022a49c48a8e4b58bff1cebba2e50760f46edf" .

ex:file_coolSpots a prov:Entity ;
    rdfs:label "Cool spots (UTM)" ;
    prov:generatedAtTime "2026-07-13T17:44:17.245000+02:00"^^xsd:dateTime ;
    prov:type ex:GeoPackageFile ;
    prov:wasDerivedFrom ex:reprojectedData ;
    prov:wasGeneratedBy ex:act8_exportOutputs ;
    schema:contentUrl "outputs/cool_spots.gpkg" ;
    schema:encodingFormat "application/geopackage+sqlite3" ;
    schema:sha256 "fd7dbb6bed299cfed22e90f2057305f27dda8572163a58d6022739c34cdcb860" .

ex:file_coolSpotsFiltered a prov:Entity ;
    rdfs:label "Cool spots filtered by min area" ;
    prov:generatedAtTime "2026-07-13T17:44:17.250000+02:00"^^xsd:dateTime ;
    prov:type ex:GeoPackageFile ;
    prov:wasDerivedFrom ex:filteredCoolSpots ;
    prov:wasGeneratedBy ex:act8_exportOutputs ;
    schema:contentUrl "outputs/cool_spots_filtered.gpkg" ;
    schema:encodingFormat "application/geopackage+sqlite3" ;
    schema:sha256 "c232b9ce525709270edd3be1d1bb709602505e64265bc72d054e0a25c38e2cc4" .

ex:file_diff a prov:Entity ;
    rdfs:label "Unserved areas (>300m)" ;
    prov:generatedAtTime "2026-07-13T17:44:17.271000+02:00"^^xsd:dateTime ;
    prov:type ex:GeoPackageFile ;
    prov:wasDerivedFrom ex:unservedAreas ;
    prov:wasGeneratedBy ex:act8_exportOutputs ;
    schema:contentUrl "outputs/diff.gpkg" ;
    schema:encodingFormat "application/geopackage+sqlite3" ;
    schema:sha256 "918e75738a37bb2cb8e24f260bbc6c42017906121710ac5e86fe968e9d8e62fa" .

ex:file_ring0_75 a prov:Entity ;
    rdfs:label "Buffer ring 0-75m" ;
    prov:generatedAtTime "2026-07-13T17:44:17.255000+02:00"^^xsd:dateTime ;
    prov:type ex:GeoPackageFile ;
    prov:wasDerivedFrom ex:multiLevelBuffers ;
    prov:wasGeneratedBy ex:act8_exportOutputs ;
    schema:contentUrl "outputs/diff_0m-75m.gpkg" ;
    schema:encodingFormat "application/geopackage+sqlite3" ;
    schema:sha256 "e16e0980138b3cdc25fd53d837b6f0dc5948d318a017dfab695f60e275fba501" .

ex:file_ring150_225 a prov:Entity ;
    rdfs:label "Buffer ring 150-225m" ;
    prov:generatedAtTime "2026-07-13T17:44:17.275000+02:00"^^xsd:dateTime ;
    prov:type ex:GeoPackageFile ;
    prov:wasDerivedFrom ex:multiLevelBuffers ;
    prov:wasGeneratedBy ex:act8_exportOutputs ;
    schema:contentUrl "outputs/diff_150m-225m.gpkg" ;
    schema:encodingFormat "application/geopackage+sqlite3" ;
    schema:sha256 "521b637211efbf3d0e44cab6950d44d4f144ab1c0c94f34e24c257b93b4f680c" .

ex:file_ring225_300 a prov:Entity ;
    rdfs:label "Buffer ring 225-300m" ;
    prov:generatedAtTime "2026-07-13T17:44:17.261000+02:00"^^xsd:dateTime ;
    prov:type ex:GeoPackageFile ;
    prov:wasDerivedFrom ex:multiLevelBuffers ;
    prov:wasGeneratedBy ex:act8_exportOutputs ;
    schema:contentUrl "outputs/diff_225m-300m.gpkg" ;
    schema:encodingFormat "application/geopackage+sqlite3" ;
    schema:sha256 "f88ac1fae96fba33c9702834eb19e762ac0213c57d2b3a4bdc1b89a85982e2f8" .

ex:file_ring75_150 a prov:Entity ;
    rdfs:label "Buffer ring 75-150m" ;
    prov:generatedAtTime "2026-07-13T17:44:17.265000+02:00"^^xsd:dateTime ;
    prov:type ex:GeoPackageFile ;
    prov:wasDerivedFrom ex:multiLevelBuffers ;
    prov:wasGeneratedBy ex:act8_exportOutputs ;
    schema:contentUrl "outputs/diff_75m-150m.gpkg" ;
    schema:encodingFormat "application/geopackage+sqlite3" ;
    schema:sha256 "04f4bf3280175f9b1aa6189bc54cc78f9e07f2ed5bbbdc862dcaf58512c6d14b" .

ex:finalOutputPackage a prov:Collection,
        prov:Entity ;
    rdfs:label "Exported spatial outputs" ;
    prov:generatedAtTime "2026-07-13T17:44:17.300000+02:00"^^xsd:dateTime ;
    prov:hadMember ex:file_buffer,
        ex:file_city,
        ex:file_coolSpots,
        ex:file_coolSpotsFiltered,
        ex:file_diff,
        ex:file_ring0_75,
        ex:file_ring150_225,
        ex:file_ring225_300,
        ex:file_ring75_150 ;
    prov:type prov:Collection,
        ex:OutputPackage ;
    prov:wasGeneratedBy ex:act8_exportOutputs .

ex:nominatimApi a prov:Entity ;
    rdfs:label "Nominatim geocoding API" ;
    prov:type schema:WebAPI ;
    schema:url "https://nominatim.openstreetmap.org/" .

ex:openStreetMap a prov:Entity ;
    rdfs:label "OpenStreetMap" ;
    dcterms:license "https://opendatacommons.org/licenses/odbl/1-0/" ;
    prov:type prov:PrimarySource ;
    schema:url "https://www.openstreetmap.org" .

ex:overpassApi a prov:Entity ;
    rdfs:label "Overpass API" ;
    prov:type schema:WebAPI ;
    schema:softwareVersion "0.7.62.11 87bfad18" ;
    schema:url "https://overpass-api.de/api" .

ex:rawOsmData a prov:Entity ;
    rdfs:label "Raw OSM vector data (EPSG:4326)" ;
    dcterms:license "https://opendatacommons.org/licenses/odbl/1-0/" ;
    prov:generatedAtTime "2026-07-13T17:44:05.800000+02:00"^^xsd:dateTime ;
    prov:hadPrimarySource ex:openStreetMap ;
    prov:type ex:OsmDataset ;
    prov:wasGeneratedBy ex:act2_acquireData ;
    ex:crs "EPSG:4326" ;
    ex:osmBaseTimestamp "2026-07-13T13:54:30Z" .

ex:unservedAreas a prov:Entity ;
    rdfs:label "Areas outside defined cool spot range" ;
    prov:generatedAtTime "2026-07-13T17:44:16.900000+02:00"^^xsd:dateTime ;
    prov:type ex:VectorDataset ;
    prov:wasDerivedFrom ex:cityBoundary,
        ex:multiLevelBuffers,
        ex:primaryBuffers ;
    prov:wasGeneratedBy ex:act7_calcDifferences .

ex:primaryBuffers a prov:Entity ;
    rdfs:label "300m buffers around cool spots" ;
    prov:generatedAtTime "2026-07-13T17:44:09.100000+02:00"^^xsd:dateTime ;
    prov:type ex:VectorDataset ;
    prov:wasDerivedFrom ex:filteredCoolSpots ;
    prov:wasGeneratedBy ex:act5_buffer300m .

ex:reprojectedData a prov:Entity ;
    rdfs:label "UTM Projected OSM data" ;
    prov:generatedAtTime "2026-07-13T17:44:06.400000+02:00"^^xsd:dateTime ;
    prov:type ex:VectorDataset ;
    prov:wasDerivedFrom ex:rawOsmData ;
    prov:wasGeneratedBy ex:act3_reproject ;
    ex:crs "EPSG:32632" .

<https://orcid.org/0000-0003-4718-2959> a prov:Agent,
        prov:Person ;
    rdfs:label "GIS Analyst" ;
    prov:type prov:Person ;
    schema:identifier "https://orcid.org/0000-0003-4718-2959" .

ex:cityBoundary a prov:Entity ;
    rdfs:label "Münster city boundary (EPSG:4326)" ;
    prov:generatedAtTime "2026-07-13T17:43:41.900000+02:00"^^xsd:dateTime ;
    prov:hadPrimarySource ex:openStreetMap ;
    prov:type ex:VectorDataset ;
    prov:wasGeneratedBy ex:act2a_geocodeCity ;
    ex:crs "EPSG:4326" .

ex:processInputs a prov:Entity ;
    rdfs:label "Workflow Parameters" ;
    prov:generatedAtTime "2026-07-13T17:43:40+02:00"^^xsd:dateTime ;
    prov:type ex:WorkflowInputs ;
    prov:wasAttributedTo <https://orcid.org/0000-0003-4718-2959> ;
    prov:wasGeneratedBy ex:act1_defineInputs ;
    ex:bufferIntervals 0,
        75,
        150,
        225,
        300 ;
    ex:distance 300 ;
    ex:location "Münster, Germany" ;
    ex:minArea 200 ;
    ex:osmTags "landuse=forest, natural=wood, leisure=park" .

ex:filteredCoolSpots a prov:Entity ;
    rdfs:label "Cool spots filtered by min area (>=200m²)" ;
    prov:generatedAtTime "2026-07-13T17:44:06.700000+02:00"^^xsd:dateTime ;
    prov:type ex:VectorDataset ;
    prov:wasDerivedFrom ex:reprojectedData ;
    prov:wasGeneratedBy ex:act4_filterAreas .

ex:multiLevelBuffers a prov:Entity ;
    rdfs:label "Multi-level buffer zones" ;
    prov:generatedAtTime "2026-07-13T17:44:15.900000+02:00"^^xsd:dateTime ;
    prov:type ex:VectorDataset ;
    prov:wasDerivedFrom ex:filteredCoolSpots ;
    prov:wasGeneratedBy ex:act6_bufferMultiLevel .

ex:act8_exportOutputs a prov:Activity ;
    rdfs:label "Step 8: Export process outputs" ;
    dcterms:isPartOf "ex:workflowRun" ;
    prov:endedAtTime "2026-07-13T17:44:17.300000+02:00"^^xsd:dateTime ;
    prov:startedAtTime "2026-07-13T17:44:17+02:00"^^xsd:dateTime ;
    prov:type ex:exportOutputs ;
    prov:used ex:cityBoundary,
        ex:filteredCoolSpots,
        ex:multiLevelBuffers,
        ex:primaryBuffers,
        ex:reprojectedData,
        ex:unservedAreas ;
    prov:wasAssociatedWith ex:gisPipelineEngine .

ex:gisPipelineEngine a prov:Agent,
        prov:SoftwareAgent,
        acttype:WorkflowRunner ;
    rdfs:label "Automated Spatial Workflow Runner" ;
    prov:actedOnBehalfOf <https://orcid.org/0000-0003-4718-2959> ;
    prov:type prov:SoftwareAgent,
        acttype:WorkflowRunner ;
    schema:softwareRequirements "Python 3.13.3",
        "geopandas 1.1.4",
        "osmnx 2.1.0",
        "shapely 2.1.2" .


```

## Schema

```yaml
$schema: https://json-schema.org/draft/2020-12/schema
$ref: https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/prov-profiles/workflow-graph/schema.yaml
x-jsonld-prefixes:
  ex: https://example.org/cool-spots#
  schema: https://schema.org/
x-bblocks-metadata:
  itemIdentifier: ogc.osc.prov-examples.52n-provenance.cool-spots
  register: https://ogcincubator.github.io/bblocks-openscience/build/register.json
  version: '0.1'
  dateOfLastChange: '2026-11-24'

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/prov-examples/52n-provenance/cool-spots/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/prov-examples/52n-provenance/cool-spots/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "wasInfluencedBy": {
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
        "length": "dct:extent"
      },
      "@id": "prov:wasInfluencedBy",
      "@type": "@id"
    },
    "qualifiedInfluence": {
      "@context": {
        "influencer": {
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
            "length": "dct:extent"
          },
          "@id": "prov:influencer",
          "@type": "@id"
        },
        "agent": {
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
            "length": "dct:extent"
          },
          "@id": "prov:agent",
          "@type": "@id"
        }
      },
      "@id": "prov:qualifiedInfluence",
      "@type": "@id"
    },
    "hadMember": {
      "@id": "prov:hadMember",
      "@type": "@id"
    },
    "id": "@id",
    "provType": "@type",
    "entityType": {
      "@id": "prov:type",
      "@type": "@id"
    },
    "name": "rdfs:label",
    "wasGeneratedBy": {
      "@id": "prov:wasGeneratedBy",
      "@type": "@id"
    },
    "wasAttributedTo": {
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
    "links": {
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
        "length": "dct:extent"
      },
      "@id": "rdfs:seeAlso"
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
    "activityType": {
      "@id": "prov:type",
      "@type": "@id"
    },
    "startedAtTime": {
      "@id": "prov:startedAtTime",
      "@type": "xsd:dateTime"
    },
    "endedAtTime": {
      "@id": "prov:endedAtTime",
      "@type": "xsd:dateTime"
    },
    "wasAssociatedWith": {
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
        "length": "dct:extent"
      },
      "@id": "prov:wasAssociatedWith",
      "@type": "@id"
    },
    "wasInformedBy": {
      "@id": "prov:wasInformedBy",
      "@type": "@id"
    },
    "used": {
      "@id": "prov:used",
      "@type": "@id"
    },
    "wasStartedBy": {
      "@id": "prov:wasStartedBy",
      "@type": "@id"
    },
    "wasEndedBy": {
      "@id": "prov:wasEndedBy",
      "@type": "@id"
    },
    "invalidated": {
      "@id": "prov:invalidated",
      "@type": "@id"
    },
    "generated": {
      "@id": "prov:generated",
      "@type": "@id"
    },
    "qualifiedUsage": {
      "@id": "prov:qualifiedUsage",
      "@type": "@id"
    },
    "qualifiedCommunication": {
      "@id": "prov:qualifiedCommunication",
      "@type": "@id"
    },
    "qualifiedStart": {
      "@id": "prov:qualifiedStart",
      "@type": "@id"
    },
    "qualifiedEnd": {
      "@id": "prov:qualifiedEnd",
      "@type": "@id"
    },
    "qualifiedAssociation": {
      "@id": "prov:qualifiedAssociation",
      "@type": "@id"
    },
    "agentType": {
      "@id": "prov:type",
      "@type": "@id"
    },
    "actedOnBehalfOf": {
      "@id": "prov:actedOnBehalfOf",
      "@type": "@id"
    },
    "qualifiedDelegation": {
      "@id": "prov:qualifiedDelegation",
      "@type": "@id"
    },
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
    "provenanceUriTemplate": "prov:provenanceUriTemplate",
    "pairKey": {
      "@id": "prov:pairKey",
      "@type": "rdfs:Literal"
    },
    "removedKey": {
      "@id": "prov:removedKey",
      "@type": "rdfs:Literal"
    },
    "agent": {
      "@id": "prov:agent",
      "@type": "@id"
    },
    "entity": {
      "@id": "prov:entity",
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
    "influenceType": {
      "@id": "prov:type",
      "@type": "@id"
    },
    "label": "rdfs:label",
    "prov": "http://www.w3.org/ns/prov#",
    "xsd": "http://www.w3.org/2001/XMLSchema#",
    "rdfs": "http://www.w3.org/2000/01/rdf-schema#",
    "dct": "http://purl.org/dc/terms/",
    "rdf": "http://www.w3.org/1999/02/22-rdf-syntax-ns#",
    "foaf": "http://xmlns.com/foaf/0.1/",
    "schema": "https://schema.org/",
    "wfprov": "http://purl.org/wf4ever/wfprov#",
    "wfdesc": "http://purl.org/wf4ever/wfdesc#",
    "wf4ever": "http://purl.org/wf4ever/wf4ever#",
    "oa": "http://www.w3.org/ns/oa#",
    "dcterms": "http://purl.org/dc/terms/",
    "skos": "http://www.w3.org/2004/02/skos/core#",
    "acttype": "https://w3id.org/ogc/rim/activity-type/",
    "ex": "https://example.org/cool-spots#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/prov-examples/52n-provenance/cool-spots/context.jsonld)

## Sources

* [VelocityAdapt](https://velocityadapt.de/)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-openscience](https://github.com/ogcincubator/bblocks-openscience)
* Path: `_sources/prov-examples/52n-provenance/cool-spots`

