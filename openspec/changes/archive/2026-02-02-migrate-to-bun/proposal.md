# Migrate to Bun

## Why

Node.js and npm have served the project well, but Bun offers significantly faster execution, built-in testing, and simpler dependency management. Migrating to Bun will improve developer experience through faster local development, reduce CI/CD pipeline execution time, and eliminate the need for external test runners while maintaining full compatibility with existing JavaScript code.

## What Changes

- Replace all `node` commands with `bun run` or `bun` in build scripts and development workflows
- Update GitHub Actions workflows to use `oven-sh/setup-bun` instead of `actions/setup-node`
- Modify Makefile targets to use Bun instead of Node.js and npm/npx
- Update documentation (README.md, GITHUB_ACTIONS_SETUP.md, YOUTUBE_API_SETUP.md) to reference Bun commands
- Replace npm-specific tooling references (csso-cli, uglify-js via npm) with Bun-native or compatible alternatives
- Update test execution to use Bun's built-in test runner where applicable
- Preserve backward compatibility by maintaining the same script entry points

## Capabilities

### New Capabilities

- `bun-build-system`: Bun-based build and execution system replacing Node.js/npm in all scripts, CI/CD pipelines, and development workflows
- `bun-test-execution`: Standardized test execution using Bun's runtime across all test suites

### Modified Capabilities

<!-- No existing spec-level requirement changes - this is primarily an implementation/tooling change -->

## Impact

**Code Changes:**

- Makefile: All `node` and `npx` commands → `bun` or `bun run`
- GitHub Actions workflows: `.github/workflows/deploy.yml`, `.github/workflows/junie.yml`
- Documentation: `README.md`, `docs/GITHUB_ACTIONS_SETUP.md`, `docs/YOUTUBE_API_SETUP.md`

**Dependencies:**

- Remove: Node.js setup steps
- Add: Bun installation/setup in CI/CD

**Scripts Affected:**

- `generate-video-config.js`
- `generate-config.js`
- All test files in `tests/` directory
- Build and minification commands

**Breaking Changes:**

- **BREAKING**: Contributors must install Bun instead of Node.js for local development
- **BREAKING**: CI/CD environments must have Bun available (GitHub Actions workflows will be updated)
