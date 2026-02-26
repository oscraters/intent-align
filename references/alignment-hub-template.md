# Alignment Hub Schema
Use this as the central state file (`alignment-hub.md`).

```yaml
meta:
  project: string
  created_at: iso-8601
  updated_at: iso-8601
  owner: string

intent_snapshot:
  user_goal: string
  non_goals: [string]
  constraints: [string]
  acceptance_criteria: [string]
  priorities: [string]
  assumptions: [string]
  spec_confidence: 0.0

intent_lint:
  ambiguity_score: 0.0
  critical_ambiguities: [string]
  major_ambiguities: [string]
  minor_ambiguities: [string]
  ambiguities_open: [string]
  clarifications_needed_by: iso-8601
  blocked_by_clarification: false

autonomy:
  level: 2
  override_on_critical_ambiguity: true

capability_matrix:
  required: [string]
  available: [string]
  missing: [string]
  adapters_selected: [string]

repos:
  - name: string
    path: string
    deps: [string]
    adapter_bindings: [string]

phases:
  - id: P1
    name: string
    deps: [P0]
    owner: string
    status: blocked|ready|in_progress|verify|done
    acceptance_checks: [string]
    verification_evidence: [string]
    drift_score: 0.0
    blockers: [string]

status:
  current_phase: string
  overall_drift_score: 0.0
  risk_level: low|medium|high
  last_sync: iso-8601
  next_user_checkin: iso-8601

tracking:
  source_of_truth: local_hub|github|tracker
  external_refs: [string]

decision_log:
  - at: iso-8601
    decision: string
    rationale: string

change_log:
  - at: iso-8601
    intent_delta_summary: string
    phases_impacted: [string]
```

Keep this schema compact; add optional fields only when tied to a concrete task need.
