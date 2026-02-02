# Tasks: Migrate to Bun

## 1. Update Makefile

- [x] 1.1 Replace all `node` commands with `bun` in test targets (test, test-all, test-api, test-pbt)
- [x] 1.2 Replace all `node` commands with `bun` in config target
- [x] 1.3 Replace `npx http-server` with `bun x http-server` in serve target
- [x] 1.4 Update runtime detection in serve target from checking `node` to checking `bun`
- [x] 1.5 Update error messages to reference Bun installation instead of Node.js
- [x] 1.6 Update help text and comments to reference Bun where appropriate

## 2. Update GitHub Actions Workflows

- [x] 2.1 Replace `actions/setup-node@v4` with `oven-sh/setup-bun@v2` in deploy.yml
- [x] 2.2 Add `bun-version: latest` to setup-bun configuration in deploy.yml
- [x] 2.3 Replace all `node` commands with `bun` in deploy.yml test steps
- [x] 2.4 Replace all `node` commands with `bun` in deploy.yml config generation steps
- [x] 2.5 Update junie.yml workflow if it uses Node.js (check file first)

## 3. Update Documentation

- [x] 3.1 Update README.md with Bun installation instructions instead of Node.js
- [x] 3.2 Replace all command examples in README.md from `node` to `bun`
- [x] 3.3 Update docs/GITHUB_ACTIONS_SETUP.md to reference Bun in workflow descriptions
- [x] 3.4 Update docs/YOUTUBE_API_SETUP.md command examples from `node` to `bun`
- [x] 3.5 Add migration notes for existing contributors explaining the Bun requirement

## 4. Testing and Verification

- [x] 4.1 Test `make test` locally with Bun installed
- [x] 4.2 Test `make test-all` locally with Bun installed
- [x] 4.3 Test `make config` locally with Bun installed (with YOUTUBE_API_KEY)
- [x] 4.4 Test `make serve` locally with Bun installed
- [x] 4.5 Verify all test outputs match Node.js behavior
- [ ] 4.6 Push to feature branch and verify GitHub Actions workflows pass
- [ ] 4.7 Verify CI/CD test execution completes successfully
- [ ] 4.8 Verify CI/CD config generation works with API key

## 5. Cleanup and Documentation

- [x] 5.1 Review all changes for consistency
- [x] 5.2 Ensure no references to Node.js remain in user-facing documentation
- [x] 5.3 Add troubleshooting section to README for common Bun installation issues
- [x] 5.4 Update any inline code comments that reference Node.js
- [ ] 5.5 Create PR with comprehensive description of changes and testing performed
