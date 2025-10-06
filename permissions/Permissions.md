# Permissions Documentation

This directory documents every permission in the system, linking backend authorization to UI features and navigation.

## Purpose

Each permission has its own documentation page that includes:

- **What it controls**: UI elements, routes, actions
- **Implementation status**: ✅ Fully implemented, 🚧 Partial, ❌ Not implemented
- **Policy methods**: Backend authorization logic
- **UI locations**: Where this permission affects the interface
- **Related features**: Navigation items, Livewire components, actions
- **Gap analysis**: What's missing vs CEO's vision

## Permission Categories

Permissions are organized by functional area:

### System Access
- [[permissions/access-authorized-entities|access_authorized_entities]] - Entity-specific access control

### User Management
- [[permissions/view-users|view_users]] - View team members
- [[permissions/manage-users|manage_users]] - Manage team members

### Artist Management
- [[permissions/view-own-artist|view_own_artist]] - View owned artists
- [[permissions/manage-own-artist|manage_own_artist]] - Manage owned artists
- [[permissions/archive-own-artist|archive_own_artist]] - Archive owned artists
- [[permissions/view-imported-artist|view_imported_artist]] - View shared artists
- [[permissions/manage-imported-artist|manage_imported_artist]] - Manage shared artists
- [[permissions/archive-imported-artist|archive_imported_artist]] - Remove shared artists
- [[permissions/view-artist-analytics|view_artist_analytics]] - Artist analytics access
- [[permissions/manage-artist-access|manage_artist_access]] - Grant artist access
- [[permissions/export-artist-data|export_artist_data]] - Export artist data
- [[permissions/view-artist-files|view_artist_files]] - Artist files access
- [[permissions/view-artist-contacts|view_artist_contacts]] - View artist contacts
- [[permissions/manage-artist-contacts|manage_artist_contacts]] - Manage artist contacts

### Venue Management
- [[permissions/view-own-venue|view_own_venue]] - View owned venues
- [[permissions/manage-own-venue|manage_own_venue]] - Manage owned venues
- [[permissions/archive-own-venue|archive_own_venue]] - Archive owned venues
- [[permissions/view-imported-venue|view_imported_venue]] - View shared venues
- [[permissions/manage-imported-venue|manage_imported_venue]] - Manage shared venues
- [[permissions/archive-imported-venue|archive_imported_venue]] - Remove shared venues
- [[permissions/claim-venue|claim_venue]] - Claim unclaimed venues
- [[permissions/manage-venue-partners|manage_venue_partners]] - Manage venue partnerships
- [[permissions/view-venue-analytics|view_venue_analytics]] - Venue analytics access
- [[permissions/manage-venue-access|manage_venue_access]] - Grant venue access
- [[permissions/export-venue-data|export_venue_data]] - Export venue data
- [[permissions/view-venue-files|view_venue_files]] - Venue files access
- [[permissions/sync-venue-data|sync_venue_data]] - Sync external venue data

### Contact Management
- [[permissions/view-contacts|view_contacts]] - View contacts
- [[permissions/manage-contacts|manage_contacts]] - Manage contacts

### Company Management
- [[permissions/view-companies|view_companies]] - View companies
- [[permissions/manage-companies|manage_companies]] - Manage companies

### Accommodation Management
- [[permissions/view-accommodations|view_accommodations]] - View accommodations
- [[permissions/manage-accommodations|manage_accommodations]] - Manage accommodations

### System Administration
- [[permissions/manage-settings|manage_settings]] - System settings access
- [[permissions/manage-roles|manage_roles]] - Role management
- [[permissions/view-tenant-audit-logs|view_tenant_audit_logs]] - Audit logs access
- [[permissions/export-tenant-data|export_tenant_data]] - System data export
- [[permissions/access-tenant-reports|access_tenant_reports]] - Reports access

## Usage

When planning a feature:

1. **Check the permission docs** to see what's implemented
2. **Identify missing permissions** for new features
3. **Update PermissionRegistry.php** with new permissions
4. **Document the new permission** in this directory
5. **Link to relevant flows/components** in `/os`

## Status Legend

- ✅ **Fully Implemented**: Permission works, UI exists, policies configured
- 🚧 **Partially Implemented**: Some functionality exists, gaps remain
- ❌ **Not Implemented**: Permission exists but no functionality built
- 🎨 **Design Only**: CEO has Figma comp but no backend work
- 📋 **Planned**: Documented requirement, not yet started

