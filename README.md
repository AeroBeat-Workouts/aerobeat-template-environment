# AeroBeat Environment Template

UGC environments (levels, lighting, skyboxes) for AeroBeat.

## 📋 Repository Details

*   **Type:** Environments (Art)
*   **License:** **CC BY-NC 4.0**
*   **Dependencies:**
    *   `aerobeat-asset-core` (Canonical shared asset/resource contract)

## GodotEnv development flow

This repo uses the AeroBeat GodotEnv asset-package convention.

- Canonical dev/test manifest: `.testbed/addons.jsonc`
- Installed dev/test addons: `.testbed/addons/`
- GodotEnv cache: `.testbed/.addons/`
- Hidden workbench project: `.testbed/project.godot`
- Repo-local unit tests: `.testbed/tests/`

The repo root remains the package/published boundary for downstream consumers. Day-to-day development, import checks, and validation happen from the hidden `.testbed/` workbench using the pinned OpenClaw toolchain: Godot `4.6.2 stable standard`.

### Restore dev/test dependencies

From the repo root:

```bash
cd .testbed
godotenv addons install
```

That restores this repo's current dev/test manifest into `.testbed/addons/`. Canonically, this template belongs to the Asset lane and should describe its shared contract in terms of `aerobeat-asset-core`.

### Open the workbench

From the repo root:

```bash
godot --editor --path .testbed
```

Use this `.testbed/` project as the canonical direct-development and import-validation surface for environment work.

### Import smoke check

From the repo root:

```bash
godot --headless --path .testbed --import
```

### Run unit tests

From the repo root:

```bash
godot --headless --path .testbed --script addons/gut/gut_cmdln.gd \
  -gdir=res://tests \
  -ginclude_subdirs \
  -gexit
```

## 📂 Structure

*   `assets/levels/` - Level scenes and composition resources.
*   `assets/lighting/` - Lighting rigs, skyboxes, and environment resources.

## Validation notes

- `.testbed/addons.jsonc` is the committed dev/test dependency contract.
- The current manifest still pins the transition-era `aerobeat-core` package key to `v0.1.0` alongside GUT `main`. Canonical lane ownership is `aerobeat-asset-core`.
- Repo-local unit tests live under `.testbed/tests/`.
- This template is root-packaged (`subfolder: "/"`) and does not use a `.testbed/src` bridge; environment assets stay under the repo root package boundary.

## Notes

- Use the hidden workbench to restore shared contracts and import/test environment resources before consuming them elsewhere.
