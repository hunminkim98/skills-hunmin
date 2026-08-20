# Never move

If a path matches this list, do not nominate it. Do not score it as 1 or 2 in order to sneak it into `garbage/`.

## Always leave

- `.git/` and git metadata
- `node_modules/`, package lockfiles, virtualenvs, `.venv/`
- Secrets and env files (`.env`, credentials, keys, `*.pem`)
- Live product source (`src/`, `frontend/src/`, `backend/` application code, tests that the suite actually runs)
- Project contracts: `AGENTS.md`, `CLAUDE.md`, `SKILL.md`, `package.json`, `pyproject.toml`, `render.yaml`
- Published docs the README links, unless the user named a draft to quarantine
- `llm-wiki/` notes (that is wiki-for-llm)
- Anything already under `garbage/` (do not re-quarantine)

## Usually leave

- Checked-in fixtures and `demo/` assets that a script or README still names
- Design files that are the current brand
- Migration files, even if old

## Not an output

An untracked `.ts` / `.py` file in a source tree is unfinished work, not a render. Leave it. Offer to mention it in chat. Do not move it.

## Secrets

If a nominee looks like a secret, stop. Do not copy it into `garbage/`. Say so in chat. Leave the file where it is unless the user takes over.
