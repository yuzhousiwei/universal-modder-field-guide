# Install Universal Modder with Claude Code

Universal Modder gives a coding agent a game-modding workflow, inspection tools, and a collection of field notes. This guide takes you from an existing Claude Code installation to a first inspection of a game, with a separate check for the `um` command-line tool.

This is an independent, unofficial guide. We do not maintain Universal Modder or represent Anthropic. The corresponding web edition is the [Claude Code installation guide](https://universalmodder.dev/guides/claude-code/).

**Source review:** October 7, 2026. Universal Modder repository snapshot: `6c02e77d9088ecb1a7d9970572d8ca5387e7cb9e`. Installation commands were checked against the upstream README and Claude Code's official plugin documentation. We did not install this plugin, run its `um` commands, or test it in a game while preparing this guide. Treat the checks below as steps for your own environment, rather than results we have obtained.

## 1. Prepare your workspace

Start with a working Claude Code session and a locally installed game you own. Keep a separate test save and a backup of saves you care about. Put your mod's source in a working directory that is distinct from your game's installed files.

The upstream prerequisites are Git, Python 3.10 or later, and ffmpeg, with uv recommended for Python tooling. Blender is needed for rendering 3D models into sprites. Generated assets are optional; a first mod can use placeholder art.

Check your terminal before installing the toolkit:

```bash
git --version
python --version
uv --version
ffmpeg -version
```

On macOS or Linux, your Python executable may be `python3`. Use whichever interpreter your tools are configured to use, and confirm its version. An installed coding agent on macOS or Linux does not make a Windows game or mod loader compatible; upstream's Windows workflows run natively or through WSL.

For Minecraft Java Edition, identify the exact Minecraft version and loader before selecting a JDK and development template. “Minecraft support” alone does not establish that a particular Fabric, Forge, or NeoForge mod will load in your instance.

## 2. Add the marketplace and install the plugin

Start Claude Code in your mod workspace. Run the following slash commands **inside Claude Code**, rather than in Terminal or PowerShell:

```text
/plugin marketplace add rehan-remade/universal-modder
/plugin install universal-modder@universal-modder
```

The marketplace name and plugin name are both `universal-modder`. The first command adds the source; the second selects the plugin from it.

In current Claude Code, the install command opens the plugin details so you can review its components and choose an installation scope. Follow the panel to complete installation. For a first experiment, local scope confines the enabled setting to the current repository. Read the installation summary: it tells you whether the plugin is active or still needs setup or reloading. Starting a new session is also a straightforward way to check what loads at startup. [Official plugin installation steps](https://code.claude.com/docs/en/discover-plugins#install-a-plugin)

Open `/plugin` and check the Installed tab. Type `/` to inspect the skills available to this session. You can also inspect the installed plugin list from your shell:

```bash
claude plugin list
```

Installing this toolkit does not install a game, its mod loader, or a finished mod. The upstream plugin also includes MCP configuration for asset tooling; inspect the plugin's components and resolve any configuration errors before using them.

## 3. Alternative: start Claude Code in an upstream clone

Use this route if you want to inspect the toolkit's files directly or your plugin installation is unavailable:

```bash
git clone https://github.com/rehan-remade/universal-modder
cd universal-modder
claude
```

The clone contains `CLAUDE.md`, `AGENTS.md`, `.claude/skills`, and MCP configuration. Review them before accepting workspace trust or enabling integrations. This clone is the toolkit working copy; it is separate from this guide repository. You do not need to copy the toolkit into a public tutorial repository.

Choose one installation route first. A clone and a marketplace installation can both contain the same skills, which makes it harder to tell which copy a session is using.

## 4. Check the `um` CLI separately

Upstream documents CLI setup for plugin installations and clones. Check whether your shell can actually resolve it:

```bash
um --help
um scan --help
um kb --help
```

If `um` is missing, the upstream standalone installation command is:

```bash
uv tool install git+https://github.com/rehan-remade/universal-modder
um --help
```

This command installs from the repository's current revision; it is not pinned to the snapshot used for this guide. Inspect the current source if you need a repeatable installation.

If uv reports that its tool executables are outside your `PATH`, use `uv tool update-shell`, then open a new terminal. This changes your shell setup. Start Claude Code from the same environment and repeat the help check. [uv tool installation and PATH guidance](https://docs.astral.sh/uv/guides/tools/#installing-tools)

For a knowledge-base check, run:

```bash
um kb search "minecraft"
```

A search result is prior documentation, not proof that the documented version matches your installation.

## 5. Keep asset generation optional

Begin with a placeholder texture or model. If you later choose fal generation, create a fal key and set it in the environment that starts Claude Code:

```bash
# macOS, Linux, or WSL
export FAL_KEY="your_fal_api_key"
```

```powershell
# Windows PowerShell
$env:FAL_KEY = "your_fal_api_key"
```

Use your real key locally; do not commit it, include it in a mod, or show it in a screenshot. Restart the agent from the configured shell if it does not inherit the variable. fal calls have separate usage costs. Upstream also offers `um comfy` for images using an existing local ComfyUI server. That does not supply every fal media capability. [Upstream asset setup](https://github.com/rehan-remade/universal-modder/blob/6c02e77d9088ecb1a7d9970572d8ca5387e7cb9e/README.md#install)

## 6. Ask for inspection before implementation

Give Claude Code a specific game path and use a first prompt like this:

```text
Find the mod-any-game skill. Inspect the game installed at [my game path]
and search the knowledge base for matching field notes. Tell me the engine,
exact version, installed loader, recommended route, save location, and files
you would change. Do not modify files or generate paid assets yet.
```

Confirm the reported edition, version, and loader against your own installation. Ask for the source field note and its version if the proposed route depends on one. Resolve missing skills, CLI tools, or integrations before letting the agent proceed.

Once inspection is correct, pick one change: one item, one weapon, or one data value. Ask for a minimal implementation using placeholder assets, a backup plan, a build command, and an in-game test procedure. A successful build is only one check; verify the change in the running game and record what actually happened.

## Common setup problems

| Symptom | Next check |
| --- | --- |
| `/plugin` is unavailable | Confirm you are in an interactive Claude Code session and consult its current installation documentation. |
| Plugin is installed but its skill is absent | Inspect the Installed and Errors tabs; read the install summary and reload or begin a new session as indicated. |
| Terminal finds `um`, but Claude Code does not | Compare the environments and launch Claude Code from the terminal where the help command works. |
| Asset server cannot start | Check its configuration and whether the agent process receives `FAL_KEY`; do not paste the key into chat. |
| Generated mod fails to load | Verify the game, loader, runtime, and mod versions; use the game's log to identify the failing component. |

## Sources and scope

- [Universal Modder README at the reviewed snapshot](https://github.com/rehan-remade/universal-modder/blob/6c02e77d9088ecb1a7d9970572d8ca5387e7cb9e/README.md): toolkit installation, prerequisites, CLI, and workflow.
- [Current upstream repository](https://github.com/rehan-remade/universal-modder): check for changes after this guide's review date.
- [Claude Code: install and manage plugins](https://code.claude.com/docs/en/discover-plugins): current plugin controls, installation scopes, and verification.
- [Claude Code: plugins overview](https://code.claude.com/docs/en/plugins): components and when plugins become available to sessions.
- [uv: using tools](https://docs.astral.sh/uv/guides/tools/): standalone tool installation and PATH handling.

Upstream examples and field notes belong to their respective authors. This guide reports documented setup; it does not certify every agent, operating system, loader, and game combination.
