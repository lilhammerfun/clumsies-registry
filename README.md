# clumsies-registry

Official registry for [clumsies](https://github.com/dylanwangeth/clumsies) - following [Clumsies Protocol v1](https://github.com/dylanwangeth/clumsies/blob/main/CLUMSIES_PROTOCOL.md).

## Structure

```
clumsies-registry/
├── prompts/
│   ├── index.json              # Prompt metadata index
│   └── {hash}.md               # Content files (with frontmatter)
└── templates/
    ├── index.json              # Template metadata index
    └── {template-name}/
        ├── meta.json           # Template definition
        └── files/
            ├── en/CLAUDE.md    # Entry file (English)
            └── zh/CLAUDE.md    # Entry file (Chinese)
```

## Usage

```bash
# Search available templates
clumsies search

# Install a template
clumsies install <template-name>

# Use in your project
clumsies use <template-name> --lang en
```

## Prompt Format

Each prompt file uses Markdown with YAML frontmatter:

```markdown
---
type: command
lang: en
path: command/00_CONTEXT_REINFORCEMENT.md
author: dylan
publication:
  name: Context Reinforcement
  description: Re-review docs and correct behavioral drift
---

# Content here...
```

## Adding Content

### Adding a Prompt

1. Create a markdown file with frontmatter
2. Compute SHA-256 hash: `shasum -a 256 your-prompt.md`
3. Rename file to `{hash}.md` and place in `prompts/`
4. Add entry to `prompts/index.json`
5. Submit a PR

### Adding a Template

1. Create `templates/{name}/meta.json`:
   ```json
   {
     "name": "your-template",
     "description": "Brief description",
     "author": "Your Name",
     "version": "1.0.0",
     "prompts": {
       "en": ["hash1", "hash2"],
       "zh": ["hash3", "hash4"]
     },
     "files": ["CLAUDE.md"]
   }
   ```
2. Add entry files to `templates/{name}/files/{lang}/`
3. Add entry to `templates/index.json`
4. Submit a PR

## License

MIT
