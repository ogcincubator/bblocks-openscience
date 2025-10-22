# A FAIR workflow Architecture using OGC standards

## Outline

The business [goals](#goals) are described in terms of what needs to be achieved, and an "[architectural vision](#architectural-vision)" describes how this can be done.

[Feasibility](#Feasibility) considers the realities of a short project cycle, in terms of constraining scope of the project whilst validating extensibility of the solution.

[Existing Building Blocks](#existing-building-blocks) provides an inventory of existing elements that already provide access to existing OGC standards and potential standardisable elements, and conform to a common semantic documentation framework. 

[Core Architectural Principles](#core-architectural-principles) documents considerations that will guide design of clean, integratable components for such an ecosystem

[Semantic Integration Layers](#semantic-integration-layers) provide simple examples 

[Implementation Architecture](#implementation-architecture) outlines a systematic roadmap to building and testing this approach.

## Goals

### 1. Interoperable workflows
- Common semantic framework to support workflow description
- Translation of workflows between platforms
- Integrated provenance from workflows executed in different platforms

i.e. Both the workflows and experiments (configured and executed workflows) are interoperable, and can be combined in a coherent ecosystem.

### 2. Reproducible Science
- Complete provenance capture from metadata and workflow execution
- Workflow descriptions use same semantic foundation as data descriptions
- Automatic validation ensures reproducibility requirements are met

### 3. Interoperability at Scale  
- Common semantic foundation enables cross-domain data integration
- Modular building blocks support domain-specific extensions while maintaining coherence
- Standards-based approach ensures broad adoption and tool compatibility

### 4. Unified Discovery  
- Single query interface across datasets and processing capabilities
- Semantic reasoning enables discovery of compatible data-process combinations
- Provenance-aware search finds all products derived from specific source data
- 
### 5. Knowledge Graph Analytics
- Integrated view enables sophisticated analysis across data lineage
- Machine-readable semantics support automated workflow optimization
- Cross-domain queries reveal insights impossible with siloed metadata

This architecture leverages the inherent semantic richness already present in STAC extensions, the proven PROV building block pathway to incorporate provenance data into OGC API environments, and the OGC API - Processes standard that enables execution of computing processes and retrieval of metadata describing their purpose and functionality. The result is a coherent semantic ecosystem where datasets, workflows, and provenance are described using consistent, interoperable vocabularies.

## Architectural Vision

By leveraging common semantic models tied to modular metadata schemas, we can achieve unified descriptions for both datasets and their processing workflows. 

This means that translation of metadata into forms needed by different platforms is limited to simple structural transformation, since the common semantic base is already established.

Such semantically explicit metadata can be used to create an integrated knowledge graph where data discovery, workflow reproducibility, and provenance tracking become seamless operations within a single, extensible framework.

The goal is to create an ecosystem that scales to address both different platform needs and additional descriptive expression as needed, without becoming unmaintainable.  It builds on the success of the STAC extension model whilst mitigating its tendencies to create overlapping and inconsistent solutions to common problems. 

## Feasibility

The feasibility of this approach leverages STAC extensions that already encode rich domain semantics - by linking these schemas to semantic models, these semantic models can be included in rich workflow descriptions through the "Open Science Ontology", which in practice will be a suite of profiles of existing standard ontologies combined to meet the needs of workflow reusability. 

Although this represents a significant innovation, the research will be to test a body of existing standards and OGC Building Blocks supporting the integration and profiling of these standards.  OGC Building Blocks provides a solution for the extremely difficult task of mapping schemas to ontologies in a scalable, testable way.

Given the availability of tooling and foundational semantic elements of such an ecosystem and a pragmatic leveraging of existing STAC semantics, developing a candidate common open "science ontology", and testing it with these shared semantics and any application specific descriptions is feasible.

Standardising specific application domain semantics is not feasible, however showing how these may be defined in a form that can be added to a standards ecosystem provides a pathway to future standardisation.

## Existing Building Blocks

### Ready to use (test)

- **[OGC Main](https://opengeospatial.github.io/bblocks/register/)** 
  Common schema elements from OGC standard used in multiple places 
  - GeoJSON
  - FG-JSON
  - JSON-LINK
  - BBOX
  - etc
- **[OGC API Features](https://ogcincubator.github.io/bblocks-ogcapi-features/)**
- **[OGC API Records](https://ogcincubator.github.io/bblocks-ogcapi-records/)**
- **[OMS/SOSA JSON schema for Observation Features](https://opengeospatial.github.io/ogcapi-sosa/)**
- **[PROV-JSONLD](https://ogcincubator.github.io/bblock-prov-schema/)** JSON schema
- **[Cross-domain-model](https://ogcincubator.github.io/cross-domain-model/)** - standard ontologies and OGC profiles for best practices

### Partially developed
- **STAC extensions**
- **GeoDCAT** and profiles


### Required
Given OSPD scope the following sets of Building Blocks would be required  
- **[OGC API Processes](https://github.com/ogcincubator/bblocks-ogcapi-processes)**
- **Open Science Workflow Ontology**
- **[Open Science API Processes Profiles](https://github.com/ogcincubator/bblocks-openscience)**

note that CI/CT for transformations from workflow descriptions to alternative platform-specific encodings could be managed in separate repositories if required, or done as part of ontology testing.

### Potential
(may be developed by other activites and leveraged)

- **ISO 19115 JSON** core and profiles
- **GeoSPARQL V2** (modular version)
- **ISO 19157 Data Quality Measures** (supporting ontology and JSON schemas)

## Core Architectural Principles

### 1. Semantic Coherence Through Shared Vocabularies

Irrespective of the various encodings and communication protocols used to transfer data and metadata, **when common concepts are used this should be identifiable**.

The rationale is very simple - simply consider the same term located in several different data sources with different schemas, and the amount of effort required to:

a. determine if content has the same meaning
b. communicate this to an audience examining the reliability of your reasoning
c. encode the instructions to treat this content as semantically equivalent
d. implement data processing steps that exploit these instructions
e. document the data processing in a transparent, repeatable and reproducible way.

The choice is to do this either:

- once, as part of metadata design for reusable data and processing,
- every time a workflow is created using these resources
- post-facto to try to understand and reproduce 

In an Open Science context, the following common patterns can be observed where 

- **Common Ontological Foundation**: PROV-O provides the backbone for all provenance relationships
- **Domain-Specific Extensions**: STAC extension semantics map to specialized ontologies (these can be derived from descriptions)
- **Workflow Integration**: OGC API Processes descriptions share the same semantic patterns as dataset metadata
- **Cross-Domain Linking**: Entities can be simultaneously datasets (DCAT), workflow inputs/outputs (PROV), and processing artifacts (OGC API Processes)

### 3. Unified Resource Identification

In order to 

Resources exist simultaneously as:
- **STAC Items/Collections**: Discoverable spatiotemporal assets
- **DCAT Datasets/Distributions**: Catalog-described data resources  
- **PROV Entities**: Inputs, outputs, and intermediate products in provenance chains
- **OGC API Process I/O**: Parameters and results in workflow definitions




### 2. Modular Schema Composition

A baseline could look something like:

```
Base Building Block (OGC API Records + DCAT)
├── + STAC Core → Spatiotemporal Assets
├── + STAC Extensions → Domain Specialization
├── + PROV Building Block → Provenance Tracking
└── + OGC API Processes → Workflow Description
```

Breaking this down into FAIR components - i.e. focus on tight scope control for reusability, the following repository architecture emerges:

[diagram](overview.png)

## Semantic Integration Layers

Some examples (placeholders) for how things will link in practice RDF and equivalent  JSON instance data (or vice versa?).

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



## Implementation Architecture

### 1. Modular Profile Generation

Tooling and training to empower participants to establish a collaborative test-driven rapid prototyping environment.

- **Extension Analysis Engine**: Extracts semantic patterns from participant STAC extensions
- **Ontology Mapping Service**: Aligns extension properties with domain vocabularies
- **Profile Composer**: Combines base building blocks with extension-specific semantics
- **Validation Framework**: Ensures semantic consistency across profile combinations

### 2. Open Science Ontology Design
- **STAC Processing Extension**: Enhanced with PROV-O semantics for lineage tracking
- **Collection-Level Provenance**: Describes processing pipelines that generate entire collections
- **Cross-Collection Dependencies**: Links derived products to source collections via provenance chains
- **Workflow Reproducibility**: Embeds sufficient provenance to enable workflow recreation

### 3. OGC API Processes Integration
- **Process Description Alignment**: Map process metadata to same vocabularies as dataset metadata  
- **I/O Semantic Typing**: Use STAC extension vocabularies to type process inputs/outputs
- **Workflow Composition**: Enable clients to integrate discovered data and processes as a workflow in an ad-hoc manner
- **Execution Provenance**: Automatic PROV generation from process execution



