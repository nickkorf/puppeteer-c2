# puppeteer-c2

**puppeteer-c2** is a modular, Go-based **Command & Control (C2) orchestration framework** designed for **legitimate pentesting labs**, red team simulations, and advanced Go learning.  
It is **not** designed for illegal use, persistence on unauthorized systems, or evasion of defenses.

---

## 🧭 Project Scope

This project aims to build a **bare-minimum but extensible** C2 framework in Go, focusing on:

- ✅ Secure transport using mTLS (agent ↔ server),
- 🧠 Clean separation of components (server / agent / operator CLI),
- 🧰 Modular task execution using a **whitelisted TaskRunner registry**,
- 📜 Full audit logging and operator accountability,
- 🧪 Safe, transparent operation in **authorized environments only**.

The project is structured as a learning journey through Go (stages G0 → GX) and can evolve to support more advanced features like gRPC, scheduling, or sidecar workers.

---

## ⚠️ Legal Disclaimer

> This software is provided **strictly for use in authorized penetration testing labs** and red team simulations.  
> Any use of this project against systems you do not own or have explicit permission to test is **illegal** and prohibited.  
> The author and contributors accept no responsibility for misuse.

---

## 🧱 Core Architecture

[Operator CLI/TUI] ──(auth)──> [Orchestrator API]
│ │
[Policy Engine]│
│ └──> [Storage: DB + Artifacts]
│
[Job Router]
│
(mTLS pull channel)
│
[Agents]
(capabilities registry)


### Components

- **Server** (`cmd/server`)  
  - HTTPS API with mTLS  
  - JWT operator auth  
  - Task queue, policy validation, storage, metrics

- **Agent** (`cmd/agent`)  
  - Pull beacon loop over mTLS  
  - Capability manifest  
  - Whitelisted task runners (inventory, net interfaces, file collect, etc.)

- **CLI/TUI** (`ui/cli`)  
  - Operator tool to manage agents, queue tasks, view results and audits

---

## 🚀 Getting Started

### Prerequisites
- Go ≥ 1.22  
- `make` and `golangci-lint`  
- `openssl` (for test PKI)

### First steps

```bash
# Clone and enter
git clone https://github.com/nickkorf/puppeteer-c2.git
cd puppeteer-c2

# Initialize modules
go mod tidy

# Build server and agent
make build
