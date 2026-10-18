# Frontend agent instructions

Scope: frontend/ and descendants. Read ../AGENTS.md first. Paths below are relative to this directory.

## Read before changes

- ../docs/product/PRD.md and relevant ../docs/product/user-stories.md entries.
- ../docs/design/README.md and ../docs/design/design-spec.md; relevant approved screens/specifications.
- ../docs/architecture/worker-protocol.md for bridge work.

## Libraries and ownership

Use React, TypeScript, Vite and Tailwind CSS. Baseline tests: Vitest and React Testing Library. Inspect actual package.json and lockfile before installation or checks; use existing versions and scripts. Do not add another frontend framework or state/UI library without a task-specific need and root-scope compliance.

Own the rule editor, connections, settings and history. Send typed commands through the WebView2 bridge; C# owns rules, persistence, OS events and worker orchestration. Do not implement a second rule engine, directly spawn processes, call FlaUI, or put Python behind an incidental HTTP server.

## Design and interaction

- Reuse actual shared tokens in src/styles/tokens.css and existing components when present. Do not invent a brand palette, logo, or approved layout.
- Use original brand SVG assets in src/assets/brand/ when supplied. Missing references must be recorded, not presented as approved design choices.
- Show When / Only if / Then clearly; validate grouped conditions, target, content, volume and duration. Keep templates disabled until explicitly enabled.
- Separate automation pause from playback pause. Show pause scope, expiry, readiness, unsupported controls and actionable errors.
- Follow root security rules: no long-lived credentials in frontend storage, logs, exports, or renderer config. Only approved MusicKit playback authorization data may enter its required SDK context.
- MusicKit playback uses JavaScript; browser rendering alone does not prove WebView2 DRM/autoplay compatibility.
- Support keyboard navigation, labels, screen readers, high contrast, focus states and 200% scaling.

## Verification

Use fake bridge/provider responses by default. Test user-visible validation and state transitions. Run applicable lint/type/build/tests from verified scripts. Compare the rendered interface to supplied approved references at the specified window size. Report unavailable references or Windows playback validation honestly.
