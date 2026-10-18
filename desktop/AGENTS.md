# Desktop agent instructions

Scope: desktop/ and descendants. Read ../AGENTS.md first. Paths below are relative to this directory.

## Read before changes

- ../docs/product/PRD.md, especially rule-engine invariants, and relevant user stories.
- ../docs/architecture/overview.md and worker-protocol.md.
- ../docs/development/testing.md and provider-limitations.md.

## Approved tools and ownership

Use C#, .NET, WPF, Microsoft.Web.WebView2, FlaUI.Core/FlaUI.UIA3, Windows APIs/WMI, System.Management where needed, and Microsoft.Data.Sqlite. UIA2 requires a demonstrated compatibility need. Baseline tests: xUnit. Read existing solution/project files before choosing versions or commands.

C# owns the tray/lifecycle, engine, SQLite writes, native events, cancellation, playback ownership, WebView2 bridge and supervised Python worker. Keep Core engine logic testable without Windows UI objects. Desktop is the host; Windows adapters contain OS/FlaUI integration. Follow existing project boundaries rather than creating speculative projects.

## Implementation invariants

- FlaUI handles native controls and UI events. Use Windows power/session APIs and WMI for wake, lock and process events.
- Use stable automation IDs/control patterns. Confirm the exact app/session and resulting state; avoid coordinates/global keystrokes.
- Run as the interactive standard user. Closing the window preserves the tray engine; Exit shuts down the app-owned worker cleanly.
- Keep UI thread work responsive; bound and cancel adapter/worker operations.
- Preserve all rule timing, conflict, exclusion and ownership semantics in the PRD. Never use audio being active as proof of app ownership.
- C# alone writes the app database. Version migrations and test disposable copies; never reset a real database to fix a schema error.
- Validate WebView2 origin and allowlisted payloads. Do not expose arbitrary native/shell methods.
- Protect credentials using Windows facilities; keep keys out of the renderer and repository.
- Live OS tests require root-specified authorization. Do not alter startup, sleep the PC, close apps, or change music as an incidental test.

## Verification

Test engine behavior with fake clock/events/providers; test bridge/worker contracts and cancellation. Validate WPF/FlaUI/power/DRM on Windows only and record unsupported environments. Run actual .NET build/test commands; do not claim Windows success from portable tests.
