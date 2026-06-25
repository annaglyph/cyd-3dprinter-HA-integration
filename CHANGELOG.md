# Changelog

All notable changes to this project will be documented in this file.

## Unreleased

## 2026.06.24

Fork maintenance release on [annaglyph/cyd-3dprinter-HA-integration](https://github.com/annaglyph/cyd-3dprinter-HA-integration). Package URLs now point at this fork. Requires ESPHome 2026.6.0+.

- Removed seconds from theme clocks so the header time displays as `HH:MM`.
- Left-anchored the Tactical, Orbit, and Monitor header clocks to reduce visual jitter when the time changes.
- Widened Orbit and Monitor header clocks so two-digit hours (e.g. `20:05`) are not clipped.
- Split temperature units into smaller labels so `C` renders at a reduced size next to the numeric value.
- Improved quick panel footer spacing so the IP address no longer pushes the online status off-screen.
- Normalized quick panel switch and power status casing from `on`/`off` to `On`/`Off`.
- Replaced deprecated ESPHome IP address string formatting to stay compatible with ESPHome 2026.8.0 and newer.
- Convert print start/end times from UTC timestamps to the Home Assistant local timezone so they match the header clock.
- Derive end time from `now + remaining` during active prints so it matches the ETA, using the same unit conversion as the ETA label.
- Capture print start time on the CYD when print status first switches to Preparing or Running, instead of using the unreliable Bambu `start_time` sensor.
- Show a screensaver clock and date overlay when auto-sleep dims the backlight.
- Add day/night screensaver brightness with a configurable schedule (default 22:00–07:00), exposed as Home Assistant config entities.
- Move `esphome.name` and `friendly_name` to the root device config for compatibility with newer ESPHome package validation.
- Add explicit display offset/pad dimensions for ESPHome 2026.6+ `mipi_spi` validation.
