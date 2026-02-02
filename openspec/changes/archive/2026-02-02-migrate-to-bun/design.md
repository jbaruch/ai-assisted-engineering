# Design: Migrate to Bun

## Context

The project currently uses Node.js v18 with npm/npx for script execution, testing, and CI/CD workflows. All JavaScript files are executed using `node` commands in the Makefile and GitHub Actions. The project has no package.json or formal dependency management - it relies on globally installed npm packages (csso-cli, uglify-js, http-server) and uses Node.js purely as a JavaScript runtime.

**Current State:**
- Makefile uses `node` for all script execution (tests, config generation)
- GitHub Actions uses `actions/setup-node@v4` with Node.js 18
- Documentation references `node` commands throughout
- No package.json - dependencies installed globally via npm

**Constraints:**
- Must maintain compatibility with existing JavaScript files (no code changes required)
- Scripts must work identically after migration (same inputs/outputs)
- CI/CD pipelines must continue to pass all tests
- Local development setup should remain simple

## Goals / Non-Goals

**Goals:**

- Replace all `node` command invocations with `bun` equivalents
- Update GitHub Actions to use Bun instead of Node.js
- Improve script execution speed (Bun is typically 3-4x faster than Node.js)
- Simplify dependency management by using Bun's built-in capabilities
- Update all documentation to reflect Bun usage
- Maintain 100% backward compatibility with existing JavaScript code

**Non-Goals:**

- Rewriting JavaScript files to use Bun-specific APIs
- Creating a package.json or formal dependency management system
- Converting to TypeScript or other language features
- Migrating to Bun's native test framework (continue using existing test files as-is)
- Performance optimization beyond runtime replacement

## Decisions

### Decision 1: Direct command replacement (node → bun)

**Choice:** Replace `node script.js` with `bun script.js` (not `bun run script.js`)

**Rationale:** 
- Bun can directly execute JavaScript files just like Node.js
- `bun script.js` is the simplest 1:1 replacement
- `bun run` is for package.json scripts, which this project doesn't use
- Minimal diff in all files (just replace the command name)

**Alternatives considered:**
- `bun run script.js`: More verbose, unnecessary without package.json
- Keep `node` with Bun installed: Defeats the purpose, no performance gains

### Decision 2: Use oven-sh/setup-bun@v2 in GitHub Actions

**Choice:** Replace `actions/setup-node@v4` with `oven-sh/setup-bun@v2`

**Rationale:**
- Official Bun action from the Bun team
- Similar interface to setup-node (specify version with `bun-version`)
- Well-maintained and widely used
- Supports caching and all major platforms

**Alternatives considered:**
- Manual Bun installation via curl: More fragile, no caching
- Keep Node.js alongside Bun: Unnecessary complexity

### Decision 3: Replace npx with bun x

**Choice:** Replace `npx http-server` with `bun x http-server`

**Rationale:**
- `bun x` is Bun's equivalent to npx for running packages
- Downloads and caches packages automatically
- Faster than npx
- Same user experience (no global install needed)

**Alternatives considered:**
- Install http-server globally: Requires extra setup step
- Use Bun's built-in server: Would require code changes (non-goal)

### Decision 4: Keep global minification tools (csso, uglifyjs) for now

**Choice:** Continue checking for globally installed csso and uglifyjs in Makefile

**Rationale:**
- These are optional development tools, not core functionality
- Bun can execute them if they're installed
- Replacing with Bun-native alternatives is out of scope
- Makefile already handles missing tools gracefully

**Alternatives considered:**
- Migrate to Bun-native minifiers: Would require research and testing
- Create package.json with dependencies: Adds complexity, not needed

### Decision 5: Version specification in CI/CD

**Choice:** Pin to latest stable Bun version (e.g., `bun-version: latest`)

**Rationale:**
- Bun is stable and maintains backward compatibility
- Using latest ensures performance improvements and bug fixes
- Can pin to specific version if issues arise
- Project has no package.json to lock versions

**Alternatives considered:**
- Pin to specific version: More stable but requires manual updates
- Use version range: Not supported by setup-bun action

## Risks / Trade-offs

**Risk 1: Bun compatibility issues with existing JavaScript**
→ Mitigation: Bun is Node.js-compatible by design. All current scripts use standard JavaScript (no Node.js-specific APIs). Run full test suite after migration to verify.

**Risk 2: Contributors unfamiliar with Bun**
→ Mitigation: Update README with clear installation instructions. Bun installation is simpler than Node.js (single curl command). Add troubleshooting section.

**Risk 3: CI/CD failure if setup-bun action has issues**
→ Mitigation: setup-bun is well-maintained and stable. Can quickly revert GitHub Actions workflows if needed (Git history preserved).

**Risk 4: Different behavior between Bun and Node.js**
→ Mitigation: Comprehensive testing before and after migration. Existing test suite validates all functionality. Any differences will be caught in CI/CD.

**Risk 5: Global npm packages (csso, uglifyjs) may not work with Bun**
→ Mitigation: These are optional build tools. Makefile already handles their absence gracefully. Can migrate to alternatives in future if needed.

**Trade-off 1: Breaking change for contributors**
Contributors must install Bun instead of Node.js. This is a one-time setup change with long-term benefits (faster development experience).

**Trade-off 2: Smaller ecosystem**
Bun's ecosystem is newer than Node.js, but this project uses standard JavaScript without dependencies, minimizing risk.

## Migration Plan

**Phase 1: Update Makefile**
1. Replace all `node` commands with `bun`
2. Replace `npx http-server` with `bun x http-server`
3. Update help text and error messages to reference Bun
4. Test locally: `make test`, `make test-all`, `make config`, `make serve`

**Phase 2: Update GitHub Actions**
1. Replace `actions/setup-node@v4` with `oven-sh/setup-bun@v2`
2. Update all `node` commands to `bun` in workflow steps
3. Test in CI: Push to feature branch and verify all workflows pass
4. Merge to main after successful CI run

**Phase 3: Update Documentation**
1. README.md: Replace Node.js installation with Bun installation
2. GITHUB_ACTIONS_SETUP.md: Update references to Bun
3. YOUTUBE_API_SETUP.md: Change command examples from `node` to `bun`
4. Add migration notes for contributors

**Phase 4: Verification**
1. Run full test suite locally with Bun
2. Verify CI/CD pipelines pass
3. Test local development server
4. Validate config generation works identically

**Rollback Strategy:**
- Git revert commits if issues arise
- All changes are in infrastructure (scripts, CI/CD), not application logic
- Can rollback individual components (Makefile, GitHub Actions) independently
- No data migration or state changes involved

## Open Questions

None - all decisions have been made and documented above.
