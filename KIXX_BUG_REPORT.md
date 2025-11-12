# Kixx 6.0.0 Bug Report

## Summary
Kixx 6.0.0 has critical issues that prevent `init-project` and `app-server` from working on fresh installations.

## Environment
- **Kixx Version**: 6.0.0
- **Node Version**: >= 16.13.2
- **OS**: macOS (Darwin 23.5.0)
- **Installation Method**: `npm install kixx`

---

## Bug #1: Missing .gitignore in project-template

### Severity: Critical
### Affects: `npx kixx init-project`

### Description
The `init-project` command fails immediately because it attempts to copy a `.gitignore` file that doesn't exist in the `node_modules/kixx/project-template/` directory.

### Steps to Reproduce
```bash
mkdir test-kixx
cd test-kixx
npm init -y
npm install kixx
npx kixx init-project --name "Test App"
```

### Expected Result
Project scaffolding should be created successfully.

### Actual Result
```
There was an unexpected error while running "init-project":

Error: ENOENT: no such file or directory, copyfile '/path/to/node_modules/kixx/project-template/.gitignore' -> '/path/to/project/.gitignore'
```

### Root Cause
The file `node_modules/kixx/project-template/.gitignore` is missing from the npm package. This may be due to:
- `.gitignore` being excluded during npm publish (npm ignores `.gitignore` by default unless explicitly included in `files` array in package.json)
- Missing from the source repository

### Suggested Fix
1. Rename `.gitignore` to `gitignore.template` in the project-template directory
2. Update `cli/init-project.js` to rename it to `.gitignore` when copying
3. OR add `.gitignore` to the `files` array in package.json to ensure it's published

### Workaround
```bash
touch node_modules/kixx/project-template/.gitignore
npx kixx init-project --name "Test App"
```

---

## Bug #2: Missing Plugin Configuration - app.Root User Type

### Severity: Critical
### Affects: `npx kixx app-server`

### Description
Even after working around Bug #1, newly initialized Kixx 6.0.0 projects fail to start because the required "app.Root" user type is not configured.

### Steps to Reproduce
```bash
mkdir test-kixx
cd test-kixx
npm init -y
npm install kixx
touch node_modules/kixx/project-template/.gitignore
npx kixx init-project --name "Test App"
npx kixx app-server --environment development
```

### Expected Result
Server should start successfully on port 3000 (or configured port).

### Actual Result
```
There was an unexpected error while running "app-server":

WrappedError: Unable to get "app.Root" user constructor as root user. Ensure plugins have been loaded and the user type class "app.Root" is defined.
```

### Root Cause
Kixx 6.0.0 introduced a plugin system with user types, but:
1. The `init-project` command doesn't create the necessary plugin configuration
2. The project template doesn't include plugin setup
3. There's no documentation explaining how to configure plugins
4. The default project template is incompatible with v6.0.0

### Suggested Fix
1. Update `project-template/` to include default plugin configuration
2. Add plugin setup to `init-project` command
3. OR make the "app.Root" user type optional/default if no plugins are configured
4. Document the plugin system and migration path from 5.x to 6.x

### Questions for Maintainer
- Is the plugin system a required feature in 6.0.0?
- Should there be a default/minimal plugin configuration?
- Is there an example of a working 6.0.0 project with plugins?
- Should this be documented as a breaking change requiring migration steps?

---

## Bug #3: Development Port Configuration Ignored (v5.2.0)

### Severity: Medium
### Affects: Kixx 5.2.0 `app-server`

### Description
In Kixx 5.2.0, the `server.port` configuration for the "development" environment in `kixx-config.jsonc` is ignored. The server always binds to port 3001 regardless of the configured port.

### Steps to Reproduce
1. Create a Kixx 5.2.0 project
2. Set development port in kixx-config.jsonc:
```jsonc
{
    "environments": {
        "development": {
            "server": {
                "port": 3002  // or any port other than 3001
            }
        }
    }
}
```
3. Start server: `npx kixx app-server --environment development`

### Expected Result
Server listens on configured port (3002).

### Actual Result
Server always listens on port 3001:
```
INFO  cfnp server listening on port 3001 - { port: 3001 }
```

### Note
- This bug was **only tested on v5.2.0** and may be fixed in v6.0.0
- Unable to verify on v6.0.0 due to Bug #2 preventing server startup
- May be related to how environment configuration is resolved
- Lower priority than bugs #1 and #2

---

## Additional Context

### Testing Notes
- Tested on fresh installations (no pre-existing project files)
- Tested with Node.js versions >= 16.13.2
- Both bugs #1 and #2 are blocking issues that prevent any use of Kixx 6.0.0
- Bug #3 is present in 5.2.0 but is a lower priority

### Impact
**Kixx 6.0.0 is currently unusable** due to these bugs. Users cannot:
- Initialize new projects (Bug #1)
- Run projects even after manual workarounds (Bug #2)

### Recommendation
Consider:
1. **Yanking version 6.0.0 from npm** until these critical bugs are fixed
2. **Publishing a hotfix release (6.0.1)** with fixes for bugs #1 and #2
3. **Adding integration tests** that verify `init-project` && `app-server` work on fresh installs
4. **Documenting breaking changes** between 5.x and 6.x

---

## Willing to Contribute

I'm happy to submit a PR to fix these issues if you can provide guidance on:
1. The intended plugin system design for 6.0.0
2. Whether .gitignore should be renamed or included in package.json files array
3. What the default/minimal plugin configuration should look like

---

## Related Files
- `cli/init-project.js` - Handles project initialization
- `lib/application/application.js:408` - Where plugin initialization fails
- `project-template/` - Missing .gitignore and plugin config

## Links
- Kixx npm: https://www.npmjs.com/package/kixx
- Kixx website: https://www.kixx.dev
- Repository: https://github.com/kixx-platform/kixx (assumed)
