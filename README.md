<div align="center">

<img src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&weight=600&size=26&duration=3000&pause=800&color=61DAFB&center=true&vCenter=true&width=650&lines=Hi%2C+I'm+Yuvraj+%F0%9F%91%8B;Full-stack+engineer+%2B+applied+ML;Shipping+FULLTIME+%E2%80%94+7+live+games;Building+Relay+%E2%80%94+a+job+queue+in+Java+21;New+Grad+SWE+2027" alt="Typing SVG" />

<br>

<a href="https://playfulltime.com"><img src="https://img.shields.io/badge/🎮_Play_FULLTIME-000000?style=for-the-badge&logoColor=white" /></a>
<a href="https://www.linkedin.com/in/yuvraj-singh-goraya-68642133b/"><img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" /></a>
<a href="mailto:yuvgoraya23799@gmail.com"><img src="https://img.shields.io/badge/Email-EA4335?style=for-the-badge&logo=gmail&logoColor=white" /></a>

<br><br>

<img src="https://img.shields.io/badge/🎓_Grad-December_2026-7F52FF?style=flat-square" />
<img src="https://img.shields.io/badge/📍_Location-Surrey,_BC-1D9E75?style=flat-square" />
<img src="https://img.shields.io/badge/💼_Status-Open_to_New_Grad_SWE-D85A30?style=flat-square" />
<img src="https://komarev.com/ghpvc/?username=Yuv1008&style=flat-square&color=61DAFB&label=PROFILE+VIEWS" />

</div>

---

<div align="center">

### 👇 Everything below is expandable — click to explore

</div>

---

<details open>
<summary><h2>🚀 &nbsp;Projects &nbsp;<sub><i>(click any to expand)</i></sub></h2></summary>

<br>

<details open>
<summary><b>🎮 &nbsp;FULLTIME</b> — multi-sport puzzle platform &nbsp;<code>LIVE</code></summary>

<br>

> **Seven live sports games. Four shared engines. One daily puzzle for everyone.**

<a href="https://playfulltime.com"><img src="https://img.shields.io/badge/▶_Live_Site-playfulltime.com-000000?style=for-the-badge" /></a>
<a href="https://github.com/Yuv1008/Fulltime"><img src="https://img.shields.io/badge/Source-181717?style=for-the-badge&logo=github" /></a>

**The interesting problem:** seven sports, but only four *kinds* of game. Building seven separate implementations would have meant seven codebases to maintain. Instead every sport plugs into a shared engine.

| Sport | Game | Engine |
|:--|:--|:--|
| ⚽ Football | Career Path | `careerPath` |
| 🏀 Basketball | Career Path: NBA | `careerPath` |
| 🏏 Cricket | Stat Attack | `higherLower` |
| 🎾 Tennis | Grand Slam Duel | `higherLower` |
| ⚾ Baseball | Diamond Legacy | `higherLower` |
| 🏎️ F1 | Podium Order | `ordering` |
| 🏉 Rugby | Nations Quiz | `quiz` |

<details>
<summary><i>→ How the architecture works</i></summary>

<br>

```mermaid
graph TD
    A[games/registry.ts<br/>single source of truth] --> B[careerPath]
    A --> C[higherLower]
    A --> D[ordering]
    A --> E[quiz]
    B --> F[(entities<br/>entity_facts)]
    C --> F
    D --> F
    E --> F
    G[seeding.ts<br/>mulberry32 + FNV-1a] --> B
    G --> C
    G --> D
    G --> E
```

**Sport-agnostic schema.** Rather than seven sets of tables, everything lives in `entities` (any player, team, driver) and `entity_facts` (any fact about them), with per-sport variation held in a `jsonb` meta column.

**Deterministic daily puzzles.** A seeded PRNG (mulberry32 + FNV-1a) keyed to the UTC date means every player worldwide gets the identical puzzle — with no coordination between clients and no server round-trip to decide what today's puzzle is.

**Anonymous-first.** Stats, streaks, and XP live in localStorage and sync to Supabase only if you choose to sign in. No account required to play or to hit the leaderboard.

</details>

<code>Next.js 14</code> <code>TypeScript</code> <code>PostgreSQL</code> <code>Supabase</code> <code>Vercel</code>

</details>

<br>

<details>
<summary><b>⚙️ &nbsp;Relay</b> — distributed job queue &nbsp;<code>IN PROGRESS</code></summary>

<br>

> **A job queue modeled on Amazon SQS, written in Java 21.**

Built to understand what actually happens inside a message queue — delivery guarantees, timeout handling, and what it takes for multiple consumers to poll the same table without stepping on each other.

<details>
<summary><i>→ Design goals</i></summary>

<br>

```mermaid
graph LR
    P[Producer] -->|enqueue| Q[(Queue)]
    Q -->|dequeue| C1[Consumer 1]
    Q -->|dequeue| C2[Consumer 2]
    C1 -->|ack| Q
    C2 -.->|timeout| Q
    Q -->|N retries| D[(Dead letter)]
```

- **At-least-once delivery** — a message is never silently lost
- **Visibility timeouts** — an in-flight message is hidden from other consumers, and reappears if the worker dies
- **Dead-letter routing** — after a configurable retry limit, poison messages get quarantined instead of looping forever
- **Multi-module Gradle build** — queue engine, API layer, and client library kept separate

</details>

<code>Java 21</code> <code>PostgreSQL</code> <code>Gradle</code>

</details>

<br>

<details>
<summary><b>🎓 &nbsp;UniHelp</b> — AI campus assistant &nbsp;<code>IN PROGRESS</code></summary>

<br>

> **Answers student questions from real institutional documents — not from model recall.**

A retrieval-augmented assistant built with my brother. Every answer is grounded in a source document, which is the whole point: a campus assistant that confidently invents a tuition deadline is worse than no assistant at all.

<details>
<summary><i>→ The RAG pipeline</i></summary>

<br>

```mermaid
graph LR
    A[Campus docs] --> B[Chunking]
    B --> C[Embeddings]
    C --> D[(pgvector)]
    E[Student question] --> F[Vector search]
    D --> F
    F --> G[Claude API]
    G --> H[Grounded answer]
```

**What I own:** the retrieval pipeline end to end — chunking strategy, embedding generation, and vector similarity search over pgvector — plus the FastAPI backend and the API contract between us.

</details>

<code>React Native</code> <code>Next.js</code> <code>FastAPI</code> <code>Supabase</code> <code>pgvector</code> <code>Claude API</code>

</details>

<br>

<details>
<summary><b>🔐 &nbsp;Insider Threat Detection</b> — anomaly detection &nbsp;<code>COMPLETE</code></summary>

<br>

> **Catches threats it has never seen before.**

An autoencoder and a variational autoencoder trained *only* on normal user activity. Anything the model reconstructs badly is, by definition, unlike normal behaviour — which means it flags novel attack patterns that a supervised classifier trained on known threats would miss entirely.

<details>
<summary><i>→ Why unsupervised</i></summary>

<br>

Labelled insider-threat data barely exists, and the threats that matter most are the ones nobody has catalogued yet. Training on normal behaviour sidesteps both problems: you only need to define *normal*, and everything else falls out as deviation measured by reconstruction error.

</details>

<code>Python</code> <code>PyTorch</code> <code>Pandas</code> <code>NumPy</code>

</details>

<br>

<details>
<summary><b>📦 &nbsp;Earlier projects</b></summary>

<br>

| Project | What it is | Stack |
|:--|:--|:--|
| EventSphere | Full-stack event management platform | React · FastAPI · SQLite |
| CHRONOVAULT | Premium single-page retail experience | React · Tailwind · Framer Motion |
| Hoppy Tales | Android storytelling app | Kotlin · Android SDK |
| FastCabs | Relational database design for ride-hailing | MySQL |
| Hotel Management System | Desktop booking and inventory system | Java |
| FIFA World Cup Simulator | Tournament simulation engine | C++ |

</details>

</details>

---

<details open>
<summary><h2>🛠️ &nbsp;Stack</h2></summary>

<br>

<div align="center">

**Languages**

![Java](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![Python](https://img.shields.io/badge/Python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![C++](https://img.shields.io/badge/C++-00599C?style=for-the-badge&logo=c%2B%2B&logoColor=white)
![Kotlin](https://img.shields.io/badge/Kotlin-7F52FF?style=for-the-badge&logo=kotlin&logoColor=white)

**Frontend**

![React](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)
![Next.js](https://img.shields.io/badge/Next.js-000000?style=for-the-badge&logo=next.js&logoColor=white)
![Tailwind](https://img.shields.io/badge/Tailwind-38B2AC?style=for-the-badge&logo=tailwind-css&logoColor=white)

**Backend & Data**

![FastAPI](https://img.shields.io/badge/FastAPI-005571?style=for-the-badge&logo=fastapi&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-6DA55F?style=for-the-badge&logo=node.js&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
![Supabase](https://img.shields.io/badge/Supabase-3FCF8E?style=for-the-badge&logo=supabase&logoColor=white)

**ML & Tools**

![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-0db7ed?style=for-the-badge&logo=docker&logoColor=white)
![Gradle](https://img.shields.io/badge/Gradle-02303A?style=for-the-badge&logo=gradle&logoColor=white)
![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)

</div>

</details>

---

<details>
<summary><h2>🎓 &nbsp;Education &amp; background</h2></summary>

<br>

**Bachelor of Computer Information Systems** — University of the Fraser Valley
Software Development major · AI/ML minor · Expected December 2026
**GPA 3.86 / 4.33** · Dean's List, 4 consecutive terms

**Coursework:** Data Structures & Algorithms · Design & Analysis of Algorithms · Distributed Computing & MapReduce · Operating Systems · Database Systems · Software Development Best Practices · Machine Learning

<br>

**Currently:** AI Intern at InAmigos Foundation · 3+ years part-time at Costco Wholesale alongside a full course load

**Trilingual** in English, Hindi and Punjabi. Messi fan. Will argue about it.

</details>

---

<details>
<summary><h2>📊 &nbsp;Stats</h2></summary>

<br>

<div align="center">

<img height="165" src="https://github-readme-stats.vercel.app/api?username=Yuv1008&theme=tokyonight&hide_border=true&include_all_commits=true&count_private=true&bg_color=00000000" />
<img height="165" src="https://github-readme-stats.vercel.app/api/top-langs/?username=Yuv1008&theme=tokyonight&hide_border=true&include_all_commits=true&count_private=true&layout=compact&bg_color=00000000&langs_count=8" />

<br><br>

<img src="https://streak-stats.demolab.com?user=Yuv1008&theme=tokyonight&hide_border=true&background=00000000" />

<br><br>

<img src="https://github-readme-activity-graph.vercel.app/graph?username=Yuv1008&theme=tokyo-night&hide_border=true&bg_color=00000000&area=true" />

<br>

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/Yuv1008/Yuv1008/output/github-contribution-grid-snake-dark.svg" />
  <img src="https://raw.githubusercontent.com/Yuv1008/Yuv1008/output/github-contribution-grid-snake.svg" />
</picture>

</div>

</details>

---

<div align="center">

### 💬 Ask me about

`RAG pipelines` · `shipping side projects around a part-time job` · `why seven games only needed four engines`

<br>

**Open to New Grad Software Engineer roles starting 2027.**

<a href="mailto:yuvgoraya23799@gmail.com"><img src="https://img.shields.io/badge/Get_in_touch-EA4335?style=for-the-badge&logo=gmail&logoColor=white" /></a>

</div>
