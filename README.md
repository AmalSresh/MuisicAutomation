# Music Automator agent and reference kit

This package restructures the existing consolidated AGENTS.md into scoped instructions and shared references. It contains no application source, mockups, credentials or working build scripts.

## Applying it

Extract this ZIP into a staging directory and review its files before copying them into your repository. Merge existing files individually; do not blindly overwrite existing instructions or local changes. Place the root AGENTS.md at the repository root and preserve the relative directory structure. Use the conventional uppercase filename AGENTS.md.

The original consolidated source remains unchanged as a historical artifact. Once this structure is adopted, the Markdown PRD and its linked references are the maintained product source; do not keep a second competing consolidated instruction file active.

## Navigation

- [Repository rules](AGENTS.md)
- [Frontend rules](frontend/AGENTS.md)
- [Desktop rules](desktop/AGENTS.md)
- [Worker rules](worker/AGENTS.md)
- [Documentation rules](docs/AGENTS.md)
- [Script rules](scripts/AGENTS.md)
- [Product requirements](docs/product/PRD.md)
- [User stories](docs/product/user-stories.md)
- [Architecture](docs/architecture/overview.md)
- [Protocol](docs/architecture/worker-protocol.md)
- [Design references](docs/design/README.md)
- [Setup](docs/development/setup.md)
- [Testing](docs/development/testing.md)

Agent rules guide supported agents; they do not enforce OS permissions. Shared safeguards live at the root, and component rules add local responsibilities. Agents must explicitly read linked references. Do not add an AGENTS.md to every leaf folder unless that folder needs distinct instructions.
