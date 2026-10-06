---
id: RISKS
status: draft
updated: 2026-10-06
---

# JoyRide risk register

Hazards and project risks, with candidate mitigations.

- Review the register monthly and at every checkpoint.
- If useful, score each risk 1 to 5 for probability and impact.
- Subsystem FMEAs live in each subsystem's `CYCLE.md` and cite these IDs.
- Link each mitigation to a goal or test where practical, so it gets verified.

| ID | Risk | Cause | Mitigation | Applies | Subsystems | Status |
| --- | --- | --- | --- | --- | --- | --- |
| RSK-001 | Lithium pack fire or thermal runaway | Cell damage, overcharge, short circuit, poor charging practice | Quality cells or a reputable pack, independent protection, main fuse near the pack, fire-safe charging area | Any lithium cell work | PACK | Open |
| RSK-002 | Unintended acceleration | Sensor, firmware, or controller fault | Redundant throttle with a plausibility check, hardware E-stop, wheels-off testing, speed-limit modes | Any powered motion | VCU, DRV | Open |
| RSK-003 | Short circuit or arc at the pack | Tool slip, wiring fault | Insulated tools, covers, fusing, precharge, a second look at wiring before power-up | Any high-current wiring | PACK, NET | Open |
| RSK-004 | Poor ventilation for soldering fumes and lithium handling | The garage and spare bedroom lack good ventilation | Fume extraction or an open-air setup for soldering; ventilation and a fire-safe spot for charging | Before any soldering or lithium work | Project, PACK | Open |
| RSK-005 | Loss of braking | Mechanical failure | Proven mechanical brakes that work independently of the electrics | Integration | CHS | Open |
| RSK-006 | Structural failure | Frame crack, loose mount | Commercial frame, inspection checklist, torque marks | Integration | CHS | Open |
| RSK-007 | Injury while driving | Speed, falls, collisions | Helmet, speed limit, a clear and closed test area | Integration | Project, VCU | Open |
| RSK-008 | Budget overrun | Parts mistakes, scrapped boards, scope growth | Monthly cap, spend checkpoints, small PCB runs | Throughout | Project | Open |
| RSK-009 | Lost interest or scope creep | Too many subsystems at once, slow progress | One cycle at a time, enjoyment check at fold-back, parking-lot backlog, Spark and Bronze as valid stops | Throughout | Project | Open |
