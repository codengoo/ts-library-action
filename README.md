# Build & Publish Template Workflow

This repository provides a reusable GitHub Actions workflow for building, testing, and publishing npm packages. It is designed to be inherited and executed by other repositories via `workflow_call`.

## Usage

In your downstream repository, reference this workflow in your `.github/workflows/your-workflow.yml`:

```yaml
jobs:
  build-publish:
    uses: codengoo/ts-library-action/.github/workflows/deploy.yml@main
    secrets: inherit
    with:
      node-version: '20.x'   # Optional, default: '20.x'
      publish: true          # Optional, default: false
```

## Inputs
- `node-version` (string, optional): Node.js version to use. Default: `20.x`
- `publish` (boolean, optional): Set to `true` to publish the package after build. Default: `false`

## Secrets
- `NPM_TOKEN` (optional): Required for publishing to npm. Pass via repository secrets.

## Workflow Steps
1. Checkout caller repository
2. Setup Node.js
3. Install dependencies (`npm ci`)
4. Run tests (`npm test`)
5. Build project (`npm run build`)
6. Publish package (`npm publish --access public`) if `publish` is `true` and `NPM_TOKEN` is provided

## Notes
- Only supports npm as the package manager.
- Make sure your project has a valid `package.json` and build/test scripts.
- For multi-repo usage, keep this workflow up-to-date and versioned.

---
Maintained by org/ci-templates.
