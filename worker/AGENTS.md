# Python worker agent instructions

Scope: worker/ and descendants. Read ../AGENTS.md first. Paths below are relative to this directory.

## Read before changes

- ../docs/architecture/worker-protocol.md and overview.md.
- Relevant ../docs/product/PRD.md requirements and user stories.
- ../docs/development/provider-limitations.md and testing.md.

## Approved libraries and boundaries

Use Python, HTTPX and standard-library JSON in a project virtual environment. Baseline tests: pytest with mocked HTTP. Inspect pyproject.toml and existing pins first. Additional signing/credential libraries require a necessary assigned use case; document and pin them rather than implementing cryptography by hand.

Own provider web requests, authorization support, refresh and optional local Apple developer-token signing. Do not own the rule engine, Windows triggers, FlaUI, UI, or SQLite writes. Do not add FastAPI or another worker HTTP server; stdin/stdout JSON is the established internal protocol. A narrowly bound provider-approved OAuth callback listener is a separate allowed integration need.

## Protocol and provider safety

- stdout contains newline-delimited protocol JSON only; diagnostics go to redacted stderr.
- Validate operations and payload bounds; correlate responses by request ID. Respect deadlines, cancellation, quota signals and Retry-After.
- Distinguish authentication, unavailable target, permission, quota, transient and ambiguous mutation errors. Do not blindly retry a timed-out playback command.
- C# supervises the worker. Coordinate recovery rather than silently starting independent background workers.
- Keep private keys and long-lived tokens in protected storage outside Git, examples, logs and renderer messages.
- Apple Music API requests do not render audio; MusicKit JavaScript handles playback. Spotify remote control requires an available explicitly selected target.
- Provider policy notes are dated. Verify current official documentation for integration changes; do not bypass provider restrictions using account rotation or UI automation.

## Verification

Test framing, errors, malformed input, cancellation, refresh, revoked credentials, rate limiting and ambiguous responses using mocks. Keep tests offline by default; do not unlink real accounts or mutate real library data. Record actual Python commands and the environment used.
