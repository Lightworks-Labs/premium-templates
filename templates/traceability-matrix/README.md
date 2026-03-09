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

## Fields

### Requirements

| Field | Type | Description |
|---|---|---|
| `req_id` | text | Human-readable ID, e.g. `REQ-001` |
| `title` | text | Short requirement statement |
| `description` | text | Full requirement text |
| `status` | select | `draft` · `active` · `deprecated` |
| `linked_tests` | relation | Linked test cases |
| `coverage_status` | select | `uncovered` · `partial` · `covered` — updated by Action |

### Tests

| Field | Type | Description |
|---|---|---|
| `test_id` | text | Human-readable ID, e.g. `TEST-001` |
| `title` | text | Short test description |
| `linked_requirements` | relation | Linked requirements |
| `last_run_status` | select | `pending` · `passed` · `failed` · `skipped` — updated by Action |
| `last_run_at` | date | Timestamp of last execution — updated by Action |
| `run_url` | url | Link to CI run — updated by Action |
