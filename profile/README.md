<p align="center">
  <img src="https://raw.githubusercontent.com/git-fabric/.github/main/profile/fabric-banner.svg" alt="git-fabric" width="900">
</p>

**git-fabric** builds composable fabric apps for Git-native infrastructure. Each app is a standalone, independently deployable module that handles one domain well and connects to everything else through the gateway. Every app exposes its capabilities as **MCP tools**, so Claude, git-steer, Cortex and GitHub Actions can all consume them the same way.

The twist is the routing. The [fabric-sdk](https://github.com/git-fabric/sdk) decides, BGP-style, whether the fabric already knows the answer, through its apps and a layer of small specialized local models, or whether it genuinely needs Claude.

<p align="center">
  <img src="https://raw.githubusercontent.com/git-fabric/.github/main/profile/fabric-map.svg" alt="Consumers call the gateway and fabric-sdk, which routes to ten fabric apps backed by fourteen local models; Claude is called only when nothing else can answer" width="100%">
</p>

## Fabric apps

| App | What it covers |
|---|---|
| [`aiana`](https://github.com/git-fabric/aiana) | Semantic memory, session context and cross-project recall |
| [`chat`](https://github.com/git-fabric/chat) | AI conversation sessions, semantic history search and context threading |
| [`cloudflare`](https://github.com/git-fabric/cloudflare) | DNS, zones, cache and KV |
| [`cve`](https://github.com/git-fabric/cve) | CVE detection to remediation: scan, enrich, triage, fix |
| [`git`](https://github.com/git-fabric/git) | Commit, push, branch, PR and repo management |
| [`k8s`](https://github.com/git-fabric/k8s) | Cluster, pods, deployments, services and logs |
| [`proxmox`](https://github.com/git-fabric/proxmox) | VMs, containers, nodes, storage and snapshots |
| [`sandfly`](https://github.com/git-fabric/sandfly) | Agentless Linux intrusion detection and incident response |
| [`tailscale`](https://github.com/git-fabric/tailscale) | Devices, DNS, ACLs and auth keys |
| [`unifi`](https://github.com/git-fabric/unifi) | Hosts, sites and devices via the UI.com Cloud API |

## Platform

| Repo | Role |
|---|---|
| [`sdk`](https://github.com/git-fabric/sdk) | BGP-style routing for fabric agents: route locally first, Claude only when nobody else can answer |
| [`gateway`](https://github.com/git-fabric/gateway) | Routes, connects and orchestrates fabric apps |
| [`fabric-ctrl`](https://github.com/git-fabric/fabric-ctrl) | Zero-trust control plane: GitHub App identity, security automation, MCP org tooling |
| [`fabric-review`](https://github.com/git-fabric/fabric-review) | Automated PR review engine for the ecosystem |
| [`fabric-forge`](https://github.com/git-fabric/fabric-forge) | k3s cluster + Helm charts for the Fabric-SDK runtime, one script |
| [`pipelines`](https://github.com/git-fabric/pipelines) | Five scheduled pipelines composing gateway tools into homelab intelligence |
| [`terminal`](https://github.com/git-fabric/terminal) | Claude Code + tmux + kubectl in a persistent container |
| [`yt-adr-feed`](https://github.com/git-fabric/yt-adr-feed) | YouTube transcripts into Qdrant and an ADR pipeline, deterministic |
| [`adr`](https://github.com/git-fabric/adr) | Global Architecture Decision Records |
| [`fabric-state`](https://github.com/git-fabric/fabric-state) | CVE queue state and scan history for fabric-ctrl |

## fabric-llm: the local models

Fourteen Ollama models, each specialized for one API, answer locally before anything escalates to Claude.

| Repo | Model | Specialty |
|---|---|---|
| [aiana-vllm](https://github.com/git-fabric/aiana-vllm) | AIANA-Ops | semantic memory |
| [cloudflare-vllm](https://github.com/git-fabric/cloudflare-vllm) | Cloudflare-Ops | Cloudflare v4 API |
| [cve-vllm](https://github.com/git-fabric/cve-vllm) | CVE-Ops | NVD / GHSA / CISA KEV |
| [fabric-invoke-vllm](https://github.com/git-fabric/fabric-invoke-vllm) | fabric-invoke | orchestration runtime |
| [fabric-router-vllm](https://github.com/git-fabric/fabric-router-vllm) | fabric-router | fabric-sdk meta-routing |
| [git-steer-vllm](https://github.com/git-fabric/git-steer-vllm) | git-steer-Ops | git-steer internals |
| [github-vllm](https://github.com/git-fabric/github-vllm) | GitHub-Ops | GitHub REST API |
| [k3s-vllm](https://github.com/git-fabric/k3s-vllm) | k3s-Ops | k3s / Kubernetes API |
| [n8n-vllm](https://github.com/git-fabric/n8n-vllm) | n8n-Ops | n8n REST API v1 |
| [proxmox-vllm](https://github.com/git-fabric/proxmox-vllm) | Proxmox-Ops | Proxmox VE API |
| [qdrant-vllm](https://github.com/git-fabric/qdrant-vllm) | qdrant-fabric-Ops | Qdrant vector ops |
| [sandfly-vllm](https://github.com/git-fabric/sandfly-vllm) | Sandfly-Ops | Sandfly Security v4 API |
| [tailscale-vllm](https://github.com/git-fabric/tailscale-vllm) | Tailscale-Ops | Tailscale v2 API |
| [unifi-vllm](https://github.com/git-fabric/unifi-vllm) | UniFi-Ops | UniFi API |

## Design principles

- **One app, one domain:** each fabric app handles a single concern end to end.
- **Adapter interfaces:** apps define what they need (`GitHubAdapter`, `StateAdapter`); consumers provide implementations.
- **Layers, not monoliths:** every app is built from composable layers (detection, intelligence, decision, action, state).
- **MCP-native:** every app exposes its capabilities as MCP tools.
- **CLI + Actions:** every app has a CLI for local use and Actions workflows for automation.

<p align="center"><sub>Built by <a href="https://github.com/ry-ops">ry-ops</a> · consumed by <a href="https://github.com/ry-ops/git-steer">git-steer</a>, <a href="https://github.com/cortex-io">Cortex</a>, and whatever comes next</sub></p>
