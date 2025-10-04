# Flows

User journeys, data flows, and process diagrams that show how the system operates end-to-end.

## Overview

This section documents how data moves through the system and how users interact with features. Each flow connects multiple [[concepts/index|concepts]] and [[components/index|components]].

## User Flows

- [[flows/user-onboarding]] - New user invitation and tenant membership
- [[flows/artist-import]] - Importing artists from Viberate API
- [[flows/venue-creation]] - Creating venues with spaces and amenities
- [[flows/contact-assignment]] - Assigning contacts to entities
- [[flows/cross-tenant-sharing]] - Sharing resources across tenants

## Data Flows

- [[flows/entity-access-resolution]] - How permissions are resolved
- [[flows/tenant-context-switching]] - Database connection management
- [[flows/file-upload]] - File storage and visibility management
- [[flows/notification-delivery]] - Multi-channel notification pipeline

## Integration Flows

- [[flows/viberate-sync]] - External data synchronization
- [[flows/webhook-processing]] - Incoming webhook handling

## Related

- See [[concepts/index]] for the mental models behind these flows
- See [[components/index]] for implementation details
