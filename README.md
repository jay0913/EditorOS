# EDITOR OS

A modular Claude Skill for professional video-editing direction and practical post-production execution with **DaVinci Resolve + FFmpeg**.

## Install in Claude

1. Download `EDITOR-OS-Claude-Skill.zip`.
2. In Claude, open **Settings → Capabilities → Skills** (wording may vary by product version).
3. Enable Skills if prompted.
4. Upload the ZIP as a custom Skill.
5. Start a conversation with footage attached and say:  
   `Use EDITOR OS. Style: wedding cinematic. Duration: 60 seconds. Format: 9:16. Sound: emotional premium. Captions: none.`

If your Claude interface expects a folder rather than a ZIP, unzip it and upload the `editor-os` folder or its contents according to the current Skills interface.

## What it does

- Routes projects to specialist editing engines.
- Creates a creative treatment, shot plan and edit decision list (EDL).
- Plans sound effects, music, ambience, Foley and dialogue treatment.
- Provides caption, typography, colour, transition and motion-design systems.
- Includes FFmpeg helpers for media inspection and a starter sequential timeline renderer.
- Includes a DaVinci Resolve scripting starter for importing media into a timeline.
- Produces a quality-control report and explicit execution status.

## Requirements for actual rendering

- Python 3.9+
- FFmpeg and FFprobe installed and available on PATH
- Sufficient local disk space and read/write permissions
- For Resolve automation: DaVinci Resolve installed, scripting enabled, and the Resolve scripting Python module configured

Claude Skill instructions do not themselves grant access to your computer, Resolve, files, or shell. Actual rendering requires a Claude environment/tool that can access the uploaded media and execute local scripts. If execution is not available, EDITOR OS prepares the EDL, captions, sound cue sheet and exact handoff instructions instead.

## Quick start

Inspect media:
```bash
python scripts/analyze_media.py "/path/to/media-folder" --output media_report.json
```

Render the example EDL:
```bash
python scripts/render_timeline.py examples/sample_edit.json --output output/editor-os-preview.mp4
```

Create a Resolve timeline from a JSON list:
```bash
python scripts/resolve_import_timeline.py examples/resolve_import.json
```

## Folder map

- `editing-engines/` — specialist creative editing systems
- `sound-design/` — sound design and mixing playbooks
- `captions/` — caption presets and typography rules
- `visual-design/` — colour, transitions, motion and finishing
- `workflows/` — selection, media audit, timeline and QC procedures
- `presets/` — platform/export presets and starter EDL
- `scripts/` — media audit, FFmpeg render and Resolve import utilities
- `examples/` — sample EDLs and cue sheets

## Important limitations

- The FFmpeg renderer is a starter sequential-cut renderer, not a replacement for a full nonlinear editor. It supports ordered clip trims, scale/pad, optional music bed, optional SRT burn-in and output encoding. Complex transitions, motion graphics, advanced colour, retiming, multicam and detailed audio automation should be finished in Resolve.
- The Resolve helper uses the public scripting API when available. It creates/imports a basic timeline; it does not automatically reproduce every Resolve grade, Fusion composition, Fairlight mix or plugin effect.
- Use only music, fonts, SFX and footage you have rights to use.
