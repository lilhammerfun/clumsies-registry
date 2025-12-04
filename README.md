# clumsies-registry

Official template registry for [clumsies](https://github.com/dylanwangeth/clumsies).

## Structure

```
clumsies-registry/
├── index.json              # Auto-generated template index
└── <template-name>/
    ├── meta.json           # Template metadata
    ├── en/                 # English version
    │   ├── CLAUDE.md       # Meta-prompt file
    │   └── prompts/        # Prompt files
    └── zh/                 # Chinese version
        ├── CLAUDE.md
        └── prompts/
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

## Adding a Template

1. Create a directory with your template name
2. Add `meta.json`:
   ```json
   {
     "name": "your-template",
     "task": "code",
     "keywords": ["keyword1", "keyword2"],
     "description": "Brief description",
     "languages": ["en", "zh"],
     "author": "Your Name",
     "version": "1.0.0"
   }
   ```
3. Add language directories (`en/`, `zh/`) with `CLAUDE.md` and `prompts/`
4. Submit a PR

The `index.json` is auto-generated from `meta.json` files via GitHub Actions.

## License

MIT
