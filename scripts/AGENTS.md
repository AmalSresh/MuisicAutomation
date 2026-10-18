# Script agent instructions

Scope: scripts/ and descendants. Read ../AGENTS.md first.

- Scripts automate verified setup/build/test tasks only; they must not become a second rule engine or an unrequested deployment pipeline.
- Prefer PowerShell for Windows developer entry points. Reuse verified manifest commands; do not invent dev.ps1 before an actual application entry point exists.
- Quote paths, resolve working directories and validate inputs. Do not interpolate untrusted strings into shell commands.
- Do not add broad recursive deletion, repository resets, automatic privilege elevation, global installs, security-policy changes, secret printing, or download-and-execute patterns.
- Startup registration and live playback/OS tests must be explicit opt-in actions. Never bundle them into ordinary builds or test startup.
- Terminate only verified task-owned processes. Avoid killing processes by name.
- Propagate errors and exit codes. Document prerequisites and effects; provide preview/dry-run behavior for consequential system changes.
- Validate scripts with safe temporary fixtures. Do not execute system-changing code merely to check syntax.
