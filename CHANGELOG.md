# Changelog

Current version: 0.0.88 (`npm install -g @untsystems/unaxis`).

## 2026-10-20

- Fixed: the launcher no longer kills the session it starts
- The agent and its updater live here; a host runs it standalone
- Fixed: autostart and bun run dev work from the UNAXIS repo

## 2026-10-16

- The TUI shows and drives Postgres's live copy
- Production Postgres gets a live copy on another machine
- Fixed: project forget --delete removes Windows-drive checkouts from the WSL TUI
- A folder is a project by its own files, not by containing UNAXIS
- Plain builds, scaffolding and the changelog follow the workspace you edit
- Fixed: dev mode works from the WSL TUI again, and runs from the checkout you edit

## 2026-10-14

- A project is a record, a workspace is a checkout from the forge
- A vault per UNAXIS project, opened from UNAXIS, used by dev mode anywhere
- Infisical sends mail through the site's SMTP
- Fixed: a port that never answers the connect is dead, not healthy
- Chaos drills for dead ports and a killed TUI
- Fixed: repair dead published ports, and never leave the TUI down

## 2026-10-05

- Fixed: backups failed since the TUI moved to WSL

## 2026-10-04

- Fixed: don't delete proxy routes for a host Docker can't answer for

## 2026-10-02

- Move a zone to another host — `zone <key> move <env>`

## 2026-10-01

- Fixed: --ref builds failed when the TUI runs in WSL
- A changelog per zone, plus core, unaxis and services — `unaxis changelog`
- Fixed: release waits for npm to serve the new version before auto-updating
- Fixed: nightly backup also backs up the forge
- Bare-metal dev mode for every zone; NPM location follows the topology

## 2026-09-30

- Fixed: secrets manager starts in shadow mode — builds keep using .env
- Builds read secrets from Infisical; retire the workspace overlay
- Self-hosted secrets manager (Infisical) as a placed role — `unaxis secrets`
- Fixed: one backup at a time — manual and nightly share a run lock
- Build zones from a forge commit — `zone <key> build --ref <ref>`
- Workspace backups with restic — `unaxis backup`
- Fixed: startup self-heal recreated the whole core stack
- [w] in Zones syncs the workspace overlay (.env + secrets → forge)
- Fixed: read build provenance with an async git call
- Fixed: images tagged gnogit — git log hung on the fsmonitor daemon
- Every zone build publishes its exact source to the forge
- Fixed: workspace overlay skips nested repos, warns on dropped files; project rules
- Workspace overlay — ignored files versioned on the forge only
- Self-hosted git forge (Forgejo) as a placed role

## 2026-09-28

- Media topology — media roles placed on any UNAXIS host

## 2026-09-08

- TUI, zone build and Stripe lane updates

## 2026-08-20

- Let a zone be given host storage

## 2026-07-13

- Add UNAXIS docs overnight runner orchestration

## 2026-06-20

- Add ZoneProvider and MovedHereToast components for zone context management

## 2026-05-31

- Update WelcomeScreen menu description and add release workflow documentation

## 2026-05-25

- Add ProjectPickerScreen for project selection and pairing key generation
- Add Docker volumes management view and create volume functionality

## 2026-05-19

- Implement Ink-based TUI framework, agent infrastructure, and environment management dashboard
- Implement Ink-based TUI for environment, infrastructure, and stack management with agent integration

## 2026-05-17

- Scaffold multi-zone architecture, TUI management system, and dashboard form/settings modules

## 2026-05-15

- Implement Ink-based TUI core runtime with multi-zone Supabase orchestration and dashboard features

## 2026-05-13

- Scaffold Ink-based TUI application structure and zone management system

## 2026-05-08

- Implement TUI core, terminal integration, and browser utilities for project management
- Implement Ink-based TUI for multi-zone orchestration, container management, and web proxy configuration

## 2026-04-20

- Implement multi-zone architecture and custom Ink-based terminal UI framework

