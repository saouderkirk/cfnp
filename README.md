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
│   └── about/         # About page (subdirectory structure)
│       ├── page.jsonc # About page metadata
│       └── page.md    # About page content
├── templates/
│   └── templates/
│       └── cfnp.html  # Custom CFNP template
└── kixx-config.jsonc  # Kixx configuration
```

## Kixx Documentation

This project contributed to comprehensive Kixx framework documentation created during development.

**👉 [Kixx Community Docs](https://github.com/saouderkirk/kixx-community-docs)**

The documentation includes:
- Quick reference for AI coding assistants
- Critical conventions and gotchas
- Deployment guides (Railway, Render, VPS)
- Troubleshooting common errors
- Real-world examples

Perfect for developers new to Kixx or AI agents needing context about the framework.

## Deployment

This is a Node.js application that requires a VPS or PaaS hosting provider (Railway, Render, DigitalOcean, etc.). Shared hosting will not work.

**Live site**: [consultingfornormalpeople.com](https://consultingfornormalpeople.com)

## License

Copyright © 2025 Consulting for Normal People

---

Built with [Kixx](https://www.kixx.dev) • Generated with [Claude Code](https://claude.com/claude-code)
