# Antigravity Claw Skill

## Skill metadata

```yaml
name: antigravity-claw
version: 1.0.0
description: >
  Apply physics-based gravity to any webpage. Inspired by the Google Gravity easter egg,
  Python's `import antigravity` module (XKCD #353), and Google's Antigravity IDE.
  Fetches URLs, extracts DOM elements, runs a Rust 2D physics engine (Verlet integration),
  and renders interactive HTML animations with real collision detection.
entry: uv run python py/antigravity.py
requires:
  - python >= 3.10
  - uv
  - rust >= 1.75 (for building the engine)
env: []
```

---

## Commands

| Command | Description |
|---|---|
| `antigravity drop [URL]` | Apply gravity to any webpage → interactive HTML |
| `antigravity google` | Classic Google Gravity (built-in demo) |
| `antigravity fly` | The `import antigravity` easter egg in terminal |
| `antigravity watch [URL]` | Live terminal gravity animation |
| `antigravity export [URL]` | Export frames as JSON |
| `antigravity modes` | List all gravity modes |
| `antigravity info` | Show engine config |

---

## Gravity modes

| Mode | Effect |
|---|---|
| `down`  | Classic — everything falls to the floor |
| `up`    | Reverse gravity — elements float upward |
| `left`  | Elements slide off the left edge |
| `right` | Elements slide off the right edge |
| `zero`  | Weightlessness — gentle drift |
| `chaos` | Rotating + pulsing gravity (maximum fun) |

---

## Prompt examples

```
Apply gravity to Google
Make HackerNews fall down
Float all elements on https://example.com
Apply chaos gravity to Reddit
Show me the import antigravity easter egg
Watch Google fall in my terminal
Apply reverse gravity to Wikipedia
Export a gravity simulation of GitHub as JSON
```

---

## Architecture

```
Antigravity-claw/
├── src/               ← Rust 2D physics engine
│   ├── main.rs        ← CLI entry (clap)
│   ├── physics.rs     ← Verlet integration + AABB collisions
│   ├── scraper.rs     ← HTTP page fetcher + element extractor
│   ├── renderer.rs    ← Terminal + HTML renderer
│   └── types.rs       ← Shared structs
├── py/                ← Python layer
│   ├── antigravity.py ← Typer CLI + engine bridge
│   ├── scraper_py.py  ← BeautifulSoup scraper
│   └── openclaw_skill.py ← OpenClaw integration
├── SKILL.md
├── install.sh
├── Cargo.toml
└── pyproject.toml
```
