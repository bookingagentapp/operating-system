# Meta

Documentation about documentation, conventions, and how we work.

## Overview

This section contains meta-information about the `/os` system itself, our conventions, and how we maintain this knowledge base.

## Contents

- [[Conventions]] - Naming and formatting standards
- [[meta/graph]] - Relationship mapping between entities
- [[meta/maintenance]] - How to keep docs up to date
- [[meta/templates]] - Using the template system

## Philosophy

The `/os` folder is designed to:

1. **Complete documentation**: Everything you need to understand the system
2. **Enable exploration**: Obsidian graph view shows relationships
3. **Stay minimal**: Only document what provides value
4. **Version with code**: Docs evolve alongside implementation
5. **Support LLMs**: Structure optimized for AI context understanding

## Key Principles

### Documentation as Code

- Treat docs like source code
- Review in PRs
- Test links and references
- Refactor when needed

### Living Documentation

- Update when implementing features
- Archive rather than delete
- Track decisions over time
- Use git history as context

### Linked Thinking

- Connect related concepts
- Build knowledge graph
- Enable discovery through links
- Show dependencies explicitly

## Quick Reference

- Main README: [[Internal Operating System]]
- Concept templates: [[concepts/_template]]
- Flow templates: [[flows/_template]]
- Component templates: [[components/_template]]
- Infrastructure templates: [[infra/_template]]

## Tools & Setup

**Obsidian Configuration:**

- WikiLinks enabled
- Graph view for visualization
- Backlinks panel for references
- Search for discovery

**Git Integration:**

- Commit docs with related code changes
- Use conventional commit messages
- Include in PR reviews
- Track evolution in git history
