# Internal Operating System

This folder serves as the living knowledge base for the BookingAgent application. Think of it as the internal OS that documents how we think, work, and build.

## Purpose

While `/docs` contains formal technical documentation, `/os` is our internal knowledge graph for:

- Mental models and system flows
- Design decisions and architectural reasoning
- Component relationships and dependencies
- Infrastructure patterns and operations
- Living glossary of domain terms
- Meta-documentation about our processes

## Philosophy

Documentation is code. It should be:

- **Living**: Updated as the system evolves
- **Linked**: Connected via relationships, not siloed
- **Discoverable**: Structured for exploration
- **Minimal**: Only what's necessary, nothing more
- **Versioned**: Tracked in git like any other artifact

## Structure

```
/os
├── concepts/        # Core domain concepts and mental models
├── flows/           # User journeys, data flows, process diagrams
├── components/      # System components and their interactions
├── infra/           # Infrastructure, deployment, operations
├── glossary/        # Domain terminology and definitions
├── meta/            # Meta-documentation and conventions
└── archive/         # Deprecated or historical information
```

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

- Link to formal docs when referencing implementation: `See /docs/SYSTEMS/CONTACTS.md`
- Link to code using relative paths: `app/Models/Artist.php`
- Link between OS concepts liberally to build the knowledge graph

## Maintenance

- Update when implementing new features
- Archive outdated information, don't delete
- Use git history to track evolution of thinking
- Obsidian graph view shows relationship density

## Getting Started

1. Browse [[concepts/index]] for core mental models
2. Explore [[flows/index]] to understand user journeys
3. Check [[components/index]] for system architecture
4. Review [[glossary/index]] for domain terminology
5. See [[meta/graph]] for relationship mapping

## Tools

- **Editor**: Obsidian (optimized for)
- **Format**: Markdown with WikiLinks
- **Version Control**: Git
- **Browsing**: Obsidian graph view, file explorer, search
