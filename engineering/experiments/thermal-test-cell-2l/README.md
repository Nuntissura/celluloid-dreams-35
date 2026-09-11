---
title: CD35 2 L Instrumented Thermal Test Cell
project: CD35
document_type: experiment-design
status: draft
revision: "0.1"
last_updated: 2026-09-11
related_issue: 3
related_spec_baseline: "0.3.0"
---

# CD35 2 L Instrumented Thermal Test Cell

This directory defines the first physical thermal prototype for CD35. It is **experimental evidence**, not an authoritative product specification.

The purpose of the rig is narrow: determine whether a removable `WBM` can dock against a dry `TSM` through a repeatable conductive interface while external circulation keeps a nominal 2 L bath thermally uniform around the C-41 developer operating condition.

## Prototype identity

**Working ID:** `TTC-2L-A`  
**Nominal medium:** water  
**Nominal working volume:** 2.00 L  
**Nominal temperature target:** 37.8 °C  
**Control sensor:** bulk-bath sensor `T2`  
**Architecture under test:** conductive WBM-to-TSM coupling + external circulation

## What is intentionally frozen for this rig

These values define the first test fixture only. They are not product requirements.

| Item | TTC-2L-A starting value |
|---|---:|
| Internal bath width | 200 mm |
| Internal bath depth | 75 mm |
| Internal bath height | 160 mm |
| 2.00 L fill height | 133.3 mm |
| Freeboard at 2.00 L | 26.7 mm |
| Thermal active opening | 160 × 100 mm |
| Thermal window starting thickness | 0.5 mm |
| TSM spreader envelope | 180 × 120 × 12 mm |
| Nominal heater power | 300 W |
| Heater test range | 150–450 W |
| Circulation test range | approximately 0.5–5 L/min |
| Electrical architecture | 24 VDC wet/thermal bench hardware |

The 2.00 L volume follows directly from `200 mm × 75 mm × 133.3 mm ≈ 2.00 L`.

## Design intent

1. The WBM is a simple transparent water vessel with a replaceable metal thermal window.
2. The TSM is dry, removable, and mechanically separate from the bath.
3. The WBM/TSM interface uses repeatable location and repeatable clamping force.
4. The bath is mixed by a separate external circulation loop.
5. Temperature is measured at deliberately different locations so the controller cannot hide a local gradient.
6. Heater power, circulation rate, interface material, and clamping condition remain adjustable.
7. Any leak from the WBM/window interface must fall into containment rather than directly onto energized hardware.
8. Mains power stays outside the wet test zone; the fixture uses low-voltage DC loads where practical.

## File map

- [`mechanical-design.md`](./mechanical-design.md) — bath geometry, thermal window, docking and TSM stack.
- [`instrumentation-control.md`](./instrumentation-control.md) — sensors, circulation, heater control, logging and fault behavior.
- [`candidate-bom.md`](./candidate-bom.md) — prototype component classes and sourcing constraints.

The test procedures and architecture gates remain tracked in GitHub issue #3.

## Non-goals

TTC-2L-A does not attempt to represent final film transport, production WBM dimensions, chemistry compatibility, product enclosure geometry, final couplings, or production electronics. It is a thermal/mechanical evidence fixture.