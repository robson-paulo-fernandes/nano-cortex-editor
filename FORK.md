# Additions in this fork

Branch `robson/editor-extras`, on top of [DrD85/nano-cortex-editor](https://github.com/DrD85/nano-cortex-editor).
The version shown in the editor is `v<upstream version>-<FORK_TAG>` (`FORK_TAG` in `index.html`).

- **USB MIDI out** to the Nano, using the documented MIDI list (as catalogued by
  [rixrix/deskop-nano-cortex](https://github.com/rixrix/deskop-nano-cortex), Apache-2.0):
  Program Change 0-63 = preset 1-64, CC 37-41 = FX slot 1-5, CC 42 = tap tempo (used by the Chocolate export; the editor's own tempo dialog taps over Bluetooth), CC 43 = tuner, CC 1 = expression.
  The channel is the Nano's MIDI channel read over Bluetooth (default 1). The Nano takes MIDI only over USB and sends
  nothing back over USB.
- **USB badge** in the top bar (green when the Nano's USB MIDI port is found; click to look again).
- **Without Bluetooth**: the preset arrows send Program Change, the tuner button CC 43, and the connect panel shows
  five switches for the effect slots (CC 37-41). They show what was sent, not the pedal's state.
- **Back up all presets…** (More menu): loads each preset for a moment, reads it like "Export preset file", returns to
  the loaded preset and saves one `nano-backup-*.json` (format `nano-cortex-backup`, version 1). Optionally reads
  switched-off effects by switching them on for a moment (the preset is not saved).
- **Restore from backup…**: for each preset in the file: load it, apply the settings like "Import preset file",
  rename it, and save it with the editor's checked Save. Esc stops a backup or restore after the current preset.
- **M-VAVE Chocolate Plus export…** (More menu): builds a CubeSuite `.fcp` file (the Chocolate's whole
  configuration, Advanced custom mode 1) from a grid of up to 8 groups x 4 switches: presets (Program Change),
  FX slot on/off (CC 37-41, alternating 127/0), tap tempo (CC 42), tuner on/off (CC 43), on the Nano's MIDI channel.
  The Chocolate's jack is set to TRS MIDI out, or to an expression pedal sent to the Nano as CC 1 (0-127).
  Load it with CubeSuite (Import) or Chocolate Studio (Import device backup, then restore), switch on U.
  Layout: nilsjesper/zoom-ms-chocolate-midi `docs/PROTOCOL.md` and matheus3301/chocolate-studio `MAPPING.md`
  (both MIT); the base image is the non-zero bytes of nilsjesper's `fcp/template.fcp` (a CubeSuite export).
  Not yet tested on the hardware with this editor; the expression pedal entry is inferred, not hardware-tested.
  Also Gate, Capture and CAB/IR on/off (CC 34-36, from the Nano Cortex User Manual 2.2.0 Incoming MIDI CC List).
- **Chocolate Studio project…** (same dialog): the same switches as an editable Chocolate Studio project
  (formatVersion 2 JSON), each switch bound to its action of the Studio's `neuraldsp.nano-cortex` 0.1.0 profile,
  two-state switches as "alternate" (first press on), and the Nano's preset names in its preset library.
  Needs a Chocolate Studio with that profile (fork robson-paulo-fernandes/chocolate-studio, branch robson/studio-extras).
- **"Based on" names**: the effect, capture and cab/IR menus list each model with its original in brackets
  ("Green 808   [Ibanez TS808]", "US Prince 65 4   [Fender Princeton 65]"), and a small "Based on …" line under
  the menu names the original of the one selected. From Neural DSP's
  [Nano Cortex device list](https://neuraldsp.com/nano-cortex-device-list); models it names no original for stay plain.
- **Gate card first** in the top row (left on wide windows, on top on narrow ones), as in the signal chain.
- **Unsaved changes on close**: with the loaded preset edited and not saved, closing the Mac app (window or Quit)
  asks Save / Don't Save / Cancel (Save uses the editor's checked Save; if it fails the window stays open).
  In a browser, the browser's own "Leave site?" prompt. Closing still ends the Bluetooth link at once.
- **Save diagnostics…**: editor version, connection state, MIDI ports and the log in one text file.

Scripts next to the repository (in the parent folder): `Gerar app.command` builds the Mac app,
`Atualizar editor.command` brings in DrD85's updates (rebase) and rebuilds.
