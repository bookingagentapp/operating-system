# Concepts

Core mental models and architectural patterns that define how the system works.

## Overview

This section documents the fundamental concepts that underpin the BookingAgent system. Each concept represents a key architectural decision or domain model.

## Key Concepts

### Multi-Tenancy

- [[concepts/multi-tenancy]] - Central vs tenant database architecture
- [[concepts/tenant-isolation]] - Data isolation and cross-tenant access
- [[concepts/entity-access]] - Permission system for shared resources

### Domain Models

- [[concepts/artist-model]] - Global artist entity and relationships
- [[concepts/venue-model]] - Venue spaces and amenities
- [[concepts/accommodation-model]] - Accommodation booking and policies
- [[concepts/contact-model]] - Person and Company management
- [[concepts/user-identity]] - Cross-tenant user identity system

### Architectural Patterns

- [[concepts/entity-scaffolding]] - Standard entity implementation pattern
- [[concepts/polymorphic-relationships]] - Flexible entity associations
- [[concepts/strategy-pattern]] - Entity-specific business logic
- [[concepts/hybrid-ids]] - Integer IDs + UUID pattern

### System Integration

- [[concepts/viberate-integration]] - External API data enrichment
- [[concepts/file-management]] - 4-level visibility system
- [[concepts/notification-system]] - Multi-channel notifications

## Related

- See [[Flows]] for how concepts manifest in user journeys
- See [[Components]] for implementation details
