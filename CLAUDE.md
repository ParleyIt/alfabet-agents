# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

Alfabet Agents is a collection of 56 specialized AI subagents for Claude Code. This is a **documentation-only repository** - there is no traditional code to build, test, or deploy. Each agent is a standalone Markdown file with YAML frontmatter.

## Key Commands

Since this is a documentation repository, there are no build/test/lint commands. Common tasks:

- **View all agents**: `ls *.md | grep -v README | grep -v CLAUDE`
- **Search agent names**: `grep "^name:" *.md`
- **Find agents by model**: `grep "^model: opus" *.md`
- **Check agent count**: `ls *.md | grep -v README | grep -v CLAUDE | wc -l`

## Architecture & Structure

### Agent File Format
Every agent MUST follow this structure:
```markdown
---
name: agent-name
description: One-line description of when to use this agent
model: haiku|sonnet|opus  # Choose based on complexity
---

System prompt defining the agent's capabilities and behavior
```

### Model Assignment Guidelines
- **haiku**: Simple tasks (data analysis, content creation, basic queries)
- **sonnet**: Most development work (coding, testing, infrastructure)
- **opus**: Critical/complex tasks (security, AI engineering, incident response)

### Agent Categories
Agents are conceptually grouped into:
- Development & Architecture (backend, frontend, mobile, database)
- Language Specialists (Python, Kotlin, JavaScript, etc.)
- Infrastructure & Operations (DevOps, cloud, deployment)
- Quality & Security (testing, security auditing, code review)
- Data & AI (ML, data engineering, AI systems)
- Business & Marketing (content, sales, analysis)

## Alfabet Platform Patterns

The `kotlin-expert.md` agent contains extensive Alfabet-specific patterns. Key patterns include:

### Common Module Structure
```kotlin
common/
├── src/main/kotlin/
│   ├── entities/        # Domain entities
│   ├── services/        # Business logic
│   ├── repositories/    # Data access
│   └── utils/          # Utilities
```

### Entity Pattern
```kotlin
@Table("table_name")
data class Entity(
    @Id val id: UUID = UUID.randomUUID(),
    @Column("column_name") val field: String
) : EntityBase()
```

### Data Access Pattern
```kotlin
class EntityDAO(ds: DataSource) : BaseDAO<Entity>(Entity::class, ds) {
    suspend fun customQuery() = query {
        where { Entity::field eq value }
    }.fetchAll()
}
```

## Contributing Guidelines

1. **Always create an issue first** before adding/modifying agents
2. **Follow the exact agent format** - no deviations
3. **Include practical examples** in agent prompts
4. **Ensure agents are complementary**, not duplicative
5. **Use clear, actionable language** in descriptions

## Content Standards

- Agents must be **respectful and inclusive**
- Focus on **practical, real-world guidance**
- Include **domain-specific patterns** where relevant
- Avoid generic advice - be specific and actionable
- Reference relevant tools/frameworks explicitly

## GitHub Actions

The repository has automated content moderation that:
- Scans all Markdown files for inappropriate content
- Automatically closes/locks issues with violations
- Notifies maintainers of critical issues

## Working with This Repository

1. **Adding a new agent**: Follow the exact format, choose appropriate model
2. **Modifying existing agents**: Maintain backward compatibility
3. **Testing agents**: No automated tests - manual review required
4. **Documentation updates**: Keep README.md in sync with agent count

## Important Notes

- This is NOT a code repository - no build/test infrastructure exists
- All changes are documentation changes
- Focus on clarity and usefulness for Claude Code users
- Consider agent orchestration possibilities when designing new agents