# HARTIS CVI Workflow Provenance

This candidate Building Block describes provenance for the complete HARTIS
Coastal Vulnerability Index workflow. It is deliberately workflow-specific:
the profile connects the workflow definition and planned processing steps to
the runtime activities and their input and output entities.

The candidate covers the following chain:

1. configuration and source data preparation;
2. coastline extraction;
3. transect generation;
4. land-cover, slope, erosion and elevation calculations; and
5. final CVI calculation and GeoJSON result generation.

The profile is developed locally in the HARTIS repository first. It is not an
official OGC Register entry or a mature shared Building Block until reviewed
and accepted through the relevant OGC contribution process.

## Relationship to shared provenance

The candidate is intended to align with the common OGC PROV Building Block and
the shared processing-step profile. Its additional value is the explicit
representation of the complete CVI workflow, including design-time plans,
runtime activities, data entities and the links between them.
