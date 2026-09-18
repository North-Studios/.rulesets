# Common Project Structure

This document defines the default structure for projects in this workspace. Use the
smallest structure that fits the project. Do not create empty directories only to
match a template, and do not move an existing project only to make it look like a
different template.

## General rules

- Keep the repository root for project metadata, documentation, source directories,
	tests, deployment configuration, and small static assets.
- Use `README.md` for purpose, setup, development, testing, deployment, and required
	environment variables. Put detailed product or API documentation in `docs/`.
- Keep secrets in environment variables or an ignored `.env` file. Commit a safe
	`.env.example` when configuration is needed.
- Keep generated and local-only content out of source control: `node_modules/`,
	`.venv/`, `__pycache__/`, `dist/`, `build/`, `out/`, coverage output, logs,
	local databases, unpacked installers, and IDE folders.
- Use one clear entry point per runnable target. Name it consistently (`src/main.*`,
	`src/index.*`, `server/index.*`, or the framework's conventional entry point).
- Put tests near the code when they are component-specific, or in a root `tests/`
	directory for integration and end-to-end tests. Test data belongs in
	`tests/fixtures/` or a clearly named project data directory.
- Keep runtime data separate from source code. Use `data/` only for checked-in
	content or an explicitly documented local data store; use `logs/` for runtime logs.

## Default npm project

Use this structure for a normal JavaScript or TypeScript library, CLI, extension,
or frontend application.

```text
project/
|-- package.json
|-- package-lock.json              # or the repository's chosen lockfile
|-- tsconfig.json                  # TypeScript projects
|-- README.md
|-- .env.example                   # only when environment variables are used
|-- src/
|   |-- main.ts                    # application entry point
|   |-- components/                # reusable UI or domain components
|   |-- features/                  # feature-owned code, when useful
|   |-- lib/                       # shared framework-independent helpers
|   |-- types/                     # shared types, when they are substantial
|   `-- assets/                    # source assets imported by code
|-- public/                        # files served or copied unchanged
|-- tests/                         # unit, integration, or end-to-end tests
|-- docs/                          # project-specific documentation
`-- scripts/                       # maintenance or build scripts
```

Rules for npm projects:

- Keep `src/` as the source of truth. Do not edit `dist/`, `out/`, or bundled files.
- Keep package scripts small and explicit: normally `dev`, `build`, `start`,
	`test`, `lint`, and `check`/`typecheck` as applicable.
- Use the framework's established directories. For Vite apps, `src/`, `public/`,
	`index.html`, and `vite.config.*` belong at the app root. For VS Code extensions,
	`src/` compiles to `out/` and extension contributions stay in `package.json`.
- A frontend-only app should not gain a server directory unless it actually owns a
	server or API.

## Default API project

Use this structure for an API-only service or a full-stack application that serves
an API. The example uses a TypeScript/Express naming style; equivalent Python,
Go, Rust, or framework conventions are valid.

```text
project/
|-- package.json or pyproject.toml
|-- README.md
|-- .env.example
|-- config/                         # environment/config loading and validation
|-- server/                         # backend application
|   |-- index.ts                    # process/bootstrap entry point
|   |-- routes/                     # route registration and HTTP handlers
|   |-- middleware/                 # auth, validation, errors, logging
|   |-- services/                   # application use cases and integrations
|   |-- db/                         # connection, schema, migrations, repositories
|   |-- validators/                 # request/response validation, when needed
|   `-- vite.ts                     # only for a Vite-served full-stack app
|-- shared/                         # contracts/types used by client and server
|-- client/                         # frontend source, only for full-stack apps
|   |-- index.html
|   `-- src/
|-- public/                         # static files for the client/server
|-- migrations/                     # only when not owned by server/db/
|-- tests/
|   |-- unit/
|   |-- integration/
|   `-- fixtures/
|-- docs/
`-- scripts/
```

API rules:

- Keep HTTP concerns in routes/controllers and business logic in services. Do not
	put database queries, authentication policy, and response formatting in one large
	entry-point file.
- Validate input at the boundary and return consistent JSON error shapes. Keep
	health/readiness endpoints separate from authenticated business routes.
- Keep database schema and migrations versioned. Never commit production secrets or
	a local runtime database unless the project explicitly treats it as fixture data.
- In a full-stack app, keep `client/`, `server/`, and `shared/` clearly separated.
	A frontend catch-all must be registered after API routes.
- For a Python API, substitute `app/` or the framework's conventional package for
	`server/`, and keep `tests/` and dependency metadata at the project root.

## Default other projects

### Python application, bot, or script

```text
project/
|-- pyproject.toml                # preferred; requirements.txt is also valid
|-- README.md
|-- .env.example
|-- src/
|   `-- package_name/
|       |-- __init__.py
|       |-- __main__.py           # optional command entry point
|       |-- config.py
|       |-- services/
|       `-- utils/
|-- tests/
|-- data/                         # checked-in fixtures or documented local data
|-- logs/                         # runtime output; normally ignored
`-- scripts/
```

Small bots and one-file tools may keep `bot.py`, `app.py`, or another entry script
at the root. As they grow, move reusable logic into a package and leave the root
file as a thin bootstrap. Prefer `pyproject.toml`; use `requirements.txt` when the
deployment platform or existing project requires it.

### Monorepo or product with multiple targets

```text
product/
|-- README.md
|-- docs/
|-- shared/                       # contracts or shared libraries, if any
|-- web/ or <Product>-Web-Client/
|-- api/ or <Product>-Server-Side/
|-- desktop/ or <Product>-Win-App/
|-- mobile/                       # when applicable
|-- tools/                        # development/release tools
`-- scripts/                      # orchestration and CI helpers
```

Each child application is independently recognizable and keeps its own manifest,
source, tests, and build configuration. Release artifacts and unpacked application
directories belong under ignored build/release output, not beside source files.

### Desktop, extension, and systems projects

- Desktop apps keep platform-specific code under a named target directory and share
	reusable code in `src/` or `shared/`.
- VS Code extensions use `package.json` for activation events and contributions,
	`src/` for TypeScript, `out/` for compiled output, and `README.md` for usage.
- Rust projects use `Cargo.toml`, `src/main.rs` or `src/lib.rs`, and `tests/` for
	integration tests. Keep `target/` generated and ignored.
- Installer and release metadata belongs in `release/`, `packaging/`, or the
	platform's established directory. Do not mix generated installers with source.

### Games and content-heavy projects

Keep engine/runtime code, content, and save or build output distinct:

```text
project/
|-- src/ or game/                 # runtime code
|-- assets/                       # source art, audio, data
|-- scripts/                      # tooling or content scripts
|-- tests/                        # automated tests, when supported
|-- saves/ or data/               # documented local or shipped data
`-- build/                        # generated output; normally ignored
```

Use the engine's required layout when it conflicts with this generic shape. The
engine convention is more important than this document.

## Choosing a structure

1. Identify the runnable target and its entry point.
2. Choose the smallest matching template above.
3. Add `server/`, `client/`, `shared/`, `db/`, or `tests/` only when the project has
	 a real responsibility for that directory.
4. Preserve the framework or engine convention when a project already has one.
5. Keep generated output and release snapshots outside the source structure.
