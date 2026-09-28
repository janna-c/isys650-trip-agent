# Repository agent instructions

## Commits

Use Scoped Commits, with a subject of at most 100 characters:

```text
<scope>: <description>
```

Pick the narrowest stable behavior or subsystem as the scope (for example, `trip-agent` or `deployment`), not a Conventional Commit prefix such as `feat`, `fix`, or `chore`. Use a body only when needed to explain why; do not add `Co-Authored-By` trailers.

Before committing, inspect `git status` and the diff. Stage only files for the requested change, run `git diff --cached --check`, and leave unrelated work untouched. Push only when asked. Report the commit hash and verification results.

## Checks

Run `uv run --no-project python -m unittest discover -s tests` before pushing. A push to `main` runs CI and deploys to 10server.net; do not commit credentials or expose the server's OpenRouter key.
