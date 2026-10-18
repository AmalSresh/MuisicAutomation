# Testing and validation

Use existing commands from actual manifests. Baseline: Vitest and React Testing Library for UI, xUnit for C#, pytest for Python. Prefer existing equivalent frameworks over duplication. Use fake providers, disposable databases, and deterministic event/clock inputs.

## Acceptance targets



- Event receipt → evaluation: p95 under 2 seconds, excluding external readiness.
- Eligible playback: at least 95% verified within 10 seconds of readiness/configured delay across 100 controlled runs per supported mode. Report blocked cases separately.
- Zero duplicate starts in 100 replay/resume cycles.
- Idle target: under 1% average CPU over 10 minutes and at most 150 MB private working set without loaded playback view; measure player views separately.
- 24-hour reliability run without crash/rule corruption, covering interruption, wake, and reauthorization. These are targets, not measured claims.
- Validate first/last instance behavior, locked wake/expiry, priority ties, manual pause, missing device, expired/revoked tokens, exclusions, duration across sleep, unlink/reconnect, and worker crash.
- Simulation must cause no live playback or system mutations. Manual integration tests require task-specific authorization and must use intended test targets.
- Windows checks require Windows: on other hosts, run portable tests and explicitly mark WPF/FlaUI/power/DRM checks unavailable. Never infer Windows validation from a web preview.



## Recorded results

No application tests or Windows integration checks have been run as part of this documentation restructure. These targets are not claims of verified support. Record actual commands, environment, results and unavailable checks when implementing a task. Run affected checks; reserve endurance and performance runs for relevant milestones rather than every wording change.
