# Betaflight OSD canvas resizer

Stretches a Betaflight OSD layout from the standard 53x20 canvas to 60x22
for DJI Goggles 3 with VISOR (UHD fonts). Needed because Betaflight 2025+
takes the canvas size from the video system and the configurator can't
place elements beyond it.

## Use
1. In the Betaflight CLI run `get osd` (or `diff all`) and copy the output.
2. Paste it into the tool, keep 53x20 -> 60x22, click Resize layout.
3. Check the preview, paste the `set` lines into the CLI.
4. Verify in the goggles.

Alternative: on Betaflight 4.5.x set the canvas in the CLI, edit the layout
in the configurator and copy the `osd_*_pos` lines to the newer firmware.
