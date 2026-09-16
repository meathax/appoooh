# Appoooh donor and reference map

The adaptation keeps the MiSTer shell and reusable sound/CPU blocks from the existing core, then replaces the board-specific memory, inputs, graphics, palette, timing and audio control with Appoooh behavior. The hardware behavior is checked against MAME's BSD-3-Clause Appoooh driver; MAME implementation code is not included in the core.

| Area | Source and use | License/provenance |
| --- | --- | --- |
| MiSTer platform | `sys/` and the top-level wrapper follow Template_MiSTer, pinned at `3ea1134cf05d62c2b1db30362277a823d739ced2`. | Per-file GPL-2.0-or-later headers; Intel/Altera generated IP retains its individual terms. |
| Z80 | TV80 `tv80s` and its dependency closure are retained from the existing core; Appoooh clocking, memory, I/O and NMI are implemented in this project. | MIT-style notice, Guy Hutchison (2004); based on T80 by Daniel Wallner. |
| PSGs | Three `sn76496_jt89` instances reuse JT89's register-decoding structure and implement the SN76489A-compatible behavior used by Appoooh, including its divide-by-eight input clock. | JT89 pinned at `b688c5767f4b5910c43f4c2b3909142156a8f584`, GPL-3.0-or-later; the adapter is separately named and covered in `THIRD_PARTY_NOTICES.md`. |
| ADPCM | JT5205 supplies the MSM5205-compatible decoder. Appoooh's sample command, nibble addressing, stop marker and ROM interface are implemented by `appoooh_adpcm_ctrl`. | JT5205 pinned at `cd3cb834764534c205b8e912b1bea26570a36f7d`, GPL-3.0-or-later. |
| Appoooh board behavior | MAME `appoooh.cpp` supplies the ROM map, bank selection, port bits, DIP meanings, graphics layouts, sprite rules, palette PROM decode, priorities and sample protocol. | BSD-3-Clause behavioral reference only; source is not compiled or copied into this core. |
| Similar video-board candidate | The local Arcade-BankPanic MiSTer project was reviewed for structural comparison. Its core is GPL-2-only, so no Bank Panic core RTL was imported into this GPL-3.0-or-later project. | GPL-2-only; used as a donor lead/reference, not as a source donor. Its independently MIT-licensed TV80 code remains usable under its own notice. |

The principal Appoooh-specific RTL is original to this adaptation: `appoooh_memory`, `appoooh_video`, `appoooh_inputs`, `appoooh_bus`, `appoooh_rom_loader` and `appoooh_adpcm_ctrl`. The SN wrapper and JT5205 derived reset/timing files retain their provenance and are documented in `THIRD_PARTY_NOTICES.md`.
