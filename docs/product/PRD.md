# Product requirements

Source baseline: Desktop Music Automation PRD v0.4 and its consolidated agent contract. This split changes organization, not feature scope. Requirement IDs remain stable.

## Purpose and scope

Build a Windows 11 x64 desktop hobby application that automates music according to local computer activity. Source lives in an open GitHub repository; friends clone, configure, and run it locally. There is no planned monetization, public packaged launch, or hosted consumer service.

Core flow: connect provider → select template or trigger → configure conditions and content → simulate → explicitly live-test → enable.

No required shared backend or product account. Keep rules and execution history local. Run in the interactive user's session as a tray application, not a Session 0 service. Closing the main window keeps the engine running; exiting stops detection, embedded playback, and the app-owned Python worker. Remote provider playback may continue.

### Out of scope unless explicitly requested

macOS/Linux, mobile control, cloud synchronization, public installers, automatic updates, payments, arbitrary scripts, elevated automation, voice control, alarms, playlist migration, audio downloads, mixing/crossfading, and event-synchronized game soundtracks. Do not add analytics, an AI service, a browser extension, or a general automation platform as incidental dependencies.

P0 = local prototype requirement. P1 = deferred until core validation or explicit request. P2 = future feature. These priorities do not establish provider permission or technical feasibility.

Authentication is limited to linking music providers. Do not introduce application registration or login. Windows user profiles separate local data. Store runtime rules under `%LOCALAPPDATA%/MusicAutomator`, outside the source repository; credentials require Windows-protected storage.

## Functional requirements

| ID | Priority | Required behavior |
| --- | --- | --- |
| FR01 | P0 | Connect/unlink Apple Music or Spotify; show authorization and playback readiness. |
| FR02 | P0 | Browse available playlists or validate provider URLs; select provider, content, target. |
| FR03 | P0 | Create, edit, duplicate, delete, enable/disable rules; offer disabled starter templates. |
| FR04 | P0 | Sign-in, wake, process start/exit, and manual-run triggers. |
| FR05 | P0 | Time window, weekday, unlocked session, app running, network/player state conditions. |
| FR06 | P0 | Play, resume, pause, delay, shuffle, player volume, duration where supported. |
| FR07 | P0 | Local persistence, tray operation, opt-in sign-in launch, global automation pause. |
| FR08 | P0 | Simulation, explicitly authorized live test, history, actionable failures. |
| FR09 | P1 | Schedules, device connection, foreground app changes, repeat. |
| FR10 | P1 | Versioned secret-free import/export; reviewed additional adapters. |
| FR11 | P1 | Match configured browser hostname/path and trigger on page entry. |
| FR12 | P0 | Sign-in/sleep/wake templates with readiness and continuity checks. |
| FR13 | P0 | Stop on paired activity exit; explicit game exclusions. |
| FR14 | P0 | Intuitive optional maximum duration and volume controls. |
| FR15 | P0 | Preserve generic custom rules on unlink; disable unresolved provider actions. |
| FR16 | P0 | Pause one rule or all rules with expiry from tray and app window. |
| FR17 | P2 | Natural-language description → validated draft → explicit user enablement. |



## Rule engine invariants

- Store ID, schema version, name, enabled state, one trigger, recursive ALL/ANY/NOT condition tree, ordered actions, provider/target references, priority, cooldown, expiry, and error policy. Show explicit grouping in previews.
- Startup means interactive sign-in after boot, never pre-login audio. Distinguish ordinary sign-in and avoid duplicate startup runs.
- App start fires at zero → one matching instances; exit at last instance closing. Select actual game separately from launcher. Existing processes at engine startup populate state without synthetic start events.
- Browser closure means last selected browser window closes, not process termination: background processes can remain.
- Deduplicate by rule and normalized event. Evaluate → wait for readiness → re-evaluate before playback. Cancel stale pending starts on relevant exit, lock, disable, pause, or exclusion.
- Serialize playback mutations. Highest numeric priority wins; tie by event time then rule ID. Record losing rules as superseded. Exclusions take precedence over numeric priority.
- Never silently transfer playback to another device. Switching providers requires pausing prior app-owned playback and remains permission-gated.
- Track ownership conservatively. Exit/duration actions affect only their unchanged app-owned session. Yield when the user changes content or target; never claim ownership solely because audio is playing.
- Manual pause suppresses automatic resume for 30 minutes by default, configurable. If pause cause cannot be determined, suppress conservatively.
- Maximum duration uses elapsed time from verified playback, including sleep. If expired while asleep, do not resume on wake. Use monotonic time for live delays/cooldowns; persist deadlines for resume reconciliation.
- Resume only playback that was active before sleep and remains eligible. Attempt pause on suspend, but sleep may interrupt API calls; reconcile on wake rather than guaranteeing an unverified remote pause.
- Temporary automation pause does not itself pause audio. Offer separate playback control; never replay triggers received during pause.
- States: Received, Waiting, Evaluating, Executing; terminal Succeeded, Skipped, Cancelled, Failed, Needs interaction. Verify playback within 10 seconds where supported; label unverified outcomes explicitly.
- Defaults: 60-second readiness expiry; at most three transient retries within expiry; honor Retry-After and quota errors. Refresh expired token once; reconnect revoked authorization. Never blindly retry ambiguous playback mutations.

## Delivery sequence



1. Feasibility prototypes: supported target matrix and documented proceed/revise/stop decisions.
2. Local engine/UI alpha with mock player and cancellation/conflict tests.
3. Authorized provider testing, including ordinary sleep, hibernate, and Modern Standby where available.
4. Reproducible friend setup: README, example configuration, gitignore, lockfiles, license decision, and fresh-clone validation.

Do not invent deadlines or broaden to P1/P2 while completing an assigned milestone.

## Related references

- [Personas and acceptance stories](user-stories.md)
- [Architecture and approved stack](../architecture/overview.md)
- [Provider limitations and security](../development/provider-limitations.md)
- [Validation targets](../development/testing.md)
- [Visual design index](../design/README.md)
