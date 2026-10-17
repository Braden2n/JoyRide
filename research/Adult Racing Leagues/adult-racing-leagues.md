---
id: RESEARCH-ADULT-LEAGUES
status: draft
updated: 2026-10-16
---

# Adult Racing Leagues

Adult kart classes set a comparable baseline for JoyRide's driver mass, kart mass, power, and energy. They replace the youth assumptions in the [eKart baseline paper](../Vehicle%20Dynamics/Analysis%20of%20Vehicle%20Dynamics%20Parameters%20for%20Electric%20Go-Kart%20(eKart)%20Design.pdf) (Golebiowski and Kubiak, 2017). Written 2026-10-16. Values are estimates for the sizing study, not requirements. REQ-SYS-004 stays TBD until the [plant model](../../tools/plant-model/README.md) runs.

## Contents

- [Findings](#findings)
- [Baseline paper review](#baseline-paper-review)
- [Combustion adult classes](#combustion-adult-classes)
- [Electric adult classes](#electric-adult-classes)
- [Driver mass](#driver-mass)
- [Extrapolation for JoyRide](#extrapolation-for-joyride)
- [Sources](#sources)

## Findings

1. Adult electric rental karts are the closest match to JoyRide. They run 48 to 50 V packs, 10 to 14 kW, about 3 to 4 kWh, and reach 40 to 53 mph.
2. Senior race pace is out of reach under 60 V at JoyRide's load. The FIA's 60 V Senior class caps power at 28 kW, which already means over 550 A at 50 V.
3. The paper's "no senior eKart" conclusion came from a regulatory mass limit, not physics. Series have since raised minimum mass for electric classes: Rotax E20 Senior runs at 220 kg against 162 kg for Senior MAX.
4. Racing duty is far heavier than rental duty. Race karts average about 0.83 of peak power over a lap. A 48 V rental kart averages about 4.2 kW.
5. The paper's method carries over with corrections. Add drivetrain efficiency, swap race time for the session length, and replace the race margins with session margins.

## Baseline paper review

The paper sizes battery energy as average lap power times maximum race time, times margins. Average lap power comes from logged engine rpm and the full-throttle power curve, with braking excluded.

| Item | Carries over to JoyRide | Note |
| --- | --- | --- |
| Energy method, `E = P_avg x t x margins` (Eq. 1 to 5) | Yes | Sound first-order method for the sizing model |
| Duty ratio, average to peak power about 0.82 to 0.84 (Mini to DD2) | Yes, as the race-duty upper bound | Micro reads 0.97, since its 6 kW kart is near full power all lap |
| Margins: +20% formation laps and rain, +20% battery fade | Partly | Fade margin carries over. The rain and formation margin becomes a session-variation margin. |
| Race times of 13 to 18 minutes | No | JoyRide uses 30 minutes target and 15 minutes minimum (REQ-SYS-002, [DEC-011](../../docs/decisions/DEC-011-useful-session-definition.md)) |
| Driver and kart mass, 110 to 173 kg total | No | Youth and lightweight senior values; see [Driver mass](#driver-mass) |
| Battery plus drivetrain mass must not exceed ICE drivetrain plus fuel | No | A league parity rule. JoyRide has no class mass limit. |
| Li-ion at 250 Wh/kg now, 350 Wh/kg by 2020 | No | These are cell figures. Shipping kart packs reach about 142 to 178 Wh/kg (BSR-R3). |

Weaknesses to correct in the extrapolation:

- Power from the full-throttle curve treats every non-braking sample as wide open. It is an upper bound on shaft power.
- The model sizes shaft energy, not battery energy. It applies no motor, inverter, or battery efficiency.
- It ignores regenerative braking. Rotax E20 also runs with regen off, so race data gives no regen credit either.
- Table 4 omits the JuniorMax energy. Its own inputs give 14.00 kW x 0.2588 h = 3.62 kWh.
- The worked MicroMax example uses MiniMax numbers (9.29 kW x 0.2397 h = 2.23 kWh). MicroMax is 1.25 kWh.
- Table 5 capacity is about 1.167 times stored energy, not the stated 1.20.

## Combustion adult classes

Total mass includes the driver in race gear. US series publish weights in pounds.

| Series and class | Age | Engine | Peak power | Min. total mass |
| --- | --- | --- | --- | --- |
| Rotax MAX Senior (Global RMC 2025) | 15+ | Rotax 125 MAX | 22 kW (paper) | 162 kg |
| Rotax MAX Senior Masters | 32+ | Rotax 125 MAX | 22 kW (paper) | 175 kg |
| Rotax DD2 | 15+ | Rotax DD2, two-speed | 25 kW (paper) | 175 kg |
| Rotax DD2 Masters | 32+ | Rotax DD2 | 25 kW (paper) | 180 kg |
| CIK-FIA OK (2025) | Senior | 125 cc direct drive | Not stated | 150 kg |
| CIK-FIA KZ2 and KZ2 Masters (2025) | Senior | 125 cc shifter | Not stated | 175 kg and 180 kg |
| SKUSA Pro X30 (2026) | 15+ | IAME X30 | About 22 kW (30 hp, IAME via Sodikart) | 360 lb (163 kg) |
| SKUSA KA100 Senior (2026) | 15+ | IAME KA100 | About 16 kW (22 hp) | 355 lb (161 kg) |
| SKUSA KA100 Master (2026) | 30+, or 21+ at 200 lb driver | IAME KA100 | About 16 kW | 390 lb (177 kg), 400 lb (181 kg) for 21+ |
| SKUSA Pro Shifter (2026) | 15+ | KZ 125 cc | Not stated | 390 lb (177 kg) |
| Briggs LO206 Senior (Texas Sprint Series) | 15+ | Briggs LO206, 6,100 rpm limit | About 6.6 kW (8.8 hp, retailer rating) | 360 lb (163 kg) |
| Briggs LO206 Senior Heavy and Masters (club rules) | 15+ and 35+ | Briggs LO206 | About 6.6 kW | 390 lb (177 kg) |

Adult class mass runs 150 to 181 kg total. Masters and heavy classes add 5 to 20 kg over the senior class. The LO206 is the low-power adult class, at about a third of a Rotax Senior.

## Electric adult classes

| Kart or class | Voltage | Peak power | Energy | Mass | Top speed | Session |
| --- | --- | --- | --- | --- | --- | --- |
| CIK-FIA E-Karting Senior (2025) | Max 60 V DC | 28 kW from the pack | Not limited | 175 kg min. total | Not stated | Not stated |
| CIK-FIA E-Karting Junior (2025) | Max 60 V DC | 23 kW from the pack | Not limited | 165 kg min. total | Not stated | Not stated |
| FIA electric karts Group 2, Li-ion (2020) | Up to 400 V | Not stated | Pack max. 22 kg | 175 to 185 kg total | Not stated | Not stated |
| Rotax E20 Senior and Masters (2026) | 350 V nominal | 24 kW | Not published | 220 kg and 224 kg min. total | 135 km/h | Race |
| Blue Shock Race X4, Senior | 96 V | 27 kW from the pack | 5.3 kWh | 110 kg kart | 125 km/h | 18+ min |
| Blue Shock Race X5, Pro | 96 V | 33 kW from the pack | 5.3 kWh | 120 kg kart | 135 km/h | 10+ min |
| BSR-R3 rental kart (2026) | 50.4 V nominal, 58.8 V charge | 10 kW, 12 kW boost | 3.2 or 4.0 kWh, 22.5 kg pack | Not stated | 85 km/h | Rental |
| Blue Shock Race 48 V rental kart | 48 V | Not stated | 35 Ah, about 1.7 kWh | Not stated | 80 km/h | 30+ min, 0.7 kWh per 10 min ride |
| OTL Storm EFD rental kart (K1 Speed) | 48 V | 14 kW | Lead or lithium options | Not stated | 40 mph | Rental |
| Electrathon America (2026) | Any | Any | About 1 kWh, 73 lb lead-acid limit | 180 lb min. driver | Not stated | 1 hour |

Electric class mass sits 25 to 58 kg above the matching combustion class. Electrathon vehicles are streamlined, so they set an efficiency floor rather than a kart baseline.

The CIK-FIA E-Karting rules also define safety hardware that suits REQ-SAF-001: a general circuit breaker, a driver master switch, an emergency stop, pack status lights, and ready-to-move lights. The pack mounts centrally under the steering column.

## Driver mass

US adults in 2015 to 2018 (CDC NHANES, men and women 20 and over, without race gear):

| Group | Mean | 50th | 90th | 95th |
| --- | --- | --- | --- | --- |
| Men | 90.6 kg (200 lb) | 87.4 kg | 119.4 kg | 130.3 kg (287 lb) |
| Women | 77.5 kg (171 lb) | 73.1 kg | 105.3 kg | 119.6 kg (264 lb) |

- Adult kart classes assume a 70 to 100 kg driver. Rotax Senior's 162 kg total leaves at most about 90 kg for the driver, given the 70 kg CIK-FIA kart minimum.
- Rental operators cap drivers near 300 lb (K1 Speed).
- REQ-SYS-003's 300 lb (136 kg) minimum sits just above the 95th percentile man before gear. Its 400 lb target is far beyond it.

## Extrapolation for JoyRide

The method follows the paper, with battery energy `E_batt = P_avg x t / eta x 1.2 x 1.2`. Two duty anchors bracket JoyRide:

- Rental duty: 4.2 kW average at the battery, measured by Blue Shock Race. No efficiency division applies.
- Senior race duty: 18.44 kW average shaft power (paper, SeniorMax). Assumed `eta` is 0.85 for motor, inverter, and pack. The plant model must replace that assumption.

| Duty | Session | Energy used | With 1.2 x 1.2 margins | Pack mass at 142 to 178 Wh/kg |
| --- | --- | --- | --- | --- |
| Rental | 15 min | 1.05 kWh | 1.5 kWh | 8 to 11 kg |
| Rental | 30 min | 2.1 kWh | 3.0 kWh | 17 to 21 kg |
| Senior race | 15 min | 5.4 kWh | 7.8 kWh | 44 to 55 kg |
| Senior race | 30 min | 10.8 kWh | 15.6 kWh | 88 to 110 kg |

The rental result checks out against hardware. A 3.0 kWh need fits the BSR-R3's 3.2 kWh standard pack.

Load correction: those anchors assume a 70 to 100 kg driver. A 136 to 181 kg JoyRide driver (REQ-SYS-003) on a 110 to 140 kg kart gives 1.5 to 1.9 times a Rotax Senior's 165 kg. The kart range spans the BSR X4 (110 kg) and Rotax E20 (142 kg, Rotax product page). Rolling and acceleration loads scale with mass, but aerodynamic drag does not. Linear scaling is therefore an upper bound.

Power under the 60 V ceiling (REQ-SAF-002) is current-limited:

| Peak power | Current at 50.4 V | Current at 44 V (low charge) |
| --- | --- | --- |
| 10 kW | 198 A | 227 A |
| 14 kW | 278 A | 318 A |
| 28 kW | 556 A | 636 A |

The BSR-R3 pack limits discharge to 250 A, which matches its 10 to 12 kW rating. A 45 mph target (72 km/h) sits inside the rental range of 40 to 53 mph.

Suggested baseline for the sizing study: an adult electric rental kart, at 48 to 50 V nominal, 10 to 14 kW peak, and 3 to 4 kWh. Scale it for JoyRide's driver mass. Use the senior race anchor only as an upper-bound case.

## Sources

Local copies, accessed 2026-10-16:

| File | Used for |
| --- | --- |
| [Global Rotax MAX Challenge Sporting Regulation 2025](Global%20Rotax%20MAX%20Challenge%20Sporting%20Regulation%202025.pdf) | Rotax age and minimum weights, including E20 |
| [Global Rotax MAX Challenge E20 Technical Regulation 2026](Global%20Rotax%20MAX%20Challenge%20E20%20Technical%20Regulation%202026.pdf) | E20 power, voltage, chassis, regen off |
| [CIK-FIA Karting Technical Regulations 2025](CIK-FIA%20Karting%20Technical%20Regulations%202025.pdf) | OK, KZ2, and E-Karting weights; 60 V and 28 kW limits; e-kart safety hardware |
| [FIA Electric Karts Technical Regulations 2020](FIA%20Electric%20Karts%20Technical%20Regulations%202020.pdf) | Group 2 Li-ion mass and battery limits |
| [Blue Shock Race Electric Karting League Technical Regulations 2025](Blue%20Shock%20Race%20Electric%20Karting%20League%20Technical%20Regulations%202025.pdf) | BSR-X4 class: 96 V, 27 kW, 400 lb heavyweight split |
| [BSR-R3 Generation 2.5 Electric Rental Kart](BSR-R3%20Generation%202.5%20Electric%20Rental%20Kart.pdf) | 50.4 V rental power, pack energy, mass, current |
| [OTL Storm EFD Kart Technical Data Sheet 2020](OTL%20Storm%20EFD%20Kart%20Technical%20Data%20Sheet%202020.pdf) | 48 V, 14 kW rental kart |
| [CDC Anthropometric Reference Data 2015-2018](CDC%20Anthropometric%20Reference%20Data%202015-2018.pdf) | US adult mass percentiles (Tables 3 and 5) |

Links (pages change each season):

| Link | Used for |
| --- | --- |
| [SKUSA 2026 Pro Tour Classes](SKUSA%202026%20Pro%20Tour%20Classes.webloc) | US X30, KA100, and shifter weights |
| [Texas Sprint Series Classes and Rules](Texas%20Sprint%20Series%20Classes%20and%20Rules.webloc) | US LO206 and KA100 weights |
| [Blue Shock Race Electric Racing Karts](Blue%20Shock%20Race%20Electric%20Racing%20Karts.webloc) | BSR X1 to X5 specifications |
| [Blue Shock Race Electric Rental Go-Kart](Blue%20Shock%20Race%20Electric%20Rental%20Go-Kart.webloc) | 0.7 kWh per 10 minute ride |
| [FIA World Motor Sport Council October 2025 Updates](FIA%20World%20Motor%20Sport%20Council%20October%202025%20Updates.webloc) | Approval of 60 V Junior and Senior e-karting |
| [Rotax E20](Rotax%20E20.webloc) | E20 product page |
| [Electrathon America Handbook 2026](Electrathon%20America%20Handbook%202026.webloc) | 1 hour energy-limited format, 180 lb driver |
| [Motorsport UK Electric Kart Tender Supplement](Motorsport%20UK%20Electric%20Kart%20Tender%20Supplement.webloc) | 48 V nominal, 60 V max youth powertrain spec |
| [K1 Speed Pricing and Driver Limits](K1%20Speed%20Pricing%20and%20Driver%20Limits.webloc) | 300 lb rental driver cap |
| [IAME KA100 Engine - Karting Australia](IAME%20KA100%20Engine%20-%20Karting%20Australia.webloc) | KA100 22 hp rating |
| [Briggs and Stratton LO206 Information - KartSport NZ](Briggs%20and%20Stratton%20LO206%20Information%20-%20KartSport%20NZ.webloc) | LO206 rev limit and class use |

Not saved: the X30 30 hp rating (Sodikart X30 product page), the LO206 8.8 hp rating (90Racing listing), and the LO206 Senior Heavy 390 lb weight (Road America Karting Club 2024 class structure).
