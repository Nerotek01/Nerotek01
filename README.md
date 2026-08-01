# Nerotek01

> Java engineer building production-grade Minecraft infrastructure. Founder of Hypeland.

I am a Java developer focused on server-side Minecraft architecture, low-level NMS optimization, and systems that hold up under concurrent load. My work lives where clean code and fast code meet — performance is treated as a feature, not an afterthought.

---

## Focus

- **Java** as primary stack (Java 8 → 21), with deep work at the `net.minecraft.server` layer
- **Minecraft 1.8.8** (Spigot / Paper) — the version competitive networks are built on
- **Async-first architecture** — database I/O never touches the main thread
- **Exploit-aware engineering** — systems designed against the breakage patterns I know exist

I also work in Kotlin, Python, TypeScript, Go, Rust, C++, and SQL — each applied where it provides a real advantage.

---

## Selected Work

### BedWars

A monolithic BedWars plugin for Minecraft 1.8.8, engineered from the ground up for networks that cannot afford downtime. A single JAR ships 33+ integrated add-ons, a native ranked system with ELO and WebSocket matchmaking, a companion BedWarsProxy plugin for BungeeCord / Velocity, and a zero-allocation replay engine.

Battle-tested with **2,000+ concurrent players** at a stable **19.5+ TPS**. Instant map resets via SlimeWorldManager. Asynchronous MongoDB + Redis + SQLite storage layer with auto-fallback.

Live demo: `mc.hypeland.org`

### Hypeland

A production Minecraft network built as a reference deployment. The website is a Next.js + TypeScript SPA with strict CSP and dark mode. Every layer of the infrastructure — proxy, game servers, frontend — runs under direct control.

---

## Engineering Principles

- **Performance is a first-class feature.** Generators are batch-scheduled, listeners register only when their feature is enabled, scoreboards rebuild only on data change.
- **Stability over feature count.** Arenas use `ConcurrentHashMap` with explicit lifecycle cleanup; servers run for weeks without restart or memory leak.
- **Single-version depth over cross-version compromise.** Deep NMS hooks are impossible to maintain across versions — so each version gets its own optimized branch.

---

## Activity

- 130 contributions in the last year
- BedWars actively developed — 17 commits in 2 days, current release v2.5.3
- Public repositories: [BedWars](https://github.com/Nerotek01/BedWars), [Nerotek01](https://github.com/Nerotek01)

---

## Contact

- **GitHub:** [@Nerotek01](https://github.com/Nerotek01)
- **Website:** [hypeland.org](https://hypeland.org/)
- **Demo server:** `mc.hypeland.org`
