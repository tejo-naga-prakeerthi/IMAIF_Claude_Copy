# IMAIF project instructions

## Product requirements

IMAIF is a teacher-facing platform for creating educational projects from syllabi and generating resources personalized to Beginner, Intermediate, and Advanced learning levels. The planned product includes teacher login, project creation, syllabus upload, resource generation and review, whole-resource and section regeneration with feedback, a personal resource library, and student distribution.

The planned eight routes are `/login`, `/dashboard`, `/projects/new`, `/generate`, `/resources`, `/regenerate`, `/library`, and `/distribution`.

## Fixed technology choices

- Frontend: React, Vite, JavaScript, CSS, React Router.
- Planned backend: Python, FastAPI.
- Planned AI: Gemini API, LangChain, LangGraph.
- Planned RAG: syllabus parsing, chunking, embeddings, ChromaDB.
- Planned database: PostgreSQL and SQLAlchemy.
- Planned version control: Git and GitHub.
- Deployment is planned for Vercel and Render or a suitable alternative.

Do not replace these choices without discussing the reason with the project owner.

## Development rules

- Use JavaScript and functional React components; do not introduce TypeScript.
- Keep components modular, beginner-readable, and maintainable.
- Use React Router for client-side navigation and ordinary CSS for styling.
- Avoid unnecessary dependencies and do not add Tailwind, Bootstrap, or another CSS framework.
- A clearly labeled frontend-only demo login is allowed in Phase 2; do not represent it as real authentication or security.
- Do not add the backend until the frontend screens and their interactions are complete and the API needs are defined. Do not add Gemini/AI APIs or paid services until their later project phase explicitly calls for them.
- Never implement fake authentication or commit credentials. Use `.env.example` to document variable names; keep real `.env` files untracked.
- Keep each implementation phase within its stated scope and update `PHASE_TRACKER.md` with actual progress.
- Do not claim checks passed unless they were run and their results observed.

## Implementation order

1. Complete the frontend screens.
2. Implement and refine frontend interactions using sample data.
3. Integrate the backend after frontend needs are understood.
4. Build the AI and RAG system after backend contracts are established.

Phase 2 implements the demo login, dashboard and project creation flow. Phase 3 implements simulated generation and resource review. Phase 4 implements specific-component regeneration. Phase 5 implements the browser-local Resource Library and simulated student distribution. Reuse `ResourceContext` for saved resources and distribution records; keep these state objects JSON-serializable in browser local storage. The distribution learning level is stored separately from the saved resource's original level and does not rewrite its content.

Phase 6A is database, migration, and API-contract documentation. Phase 6B1 adds the FastAPI foundation, validated settings, PostgreSQL engine/session dependency, and health routes. Phase 6B2 adds only the seven approved SQLAlchemy entities, their constraints/relationships, and explicit Alembic migrations; it does not call `Base.metadata.create_all()`. Phase 6C1 implements project endpoints only. Teacher identity and ownership are unresolved, so do not invent fake authentication; clearly limit unscoped APIs to local development. Phase 6C2 implements resource/version APIs from the contracts. Keep the backend independent from React until frontend integration is explicitly in scope. Do not add authentication, AI, or RAG ahead of their agreed stage; AI/RAG remains Phase 7. Follow `PHASE_TRACKER.md` and do not start later-phase work early.
