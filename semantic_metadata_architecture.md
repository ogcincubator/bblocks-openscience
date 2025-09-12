# Semantic Metadata Ecosystem Architecture: STAC-DCAT-PROV-Workflows Integration

## Architectural Vision

By leveraging common semantic models tied to modular metadata schemas, we can achieve unified descriptions for both datasets and their processing workflows. 

This means that translation of metadata into forms needed by different platforms is limited to simple structural transformation, since the common semantic base is already established.

Such semantically explicit metadata can be used to create an integrated knowledge graph where data discovery, workflow reproducibility, and provenance tracking become seamless operations within a single, extensible framework.

The goal is to create an ecosystem that scales to address both different platform needs and additional descriptive expression as needed, without becoming unmaintainable.  It builds on the success of the STAC extension model whilst mitigating its tendencies to create overlapping and inconsistent solutions to common problems. 

## Feasibility

The feasibility of this approach leverages STAC extensions that already encode rich domain semantics - by linking these schemas to semantic models, these semantic models can be included in rich workflow descriptions through the "Open Science Ontology", which in practice will be a suite of profiles of existing standard ontologies combined to meet the needs of workflow reusability. 

Although this represents a significant innovation, the research will be to test a body of existing standards and OGC Building Blocks supporting the integration and profiling of these standards.  OGC Building Blocks provides a solution for the extremely difficult task of mapping schemas to ontologies in a scalable, testable way.

## Existing Building Blocks 

### Ready to use (test)

- **OGC Main** 
  Common schema elements from OGC standard used in multiple places 
  - GeoJSON
  - FG-JSON
  - JSON-LINK
  - BBOX
  - etc
- **OGC API Common**
- **OGC API Features**
- **OGC API Records**
- **OMS/SOSA JSON schema** for Observation Features
- **PROV** JSON schema
- **Cross-domain-model** (standard ontologies)

### Partially developed
- **STAC extensions**
- **GeoDCAT** and profiles

### Required
Given OSPD scope the following sets of Building Blocks would be required  
- **OGC API Processes**
- **Open Science Workflow Ontology**
- **Open Science API Processes Profiles**

note that CI/CT for transformations from workflow descriptions to alternative platform-specific encodings could be managed in separate repositories if required, or done as part of ontology testing.

### Potential
(may be developed by other activites and leveraged)

- **ISO 19115 JSON** core and profiles
- **GeoSPARQL V2** (modular version)
- **ISO 19157 Data Quality Measures** (supporting ontology and JSON schemas)

## Core Architectural Principles

### 1. Semantic Coherence Through Shared Vocabularies
- **Common Ontological Foundation**: PROV-O provides the backbone for all provenance relationships
- **Domain-Specific Extensions**: STAC extension semantics map to specialized ontologies (these can be derived from descriptions)
- **Workflow Integration**: OGC API Processes descriptions share the same semantic patterns as dataset metadata
- **Cross-Domain Linking**: Entities can be simultaneously datasets (DCAT), workflow inputs/outputs (PROV), and processing artifacts (OGC API Processes)

### 2. Modular Schema Composition

A baseline could look somethign like:

```
Base Building Block (OGC API Records + DCAT)
├── + STAC Core → Spatiotemporal Assets
├── + STAC Extensions → Domain Specialization
├── + PROV Building Block → Provenance Tracking
└── + OGC API Processes → Workflow Description
```

### 3. Unified Resource Identification
Resources exist simultaneously as:
- **STAC Items/Collections**: Discoverable spatiotemporal assets
- **DCAT Datasets/Distributions**: Catalog-described data resources  
- **PROV Entities**: Inputs, outputs, and intermediate products in provenance chains
- **OGC API Process I/O**: Parameters and results in workflow definitions

## Semantic Integration Layers

### Layer 1: Foundation Semantics (PROV-O + DCAT)
```turtle
# Base semantic framework
@prefix prov: <http://www.w3.org/ns/prov#> .
@prefix dcat: <http://www.w3.org/ns/dcat#> .

# A dataset is simultaneously a DCAT Dataset and PROV Entity
:satellite_imagery_collection
    a dcat:Dataset, prov:Entity ;
    dcat:title "Sentinel-2 L2A Collection" ;
    prov:wasGeneratedBy :atmospheric_correction_process .
```

### Layer 2: STAC Extension Semantics
```turtle
# STAC EO extension maps to Earth Observation ontology
@prefix eo: <http://www.opengis.net/ont/eo#> .
@prefix stac: <http://www.opengis.net/ont/stac#> .

:sentinel2_item
    a stac:Item, dcat:Dataset, prov:Entity ;
    eo:hasInstrument :msi_sensor ;
    eo:hasPlatform :sentinel2a_satellite ;
    stac:eo_cloud_cover 15.3 ;
    prov:wasGeneratedBy :l2a_processing_activity .
```

### Layer 3: Workflow Process Semantics
```turtle
# OGC API Processes aligned with PROV Activities
@prefix ogcproc: <http://www.opengis.net/ont/ogc-api-processes#> .

:atmospheric_correction_process
    a ogcproc:Process, prov:Activity ;
    ogcproc:hasInput :l1c_imagery ;
    ogcproc:hasOutput :l2a_imagery ;
    prov:used :dem_data, :atmospheric_model ;
    prov:generated :l2a_imagery .
```

## Building Block Architecture

### 1. Semantic Building Blocks Registry
```yaml
stac-eo-dcat-profile:
  inherits: [geodcat-base, stac-core, prov-schema]
  schema: stac-eo-extension.schema.yaml
  context: 
    - https://schemas.stacspec.org/v1.0.0/item-spec/json-schema/item.json#/$defs/eo
    - geodcat-mappings.jsonld
    - eo-ontology-context.jsonld
    - prov-context.jsonld
```

### 2. Workflow-Aware Metadata Profiles
```yaml
processing-workflow-profile:
  inherits: [ogc-api-processes-base, prov-schema]
  semantic_alignment:
    ogc:Process → prov:Activity
    ogc:Input → prov:Entity
    ogc:Output → prov:Entity  
    ogc:Job → prov:Activity (instance)
  links_to: [stac-profiles, dcat-profiles]
```

### 3. Cross-Domain Linking Patterns
```json
{
  "@context": {
    "stac": "http://www.opengis.net/ont/stac#",
    "prov": "http://www.w3.org/ns/prov#",
    "dcat": "http://www.w3.org/ns/dcat#"
  },
  "@type": ["stac:Item", "dcat:Dataset", "prov:Entity"],
  "id": "sentinel2-l2a-20231201",
  "prov:wasGeneratedBy": {
    "@type": ["prov:Activity", "ogc:ProcessExecution"],
    "prov:used": [
      {
        "@id": "sentinel2-l1c-20231201",
        "@type": ["stac:Item", "prov:Entity"]
      }
    ]
  }
}
```

## Implementation Architecture

### 1. Modular Profile Generation
- **Extension Analysis Engine**: Extracts semantic patterns from participant STAC extensions
- **Ontology Mapping Service**: Aligns extension properties with domain vocabularies
- **Profile Composer**: Combines base building blocks with extension-specific semantics
- **Validation Framework**: Ensures semantic consistency across profile combinations

### 2. Provenance Integration Points
- **STAC Processing Extension**: Enhanced with PROV-O semantics for lineage tracking
- **Collection-Level Provenance**: Describes processing pipelines that generate entire collections
- **Cross-Collection Dependencies**: Links derived products to source collections via provenance chains
- **Workflow Reproducibility**: Embeds sufficient provenance to enable workflow recreation

### 3. OGC API Processes Integration
- **Process Description Alignment**: Map process metadata to same vocabularies as dataset metadata  
- **I/O Semantic Typing**: Use STAC extension vocabularies to type process inputs/outputs
- **Workflow Composition**: Enable clients to integrate discovered data and processes as a workflow in an ad-hoc manner
- **Execution Provenance**: Automatic PROV generation from process execution

## Semantic Consistency Patterns

### 1. Vocabulary Alignment Matrix
```
STAC Extension Property → Domain Ontology → PROV Role → OGC Process Type
eo:cloud_cover → eo:CloudCover → prov:qualifier → ogc:QualityMetric  
sar:polarizations → radar:Polarization → prov:parameter → ogc:InputSpec
projection:epsg → crs:CoordinateSystem → prov:location → ogc:SpatialContext
```

### 2. Cross-Profile Validation Rules
- **Semantic Type Consistency**: Entities maintain consistent typing across STAC/DCAT/PROV views
- **Provenance Chain Integrity**: Processing relationships valid across workflow and dataset descriptions  
- **Vocabulary Coherence**: Extension-specific terms properly grounded in domain ontologies
- **Profile Composition**: Combined profiles maintain semantic consistency

### 3. Knowledge Graph Views
```sparql
# Query spanning datasets, workflows, and provenance
SELECT ?dataset ?process ?sensor WHERE {
  ?dataset a stac:Item, dcat:Dataset ;
           eo:hasInstrument ?sensor ;
           prov:wasGeneratedBy ?process .
  
  ?process a prov:Activity, ogc:Process ;
           ogc:hasInput ?input_data .
           
  ?sensor eo:onPlatform ?platform .
}
```

## Value Realization

### 1. Unified Discovery
- Single query interface across datasets and processing capabilities
- Semantic reasoning enables discovery of compatible data-process combinations
- Provenance-aware search finds all products derived from specific source data

### 2. Reproducible Science
- Complete provenance capture from STAC metadata and OGC API Processes execution
- Workflow descriptions use same semantic foundation as data descriptions
- Automatic validation ensures reproducibility requirements are met

### 3. Interoperability at Scale  
- Common semantic foundation enables cross-domain data integration
- Modular building blocks support domain-specific extensions while maintaining coherence
- Standards-based approach ensures broad adoption and tool compatibility

### 4. Knowledge Graph Analytics
- Integrated view enables sophisticated analysis across data lineage
- Machine-readable semantics support automated workflow optimization
- Cross-domain queries reveal insights impossible with siloed metadata

This architecture leverages the inherent semantic richness already present in STAC extensions, the proven PROV building block pathway to incorporate provenance data into OGC API environments, and the OGC API - Processes standard that enables execution of computing processes and retrieval of metadata describing their purpose and functionality. The result is a coherent semantic ecosystem where datasets, workflows, and provenance are described using consistent, interoperable vocabularies.