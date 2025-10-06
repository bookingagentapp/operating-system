---
permission: permission_name_here
category: Category Name
status: ✅ Fully Implemented | 🚧 Partial | ❌ Not Implemented | 🎨 Design Only
---

# Permission: `permission_name_here`

**Label**: Human Readable Name  
**Category**: Category Name  
**Group**: owned | shared | advanced | basic | management | system  

## Description

[Brief description of what this permission controls]

## Implementation Status

**Overall Status**: [✅ | 🚧 | ❌ | 🎨]

### What's Implemented

- [ ] Backend policy methods
- [ ] Routes with middleware
- [ ] UI navigation items
- [ ] Livewire components
- [ ] Action classes
- [ ] Database schema
- [ ] Tests

### What's Missing

- List any gaps between permission intent and actual implementation

## Backend Implementation

### Policy

**File**: `app/Policies/XxxPolicy.php`

**Methods**:
```php
public function methodName(User $user, Model $model): bool
{
    return $user->can('permission_name_here');
}
```

### Routes

**File**: `routes/tenant.php` or `routes/web.php`

```php
Route::middleware('can:permission_name_here')->group(function () {
    // Protected routes
});
```

## Frontend Implementation

### Navigation

**File**: `resources/views/components/navigation/side-tenant.blade.php`

**Line**: [Line number]

```blade
@can('permission_name_here')
    <x-navigation.items.left ... />
@endcan
```

### UI Components

**Livewire Components**:
- `App\Livewire\Path\ComponentName`

**Blade Files**:
- `resources/views/path/to/view.blade.php`

### Actions Controlled

**Action Classes**:
- `App\Actions\Path\ActionName`

## CEO's Vision vs Reality

### Figma Designs

[Link or description of Figma comps if they exist]

### Navigation Requirements

From CEO's navigation document:

- **Section**: [Navigation section name]
- **Items**: [List navigation items]

### Gap Analysis

| Feature | Designed | Backend | Frontend | Status |
|---------|----------|---------|----------|--------|
| Example | ✅ | ❌ | ❌ | Not started |

## Related Documentation

- [[concepts/concept-name]] - Related concept
- [[flows/flow-name]] - Related flow
- [[components/ComponentName]] - Related component

## Notes

Any additional context, edge cases, or implementation considerations.

