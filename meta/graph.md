---
title: Knowledge Graph
type: meta
status: draft
updated: 2025-10-04
---

# Knowledge Graph

Visual representation of relationships between entities, concepts, and flows.

## Overview

This document will contain relationship diagrams showing how concepts, components, and flows interconnect. Currently a placeholder for future OPM (Object-Process Methodology) or similar notation.

## Core Relationships

```
Artist (Central)
  ├─ has → EntityAccess (permissions)
  ├─ has → Genre (many-to-many)
  ├─ has → Person (via HasContactables)
  └─ syncs ← ViberateService

Venue (Central)
  ├─ has → EntityAccess
  ├─ has → Space (polymorphic)
  ├─ has → Amenity (polymorphic)
  ├─ has → VenueCategory
  └─ has → Address

User (Tenant)
  ├─ maps to → UserIdentity (central)
  ├─ belongs to → TenantMembership
  └─ has → EntityUserAccess (delegated permissions)

Tenant (Isolation Boundary)
  ├─ owns → User
  ├─ owns → Company
  ├─ owns → Contact
  └─ accesses → [Central Entities] via EntityAccess
```

## Concept Dependencies

```
Multi-Tenancy
  ├─ requires → Tenant Isolation
  ├─ requires → Entity Access
  ├─ enables → Cross-Tenant Sharing
  └─ uses → Connection Management

Entity Access
  ├─ implements → Permission System
  ├─ uses → Hybrid IDs
  └─ checked by → HasEntityAccessPermissions

Polymorphic Relationships
  ├─ enables → HasContactables
  ├─ enables → HasSpaces
  ├─ enables → HasAmenities
  └─ requires → Strategy Pattern
```

## Flow Connections

```
User Onboarding
  → creates UserIdentity
  → creates TenantMembership
  → may trigger Cross-Tenant Sharing

Artist Import
  → calls ViberateService
  → creates Artist
  → creates EntityAccess
  → may assign Person (contact)

Permission Resolution
  → checks EntityAccess
  → checks EntityUserAccess
  → validates Tenant Context
  → returns Access Level
```

## Future Enhancements

This section will evolve to include:

- OPM diagrams for complex processes
- Dependency graphs for services
- Data flow diagrams
- Component interaction maps
- State machine diagrams

## Tools

Consider using:

- Mermaid for inline diagrams
- Excalidraw for sketches
- PlantUML for formal diagrams
- Obsidian Canvas for visual maps

## Related

- See [[Concepts]] for individual concept docs
- See [[Components]] for component details
- See [[Flows]] for process flows
