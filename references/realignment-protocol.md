# Realignment Protocol

Use this protocol whenever intent may have changed or drift is detected.

## Triggers
- User message changes goals, constraints, priorities, or scope.
- Drift score crosses threshold in the hub.
- Verification fails against acceptance criteria.
- New dependency or auth blocker changes execution path.

## Procedure
1. Capture change candidate and classify it.
2. Build `intent_delta`.
3. Identify impacted phases/repos only.
4. Re-plan only impacted phases.
5. Preserve completed unaffected phases unless user requests rollback.
6. Ask for confirmation if change affects acceptance criteria or hard constraints.
7. Update hub logs and next check-in time.

## Clarification Loop
When ambiguity remains:
1. Ask targeted clarification questions.
2. Offer a recommended default.
3. Record answer as structured update in `intent_snapshot`.
4. Recompute drift and blockers.

If the user does not answer and autonomy permits progress:
- continue only on low-risk, reversible tasks.
- keep blocked phases paused.

## Check-in Cadence
- Strict: before each phase start.
- Balanced: phase end and on major drift.
- Aggressive: major drift only.
- Exploratory: periodic summaries; block only on critical ambiguity/risk.
