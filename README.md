# i0xwUnlocker — Roblox FPS Unlocker (Unlimited FPS) 

NO FASTFLAGS, NO INJECTING IN ROBLOX. 
running external.

A small Windows console utility to patch Roblox client settings and set a target FPS cap in `ClientAppSettings.json`.  
Intended for advanced users who want to experiment with the client-side FPS target setting or automate applying a preferred FPS cap across Roblox installs. The tool is authored by @47ioxw.

Credits
- @47ioxw  
- [github/47ioxw](https://github.com/47ioxw)
- https://guns.lol/47ioxw

---

## **IMPORTANT**

Download the .NET Desktop Runtime from this link:  
[Download Now.](https://builds.dotnet.microsoft.com/dotnet/WindowsDesktop/6.0.36/windowsdesktop-runtime-6.0.36-win-x64.exe)

Paste it in your browser, run the installer, and finish the setup.  
Once it's installed, the FPS Unlocker will work with no issues.
---

## What this does

- Locates the latest Roblox version folder in `%LOCALAPPDATA%\Roblox\Versions`.
- Parses `ClientAppSettings.json` and sets the `DFIntTaskSchedulerTargetFps` property to a user-provided integer value.
- Creates a timestamped backup of the original `ClientAppSettings.json` before making changes.
- Offers checks and an animated console progress display while applying changes.
- Optionally can detect running Roblox processes and prompt to restart them.

This is a console application (no GUI). It uses animated text and colored output for status reporting.

---

## Important notes & warnings

- This modifies a local Roblox configuration file. Use at your own risk.
- A backup is always created (filename like `ClientAppSettings.json.bak.20251231235959`).
- You may need to run the program with permissions that allow writing inside the Roblox installation folder.
- Changes may not take effect until Roblox is restarted.
- This tool is provided as-is. It is the user's responsibility to ensure compliance with Roblox's Terms of Service.

---

## Requirements

- Windows OS
- .NET SDK (recommended: .NET 6, .NET 7, or .NET 8)
- Access to the local user profile where Roblox is installed

---

## Build & run

1. Place the provided `Program.cs` and project file in a folder.
2. Build:

   dotnet build

3. Run:

   dotnet run --project ./YourProjectName.csproj

(If you built an executable, run the produced .exe directly.)

---

## Usage (interactive)

When you run the program it will:

1. Display a small credits box:
   - @47ioxw
   - github.com/47ioxw
   - guns.lol/47ioxw

2. Prompt:
   > Press Enter to load FPS unlocker

3. Prompt for the FPS cap:
   > What is your target fps? > [user enters integer]

4. Press Enter to apply.

The console then performs several checks (animated, colored) and will:
- Show whether it found Roblox.
- Create a backup.
- Parse JSON.
- Write the new value in-memory and save the file.
- Show whether Roblox is running and optionally restart it.

At the end the console prints a summary and auto-closes after a short delay.

---

## Command-line options and behavior

This tool is primarily interactive. It performs these actions by default:

- Find latest Roblox version folder
- Ensure `ClientAppSettings.json` exists and is writable
- Backup settings file
- Apply the FPS cap value (property `DFIntTaskSchedulerTargetFps`)
- Save patched JSON (writes to a temp then replaces the original)
- Detect running Roblox processes and optionally restart them

There are no required command-line arguments in the supplied version. You can extend the source to add non-interactive flags (for batch automation).

---

## Backup & Restore

- Backups are created in the same directory as the original settings file and are named:
  `ClientAppSettings.json.bak.<timestamp>`
- To restore: copy the backup file over the original `ClientAppSettings.json` (or use any GUI/file manager).

Example:

cp "%LOCALAPPDATA%\Roblox\Versions\<version>\ClientSettings\ClientAppSettings.json.bak.20251231235959" "%LOCALAPPDATA%\Roblox\Versions\<version>\ClientSettings\ClientAppSettings.json"

---

## Example session

- Console shows credits box.
- Press Enter.
- Enter `5` for target FPS.
- Press Enter to apply.
- Animated checks run (colored output).  
  - [+] Checking Roblox Versions folder (green)
  - [+] Found latest Roblox version folder (green)
  - [+] ClientAppSettings.json exists (green)
  - [+] Settings file writable (green)
  - [+] Backup created (green)
  - [+] Parsed settings JSON (green)
  - [+] Settings FPS cap present (DFIntTaskSchedulerTargetFps) (green)
  - [+] Updated JSON property in-memory (green)
  - [+] Saved patched settings file (green)
  - [-] Roblox processes running (red) — if Roblox is running this check shows a failure so you can opt to restart the client.
- Summary printed (successes in dark green, failures in red).
- Console closes automatically after a short delay.

---

## Troubleshooting

- "Settings file not found": ensure Roblox is installed and you are running under the correct Windows user who installed Roblox.
- "Settings file not writable": run the console as a user with appropriate privileges or ensure the file is not locked by another process.
- If changes don't appear in-game, restart Roblox.

---

## Security & privacy

- The tool edits a local configuration file only. No network connectivity is required or used by the base tool.
- Inspect the code before running; it is open source and simple (text file parsing/writing).

---

## License

This project is provided under the MIT license (or choose your preferred license). Include an appropriate LICENSE file when publishing.

---

## Changelog / Story (short)

- v1.0 — Initial console tool that finds Roblox settings and patches the FPS cap with animated checks and backups.
- Future — may add non-interactive CLI flags, watch mode, improved validation, and cross-user install detection.

---

If you want, I can also:
- Produce a short GitHub repo description for the web UI,
- Add a sample LICENSE file,
- Make a small PowerShell wrapper for running non-interactively.

```
