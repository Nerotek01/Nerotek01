text
<h1 align="center">Nerotek01</h1>

<p align="center">
  <em>Java engineer · Minecraft infrastructure · Founder of <a href="https://hypeland.org/">Hypeland</a></em>
</p>

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

### Architecture (Single-version, Async-first)

```mermaid
flowchart LR
  Clients["Players\nMinecraft Client 1.8.8"]
  Staff["Staff\nModeration Client"]
  Web["Web / Panel\nhypeland.org"]

  Proxy["Proxy Layer\nBungeeCord / Velocity"]
  API["Backend API\nREST / WebSocket"]

  subgraph CONTROL["Control Plane (routing, identity, rules)"]
    direction TB
    Auth["Auth & Sessions\nlogin, tokens, ip rules"]
    Perms["Permissions\nranks, groups"]
    Match["Matchmaker\nqueue, party, routing"]
    Config["Config Service\nfeature flags, runtime toggles"]
    Punish["Punishments\nban, mute, blacklist"]
    Audit["Audit Stream\nsecurity events"]
  end

  subgraph GAME["Game Plane (Spigot/Paper 1.8.8)"]
    direction TB

    subgraph LOBBY["Lobby Servers"]
      direction LR
      LobbyNetty["Netty I/O\npacket ingress/egress"]
      LobbyMain["Main Thread\n20 TPS tick"]
      LobbyPlugins["Gameplay\nhub features, cosmetics"]
      LobbyNMS["NMS Hooks\npackets, entities, physics"]

      LobbyMain --> LobbyPlugins --> LobbyNMS
      LobbyNetty --> LobbyNMS
    end

    subgraph SHARDS["Game Shards (e.g., BedWars)"]
      direction LR
      ShardNetty["Netty I/O\npacket ingress/egress"]
      ShardMain["Main Thread\n20 TPS tick"]
      ShardLogic["Game Logic\nmatches, teams, scoring"]
      ShardNMS["NMS Hooks\ncombat, kb, TNT, packets"]

      ShardMain --> ShardLogic --> ShardNMS
      ShardNetty --> ShardNMS
    end
  end

  subgraph SECURITY["Exploit-aware Layer (hot-path safe)"]
    direction TB
    PacketFilters["Packet Filters\nsanity checks, rate limits"]
    Signals["Anti-cheat Signals\nheuristics, flags"]
  end

  subgraph ASYNC["Async Layer (off-main thread)"]
    direction TB
    Pools["Executors\nfixed pools, CF pipelines"]
    Storage["Storage Services\nDAOs, repositories"]
    Messaging["Messaging\nfanout, pubsub"]
    Replay["Replay / Match Audit I/O\nstream writer"]

    Pools --> Storage
    Pools --> Messaging
    Pools --> Replay
  end

  subgraph DATA["Data Plane"]
    direction TB
    Redis[(Redis\ncache, pubsub, locks)]
    DB[(MongoDB / SQL\nprofiles, stats, economy)]
    SWM[(SlimeWorldManager\nworld templates, blobs)]
    Files[(File Store\nreplays, exports)]
  end

  subgraph OBS["Observability"]
    direction TB
    Metrics["Metrics\nTPS, latency, pool saturation"]
    Logs["Logs\nstructured, rotation"]
    Alerts["Alerts\nthresholds, paging"]
  end

  Clients --> Proxy
  Staff --> Proxy
  Web --> API

  API --> Auth
  API --> Perms
  API --> Match
  API --> Config
  API --> Punish
  API --> Audit

  Proxy --> Match
  Match --> Proxy
  Proxy --> Auth

  Proxy --> LobbyMain
  Proxy --> ShardMain

  LobbyNMS --> PacketFilters
  ShardNMS --> PacketFilters
  PacketFilters --> Signals
  Signals --> Punish

  LobbyMain -->|"enqueue"| Pools
  ShardMain -->|"enqueue"| Pools

  Storage --> Redis
  Storage --> DB
  Storage --> SWM
  Messaging --> Redis
  Replay --> Files

  Storage -->|"safe callback"| LobbyMain
  Storage -->|"safe callback"| ShardMain
  Replay -->|"safe callback"| ShardMain

  LobbyMain --> Metrics
  ShardMain --> Metrics
  Pools --> Metrics

  API --> Logs
  LobbyMain --> Logs
  ShardMain --> Logs

  Metrics --> Alerts
```

---

### Tech Stack

**Languages**

<p>
  <img src="https://img.shields.io/badge/Java-Expert-ED8B00?style=flat-square&logo=openjdk&logoColor=white"/>
  <img src="https://img.shields.io/badge/Kotlin-Advanced-7F52FF?style=flat-square&logo=kotlin&logoColor=white"/>
  <img src="https://img.shields.io/badge/Python-Advanced-3776AB?style=flat-square&logo=python&logoColor=white"/>
  <img src="https://img.shields.io/badge/TypeScript-Advanced-3178C6?style=flat-square&logo=typescript&logoColor=white"/>
  <img src="https://img.shields.io/badge/JavaScript-Advanced-F7DF1E?style=flat-square&logo=javascript&logoColor=black"/>
  <img src="https://img.shields.io/badge/Go-Proficient-00ADD8?style=flat-square&logo=go&logoColor=white"/>
  <img src="https://img.shields.io/badge/Rust-Proficient-000000?style=flat-square&logo=rust&logoColor=white"/>
  <img src="https://img.shields.io/badge/C%2B%2B-Proficient-00599C?style=flat-square&logo=c%2B%2B&logoColor=white"/>
  <img src="https://img.shields.io/badge/C-Proficient-A8B9CC?style=flat-square&logo=c&logoColor=black"/>
  <img src="https://img.shields.io/badge/C%23-Proficient-239120?style=flat-square&logo=csharp&logoColor=white"/>
  <img src="https://img.shields.io/badge/PHP-Proficient-777BB4?style=flat-square&logo=php&logoColor=white"/>
  <img src="https://img.shields.io/badge/Shell-Advanced-4EAA25?style=flat-square&logo=gnubash&logoColor=white"/>
  <img src="https://img.shields.io/badge/SQL-Advanced-4479A1?style=flat-square&logo=postgresql&logoColor=white"/>
</p>

**Minecraft Ecosystem**

<p>
  <img src="https://img.shields.io/badge/Spigot%20%2F%20Paper-1.8.8-7B68EE?style=flat-square"/>
  <img src="https://img.shields.io/badge/BungeeCord-2DA67B?style=flat-square"/>
  <img src="https://img.shields.io/badge/Velocity-1B1B1B?style=flat-square"/>
  <img src="https://img.shields.io/badge/NMS%20Hooks-181717?style=flat-square"/>
  <img src="https://img.shields.io/badge/SlimeWorldManager-6D4AFF?style=flat-square"/>
  <img src="https://img.shields.io/badge/PlaceholderAPI-2EA44F?style=flat-square"/>
  <img src="https://img.shields.io/badge/Citizens-7B68EE?style=flat-square"/>
  <img src="https://img.shields.io/badge/Packet%20Interception-181717?style=flat-square"/>
</p>

**Databases & Caching**

<p>
  <img src="https://img.shields.io/badge/MongoDB-Expert-47A248?style=flat-square&logo=mongodb&logoColor=white"/>
  <img src="https://img.shields.io/badge/Redis-Expert-DC382D?style=flat-square&logo=redis&logoColor=white"/>
  <img src="https://img.shields.io/badge/SQLite-Expert-003B57?style=flat-square&logo=sqlite&logoColor=white"/>
  <img src="https://img.shields.io/badge/MySQL-Advanced-4479A1?style=flat-square&logo=mysql&logoColor=white"/>
  <img src="https://img.shields.io/badge/PostgreSQL-Advanced-4169E1?style=flat-square&logo=postgresql&logoColor=white"/>
  <img src="https://img.shields.io/badge/MariaDB-Advanced-003545?style=flat-square&logo=mariadb&logoColor=white"/>
  <img src="https://img.shields.io/badge/Cassandra-Proficient-1287B1?style=flat-square&logo=apachecassandra&logoColor=white"/>
</p>

**Backend, Frontend & DevOps**

<p>
  <img src="https://img.shields.io/badge/Node.js-Advanced-339933?style=flat-square&logo=nodedotjs&logoColor=white"/>
  <img src="https://img.shields.io/badge/Next.js-Advanced-000000?style=flat-square&logo=next.js&logoColor=white"/>
  <img src="https://img.shields.io/badge/React-Advanced-61DAFB?style=flat-square&logo=react&logoColor=black"/>
  <img src="https://img.shields.io/badge/TailwindCSS-Advanced-06B6D4?style=flat-square&logo=tailwindcss&logoColor=white"/>
  <img src="https://img.shields.io/badge/Docker-Proficient-2496ED?style=flat-square&logo=docker&logoColor=white"/>
  <img src="https://img.shields.io/badge/Linux-Advanced-FCC624?style=flat-square&logo=linux&logoColor=black"/>
  <img src="https://img.shields.io/badge/Git-Expert-F05032?style=flat-square&logo=git&logoColor=white"/>
  <img src="https://img.shields.io/badge/Maven-Advanced-C71A36?style=flat-square&logo=apachemaven&logoColor=white"/>
  <img src="https://img.shields.io/badge/Gradle-Advanced-02303A?style=flat-square&logo=gradle&logoColor=white"/>
  <img src="https://img.shields.io/badge/WebSocket-Advanced-4A90D9?style=flat-square"/>
  <img src="https://img.shields.io/badge/REST%20API-Advanced-2EA44F?style=flat-square"/>
</p>

---

### How I Work

| Principle | In practice |
|---|---|
| Async by default | Storage, network, and replay I/O run on dedicated pools — the main thread never waits. |
| Single-version depth | One Minecraft version means one test surface. NMS hooks stay precise; nothing is layered behind a compatibility shim. |
| Exploit-aware design | Listeners register only for active features. Collections use `ConcurrentHashMap` with explicit cleanup. Hot paths are allocation-free. |
| Stability over scope | A server should not need a restart for weeks. Memory leaks and TPS drift are treated as bugs, not background noise. |

---

### Notable Work

- **BedWars** — a production-grade plugin for 1.8.8 networks, battle-tested at 2,000+ concurrent players. See [Nerotek01/BedWars](https://github.com/Nerotek01/BedWars).
- **Hypeland** — my reference deployment, where every change is validated under real load before it ships anywhere else. Live at [hypeland.org](https://hypeland.org/) and `mc.hypeland.org`.

---

### Contact

<p>
  <a href="https://github.com/Nerotek01">
    <img src="https://img.shields.io/badge/GitHub-Nerotek01-181717?style=flat-square&logo=github&logoColor=white"/>
  </a>
  <a href="https://hypeland.org/">
    <img src="https://img.shields.io/badge/Web-hypeland.org-2EA44F?style=flat-square&logo=googlechrome&logoColor=white"/>
  </a>
  <img src="https://img.shields.io/badge/Minecraft-mc.hypeland.org-7B68EE?style=flat-square&logo=minecraft&logoColor=white"/>
</p>
