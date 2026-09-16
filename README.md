# Appoooh MiSTer core

This repository adapts the existing MiSTer Z80 arcade-core foundation for Sanritsu/Sega's 1984 Appoooh. The core targets the MiSTer DE10-Nano Cyclone V and is licensed under GPL-3.0-or-later; third-party code and notices are listed in [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md).

## Appoooh hardware

- One Z80 CPU at the MAME-configured 3.072 MHz clock.
- Fixed program ROM at 0000-9FFF and two selectable 16 KiB banks at A000-DFFF. Work RAM occupies E000-EFFF; the F000-FFFF range contains both sprite lists, video RAM and color RAM.
- Two 32×32 8×8 tilemaps, two sprite lists using 16×16 graphics, and the board's palette and character lookup PROMs.
- Three SN76489A PSGs and an MSM5205 ADPCM path, with a 384 kHz source clock and 6 kHz nibble playback.
- Active picture is 256×224 pixels inside a 320×256 raster; Appoooh is presented in its native horizontal orientation.

The memory map, ROM hashes, control bits, graphics layouts, and priority behavior are implemented from MAME's BSD-3-Clause Appoooh hardware reference: [appoooh.cpp](https://github.com/mamedev/mame/blob/master/src/mame/sanritsu/appoooh.cpp). MAME source is not included in this repository.

The reusable CPU, PSG, ADPCM and MiSTer platform sources—and the decision to avoid GPL-2-only donor RTL—are documented in [DONORS.md](DONORS.md).

## ROM set

Place the legally obtained appoooh.zip at rom/appoooh.zip for local testing. The root rom/ directory is ignored by Git. The MiSTer descriptor is [Appoooh.mra](releases/Appoooh.mra); its 23 ROM parts are packed in populated MAME-address order, omitting the empty 0x2000 program-ROM hole. The descriptor's hashes identify the expected files without including ROM data in source control.

## Build

Open [Arcade-Appoooh.qpf](Arcade-Appoooh.qpf) with Quartus Prime Lite 17.0.2 for the DE10-Nano. The project files, core RTL and MiSTer system framework are listed in files.qip. Run Analysis & Synthesis, Fitter, TimeQuest timing analysis, then Assembler before treating a generated RBF as a release candidate.
