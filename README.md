<h1 align="center">Nerotek01</h1>

<p align="center">
  <em>Java Engineer · High-Performance Minecraft Infrastructure · Minestom & Microservices</em>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Java-25-ED8B00?style=flat-square&logo=openjdk&logoColor=white" alt="Java"/>
  <img src="https://img.shields.io/badge/Focus-Minestom%20%26%20Microservices-4A90D9?style=flat-square" alt="Focus"/>
  <img src="https://img.shields.io/badge/Architecture-Distributed%20Systems-7B68EE?style=flat-square" alt="Architecture"/>
  <img src="https://img.shields.io/badge/Status-Available%20for%20work-2EA44F?style=flat-square" alt="Status"/>
</p>

---

### About

I am a Java engineer specializing in high-performance Minecraft server infrastructure. My focus lies at the intersection of **Minestom**, **microservices architecture**, and **distributed systems** — designing server backends that scale horizontally, communicate asynchronously, and maintain sub-millisecond tick budgets under load.

I approach infrastructure as an engineering discipline, not a configuration exercise. Every system I build is architected around **service isolation**, **state consistency across nodes**, and **resilient inter-service communication** via Redis pub/sub and message queues. The goal is not merely to run a server — it is to build a network that behaves predictably when thousands of players, dozens of game shards, and multiple backend services interact simultaneously.

I read protocol implementations and concurrency internals the way some engineers read framework documentation. Understanding where a system breaks — and why — is the foundation of building one that does not.

---

### System Overview

<table>
<tr>
<td width="50%">

**Service Mesh & Communication**
Distributed service topology built on Redis pub/sub and message queues. Each service (matchmaking, economy, party, replay) runs as an isolated unit with its own lifecycle. Inter-service communication is asynchronous by default, with explicit contracts and fallback strategies.

</td>
<td width="50%">

**Game Server Layer**
Minestom-based game shards running Java 25 with virtual threads. No Spigot compatibility layer — direct control over packet handling, entity ticking, and instance management. Each shard maintains consistent TPS while offloading all I/O to dedicated async executors.

</td>
</tr>
<tr>
<td width="50%">

**State & Persistence**
MongoDB for player profiles, stats, and economy data. Redis for caching, distributed locks, and cross-service event streams. All storage access is non-blocking, with MongoDB connection pooling and Redis pipeline batching to minimize round-trips.

</td>
<td width="50%">

**Infrastructure & Orchestration**
Dockerized service deployment with compose-based orchestration. Each microservice is containerized and independently scalable. Health checks, graceful shutdowns, and rolling updates are part of the deployment contract — not afterthoughts.

</td>
</tr>
</table>

---

### Tech Stack

**Languages**

<p>
  <img src="https://img.shields.io/badge/Java-Expert-ED8B00?style=flat-square&logo=openjdk&logoColor=white"/>
  <img src="https://img.shields.io/badge/Kotlin-Advanced-7F52FF?style=flat-square&logo=kotlin&logoColor=white"/>
  <img src="https://img.shields.io/badge/Python-Advanced-3776AB?style=flat-square&logo=python&logoColor=white"/>
  <img src="https://img.shields.io/badge/TypeScript-Advanced-3178C6?style=flat-square&logo=typescript&logoColor=white"/>
  <img src="https://img.shields.io/badge/Go-Proficient-00ADD8?style=flat-square&logo=go&logoColor=white"/>
  <img src="https://img.shields.io/badge/Rust-Proficient-000000?style=flat-square&logo=rust&logoColor=white"/>
</p>

**Minecraft Server Engineering**

<p>
  <img src="https://img.shields.io/badge/Minestom-Expert-6D4AFF?style=flat-square"/>
  <img src="https://img.shields.io/badge/Java%2025%20Virtual%20Threads-Expert-ED8B00?style=flat-square"/>
  <img src="https://img.shields.io/badge/Microservices-Expert-4A90D9?style=flat-square"/>
  <img src="https://img.shields.io/badge/Distributed%20Systems-Expert-7B68EE?style=flat-square"/>
  <img src="https://img.shields.io/badge/Packet%20Handling-Advanced-181717?style=flat-square"/>
  <img src="https://img.shields.io/badge/World%20Management-Advanced-2EA44F?style=flat-square"/>
</p>

**Data & Messaging**

<p>
  <img src="https://img.shields.io/badge/MongoDB-Expert-47A248?style=flat-square&logo=mongodb&logoColor=white"/>
  <img src="https://img.shields.io/badge/Redis-Expert-DC382D?style=flat-square&logo=redis&logoColor=white"/>
  <img src="https://img.shields.io/badge/Redis%20Pub%2FSub-Expert-DC382D?style=flat-square"/>
  <img src="https://img.shields.io/badge/Message%20Queues-Advanced-4A90D9?style=flat-square"/>
  <img src="https://img.shields.io/badge/MySQL-Advanced-4479A1?style=flat-square&logo=mysql&logoColor=white"/>
  <img src="https://img.shields.io/badge/PostgreSQL-Advanced-4169E1?style=flat-square&logo=postgresql&logoColor=white"/>
</p>

**Infrastructure & DevOps**

<p>
  <img src="https://img.shields.io/badge/Docker-Advanced-2496ED?style=flat-square&logo=docker&logoColor=white"/>
  <img src="https://img.shields.io/badge/Docker%20Compose-Advanced-2496ED?style=flat-square&logo=docker&logoColor=white"/>
  <img src="https://img.shields.io/badge/Linux-Advanced-FCC624?style=flat-square&logo=linux&logoColor=black"/>
  <img src="https://img.shields.io/badge/Gradle-Advanced-02303A?style=flat-square&logo=gradle&logoColor=white"/>
  <img src="https://img.shields.io/badge/Git-Expert-F05032?style=flat-square&logo=git&logoColor=white"/>
</p>

---

### How I Work

| Principle | In practice |
|---|---|
| **Service isolation by default** | Every microservice owns its data, exposes a clear contract, and fails independently. No shared mutable state across service boundaries. |
| **Async-first communication** | Redis pub/sub, message queues, and virtual threads handle inter-service messaging. No blocking calls in hot paths — ever. |
| **Minestom-native depth** | Direct control over packet flow, entity ticking, and instance management. No compatibility shims, no version-agnostic abstractions that hide the cost. |
| **Operational resilience** | Services are containerized, health-checked, and designed for graceful shutdown. Redis pub/sub failures trigger fallback paths, not cascading outages. |

---

### Notable Work

- **HypixelRecreation** — a Minestom-based, microservices-architected recreation of Hypixel with distributed game shards, Redis-backed inter-service messaging, and MongoDB persistence. Active at [Swofty-Developments/HypixelRecreation](https://github.com/Swofty-Developments/HypixelRecreation).
- **Hypeland** — my reference deployment, where every architectural change is validated under real player load before it ships anywhere else. Live at [hypeland.org](https://hypeland.org/) and `mc.hypeland.org`.

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
