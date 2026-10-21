# UNAXIS CLI reference

Generated from UNAXIS 0.0.88. Every command also runs inside the TUI; `--bg` queues long operations as background stack items (watch them with `unaxis stacks`).

## `unaxis backup`

Workspace backups with restic: encrypted, versioned snapshots of the dev drive to several targets (folders, or rest-server on any UNAXIS host). Nightly by default.

Subcommands: `status`, `run`, `snapshots`, `source`, `target`, `schedule`

Arguments: `action` (optional), `name` (optional), `path` (optional)

| Option | Type | Description |
|---|---|---|
| `--dir` | string | target add: a folder on the control-plane host. |
| `--env` | string | target add: deploy an append-only rest-server on this UNAXIS host and use it. |
| `--port` | number | target add --env: rest-server port (default 8010). |

## `unaxis build-doctor`

Diagnose build-time SSG hangs: Docker memory + endpoint reachability from the project network.

Arguments: `zone` (optional)

## `unaxis build-mem`

Snapshot every container's memory usage + limit (run during a build to watch the builder).

## `unaxis builder-reset`

Remove the unaxis-net buildx builder (recreated on next build); unsticks a zombie build.

## `unaxis changelog`

One changelog per part of the platform, from commit messages and the deploy ledger. <zone>: each deploy and the commits it shipped (the zone's own source + core), plus what is committed but not deployed yet. core / unaxis / services [<name>]: recent commits by day. No argument: every zone's deploy state and the latest change in each scope.

Arguments: `target` (optional), `name` (optional)

| Option | Type | Description |
|---|---|---|
| `--limit` | number | Zone: deploys to show (default 10). Scopes: commits (default 30). |
| `--json` | boolean | Machine-readable output. |

## `unaxis clean`

Prune unused Docker images/stopped containers/build cache to free disk. Never touches volumes or anything a running container needs.

| Option | Type | Description |
|---|---|---|
| `--dry-run` | boolean | Show what docker system df currently reports without deleting anything. |

## `unaxis data`

Production data's live copy on another machine. An object store (Garage, S3-compatible) placed on any UNAXIS host; Postgres archives its write-ahead log there continuously (WAL-G) plus a nightly base backup, so the database can be restored to any minute. `archive setup` writes WAL-G's config and takes a base backup (no restart); `archive enable` sets archive_mode, which takes effect at the next Postgres restart.

Subcommands: `status`, `place`, `deploy`, `backup`, `archive`

Arguments: `target` (optional)

| Option | Type | Description |
|---|---|---|
| `--bg` | boolean | deploy / backup / archive setup: run as a background stack op. |

## `unaxis db control-info`

Show local SQLite control-db path, zone count, environment count, and schema version.

## `unaxis db core`

Interact with the core control plane database.

Subcommands: `status`, `heal`, `restart`

| Option | Type | Description |
|---|---|---|
| `--bg` | boolean | Run operation in background. |
| `--json` | boolean | Output output/task status as JSON. |

## `unaxis db instances`

List all active Supabase tenant databases.

| Option | Type | Description |
|---|---|---|
| `--json` | boolean | Output as structured JSON. |

## `unaxis db migrate-control`

One-time import: migrate zones + environments from project.db (Supabase) into the local SQLite control-plane DB. Safe to re-run.

## `unaxis domain`

Manage provider-aware domain controllers and their zone bindings.

Subcommands: `list`, `add`, `show`, `check`, `records`, `capabilities`, `backend`, `official-inspect`, `plan`, `dns-plan`, `plans`, `plan-cancel`, `plan-apply`, `bind`, `unbind`, `remove`, `help`

Arguments: `name` (optional), `zone` (optional)

| Option | Type | Description |
|---|---|---|
| `--provider` | string | Provider: dns, unstoppable, ens, or web3. |
| `--role` | string | Role: primary, alias, redirect, identity, or decentralized-site. |
| `--project` | string | Owning project slug. |
| `--workspace` | string | Domain-controller workspace path; may be on another drive. |
| `--owner` | string | Onchain owner address (metadata only). |
| `--chain` | string | Onchain network name. |
| `--path` | string | Path mounted to the zone binding. Default: /. |
| `--confirm` | boolean | Confirm registry removal; external records are never deleted. |
| `--json` | boolean | Output structured JSON. |

## `unaxis env audit-image`

Audit image layers for embedded secrets or bloated COPY commands.

Arguments: `imageName`, `envName` (optional)

| Option | Type | Description |
|---|---|---|
| `--json` | boolean | Output as structured JSON. |

## `unaxis env containers`

List raw Docker containers related to an environment.

Arguments: `envName`

| Option | Type | Description |
|---|---|---|
| `--json` | boolean | Output as structured JSON. |

## `unaxis env events`

Stream recent Docker events.

Arguments: `envName` (optional)

| Option | Type | Description |
|---|---|---|
| `--since` | string | Look back a time window (e.g. 1h, 30m). |
| `--json` | boolean | Output as structured JSON. |

## `unaxis env health`

Deep state detection per environment: online, busy, sleeping (engine off), wedged, restarting, agent-down, or offline.

Arguments: `envName` (optional)

| Option | Type | Description |
|---|---|---|
| `--json` | boolean | Output as structured JSON. |

## `unaxis env images`

List or clean Docker images on an environment.

Arguments: `envName` (optional)

| Option | Type | Description |
|---|---|---|
| `--json` | boolean | Output as structured JSON. |
| `--prune-stale` | boolean | Find stale UNAXIS image tags. |
| `--dangling-only` | boolean | Limit stale-image pruning to dangling images. |
| `--remove-repo` | string | Remove every local tag for one UNAXIS-owned repository. |
| `--yes` | boolean | Apply an image cleanup instead of showing a dry run. |

## `unaxis env list`

List environment mappings and domains.

| Option | Type | Description |
|---|---|---|
| `--json` | boolean | Output as structured JSON. |

## `unaxis env security`

Inspect container security posture (privileged, capabilities, user, mounts).

Arguments: `envName` (optional)

| Option | Type | Description |
|---|---|---|
| `--json` | boolean | Output as structured JSON. |

## `unaxis events`

Subscribe to an event stream of TUI actions.

| Option | Type | Description |
|---|---|---|
| `--watch` | boolean | Keep connection open and stream JSON events. |

## `unaxis forge`

Self-hosted git forge (Forgejo): place it on any UNAXIS host, deploy it through that host's agent, and back it up to several places.

Subcommands: `status`, `place`, `set`, `deploy`, `backup`, `backup-target`

Arguments: `target` (optional), `path` (optional)

| Option | Type | Description |
|---|---|---|
| `--root-url` | string | place/set: public URL override (default http://<tailnet-or-LAN-ip>:<http-port>/). |
| `--http-port` | number | place/set: host port for the web UI (default 3300). |
| `--ssh-port` | number | place/set: host port for git over SSH (default 2222). |
| `--image` | string | set: Forgejo image to run on the next deploy. |
| `--keep-in-volume` | number | set: dumps kept inside the forge's volume (default 7). |
| `--keep-per-dir` | number | set: dumps kept in each backup directory (default 14). |

## `unaxis host`

Inspect host resources, or diagnose Docker Desktop WSL VHD path and ownership guardrails.

Subcommands: `doctor`

| Option | Type | Description |
|---|---|---|
| `--json` | boolean | Output as structured JSON. |

## `unaxis media`

Media topology: which UNAXIS host runs which media role (origin, edge, turn, ingress, camera-receiver), port-forward checks, viewer capacity, and config generated from it.

Subcommands: `topology`, `facts`, `place`, `unplace`, `gateway`, `render`, `apply`, `edge`, `seed`

Arguments: `target` (optional), `detail` (optional)

| Option | Type | Description |
|---|---|---|
| `--json` | boolean | topology: output as JSON. |
| `--discover` | boolean | facts: read addresses/cores/load from the host's agent. |
| `--lan-ip` | string | facts: host LAN address. |
| `--tailnet-ip` | string | facts: host tailnet address. |
| `--public-ip` | string | facts/gateway: public address. |
| `--uplink` | number | facts: measured upload of the host's internet connection, Mbps. |
| `--gateway` | string | facts: home-router gateway key the host sits behind, or 'none'. |
| `--primary` | boolean | place media-edge: serve the public HLS path. |
| `--public-whep` | boolean | place media-edge: also answer public WebRTC. |
| `--key` | string | place: custom placement key. |
| `--config` | string | place: role config overrides as JSON. |
| `--forwards` | string | gateway: the router's port-forwards as a JSON array. |
| `--dry-run` | boolean | apply: show drift without writing. |

## `unaxis notify`

Push a notification into the running TUI from outside. Appears immediately in the notifications pane.

Arguments: `message`

| Option | Type | Description |
|---|---|---|
| `--type` | string | Notification type: success \| error \| info  (default: info) |
| `--priority` | string | Queue priority: low \| medium \| high \| immediate  (default: medium) |
| `--timeout` | number | Display duration in ms. Defaults to type default (success=5s, error=8s, info=3s). |
| `--key` | string | Dedup key — same-key calls update the existing notification instead of stacking. |

## `unaxis project clone`

A new workspace: clone the project from its remote into <home>/unaxis/workspaces/<slug> (or --to) and register it. The first workspace becomes the active one on this machine.

Arguments: `slug`

| Option | Type | Description |
|---|---|---|
| `--to` | string | Folder to clone into (default <home>/unaxis/workspaces/<slug>; UNAXIS_WORKSPACES_ROOT overrides the base). |
| `--branch` | string | Branch to check out (default: the project's). |
| `--bg` | boolean | Run as a background stack op. |

## `unaxis project forget`

Drop a workspace record. --delete also removes its folder, only if the checkout has no uncommitted changes. The active workspace can't be forgotten.

Arguments: `slug`, `workspaceId`

| Option | Type | Description |
|---|---|---|
| `--delete` | boolean | Also delete the folder (clean checkouts only). |

## `unaxis project set`

Where a project's code lives: its git remote (the forge) and default branch. A project is a record, not a folder.

Arguments: `slug`

| Option | Type | Description |
|---|---|---|
| `--remote` | string | Git remote URL (ssh://… or https://…). |
| `--branch` | string | Default branch (default: main). |

## `unaxis project studio`

Toggle public access to core Supabase Studio via the NPM proxy (studio.example.com).

Arguments: `action` (optional)

## `unaxis project use`

Work in this checkout of the project on this machine (see project workspaces for ids).

Arguments: `slug`, `workspaceId`

## `unaxis proxy`

Manage the local Nginx Proxy Manager instance.

Subcommands: `status`, `restart`, `build`, `push`, `reset`

| Option | Type | Description |
|---|---|---|
| `--bg` | boolean | Run operation in background. |
| `--json` | boolean | Output output/task status as JSON. |

## `unaxis recreate-core`

Force-recreate one root docker-compose.yml service (auth, app, db, kong, rest, realtime, storage, meta, studio, proxy) so it picks up the current .env. `restart` / `env restart <container>` only stop+start the existing container and keep whatever env it was created with — this is the one that actually re-reads .env. Runs `docker compose up -d --force-recreate --no-deps <service>`; --no-deps keeps it scoped to just that one service.

Arguments: `service`

## `unaxis secrets`

Secrets manager (self-hosted Infisical): per-project, per-environment secrets with per-person and per-agent access. Placed on any UNAXIS host; its database is dumped before every backup. `link [<project>] <vaultProjectId>` ties a UNAXIS project to its vault project and writes .infisical.json into its repo; `open [<project>]` opens that project's vault in the browser. Dev mode on any device reads the vault through the person's own `infisical login`, falling back to .env.

Subcommands: `status`, `place`, `deploy`, `link`, `open`, `connect`, `check`, `pull`, `use-for-builds`, `dump`

Arguments: `target` (optional)

| Option | Type | Description |
|---|---|---|
| `--environment` | string | connect/check/pull: Infisical environment slug (default prod). |
| `--out` | string | pull: file to write (default .env.from-secrets; .env itself is backed up first). |
| `--http-port` | number | place: host port for the web UI (default 8222). |
| `--site-url` | string | place: public URL override (default http://<tailnet-or-LAN-ip>:<port>). |
| `--bg` | boolean | deploy: run as a background stack op. |

## `unaxis session`

Get the current TUI and project state.

| Option | Type | Description |
|---|---|---|
| `--json` | boolean | Output as structured JSON. |

## `unaxis snap`

Capture the current live TUI frame, or record a timed frame sequence.

| Option | Type | Description |
|---|---|---|
| `--save` | boolean | Write the single-frame snapshot to .snapshots/. |
| `--json` | boolean | Output the single-frame snapshot as structured JSON. |
| `--label` | string | Label used for saved snapshot or frame-series directories. |
| `--series` | boolean | Record repeated live TUI frames into a frame-series folder. |
| `--every` | number | Frame-series sample interval in milliseconds. Default: 100. |
| `--duration` | number | Frame-series recording duration in milliseconds. Default: 4000. |
| `--arm-startup` | boolean | Arm the next TUI boot to record the startup splash as a frame series. |

## `unaxis snap-view`

View a recorded frame series: manifest stats, sample timeline, and inline film strip of unique frames. Standalone fast-path — no TUI or IPC required. Defaults to logs/startup-series-latest.json.

Arguments: `manifestOrDir` (optional)

| Option | Type | Description |
|---|---|---|
| `--summary` | boolean | Only print manifest stats and frame timeline. |
| `--strip` | boolean | Print unique frames inline as a compact film strip. Default unless --summary. |
| `--all-samples` | boolean | Include repeat samples as timing rows. Default. |
| `--unique-only` | boolean | Omit repeat samples from the timeline. |
| `--max-frames` | number | Limit inline unique frames. Default: all unique frames. |

## `unaxis stack`

Get the current background operations stack, or `stack clear` to remove finished ops.

Subcommands: `clear`

Arguments: `opId` (optional)

| Option | Type | Description |
|---|---|---|
| `--json` | boolean | Output as structured JSON. |
| `--failed` | boolean | With `clear`: remove only failed ops. |

## `unaxis stacks`

Show all background stack ops and a tail of each one's output.

| Option | Type | Description |
|---|---|---|
| `--tail` | number | Lines of output to show per op (default 6). |

## `unaxis up`

Cold-start the platform: bring the core compose stack (db, kong, auth, app, proxy…) up, wait for db+kong health, then hydrate the control DB from project.db. Idempotent — THE command to run after a reboot or when everything is down.

| Option | Type | Description |
|---|---|---|
| `--no-hydrate` | boolean | Only start containers; skip the control-DB hydration step. |

## `unaxis zone`

Manage lifecycle and public footer tags for individual zones.

Arguments: `zoneName`, `action` (optional)

| Option | Type | Description |
|---|---|---|
| `--bg` | boolean | Run operation in background. |
| `--ref` | string | build/rebuild/move <env>: move deploys the zone on another host, then removes the old container; build this exact forge branch, tag or commit from a clean checkout instead of the dev drive. |
| `--json` | boolean | Output output/task status as JSON. |

## `unaxis zones`

List all zones managed by the control plane, including public footer tag state.

| Option | Type | Description |
|---|---|---|
| `--json` | boolean | Output as structured JSON. |

