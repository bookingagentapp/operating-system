---
permission: access_authorized_entities
category: Access Authorized Entities
status: ✅ Fully Implemented
---

# Permission: `access_authorized_entities`

**Label**: Access Authorized Entities  
**Category**: System Access  
**Group**: system

## Description

Grants users access to **only specific entities** (venues, artists, accommodations) that administrators have explicitly authorized for them. This is a restrictive permission that overrides the normal view-all permissions.

**Key Concept**: Users with this permission can ONLY see entities they've been granted individual access to via `EntityUserAccess` records. They cannot see all entities their tenant has access to.

## Implementation Status

**Overall Status**: ✅ Fully Implemented

### What's Implemented

- [x] Backend permission check via policies
- [x] Database schema (entity_user_access table)
- [x] Navigation visibility logic
- [x] Scoped queries in Livewire components
- [x] UI for granting user access (in entity detail pages)
- [x] Active/inactive status tracking
- [x] Revocation workflow

### What's Missing

- [ ] Bulk grant access UI
- [ ] User access dashboard (show user what they have access to)
- [ ] Access expiration dates
- [ ] Access request workflow (user requests, admin approves)

## Backend Implementation

### Policy

**Policies Affected**: `ArtistPolicy`, `VenuePolicy`, `AccommodationPolicy`

**Pattern** (from `ArtistPolicy`):

```php
public function view(User $user, Artist $artist): bool
{
    // If user has restricted access permission
    if ($user->can('access_authorized_entities')) {
        // Check if they have explicit access to THIS artist
        return EntityUserAccess::where('user_id', $user->id)
            ->where('entity_type', Artist::class)
            ->where('entity_id', $artist->id)
            ->active()
            ->exists();
    }

    // Otherwise, check normal tenant-level access
    return $artist->isAccessibleByTenant(tenant());
}
```

### Database Schema

**Table**: `entity_user_access` (tenant database)

**Columns**:

- `id` - Primary key
- `user_id` - Foreign key to users
- `entity_type` - Polymorphic type (Artist::class, Venue::class, etc.)
- `entity_id` - Polymorphic ID
- `granted_by_user_id` - Who granted access
- `access_type` - Type of access granted (view, manage, etc.)
- `status` - active, inactive, revoked, expired
- `granted_at` - Timestamp
- `revoked_at` - Timestamp
- `expires_at` - Optional expiration (not used yet)
- `notes` - Admin notes

**Relationships**:

```php
// App\Models\EntityUserAccess
public function user(): BelongsTo
{
    return $this->belongsTo(User::class, 'user_id');
}

public function entity(): MorphTo
{
    return $this->morphTo();
}

public function grantedBy(): BelongsTo
{
    return $this->belongsTo(User::class, 'granted_by_user_id');
}

// Scopes
public function scopeActive($query)
{
    return $query->where('status', 'active');
}
```

## Frontend Implementation

### Navigation

**File**: `resources/views/components/navigation/side-tenant.blade.php`

**Lines**: 40-52 (Artists), 71-83 (Venues), 101-113 (Accommodations)

**Pattern**:

```blade
@php
    $canViewArtists = auth()->user()->can('view-any', \App\Models\Artist::class);
    $hasArtistAccess = false;

    // Check if user has restricted access and has any artists
    if (auth()->user()->can('access_authorized_entities')) {
        $hasArtistAccess = \App\Models\EntityUserAccess::where('user_id', auth()->id())
            ->where('entity_type', \App\Models\Artist::class)
            ->active()
            ->exists();
    }

    $showArtists = $canViewArtists || $hasArtistAccess;
@endphp

@if($showArtists)
    <!-- Show navigation item -->
@endif
```

**Logic**:

1. First check if user has normal view permissions
2. If not, check if they have `access_authorized_entities` permission AND have at least one entity granted
3. Show navigation if either condition is true

### UI Components

**Granting Access** (in entity detail pages):

**Livewire Component**: Inline in `Artists\Show`, `Venues\Show`, etc.

**What Admins Can Do**:

- Grant specific users access to a single entity
- Revoke access
- View list of users with access
- Add notes about why access was granted

**What Restricted Users See**:

- Only entities they have access to in list views
- Cannot access entity URLs they don't have permission for
- Navigation only shows if they have at least one accessible entity

### Actions Controlled

**User Impact**:

- **With this permission**: User is RESTRICTED to only seeing authorized entities
- **Without this permission**: User sees all entities their tenant has access to (subject to other permissions)

**Admin Actions**:

- Grant user access via `EntityUserAccess::create()`
- Revoke access by setting `status = 'revoked'`
- Temporarily suspend access with `status = 'inactive'`

## CEO's Vision vs Reality

### Use Cases

This permission enables scenarios like:

1. **Junior Agent**: Can only see the 5 artists they directly manage
2. **Client Portal User**: External user who can only see their own artist
3. **Temp Worker**: Limited access to specific venues during a project
4. **Freelance Consultant**: Access to one specific artist for a campaign

### Navigation Requirements

From CEO's navigation document:

- **Client Access** (under Team Manager) 🚧
  - This permission is the foundation for client access
  - Need dedicated "Client" role with this permission enabled
  - Need client invitation workflow

### Gap Analysis

| Feature                 | Designed | Backend | Frontend | Status                  |
| ----------------------- | -------- | ------- | -------- | ----------------------- |
| Entity-specific access  | ✅       | ✅      | ✅       | Complete                |
| Navigation visibility   | ✅       | ✅      | ✅       | Complete                |
| Grant/revoke UI         | ✅       | ✅      | ✅       | Complete                |
| User access dashboard   | ❌       | ❌      | ❌       | Not started             |
| Access request workflow | 🎨       | ❌      | ❌       | Not started             |
| Bulk grant access       | ❌       | ❌      | ❌       | Not started             |
| Access expiration       | ❌       | 🚧      | ❌       | Schema exists, not used |

## Related Documentation

- [[concepts/entity-access]] - Overall entity access system (TODO)
- [[flows/entity-access-resolution]] - How permission checks work (empty)
- [[components/EntityUserAccess]] - Model documentation (TODO)
- [[permissions/manage-artist-access]] - Related permission for sharing

## Implementation Example

### Granting Access (Backend)

```php
use App\Models\EntityUserAccess;
use App\Models\Artist;

// Admin grants junior agent access to specific artist
EntityUserAccess::create([
    'user_id' => $juniorAgent->id,
    'entity_type' => Artist::class,
    'entity_id' => $artist->id,
    'granted_by_user_id' => auth()->id(),
    'access_type' => 'view', // or 'manage'
    'status' => 'active',
    'granted_at' => now(),
    'notes' => 'Assigned as primary contact for this artist',
]);
```

### Checking Access (Backend)

```php
// In policy or query scope
$user->can('access_authorized_entities')
    && EntityUserAccess::where('user_id', $user->id)
        ->where('entity_type', Artist::class)
        ->where('entity_id', $artist->id)
        ->active()
        ->exists();
```

### Scoping Queries (Livewire)

```php
// In Artists\ListComponent
public function getArtistsProperty()
{
    $query = Artist::query();

    // If user has restricted access
    if (auth()->user()->can('access_authorized_entities')) {
        // Only show artists they have explicit access to
        $artistIds = EntityUserAccess::where('user_id', auth()->id())
            ->where('entity_type', Artist::class)
            ->active()
            ->pluck('entity_id');

        $query->whereIn('id', $artistIds);
    } else {
        // Show all artists tenant has access to
        $query->accessibleByTenant(tenant());
    }

    return $query->get();
}
```

## Notes

**Important Behaviors**:

- This is a **restrictive** permission - it limits what users see
- Most permissions are **additive** - they grant capabilities
- Users with this permission need BOTH:
  1. The `access_authorized_entities` permission on their role
  2. Explicit `EntityUserAccess` records for each entity

**Navigation Design**:

- Navigation items only show if user has at least ONE accessible entity
- Prevents showing empty sections to restricted users
- Queries check `exists()` not `count()` for performance

**Cross-Tenant**:

- `EntityUserAccess` is in the **tenant database**
- Works in combination with `EntityAccess` (cross-tenant sharing)
- User might have access to a shared entity from another tenant

**Future Enhancements**:

- Add expiration dates for temporary access
- Add access request workflow (user requests, admin approves)
- Add notification when access is granted/revoked
- Add user dashboard showing "My Accessible Entities"
