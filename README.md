<h1 align="center">Nerotek01</h1>
<p align="center"><em>Java engineer · Minecraft infrastructure · Founder of <a href="https://hypeland.org/">Hypeland</a></em></p>

<p align="center">
  <img src="https://img.shields.io/badge/Java-21-ED8B00?style=flat-square&logo=openjdk&logoColor=white" alt="Java"/>
  <img src="https://img.shields.io/badge/Focus-NMS%20%26%20Async-4A90D9?style=flat-square" alt="Focus"/>
  <img src="https://img.shields.io/badge/Target-1.8.8%20Spigot%20%2F%20Paper-7B68EE?style=flat-square" alt="Target"/>
  <img src="https://img.shields.io/badge/Status-Available%20for%20work-2EA44F?style=flat-square" alt="Status"/>
</p>

---

### About

I am a Java developer who works where server internals, concurrency, and latency intersect. My specialty is the `net.minecraft.server` layer — packet interception, custom entity registration, TNT physics overrides, and low-level hooks that only make sense when you control the exact server version underneath them.

I treat performance as a design constraint, not a tuning phase. The systems I ship are built to hold thousands of concurrent players without dipping from 20 TPS, and to run for weeks without a restart. Async-first architecture, thread-isolated storage, and zero-allocation hot paths are the baseline, not the optimization.

On the side, I read exploits the way some people read documentation. Understanding how a system breaks is the only honest way to build one that does not.

---

### Tech Stack

<p>
  <img src="https://img.shields.io/badge/Java-Expert-ED8B00?style=flat-square&logo=openjdk&logoColor=white"/>
  <img src="https://img.shields.io/badge/Kotlin-Advanced-7F52FF?style=flat-square&logo=kotlin&logoColor=white"/>
  <img src="https://img.shields.io/badge/Python-Advanced-3776AB?style=flat-square&logo=python&logoColor=white"/>
  <img src="https://img.shields.io/badge/TypeScript-Advanced-3178C6?style=flat-square&logo=typescript&logoColor=white"/>
  <img src="https://img.shields.io/badge/Go-Proficient-00ADD8?style=flat-square&logo=go&logoColor=white"/>
  <img src="https://img.shields.io/badge/Rust-Proficient-000000?style=flat-square&logo=rust&logoColor=white"/>
  <img src="https://img.shields.io/badge/C%2B%2B-Proficient-00599C?style=flat-square&logo=c%2B%2B&logoColor=white"/>
  <img src="https://img.shields.io/badge/SQL-Advanced-4479A1?style=flat-square&logo=postgresql&logoColor=white"/>
</p>

<p>
  <img src="https://img.shields.io/badge/Spigot%20%2F%20Paper-1.8.8-7B68EE?style=flat-square"/>
  <img src="https://img.shields.io/badge/BungeeCord-2DA67B?style=flat-square"/>
  <img src="https://img.shields.io/badge/Velocity-1B1B1B?style=flat-square"/>
  <img src="https://img.shields.io/badge/MongoDB-47A248?style=flat-square&logo=mongodb&logoColor=white"/>
  <img src="https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white"/>
  <img src="https://img.shields.io/badge/SQLite-003B57?style=flat-square&logo=sqlite&logoColor=white"/>
  <img src="https://img.shields.io/badge/Next.js-000000?style=flat-square&logo=next.js&logoColor=white"/>
  <img src="https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white"/>
</p>

---

### How I Work

| Principle | In practice |
|---|---|
| **Async by default** | Storage, network, and replay I/O run on dedicated pools — the main thread never waits. |
| **Single-version depth** | One Minecraft version means one test surface. NMS hooks stay precise; nothing is layered behind a compatibility shim. |
| **Exploit-aware design** | Listeners register only for active features. Collections use `ConcurrentHashMap` with explicit cleanup. Hot paths are allocation-free. |
| **Stability over scope** | A server should not need a restart for weeks. Memory leaks and TPS drift are treated as bugs, not background noise. |

---

### Notable Work

- **BedWars** — a production-grade plugin for 1.8.8 networks, battle-tested at 2,000+ concurrent players. See [Nerotek01/BedWars](https://github.com/Nerotek01/BedWars).
- **Hypeland** — my reference deployment, where every change is validated under real load before it ships anywhere else. Live at [hypeland.org](https://hypeland.org/) and `mc.hypeland.org`.

---

### GitHub Activity

<p align="center">
  <img src="https://github-readme-stats.vercel.app/api?username=Nerotek01&show_icons=true&hide_border=true&theme=dark&count_private=true" alt="Nerotek01 GitHub stats" width="48%"/>
  <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=Nerotek01&layout=compact&hide_border=true&theme=dark" alt="Top languages" width="48%"/>
</p>

---

### Contact

<p>
  <a href="https://github.com/Nerotek01"><img src="https://img.shields.io/badge/GitHub-Nerotek01-181717?style=flat-square&logo=github&logoColor=white"/></a>
  <a href="https://hypeland.org/"><img src="https://img.shields.io/badge/Web-hypeland.org-2EA44F?style=flat-square&logo=googlechrome&logoColor=white"/></a>
  <img src="https://img.shields.io/badge/Minecraft-mc.hypeland.org-7B68EE?style=flat-square&logo=minecraft&logoColor=white"/>
</p>
