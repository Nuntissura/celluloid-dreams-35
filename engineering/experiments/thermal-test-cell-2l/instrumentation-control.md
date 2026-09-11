---
title: TTC-2L-A Instrumentation and Control
project: CD35
document_type: experiment-design
status: draft
revision: "0.1"
last_updated: 2026-09-11
---

# TTC-2L-A Instrumentation and Control

## Measurement goal

The fixture must measure the bath well enough to distinguish a genuinely uniform 37.8 °C bath from a system where one convenient sensor reads correctly while another region is materially hotter or colder.

## TTC-INS requirements

- **TTC-INS-001** — `T1`, `T2`, and `T3` shall use the same temperature-sensor type and acquisition method so spatial differences are not dominated by unlike sensors.
- **TTC-INS-002** — The complete temperature measurement chain shall be calibrated over the 35–40 °C region before thermal-uniformity conclusions are drawn.
- **TTC-INS-003** — The target post-calibration measurement uncertainty for comparative bath work is ≤ approximately ±0.05 °C where practical.
- **TTC-INS-004** — `T2` shall be the normal control sensor for the first tests; `T1` near the thermal interface shall not be used as the sole control sensor.
- **TTC-INS-005** — A dry-side plate sensor `TP` shall measure the TSM spreader temperature.
- **TTC-INS-006** — Ambient air temperature shall be logged for every test run.
- **TTC-INS-007** — Heater command/duty and active power state shall be timestamped with temperature data.
- **TTC-INS-008** — The first rig shall provide an independent hardware thermal cutoff that can interrupt heater power without relying on the application controller.
- **TTC-INS-009** — Low bath level shall inhibit heater operation.
- **TTC-INS-010** — A triggered containment/leak sensor shall remove heater power and stop replenishment/transfer functions; circulation response may be configured according to the leak location.
- **TTC-INS-011** — Raw timestamped data shall be retained in a simple exportable format such as CSV.

## Temperature instrumentation

### Bath probes

Preferred starting class: small stainless-sheathed RTD probes, such as calibrated 4-wire PT100 probes or an equivalent measurement chain demonstrated to meet the experiment uncertainty target.

Do not assume a catalogue accuracy class alone is sufficient. The three bath probes should be calibrated together against a better reference around the actual test temperature.

Starting sensors:

- `T1`: near-interface bath temperature;
- `T2`: representative bulk bath temperature and PID input;
- `T3`: far/upper bath temperature;
- `TP`: dry TSM spreader temperature;
- `TA`: ambient air temperature.

An independent reference thermometer should be used during calibration and occasional verification.

## Heater control

### Electrical architecture

Use low-voltage DC heater hardware for the first wet bench fixture where practical.

Starting target:

- 24 VDC heater bus;
- approximately 300 W nominal heater capability;
- up to approximately 450 W short-duration test capability;
- mains AC confined to an enclosed external power supply away from the drip tray.

At 24 VDC:

- 150 W ≈ 6.25 A;
- 300 W ≈ 12.5 A;
- 450 W ≈ 18.75 A.

Size wiring, fusing, connectors and switching for the maximum configured test current rather than the nominal PID duty.

### Control loop

Use a deterministic PID or equivalent controller with `T2` as the normal process variable.

Log at least:

- setpoint;
- T1/T2/T3/TP/TA;
- heater output percentage or PWM duty;
- active heater channels;
- fault state;
- circulation operating point.

A sample interval around 0.5–1 s is adequate for initial water-bath dynamics; faster sampling is not inherently better if sensor filtering and RTD conversion are slower.

## Independent thermal protection

Provide a normally closed hardware thermal switch or equivalent independent cutoff physically coupled to the TSM heater/spreader assembly.

The exact trip temperature is not frozen until plate-to-bath temperature delta is measured. For the first tests, choose a conservative trip point high enough not to nuisance-trip during normal warm-up but low enough to prevent runaway heating after circulation or control failure.

A one-shot thermal fuse may be added as a final backup, but it does not replace the resettable independent cutoff.

## Level sensing

The thermal experiment only needs reliable protection and repeatability, not a production level-sensor architecture.

Preferred first implementation:

- one removable top-mounted level cartridge;
- `LOW` state below minimum safe heated volume;
- `NOMINAL` state near the 2.00 L line;
- optional `HIGH` state below overflow/freeboard limit.

Float switches, conductive probes, optical sensors, or another simple water-compatible method may be used. The selected prototype method shall not be interpreted as the production WBM sensor choice.

## Leak detection

Place at least one water detector in the containment tray directly below the WBM thermal-window interface and fluid ports.

Fault response:

1. heater power removed immediately;
2. test marked failed/interrupted in log;
3. transfer/replenishment functions disabled;
4. operator alert asserted.

## Circulation loop

### Operating range

Initial target flow range: approximately `0.5–5 L/min`.

For a 2 L bath this represents roughly 0.25–2.5 nominal bath volumes per minute, but actual mixing effectiveness depends strongly on port direction and internal flow pattern.

### Pump

Use an external low-voltage pump whose flow can be varied or throttled repeatably. Pump technology is not being selected for CD35 by this rig.

### Flow measurement

For the first rig, a transparent rotameter is acceptable and may be preferable to adding an electronic turbine sensor. Record the flow setpoint manually in the run metadata. Add electronic flow logging only if the test results show it is useful.

### Initial port direction

Return flow should enter near the upper far corner and sweep toward the thermal side; suction should leave near the lower thermal-side corner. The return nozzle should be adjustable so the effect of direction can be tested.

## Suggested controller implementation

A low-cost prototype can use:

- MCU or small industrial controller;
- multi-channel RTD interface;
- MOSFET/DC SSR heater switching;
- USB or SD-card CSV logging;
- simple physical heater-enable switch;
- hardware emergency power isolation.

The experiment does not select the final CD35 controller platform.

## Data record

Each test run should record a header containing:

- test ID;
- date/time;
- water volume;
- starting water temperature;
- ambient temperature;
- thermal-window coupon ID/material/thickness;
- interface material and thickness;
- docking/clamp setting;
- heater configuration;
- circulation flow setting;
- return-nozzle orientation;
- sensor calibration revision.

Then log timestamped values for all measured channels.

## Fault tests

At minimum validate:

- circulation stopped while heating;
- T2 open/disconnected;
- T2 implausible relative to T1/T3;
- low-level state;
- containment leak input;
- controller output forced high with independent cutoff active;
- loss and restoration of controller power.