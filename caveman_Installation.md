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

## Installation Process Log - 2026-04-22T12:22:40+06:00

Machine:

```text
hostname: DESKTOP-NAF9NIA
platform.uname: Linux DESKTOP-NAF9NIA 6.6.87.2-microsoft-standard-WSL2 #1 SMP PREEMPT_DYNAMIC Thu Jun  5 18:30:46 UTC 2025 x86_64 x86_64
os-release: PRETTY_NAME="Ubuntu 24.04.2 LTS"; VERSION_ID="24.04"; VERSION_CODENAME=noble
timezone/current_date_context: Asia/Dhaka / 2026-04-22
cwd: /mnt/f/GitHubDesktop/GitHubCloneFiles/Webassembly/CCGS_WASM
repo_root: /mnt/f/GitHubDesktop/GitHubCloneFiles
```

Tool checks:

```text
codex --version:
codex-cli 0.122.0-alpha.13

npm --version:
10.9.7

npx --version:
10.9.7

python3 --version:
Python 3.12.3
```

Software inventory:

```text
git --version:
git version 2.43.0

bash --version:
GNU bash, version 5.2.21(1)-release (x86_64-pc-linux-gnu)
Copyright (C) 2022 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>

This is free software; you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

python3 -m pip --version:
/usr/bin/python3: No module named pip
```

Hardware snapshot:

```text
lscpu:
Architecture:                         x86_64
CPU op-mode(s):                       32-bit, 64-bit
Address sizes:                        46 bits physical, 48 bits virtual
Byte Order:                           Little Endian
CPU(s):                               12
On-line CPU(s) list:                  0-11
Vendor ID:                            GenuineIntel
Model name:                           12th Gen Intel(R) Core(TM) i5-12500
CPU family:                           6
Model:                                151
Thread(s) per core:                   2
Core(s) per socket:                   6
Socket(s):                            1
Stepping:                             5
BogoMIPS:                             5990.39
Flags:                                fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ss ht syscall nx pdpe1gb rdtscp lm constant_tsc arch_perfmon rep_good nopl xtopology tsc_reliable nonstop_tsc cpuid tsc_known_freq pni pclmulqdq vmx ssse3 fma cx16 pdcm pcid sse4_1 sse4_2 x2apic movbe popcnt tsc_deadline_timer aes xsave avx f16c rdrand hypervisor lahf_lm abm 3dnowprefetch ssbd ibrs ibpb stibp ibrs_enhanced tpr_shadow ept vpid ept_ad fsgsbase tsc_adjust bmi1 avx2 smep bmi2 erms invpcid rdseed adx smap clflushopt clwb sha_ni xsaveopt xsavec xgetbv1 xsaves avx_vnni vnmi umip waitpkg gfni vaes vpclmulqdq rdpid movdiri movdir64b fsrm md_clear serialize arch_lbr flush_l1d arch_capabilities
Virtualization:                       VT-x
Hypervisor vendor:                    Microsoft
Virtualization type:                  full
L1d cache:                            288 KiB (6 instances)
L1i cache:                            192 KiB (6 instances)
L2 cache:                             7.5 MiB (6 instances)
L3 cache:                             18 MiB (1 instance)
NUMA node(s):                         1
NUMA node0 CPU(s):                    0-11
Vulnerability Gather data sampling:   Not affected
Vulnerability Itlb multihit:          Not affected
Vulnerability L1tf:                   Not affected
Vulnerability Mds:                    Not affected
Vulnerability Meltdown:               Not affected
Vulnerability Mmio stale data:        Not affected
Vulnerability Reg file data sampling: Not affected
Vulnerability Retbleed:               Mitigation; Enhanced IBRS
Vulnerability Spec rstack overflow:   Not affected
Vulnerability Spec store bypass:      Mitigation; Speculative Store Bypass disabled via prctl
Vulnerability Spectre v1:             Mitigation; usercopy/swapgs barriers and __user pointer sanitization
Vulnerability Spectre v2:             Mitigation; Enhanced / Automatic IBRS; IBPB conditional; RSB filling; PBRSB-eIBRS SW sequence; BHI BHI_DIS_S
Vulnerability Srbds:                  Not affected
Vulnerability Tsx async abort:        Not affected

memory:
total        used        free      shared  buff/cache   available
Mem:            15Gi       638Mi        14Gi       3.5Mi       289Mi        14Gi
Swap:          4.0Gi          0B       4.0Gi

disk:
Filesystem      Size  Used Avail Use% Mounted on
F:\             293G   63G  231G  22% /mnt/f
```

Account/user snapshot:

```text
whoami: shyed2001
id:
uid=1000(shyed2001) gid=1000(shyed2001) groups=1000(shyed2001),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),100(users)
home: /home/shyed2001
shell: /bin/bash
```

Environment snapshot, selected non-secret values only:

```text
SHELL=/bin/bash
HOME=/home/shyed2001
USER=shyed2001
USERNAME=User
PATH=/home/shyed2001/.codex/tmp/arg0/codex-arg0fVHsPg:/mnt/c/Users/User/.vscode/extensions/openai.chatgpt-26.417.40842-win32-x64/bin/linux-x86_64:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/usr/lib/wsl/lib:/mnt/e/Program Files/Microsoft VS Code:/mnt/e/Program Files/Python313/Scripts/:/mnt/e/Program Files/Python313/:/mnt/c/Windows/system32:/mnt/c/Windows:/mnt/c/Windows/System32/Wbem:/mnt/c/Windows/System32/WindowsPowerShell/v1.0/:/mnt/c/Windows/System32/OpenSSH/:/mnt/c/Program Files/NVIDIA Corporation/NVIDIA app/NvDLISR:/mnt/c/Program Files (x86)/NVIDIA Corporation/PhysX/Common:/mnt/e/Program Files/Microsoft VS Code/bin:/mnt/c/Program Files (x86)/HP/HP OCR/DB_Lib/:/mnt/c/Program Files/HP/Common/HPDestPlgIn/:/mnt/c/Program Files (x86)/HP/Common/HPDestPlgIn/:/mnt/c/ProgramData/chocolatey/bin:/mnt/e/Program Files/CMake/bin:/mnt/c/Program Files/Microsoft SQL Server/150/Tools/Binn/:/mnt/c/Program Files/Microsoft SQL Server/Client SDK/ODBC/170/Tools/Binn/:/mnt/c/Program Files/GitHub CLI/:/mnt/c/Program Files/Go/bin:/mnt/e/Program Files/nodejs/:/mnt/c/Program Files/dotnet/:/mnt/c/Program Files (x86)/Windows Kits/10/Windows Performance Toolkit/:/mnt/c/Program Files/Tailscale/:/mnt/e/Program Files/Git/cmd:/mnt/c/Users/User/.local/bin:/mnt/c/Users/User/AppData/Local/Microsoft/WindowsApps:/mnt/c/Users/User/AppData/Local/GitHubDesktop/bin:/mnt/c/Program Files/HP/Common/HPDestPlgIn/:/mnt/c/Program Files (x86)/HP/Common/HPDestPlgIn/:/mnt/c/Users/User/.dotnet/tools:/mnt/c/Users/User/AppData/Local/Microsoft/WindowsApps/python.exe:/mnt/e/Users/User/AppData/Local/Programs/Antigravity/bin:/mnt/c/Users/User/go/bin:/mnt/e/Programs/Obsidian:/mnt/c/Users/User/go/bin:/mnt/c/Users/User/AppData/Roaming/npm:/mnt/c/Users/User/.dotnet/tools:/snap/bin
WSL_DISTRO_NAME=Ubuntu
WSL_INTEROP=/run/WSL/316_interop
LANG=C.UTF-8
TERM=xterm-256color
```

Network snapshot, local routing/interfaces only:

```text
ip route:
default via 172.30.64.1 dev eth0 proto kernel 
172.30.64.0/20 dev eth0 proto kernel scope link src 172.30.75.219

ip addr brief:
lo               UNKNOWN        127.0.0.1/8 10.255.255.254/32 ::1/128 
eth0             UP             172.30.75.219/20 fe80::215:5dff:febf:4328/64

resolv.conf nameservers:
nameserver 10.255.255.254
```

Actions completed in this Codex session:

```text
Read local Caveman and Cavemem installation notes.
Verified Cavemem native installers support claude-code, codex, cursor, gemini-cli, opencode.
Verified Copilot needs skills install / MCP bridge; Cavemem has no native copilot installer.
Verified Antigravity has no native Cavemem installer in local repo scan; use instruction files + MCP-compatible bridge where available.
Created Windows PowerShell installer:
F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\scripts\install_caveman_cavemem_windows.ps1
Created guide:
F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\docs\caveman-cavemem-local-ai-install.md
Updated canonical AI tooling index to link installer and guide.
Refreshed compact repo policy references via consolidate_agent_tooling_policy.py.
Added backup behavior before installer edits JSON/text configs.
Kept MemPalace install optional behind -InstallMemPalace.
```

Blocked / not performed:

```text
Did not run npm install -g cavemem from WSL shell because Windows npm/npx fail here:
WSL 1 is not supported. Please upgrade to WSL 2 or above.
Could not determine Node.js install directory

Note: uname reports WSL2, but visible npm/npx shims still fail from this shell.
Best practice: run installer from normal Windows PowerShell so Node/npm/native modules/MCP runtime use one Windows Node version.

Codex plugin marketplace add was attempted but user rejected approval, so Codex plugin config was not changed by this session.
```

Next safe command for this machine:

```powershell
cd "F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM"
powershell -ExecutionPolicy Bypass -File .\scripts\install_caveman_cavemem_windows.ps1
```

Optional MemPalace bridge:

```powershell
powershell -ExecutionPolicy Bypass -File .\scripts\install_caveman_cavemem_windows.ps1 -InstallMemPalace
```

Multi-machine note:

```text
Each computer should run the PowerShell installer locally.
Do not copy machine-specific MCP config blindly across computers.
Use same repo root when possible: F:\GitHubDesktop\GitHubCloneFiles
Installer creates backups before edits and skips unavailable optional tools.
```

