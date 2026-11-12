# IMAIF phase tracker

## Git checkpoints

- Phase 1: `63efeaf` — `Complete Phase 1 - React project setup and routing`
- Phase 2: `f172849` — `Complete Phase 2 - Core frontend`
- Phase 3: `b8fa40f` — `Complete Phase 3 - Resource generation and review`
- Phase 4: `89a85d3` — `Complete Phase 4 - Component-level regeneration` (amended checkpoint)
- Phase 5: `1e8e50e` — `Complete Phase 5 - Resource library and student distribution`
- Phase 6A: `63863f7` — `Complete Phase 6A - Database design and API contracts`
- Phase 6B1: `9e2a4e6` — `Complete Phase 6B1 - FastAPI backend foundation`
- Phase 6B2: `e39275e` — `Complete Phase 6B2 - SQLAlchemy models and migrations`

## Phase 1 — Project setup and frontend routing

**Status: Complete**

- [x] Confirm Node.js and npm availability.
- [x] Create React + Vite JavaScript project.
- [x] Add React Router and configure the application entry point.
- [x] Create eight distinct route page components and shared layout/navigation.
- [x] Add global responsive CSS.
- [x] Add `.gitignore`, `.env.example`, `README.md`, and `AGENTS.md`.
- [x] Initialize Git if not already initialized.
- [x] Install dependencies and run the requested build and route checks.

Verification performed: `npm install react-router-dom` completed successfully with 0 reported vulnerabilities; `npm run build` completed successfully. The Vite dev server was opened in a browser and all eight route headings rendered as expected. Navigation from the dashboard to the project route worked. No automated test suite is configured in Phase 1.

Route pages are placeholders only; no feature design or backend behavior is included.

## Phase 2 — Core frontend

**Status: Complete**

- [x] Create demo teacher login with client-side validation and password visibility control.
- [x] Create dashboard with sample statistics, recent projects, and project creation actions.
- [x] Create project form for class details, objectives, PDF syllabus selection, learning level, and resource types.
- [x] Keep all eight routes and responsive shared navigation accessible.
- [x] Keep demo project records in browser local storage; do not upload syllabus files.
- [x] Verify login and project form validation, all routes and navigation, lint, and production build.
- [x] Add responsive breakpoints for desktop, tablet/narrow and mobile layouts.

The demo login provides no authentication or identity verification. Project sample records are stored in the current browser only. Selected syllabus files are not transmitted or stored. Five resource workflow routes remain placeholders.

Verification performed: `npm run lint` completed with no warnings; `npm run build` succeeded. Browser checks confirmed all eight route headings, sidebar navigation to project creation, empty/invalid/valid demo login behavior, password visibility toggle, required project field blocking, at-least-one resource validation, and successful project submission appearing in the dashboard sample list. The dashboard and project form were visually inspected at the available desktop viewport. Responsive CSS breakpoints are in place at 850px and 640px, but tablet/mobile visual checks were unavailable because the connected browser does not expose a viewport resizing control.

## Phase 3 — Generation and review UI

**Status: Complete**

- [x] Simulate resource generation from a selected project and show progress, success, and error states.
- [x] Show generated resources and provide type-specific previews for notes, presentations, quizzes, and worksheets.
- [x] Add accept and save interactions, saved-state visibility, and duplicate-save prevention.
- [x] Add feedback-driven whole-resource sample regeneration with a new version preview.
- [x] Persist sample resource and review state in browser local storage.
- [x] Verify all eight routes and navigation to generation from a project.
- [x] Verify simulated loading/progress and successful navigation into resource review.
- [x] Verify the notes, presentations, quizzes, and worksheets preview layouts.
- [x] Verify accept/save status, duplicate-save prevention, whole-resource regeneration, and updated preview.
- [x] Verify resource and accepted/saved state persists after browser refresh.
- [x] Run `npm run lint` and `npm run build`.
- [x] Add responsive styles for tablet/narrow and mobile breakpoints.
- [ ] Visually verify tablet and mobile viewports when a browser viewport control is available.

All generated text is static sample content. No AI service is called. Saved status is not the full Resource Library, which remains Phase 5. Slide/chapter/section regeneration remains Phase 4.

Verification performed: all eight route headings rendered in the browser; project creation linked to `/generate`; the sample generation progress appeared and completed; all four type-specific previews showed content; accept enabled save; saved state prevented duplicate saves and survived page reload; feedback-based whole-resource regeneration produced version 2, displayed the feedback, reset acceptance, and changed quiz question content. Browser console contained no errors on the checked Phase 3 app. `npm run lint` passed with no warnings and `npm run build` succeeded. Dashboard and review screens were visually inspected at desktop width. Tablet/mobile viewport visual QA could not be performed because the connected browser does not expose a viewport resizing control; responsive CSS is in place at 850px and 640px.

## Phase 4 — Specific regeneration

**Status: Complete**

- [x] Select an existing resource and list only its selectable components by type.
- [x] Collect feedback and prepare a different sample replacement for slides, questions, activities, and notes sections.
- [x] Keep the original until acceptance; support comparison, accept, and reject.
- [x] Update only the chosen component on acceptance, retain its previous version, and require whole-resource review again.
- [x] Persist pending and accepted component changes in browser local storage.
- [x] Verify all eight routes and resource/component selection for presentations, quizzes, worksheets, and notes.
- [x] Verify feedback validation, replacement preview, accept/reject, and that unselected components remain unchanged.
- [x] Verify pending replacement persistence after refresh and accepted version history.
- [x] Verify existing whole-resource regeneration still works.
- [x] Run `npm run lint` and `npm run build`.
- [x] Add responsive styling for desktop, tablet/narrow, and mobile breakpoints.
- [ ] Visually verify tablet and mobile viewports when a browser viewport control is available.

Verification performed: all eight routes rendered. Browser checks covered component selection and preview for all four resource types, required-feedback validation, simulated loading, original/replacement comparison, acceptance and rejection, unchanged unselected items, pending-candidate persistence across refresh, and component version history. The Phase 3 whole-resource regeneration flow was also exercised and remained functional. Browser console reported no errors. `npm run lint` completed without warnings and `npm run build` succeeded. Responsive CSS is in place, but tablet/mobile visual QA could not be performed because the connected browser does not expose viewport resizing controls.

No real AI is called. Specific regeneration uses locally defined alternatives and feedback text. Pending/accepted state is stored in browser local storage. Whole-resource regeneration remains available on `/resources`.

## Phase 5 — Resource library and student distribution

**Status: Implementation complete; interaction verification incomplete**

- [x] Show saved resources with subject, type, class, original learning level, save date, and revision count.
- [x] Add title search and clearable subject, type, and learning-level filters.
- [x] Preview saved resources, show component revision history, and open an individual resource in the review workspace.
- [x] Download current resource content and revision history as a browser-generated UTF-8 TXT file.
- [x] Confirm before deleting a saved resource and remove it from browser-local saved data.
- [x] Add sample Class 8A, 9A, and 10A classes with fictional individual/all student selection.
- [x] Require a saved library resource and at least one recipient; keep original resource level separate from selected distribution level.
- [x] Add review, edit, and simulated confirmation states for distribution.
- [x] Persist distribution records with ID, class, student IDs/names, resource ID/title/type, subject, original level, selected level, timestamp, and demo status.
- [x] Update README.md and AGENTS.md with the Phase 5 workflows and Phase 6 handover.
- [ ] Verify library filters, preview for all resource types, TXT download, deletion confirmation and persistence, distribution validation/confirmation/persistence, all routes, and previous workflows in the browser.
- [x] Run final `npm run lint` and `npm run build` after the last source changes.
- [ ] Visually check tablet/mobile layouts where browser tooling permits.

Implementation notes: Saved resources and distribution history are stored in `imaif.resources` and `imaif.distributions` local storage entries through `ResourceProvider`. Saving records `savedAt`; resources saved before this field existed display “Date not recorded.” The library offers a native browser confirmation before deleting. TXT downloads include the current resource content and retained component revisions. PDF export is not included. Distribution records are local demo records only; no student notifications, content adaptation, or actual delivery occurs.

Verification so far: the `/library` route rendered in Edge and showed the correct empty-library state; the generation route also rendered its available sample project and resource plan. Final `npm run lint` completed with no warnings and final `npm run build` succeeded. The UI automation could not reliably activate the generation controls, so saved-resource interactions, download, delete, distribution workflows, all-route browser smoke tests, and the previous-workflow regression checks remain unverified. Tablet/mobile visual checks also remain unverified. The local development server was stopped after checks.

## Phase 6 — Database design and backend integration

Keep Phase 6 split into design/contracts (6A) and backend implementation/integration (6B). Do not introduce AI/RAG work in either subphase.

### Phase 6A — Database design and API contracts

**Status: Complete**

- [x] Inspect project/provider/resource flows and verified local-storage keys.
- [x] Design PostgreSQL/SQLAlchemy-compatible relational entities and foreign keys.
- [x] Specify immutable whole-resource snapshots, component revision events, and append-only restore behavior.
- [x] Define REST contracts for project/resource/version/revision/distribution workflows and local import.
- [x] Document a safe, idempotent localStorage migration plan and source limitations.
- [x] Create Phase 6A handover and link documentation from README.
- [x] Validate JSON examples, endpoint count, foreign-key references, version/restore invariants, migration guarantees, and ensure no frontend/dependency changes.

Deliverables: `docs/backend/DATABASE_DESIGN.md`, `docs/backend/API_CONTRACTS.md`, `docs/backend/LOCAL_STORAGE_MIGRATION.md`, and `docs/backend/PHASE_6A_HANDOVER.md`. Validation parsed 30 fenced JSON examples and 65 inline API JSON objects; checked 22 endpoint sections for purpose/path/query/body/success/status/validation; checked referenced FK table names, version/distribution/migration invariants, and relative documentation links. Git diff inspection confirmed only documentation files changed; no frontend source, dependency, backend, or AI code was changed or added. Phase 6A is documentation only; no FastAPI or database code has been implemented.

### Phase 6B1 — FastAPI backend foundation

**Status: Complete**

- [x] Add the Python backend layout with FastAPI, Pydantic Settings, SQLAlchemy, a PostgreSQL driver, and Uvicorn.
- [x] Configure environment-backed settings and local Vite CORS origins without credentials.
- [x] Add SQLAlchemy engine, session factory, declarative base, and a cleanup-safe request dependency.
- [x] Add versioned liveness and database readiness health endpoints; do not create tables.
- [x] Document Windows PowerShell setup and update project handover instructions.
- [x] Keep React workflows independent and defer entities, migrations, CRUD, auth, and AI/RAG.

Verification performed: Python 3.14.4 was available. A backend virtual environment was created and all requirements installed successfully (FastAPI 0.162.0, Uvicorn 0.54.0, SQLAlchemy 2.1.6, psycopg 3.3.6, Pydantic Settings 2.16.2). `compileall` and app import succeeded; OpenAPI lists `/api/v1/health/live` and `/api/v1/health/ready`. With PostgreSQL unavailable, Uvicorn started successfully; liveness returned HTTP 200 with `{"status":"alive"}`, readiness returned HTTP 503 with a sanitized unavailable response, and Swagger `/docs` returned HTTP 200. A 3-second PostgreSQL connection timeout keeps the unavailable readiness response bounded. `npm run lint` and `npm run build` both succeeded. No PostgreSQL-connected readiness check was possible because no running database was available. No tables, entity models, migrations, CRUD APIs, React integration, or AI features were added. No frontend source or package files were changed.

### Phase 6B2 — SQLAlchemy models and Alembic migrations

**Status: Implementation complete; live PostgreSQL verification unavailable**

- [x] Add Alembic configuration using validated backend settings and `Base.metadata` for autogeneration.
- [x] Implement the seven Phase 6A entities with named constraints, PostgreSQL types, relationships, indexes, and `RESTRICT` delete behavior.
- [x] Preserve immutable resource snapshots, same-resource current/parent pointers, component revision links, and exact-version distribution references.
- [x] Add the initial migration and reversible downgrade operations; no application-startup table creation.
- [x] Add code-level model tests and Windows PowerShell migration/database instructions.
- [x] Keep CRUD APIs, React integration, authentication, local-storage import, and AI/RAG out of scope.

Verification performed: Alembic 1.20.1 and pytest 8.4.2 installed in the backend virtual environment. Model import and mapper configuration succeeded; all seven tables compile to PostgreSQL DDL. `pytest -q` passed 11 code-level tests. `alembic upgrade head --sql` generated PostgreSQL SQL for the seven application tables (plus Alembic's version table), 40 constraints, and 10 indexes; offline downgrade SQL generated seven table drops. Alembic reports `6b2_initial_schema` as the head. PostgreSQL and Docker were unavailable (`psql` and `docker` commands absent; localhost:5432 closed), so no live upgrade, schema inspection, constraint integration tests, or database `current` revision check was performed. Frontend files were not changed. This phase does not implement CRUD, API, auth, or AI features.

### Phase 6C1 — Project CRUD API

**Status: Complete; PostgreSQL integration unavailable**

- [x] Implement `POST`, `GET` list, `GET` detail, `PATCH`, and soft-archive `DELETE` on `/api/v1/projects`.
- [x] Validate project fields, reject unknown database fields, and support contract pagination, filters, and stable sorting.
- [x] Return active project detail with summaries of its active resources' current versions.
- [x] Use transactional writes, rollback on database errors, and sanitized 404/409/422/500 responses.
- [x] Preserve health routes; keep frontend integration, authentication, resource APIs, and AI/RAG out of scope.
- [x] Add mocked-session HTTP tests for CRUD, validation, missing IDs, filters, pagination, database failures, and liveness.

Verification performed: `compileall` succeeded and `pytest -q` passed 31 tests using mocked SQLAlchemy sessions and FastAPI's HTTP test client. These are isolated API tests, not PostgreSQL integration tests. PostgreSQL was unavailable (`psql`/Docker absent and port 5432 closed), so no migration application or live database behavior was verified. Liveness and readiness were both exercised with mocked database behavior. No frontend files changed. Teacher identity/ownership remains deliberately unimplemented; these unscoped routes are for a single local-development dataset and are not production multi-teacher access control.

### Phase 6C2A — Basic resource CRUD and saved-state APIs

**Status: Implementation complete; mocked API verification passed; PostgreSQL integration pending**

- [x] Add resource creation with an immutable initial version in one transaction.
- [x] Add filtered, paginated resource list and current-version detail endpoints.
- [x] Add soft archive and saved/unsaved library state endpoints.
- [x] Keep version, restore, and component-revision endpoints out of this subphase.
- [x] Add mocked HTTP tests for resource endpoint behavior.
- [x] Complete backend regression suite, OpenAPI verification, and diff checks.
- [ ] Verify against live PostgreSQL when available.

Implementation follows the Phase 6A contract. Saving changes only `resources.is_saved` and `saved_at`; it does not change the immutable version's `review_status`. The contract leaves acceptance enforcement conditional, so this endpoint does not introduce a separate acceptance workflow. Mocked project and resource API tests and the complete backend suite pass when run outside the Windows sandbox, which blocks the local socketpair used by Starlette TestClient. PostgreSQL integration remains pending.

### Phase 6C2B1 — Resource version creation on update

**Status: Implementation complete; mocked API/service verification passed; PostgreSQL integration pending**

- [x] Implement the existing `PATCH /api/v1/resources/{resource_id}` contract.
- [x] Require `expected_current_version_id`; lock the active resource row and return `409` for stale writes.
- [x] Merge partial changes into the current snapshot and validate the complete type-specific content.
- [x] Append a `metadata_update` snapshot, advance the current pointer, and clear saved state in one transaction.
- [x] Preserve all previous version rows and resource/project identity.
- [x] Add API/service coverage for success, snapshot history, invalid input, rollback, missing/archived resources, and stale writes.
- [x] Run focused, project regression, resource API, and full backend suites; run `git diff --check`.
- [ ] Verify against live PostgreSQL when available.

The contract already defined the PATCH route, request shape, `201` response, append-only snapshots, stale-version `409`, and saved-state reset, so no API contract change was needed. The update locks the active resource row, appends a complete `metadata_update` snapshot with the prior version as parent, advances the current pointer, and clears saved state in one transaction. Mocked tests do not verify database locking behavior against a live PostgreSQL server.

Verification performed: focused update tests passed (8); project API regression tests passed (20); resource API tests passed (23); full backend suite passed (54, 0 failures, 0 skips). Tests ran outside the Windows sandbox because it blocks the local socketpair required by Starlette TestClient. Python compile checks and OpenAPI route inspection succeeded; `git diff --check` passed. PostgreSQL integration remains unverified.

### Phase 6C2B2 — Resource version history retrieval

**Status: Implementation complete; mocked API verification passed; PostgreSQL integration pending**

- [x] Implement the contract's paginated, newest-first version history endpoint.
- [x] Implement the contract's full individual-version detail endpoint.
- [x] Scope every query to the requested active resource and return 404 for archived/missing resources or non-owned versions.
- [x] Compute `is_current` from the resource's current-version pointer without changing it.
- [x] Add tests for ordering, pagination, full snapshot response, missing/archived resources, wrong-resource version IDs, empty history, and read-only behavior.
- [x] Run the resource and project API tests, complete backend suite, compile check, OpenAPI inspection, and `git diff --check`.
- [ ] Verify against live PostgreSQL when available.

Verification performed: focused history tests passed (4); resource API tests passed (27); project API tests passed (20); full backend suite passed (58, 0 failures, 0 skips). Tests used mocked sessions and ran outside the Windows sandbox because it blocks the local socketpair required by Starlette TestClient. Compileall, OpenAPI route inspection, and `git diff --check` passed. No database schema change was needed. PostgreSQL integration remains unverified.

### Phase 6C2B3 — Resource version restoration

**Status: Implementation complete; mocked API verification passed; PostgreSQL integration pending**

- [x] Implement the contracted restore endpoint with expected-current-version checking and active-resource row locking.
- [x] Append a new sequential `restore` snapshot copied from the selected version; parent it to the previously current version.
- [x] Advance the resource pointer, timestamp and saved state atomically with the new version.
- [x] Add tests for restore behavior, immutable history, ownership, missing/archived targets, stale requests, and transaction failures.
- [x] Run focused restore tests, full backend suite, compile check, OpenAPI inspection, and `git diff --check`.
- [ ] Verify against live PostgreSQL when available.

Verification performed: focused restore tests passed (4); full backend suite passed (62, 0 failures, 0 skips); `compileall`, OpenAPI route inspection, and `git diff --check` passed. Tests used mocked sessions and ran outside the Windows sandbox because it blocks the local socketpair required by Starlette TestClient. Restoration never updates or deletes an existing version. PostgreSQL transaction and row-lock behavior remains unverified.

### Phase 6C2C1 — Component revision history retrieval

**Status: Implementation complete; mocked API verification passed; PostgreSQL integration pending**

- [x] Implement the contracted paginated `GET /api/v1/resources/{resource_id}/component-revisions` endpoint with optional `component_key` filtering.
- [x] Scope events to an active resource and return complete immutable revision event metadata.
- [x] Order deterministically by descending revision number and ID; validate pagination and component keys.
- [x] Add tests for filtering, ownership, missing/archived resources, empty results, pagination, deterministic ties, validation, and read-only behavior.
- [x] Run focused component history tests, full backend suite, compile check, OpenAPI inspection, and `git diff --check`.
- [ ] Verify against live PostgreSQL when available.

Verification performed: focused component history tests passed (2); full backend suite passed (64, 0 failures, 0 skips); `compileall`, OpenAPI inspection, and `git diff --check` passed. Tests used mocked sessions and ran outside the Windows sandbox because it blocks the local socketpair required by Starlette TestClient. The schema has no component entity or current-revision pointer, and the contract defines no `is_current` field. A component key with no revision events returns an empty paginated list. PostgreSQL integration remains unverified.

### Phase 6C2C2 — Component revision restoration

**Status: Implementation complete; mocked API verification passed; PostgreSQL integration pending**

- [x] Implement the contracted `POST /api/v1/resources/{resource_id}/component-revisions/{revision_id}/restore` endpoint with `expected_current_version_id` and `target_state` validation.
- [x] Restore the selected event's before/after component into a copied current snapshot, preserving other components.
- [x] Append a new `restore` resource version and component revision event with sequential numbering, correct before/after links, and `restores_revision_id`.
- [x] Lock the resource row and atomically write the version, event, pointer, timestamp, and cleared saved state.
- [x] Add tests for both target states, missing/foreign/archived resources and revisions, missing component, stale writes, immutable history, and rollback failures.
- [x] Run focused tests, full backend suite, compile check, OpenAPI inspection, and `git diff --check`.
- [ ] Verify transaction and row-lock behavior against live PostgreSQL when available.

Verification performed: focused component restoration tests passed (8); full backend suite passed (72, 0 failures, 0 skips); `compileall`, OpenAPI inspection, and `git diff --check` passed. Tests used mocked sessions. PostgreSQL integration and live locking/transaction behavior remain unverified. At that checkpoint, Phase 6C3 and Phase 6C4 were unimplemented.

### Phase 6C3A — Distribution creation APIs

**Status: Implementation complete; mocked API verification passed; PostgreSQL integration pending**

- [x] Implement the contracted `POST /api/v1/distributions` endpoint for a saved current resource version and one or more recipients.
- [x] Return the exact version metadata, distribution learning level, `prepared_demo` status, `native` resolution, and created recipient snapshots.
- [x] Validate request fields, recipient names/references, duplicate non-null recipient references, active resource/version, and saved-current state.
- [x] Create the distribution and recipients atomically; roll back on database write failures.
- [x] Document the route and limitations; leave recipient management, distribution reads, and real delivery outside Phase 6C3A scope.
- [x] Run focused tests, complete backend suite, compile check, OpenAPI inspection, and `git diff --check`.
- [ ] Verify database constraints and transaction behavior against live PostgreSQL when available.

Verification performed at the Phase 6C3A checkpoint: focused distribution tests passed (21); full backend suite passed (93, 0 failures, 0 skips); `compileall`, OpenAPI inspection, and `git diff --check` passed. Tests use mocked sessions. PostgreSQL integration and live transaction behavior remain unverified. At that checkpoint, recipient management, distribution listing/retrieval, and real delivery had not been implemented; listing/retrieval is implemented by the following Phase 6C3B entry.

### Phase 6C3B — Distribution retrieval and listing APIs

**Status: Implementation complete; mocked API verification passed; PostgreSQL integration pending**

- [x] Implement the contracted `GET /api/v1/distributions` list with pagination, exact filters, inclusive timezone-aware date bounds, and fixed `created_at DESC, id DESC` ordering.
- [x] Implement `GET /api/v1/distributions/{distribution_id}` using the exact referenced resource version and persisted recipient snapshots.
- [x] Keep retrieval read-only, include historical distributions even when the referenced resource is archived, and avoid N+1 queries.
- [x] Add tests for response structures, recipient snapshots/counts, pagination, filters, dates, sort validation, archived history, missing IDs, and sanitized read failures.
- [x] Run focused tests, complete backend suite, compile check, OpenAPI inspection, and `git diff --check`.
- [ ] Verify the SQL queries against live PostgreSQL when available.

Verification performed: distribution creation/retrieval API tests passed (43); full backend suite passed (115, 0 failures, 0 skips); `compileall`, OpenAPI inspection, and `git diff --check` passed. No database schema change was made. PostgreSQL integration remains unverified; API tests use mocked sessions. Distribution creation remains in Phase 6C3A; recipient management, delivery, and Phase 6C3C remain unimplemented.

## Phase 7 — AI and RAG system

After backend integration and review, implement syllabus parsing, chunking, embeddings, ChromaDB retrieval, and the Gemini/LangChain/LangGraph multi-agent workflow. Keep credentials in environment variables and never commit secrets.

### Phase 7A — AI/RAG architecture and API contract design

**Status: Design complete; implementation not started**

- [x] Define the ₹0-cost MVP direction: local/open-source LLM and embeddings by default; Gemini is optional and may incur charges.
- [x] Define PDF-only syllabus ingestion (20 MiB maximum), temporary processing, no OCR, chunk metadata/version identity, and local ChromaDB retrieval filtered by project and syllabus version (initial target top-k 5).
- [x] Define the minimal LangGraph flow: project requirements → retrieval → generation → deterministic validation → persistence or clear error; no separate planner LLM or automatic repair loop.
- [x] Propose syllabus-upload and project-generation APIs without changing `API_CONTRACTS.md` or implementing routes.
- [x] Document provider abstraction, immutable resource/version persistence, fake-provider testing, and current authentication/ownership limitation.
- [x] Record implementation choices that remain open, including model selection, index lifecycle, insufficient-context behavior, provenance, and endpoint details.

Design record: [`docs/backend/PHASE_7A_DESIGN.md`](docs/backend/PHASE_7A_DESIGN.md). At the 7A checkpoint no application code, API contract, dependency, database schema, or migration was changed and no packages were installed.

### Phase 7B1 — PDF upload, validation, and text extraction

**Status: Implementation complete; mocked API verification passed**

- [x] Implement `POST /api/v1/projects/{project_id}/syllabus` using multipart PDF upload and the existing active-project lookup.
- [x] Enforce PDF signature/parsing validation, non-empty upload, 20 MiB maximum, and clear errors for malformed, password-protected, and no-text PDFs.
- [x] Extract and normalize text page by page using `pypdf`; keep page-numbered text request-local and return metadata only.
- [x] Use temporary FastAPI upload spooling and close the upload stream; do not persist the PDF or extracted text or change the database schema.
- [x] Add focused API/service tests; run the full backend suite, compile check, OpenAPI inspection, and `git diff --check`.
- [x] Document endpoint behavior and limitations in [`docs/backend/PHASE_7B1_HANDOVER.md`](docs/backend/PHASE_7B1_HANDOVER.md).

Verification performed: focused Phase 7B1 tests passed (13); full backend suite passed (128, 0 failures, 0 skips); `compileall`, OpenAPI inspection, and `git diff --check` passed. Tests use mocked database sessions; PostgreSQL integration remains unverified. Added only `pypdf` and `python-multipart`; no paid/AI packages were installed. No schema/API-contract/migration change was made. At the 7B1 checkpoint, OCR, persistence, indexing, chunking, embeddings, RAG, generation, and frontend integration remained out of scope; the next checkpoint was Phase 7B2.

### Phase 7B2 — Syllabus text chunking

**Status: Implementation complete; deterministic chunking tests passed**

- [x] Add a dependency-free deterministic chunker that consumes the Phase 7B1 page-aware extraction result without duplicating PDF parsing.
- [x] Use an explicit default target of 500 approximate lexical tokens, 75-token overlap, and a 50-token boundary lookback; prefer paragraph and sentence boundaries where practical.
- [x] Preserve project ID, deterministic temporary ingestion identity, filename, page range, null section metadata when unavailable, zero-based chunk index, text, and SHA-256 checksum.
- [x] Keep chunks in memory only; do not expose them from the upload API, persist them, or add schema, embedding, or ChromaDB changes.
- [x] Add focused tests for target/overlap, boundaries, long and short content, metadata, checksums, page ranges, no lexical text loss, and repeatability.
- [x] Document the strategy and limitations in [`docs/backend/PHASE_7B2_HANDOVER.md`](docs/backend/PHASE_7B2_HANDOVER.md).

Verification performed: focused chunking tests passed (9); full backend suite passed (137, 0 failures, 0 skips); `compileall` and `git diff --check` passed. Chunking tests require no PostgreSQL, ChromaDB, embeddings, Gemini, or external API. PostgreSQL integration remains unverified. Next checkpoint: Phase 7B3 — embeddings and ChromaDB.

### Phase 7B3 — Embeddings and ChromaDB vector storage

**Status: Implementation complete; local model and vector store tests passed**

- [x] Implement local, ₹0-cost embedding provider using `all-MiniLM-L6-v2` via ONNX runtime (384 dimensions).
- [x] Implement test seam with deterministic `FakeEmbeddingProvider` for fast, isolated test execution.
- [x] Implement project-isolated ChromaDB storage with collection naming `project_{project_id.hex}`.
- [x] Store verbatim chunk text and complete Phase 7B2 metadata (`project_id`, `ingestion_id`, `original_filename`, `chunk_index`, `checksum`, `approximate_token_count`, `page_start`, `page_end`).
- [x] Filter None metadata values to maintain strict ChromaDB non-null metadata constraints.
- [x] Implement stable deterministic chunk IDs (`{ingestion_id}_{chunk_index}`) and idempotent `upsert` indexing.
- [x] Support ingestion filtering and deletion within project collections.
- [x] Add focused tests for embedding generation, vector dimensionality, Chroma storage, project isolation, deduplication, and end-to-end chunking-to-indexing pipeline.
- [x] Document implementation, model rationale, and next steps in [`docs/backend/PHASE_7B3_HANDOVER.md`](docs/backend/PHASE_7B3_HANDOVER.md).

Verification performed: focused embedding and vector store tests passed (19); full backend suite passed (156 passed, 0 failures, 0 skips); `compileall` passed. Real `all-MiniLM-L6-v2` ONNX model was executed locally during tests. ChromaDB was exercised in memory and persistent modes. PostgreSQL integration remains unverified. At the 7B3 checkpoint, the next planned checkpoint was Phase 7B4 — syllabus retrieval.

### Phase 7B4 — Syllabus retrieval

**Status: Implementation complete; local Chroma retrieval tests passed**

- [x] Add a low-level similarity query to the existing `ChromaVectorStore` and a typed syllabus retrieval service.
- [x] Embed teacher queries using the same provider configured for indexing; default `top_k` to 5.
- [x] Enforce project collection and metadata isolation, with optional `ingestion_id` filtering.
- [x] Return ranked chunk IDs, exact text, stored metadata, one-based rank, and unmodified Chroma distance; missing/empty results return an empty tuple.
- [x] Validate blank queries and invalid top-k values without adding a relevance threshold or public endpoint.
- [x] Add focused Chroma-backed tests for ranking, top-k, filtering/isolation, empty results, validation, metadata/distance, and non-mutation.
- [x] Document service behavior and limitations in [`docs/backend/PHASE_7B4_HANDOVER.md`](docs/backend/PHASE_7B4_HANDOVER.md).

Verification performed: focused retrieval tests passed (12); Phase 7B3 embedding/vector-store regressions passed (19); full backend suite passed (168, 0 failures, 0 skips); `compileall`, FastAPI application import, and service import checks passed. Chroma retrieval tests use ephemeral storage and fake embeddings. Chroma emitted existing Pydantic `model_fields` deprecation warnings during tests. PostgreSQL integration remains unverified. No API, database, frontend, or LLM-generation work is included.

### Phase 7C — LLM provider and generation boundary design

**Status: Design proposal recorded; implementation not started**

- [x] Inspect existing project/resource schemas, immutable version persistence, API contracts, frontend sample generation, and Phase 7B retrieval types.
- [x] Propose a provider-independent service boundary, typed project/retrieval inputs, structured draft output, grounding/prompt rules, bounded provider configuration/failures, and fake-provider test strategy.
- [x] Split the work into 7C1 provider types/interface, 7C2 local provider adapter/settings, and 7C3 grounded single-resource generation service.
- [x] Record that no approved generation API exists and that the existing upload route does not yet chain extraction into chunking, embedding, and Chroma indexing.
- [x] Record open choices for local model/runtime, component IDs, ingestion identity selection, insufficient-context behavior, and future API/persistence semantics in [`docs/backend/PHASE_7C_DESIGN.md`](docs/backend/PHASE_7C_DESIGN.md).

This is documentation only. No production implementation, dependency, API contract, frontend code, database schema, or migration was changed. The earlier Phase 7A design document remains untouched. Resolve the ingestion/indexing and model/runtime decisions before integrating 7C3. Phase 7D workflow/validation and later persistence/API work have not started.

### Phase 7C1 — Generation types and provider interface

**Status: Implementation complete; provider-independent tests passed**

- [x] Add typed project/resource/retrieval generation input and provider request/result schemas for the existing four resource types.
- [x] Add the service-level `LLMProvider` protocol and typed provider failure classes without a concrete model/provider.
- [x] Add a deterministic fake provider for isolated tests; it is not selected for production use.
- [x] Preserve the Phase 7B4 retrieval fields in a generation-side type without importing ChromaDB into the provider boundary.
- [x] Decide that the future 7C3 application layer assigns component IDs after parsing provider content; providers return only content fields.
- [x] Add focused tests and document 7C1 scope and open 7C2 choices in [`docs/backend/PHASE_7C1_HANDOVER.md`](docs/backend/PHASE_7C1_HANDOVER.md).
- [ ] Select and test a concrete local model/runtime in Phase 7C2.

Verification performed at the 7C1 checkpoint: focused Phase 7C1 tests passed (19); full backend suite passed (187, 0 failures, 0 skips); `compileall`, FastAPI/provider imports, provider import isolation from ChromaDB, and `git diff --check` passed. The full suite emitted 161 existing ChromaDB/Pydantic deprecation warnings. This phase added no dependencies, API route, database or persistence changes, frontend integration, or model calls. No PostgreSQL integration is involved.

### Phase 7C2 — Local Ollama provider

**Status: Implementation complete; mocked provider verification passed; live model smoke test pending runtime installation**

- [x] Inspect the Python 3.11 environment and confirm no local LLM runtime/model was already installed.
- [x] Implement one local-only Ollama adapter behind the Phase 7C1 provider protocol, using standard-library HTTP and structured Pydantic JSON Schema output.
- [x] Select `qwen2.5:1.5b` as the default small local model; add bounded local URL, timeout, context, and output settings without provider-selection complexity.
- [x] Add syllabus-grounded prompt formatting, context overflow rejection without truncation, typed failure mapping, and secret-safe errors.
- [x] Add mocked tests for provider startup/request, all resource types, response parsing/errors, timeout/unavailable behavior, context limits, configuration, and prompt contents.
- [x] Document model installation, settings, manual smoke test, limitations, and verification in [`docs/backend/PHASE_7C2_HANDOVER.md`](docs/backend/PHASE_7C2_HANDOVER.md).
- [ ] Install Ollama and manually verify real local inference when the project owner is ready.

Verification performed at the 7C2 checkpoint: focused provider tests passed (41); full backend suite passed (209, 0 failures, 0 skips); `compileall`, FastAPI/provider imports, provider import isolation from ChromaDB, and `git diff --check` passed. The full suite emitted 161 existing ChromaDB/Pydantic deprecation warnings. No Python dependencies, API, frontend, persistence, schema/migration, or live-model integration were added at that checkpoint. PostgreSQL integration remains unverified.

### Phase 7C3 — Grounded single-resource generation service

**Status: Implementation complete; mocked tests passed; local Qwen structure smoke test passed with grounding limitation observed**

- [x] Add provider-independent `GenerationService` consuming validated project/resource input and supplied retrieval context; do not perform retrieval inside the service.
- [x] Build labeled grounding/project/context/output prompt sections with chunk IDs, page range, rank, source metadata, and verbatim text; omit raw Chroma distance.
- [x] Reject empty retrieval before provider calls and preserve provider insufficient-context outcomes as a typed generation error.
- [x] Validate provider result shape/type, assign deterministic type-specific component IDs, and validate the non-persisted draft with existing `ResourceCreate` rules.
- [x] Support Notes, Presentations, Quizzes, and Worksheets with Beginner, Intermediate, and Advanced learning-level instructions.
- [x] Test with the deterministic fake provider; keep live Ollama outside automated tests.
- [x] Document service behavior, manual use, limitations, and remaining end-to-end work in [`docs/backend/PHASE_7C3_HANDOVER.md`](docs/backend/PHASE_7C3_HANDOVER.md).
- [x] Resolve the upload-to-indexing and initial generation API/persistence gaps in Phases 7C4 and 7C5.
- [ ] Complete frontend generation/review integration and resolve or explicitly accept the semantic-grounding limitation before claiming end-to-end Stage 1 generation.

Verification performed: focused Phase 7C3 tests passed (12); Phase 7B4 retrieval tests passed (12); Phase 7B3 embedding/vector-store tests passed (19); focused 7C1/7C2 tests passed (42); full backend suite passed (222, 0 failures, 0 skips); compile/import checks and `git diff --check` passed. The full suite emitted 161 existing ChromaDB/Pydantic deprecation warnings. Manual local `qwen2.5:1.5b` calls returned valid `ResourceCreate` drafts but added unsupported examples on two smoke prompts. No automatic semantic validator/retry was added. No endpoint, frontend, persistence, or database schema change was made. PostgreSQL integration remains unverified.

### Phase 7C4 — Upload-to-index integration

**Status: Complete**

- [x] Connect the existing project syllabus upload route to the existing PDF extraction, deterministic chunking, embedding, and Chroma indexing components through a small service.
- [x] Reuse the deterministic Phase 7B2 ingestion ID and Phase 7B3 project-specific collections, metadata, stable chunk IDs, and idempotent upsert behavior.
- [x] Extend successful upload metadata with `ingestion_id`, `chunk_count`, and `indexing_status`; continue withholding PDF bytes and extracted/chunk text from the HTTP response and PostgreSQL.
- [x] Return a typed API error when chunking or indexing fails; clean up a newly-created partial ingestion when supported without deleting a preexisting identical ingestion.
- [x] Prove upload → extraction → chunking → fake embedding → ephemeral Chroma storage → retrieval with an integration-style API test, including project isolation and repeated-upload idempotency.
- [x] Document the indexing flow and remaining Stage 1 work in [`docs/backend/PHASE_7C4_HANDOVER.md`](docs/backend/PHASE_7C4_HANDOVER.md).

Verification performed: syllabus upload/index API tests passed (15); Phase 7B4 retrieval regressions passed (12); Phase 7B3 embedding/vector-store regressions passed (19); full backend suite passed (224, 0 failures, 0 skips); `compileall`, application/OpenAPI/service import inspection, and `git diff --check` passed. Tests use mocked project sessions, ephemeral Chroma, and fake embeddings; Chroma emitted existing Pydantic `model_fields` deprecation warnings. PostgreSQL integration remains unverified. This phase adds no generation route, frontend integration, database schema, or Stage 1 completion claim.

### Phase 7C5 — Persisted single-resource generation API

**Status: Complete; deterministic integration tests passed; live Qwen check remains manual**

- [x] Add `POST /api/v1/projects/{project_id}/generate` with validated resource type and learning level, optional existing syllabus `ingestion_id`, and optional existing generation instructions.
- [x] Orchestrate active project validation → existing project-scoped syllabus retrieval → existing `GenerationService`/configured local provider → existing `ResourceCreate` validation → existing `create_resource` transaction.
- [x] Return the existing resource response with version 1/current pointer; preserve `ready` review status and unsaved state.
- [x] Map no-context, provider, generated-output, and persistence errors through the existing API error envelope.
- [x] Add deterministic API tests for all resource types and an indexed-context-to-persisted-resource integration-style test.
- [x] Update the API contract and add [`docs/backend/PHASE_7C5_HANDOVER.md`](docs/backend/PHASE_7C5_HANDOVER.md).

Verification performed: focused 7C5 API tests passed (15); syllabus upload API tests passed (15); retrieval tests passed (12); generation service tests passed (12); resource API tests passed (41); complete backend suite passed (239, 0 failures, 0 skips); compile/import/OpenAPI and `git diff --check` passed. Tests use fake providers, mocked SQLAlchemy sessions, ephemeral Chroma, and fake embeddings. The full suite reported 322 existing ChromaDB/Pydantic deprecation warnings. No live Ollama call or PostgreSQL integration test was run in this phase.

Stage 1 remains incomplete. The frontend generation/review path and teacher authentication/ownership are not implemented, and the known Qwen grounding limitation remains. PostgreSQL integration remains unverified.

### Phase 7D — Frontend integration

**Status: Implementation and local frontend checks complete; live Qwen browser flow requires manual verification**

- [x] Add a centralized frontend API client for the existing FastAPI project, syllabus, generation, resource, and saved-state endpoints.
- [x] Connect the existing project form and dashboard to persisted backend projects.
- [x] Connect optional PDF upload to syllabus extraction/indexing and show only API-confirmed filename/page/chunk/index status.
- [x] Replace sample generation in the `/generate` workflow with the existing FastAPI generation endpoint and display the actual persisted resource response.
- [x] Connect `/resources` and `/library` to persisted resources and existing saved-state behavior.
- [x] Document local frontend/backend setup, the browser workflow, and preserved demo-only areas in [`docs/backend/PHASE_7D_HANDOVER.md`](docs/backend/PHASE_7D_HANDOVER.md).
- [ ] Manually verify project → PDF indexing → generation → persisted resource display with FastAPI, Chroma, and Ollama/Qwen running.

Automated frontend verification is limited to the existing lint/build scripts; `package.json` defines no frontend test suite. The live model browser flow and PostgreSQL integration are unverified. Stage 1 remains incomplete, and the known Qwen grounding limitation remains. Login, component regeneration, and distribution remain demo-only.


## Phase 8 — Validation and evaluation

Validate generated content and structure, compare Beginner/Intermediate/Advanced outputs, test full and component regeneration, and document quality, relevance, and failure cases.

## Phase 9 — Deployment

Configure environment variables and CORS, deploy the frontend and backend, configure persistent data storage, and verify end-to-end flows on the deployed application.
