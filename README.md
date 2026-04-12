# Plexi App Registry

The official registry of apps for [Plexi](https://github.com/ianjamesburke/PLEXI) — a keyboard-driven terminal multiplexer with a built-in app platform.

`registry.json` is the single source of truth. Kona (Plexi's app installer) reads this file to discover, search, and install apps directly from within the terminal.

## Schema

Each entry in `registry.json` follows this shape:

```json
{
  "id": "app-id",
  "name": "Display Name",
  "description": "One sentence description.",
  "version": "1.0.0",
  "author": "github-username",
  "repo": "github-username/repo-name",
  "path": "path/to/app/in/repo",
  "tags": ["tag1", "tag2"]
}
```

| Field | Required | Description |
|---|---|---|
| `id` | Yes | Unique kebab-case identifier. Used as the install directory name. |
| `name` | Yes | Human-readable display name shown in Kona's browser. |
| `description` | Yes | One sentence. Shown in search results and the app detail view. |
| `version` | Yes | Semver string matching the version in the app's `manifest.toml`. |
| `author` | Yes | GitHub username of the app's author. |
| `repo` | Yes | GitHub repo shorthand (`owner/repo`) where the app lives. |
| `path` | Yes | Subdirectory within `repo` containing `manifest.toml` and the entry point. |
| `tags` | Yes | Array of lowercase tag strings for filtering. |

Kona constructs download URLs as:

```
https://raw.githubusercontent.com/{repo}/alpha/{path}/
```

Files fetched: `manifest.toml` and whatever entry point is declared inside it.

## Submitting an App

1. Fork this repo.
2. Add your entry to `registry.json` — one JSON object in the array, following the schema above.
3. Make sure your app's repo is public and the `path` directory contains a valid `manifest.toml`.
4. Open a pull request. Include a link to the app's source so it can be reviewed.

Apps must be open source, functional, and not harmful. The maintainer reserves the right to reject or remove entries at any time.

## Tags

Common tags in use:

| Tag | Use for |
|---|---|
| `productivity` | Tools that help you get work done |
| `git` | Git / version control tools |
| `system` | System monitoring and management |
| `network` | Networking and connectivity tools |
| `reference` | Information lookup and reading |
| `files` | File system navigation and management |
| `utility` | General-purpose utilities |
| `creative` | Art, music, and generative tools |
| `ai` | AI-powered apps |
| `game` | Games |
| `toy` | Playful, ambient, or non-goal-oriented |
| `simulation` | Simulations |
| `ambient` | Passive / background apps |
| `code` | Coding and development tools |
| `music` | Music and audio |
