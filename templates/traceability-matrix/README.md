# Traceability Matrix

A requirements-to-tests traceability matrix for regulated software teams — supporting IEC 62304, ISO 13485, and 21 CFR Part 820 compliance.

## What's included

- **Requirements database** — track system requirements with status, description, and coverage status
- **Tests database** — track test cases and their latest execution results (pass/fail/skipped)
- **Many-to-many relationship** — link any requirement to any number of tests and vice versa
- **`post-test.yml` GitHub Action** — automatically updates test run status and recomputes coverage after every CI run

## How it works

1. Add requirements to the **Requirements** database (`REQ-001`, `REQ-002`, …)
2. Add test cases to the **Tests** database (`TEST-001`, `TEST-002`, …)
3. Link them together using the relation fields
4. Configure `post-test.yml` with your test runner — it will update `last_run_status` and `coverage_status` after every push

## Setup

After installing, add the following secrets to your repository:

| Secret | Description |
|---|---|
| `LIGHTWORKS_API_TOKEN` | Org-scoped token with write access to databases |
| `LIGHTWORKS_ORG_ID` | Your Lightworks organization ID |

Then configure the test result path in `.github/workflows/post-test.yml` to match your test runner's output format (JUnit XML by default).
