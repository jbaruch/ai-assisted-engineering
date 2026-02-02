# Spec: bun-build-system

## ADDED Requirements

### Requirement: Makefile uses Bun for script execution

The Makefile SHALL replace all `node` commands with `bun` commands for executing JavaScript files.

#### Scenario: Running test scripts with Bun

- **WHEN** a user runs `make test`
- **THEN** the Makefile SHALL execute `bun tests/test-core-functionality.js` instead of `node tests/test-core-functionality.js`

#### Scenario: Running config generation with Bun

- **WHEN** a user runs `make config`
- **THEN** the Makefile SHALL execute `bun generate-video-config.js` instead of `node generate-video-config.js`

#### Scenario: Running all test suites with Bun

- **WHEN** a user runs `make test-all`
- **THEN** the Makefile SHALL execute `bun tests/run-all-tests.js` instead of `node tests/run-all-tests.js`

### Requirement: Makefile uses bun x for package execution

The Makefile SHALL replace all `npx` commands with `bun x` commands for executing npm packages.

#### Scenario: Starting development server with bun x

- **WHEN** a user runs `make serve`
- **THEN** the Makefile SHALL execute `bun x http-server` instead of `npx http-server`

### Requirement: Makefile checks for Bun installation

The Makefile SHALL check for Bun availability instead of Node.js when verifying runtime prerequisites.

#### Scenario: Detecting Bun installation

- **WHEN** the serve target checks for available runtimes
- **THEN** it SHALL check for `bun` command availability using `command -v bun`

#### Scenario: Bun not found error message

- **WHEN** Bun is not installed and no fallback is available
- **THEN** the error message SHALL instruct users to install Bun instead of Node.js

### Requirement: GitHub Actions uses Bun runtime

GitHub Actions workflows SHALL use `oven-sh/setup-bun` action instead of `actions/setup-node` for JavaScript execution.

#### Scenario: Setting up Bun in CI/CD

- **WHEN** a GitHub Actions workflow initializes the runtime environment
- **THEN** it SHALL use `oven-sh/setup-bun@v2` with `bun-version: latest`

#### Scenario: Removing Node.js setup

- **WHEN** migrating a workflow to Bun
- **THEN** the workflow SHALL NOT include `actions/setup-node` steps

### Requirement: GitHub Actions executes scripts with Bun

GitHub Actions workflows SHALL replace all `node` commands with `bun` commands in run steps.

#### Scenario: Running tests in CI with Bun

- **WHEN** a workflow runs test scripts
- **THEN** it SHALL execute `bun tests/test-core-functionality.js` instead of `node tests/test-core-functionality.js`

#### Scenario: Generating config in CI with Bun

- **WHEN** a workflow generates video configuration
- **THEN** it SHALL execute `bun generate-video-config.js` instead of `node generate-video-config.js`

### Requirement: Documentation references Bun commands

All documentation files SHALL be updated to reference `bun` commands instead of `node` commands.

#### Scenario: README installation instructions

- **WHEN** a user reads the README.md setup instructions
- **THEN** it SHALL provide Bun installation steps instead of Node.js installation steps

#### Scenario: Command examples use Bun

- **WHEN** documentation shows command-line examples
- **THEN** it SHALL use `bun` instead of `node` (e.g., `bun generate-video-config.js` instead of `node generate-video-config.js`)

### Requirement: Backward compatibility with existing scripts

All existing JavaScript files SHALL execute without modification under Bun runtime.

#### Scenario: Executing existing JavaScript files

- **WHEN** any existing .js file is executed with `bun` instead of `node`
- **THEN** it SHALL produce identical output and behavior

#### Scenario: No code changes required

- **WHEN** migrating from Node.js to Bun
- **THEN** NO modifications SHALL be made to .js file contents (only execution commands change)
