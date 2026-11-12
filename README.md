# IMAIF backend (Phases 6B1–7C5)

This backend is independent of the React app. It contains the FastAPI foundation, validated settings, PostgreSQL connection/session plumbing, seven SQLAlchemy entities, the initial Alembic migration, project/resource/version/revision/distribution APIs, and the local Phase 7 syllabus extraction, indexing, retrieval, and single-resource generation flow. Recipient updates, real delivery, authentication, local-storage import execution, and regeneration APIs remain deferred. Phase 7D frontend integration is described below.

## Requirements

- Python 3.10 or newer (developed and checked with Python 3.14.4 in this environment).
- A locally supported PostgreSQL release for applying migrations and integration testing (not available in the implementation environment).
- PostgreSQL is needed for the readiness endpoint to report ready; the API process itself can start while PostgreSQL is stopped.

## Windows PowerShell setup

From the repository root:

```powershell
Set-Location backend
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install -r requirements-dev.txt
Copy-Item .env.example .env
```

If PowerShell blocks virtual-environment activation, use this for the current terminal only:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
.\.venv\Scripts\Activate.ps1
```

Edit `.env` to match a local PostgreSQL database. The example contains development placeholders only; replace them locally and never commit `.env`. Use URL-encoded characters if a local password contains reserved URL characters.

## Create a local development database

Install PostgreSQL locally and use a dedicated development role/database. In PowerShell, connect as a PostgreSQL administrator and create the role and database (replace the local-only password):

```powershell
psql -U postgres -c "CREATE ROLE imaif WITH LOGIN PASSWORD 'choose-a-local-password';"
psql -U postgres -c "CREATE DATABASE imaif OWNER imaif;"
```

Set `DATABASE_URL` in `backend/.env` to match, for example:

```text
DATABASE_URL=postgresql+psycopg://imaif:choose-a-local-password@localhost:5432/imaif
```

The role and password above are for local development only. Keep the real local `.env` untracked. Do not point destructive development downgrades at a database containing data you need.

## Models

`app/models/` contains the seven tables from `docs/backend/DATABASE_DESIGN.md`: `projects`, `resources`, `resource_versions`, `component_revisions`, `distributions`, `distribution_recipients`, and `migration_batches`. `app/models/__init__.py` imports every entity so Alembic sees the complete `Base.metadata`.

The schema uses PostgreSQL UUID, JSONB, and timezone-aware timestamps; named check/unique/foreign-key constraints; and explicit indexes. Related rows use `ON DELETE RESTRICT`. A resource's current-version pointer and a version's parent pointer are constrained to the same resource. Each resource version is a complete snapshot; distributions reference an exact `resource_versions.id`. Component revision rows are append-only history events linked to their before/after resource versions. No model operation creates a table automatically.

## Alembic migrations

`alembic/env.py` reads `DATABASE_URL` from the existing Pydantic Settings object and uses `Base.metadata` for autogeneration. Migration scripts are stored in `alembic/versions/`. All schema changes must be made through Alembic; do not call `Base.metadata.create_all()`.

With the virtual environment active and the shell in `backend/`:

```powershell
# Apply migrations to the configured development database.
python -m alembic upgrade head

# Inspect local migration history and the configured database revision.
python -m alembic history
python -m alembic heads
python -m alembic current

# Inspect tables and representative constraints in psql.
psql -U imaif -d imaif -c "SELECT version_num FROM alembic_version;"
psql -U imaif -d imaif -c "\dt"
psql -U imaif -d imaif -c "\d+ resource_versions"
```

After changing models, create a reviewable migration, inspect its Python operations, then apply it to a disposable development database:

```powershell
python -m alembic revision --autogenerate -m "describe the schema change"
python -m alembic upgrade head
```

The initial migration is `6b2_initial_schema`. Its downgrade removes all seven application tables and their data. To test that downgrade, use only a disposable database with no data to preserve:

```powershell
python -m alembic downgrade -1
python -m alembic upgrade head
```

Never downgrade or otherwise run destructive migration operations against a database containing user data. Take and verify a backup before any production schema operation. Do not edit an already-applied migration; create a new revision instead.

## Tests

From `backend/` with the environment active:

```powershell
python -m pytest -q
```

The suite checks model imports/relationships and constraints, PostgreSQL DDL compilation, mocked-session project/resource/distribution APIs, PDF upload validation, temporary extraction, local indexing/retrieval, and provider-independent generation. Chroma-backed upload/retrieval tests use an ephemeral Chroma client and fake embeddings; they do not require Ollama or PostgreSQL. On Windows, run TestClient-based tests outside environments that block local socketpair creation. Mocked API tests do not prove PostgreSQL integration. A local PostgreSQL server is required for applying migrations and database integration tests.

To validate the initial migration's PostgreSQL SQL without a server:

```powershell
python -m alembic upgrade head --sql
python -m alembic downgrade 6b2_initial_schema:base --sql
```

## Run and inspect the API

```powershell
uvicorn app.main:app --reload
```

The service listens at `http://127.0.0.1:8000` by default.

- Liveness: `http://127.0.0.1:8000/api/v1/health/live` — independent of PostgreSQL.
- Readiness: `http://127.0.0.1:8000/api/v1/health/ready` — runs `SELECT 1`; responds with HTTP 503 when PostgreSQL cannot be reached.
- Swagger UI: `http://127.0.0.1:8000/docs`.

## Local generation (Phase 7C5)

Create an active project with the requested resource type, upload a text-based PDF through `POST /api/v1/projects/{project_id}/syllabus`, then call `POST /api/v1/projects/{project_id}/generate` with the returned ingestion ID:

```json
{"resource_type":"Notes","learning_level":"Beginner","ingestion_id":"<upload-response-ingestion-id>"}
```

The local Ollama provider must be running with the configured model available. A successful request creates an unsaved resource and its initial immutable version. Generated content has only passed structural validation; teacher review is still required. See [`docs/backend/PHASE_7C5_HANDOVER.md`](../docs/backend/PHASE_7C5_HANDOVER.md) for the manual check and limitations.

## Project API (Phase 6C1)

All routes use the `/api/v1` prefix and JSON fields use `snake_case`.

| Method | Path | Behavior |
| --- | --- | --- |
| `POST` | `/api/v1/projects` | Create a project; returns `201`, the project representation, and a `Location` header. |
| `GET` | `/api/v1/projects` | List active projects with pagination and filters. |
| `GET` | `/api/v1/projects/{project_id}` | Get an active project and summaries of its current, non-archived resources. |
| `PATCH` | `/api/v1/projects/{project_id}` | Update supplied project fields only; returns `200`. |
| `DELETE` | `/api/v1/projects/{project_id}` | Soft-archive the project and preserve related history; returns `204`. |

Create request example:

```json
{
  "title": "Fractions in Everyday Life",
  "subject": "Mathematics",
  "grade": "Class 6",
  "board": "CBSE",
  "objectives": "Explain fractions using familiar examples.",
  "learning_level": "Beginner",
  "requested_resource_types": ["Notes", "Quizzes"],
  "syllabus_file_name": "fractions.pdf"
}
```

List supports `page` (default `1`), `page_size` (default `20`, maximum `100`), `search`, `subject`, `grade`, `learning_level`, and `sort`. Search is trimmed and case-insensitive. Sort accepts `created_at`, `updated_at`, or `title`, with an optional `-` prefix for descending order. Ties use project ID for stable ordering. The response contains `items` and `pagination` (`page`, `page_size`, `total_items`, `total_pages`).

Update example:

```http
PATCH /api/v1/projects/05be07ed-99a9-4cae-943f-099b23ce21c6
Content-Type: application/json
```

```json
{"objectives":"Compare equivalent fractions using visual models."}
```

Project errors use the documented `error` envelope with `code`, `message`, `details`, and `request_id`. Invalid bodies/filters return `422`, missing or archived IDs return `404`, database constraint conflicts return a sanitized `409`, and unexpected SQLAlchemy failures return a sanitized `500`.

**Ownership limitation:** Phase 6A leaves teacher identity and ownership unresolved and defines no authentication behavior. These project routes currently access the single local-development dataset without teacher scoping. Do not expose them as production multi-teacher APIs. No fake authentication is used.

Resource and distribution routes (Phases 6C2A–6C3B):

| Method | Path | Behavior |
| --- | --- | --- |
| `POST` | `/api/v1/projects/{project_id}/resources` | Create a resource and immutable initial version in one transaction. |
| `GET` | `/api/v1/resources` | List active resources with documented filters, pagination, and stable sorting. |
| `GET` | `/api/v1/resources/{resource_id}` | Get resource identity and its current snapshot. |
| `DELETE` | `/api/v1/resources/{resource_id}` | Soft-archive the resource; preserve versions and related records. |
| `PUT` | `/api/v1/resources/{resource_id}/saved` | Set or clear library saved state and timestamp. |
| `PATCH` | `/api/v1/resources/{resource_id}` | Append an immutable snapshot from partial metadata/content changes using `expected_current_version_id`; returns `201`, or `409` for a stale version. |
| `GET` | `/api/v1/resources/{resource_id}/versions` | List snapshots with pagination, newest version first by default. |
| `GET` | `/api/v1/resources/{resource_id}/versions/{version_id}` | Read the complete snapshot if it belongs to the active resource. |
| `POST` | `/api/v1/resources/{resource_id}/versions/{version_id}/restore` | Append the selected snapshot as a new current `restore` version; requires `expected_current_version_id`, accepts optional feedback, returns `201`. |
| `GET` | `/api/v1/resources/{resource_id}/component-revisions` | List immutable component revision events, optionally filtered by `component_key`, with pagination. |
| `POST` | `/api/v1/resources/{resource_id}/component-revisions/{revision_id}/restore` | Restore the selected event's `before` or `after` content into a new current snapshot and append a corresponding revision event. |
| `POST` | `/api/v1/distributions` | Create a prepared distribution for a saved current version and one or more recipients; this records intent only. |
| `GET` | `/api/v1/distributions` | List prepared distributions with documented filters, pagination, exact referenced-version metadata, and recipient counts. |
| `GET` | `/api/v1/distributions/{distribution_id}` | Read a distribution and its persisted recipient snapshots using its exact referenced version. |

Saved state does not mutate the immutable version snapshot. The endpoint follows the contract's save/unsave behavior; a separate acceptance workflow is not part of Phase 6C2A. The Phase 6C2B1 PATCH, Phase 6C2B3 resource restore, and Phase 6C2C2 component restore endpoints lock the resource row, check expected current versions, and atomically append snapshots and advance the pointer. Component restoration also appends an event that records current before-content, selected restored after-content, and `restores_revision_id`; selected historical events are never changed. New component events increment the per-resource/component revision number. Component restoration clears saved state. Phase 6C2B2 history/detail and Phase 6C2C1 component revision history remain read-only. These APIs use mocked sessions; transaction and row-lock behavior have not been verified against live PostgreSQL. Component revision creation, recipient management, real delivery, and local-storage import remain unimplemented.

Distribution creation stores the exact saved current `resource_version_id`, distribution learning level, class name, and recipient snapshots in one transaction. New records use `prepared_demo` and `version_resolution=native`. Student references are optional; duplicate non-null references in one request are rejected. Recipient status is not part of the current schema. Distribution listing/detail reads derive metadata from the exact referenced version; archived resource history remains available through distribution records. Reads do not mutate records. These endpoints do not send email, notifications, or assignments and do not contact students. PostgreSQL integration and live transaction behavior remain unverified; API tests use mocked sessions.

The Vite development origins `http://localhost:5173` and `http://127.0.0.1:5173` are allowed by CORS. Credentials are not allowed.

## Troubleshooting

- **`python` not found:** install Python 3.10+ and ensure it is on `PATH`; reopen PowerShell.
- **Invalid `DATABASE_URL`:** use a PostgreSQL URL with a host and database, such as `postgresql+psycopg://user:password@localhost:5432/imaif`.
- **Readiness returns 503:** confirm PostgreSQL is running, the database exists, and the local username/password/port in `.env` are correct. The API intentionally remains available and liveness remains healthy while the database is down.
- **Missing driver/package:** activate `.venv` and run `python -m pip install -r requirements.txt`.
- **Port in use:** pass another port, e.g. `uvicorn app.main:app --reload --port 8001`.

The API still starts without a database connection, but readiness returns HTTP 503 until PostgreSQL is reachable. Keep production secrets in deployment environment variables and configure production CORS origins explicitly before deployment.
# Frontend integration (Phase 7D)

The React development server runs separately from FastAPI. Configure the optional frontend `VITE_API_BASE_URL` (default `http://127.0.0.1:8000/api/v1`) and keep FastAPI running with its configured CORS origins. The browser flow is project creation → PDF upload and indexing → generation request → backend retrieval and Ollama/Qwen generation → persisted resource/version → resource review and saved-resource listing. The browser never calls Ollama directly. See [`docs/backend/PHASE_7D_HANDOVER.md`](../docs/backend/PHASE_7D_HANDOVER.md) for limits and manual checks.
