# User profiles and acceptance stories

Read alongside [PRD.md](PRD.md). FR priorities in the PRD govern implementation order; personas do not authorize deferred work.



- **Mark, 17, twelfth-grade student:** study playlist on his math Canvas page; chosen collection shuffled for Valorant/Counter-Strike; stop on activity exit; no automated music during GTA. Preserve this persona as a use case, not evidence of provider eligibility.
- **Claire, 20, college student:** Apple Music after sign-in, pause on sleep, resume the same session after wake and unlock.
- **Thomas/Tom, 23, software engineer:** create and test custom listening rules using a clear When / Only if / Then editor.

| Story | Acceptance contract |
| --- | --- |
| US01 Connect and use templates | Show compatible templates; require content/target completion and explicit enablement. |
| US02 Choose music for triggers | Support explicit content and readable preview; never silently replace content/target. |
| US03 Volume and duration | Labeled player-volume control, minutes or Until stopped; timer starts after verified playback. |
| US04 Unlink while keeping rules | Delete credentials/provider personal data; keep generic structure, use Account required placeholders; reselect content and enable after reconnect. |
| US05 Temporarily pause | Preset/custom/indefinite durations, visible scope/expiry, resume action; cancel pending work and discard paused-period events. |
| US06 Natural-language rules | P2 only; validate a draft, ask about missing details, review before enabling. |
| US07 Canvas study routine | Match browser/hostname/course path; one start per entry with cooldown; last browser window closing pauses owned playback. Navigation away stops only if configured. |
| US08 Competitive games | Match actual executable; first instance starts, last exit stops; resolve collection and verify shuffle. |
| US09 Story-game exclusion | Overrides every automated start/resume; pauses app-owned music; clears without replay on game exit. |
| US10 Computer lifecycle | Start once when ready; resume only previously playing app-owned session, subject to manual pause/exclusion/duration. |
| US11 Custom rule editor | Grouped conditions, ordered actions, local validation, explain each test result. |

“Regular library” and “music type” must resolve to supported, explicitly selected content. Do not assume a provider can play an entire saved library as a single context.
