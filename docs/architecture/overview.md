# Architecture and approved stack

## Component ownership and tools

| Component | Libraries or tools | Owns |
| --- | --- | --- |
| Frontend | React, TypeScript, Vite | Rule editor, settings, connections, history, accessible controls |
| Styling | Tailwind CSS | Layout, themes, reusable UI |
| Desktop host | C#, .NET, WPF, `Microsoft.Web.WebView2` | Window, tray, lifecycle, bridge, worker supervision |
| UI automation | `FlaUI.Core`, `FlaUI.UIA3`; UIA2 only if compatibility requires it | Native UI discovery, control actions, UI-related events |
| System events | Windows APIs, WMI; `System.Management` where needed | Power, session, process lifecycle events |
| Rule engine | C# | Conditions, priorities, cancellation, delays, ownership, execution state |
| Provider worker | Python, HTTPX, standard-library JSON | Web API requests, authorization support, refresh, optional local Apple token signing |
| Persistence | SQLite; `Microsoft.Data.Sqlite` | C# owns database writes; no independent competing worker database |
| Apple audio rendering | MusicKit on the Web / JavaScript | Embedded playback, authorization flow, supported player controls |
| Spotify control | Spotify Web API Player endpoints | Selected local Spotify Connect target first |
| Optional native transport | `GlobalSystemMediaTransportControlsSessionManager` | Controls available from the intended media session |

Testing baseline: Vitest and React Testing Library for UI, xUnit for C# engine tests, pytest for Python worker tests. Use existing repository testing tools if already equivalent; do not introduce duplicate frameworks. Use mocked HTTP responses and isolated temporary storage.

Development tools: Git, `rg`, the .NET SDK, Node/npm, and Python with a project virtual environment. Pin compatible versions in manifests and lockfiles after inspecting the repository. Do not invent version numbers, project paths, or test commands. Document the versions actually verified.

Do not substitute Electron, Tauri, WinUI, a Python GUI framework, FastAPI, AutoHotkey, or Power Automate Desktop without approval for an architecture change. Add a dependency only when necessary for the assigned requirement; use current official documentation and explain its purpose. Use existing utilities first.



## Windows mechanisms



- Sign-in launch: opt-in per-user Task Scheduler registration or packaged `StartupTask`; no duplicate registrations.
- Power: `WM_POWERBROADCAST` and supported notifications; normalize duplicate resume events.
- Session: `WTSRegisterSessionNotification`, scoped to the current interactive user.
- Processes: WMI start/stop trace events, including `Win32_ProcessStartTrace`; reconcile missed state as a standard user.
- FlaUI is not the system wake/process event engine. Prefer automation IDs and supported control patterns to coordinates or global keystrokes. Verify app identity and resulting state.
- Specific browser-page detection is P1: prototype address-bar and window inspection with FlaUI. A browser extension is a possible later proposal, not an approved implementation dependency.

## References

Use the [worker protocol](worker-protocol.md) for message boundaries and [provider limitations](../development/provider-limitations.md) for integration constraints. There is no application account service or required shared backend.
