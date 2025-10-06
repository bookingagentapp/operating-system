# Glossary

Domain terminology and definitions used throughout the application.

## Overview

This glossary defines terms specific to the BookingAgent domain. Use it as a reference when writing documentation or code to ensure consistent terminology.

## Core Terms

### Tenant

A single organization using the BookingAgent system. Each tenant has its own isolated database with users, and configurations. See [[concepts/multi-tenancy]].

### Central Database

The shared PostgreSQL database containing globally accessible entities like Artists, Venues, and Accommodations. See [[concepts/multi-tenancy]].

### Entity Access

Permission system that controls which tenants can access central database entities. Implemented via [[components/EntityAccess]] model.

### User Identity

Central registry of all users across all tenants. Enables cross-tenant invitations and collaboration. See [[components/UserIdentity]].

### Tenant Membership

Represents a user's membership in a specific tenant. One user can belong to multiple tenants. See [[components/TenantMembership]].

## Entities

### Artist

Global entity representing a musical artist. Stored in central database, accessible across tenants with permissions. See [[components/Artist]].

### Venue

Global entity representing a performance venue with spaces and amenities. See [[components/Venue]].

### Accommodation

Global entity for lodging options. See [[components/Accommodation]].

### Person

Global contact record representing an individual. Can be assigned to entities via contactables. See [[components/Person]].

### Company

Tenant-specific organization record. See [[components/Company]].

### Contact

Polymorphic assignment of Person or Company to entities within a tenant. See [[concepts/contact-model]].

## Technical Terms

### Polymorphic Relationship

Laravel pattern where a model can belong to multiple other models. Used for Spaces, Amenities, Attachments, Comments.

### Hybrid ID Strategy

Using integer primary keys for performance with UUID public identifiers for APIs. See [[concepts/hybrid-ids]].

### Strategy Pattern

Encapsulating entity-specific logic in dedicated strategy classes. See [[concepts/strategy-pattern]].

### Central Connection

Laravel trait forcing a model to always use the central database. See [[components/CentralConnection]].

### Contactable

Any entity that can have Person or Company contacts assigned. Uses [[components/HasContactables]] trait.

## Integration Terms

### Viberate

External API providing artist and venue data enrichment. See [[components/ViberateService]].

### Echo Framework

WebSocket management for real-time features. Used for real-time notifications and updates.

## Related

- See [[Concepts]] for detailed concept explanations
- See [[Components]] for implementation details
