# RAWM

RAWM is a portable, local PowerShell chat app. Type `roman` after one-time registration to open it in the current terminal. The in-app title and prompt use the configured passcode (`interface.passcode`, currently `roman`) so the visible identity can become personal to each user.

## Setup

From the RAWM folder:

```powershell
.\Install-RAWM.ps1 -Component all
.\Register-RAWM.ps1 -AllPowerShellEditions
```

Open a new PowerShell window and run `roman`. The first command downloads a local llama.cpp runtime plus Qwen model files and can take time. After setup, chats and inference remain local and need no API key.

Run `.\Start-RAWM.ps1` directly when using an unregistered computer. Run `.\Unregister-RAWM.ps1 -AllPowerShellEditions` to remove only RAWM's profile blocks.

Use `/help` inside RAWM for chat commands. Use `/paste` for multiline code and end it with `.send`.

## Local agent

RAWM now supports local file review and controlled actions from the same chat:

```text
Check "C:\path\script.py" for bugs
List workspace files
Create file "notes.txt" containing "Hello Roman"
Rename "notes.txt" to "ideas.txt"
Open Notepad and write hello green world
Hello - open Chrome or the Edge browser and open up YouTube
Open YouTube and search for cooking videos
Is the agent active right now?
Open Notepad and write an HTML program that says Hello World
Create first.txt containing alpha, then rename it to second.txt.
```

Actions show a plain-language preview and wait for **y** (approve) or **n** (cancel). No slash command is needed. Say `turn agent off` to switch to chat only, or `turn agent on` to re-enable actions. Approval expires after five minutes and applies only to the displayed action. File creation and renaming stay inside RAWM's `workspace` folder. Explicit file inspection can read a selected local text/code file elsewhere.

Notepad accepts unquoted text and the spelling `note pad`. If you ask to write without supplying text, RAWM asks what to type before proposing the action. Requests to generate code in Notepad use the installed local coding model, then show the actual code for approval. Drafts support up to 16,000 characters. The adapter verifies the visible editor text before reporting success; the draft remains open and unsaved.

Browser launches use Chrome or Edge directly, without loading a model. A website needs internet access; model inference stays local. A launch result confirms that Windows accepted the URL, not that the page finished loading. Opening a browser without a destination opens a blank page. Agent-status questions read the application's real state. Say `copy the last answer` to copy a response without using Ctrl+C.

Operations show their name and elapsed time every five seconds while waiting. Escape or Ctrl+C in the TZ terminal cancels active model/worker waits and returns control; completed changes remain. No animation or alternate-screen UI is used. Mouse selection and copy shortcuts still depend on the terminal hosting TZ. See the [September reliability changes](docs/TZ-RELIABILITY-2026-09-15.md) for test results and remaining limits.

## Agent workers

RAWM can discover installed Pi Code, Qwen Code, and Codex CLI workers. Say `show workers` (or use `/workers`) to see availability; `/worker auto|pi|qwen|codex|local` selects one for the session. Broad coding and desktop requests show the exact task and selected worker before approval. Direct browser and Notepad actions take precedence. Pi and Qwen use local Ollama with the supplied configuration. Automatic selection excludes Codex; selecting it explicitly requires its own credentials and can use a remote service. A worker report is labeled as a report, rather than verified task completion.

See [the compute-funnel handoff](ROMAN-RAWM-COMPUTE-FUNNEL-HANDOFF.md) for the current state and the next verification.
