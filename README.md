# Lunar Prototypes – Parametric Design System (Documentation)

This repository documents the conceptual architecture and design philosophy behind Lunar Prototypes, a system for delivering practical, customizable 3D printable designs through a web interface.

This is a documentation-only repository.
It intentionally does not include production code, APIs, or Fusion 360 add-ins.

If you are looking to use the tools described here, visit:
https://lunarprototypes.com

---

## What problem this system solves

Parametric CAD models are powerful, but they assume:
- access to CAD software
- familiarity with parametric modeling
- willingness to manually edit parameters for small, repetitive changes

Lunar Prototypes exists to reduce that friction.

The goal is to allow a user to:
1. Select a practical design
2. Enter a small number of real-world dimensions
3. Receive a ready-to-print STL generated from a parametric source model

This approach prioritizes:
- fit over aesthetics
- reuse of existing hardware
- waste reduction
- practical problem solving over novelty

---

## High-level system overview

At a conceptual level, the system is composed of four parts:

+-------------------+
| User (Browser)    |
+-------------------+
          |
          v
+-------------------+
| Web Interface     |
| - choose design   |
| - enter params    |
+-------------------+
          |
          v
+-------------------+
| API Layer         |
| - validate params |
| - queue job       |
| - orchestrate     |
+-------------------+
          |
          v
+--------------------+
| Fusion 360 Worker  |
| - apply parameters |
| - export STL      |
+--------------------+
          |
          v
+--------------------+
| STL returned       |
| to the user        |
+--------------------+

Each step is intentionally separated to keep concerns clear and failure modes isolated.

---

## Architectural principles

### 1) Parametric models remain the source of truth
All customization originates from a single parametric Fusion 360 file. There are no geometry generators or mesh manipulation shortcuts.

This supports:
- predictable outputs
- consistent tolerances
- easier long-term maintenance of designs

### 2) Web customization is an interface, not a replacement for CAD
The web layer exists to expose intentional parameters only. It does not attempt to replicate CAD functionality.

If a design cannot be safely constrained via parameters, it does not belong in the system.

### 3) Automation should reduce friction, not add magic
The system avoids opaque behavior. Each job follows a deterministic flow:
- validate inputs
- apply parameters
- export STL
- return result

Failures are expected and treated as normal system states.

---

## Technology choices (high level)

Specific implementations may change over time, but the system currently relies on:
- Fusion 360 for parametric modeling and STL generation
- a Python-based API layer for job handling
- containerized services for isolation and repeatability
- a lightweight web frontend for user interaction

Open-source tools are used wherever practical, but this project is not an attempt to build a generalized CAD platform.

---

## What is intentionally not included here

This repository does not include:
- Fusion 360 scripts or add-ins
- API source code
- infrastructure definitions
- security models
- deployment instructions

Those components are tightly coupled to production constraints and are not suitable for public reuse in their current form.

---

## Design philosophy

Lunar Prototypes is built around a few core ideas:
- customization is a delivery method, not the product
- solving a real problem beats printing something clever
- reducing waste is as important as reducing cost
- tools should fit the user’s space, hardware, and constraints

This documentation exists to explain how the system thinks, not to provide a toolkit.

---

## Further reading

- Project site and live tools: https://lunarprototypes.com
- Blog and development notes: https://layeredlearning.blog
- System architecture background: From Idea to Reality with AI (April 2024)

---

## Status

This repository is stable and intentionally low-activity.
Issues and pull requests are not expected to be accepted.

It exists as a reference for those curious about the technical approach behind Lunar Prototypes.
