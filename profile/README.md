## Lobstack

The deployment layer for business AI agents. Every agent gets a dedicated
machine with persistent memory, real tool integrations and multi-channel access,
reachable through one OpenAI-compatible API.

### Repositories

| | What it is |
| --- | --- |
| **[lobstack](https://github.com/Lobstack-ai/lobstack)** | The control plane and the website. Next.js app, the Gateway, the Console, provisioning, billing, Overseer and Operator. |
| **[agent-bridge](https://github.com/Lobstack-ai/agent-bridge)** | The Agent Runtime that runs on every agent VM. Separately versioned, rolled out to the fleet on its own schedule. |
| **[lob-bot](https://github.com/Lobstack-ai/lob-bot)** | The desktop agent harness — Tauri shell, Node daemon, connectors. |
| **[sdk](https://github.com/Lobstack-ai/sdk)** | TypeScript client for the API: inference, usage, keys. Dependency-free. |
| **[contracts](https://github.com/Lobstack-ai/contracts)** | Lobstack Pay smart contracts — LobstackSettlement (LSP-1), Foundry. |
| **[infra](https://github.com/Lobstack-ai/infra)** | Terraform, Kubernetes, Helm, Vault. |
| **[agent](https://github.com/Lobstack-ai/agent)** | Lobstack Agent. |

### How the pieces fit

```
                    ┌──────────────────────────┐
  a browser  ─────► │   Console  (lobstack)    │
  Lob Bot    ─────► │   Gateway  (lobstack)    │ ◄──── an SDK, or any
  your code  ─────► │      /api/gateway/v1     │       OpenAI client
                    └────────────┬─────────────┘
                                 │  provisions, meters, controls
                                 ▼
                    ┌──────────────────────────┐
                    │  agent VM (agent-bridge) │  one per agent
                    └──────────────────────────┘
```

Everything that talks to the API carries an API key and comes back with a
request id, so a failure can be looked up rather than described.

### A note on the split

`agent-bridge`, `contracts` and `infra` were extracted from `lobstack` with
their history intact — `git blame` still works, and commits from before the
split remain in `lobstack` too. They live apart because they ship on different
schedules to different targets: the control plane deploys on every merge, the
runtime deploys to a fleet of machines behind a version number, and the
contracts deploy to a chain and then never change.
