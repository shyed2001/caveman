# Caveman Installation Guide for Shyed's Other Computers

Date: 2026-04-22 Asia/Dhaka

Purpose: repeatable Caveman setup for Codex CLI, Codex VS Code IDE extension, Claude Code, GitHub Copilot, Gemini CLI, Cursor/Windsurf, and local repo workflows.

## Scope

This guide uses your standard Windows repo layout:

```text
F:\GitHubDesktop\GitHubCloneFiles\caveman
F:\GitHubDesktop\GitHubCloneFiles\cavemem
F:\GitHubDesktop\GitHubCloneFiles\Obsidian_Vault
```

Canonical AI/tooling policy:

```text
F:\GitHubDesktop\GitHubCloneFiles\Obsidian_Vault\8 AI_Prompt_Engineering\000 AI Tools Workflow Index.md
```

Use repo instructions first, then canonical policy, then tool defaults.

## What Caveman Does

Caveman compresses agent output. Less filler, same technical substance.

Default grammar:

```text
Drop articles/filler/pleasantries/hedging.
Fragments OK.
Short synonyms.
Pattern: [thing] [action] [reason]. [next step].
Code/commits/security: write normal.
Off switch: "normal mode" or "stop caveman".
```

Codex trigger:

```text
$caveman
```

Other agents may use:

```text
/caveman
caveman mode
talk like caveman
less tokens please
```

## Prerequisites

PowerShell:

```powershell
node --version
npm --version
git --version
codex --version
```

Recommended: one Windows Node install per machine. Avoid mixing Node versions for global AI tools.

Repo clone:

```powershell
cd "F:\GitHubDesktop\GitHubCloneFiles"
git clone https://github.com/JuliusBrussee/caveman.git
```

If repo already exists:

```powershell
cd "F:\GitHubDesktop\GitHubCloneFiles\caveman"
git pull
```

## Windows Symlink Choice

Safer repo-local setting:

```powershell
git -C "F:\GitHubDesktop\GitHubCloneFiles\caveman" config core.symlinks true
```

Avoid global unless needed:

```powershell
git config --global core.symlinks true
```

Why avoid global by default:

- Future repos may check out real symlinks.
- FAT/exFAT/network shares may fail.
- Some Windows tools handle symlinks poorly.

Undo global:

```powershell
git config --global --unset core.symlinks
```

Verify:

```powershell
git -C "F:\GitHubDesktop\GitHubCloneFiles\caveman" config --show-origin --get core.symlinks
```

Expected:

```text
file:.git/config true
```

## Install Caveman for Codex CLI

PowerShell:

```powershell
cd "F:\GitHubDesktop\GitHubCloneFiles\caveman"
codex plugin marketplace add "F:\GitHubDesktop\GitHubCloneFiles\caveman"
codex --no-alt-screen
```

Inside Codex:

```text
/plugins
```

Then:

```text
Search: caveman
Open: Caveman
Choose: Install plugin
```

Verify inside Codex:

```text
$caveman
```

Expected:

```text
Caveman mode active. What task?
```

## Install Caveman for Codex VS Code IDE Extension

Codex IDE extension uses same Codex plugin/config state as Codex CLI.

Steps:

```text
Open VS Code
Open folder: F:\GitHubDesktop\GitHubCloneFiles\caveman
Open Codex sidebar
Open Codex Settings / Plugins
Find Caveman Repo
Install Caveman
Reload VS Code window
```

Use in Codex IDE chat:

```text
$caveman
```

Windows note: repo hooks may not auto-start in all Codex Windows surfaces. Manual `$caveman` is reliable.

## Install Caveman for Claude Code

PowerShell:

```powershell
claude plugin marketplace add JuliusBrussee/caveman
claude plugin install caveman@caveman
```

Verify in Claude Code:

```text
/caveman
```

## Install Caveman for GitHub Copilot

PowerShell:

```powershell
npx skills add JuliusBrussee/caveman -a github-copilot
```

If symlink trouble:

```powershell
npx skills add JuliusBrussee/caveman -a github-copilot --copy
```

Note: `npx skills add` installs skill files. It may not add always-on Copilot instructions. Add this to Copilot custom instructions if needed:

```text
Terse like caveman. Technical substance exact. Only fluff die.
Drop articles, filler, pleasantries, hedging.
Fragments OK. Short synonyms. Code unchanged.
Pattern: [thing] [action] [reason]. [next step].
ACTIVE EVERY RESPONSE. Off: "normal mode" or "stop caveman".
Code/commits/security: write normal.
```

## Install Caveman for Gemini CLI

PowerShell:

```powershell
gemini extensions install https://github.com/JuliusBrussee/caveman
```

Verify:

```text
/caveman
```

## Install Caveman for Cursor / Windsurf

PowerShell:

```powershell
npx skills add JuliusBrussee/caveman -a cursor
npx skills add JuliusBrussee/caveman -a windsurf
```

If symlink trouble:

```powershell
npx skills add JuliusBrussee/caveman -a cursor --copy
npx skills add JuliusBrussee/caveman -a windsurf --copy
```

## Session Log from This Machine

User goal:

```text
Install Caveman and Cavemem for Codex CLI and Codex IDE extension.
```

Actions performed:

```powershell
git -C /mnt/f/GitHubDesktop/GitHubCloneFiles/caveman config core.symlinks true
codex plugin marketplace add /mnt/f/GitHubDesktop/GitHubCloneFiles/caveman
codex --no-alt-screen
```

Codex TUI steps performed:

```text
Trusted repo directory.
Opened /plugins.
Searched caveman.
Opened Caveman details.
Selected Install plugin.
Saw: Installed Caveman plugin. No additional app authentication is required.
Ran: $caveman
Saw: Caveman mode active. What task?
```

Results:

```text
codex-cli 0.122.0-alpha.13
Caveman Repo already added
Caveman plugin installed
$caveman works
core.symlinks true repo-local
codex_hooks true
```

Warnings seen:

```text
Codex could not find bubblewrap on PATH.
Codex will use vendored bubblewrap in the meantime.
```

Meaning: non-blocking. Codex continued.

Warning:

```text
Under-development features enabled: codex_hooks.
```

Meaning: hooks enabled but feature under development. Keep if you want repo-local hook behavior.

## Errors and Avoidance

Problem:

```text
git config failed: could not lock config file .git/config: Read-only file system
```

Cause: sandbox write restriction.

Fix: run with approval/escalation, or run command directly in PowerShell:

```powershell
git -C "F:\GitHubDesktop\GitHubCloneFiles\caveman" config core.symlinks true
```

Problem:

```text
Codex plugin CLI has marketplace add, but no direct plugin install subcommand.
```

Fix: use Codex TUI or VS Code Codex plugin UI:

```text
/plugins -> Caveman -> Install plugin
```

Problem:

```text
Enter key in Codex TUI did not execute first try.
```

Fix: press Enter again. TUI eventually opened plugin list.

Problem:

```text
Windows hooks may not auto-start Caveman everywhere.
```

Fix: run manually:

```text
$caveman
```

## Maintenance

Update Caveman repo:

```powershell
cd "F:\GitHubDesktop\GitHubCloneFiles\caveman"
git pull
codex plugin marketplace upgrade caveman-repo
```

Re-test:

```powershell
codex --no-alt-screen
```

Inside Codex:

```text
$caveman
```

## Audit Log and Reasoning Boundary

This guide records user requests, commands, actions, test results, error logs, fixes, and prevention notes.

Hidden chain-of-thought cannot be included. Use this safe substitute instead:

```text
User prompt summary: what user asked for.
Action log: commands/UI steps performed.
Observation log: outputs, warnings, failures, success messages.
Decision notes: short reason for each setup choice.
Avoidance notes: how to prevent same error on other computers.
```

Decision notes from this setup:

```text
Decision: use repo-local core.symlinks to avoid global Git behavior changes.
Decision: use Codex TUI because CLI has no plugin install subcommand.
Decision: manual $caveman remains reliable on Windows.
```

Do not paste private secrets into logs. Use redacted placeholders:

```text
TOKEN=<redacted>
PATH=<machine-specific path>
USER=<windows user>
```
