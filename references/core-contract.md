# Core Contract

Use this file as the required execution contract for intent alignment.

## Required Objects
Use these objects in the alignment hub and phase loop.

```yaml
intent_snapshot:
  user_goal: string
  non_goals: [string]
  constraints: [string]
  acceptance_criteria: [string]
  priorities: [string]
  assumptions: [string]

intent_lint:
  ambiguity_score: 0.0
  critical_ambiguities: [string]
  warnings: [string]

intent_delta:
  reason: string
  changed_fields: [goal|constraints|acceptance_criteria|priorities|scope]
  impact: {phases_affected: [string], repos_affected: [string]}
  requires_replan: true

phase_gate:
  phase: string
  status: blocked|ready|in_progress|verify|done
  blocker_type: none|ambiguity|dependency|auth|risk

verification_evidence:
  phase: string
  artifacts: [string]
  checks_run: [string]
  result: pass|fail|partial
  notes: string

capability_matrix:
  required: [string]
  available: [string]
  missing: [string]
  adapters_selected: [string]
```

## Intent Quality Gate
Run before planning.

1. Build `intent_snapshot`.
2. Run `intent_lint`.
3. Classify ambiguities:
- critical: blocks phase planning.
- major: allows planning but blocks execution.
- minor: allow execution and track in hub.
4. If critical ambiguity exists, ask targeted questions before proceeding.

## Ambiguity Classes
- Missing acceptance criteria.
- Conflicting constraints.
- Undefined scope boundaries.
- Unclear priority tradeoffs.
- Missing environment/tool access assumptions.

## Clarification Question Rules
- Ask 1-3 high-impact questions.
- Ask questions in decision-ready form (pick A vs B, define threshold, set priority).
- Propose a default when confidence is high enough; request explicit override.

## Pre-Execution Clarification Gate
Run before each phase starts.

1. Re-run lint on latest intent state.
2. Check new blockers (including auth/capability blockers).
3. If blocked, request clarification or authorization path.
4. Resume only when phase gate is `ready`.

## Capability Binding Rules
- Match required capabilities to available adapters.
- If a capability is missing, switch to degraded mode and notify the user.
- Never fabricate unavailable tool access.
