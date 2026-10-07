# Install Universal Modder with Codex

Universal Modder adds game-modding skills, an inspection CLI, and field notes to a coding-agent workflow. This guide covers its Codex plugin installation, a repository-clone alternative, and checks to perform before changing game files.

This is an independent, unofficial guide. We do not maintain Universal Modder or represent OpenAI. The corresponding web edition is the [Codex installation guide](https://universalmodder.dev/guides/codex/).

**Source review:** October 7, 2026. Universal Modder repository snapshot: `6c02e77d9088ecb1a7d9970572d8ca5387e7cb9e`. Plugin command syntax was checked with local Codex CLI `0.160.1` help and official OpenAI documentation. This confirms command availability and syntax, rather than an installation result. We did not install Universal Modder, run its `um` commands, generate assets, or test a mod in a game while preparing this guide.

## 1. Prepare the agent and game

Use a working Codex CLI installation. Confirm that you can open a normal session, then check the available plugin commands from your terminal:

```bash
codex --version
codex plugin --help
codex plugin marketplace add --help
codex plugin add --help
```

If your installed version does not include the `plugin` subcommand, check the current OpenAI installation guidance or use the clone route below. Do not substitute Claude Code's `/plugin` commands; Codex's installation commands run in your system shell.

Keep a separate mod-source directory and test save for a locally installed game you own. Upstream lists Git, Python 3.10 or later, and ffmpeg as prerequisites and recommends uv. Blender is required for 3D-to-sprite rendering. Check your tools:

```bash
git --version
python --version
uv --version
ffmpeg -version
```

Your interpreter may be named `python3` on macOS or Linux. Confirm its version. Windows game workflows require a suitable native Windows or WSL setup; running Codex on another operating system does not make a game's binary or mod loader compatible.

## 2. Install through the plugin marketplace

Run these commands in Terminal or PowerShell:

```bash
codex plugin marketplace add rehan-remade/universal-modder
codex plugin add universal-modder@universal-modder
```

The marketplace command accepts the GitHub `owner/repo` form. The plugin selector uses `plugin@marketplace`; both names here are `universal-modder`. These forms match the [official marketplace reference](https://learn.chatgpt.com/docs/developer-commands#codex-plugin-marketplace) and [plugin reference](https://learn.chatgpt.com/docs/developer-commands#codex-plugin).

Check the result:

```bash
codex plugin marketplace list
codex plugin list --marketplace universal-modder
```

For more detailed installed and enabled fields, use:

```bash
codex plugin list --marketplace universal-modder --json
```

Start a new Codex session in your mod workspace and ask it to locate the `mod-any-game` skill. A successful marketplace addition only registers a source; verify that the plugin installation itself completed and the new session can use its skills.

The toolkit installation is separate from your game, game-specific loader, JDK or other build runtime, and finished mod. Review the plugin's components and any requested integration configuration before enabling them.

## 3. Alternative: work from the upstream clone

For a direct look at the toolkit files, or when your client lacks plugin commands:

```bash
git clone https://github.com/rehan-remade/universal-modder
cd universal-modder
codex
```

The upstream clone includes `AGENTS.md`, `.agents/skills`, and `.codex/config.toml`. Read those files before deciding to trust the workspace or enable its integrations. Official OpenAI documentation states that project-scoped MCP configuration is loaded for trusted projects. [Codex MCP configuration](https://learn.chatgpt.com/docs/extend/mcp)

This is a working copy of the upstream toolkit, separate from this independent guide repository. Publishing a tutorial does not require copying the upstream project into your own public repository. Choose one setup route first so you can identify the skills and configuration your session is loading.

## 4. Confirm that `um` is on the agent's PATH

Upstream documents CLI setup for plugin installations and clones. Check the shell rather than assuming setup completed:

```bash
um --help
um scan --help
um kb --help
```

If the command is missing, install the standalone CLI using the upstream command:

```bash
uv tool install git+https://github.com/rehan-remade/universal-modder
um --help
```

That command installs from the current repository revision, rather than pinning the reviewed snapshot. Inspect the current source when reproducing the setup later.

If uv warns that the executable directory is outside your `PATH`, run `uv tool update-shell` and open a new terminal before launching Codex. This updates your shell setup. A working terminal and an already-running agent can have different environments. [uv's tool installation guidance](https://docs.astral.sh/uv/guides/tools/#installing-tools)

Check knowledge-base access without changing the game:

```bash
um kb search "minecraft"
```

For a different game, replace the search text. Compare each field note's version and loader to your installation before following it.

## 5. Start with placeholder assets

You can inspect a game and plan a minimal mod before choosing a paid generation workflow. If you later want fal-generated assets, obtain a fal key and provide it locally in the environment that launches Codex:

```bash
# macOS, Linux, or WSL
export FAL_KEY="your_fal_api_key"
```

```powershell
# Windows PowerShell
$env:FAL_KEY = "your_fal_api_key"
```

Keep the actual key out of source control, packaged mods, screenshots, and chat. fal usage is billed separately. Start a fresh agent from the configured environment when checking key inheritance. An existing local ComfyUI server is another upstream image route via `um comfy`; it does not replace every fal service. [Upstream asset setup](https://github.com/rehan-remade/universal-modder/blob/6c02e77d9088ecb1a7d9970572d8ca5387e7cb9e/README.md#install)

## 6. Inspect first, then make one change

Use a first prompt that includes a real game path:

```text
Find the mod-any-game skill. Inspect the game installed at [my game path]
and search the knowledge base for matching field notes. Report the engine,
exact game version, installed loader, save location, and proposed modding
route. List the files you would change. Do not modify files, install loaders,
or generate paid assets yet.
```

Confirm those findings yourself. For Minecraft, record the edition, Minecraft version, loader name and version, and JDK target before creating the workspace. A loader for one version does not establish compatibility with another.

Then ask Codex to plan one small feature, such as one item or one reversible data change. The plan should include save backups, placeholder assets, a build command, an installation location, and the expected in-game result. Review the changes and check the game log during testing. Record successful builds and successful in-game checks separately.

## Troubleshooting by layer

| Problem | What to inspect |
| --- | --- |
| `codex plugin` is unavailable | Installed CLI version and help output; use the documented clone alternative if needed. |
| Marketplace exists, but plugin is absent | `codex plugin list` and the installation output; adding a marketplace alone does not install a plugin. |
| Plugin is listed, but the skill is missing | Installed/enabled fields and the skills visible to a fresh session. |
| Clone instructions load, but its MCP integration does not | Project trust, `.codex/config.toml`, and the configured server's requirements. |
| Codex cannot find `um` | CLI installation and the environment used to start Codex. |
| A mod builds but the game rejects it | Game and loader versions, dependencies, packaging, and the actual game log. |

## Sources and scope

- [Universal Modder README at the reviewed snapshot](https://github.com/rehan-remade/universal-modder/blob/6c02e77d9088ecb1a7d9970572d8ca5387e7cb9e/README.md): installation, prerequisites, CLI, and workflow.
- [Current upstream repository](https://github.com/rehan-remade/universal-modder): changes since this review.
- [OpenAI developer commands: Codex plugins](https://learn.chatgpt.com/docs/developer-commands#codex-plugin): plugin selectors and listing fields.
- [OpenAI developer commands: plugin marketplaces](https://learn.chatgpt.com/docs/developer-commands#codex-plugin-marketplace): accepted sources and marketplace management.
- [OpenAI: Model Context Protocol](https://learn.chatgpt.com/docs/extend/mcp): trusted project configuration and MCP transport support.
- [uv: using tools](https://docs.astral.sh/uv/guides/tools/): installation and executable PATH handling.

Local command checks for this review were limited to `codex --version`, `codex --help`, and relevant plugin subcommands with `--help`. No Universal Modder installation or game test is implied by this guide.
