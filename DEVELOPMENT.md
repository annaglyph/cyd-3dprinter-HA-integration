# Development

This fork is the maintained source for the CYD dashboard firmware. Day-to-day workflow:

1. Edit package files under `packages/`
2. Test locally with `!include` (see below)
3. Commit and push to `main` on [annaglyph/cyd-3dprinter-HA-integration](https://github.com/annaglyph/cyd-3dprinter-HA-integration)
4. Flash your CYD — it loads packages from `github://annaglyph/cyd-3dprinter-HA-integration/...@main`

Upstream [maelremrem/cyd-3dprinter-HA-integration](https://github.com/maelremrem/cyd-3dprinter-HA-integration) is fetched as `origin`. Sync occasionally if needed:

```bash
git fetch origin
git merge origin/main   # only if upstream has changes you want
```

## Device config (production)

Point your ESPHome device YAML at this fork:

```yaml
esphome:
  name: ${device_name}
  friendly_name: ${friendly_name}
  name_add_mac_suffix: false
  min_version: 2026.6.0

packages:
  pins: github://annaglyph/cyd-3dprinter-HA-integration/packages/cyd-dashboard-pins.yaml@main
  colors: github://annaglyph/cyd-3dprinter-HA-integration/packages/cyd-dashboard-colors.yaml@main
  dashboard: github://annaglyph/cyd-3dprinter-HA-integration/packages/cyd-dashboard.yaml@main
```

ESPHome caches GitHub packages locally and refreshes about once per day. After pushing to `main`, re-run **Install** in ESPHome Builder to pick up changes immediately.

If you still see stale package errors after a push, use `refresh: 0s` on the dashboard package (see `exemple-esphome-file.yaml`) or switch to local `!include` while testing.

**Using local `!include`:** ESPHome reads `/config/esphome/packages/cyd-dashboard.yaml` on disk — pushing to GitHub does not update that file. Recopy from this repo after each change.

The `esphome.name` and `friendly_name` fields must be in your root device YAML, not inside the dashboard package. Recent ESPHome versions validate those names before package substitutions are expanded.

## Testing local package changes

Before pushing, test from a local clone without waiting for GitHub cache:

Copy package files into your Home Assistant ESPHome directory:

```text
/config/esphome/packages/cyd-dashboard-pins.yaml
/config/esphome/packages/cyd-dashboard-colors.yaml
/config/esphome/packages/cyd-dashboard.yaml
```

Then use local includes in your device config:

```yaml
packages:
  pins: !include packages/cyd-dashboard-pins.yaml
  colors: !include packages/cyd-dashboard-colors.yaml
  dashboard: !include packages/cyd-dashboard.yaml
```

After testing, push to `main` on this fork and switch the device config back to the `github://annaglyph/...` URLs above.

## Branch layout

| Branch | Purpose |
|--------|---------|
| `main` | Stable firmware — use this for `github://...@main` |
| `origin/main` | Upstream (read-only reference) |

Feature branches can be merged into `main` when ready. No need to open pull requests upstream unless the original author starts merging again.
