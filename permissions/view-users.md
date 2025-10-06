---
permission: view_users
category: User Management
status: ✅ Fully Implemented
---

# Permission: `view_users`

**Label**: View Users  
**Category**: User Management  
**Group**: basic  

## Description

Allows users to view team members and their basic information. This is a read-only permission for accessing the team directory.

## Implementation Status

**Overall Status**: ✅ Fully Implemented

### What's Implemented

- [x] Backend policy methods
- [x] Routes with middleware
- [x] UI navigation items
- [x] Livewire components
- [x] Team member list view
- [x] Team member detail view

### What's Missing

- [ ] Advanced search/filtering
- [ ] Export team member list
- [ ] Org chart view

## Backend Implementation

### Policy

**File**: `app/Policies/UserPolicy.php`

**Methods**:
```php
public function viewAny(User $user): bool
{
    return $user->can('view_users');
}

public function view(User $user, User $model): bool
{
    return $user->can('view_users');
}
```

### Routes

**File**: `routes/tenant.php`

**Lines**: 117-121

```php
Route::prefix('team')->middleware('can:view_users')->group(function () {
    Route::get('/', [TeamController::class, 'index'])->name('tenant.team.index');
    Route::get('/{user}', [TeamController::class, 'show'])
        ->whereUuid('user')
        ->name('tenant.team.show');
});
```

## Frontend Implementation

### Navigation

**File**: `resources/views/components/navigation/side-tenant.blade.php`

**Lines**: 131-142

```blade
@canany(['view_contacts', 'view_companies', 'view_users'])
    <x-navigation.items.left icon="user-framed" label="{{ __('Contacts') }}" :children="[
        // ...
        [
            'label' => __('Team Members'), 
            'route' => currentContext() . '.team.index', 
            'permission' => auth()->user()->can('view_users')
        ],
    ]" />
@endcanany
```

### UI Components

**Livewire Components**:
- `App\Livewire\Team\ListComponent` - Team member listing
- `App\Livewire\Team\Show` - Team member detail

**Blade Files**:
- `resources/views/team/index.blade.php`
- `resources/views/team/show.blade.php`

### Actions Controlled

**What Users Can Do**:
- View list of team members
- See team member details (name, email, role)
- View team member permissions
- Cannot edit or manage users (requires `manage_users`)

## CEO's Vision vs Reality

### Navigation Requirements

From CEO's navigation document:

- **Section**: Team Manager
- **Items**: 
  - Add User ✅ (requires `manage_users`)
  - Roles & Permissions ✅ (requires `manage_roles`)
  - Import/Export Team 🎨 (not implemented)
  - Client Access 🎨 (not implemented)

### Gap Analysis

| Feature | Designed | Backend | Frontend | Status |
|---------|----------|---------|----------|--------|
| View team list | ✅ | ✅ | ✅ | Complete |
| View team details | ✅ | ✅ | ✅ | Complete |
| Search/filter team | 🎨 | 🚧 | 🚧 | Basic only |
| Export team list | 🎨 | ❌ | ❌ | Not started |
| Org chart view | ❌ | ❌ | ❌ | Not planned |

## Related Documentation

- [[permissions/manage-users]] - Management permission
- [[components/User]] - User model (TODO)
- [[concepts/user-identity]] - Cross-tenant user system (TODO)

## Notes

- This permission is separate from `manage_users` for security
- Guest roles typically get this permission for team visibility
- Users in tenant database, identity in central database
- Cross-tenant users can belong to multiple tenants

