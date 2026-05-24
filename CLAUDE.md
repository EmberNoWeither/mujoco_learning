# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is a MuJoCo physics simulator tutorial repository, accompanying a video tutorial series. It covers modeling (MJCF XML), C++ API, and Python API usage of MuJoCo.

## Repository structure

- **MJCF/** — XML-based MuJoCo model definition tutorials (15 chapters). Covers world body, joints, friction, actuators, lights, tendons, sensors, CAD import, equality constraints, defaults, composite objects, flexibles, and keyframes. Each chapter contains `.xml` model files and a `tutorial.md`.
- **CPP/** — C++ API tutorials (8 chapters). Each chapter has a `tutorial.md`, source files (`.cc`), and a CMake-based build.
- **Python/** — Python API tutorials (7 chapters). Each chapter has a `tutorial.md` and `.py` scripts. Mirrors the C++ chapters.
- **extend/** — Advanced/extension topics:
  - `jax/` — MJX (MuJoCo XLA) tutorials including batching, rendering, ray casting, and RL training with APG. Uses Jupyter notebooks.
  - `soft_contact/` — Soft contact modeling with MJCF, C++, and Python.
  - `touch/` — Tactile sensing (rigid and flexible touch pads) via API (not plugins).
  - `plugin/` — MuJoCo plugin (ray caster) demonstrations.
  - `equality/` — Equality constraint examples with C++ and Python.
  - `piper/` — Piper robot touch examples.
  - `mujoco_red_stone/` — Red stone robot model.
  - `deep_camera/` — Depth camera implementation via ray casting.
- **utils/mujoco_thread/** — MuJoCo threading utility.

## Build & run

### C++

MuJoCo must be installed at `/opt/mujoco` (CMake find_package). Each C++ chapter builds independently:

```bash
cd CPP/<chapter-dir>
mkdir -p build && cd build
cmake .. && make
./basic          # basic viewer
```

Some chapters also build a `simulate` target with lodepng support.

### Python

Python scripts run directly. Most require a MuJoCo XML model file as an argument:

```bash
python Python/<chapter-dir>/<script>.py path/to/model.xml
```

MuJoCo Python bindings (`mujoco`) must be installed.

### JAX / MJX

JAX and `mujoco-mjx` required. Notebooks in `extend/jax/` can be run with Jupyter:

```bash
cd extend/jax
jupyter notebook tutorial.ipynb
```

To unset CUDA visible devices: `source unset_cuda.sh`.

## Key dependencies

- MuJoCo >= 3.3.0 (C++ libs at `/opt/mujoco`)
- C++: CMake >= 3.20, GLUT, GL, GLU, GLFW
- Python: `mujoco`, `numpy`
- MJX: `jax`, `mujoco-mjx`
