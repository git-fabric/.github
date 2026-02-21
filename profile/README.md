<p align="center">
  <img src="https://raw.githubusercontent.com/git-fabric/.github/main/profile/fabric-banner.svg" alt="git-fabric" width="900">
</p>

## About

**git-fabric** builds composable fabric apps for Git-native infrastructure. Each app is a standalone, independently deployable module that handles one domain well — and connects to everything else through the fabric gateway.

Built by [ry-ops](https://github.com/ry-ops). Consumed by [git-steer](https://github.com/ry-ops/git-steer), [cortex](https://github.com/cortex-io/cortex), and whatever comes next.

## Apps

| App | Description | Status |
|-----|-------------|--------|
| [`cve`](https://github.com/git-fabric/cve) | CVE detection-to-remediation pipeline — scan, enrich, triage, fix | Active |
| [`gateway`](https://github.com/git-fabric/gateway) | Fabric gateway — routes, connects, and orchestrates fabric apps | Scaffolding |

## Architecture

```
┌─────────────────────────────────────────────────────────┐
│                    Consumers                             │
│  git-steer  •  cortex  •  Claude Desktop  •  Actions    │
└────────────────────────┬────────────────────────────────┘
                         │
              ┌──────────▼──────────┐
              │      gateway        │
              │  route • connect •  │
              │  orchestrate        │
              └──┬───────┬──────┬──┘
                 │       │      │
          ┌──────▼──┐ ┌──▼───┐ ┌▼─────┐
          │   cve   │ │ ...  │ │ ...  │
          │ detect  │ │      │ │      │
          │ enrich  │ │      │ │      │
          │ triage  │ │      │ │      │
          │ action  │ │      │ │      │
          │ state   │ │      │ │      │
          └─────────┘ └──────┘ └──────┘
              Fabric Apps
```

## Design Principles

- **One app, one domain** — each fabric app handles a single concern end-to-end
- **Adapter interfaces** — apps define what they need (`GitHubAdapter`, `StateAdapter`), consumers provide implementations
- **Layers, not monoliths** — every app is built from composable layers (detection, intelligence, decision, action, state)
- **MCP-native** — every app exposes its capabilities as MCP tools
- **CLI + Actions** — every app has a CLI for local use and Actions workflows for automation
- **Zero coupling** — fabric apps don't know about each other; the gateway handles routing
