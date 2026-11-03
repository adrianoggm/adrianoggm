# 👋 Hi, I'm Adriano García-Giralda Milena

💻 **Software Engineer @ INNOVASUR** · 🎓 **M.Sc. in Computer Engineering — University of Granada** · 🔬 **Distributed AI research**

I build the parts that make real-world data useful: third-party integrations, ETL pipelines, event-driven backends, and the infrastructure that keeps them running in production. In the lab, I research federated learning at the edge and what happens to a time series when you turn it into an image.

🌐 **Portfolio:** [adrianoggm.github.io](https://adrianoggm.github.io/)

---

## ✍️ How I Work

*Field notes: habits I picked up running production systems. I learned most of them the hard way.*

### 1. Production is read-only until proven otherwise

When something breaks in production, I look before I touch anything. I gather evidence (logs, events, node state, diffs), write down a diagnosis and a proposed fix, and only then change things, with the people who own the system knowing what is about to happen. A fix nobody understood just becomes the next incident.

### 2. Verify before shipping, watch while it lands

A deploy is a checklist. Before applying, I confirm that every artifact the change references exists in the registry, and I run a diff that should show only what I expect to change. During the rollout, I watch it and check which node each pod lands on: a node low on disk will evict your pods while it pulls a 1 GB image. Afterwards, I check the service from the outside. "Pods are Running" is not the same as working.

### 3. Narrate the waits

Rollouts, image pulls and migrations are where incidents hide. I say up front what I'm waiting for and why. I use short timeouts with checks in between, and I report anomalies (evictions, restarts, unexpected diffs) as soon as they appear, not at the end.

### 4. Secrets never travel in clear text

Secrets live encrypted in the repository (SOPS + age) and a script applies them. Passwords go through stdin, never as arguments or into shell history. When I generate a credential, I fill it in and encrypt it in the same command, so a plaintext copy never touches the disk. If a secret has already been committed, it goes on the list to rotate and move to the vault, and that list gets worked.

### 5. Rehearse irreversible changes

Schema changes can't be rolled back, so they run against a local copy of the database first. I'm just as wary of scripts that stitch migrations together: a single missing trailing newline can silently turn the next statement into a comment.

### 6. Write down the traps

Next to every procedure I keep a short list of the gotchas that cost me time:

- line endings that break shell scripts
- certificate files with no trailing newline
- archive filenames containing `*` that vanish when extracted on Windows
- key fingerprints that differ only because of CRLF

The README holds the steps and the notes hold the traps, so the next person (usually future me) doesn't pay for them twice.

### 7. Architecture as a shared vocabulary

For backend services I default to **hexagonal architecture + CQRS**, in NestJS/TypeScript and FastAPI/Python. Every service uses the same layers (domain / application / infrastructure / interface), naming, structured logs and README template. I don't do it for purity: it means any teammate can open any service and know where things are.

### 8. Small, traceable changes

Every task follows the same path: ticket, branch, short plan, implementation, verification against real environments, atomic commits, and a merge request that someone can actually review. In deployment repositories I make one commit per changed manifest, so `git log` reads like a changelog.

### 9. Less code, on purpose

Before writing something, I check three things: does it need to exist, do the standard library or the platform already do it, and what is the smallest version that works. When I take a shortcut on purpose, I leave a comment that names its limit and how to upgrade it. That way the simple version reads as a decision, not an oversight.

### 10. Encode what the team knows

I turn recurring procedures into written playbooks that both people and AI coding agents can follow. Examples include onboarding a new tenant, building Power BI reports and semantic models as code on Microsoft Fabric, and producing data-lineage documents for clients. AI multiplies what I can get done, but it doesn't run on autopilot: it follows the same rules as everyone else (production is read-only, verify before applying, no secrets in clear text).

### 11. Be honest about results

The same rules apply in research: honest baselines, statistical tests, and a hunt for leakage before celebrating. When I re-evaluated my own federated-learning prototype, I found no significant federated-vs-centralized difference, and I found data leakage in the dataset. That result is worth more than a nice chart. New research ideas go through an adversarial review that actively looks for prior work that would sink them.

---

## 🏗️ What I Do

- **Backend & integrations:** microservices and connectors that turn many different APIs, devices and platforms into reliable products: REST, MQTT, RabbitMQ, event-driven flows.
- **Data engineering:** ingestion, ETL and time-series storage for IoT and Smart City platforms, plus analytics on Microsoft Fabric and Power BI.
- **Infrastructure:** containerized services on Docker and Kubernetes (k3s), with GitLab CI/CD, Traefik routing, a private Harbor registry and Grafana observability.
- **AI in production:** LLM, RAG and agent integrations that keep model interpretation separate from deterministic services and actions the user has authorized.

---

## 🔬 Research

I collaborate with the **MYDASS research group** on the **OnTheEdge project**, working on real-time stress monitoring and on processing physiological and contextual data at the edge.

- **Federated learning under real constraints:** non-IID data, client drift, robust aggregation, differential privacy, unreliable networks, and continual or asynchronous training.
- **Time series as images:** Recurrence Plots, Gramian Angular Fields and Markov Transition Fields. How much information survives the encoding, whether the original signal can be reconstructed from it, and how useful the image is for downstream ML.

---

## 📂 Selected Projects

| Project | What it is |
|---|---|
| [Onion-FL](https://github.com/adrianoggm/Onion-FL) | Hierarchical federated-learning framework and simulator (edge → fog → cloud): SCAFFOLD, FedNova, FedDyn, MOON, Byzantine attacks, differential privacy. |
| [time-series-image-reconstruction](https://github.com/adrianoggm/time-series-image-reconstruction) | Reproducible benchmark of information loss and signal reconstruction across image encodings of time series. |
| [flower-basic](https://github.com/adrianoggm/flower-basic) | Flower + MQTT fog-computing prototype, plus the statistical re-evaluation described above. |
| [FinGuard](https://github.com/adrianoggm/FinGuard) | Voice and text banking assistant (LangGraph) that keeps the LLM away from deterministic logic and authorized actions. |
| [MoodPal](https://github.com/adrianoggm/MoodPal) | Android wellbeing app built in 48 h. 🥈 2nd prize at HackForGood UGR 2024 (Telefónica Chair), advanced to the national phase. |
| [FootballHubManager](https://github.com/adrianoggm/footballhubmanager) | FastAPI + React platform for amateur football leagues: players, seasons, standings and player-performance stats. |
| [TrueBeamControl](https://github.com/adrianoggm/TrueBeamControl) | Streamlit tool for daily quality-control CSVs from a medical linear accelerator (TrueBeam), with tolerance lines. |

---

## 🛠️ Tech Stack

| Area | Tools |
|---|---|
| Languages | `Python` · `TypeScript` · `JavaScript` · `SQL` · `Java` · `C++` · `Kotlin` |
| Backend | `NestJS` · `FastAPI` · `Node.js` · `RabbitMQ` · `MQTT` · `Redis` |
| Data | `MySQL` · `PostgreSQL` · `MongoDB` · `InfluxDB` · `Microsoft Fabric` · `Power BI` |
| Infrastructure | `Docker` · `Kubernetes (k3s)` · `Helm` · `Traefik` · `Harbor` · `GitLab CI/CD` · `GitHub Actions` · `Grafana` · `SOPS + age` |
| AI / ML | `PyTorch` · `scikit-learn` · `Flower` · `LangGraph` · `RAG` · `LLM integration` |

---

## 🎯 Where I'm Heading

I want to keep working where **research meets real-world engineering**: intelligent systems that have to run reliably across distributed, messy environments. I'm also interested in pursuing a **PhD on intelligent and distributed systems**.

Outside the keyboard: sport, football and a good game. I'm competitive, but I care just as much about good teammates and making the next version better.

---

## 🌐 Connect with Me

<p align="center">
  <a href="https://adrianoggm.github.io/">
    <img src="https://img.shields.io/badge/Portfolio-1f2937?style=for-the-badge&logo=githubpages&logoColor=white" />
  </a>
  <a href="https://linkedin.com/in/adriano-garcía-giralda-milena-7b7a152a9">
    <img src="https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white" />
  </a>
  <a href="mailto:adrianogarciagiraldamilena@gmail.com">
    <img src="https://img.shields.io/badge/Email-EA4335?style=for-the-badge&logo=gmail&logoColor=white" />
  </a>
  <a href="https://x.com/adrianolol12345">
    <img src="https://img.shields.io/badge/X-000000?style=for-the-badge&logo=x&logoColor=white" />
  </a>
</p>

<p align="center">
  <b>Building intelligent systems from data to deployment.</b>
</p>
