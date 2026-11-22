# OSD canvas resizer for Betaflight and ArduPilot

**Live tool: https://jaroszmm.github.io/Betaflight-VISOR-OSD-resizer/**

Stretches an OSD layout to a bigger canvas by moving element positions.
Works with Betaflight (CLI output) and ArduPilot (param file). It runs entirely
in your browser, and nothing you paste is sent anywhere.

## Why

DJI Goggles 3 with VISOR (UHD fonts) draw a 60x22 OSD grid, but the O3/O4 air
unit reports the standard 53x20 canvas. Betaflight 2025 and newer takes its
canvas size from the video system and no longer lets you set it in the CLI,
so the configurator can't place elements in the extra columns and rows.
In ArduPilot the same stretch (for example 50x18 to 60x22) saves you moving
every item by hand.

With HD fonts the stock canvas is already right and you don't need this tool.

## How to use

### Betaflight
1. In the CLI run `get osd` (or `diff all`) and copy the output.
2. Open the tool, choose **Betaflight**, and paste it in.
3. Keep **53x20** as the source and **60x22** as the target (or set your own).
4. Click **Resize layout** and check the preview.
5. Paste the resulting `set` lines into the CLI. They end with `save`.
6. Check the layout in the goggles. The configurator shows the right-hand
   elements past its border, which is expected.

### ArduPilot
1. Save your parameters to a file, or copy the `OSD1_*` lines.
2. Choose **ArduPilot**, paste them in, and pick the OSD screen.
3. Keep **50x18** as the source and **60x22** as the target (or set your own).
4. Click **Resize layout** and check the preview.
5. Download the `.param` file and load it in Mission Planner or your ground station.
6. Check that `OSDn_TXT_RES` is set for the new canvas.

## What it does

- Left third of the screen: stays in place.
- Middle third: moves by half the extra width.
- Right third: moves by the full extra width, so it keeps its distance from the right edge.
- Top two rows stay, the bottom rows move down, and the rest is scaled in proportion.
- The horizon (and Betaflight's crosshairs and sidebars) go to the new canvas centre.
- Only position values change. Betaflight profile flags are kept.

## Limits

- The result is a good starting point, not a perfect layout. The tool places
  elements by zone and doesn't know how wide each element is, so check the
  preview for overlaps.
- Hidden or disabled elements are left alone unless you tick the box.
- It does not set the canvas size. In Betaflight that comes from the video
  system, and in ArduPilot it is set by `OSDn_TXT_RES` and the OSD type.
- Tested on my own setup (DJI Goggles 3 with VISOR, O4, Betaflight 4.5.x and
  2025 firmware, ArduPilot with MSP DisplayPort). Other setups may need tweaks.

## Alternative for Betaflight

Use an older Betaflight (4.5.x): set `osd_canvas_width` and `osd_canvas_height`
in the CLI, arrange the layout in the configurator, then copy the
`osd_*_pos` lines to the newer firmware.
