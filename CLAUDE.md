# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

Single-file vanilla HTML/CSS/JS project — no build step, no dependencies, no package manager.

## Running

```bash
open galaxy.html        # macOS
```

Or drag `galaxy.html` into any browser.

## Architecture

`galaxy.html` is a self-contained Canvas 2D particle simulation:

- **`Particle` class** — each particle tracks position, velocity, trail history, color (from a fixed palette), and lifetime. Particles wrap at canvas edges and decay over time; dead ones are replaced to keep a steady count of ~320.
- **Physics modes** (`attract` / `repel` / `orbit`) — applied each frame as a force toward/away from the mouse cursor. A global subtle spin force is always active regardless of mode.
- **Rendering pipeline** — each frame: fade background → draw mouse aura → draw connection lines between nearby particles (capped at 200 pairs, max distance 90px) → update + draw particles → draw center nebula pulse.
- **`addBurst(x, y)`** — spawns 120 short-lived fast particles for click explosions.
