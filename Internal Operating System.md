This folder serves as the living knowledge base for the BookingAgent application. Think of it as the internal OS that documents how we think, work, and build.

## Purpose

`/os` is our **single source of truth** for:

- Mental models and system flows
- Design decisions and architectural reasoning
- Component relationships and dependencies
- Infrastructure patterns and operations
- **Permission-to-feature mapping**
- Living glossary of domain terms
- **Gap analysis between design and implementation**
- Meta-documentation about our processes

## Philosophy

Documentation is code. It should be:

- **Living**: Updated as the system evolves
- **Linked**: Connected via relationships, not siloed
- **Discoverable**: Structured for exploration
- **Minimal**: Only what's necessary, nothing more
- **Versioned**: Tracked in git like any other artifact
- **Permission-Driven**: Features documented from authorization perspective
- **Reality-Based**: Track what's implemented vs what's designed

## Structure

```
/os
├── feature-planning/    # Feature planning and CEO QA board
├── permissions/         # Permission documentation (backend → frontend mapping)
├── concepts/            # Core domain concepts and mental models
├── flows/               # User journeys, data flows, process diagrams
├── components/          # System components and their interactions
├── infra/               # Infrastructure, deployment, operations
├── glossary/            # Domain terminology and definitions
├── meta/                # Meta-documentation and conventions
└── archive/             # Deprecated or historical information
```

### Feature Planning

The `/os/feature-planning/` directory contains:

- **feature-planning.md**: QA board for all navigation items
  - Nested structure matching CEO's navigation
  - Questions to clarify with CEO
  - Implementation status tracking
  - Missing permissions identified
  - Dependencies and blockers

**Use this** to track what needs clarification before building features.

### Permissions

The `/os/permissions/` directory documents every permission with implementation status and related code.

Each concept folder contains:

- `index.md` - Main entry point
- Supporting markdown files as needed
- All lowercase, hyphen-separated filenames

## Naming Conventions

- **Code Entity Files**: Exact code name (e.g. `Artist.md`, `HasContactables.md`, `ViberateService.md`)
- **Concept Files**: `kebab-case.md` (e.g. `multi-tenancy.md`, `user-onboarding.md`)
- **Folders**: `kebab-case/` (e.g. `concepts/`, `flows/`)
- **Links**: Use Obsidian WikiLinks `[[folder/page]]` or `[[folder/page|Display Text]]`
- **Anchors**: `[[page#section-heading]]`

**Rationale**: Code entity files match their source exactly for 1:1 mapping. General concepts use readable kebab-case.

## Linking Between Documents

Always prefer explicit links over implicit references:

```markdown
# Good

See [[flows/user-onboarding]] for the complete flow.
Permission checking follows [[concepts/entity-access]].

# Bad

See the user onboarding documentation.
Check the entity access concept.
```

## Cross-References

- Link to code using relative paths: `app/Models/Artist.php`
- Link between OS concepts liberally to build the knowledge graph
- Use WikiLinks for all internal references

## Maintenance

- Update when implementing new features
- Archive outdated information, don't delete
- Use git history to track evolution of thinking
- Obsidian graph view shows relationship density

## Getting Started

1. Browse [[Concepts]] for core mental models
2. Explore [[Flows]] to understand user journeys
3. Check [[Components]] for system architecture
4. Review [[Glossary]] for domain terminology
5. See [[meta/graph]] for relationship mapping

## Tools

- **Editor**: Obsidian (optimized for)
- **Format**: Markdown with WikiLinks
- **Version Control**: Git
- **Browsing**: Obsidian graph view, file explorer, search
