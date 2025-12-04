# Claude Agent - Prompts System

> A universal AI Agent prompts system that guides Claude Code's behavior.

## 1. Prompts System

This system uses the `prompts/` directory to organize all AI Agent related documentation.

### 1.1 Directory Structure

```
project-root/
├── CLAUDE.md                    # Entry file (this file)
└── prompts/
    ├── biz/                     # Business context
    │   ├── OVERVIEW.md          # Business overview
    │   └── {module}/            # Module-specific business docs
    ├── tech/                    # Technical context
    │   └── {project}/           # Project-specific technical docs
    ├── conduct/                 # Development standards
    │   ├── CODE_COMMENTS.md     # Code commenting standards
    │   ├── DEPENDENCIES.md      # Dependency management
    │   ├── TESTING.md           # Testing requirements
    │   ├── COMPATIBILITY.md     # Backward compatibility
    │   ├── GIT_COMMIT.md        # Git commit message standards
    │   └── GIT_OPERATIONS.md    # Git operation permissions
    └── command/                 # Custom commands
        ├── 00_CONTEXT_REINFORCEMENT.md
        └── 01_REVIEW_COMMIT.md
```

### 1.2 Directory Description

| Directory | Purpose | Examples |
|-----------|---------|----------|
| `biz/` | Business context | Product logic, business flows, domain models |
| `tech/` | Technical context | Architecture design, tech stack, API docs |
| `conduct/` | Development standards | Code style, Git standards, testing requirements |
| `command/` | Custom commands | Reusable task workflows |

### 1.3 File Naming Conventions

- **Documentation files**: UPPER_SNAKE_CASE
  - Examples: `OVERVIEW.md`, `CODE_COMMENTS.md`, `GIT_COMMIT.md`
  - Reason: Self-documenting, easy to identify

- **Command files**: Number prefix + UPPER_SNAKE_CASE
  - Examples: `00_CONTEXT_REINFORCEMENT.md`, `01_REVIEW_COMMIT.md`
  - Reason: Numbers enable quick reference ("execute command 0")
  - Special: `00` prefix usually indicates system/meta-level commands

- **Directories**: lowercase kebab-case
  - Examples: `biz/`, `tech/`, `conduct/`, `command/`

- **No README.md**: File names should directly describe content, avoid redundant indexes

---

## 2. Custom Command System

### 2.1 Purpose

Define reusable command workflows for frequently executed tasks.

### 2.2 Command File Format

```markdown
# Command Name

## Description
Brief description of what this command does

## Execution Steps
1. First step
2. Second step
3. ...

## Notes
- Standards to follow
- Special constraints
```

### 2.3 Usage

Users can execute commands via:
- **By number**: "execute command 0" → reads `prompts/command/00_*.md`
- **By name**: "execute REVIEW_COMMIT" → reads corresponding command file
- Agent follows the steps defined in the documentation

### 2.4 Built-in Commands

| Number | Name | Purpose |
|--------|------|---------|
| 00 | CONTEXT_REINFORCEMENT | Context reinforcement, re-review docs and correct errors |
| 01 | REVIEW_COMMIT | Check git changes and generate commit message |

---

## 3. Documentation Principles

### 3.1 Reading Order

Before starting any development work, **must** read relevant documentation:

1. `CLAUDE.md` (this document) → Understand guidelines and standards
2. `prompts/biz/` → Understand business logic
3. `prompts/tech/{project}/` → Project technical documentation
4. `prompts/conduct/` → General development standards

### 3.2 Documentation-First Development

- If requirements involve **business logic changes** → Update `biz/` docs first
- If requirements involve **technical approach changes** → Update `tech/` docs first
- **Update documentation before starting development**

### 3.3 Keep Documentation Current

- Documentation only records **current version**, not historical changes
- When new requirements/designs are added, remove corresponding old content
- Historical changes are tracked by Git

---

## 4. Agent Behavior Guidelines

### 4.1 Language Requirements

Follow specific language usage standards based on project configuration:
- **Answering questions and thinking process**: Use project's preferred language (default: English)
- **Code and comments**: Use English (international convention)
- **Git commit messages**: Use English (open source community convention)

### 4.2 Development Standards

Refer to `prompts/conduct/` directory for specific development standards:
- `CODE_COMMENTS.md` — Code commenting standards
- `DEPENDENCIES.md` — Dependency management
- `TESTING.md` — Testing requirements
- `COMPATIBILITY.md` — Backward compatibility
- `GIT_COMMIT.md` — Git commit message standards
- `GIT_OPERATIONS.md` — Git operation permissions

---

## 5. Execution Priority

When conflicts occur, handle by the following priority:

1. **CLAUDE.md** (this document) — Highest priority
2. **conduct/** — Development behavior standards
3. **biz/** — Business logic understanding
4. **tech/** — Project technical documentation
5. **User instructions** — Specific task requirements

Higher priority overrides lower priority.

---

## 6. Extension Guide

Based on project needs, you can add the following directories:

- `prompts/biz/` — Business logic documentation
- `prompts/tech/` — Project technical documentation

---

**Remember: All rules, standards, and context are in the `prompts/` directory.**
