# qbittorrent-mcp-server

An [MCP](https://modelcontextprotocol.io) server that exposes a qBittorrent instance running on-premise — on the same Raspberry Pi cluster behind [TradePilot](https://github.com/zeluizgo/tradepilot-overview) — as a tool an AI agent can call directly. Add a magnet link, check download status, from a conversation with Claude instead of opening a browser tab to the cluster.

## Why this exists

The cluster this runs on is the same one documented in the two studies below — a home lab that started as "can I monitor my own media library" and grew into a Docker Swarm cluster running production services. This project is the next logical step: instead of a human operating services on the cluster, an AI agent operates them, through a typed, auditable interface — the same "typed tools, not free text" principle TradePilot's AI orchestrator uses for market data.

## The series this continues

| # | Study | Year |
|---|---|---|
| 1 | [Docker fundamentals — home monitoring & media library](https://medium.com/@joseluizcg/estudo-1-primeira-aplicação-prática-de-docker-monitoração-e-biblioteca-de-mídia-própria-em-casa-b8f188ef98b0) | 2022 |
| 2 | [Docker Swarm orchestration — a Spark cluster for data science](https://medium.com/@joseluizcg/estudo-2-orquestração-nativa-docker-swarm-spark-em-cluster-para-ciência-de-dados-51c14f861964) | 2023 |
| 3 | Spark over reactive Spring Boot — *in progress* | — |
| 4 | **MCP as a bridge: putting on-premise services in reach of an AI agent** — *this repo is the working proof, article to follow* | — |

If #1 was "I can run services at home" and #2 was "I can orchestrate them properly," this is "an AI agent can now operate them too" — without SSH, without a dashboard, through a protocol built for exactly this.

## What it does

- Accepts a magnet link and starts the download on the target qBittorrent instance
- Confirms the download started and reports back status
- Runs as an MCP server, so any MCP-compatible client (Claude, Claude Code, other agent tooling) can call it as a tool — no custom integration per client

## Why MCP, not a REST wrapper

A REST wrapper would need a bespoke client on every side that wants to use it. MCP standardizes the contract: the server declares its tools once, and any compliant agent can discover and call them the same way it calls every other tool in its toolbox. For a home lab exposing a handful of services to an agent, that standardization is the entire point — one server, reusable across every agent surface, present and future.

## Stack

Runs alongside the other services on the same on-prem Docker Swarm cluster documented in the studies above.

---

Built by [José Luiz Clemente Gonçalves](https://github.com/zeluizgo) — see [TradePilot](https://github.com/zeluizgo/tradepilot-overview) for the production system this same cluster also runs.
