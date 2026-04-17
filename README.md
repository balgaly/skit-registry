# skit-registry

Community registry for [skit](https://github.com/balgaly/skit) — a cross-platform package manager for AI agent skills.

This repo hosts a single `index.json` file that powers `skit`'s **Browse Registry** TUI screen. Entries point to GitHub repos that contain agent skills (`SKILL.md` files, slash commands, rule files, etc.).

## Adding your skill

Open an issue using the [Add repo](https://github.com/balgaly/skit-registry/issues/new?template=add-repo.md) template. Include:

- **URL** — your GitHub repo (must be `https://github.com/<user>/<repo>`)
- **Description** — one line, what your skill does
- **Tags** — comma-separated keywords (e.g. `testing`, `productivity`)
- **Agents** — which agents it supports (`claude-code`, `cursor`, `windsurf`)

Requirements:

- Repo must contain at least one `SKILL.md` at the root or in a subdirectory
- Repo must be public
- No abandoned / archived repos

## Schema

```json
{
  "version": 1,
  "updated": "YYYY-MM-DD",
  "entries": [
    {
      "name": "skill-name",
      "description": "One-line description",
      "url": "https://github.com/user/repo",
      "tags": ["tag1", "tag2"],
      "author": "github-username",
      "agents": ["claude-code", "cursor", "windsurf"]
    }
  ]
}
```

Fields `name`, `description`, `url`, `author` are required. `tags` and `agents` default to empty arrays when omitted.

## How `skit` consumes this

- `skit` fetches `https://raw.githubusercontent.com/balgaly/skit-registry/main/index.json`
- Response is cached locally for 1 hour
- URLs are validated: only `https://github.com/` hostnames pass
- ANSI escape codes are stripped from strings for safety

## License

The registry index is public domain (CC0). Individual skill repos retain their own licenses — check before installing.
