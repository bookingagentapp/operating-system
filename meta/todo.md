---
title: Documentation Todo List
type: meta
status: active
updated: 2025-10-04
---

# Documentation Todo List

Comprehensive list of components, concepts, flows, and infrastructure that need documentation in the `/os` system.

## Concepts to Document

### Core Architecture

- [ ] `multi-tenancy.md` - Central vs tenant database pattern
- [ ] `tenant-isolation.md` - Data isolation guarantees and context switching
- [ ] `entity-access.md` - Permission system for cross-tenant sharing
- [ ] `entity-scaffolding.md` - Standard entity implementation pattern
- [ ] `hybrid-ids.md` - Integer IDs + UUID strategy
- [ ] `strategy-pattern.md` - Entity-specific business logic encapsulation
- [ ] `polymorphic-relationships.md` - Flexible entity associations

### Domain Models

- [ ] `artist-model.md` - Global artist entity and management
- [ ] `venue-model.md` - Venues with spaces and amenities
- [ ] `accommodation-model.md` - Accommodation booking patterns
- [ ] `contact-model.md` - Person/Company contact management
- [ ] `user-identity.md` - Cross-tenant user identity system
- [ ] `tenant-membership.md` - User-tenant relationship model
- [ ] `company-model.md` - Tenant company entities
- [ ] `space-model.md` - Polymorphic space management
- [ ] `amenity-model.md` - Polymorphic amenity system
- [ ] `genre-model.md` - Music genre taxonomy

### File & Document Management

- [ ] `file-system.md` - File, Directory, Document architecture
- [ ] `file-permissions.md` - 4-level visibility system
- [ ] `attachment-system.md` - Polymorphic attachments
- [ ] `image-processing.md` - Context-aware image processing

### Communication & Activity

- [ ] `notification-system.md` - Multi-channel notification delivery
- [ ] `activity-tracking.md` - Activity items and timeline
- [ ] `comment-system.md` - Polymorphic comments
- [ ] `call-logs.md` - Call tracking system
- [ ] `notes-system.md` - Notes and annotations

### Integration

- [ ] `viberate-integration.md` - External API data enrichment
- [ ] `artist-import.md` - Artist data import from Viberate
- [ ] `venue-import.md` - Venue data import
- [ ] `social-media-sync.md` - Social platform data synchronization

### Permission Architecture

- [ ] `entity-access-resolution.md` - How permissions are resolved
- [ ] `entity-user-access.md` - Delegated user permissions
- [ ] `contact-sync-permissions.md` - Two-layer contact permission system
- [ ] `file-permission-system.md` - File access control

## Flows to Document

### User Workflows

- [ ] `user-onboarding.md` - New user invitation and setup
- [ ] `tenant-switching.md` - User switching between tenants
- [ ] `cross-tenant-invitation.md` - Inviting users to resources
- [ ] `artist-search.md` - Searching and filtering artists
- [ ] `venue-browsing.md` - Finding and viewing venues

### Data Flows

- [ ] `artist-import.md` - Complete Viberate artist import flow
- [ ] `venue-creation.md` - Creating venues with spaces/amenities
- [ ] `accommodation-setup.md` - Setting up accommodations
- [ ] `contact-assignment.md` - Assigning contacts to entities
- [ ] `contact-sync-flow.md` - Contact permission synchronization
- [ ] `entity-access-resolution.md` - Permission checking flow
- [ ] `tenant-context-switching.md` - Database connection management
- [ ] `file-upload.md` - File storage and processing
- [ ] `notification-delivery.md` - Notification creation and delivery
- [ ] `activity-creation.md` - Activity item generation

### Integration Flows

- [ ] `viberate-artist-sync.md` - Artist data synchronization
- [ ] `viberate-venue-sync.md` - Venue data synchronization
- [ ] `social-media-fetch.md` - Fetching social media data
- [ ] `artist-analytics-enrichment.md` - Analytics data updates
- [ ] `geocoding-flow.md` - Address geocoding process

### Administrative Flows

- [ ] `tenant-provisioning.md` - New tenant creation process
- [ ] `role-assignment.md` - Assigning roles to contacts
- [ ] `permission-granting.md` - Granting entity access
- [ ] `user-invitation.md` - Inviting users to tenants

## Components to Document

### Central Database Models

- [ ] `Artist.md` - Global artist model
- [ ] `Venue.md` - Venue model with spaces/amenities
- [ ] `Accommodation.md` - Accommodation model
- [ ] `Person.md` - Global person records
- [ ] `Genre.md` - Music genre model
- [ ] `EntityAccess.md` - Cross-tenant permission model
- [ ] `UserIdentity.md` - Central user registry
- [ ] `TenantMembership.md` - User-tenant relationships
- [ ] `ViberateEvent.md` - Cached Viberate events
- [ ] `ArtistAnalytics.md` - Artist analytics data
- [ ] `ArtistPerformance.md` - Artist performance metrics
- [ ] `VenueCategory.md` - Venue categorization
- [ ] `TenantArtist.md` - Tenant-specific artist data

### Tenant Database Models

- [ ] `User.md` - Tenant-specific user
- [ ] `Company.md` - Tenant company
- [ ] `ContactAssignment.md` - Contact pivot model
- [ ] `File.md` - File management model
- [ ] `Directory.md` - Directory structure
- [ ] `Document.md` - Document model
- [ ] `FilePermission.md` - File permission model
- [ ] `Attachment.md` - Polymorphic attachments
- [ ] `Comment.md` - Polymorphic comments
- [ ] `Note.md` - Notes model
- [ ] `CallLog.md` - Call tracking
- [ ] `ActivityItem.md` - Activity timeline
- [ ] `Notification.md` - Notification model
- [ ] `NotificationRecipient.md` - Notification recipients
- [ ] `NotificationAction.md` - Notification actions
- [ ] `NotificationActionResponse.md` - Action responses
- [ ] `ContactSync.md` - Contact synchronization
- [ ] `EntityUserAccess.md` - Delegated permissions

### Polymorphic Models

- [ ] `Space.md` - Polymorphic space model
- [ ] `Amenity.md` - Polymorphic amenity model
- [ ] `Address.md` - Polymorphic address model
- [ ] `Attachment.md` - Polymorphic attachment model

### Traits

- [ ] `HasContactables.md` - Contact assignment functionality
- [ ] `HasSpaces.md` - Space management trait
- [ ] `HasAmenities.md` - Amenity assignment trait
- [ ] `HasEntityAccessPermissions.md` - Permission checking trait
- [ ] `HasAttachments.md` - Attachment management trait
- [ ] `CentralConnection.md` - Central database designation
- [ ] `AccessibleForTenant.md` - Tenant access control
- [ ] `HasAddresseses.md` - Address management trait
- [ ] `HasRoleEnum.md` - Role enum resolution
- [ ] `HasHierarchy.md` - Hierarchical relationships
- [ ] `ManagesGenres.md` - Genre management
- [ ] `WithSocialMediaAssignment.md` - Social media links
- [ ] `WithAddressFormComponent.md` - Address form handling
- [ ] `WithIntegrationUrlsComponent.md` - Integration URLs
- [ ] `NeedsTenantUrl.md` - Tenant URL generation
- [ ] `Formatters.md` - Data formatting utilities

### Services

#### Core Services

- [ ] `ContactableService.md` - Contact management service
- [ ] `ContactSyncService.md` - Contact permission sync
- [ ] `ContactPermissionService.md` - Contact permission checking
- [ ] `ContactDataTransformer.md` - Contact data transformation
- [ ] `ContactAuditService.md` - Contact audit logging
- [ ] `NotificationService.md` - Notification creation
- [ ] `NotificationDeliveryService.md` - Notification delivery
- [ ] `FilePermissionService.md` - File permission management
- [ ] `AttachmentService.md` - Attachment handling
- [ ] `AddressService.md` - Address management
- [ ] `GlobalSearchService.md` - Global search functionality
- [ ] `CrossTenantUserService.md` - Cross-tenant user operations
- [ ] `CrossTenantInvitationService.md` - Invitation management
- [ ] `CallLogService.md` - Call log management
- [ ] `PageTitleService.md` - Dynamic page titles
- [ ] `WorldLocationService.md` - Location data service
- [ ] `GeocodingService.md` - Address geocoding
- [ ] `GenreService.md` - Genre management
- [ ] `RolesService.md` - Role management

#### Performance & Analytics

- [ ] `PerformanceService.md` - Performance metrics
- [ ] `AnalyticsService.md` - Analytics aggregation
- [ ] `VibrateAnalyticsService.md` - Viberate analytics
- [ ] `VibratePerformanceService.md` - Viberate performance data
- [ ] `VibrateEngagementService.md` - Engagement metrics

#### Infrastructure Services

- [ ] `CacheService.md` - Caching layer
- [ ] `PrivateCacheService.md` - Private cache management
- [ ] `ImageProcessingService.md` - Image processing
- [ ] `FaviconService.md` - Favicon generation

#### Viberate Integration

- [ ] `ViberateService.md` - Main Viberate service
- [ ] `ViberateAPIService.md` - API wrapper
- [ ] `ImportArtistService.md` - Artist import logic
- [ ] `ImportVenueService.md` - Venue import logic

#### Contact Strategies

- [ ] `ContactStrategyFactory.md` - Contact strategy factory
- [ ] Contact strategy implementations (various)

### Livewire Components

#### Artists

- [ ] `Artists.ListComponent.md` - Artist list view
- [ ] `Artists.Show.md` - Artist detail page
- [ ] `Artists.Import.md` - Artist import interface
- [ ] `Artists.Create.md` - Artist creation form

#### Venues

- [ ] `Venues.Show.md` - Venue detail page
- [ ] Venue management components

#### Companies

- [ ] `Companies.Show.md` - Company detail page

#### Persons

- [ ] `Persons.Show.md` - Person detail page

#### Accommodations

- [ ] Accommodation components

#### Widgets

- [ ] Artist widgets (social media, analytics, etc.)

#### Core Components

- [ ] `GlobalSearch.md` - Global search component
- [ ] `NotificationDropdown.md` - Notification dropdown
- [ ] `Settings.md` - Settings management
- [ ] `Roles.md` - Role management component

### Actions

#### Artist Actions

- [ ] `CreateArtist.md` - Artist creation action
- [ ] `UpdateArtistProfile.md` - Artist update action

#### Venue Actions

- [ ] `CreateVenue.md` - Venue creation action
- [ ] `InviteVenueClient.md` - Venue client invitation

#### Contact Actions

- [ ] `AssignContact.md` - Contact assignment action
- [ ] `RemoveContact.md` - Contact removal action
- [ ] `CreatePersonContact.md` - Person contact creation
- [ ] `CreateCompanyContact.md` - Company contact creation
- [ ] `CreatePersonWithCompanyAssignment.md` - Person with company

#### Other Actions

- [ ] Company, Accommodation, Person, Address actions

### Policies

- [ ] `ArtistPolicy.md` - Artist authorization
- [ ] `VenuePolicy.md` - Venue authorization
- [ ] `AccommodationPolicy.md` - Accommodation authorization
- [ ] `PersonPolicy.md` - Person authorization
- [ ] `CompanyPolicy.md` - Company authorization
- [ ] `UserPolicy.md` - User authorization
- [ ] `GenrePolicy.md` - Genre authorization
- [ ] `TenantPolicy.md` - Tenant authorization
- [ ] `RolePolicy.md` - Role authorization
- [ ] `CallLogPolicy.md` - Call log authorization

### Enums

#### Entity Enums

- [ ] `EntityTypeEnum.md` - Entity type definitions
- [ ] `EntityAccessTypeEnum.md` - Access type levels
- [ ] `StatusEnum.md` - Generic status values
- [ ] `GenderEnum.md` - Gender options

#### Artist Enums

- [ ] `ArtistStatus.md` - Artist status values
- [ ] `ArtistTypeEnum.md` - Artist types

#### Venue Enums

- [ ] `VenueStatus.md` - Venue status
- [ ] `VenueCategoryEnum.md` - Venue categories
- [ ] `VenueVisibilityEnum.md` - Venue visibility
- [ ] `VenueAddressTypeEnum.md` - Venue address types

#### Accommodation Enums

- [ ] `AccommodationStatus.md` - Accommodation status
- [ ] `AccommodationTypeEnum.md` - Accommodation types
- [ ] `AccommodationAddressTypeEnum.md` - Address types

#### Space & Amenity Enums

- [ ] `SpaceStatus.md` - Space status
- [ ] `SpaceTypeEnum.md` - Space types
- [ ] `AmenityStatus.md` - Amenity status
- [ ] `AmenityTypeEnum.md` - Amenity categories

#### File & Document Enums

- [ ] `FilePermissionTypeEnum.md` - Permission types
- [ ] `FilePermissionGranteeTypeEnum.md` - Grantee types
- [ ] `AttachmentVisibilityEnum.md` - Attachment visibility
- [ ] `AttachmentContextEnum.md` - Attachment contexts
- [ ] `DocumentType.md` - Document types
- [ ] `DocumentStatus.md` - Document status
- [ ] `MimeTypeEnum.md` - Supported MIME types

#### Activity Enums

- [ ] `ActivityType.md` - Activity types
- [ ] `ActivityStatus.md` - Activity status
- [ ] `ActivityOutcome.md` - Activity outcomes
- [ ] `ActivityPriority.md` - Activity priorities

#### Contact & Role Enums

- [ ] `ContactVisibilityEnum.md` - Contact visibility
- [ ] `ContactSyncSourceEnum.md` - Sync sources
- [ ] `ArtistPersonRoleEnum.md` - Artist-Person roles
- [ ] `ArtistCompanyRoleEnum.md` - Artist-Company roles
- [ ] `VenuePersonRoleEnum.md` - Venue-Person roles
- [ ] `VenueCompanyRoleEnum.md` - Venue-Company roles
- [ ] `AccommodationPersonRoleEnum.md` - Accommodation-Person roles
- [ ] `AccommodationCompanyRoleEnum.md` - Accommodation-Company roles
- [ ] `CompanyPersonRoleEnum.md` - Company-Person roles

#### Other Enums

- [ ] `SocialPlatform.md` - Social media platforms
- [ ] `CompanyCategory.md` - Company categories
- [ ] `AddressTypeEnum.md` - Address types
- [ ] `CallDirectionEnum.md` - Call directions
- [ ] `CallOutcomeEnum.md` - Call outcomes
- [ ] `IntegrationsEnum.md` - Integration types
- [ ] `RateFrequencyEnum.md` - Rate frequencies

### Enum Traits

- [ ] `HasEnumLabels.md` - Enum label functionality

## Infrastructure to Document

### Multi-Tenancy

- [ ] `multi-tenant-database.md` - Database architecture
- [ ] `tenant-provisioning.md` - Tenant creation process
- [ ] `connection-management.md` - Database connection switching
- [ ] `tenant-context.md` - Context management patterns

### Storage & Files

- [ ] `file-storage.md` - S3-compatible storage
- [ ] `image-processing.md` - Image processing pipeline
- [ ] `backup-strategy.md` - Data backup approach

### Jobs & Queues

- [ ] `queue-architecture.md` - Queue system design
- [ ] `job-isolation.md` - Tenant-specific jobs
- [ ] `background-jobs.md` - Job patterns
- [ ] `queue-workers.md` - Worker management

### Caching

- [ ] `cache-strategy.md` - Caching patterns
- [ ] `cache-invalidation.md` - Cache invalidation
- [ ] `tenant-cache.md` - Per-tenant caching

### Security

- [ ] `tenant-isolation.md` - Data isolation
- [ ] `api-security.md` - API authentication
- [ ] `file-permissions.md` - File access control

### Deployment

- [ ] `deployment-process.md` - Release workflow
- [ ] `environment-config.md` - Environment setup
- [ ] `docker-setup.md` - Container configuration

### Monitoring

- [ ] `logging.md` - Application logging
- [ ] `error-tracking.md` - Error monitoring
- [ ] `performance-monitoring.md` - Performance metrics

## Priority Levels

### High Priority (Start Here)

Essential concepts and flows for understanding the system:

1. Multi-tenancy concept and flow
2. Entity access and permissions
3. Artist, Venue, Accommodation models
4. HasContactables, HasSpaces, HasAmenities traits
5. Contact management flow
6. Viberate integration flow
7. User identity and cross-tenant system

### Medium Priority

Important for daily development:

1. File and attachment system
2. Notification system
3. Activity tracking
4. Livewire component patterns
5. Service layer architecture
6. Policy implementations

### Low Priority

Nice to have for completeness:

1. Individual enum documentation
2. Specific action classes
3. Detailed widget documentation
4. Infrastructure monitoring details

## Documentation Strategy

### Phase 1: Core Concepts (Week 1)

Focus on fundamental architectural concepts that everything else builds on.

### Phase 2: Main Flows (Week 2)

Document the primary user and data flows that demonstrate concepts in action.

### Phase 3: Key Components (Week 3-4)

Document the most frequently used models, traits, and services.

### Phase 4: Supporting Components (Week 5-6)

Fill in remaining components, enums, and infrastructure.

### Phase 5: Polish & Links (Week 7)

Review all docs, ensure links are correct, update graph.md with relationships.

## Notes

- Use templates in each section folder
- Update this todo as documentation is completed
- Cross-link liberally between related docs
- Keep each doc focused and concise
- Reference `/docs` for technical details
- Update `meta/graph.md` as relationships become clear
