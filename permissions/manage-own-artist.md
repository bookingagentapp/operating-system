---
permission: manage_own_artist
category: Artist Management
status: ✅ Fully Implemented
---

# Permission: `manage_own_artist`

**Label**: Manage Own Artists  
**Category**: Artist Management  
**Group**: owned  

## Description

Allows users to create, edit, and manage artists owned by their organization. This includes updating artist profiles, social media links, managing contacts, and controlling who has access to the artist.

## Implementation Status

**Overall Status**: ✅ Fully Implemented

### What's Implemented

- [x] Backend policy methods
- [x] Routes with middleware
- [x] UI navigation items
- [x] Livewire components (Create, Edit, Show)
- [x] Action classes (CreateArtist, UpdateArtistProfile)
- [x] Database schema (artists, entity_access tables)
- [x] Tests (partial)

### What's Missing

- [ ] Comprehensive test coverage
- [ ] Bulk edit functionality
- [ ] Artist merge/duplicate detection

## Backend Implementation

### Policy

**File**: `app/Policies/ArtistPolicy.php`

**Methods**:
```php
public function update(User $user, Artist $artist): bool
{
    // Owner tenants can always update
    if ($artist->isOwnedBy(tenant())) {
        return $user->can('manage_own_artist');
    }
    
    // Shared artists require different permission
    return $user->can('manage_imported_artist');
}
```

### Routes

**File**: `routes/tenant.php`

```php
Route::prefix('artists')->group(function () {
    Route::get('/add', [ArtistsController::class, 'import'])
        ->name('tenant.artists.add');
    Route::get('/create', [ArtistsController::class, 'create'])
        ->name('tenant.artists.create');
    
    Route::prefix('{artist}')->group(function () {
        Route::get('/edit', [ArtistsController::class, 'edit'])
            ->name('tenant.artists.edit');
        // Policy check happens in controller
    });
});
```

## Frontend Implementation

### Navigation

**File**: `resources/views/components/navigation/side-tenant.blade.php`

**Lines**: 54-68

```blade
@if($showArtists)
    <x-navigation.items.left icon="artists-outline" label="{{ __('Artists Database') }}" :children="[
        // ...
        [
            'label' => __('Add Artist'),
            'route' => currentContext() . '.artists.add',
            'permission' => auth()->user()->can('create', \App\Models\Artist::class),
        ],
    ]" />
@endif
```

### UI Components

**Livewire Components**:
- `App\Livewire\Artists\Import` - Import artists from Viberate
- `App\Livewire\Artists\Show` - Artist detail page with inline editing
- `App\Livewire\Artists\Create` - Manual artist creation (fallback)

**Blade Files**:
- `resources/views/artists/import.blade.php`
- `resources/views/artists/show.blade.php`

### Actions Controlled

**Action Classes**:
- `App\Actions\Artist\CreateArtist` - Creates new artist
- `App\Actions\Artist\UpdateArtistProfile` - Updates artist data
- `App\Actions\Artist\ImportArtistFromViberate` - Import from external API

**What Users Can Do**:
- Import artists from Viberate API
- Create artists manually
- Edit artist name, bio, location
- Manage artist genres
- Update social media links
- Assign contacts (persons/companies) to artists
- Manage artist spaces and amenities
- Control who can access the artist (EntityAccess)

## CEO's Vision vs Reality

### Figma Designs

- Artist import flow: ✅ Implemented
- Artist edit form: ✅ Implemented
- Artist detail page: ✅ Implemented

### Navigation Requirements

From CEO's navigation document:

- **Section**: Artist Database
- **Items**: 
  - Artist Importer ✅ (maps to "Add Artist")
  - Watchlist 🎨 (not implemented - need favorites system)
  - Archived Artists ✅ (route exists, UI partial)

### Gap Analysis

| Feature | Designed | Backend | Frontend | Status |
|---------|----------|---------|----------|--------|
| Import from Viberate | ✅ | ✅ | ✅ | Complete |
| Manual artist creation | ✅ | ✅ | ✅ | Complete |
| Inline editing | ✅ | ✅ | ✅ | Complete |
| Artist watchlist/favorites | 🎨 | ❌ | ❌ | Not started |
| Bulk artist operations | ❌ | ❌ | ❌ | Not planned |
| Artist merge | ❌ | ❌ | ❌ | Not planned |

## Related Documentation

- [[concepts/artist-model]] - Artist domain model (TODO)
- [[flows/artist-import]] - Artist import flow (TODO)
- [[components/Artist]] - Artist model documentation (TODO)
- [[permissions/view-own-artist]] - Viewing permission
- [[permissions/manage-artist-access]] - Access control permission

## Related Permissions

This permission is part of the artist ownership hierarchy:

- **view_own_artist** - Required to see owned artists
- **manage_own_artist** - This permission (create/edit)
- **archive_own_artist** - Required to archive
- **manage_artist_access** - Required to share with other tenants

## Notes

- Artists are stored in the **central database** (not tenant-specific)
- Ownership is determined by `EntityAccess` records with type `owner`
- The permission check happens via `ArtistPolicy` which delegates to `HasEntityAccessPermissions` trait
- Users can have granular access to specific artists via `EntityUserAccess` if they have the `access_authorized_entities` permission
- The Viberate integration enriches artist data with social media stats, tour dates, and analytics

