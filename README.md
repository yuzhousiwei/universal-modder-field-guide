# Universal Modder Field Guide

Independent setup tutorials for the open-source [Universal Modder toolkit](https://github.com/rehan-remade/universal-modder), with prerequisites, installation commands, verification steps, and troubleshooting notes.

Read the complete field guide at **[universalmodder.dev](https://universalmodder.dev/)**.

This repository is maintained by the independent guide author. It is not the official toolkit, a fork of the upstream project, or an endorsement by its maintainers. For releases, tool source code, and contributions to the toolkit, use the upstream repository.

## Tutorials

| Guide | What it covers | Website edition |
|---|---|---|
| [Claude Code setup](docs/claude-code.md) | Prerequisites, plugin installation, the `um` CLI, asset workflows, and setup checks | [Read on the website](https://universalmodder.dev/guides/claude-code/) |
| [Codex setup](docs/codex.md) | Codex plugin commands, the repository-clone alternative, and checks before changing game files | [Read on the website](https://universalmodder.dev/guides/codex/) |

The tutorials are written to be useful when read directly on GitHub. The website adds navigation across game routes, related guides, and upstream case studies.

## Minecraft reference guides

- [Fabric, Forge, and NeoForge compatibility](https://universalmodder.dev/guides/minecraft-mod-loaders/): editions, game versions, loader versions, and Java requirements.
- [A mod that will not load](https://universalmodder.dev/guides/minecraft-mod-not-loading/): follow build and game logs to identify version mismatches, missing dependencies, and resource errors.
- [Copper Token practice walkthrough](https://universalmodder.dev/guides/minecraft-first-mod/): a source exercise targeting Minecraft Java 1.21.1, NeoForge 21.1.252, and JDK 21.

The Copper Token package has passed source and file checks. It has **not** been compiled or verified inside a running game by this guide. It is a source exercise, not a ready-to-install mod.

## Before you start

You need a coding agent and a game you own. Game and loader versions matter. Start with a separate test instance and a backup, and verify one small change before attempting a larger mod.

The upstream toolkit uses Git, Python 3.10+, and ffmpeg. Generated media may require a paid fal account; a local ComfyUI workflow can provide an alternative for some image tasks. Installing a coding-agent plugin does not install your game, its mod loader, or a finished mod.

## Sources and verification

These tutorials adapt the guide site's installation pages and cite the original project instructions. Agent installation and game compatibility are different checks. We do not claim to have installed every supported agent or tested every game and version.

See [Sources and verification](SOURCES.md) for the reviewed snapshot, original documentation, and verification boundaries.

If you report a documentation problem, include the guide name, operating system, agent version, and the relevant error text. Remove credentials and personal paths before sharing logs.
