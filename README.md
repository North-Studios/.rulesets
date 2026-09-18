# Common Rulesets

---

## 1. Document Structure

### 1.1 Required Sections (in order)

1. **Title** — `# Project Name` (with emoji optionally, e.g. `# 📡 DownDetect`)
2. **One-line description** — what the project is, in one sentence
3. **Features** — bullet list of key capabilities
4. **Tech Stack** — languages, frameworks, databases
5. **Prerequisites** — Node/Python versions, external services
6. **Installation** — dependency install + env setup
7. **Configuration** — environment variables table
8. **Running** — dev + production commands
9. **API Reference** — endpoints (if applicable)
10. **Project Structure** — directory tree (if applicable)
11. **Troubleshooting** — common issues (optional)
12. **License** (optional)

### 1.2 Heading Conventions

- Use `##` for top-level sections, `###` for subsections
- Section titles are **Title Case** or **Sentence case** — be consistent within a file
- Emojis are permitted in section headings but must be consistent (either all or none)
- Do **not** skip heading levels (no `##` → `####`)

---

## 2. Formatting Rules

### 2.1 Code Blocks

- Always specify the language: ` ```bash `, ` ```env `, ` ```json `, ` ```ini `, ` ```text `
- Use `bash` for shell commands (even on Windows — note Windows variants inline)
- Use `env` or `ini` for environment variable examples
- Use `text` for directory trees and plain output

### 2.2 Tables

- Use tables for: environment variables, API endpoints, scripts, configuration options
- **Always** include a header row with column names
- Align columns with pipes; padding is optional but must be consistent
- Example:

```markdown
| Variable | Description | Default |
| -------- | ----------- | ------- |
| `PORT`   | HTTP port   | `3000`  |
```

### 2.3 Inline Code

- Wrap all of the following in backticks:
  - File names: `app.py`, `package.json`
  - Directory names: `data/`, `client/`
  - Variable names: `API_KEY`, `VITE_API_ORIGIN`
  - Commands: `npm run dev`
  - Values: `true`, `5001`, `stable`

### 2.4 Lists

- Use `-` (hyphen) for unordered lists, not `*` or `+`
- Use `1.` for ordered lists (steps must be sequential)
- End list items with periods only if they are full sentences
- Nested lists: indent by 2 spaces

### 2.5 Emphasis

- **Bold** for critical warnings, required fields, key terms on first use
- *Italic* sparingly — prefer bold
- Do not use ALL CAPS for emphasis

---

## 3. Content Rules

### 3.1 Title & Description

- Title = project name exactly as it appears in code
- Description = one sentence, no period needed if it's a fragment
- Include the **purpose** (what problem it solves), not just the category

### 3.2 Features Section

- Bullet list, each item starts with a **bold keyword** followed by `—` (em dash) and explanation
- Group related features under `###` subsections if more than ~8 items
- Example:

```markdown
- **File storage** — Upload single or multiple files, organize in folders
- **Sharing** — Share files and folders with other users
```

### 3.3 Environment Variables

- **Always** provide a table with: `Variable`, `Purpose`/`Description`, `Default`
- Mark required variables explicitly (e.g. "Required for production")
- Group related variables (e.g. all `SMTP_*` together)
- Use `.env.example` as the source of truth — README must match it
- Document the difference between build-time (`VITE_*`) and runtime variables

### 3.4 Installation / Quick Start

- Start with prerequisites (runtime versions)
- Use `cp .env.example .env` (note Windows `copy` variant inline)
- Provide a **minimal** quick start that works without external services (mock mode)
- Then a **production** section with real services

### 3.5 Commands / Scripts

- Provide a table with `Command` and `Description` columns
- Show the most common commands first (`dev`, `build`, `start`)
- Note any commands that require the server to be running

### 3.6 API Documentation

- Group endpoints by resource (Auth, Users, Tasks, etc.)
- Use a table with `Method`, `Path`, `Description` columns
- Note authentication requirements per group (e.g. `X-API-Key`, `JWT`)
- Include request/response examples for non-obvious endpoints
- Document status codes when non-standard

### 3.7 Project Structure

- Use a `text` code block with a tree
- Only show top 2–3 levels of depth
- Annotate key files/directories with `#` comments
- Keep it consistent with the actual repo layout

### 3.8 Troubleshooting

- Format as numbered list or `###` subsections
- Symptom first, then cause, then fix
- Include the most common issues (auth, CORS, database path, env not loaded)

---

## 4. Language & Tone

- **English** for all READMEs (even if UI supports other languages)
- **Second person** ("you can", "set the variable") or **imperative** ("set the variable") — be consistent
- **Present tense** for descriptions ("The server returns…")
- **Active voice** over passive
- No marketing fluff — describe what it does, not how great it is
- Use "for example" and "that is" sparingly; prefer "e.g." and "i.e."
- Use em dashes (`—`) for parenthetical explanations, not hyphens

---

## 5. Consistency Rules Across READMEs

### 5.1 Terminology

| Use this | Not this |
| -------- | -------- |
| `environment variables` | `env vars` (in prose) |
| `API key` | `apikey`, `api-key` |
| `sign-in` / `sign in` | `login` (as verb), `log-in` |
| `README` | `readme`, `Readme` |
| `PostgreSQL` | `Postgres`, `postgres` (in prose) |
| `SQLite` | `sqlite`, `Sqlite` |
| `OAuth 2.1` | `OAuth2.1`, `oauth 2.1` |
| `X-API-Key` | `X-API-KEY`, `x-api-key` |

### 5.2 Code Block Conventions

- Bash commands: no `$` prefix (easier to copy)
- Comments in code blocks: `#` for bash/env, `//` for JS/TS
- Long commands: use `\` for line continuation in bash
- Windows alternatives: note with `# Windows` comment

### 5.3 URL & Path Conventions

- Use `http://localhost:PORT` format for local URLs
- Use `https://` for production examples
- Trailing slashes: omit in base URLs, include in paths where meaningful
- File paths: use forward slashes even on Windows in docs

### 5.4 Version References

- Node.js: `Node.js 20+` (not `node 20`, `Node 20.x`)
- Python: `Python 3.11+` (not `python3`, `Python3`)
- npm: `npm 10+`

---

## 6. Maintenance Rules

- README must be updated in the same PR as code changes that affect:
  - Environment variables (add/remove/rename)
  - API endpoints (add/remove/change)
  - Scripts in `package.json` / `Makefile`
  - Prerequisites (runtime version bumps)
  - Project structure (new top-level directories)
- `.env.example` is the source of truth for env vars — README must match
- Remove references to deprecated features in the same release they are removed
- Do not document internal/private APIs in public READMEs

---

## 7. Per-Project README Checklist

Before merging a README, verify:

- [ ] Title matches project name in `package.json` / `pyproject.toml` / `config.py`
- [ ] One-line description explains purpose
- [ ] Features list is accurate and current
- [ ] Prerequisites list exact runtime versions
- [ ] Install steps work from a clean checkout
- [ ] `.env.example` exists and matches env table in README
- [ ] Dev and production run commands are both documented
- [ ] All scripts in `package.json` / `Makefile` are documented or intentionally omitted
- [ ] API tables cover all public endpoints
- [ ] Project structure matches actual top-level layout
- [ ] Troubleshooting covers the 3 most common issues
- [ ] No broken links, no placeholder text (`TODO`, `TBD`, `XXX`)
- [ ] Code blocks have language tags
- [ ] Tables are well-formed (header + separator + rows)
- [ ] Consistent terminology per §5.1

---

## 8. Exceptions

- **Monorepo sub-READMEs** (e.g. `QuantumToDo-Win-App`, `QuantumToDo-Web-Client`, `QuantumToDo-Server-Side`) may reference each other by name instead of repeating shared setup. The parent README should link to them.
- **Internal-only services** may omit the "Quick Start (mock)" section if no mock mode exists.
- **Libraries** (no runnable service) replace "Running" with "Usage" and show code examples instead of shell commands.
- **Frontend-only projects** may omit the "Database" section but must still document `API_BASE_URL` / `VITE_API_ORIGIN`.
