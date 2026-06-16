# Changelog

All notable changes to this project will be documented in this file.

## Unreleased

- Removed seconds from theme clocks so the header time displays as `HH:MM`.
- Left-anchored the Tactical, Orbit, and Monitor header clocks to reduce visual jitter when the time changes.
- Widened Orbit and Monitor header clocks so two-digit hours (e.g. `20:05`) are not clipped.
- Split temperature units into smaller labels so `C` renders at a reduced size next to the numeric value.
- Improved quick panel footer spacing so the IP address no longer pushes the online status off-screen.
- Normalized quick panel switch and power status casing from `on`/`off` to `On`/`Off`.
- Replaced deprecated ESPHome IP address string formatting to stay compatible with ESPHome 2026.8.0 and newer.
- Convert print start/end times from UTC timestamps to the Home Assistant local timezone so they match the header clock.
- Treat ISO-format Bambu timestamps without an explicit offset as UTC, and derive end time from remaining duration when a print is active so it matches the ETA.
- Capture print start time on the CYD when print status first switches to Preparing or Running, instead of using the unreliable Bambu `start_time` sensor.
