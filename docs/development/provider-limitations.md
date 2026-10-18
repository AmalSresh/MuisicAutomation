# Provider feasibility and security

- Apple Music API handles catalog/library requests; it is not a remote transport API for Apple's Windows client. MusicKit JavaScript renders Apple audio. Prototype WebView2 authorization persistence, DRM, autoplay, cold start, and resume before claiming unattended support.
- Spotify first controls an explicitly selected available Spotify Connect target, normally this PC's installed client. The Web API does not render audio. Embedded Web Playback SDK is optional and gated.
- Use Spotify Authorization Code with PKCE and state validation through the system browser, approved redirect URIs, minimal scopes, and protected refresh tokens. Never request provider passwords.
- Use MusicKit authorization and developer tokens; keep Apple private keys outside Git and the renderer. Local signing may use the developer's own credentials. No shared token service is required.
- Provider notes were checked for PRD v0.4 on 2026-10-11: Spotify development mode has five allowlisted users and Premium requirements; multi-service integration is policy-restricted. Noncommercial/open-source use is not an exemption. Recheck official rules when touching these assumptions; do not bypass quotas, DRM, authorization, or provider policy through UI automation.
- Record unresolved capability/permission questions. Continue mock-based engine/UI work when a live provider mode is blocked; do not claim the blocked integration is validated.
- Store credentials with Windows protected storage, not SQLite plaintext or frontend local storage. Redact logs, bridge responses, exports, and errors.
- Observe only selected app identity/session data. For P1 browser matching, use hostname/path only; discard query strings and do not record page contents, keys, or credentials.
- Validate provider URLs, rule schemas, action types, counts, and bounds. No arbitrary executable actions in imported rules.
- History stays local, defaults to 30-day retention, supports deletion and explicit diagnostic export. No listening analytics or telemetry derived from Spotify content.
- Unlink deletes provider personal data and credentials, retains generic rule names/triggers/conditions/action settings, clears affected content references, and disables dependent rules.
- Use specific errors and next actions. If cold start always needs a click, label the mode assisted playback. Disable unsupported actions; never silently change Windows master volume.
- Support keyboard navigation, screen readers, high contrast, and 200% scaling. Embedded streaming must display required provider attribution, artwork, and metadata.

## Primary references

Use official documentation for current API behavior and policy. Links are references, not permission to change the stack.

- Apple MusicKit and Apple Music API: https://developer.apple.com/musickit/
- Spotify Player API: https://developer.spotify.com/documentation/web-api/reference/start-a-users-playback
- Spotify PKCE: https://developer.spotify.com/documentation/web-api/tutorials/code-pkce-flow
- Spotify SDK: https://developer.spotify.com/documentation/web-playback-sdk
- Spotify quotas: https://developer.spotify.com/documentation/web-api/concepts/quota-modes
- Spotify policy: https://developer.spotify.com/policy
- FlaUI: https://github.com/FlaUI/FlaUI
- WebView2 bridge: https://learn.microsoft.com/en-us/microsoft-edge/webview2/how-to/communicate-btwn-web-native
- Power notifications: https://learn.microsoft.com/en-us/windows/win32/power/wm-powerbroadcast
- Session events: https://learn.microsoft.com/en-us/windows/win32/api/wtsapi32/nf-wtsapi32-wtsregistersessionnotification
- Process events: https://learn.microsoft.com/en-us/previous-versions/windows/desktop/krnlprov/win32-processstarttrace
- Media sessions: https://learn.microsoft.com/en-us/uwp/api/windows.media.control.globalsystemmediatransportcontrolssessionmanager
