# Frontend bridge and Python worker protocol

## Established requirements



- React ↔ C#: typed JSON through the WebView2 message bridge. Validate origin, operation allowlist, payload schema, and bounds. Do not expose arbitrary shell or native execution.
- C# ↔ Python: a supervised child process using newline-delimited JSON over redirected stdin/stdout. Reserve stdout for protocol messages; stderr contains redacted diagnostics.
- Requests include request ID, operation, payload, and deadline; responses include the same ID and result or structured error. Support timeout, cancellation, and bounded recovery.
- C# owns orchestration. Python must not implement a second rule engine. Keep worker requests nonblocking for the desktop UI.
- No internal HTTP server is required. A provider-approved OAuth callback listener may still be needed; bind it narrowly and validate the callback.
- After timeout or worker crash, inspect provider state before replaying a playback command.



## Specification status

This is a contract outline, not an implemented wire schema. Exact field names, operation enums, schema version representation, error codes, maximum message size, and cancellation messages remain to be specified when the assigned integration task requires them. Inspect existing code first. Do not invent or claim an implementation already exists.

When implementing a protocol change, document the concrete request/response examples, framing, validation, timeout/cancellation semantics, version compatibility, and error behavior here. Update both sides and add contract tests in the same scoped change. Never place real tokens in examples.
