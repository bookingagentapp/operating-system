---
title: Conventions Guide
type: meta
status: active
updated: 2025-10-04
---

# Conventions Guide

Standards and conventions for maintaining the `/os` documentation system.

## File Naming

### Code Entity Files

Use the exact name from the codebase:

- Models: `Artist.md`, `Venue.md`, `EntityAccess.md`
- Traits: `HasContactables.md`, `CentralConnection.md`
- Services: `ViberateService.md`, `ArtistService.md`
- Livewire: `Artists.Show.md`, `Companies.Show.md`

**Rationale**: 1:1 mapping between code and docs eliminates confusion.

### Concept Files

Use lowercase kebab-case for general concepts:

- `multi-tenancy.md`
- `user-onboarding.md`
- `permission-resolution.md`

**Rationale**: Readable for non-code concepts.

### Folders

Always lowercase, hyphen-separated:

- `concepts/`
- `flows/`
- `components/`
- `components/livewire/`

## Linking Conventions

### WikiLinks

Always use Obsidian WikiLinks for internal references:

```markdown
[[concepts/multi-tenancy]]
[[components/Artist]]
[[flows/user-onboarding]]
[[components/HasContactables]]
```

With custom text:

```markdown
[[concepts/multi-tenancy|multi-tenant architecture]]
[[components/Artist|Artist model]]
```

With anchors:

```markdown
[[concepts/multi-tenancy#database-architecture]]
```

### Code References

Use relative paths for code:

```markdown
See `app/Models/Artist.php` for implementation.
Check `app/Services/ContactableService.php` for the service layer.
```

## Frontmatter

All documents should include YAML frontmatter:

```yaml
---
title: Document Title
type: concept|flow|component|infra|meta
category: relevant-category
status: active|draft|deprecated
updated: 2025-10-04
---
```

Optional fields:

```yaml
location: app/path/to/File.php
database: central|tenant|both
actors: User, System, External
```

## Document Structure

### All Documents

1. One-sentence summary
2. Overview section
3. Main content
4. Related links section

### Use Headers Consistently

- H1 (`#`) - No h1, uses the h1 from the native file name, example Architecture.md
- H2 (`##`) - Major sections
- H3 (`###`) - Subsections
- H4 (`####`) - Details (sparingly)

## Content Guidelines

### Be Concise

- One concept per document
- Use bullet points over paragraphs
- Link rather than repeat
- Code examples over prose

### Link Liberally

- Connect related concepts
- Reference implementations
- Show dependencies
- Build the graph

### Keep It Current

- Update when code changes
- Archive obsolete content
- Use git history for context
- Review in PRs

### No Binary Content

- Only markdown files
- Use code blocks for examples
- ASCII diagrams or Mermaid syntax for visualizations
- Keep it text-searchable

## Template Usage

Each section has a `_template.md`:

- Copy the template
- Fill in all sections
- Remove irrelevant parts
- Update frontmatter

Don't leave template placeholders in docs.

## Archiving

When content becomes outdated:

1. Move to `archive/` folder
2. Add deprecation note at top:

```markdown
> **Deprecated**: This concept was replaced by [[concepts/new-approach]].
> Archived: 2025-10-04
```

3. Update links to point to new docs
4. Keep for historical context

## Git Workflow

### Commit Messages

```bash
docs(os): add Artist component documentation
docs(os): update multi-tenancy concept
docs(os): archive old permission model
```

### PR Reviews

- Docs reviewed like code
- Check links work
- Verify accuracy
- Ensure consistency

### Branch Strategy

- Update docs in feature branches
- Commit with related code
- Merge together

## Obsidian Integration

### Recommended Settings

- WikiLinks: enabled
- Strict line breaks: disabled
- Default location for new notes: root
- New link format: Shortest path

### Useful Plugins

- Graph view (core)
- Backlinks (core)
- Outgoing links (core)
- Tag pane (core)

### Vault Structure

- Root: `/os`
- Templates: `_template.md` in each folder
- Meta: `meta/` folder

## Quality Checklist

Before committing:

- [ ] Frontmatter complete
- [ ] Links use WikiLink format
- [ ] Code names match exactly
- [ ] Related docs linked
- [ ] Template sections filled
- [ ] One-sentence summary clear
- [ ] Status is accurate
- [ ] Updated date current

## Related

- [[meta/graph]] - Relationship visualization
- [[meta/maintenance]] - Keeping docs fresh
- [[Internal Operating System]] - Main OS documentation
