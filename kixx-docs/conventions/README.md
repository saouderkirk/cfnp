# Conventions Reference

All the conventions Kixx uses to reduce configuration and code.

## Directory Structure

### Standard Project Layout

```
my-kixx-app/
├── kixx-config.jsonc       # Application configuration
├── virtual-hosts.jsonc     # Virtual host routing
├── package.json           # Node.js dependencies
├── pages/                 # Page content and metadata
├── routes/                # Route definitions
└── templates/             # HTML templates
    ├── templates/         # Main templates
    └── partials/          # Reusable template parts
```

**TODO**: Document optional directories and their purposes.

---

## File Naming Conventions

### Pages Directory

**CRITICAL - Path Mapping Rules**:

Kixx strips "index" from URL paths when mapping to files. This is the most important convention to understand:

| URL Path | Maps To | NOT |
|----------|---------|-----|
| `/` | `pages/page.jsonc` | ~~`pages/index.jsonc`~~ |
| `/about` | `pages/about.jsonc` OR `pages/about/page.jsonc` | ~~`pages/about/index.jsonc`~~ |
| `/blog/post` | `pages/blog/post.jsonc` OR `pages/blog/post/page.jsonc` | ~~`pages/blog/post/index.jsonc`~~ |

**File Types**:
- `page.jsonc` - Page metadata (title, description, baseTemplateId)
- `page.md` - Markdown content (compiled to HTML)
- `page.html` - Custom HTML content

**Key Rules**:
1. **Always use `page.jsonc`**, never `index.jsonc` (even for the homepage)
2. Metadata and content are separate files with the same base name
3. Path `/about/index` and `/about` both map to the same file (index is stripped)

### Routes Directory

**What we know**:
- `*.jsonc` files define routes
- Routes reference pages by name

**TODO**: Document:
- Naming conventions for route files
- How multiple route files are loaded
- Load order if it matters

### Templates Directory

**What we know**:
- `templates/` contains main templates like `base.html`
- `partials/` contains reusable components

**TODO**: Document:
- Naming conventions
- How templates are discovered
- Default template names

---

## Configuration Conventions

### kixx-config.jsonc

**What we know**:
```jsonc
{
    "name": "App Name",
    "processName": "appname",
    "environments": {
        "development": { /* config */ },
        "production": { /* config */ }
    }
}
```

**TODO**: Document:
- All available configuration keys
- Default values for each
- Which settings can be overridden

### virtual-hosts.jsonc

**What we know**:
- Hostnames are written backwards: `"com.example.subdomain"`
- Routes use protocols: `"app://file.jsonc"` or `"kixx://defaults.json"`

**TODO**: Document:
- Hostname matching rules
- Available route protocols
- Route resolution order

---

## Routing Conventions

### Route Definitions

**What we know**:
```jsonc
{
    "methods": ["GET"],
    "path": "/about",
    "handler": "PageHandler",
    "page": "about"
}
```

**TODO**: Document:
- All available handler types
- All route configuration options
- Path parameter syntax
- HTTP method conventions

---

## Template Conventions

### Template Syntax

**What we know**:
- Handlebars-like syntax
- `{{> partial.html}}` for partials
- `{{#if condition}}` for conditionals
- `{{ variable }}` for interpolation
- `{{noop body}}` for special placeholders

**TODO**: Document:
- All available syntax
- Context variables available in templates
- Helper function conventions

### Special Variables

**What we know from templates**:
- `title` - Page title
- `description` - Page description
- `openGraph` - Open Graph metadata
- `canonicalURL` - Canonical URL
- `body` - Page content

**TODO**: Document all available context variables.

---

## Page Metadata Conventions

### Standard Metadata Fields

**Required Structure** (`pages/page.jsonc`):
```jsonc
{
    "title": "Page Title",
    "description": "Page description",
    "baseTemplateId": "base.html"
}
```

**CRITICAL**: Use `baseTemplateId` (not `template`!) and include the `.html` extension.

**Known Fields**:
- `title` - Page title (processed as template, can include {{variables}})
- `description` - Meta description (processed as template)
- `baseTemplateId` - Template file name with extension (e.g., `"custom.html"`)
- `canonicalURL` - Canonical URL (auto-generated if not provided)
- `contentType` - Override content type (defaults to `text/html`)
- `openGraph` - Open Graph metadata object:
  - `type` - OG type (defaults to `"website"`)
  - `title` - OG title (defaults to page title)
  - `description` - OG description
  - `image` - OG image URL

**Default Behavior**:
- If no `baseTemplateId` specified, uses `base.html`
- Title and description support Handlebars syntax: `"title": "Welcome, {{userName}}"`
- Open Graph metadata auto-populated from page metadata

**TODO**: Document other available metadata fields beyond what we've discovered.

---

## Environment Conventions

### Environment Names

**What we know**:
- `development` - Dev environment
- `production` - Production environment

**TODO**: Document:
- Can you create custom environments?
- How to select environment at runtime
- Environment-specific conventions

---

## Default Behaviors

### Default Routes
**TODO**: Document what `"kixx://defaults.json"` includes.

### Default Templates
**TODO**: Document if there are default templates provided.

### Default Error Pages
**TODO**: Document how error pages work by default.

---

## Overriding Conventions

**TODO**: Document how to override any convention when needed.
