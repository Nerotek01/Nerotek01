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

I am a Java developer who works where server internals, concurrency, and latency intersect. My specialty is the net.minecraft.server layer — packet interception, custom entity registration, TNT physics overrides, and low-level hooks that only make sense when you control the exact server version underneath them.

I treat performance as a design constraint, not a tuning phase. The systems I ship are built to hold thousands of concurrent players without dipping from 20 TPS, and to run for weeks without a restart. Async-first architecture, thread-isolated storage, and zero-allocation hot paths are the baseline, not the optimization.

On the side, I read exploits the way some people read documentation. Understanding how a system breaks is the only honest way to build one that does not.

---

### Architecture (Single-version, Async-first)

```mermaid
flowchart LR
  proxy["Proxy\nBungeeCord / Velocity"] --> entry["Spigot/Paper 1.8.8"]

  subgraph runtime["Spigot/Paper 1.8.8 Runtime"]
    mt["Main Thread\nTick loop (20 TPS)"]
    nms["NMS Layer\nPackets, Entities, Physics, Hooks"]
    mt --> nms
  end

  entry --> mt

  subgraph async["Async Pools"]
    io["Storage I/O"]
    net["Network / Replay I/O"]
    cache["Thread-isolated caches"]
  end

  mt -->|"enqueue"| io
  mt -->|"enqueue"| net
  mt -->|"enqueue"| cache

  io -->|"safe handoff"| mt
  net -->|"safe handoff"| mt
  cache -->|"safe handoff"| mt

  db[("MongoDB / SQL")]
  redis[("Redis")]

  io --> db
  cache --> redis
