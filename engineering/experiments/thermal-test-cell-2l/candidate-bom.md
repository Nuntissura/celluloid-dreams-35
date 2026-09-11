---
title: TTC-2L-A Candidate BOM
project: CD35
document_type: experiment-bom
status: draft
revision: "0.1"
last_updated: 2026-09-11
---

# TTC-2L-A Candidate BOM

This BOM defines component **classes and starting quantities**, not approved production parts. Source actual components before finalizing holes, threads, connector cut-outs, heater bores, or mounting geometry.

## Mechanical / wet cell

| Ref | Qty | Candidate item | Starting requirement |
|---|---:|---|---|
| `WBM-BODY` | 1 | clear fabricated vessel | 200 × 75 × 160 mm internal chamber |
| `WBM-WIN` | 2+ | replaceable metal thermal-window coupons | approx. 180 × 120 mm; first coupon ~0.5 mm stainless |
| `WBM-GSK` | 2+ | window perimeter gasket | water-compatible, replaceable, mechanically compressed |
| `WBM-FRM` | 1 | thermal-window clamp frame | spreads fastener load outside 160 × 100 mm opening |
| `PORT-S` | 1 | suction bulkhead fitting | prototype ~8 mm ID hose connection |
| `PORT-R` | 1 | adjustable return fitting/nozzle | prototype ~8 mm ID hose connection |
| `PORT-D` | 1 | low service drain | simple manual drain into container |
| `TRAY` | 1 | containment tray | covers WBM, window and fluid-port footprint |

## TSM

| Ref | Qty | Candidate item | Starting requirement |
|---|---:|---|---|
| `TSM-BLK` | 1 | aluminium spreader/heater block | target 180 × 120 × 12 mm |
| `TSM-H1..H3` | 3 | replaceable low-voltage heater elements | total selectable range roughly 150–450 W |
| `TSM-TIM` | several | thermal-interface samples | dry contact, thin compliant pad, benchmark compound |
| `TSM-TP` | 1 | plate temperature sensor | same measurement discipline as bath sensors where practical |
| `TSM-CUT` | 1 | independent NC thermal cutoff | hardware interruption of heater bus |
| `TSM-INS` | 1 | rear insulation/guard | prevents accidental contact and reduces rear losses |
| `TSM-BACK` | 1 | service backplate/enclosure | dry wiring and strain relief |

## Docking fixture

| Ref | Qty | Candidate item | Starting requirement |
|---|---:|---|---|
| `DATUM-A` | 1 | flat base datum | repeatable vertical support |
| `DATUM-B` | 1 | round locator | primary lateral location |
| `DATUM-C` | 1 | slotted/diamond locator | rotational location without overconstraint |
| `CLAMP` | 4 | spring-loaded clamp points | total force design space ~400–800 N |
| `FRAME` | 1 | rigid bench frame/base | aluminium extrusion or plate fixture |

## Temperature and level instrumentation

| Ref | Qty | Candidate item | Starting requirement |
|---|---:|---|---|
| `RTD-T1` | 1 | calibrated bath RTD probe | near thermal interface |
| `RTD-T2` | 1 | calibrated bath RTD probe | bulk/control sensor |
| `RTD-T3` | 1 | calibrated bath RTD probe | upper far zone |
| `RTD-TA` | 1 | ambient sensor | room-condition compensation |
| `RTD-REF` | 1 | independent reference thermometer | calibration/verification |
| `LVL` | 1 | removable prototype level cartridge | LOW / NOMINAL / optional HIGH |
| `LEAK` | 1+ | tray water detector | below thermal window / fluid ports |
| `RAIL` | 1 | adjustable sensor rail | movable probe coordinates |

## Fluid loop

| Ref | Qty | Candidate item | Starting requirement |
|---|---:|---|---|
| `PUMP` | 1 | external low-voltage circulation pump | adjustable/repeatable 0.5–5 L/min region |
| `FLOW` | 1 | rotameter or calibrated flow indicator | covers experimental flow range |
| `HOSE` | as needed | clear flexible hose | ~8 mm ID starting size |
| `VALVE` | 1 | flow trim valve if pump alone is insufficient | low restriction |
| `CLAMP-H` | as needed | hose clamps/retainers | reusable serviceable type |

## Electrical and control

| Ref | Qty | Candidate item | Starting requirement |
|---|---:|---|---|
| `PSU-24` | 1 | enclosed 24 VDC PSU | sized for configured heater + pump load with margin |
| `FUSE-H` | 1+ | heater branch fuse/protection | sized to selected heater wiring |
| `CTRL` | 1 | MCU/small PLC/controller | PID, logging, interlocks |
| `RTD-IF` | 4+ channels | RTD acquisition interface | stable, calibratable measurement |
| `SW-H` | 1+ | MOSFET or DC SSR | rated above maximum heater current |
| `E-STOP` | 1 | physical heater/power isolation | bench-accessible |
| `LOGGER` | 1 | USB/SD/PC logging path | timestamped CSV |

## Sourcing rule for this prototype

Before machining or drilling around a purchased part:

1. select the actual component;
2. obtain the manufacturer datasheet/drawing;
3. verify temperature/current/pressure/material ratings;
4. record the manufacturer part number and source;
5. then freeze the mating geometry.

Do not create a custom opening or bracket from a guessed catalogue pattern.