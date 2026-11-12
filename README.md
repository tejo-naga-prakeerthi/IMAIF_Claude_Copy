# IMAIF

IMAIF is a teacher-focused platform for generating personalized educational resources. The React + Vite frontend now connects project creation, PDF syllabus indexing, resource generation, persisted resource review, and saved-resource listing to the FastAPI backend. Generation runs through the backend's local retrieval and Ollama/Qwen path; the browser does not call the model directly. Login remains a demo and is not authentication. Component regeneration and student distribution remain browser-only demonstrations. The backend includes project/resource/distribution APIs and the Phase 7 syllabus indexing and generation path. Recipient management and real delivery remain deferred.

## Requirements

- Node.js 20.19+ or 22.12+
- npm (included with Node.js)

## Setup and run

```bash
npm install
npm run dev
```

Run the backend separately using the setup in [`backend/README.md`](./backend/README.md). The frontend API base defaults to `http://127.0.0.1:8000/api/v1`; set `VITE_API_BASE_URL` in a local `.env` file to override it. FastAPI permits the Vite development origins configured by the backend.

Vite prints the local development URL (normally `http://localhost:5173`). Stop the server with `Ctrl+C`.

To create a production build and serve it locally for preview:

```bash
npm run build
npm run preview
```

## Routes

| Route | Page |
| --- | --- |
| `/login` | Demo teacher sign-in; validates form fields locally only |
| `/dashboard` | Dashboard with backend projects and recent project links |
| `/projects/new` | Backend project creation and optional PDF syllabus upload/indexing |
| `/generate` | Backend retrieval and local-model resource generation |
| `/resources` | Persisted backend resource list, detail preview, and save-to-library action |
| `/regenerate` | Compare and accept/reject a sample replacement for one selected component |
| `/library` | Backend saved resources with title/type/level filters, preview, and browser TXT download |
| `/distribution` | Sample class and student selection, saved-resource selection, learning-level choice, review, and locally persisted simulated distribution records |

Unknown paths redirect to `/dashboard`; `/` redirects to `/login`.

## Project structure

Page components live in route-named folders under `src/pages`. Shared layout and placeholder components are in `src/components`; global responsive styles are in `src/styles`. Routing is defined centrally in `src/App.jsx`, while `src/main.jsx` sets up the browser router and application entry point.

See [PHASE_TRACKER.md](./PHASE_TRACKER.md) for implementation status and [AGENTS.md](./AGENTS.md) for project requirements and contributor rules. Phase 6A database and API design documents are in [`docs/backend/`](./docs/backend/): database schema, endpoint contracts, local-storage migration, and Phase 6B handover.

The connected generation path stores resources and versions through the backend. The older local `ResourceProvider` still supports the separate sample component-regeneration and distribution demonstrations. Library downloads are UTF-8 plain text `.txt` files created by the browser; no PDF exporter is installed. Distribution remains simulated and does not notify students or deliver assignments. Follow the ordered phase handovers in [PHASE_TRACKER.md](./PHASE_TRACKER.md).

## Phase 6A and 6B handover

Phase 6A documents the PostgreSQL schema, API contracts, and safe local-storage import plan. Phase 6C provides the project, resource/version, component revision, and distribution APIs. Phase 7 adds local syllabus ingestion, embeddings, ChromaDB retrieval, and local Ollama/Qwen resource generation. Phase 7D connects the browser project, upload, generation, review, and library flows to those APIs. Stage 1 is not complete until its end-to-end browser flow and remaining quality limitations are verified. PostgreSQL integration remains unverified. See the phase handovers in [`docs/backend/`](./docs/backend/) and [PHASE_TRACKER.md](./PHASE_TRACKER.md).
