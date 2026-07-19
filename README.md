# RS-Key Builder

Build [RS-Key](https://github.com/TheMaxMur/RS-Key) firmware — no local toolchain needed.

## Usage

1. **Create a repo** from this template (green "Use this template" button).
2. **Enable GitHub Actions** in your new repo (Settings → Actions → Allow all actions).
3. **Trigger a build** — go to Actions → "Build RS-Key firmware" → "Run workflow".
   Fill in the build parameters.
4. **Download** the resulting `firmware.uf2` from the created GitHub Release.
5. **Flash** your RP2350 board:
   ```
   picotool load -v firmware.uf2 && picotool reboot
   ```
   Or hold BOOTSEL, plug in, and drag-and-drop the UF2 onto the `RP2350` volume.
6. **Delete the repo** — it served its purpose.

## Build inputs

| Input | Default | Description |
|---|---|---|
| `RS_KEY_VERSION` | `latest` | Git ref to build (tag, branch, commit, or `latest`) |
| `BOARD` | `waveshare-rp2350-one` | Board hardware preset (`custom` for manual) |
| `VIDPID` | `RSKey` | USB identity (RSKey, Yubikey5, NitroFIDO2, etc.) |
| `FW_VERSION` | `5.7.4` | Firmware version string |
| `PRESENCE_PIN` | `bootsel` | Touch button GPIO |
| `FEATURES` | — | Cargo features, comma-separated (e.g. `no-touch,display`) |
| `ENV_EXTRA` | — | `KEY=VAL` pairs for rare knobs |

All env vars from [RS-Key build.md](https://github.com/TheMaxMur/RS-Key/blob/main/docs/build.md) are
available — either as dedicated inputs or through `ENV_EXTRA` for rare knobs. Board presets
pre-fill hardware values; individual inputs override the preset when filled.

## Flashing

Put your RP2350 board into BOOTSEL mode (hold the BOOT button while plugging in USB):

```
picotool load -v firmware.uf2 && picotool reboot
```

Or copy `firmware.uf2` to the mounted `RP2350` volume.

Quick start guide: https://github.com/TheMaxMur/RS-Key/blob/main/docs/quickstart.md
