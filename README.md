# Meltdown 🧪🔥
## Hey Troublemakers.. Got Web Containers? 

![meltdown](md.gif)

Tiny rogue lab of HTML+JS torture scenes for poking at browser‑hosted container / WebContainer performance (rendering, CPU, memory, event loop resilience) — and for having a little neon cyberpunk fun while you do it.

> I really, really enjoy WebContainers. It's kind of a miracle. Thought some of you other jokers might enjoy this.

![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg) ![Status: Experimental](https://img.shields.io/badge/Status-EXPERIMENTAL-orange) ![Made with Vanilla JS](https://img.shields.io/badge/Stack-Vanilla_JS-00cc88)

## ⚠️ Health & Hardware Warning
The `webcontainer-meltdown-test.html` page contains **rapid flashing, high‑contrast, high‑density animation**. It may trigger **photosensitive reactions** or make laptops spin fans like jet engines. Don't run it full screen near anyone who might be affected. Press `Esc` to emergency halt.

---

## Table of Contents
1. What Is This?
2. Included Test Pages
3. Quick Start
4. Test Categories & What They Stress
5. How To Measure Stuff
6. Customizing / Hacking
7. Safety Notes
8. Contributing
9. License

---

## 1. What Is This?
Two self‑contained HTML files you can open locally (or drop into a WebContainer platform like StackBlitz) to create **load patterns** that visually & programmatically stress parts of the runtime:

- Massive DOM churn
- Canvas / pixel noise generation
- Layout / paint storms (glitch layers, scanlines, matrix rain)
- JS allocation & CPU tight loops
- Simulated network burst (data URLs to stay offline)
- Simulated file operation flood (in‑memory objects)

The goal: quick gut‑check of responsiveness, frame rate stability, throttling, scheduling, and limit enforcement — without pulling in build tools or deps.

## 2. Included Test Pages

| File | Purpose | Open Risk |
|------|---------|-----------|
| `webcontainer-meltdown-test.md` (HTML inside) | Pure visual / GPU & animation chaos (fractal grid, glitch layers, matrix rain, rings, lightning, static noise, cursor FX) + FPS counter | High (flash + GPU load) |
| `webcontainers-test.md` (HTML inside) | Six button‑driven simulated resource tests (fork bomb, memory balloon, CPU burn, network flood, file churn, spawn storm) | Moderate |

> Both files are Markdown wrappers containing full HTML (for convenience / copyability). You can rename to `.html` or just open them if your viewer renders raw source.

## 3. Quick Start

Option A (fastest):
1. Grab the code inside one of the .md files provided and paste it in WC. 

Option B (local static server — helps with certain APIs):

You can just change the extensions to html and they should run in any browser that supports html and js... or you can stand up a lil server I guess? 

```bash
python3 -m http.server 8000
# then visit http://localhost:8000/meltdown.html
```

## 4. Test Categories & What They Stress

| Category | Mechanism | Signals To Watch |
|----------|-----------|------------------|
| Visual Chaos | Dozens of layered CSS animations + dynamic DOM insert/remove + canvas static | FPS drops, GPU time, repaint cost |
| Fork Bomb (simulated) | Exponential counter loop w/ interval doubling (capped) | Throttling, task scheduling fairness |
| Memory Balloon | Repeated 10MB array allocations then cleanup | JS heap growth, GC pauses |
| CPU Burn | Tight math loops inside `requestAnimationFrame` | Main thread blocking, input latency |
| Network Flood (simulated) | Repeated fetch of data URLs (Promise churn) | Concurrency limits, microtask queue behavior |
| File Chaos (simulated) | In‑memory object create/delete cycles | GC fragmentation, allocation rate |
| Spawn Storm (conceptual) | Sequenced increments (proxy for container spawn) | Burst handling, UI updates |

## 5. How To Measure Stuff

- Chrome DevTools > Performance: record 5s run during CPU burn.
- Performance panel FPS meter or `Rendering` tools (enable in DevTools Command Menu) for frame pacing.
- Memory tab: watch heap allocation during memory balloon; take snapshots before & after.
- Performance Insights (Chrome) for layout / paint cost spikes.
- Throttle CPU (e.g., 4× slowdown) to accentuate scheduling side effects.
- Observe input latency: move mouse during chaos; note lag or cursor jank.

## 6. Customizing / Hacking

Ideas:
- Lower visual density: reduce counts in `generateSquares`, `generateNeonRings`, `generateText` loops.
- Increase brutality: raise counts / shorten animation durations.
- Swap `data:text/plain` to a real endpoint if you actually want network stress (be nice — rate limits!).
- Add WebWorker versions of CPU burn to contrast main thread vs off‑thread cost.
- Wrap timing with `performance.mark/measure` for more precise profiling.

## 7. Safety Notes

- Press `Esc` in meltdown view to halt animations.
- Close the tab if your device fans or thermals spike uncomfortably.
- Do **not** run while screen‑sharing to sensitive audiences.
- Simulations are intentionally **non‑destructive** (no real fork bomb, no actual filesystem / network hammering). Modify responsibly if you change that.

## 8. Contributing

PRs welcome for:
- Additional controlled stress modules (e.g., OffscreenCanvas, WASM compute)
- Metrics overlays (long task detector, frame time histogram)
- Accessibility-safe test variants (reduced flashing)
- Docs improvements / translation

Please keep zero‑dependency philosophy unless a measurement aid is compelling.

## 9. License

MIT — Do what thou wilt. See `LICENSE` if/when added; the header here governs meanwhile.

---

Made with curiosity, caffeine, and appreciation for melting stuff. 