# UNAXIS

**A terminal control plane for self-hosted, multi-host web platforms.**

UNAXIS runs your platform from one TUI and one CLI: Next.js zones built and shipped from your own git forge, Docker hosts reached through a small agent on each machine, a reverse proxy and Nginx Proxy Manager for the edge, Supabase instances, encrypted backups, a secrets vault and media services. It is built for people who run their own hardware and want the convenience of a PaaS without handing it over.

> This repository is the public home of UNAXIS: install instructions, documentation, releases and issues. The source is developed on a private forge.

## Install

Requirements: Windows with WSL2 (Ubuntu) or Linux, Docker (Docker Desktop on Windows), [Bun](https://bun.sh) ≥ 1.1, Node ≥ 20, git.

```bash
npm install -g @untsystems/unaxis
unaxis --version
```

## Quick start

1. Describe your project to UNAXIS with a `unaxis.json` at its root (see [`examples/unaxis.json`](examples/unaxis.json)).
2. Start the TUI from anywhere: `unaxis`. Pick your project, or point at it with `UNAXIS_PROJECT_ROOT=/path/to/project unaxis`.
3. Add your machines as environments; each gets the UNAXIS agent (one container, updated by its own health-gated updater with automatic rollback).

## What it does

| Area | Commands |
|---|---|
| Zones (sites/apps) | `unaxis zone <key> build \| dev start \| logs \| status` — ship an exact forge commit with `build --ref main` |
| Hosts | `unaxis env list \| ping \| health \| containers \| update` |
| Edge | `unaxis sync-routes`, `unaxis npm …` |
| Data | `unaxis data status \| backup` — continuous Postgres archiving (WAL-G) to an S3-compatible store on another machine |
| Backups | `unaxis backup status \| run` — restic, to several targets |
| Secrets | `unaxis secrets status \| link \| open` — a self-hosted vault per project |
| Forge | `unaxis forge status \| backup` — your own git server as the source of truth |
| Projects | `unaxis project clone \| use \| workspaces` — develop from any machine |

Full command reference: [`docs/cli.md`](docs/cli.md). What changed: [`CHANGELOG.md`](CHANGELOG.md).

## Design in one paragraph

Every machine runs the same agent; the TUI talks to them over your private network with per-machine key pairing (no shared secrets). Production ships from your forge, never from a laptop's working copy. Every class of state has a home and a live copy on another machine: code on the forge and its backups, the database archived continuously, uploads replicated, and only the root keys held by a person.

## Feedback

Bugs and ideas: [open an issue](../../issues). Security reports: please use GitHub's private vulnerability reporting rather than a public issue (see [`SECURITY.md`](SECURITY.md)).
