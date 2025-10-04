# Components

System components, models, services, and their interactions.

## Overview

This section documents the building blocks of the application. Components can be models, traits, services, Livewire components, or any discrete piece of functionality.

## Models

### Central Database Models

- [[components/Artist]] - Global artist entity
- [[components/Venue]] - Venue with spaces and amenities
- [[components/Accommodation]] - Accommodation management
- [[components/Person]] - Global person records
- [[components/Genre]] - Music genre taxonomy
- [[components/EntityAccess]] - Cross-tenant permissions
- [[components/UserIdentity]] - Central user registry
- [[components/TenantMembership]] - User-tenant relationships

### Tenant Database Models

- [[components/User]] - Tenant-specific user
- [[components/Company]] - Tenant companies
- [[components/Contact]] - Contact assignments
- [[components/File]] - File management
- [[components/Notification]] - Notification system

### Polymorphic Models

- [[components/Space]] - Capacity and area tracking
- [[components/Amenity]] - Amenity system
- [[components/Attachment]] - File attachments
- [[components/Comment]] - Comments system

## Traits

- [[components/HasContactables]] - Contact assignment functionality
- [[components/HasSpaces]] - Space management
- [[components/HasAmenities]] - Amenity assignment
- [[components/HasEntityAccessPermissions]] - Permission checking
- [[components/CentralConnection]] - Central database designation
- [[components/AccessibleForTenant]] - Tenant access control

## Services

- [[components/ArtistService]] - Artist business logic
- [[components/VenueService]] - Venue operations
- [[components/ContactService]] - Contact management
- [[components/ViberateService]] - External API integration
- [[components/NotificationService]] - Notification delivery

## Livewire Components

- [[components/livewire/Artists.Show]] - Artist detail page
- [[components/livewire/Venues.Show]] - Venue detail page
- [[components/livewire/Companies.Show]] - Company detail page

## Related

- See [[concepts/index]] for architectural patterns
- See [[flows/index]] for how components work together
- See `/docs/ENTITIES/` for detailed model documentation
