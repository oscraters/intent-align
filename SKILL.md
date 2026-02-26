---
name: intent-align
description: Traycer-inspired orchestrator for aligned agent swarms: intent → MVP spec/phases/Mermaid → spawn subagents (parallel/multi-repo/non-git) → check-ins/steer → verify/refactor. Adaptive: git/gh/canvas/kanban/SaaS tracking, 4 autonomy levels (strict/YOLO). Use when: (1) Coding/PRs/issues/monorepos/teams, (2) Prototypes/files/APIs, (3) Phased tasks needing vision lock/anti-drift, (4) Flexible workflows (user prefs via memory_search).
---

# Intent-Align: Traycer-Style Swarm Orchestrator

Anti-drift for OpenClaw: Keeps subagents locked to user vision w/ flexibility.

## Quick Start
User: \"Align swarm: Build MVP todo app w/ API.\"  
1. Gen spec/phases (canvas Mermaid).  
2. Setup hub (refs/alignment-hub-template.md).  
3. Spawn/check/verify.

## Core Workflow (Imperative)
1. **Intent → Spec**: LLM → phases/files/Mermaid (canvas present assets/mermaid-spec-template.md). Write `plans/${project}-spec.md`. memory_search \"user vision/prefs\".
2. **Hub Setup**: read refs/alignment-hub-template.md → edit {spec, autonomy:2, tracking:gh}. write temp/${project}/alignment-hub.md.
3. **Autonomy Levels** (config in hub; periodic message check):  
   - 1 Strict: Check every phase (block spawn).  
   - 2 Balanced: Phase-end check-in.  
   - 3 Aggressive: Auto-verify + minor refactor.  
   - 4 Wild: Log-only.  
   Prompt spawns: \"Autonomy ${level}: ${rules}. No drift from spec.\"
4. **Swarm Spawn**: sessions_spawn per phase/repo (parallel loop, thread=true, label=team-phase). Pass: spec + hub + memory_search.
5. **Loop (heartbeat/subagents list)**:  
   - Poll status.  
   - Cross-sync: sessions_send peers via hub.deps.  
   - Check-in: message \"Phase X: Aligned? Tweaks? Level?\" → steer/kill/update hub.  
   - Verify: coding-agent diffs/tests; gh-issues PRs; canvas eval.
6. **Close**: Aggregate hub → MEMORY.md update; cleanup temp/.

## Adaptive Tracking (User Prefs)
- memory_search \"track in [gh/obsidian/trello]\" → gh-issues/browser/obsidian.  
- Canvas Mermaid kanban: phases|agents|status.  
- SaaS: browser act (login/create).

## Edge Cases
**Multi-Repo Parallel**: repos=[fe,be]; mkdir temp/swarm-hub/. Parallel sessions_spawn workdir=temp/${repo}. Cross-hub deps sync (sessions_send).  
**Non-Git Proto**: Skip git; file ops + canvas mocks.  
**Teams**: Labels=frontend-team; gh assignee.  

Read refs/alignment-hub-template.md for schema. assets/ for templates.  
Publish via clawhub when refined.