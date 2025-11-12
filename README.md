# Consulting for Normal People

A professional consulting website built with the [Kixx framework](https://www.kixx.dev).

## About

CFNP (Consulting for Normal People) is a consulting service that provides high-impact strategy and execution support without corporate theater or inflated fees.

## Tech Stack

- **Framework**: Kixx 5.2.0
- **Runtime**: Node.js
- **Template Engine**: Kixx's built-in Handlebars-like engine
- **Content**: Markdown + JSON metadata

## Local Development

```bash
# Install dependencies
npm install

# Run development server
npx kixx app-server --environment development

# Server runs at http://localhost:3001
```

## Project Structure

```
.
├── pages/              # Page content and metadata
│   ├── page.jsonc     # Homepage metadata
│   ├── page.md        # Homepage content
│   ├── about.jsonc    # About page metadata
│   └── about.md       # About page content
├── templates/
│   └── templates/
│       └── cfnp.html  # Custom CFNP template
├── kixx-config.jsonc  # Kixx configuration
└── kixx-docs/         # Framework documentation
```

## Deployment

See deployment guide in `kixx-docs/` for instructions on deploying to production.

## Documentation

Comprehensive Kixx framework documentation is available in the [`kixx-docs/`](./kixx-docs/) directory, including:

- [Agent Reference](./kixx-docs/AGENT_REFERENCE.md) - Quick reference for AI assistants
- [How-To Guides](./kixx-docs/how-to-guides/) - Step-by-step tutorials
- [Conventions](./kixx-docs/conventions/) - File naming and project structure
- [Troubleshooting](./kixx-docs/troubleshooting/) - Common errors and solutions

## License

Copyright © 2025 Consulting for Normal People

---

Built with [Kixx](https://www.kixx.dev) • Generated with [Claude Code](https://claude.com/claude-code)
