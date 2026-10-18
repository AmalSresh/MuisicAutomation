# Local development setup

## Status

This package contains instructions and references, not a scaffolded application. Application projects, manifests, dependency pins, and launch scripts are not included. Do not run guessed commands or create the whole app merely to fill this guide.

## Required setup documentation when code exists

- Actual supported Windows, .NET SDK, Node/npm, Python, and WebView2 versions.
- Frontend dependency installation and build commands from package.json and lockfile.
- Desktop solution restore/build/run commands from the actual solution location.
- Python virtual environment and dependency setup from pyproject.toml and dependency pins.
- One documented desktop entry point that supervises its worker.
- Placeholder configuration examples, provider developer prerequisites and linking instructions.
- Runtime data location: `%LOCALAPPDATA%/MusicAutomator`; no app account required.
- Troubleshooting for missing player targets, required interaction, and worker failure.

Keep credentials, databases, logs, virtual environments and build outputs out of Git. The owner must choose the repository license; none is selected by this package.
