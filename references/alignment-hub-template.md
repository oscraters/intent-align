# Alignment Hub Schema
Use as central state file (write alignment-hub.md):

```yaml
spec: {mvp_goal, phases: [{name, tasks, files}], mermaid: '...'}
autonomy: {level: 2, lock: false, rules: 'Strict=1/full-checks,...'}
repos: [{name: frontend, path: temp/frontend, deps: []}]
status: {phase: impl, drift_score: 0.1, last_sync: now}
tracking: {type: gh-issues, board_id: 'abc'}
```
memory_search/update on changes. sessions_send peers for cross-sync.