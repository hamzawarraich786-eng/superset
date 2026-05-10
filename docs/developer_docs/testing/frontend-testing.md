---
title: Frontend Testing
sidebar_position: 2
---

<!--
Licensed to the Apache Software Foundation (ASF) under one
or more contributor license agreements.  See the NOTICE file
distributed with this work for additional information
regarding copyright ownership.  The ASF licenses this file
to you under the Apache License, Version 2.0 (the
"License"); you may not use this file except in compliance
with the License.  You may obtain a copy of the License at

  http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing,
software distributed under the License is distributed on an
"AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
KIND, either express or implied.  See the License for the
specific language governing permissions and limitations
under the License.
-->

# Frontend Testing

🚧 **Coming Soon** 🚧

Comprehensive guide for testing Superset's frontend components and features.

## Topics to be covered:

- Jest configuration and setup
- React Testing Library best practices
- Component testing strategies
- Redux store testing
- Async operations and API mocking
- Snapshot testing guidelines
- Coverage requirements and reporting
- Debugging test failures
- Performance testing for UI components

## Quick Commands

```bash
# Run all frontend tests
npm run test

# Run tests in watch mode
npm run test -- --watch

# Run tests with coverage
npm run test -- --coverage

# Run specific test file
npm run test -- MyComponent.test.tsx
```

## Narrow frontend maintenance validation

For small, low-risk frontend maintenance changes — for example a dependency
or lockfile bump, a tweak to a single utility, or an edit to one Jest test
file — prefer running narrow validation scoped to the files you touched
rather than the full frontend build or the entire test suite.

All commands below are defined in `superset-frontend/package.json` and are
run from the `superset-frontend` directory.

- **Dependency or lockfile changes** (`package.json`, `package-lock.json`):

  ```bash
  # Verify the lockfile installs cleanly from a clean state
  npm ci
  ```

- **A small frontend utility change** (a single `.ts`/`.tsx` file):

  ```bash
  # Type-check the frontend (no emit)
  npm run type

  # Lint just the file(s) you changed
  npx oxlint --config oxlint.json --quiet path/to/changed-file.ts

  # Run the colocated test for that utility
  npm run test -- path/to/changed-file.test.ts
  ```

- **A focused frontend test change** (a single `*.test.ts`/`*.test.tsx`):

  ```bash
  # Run only that test file
  npm run test -- path/to/changed-file.test.ts
  ```

You can also run [`pre-commit`](https://pre-commit.com/) against only the
files you changed, which is much faster than `--all-files`:

```bash
# From the repo root, after `git add`-ing your changes
pre-commit run --files superset-frontend/path/to/changed-file.ts
```

Avoid `npm run build`, `npm run cover`, and unfiltered `npm run test` for
this class of change — they are slow and broader than the change warrants.
CI will still run the full suite on the pull request.

---

*This documentation is under active development. Check back soon for updates!*
