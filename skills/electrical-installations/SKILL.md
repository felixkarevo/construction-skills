---
name: electrical-installations
description: >
  Electricity, wiring and electronics for building or renovating a house in
  DACH practice, sized from DIN VDE 0100 / DIN 18015 / DIN EN 62305 / DIN EN
  12464 rules (distilled from Kasikci "Planung von Elektroanlagen", Bohne
  "Gebäudetechnik", Fischer "Elektrotechnik", Böker "Grundlagen der elektrischen
  Energietechnik"). Covers: house-relevant electrical fundamentals (three-phase
  P=√3·U·I·cosφ, body-current zones & 50 V touch voltage, transformer u_k%,
  motor starting 5–8·I_N, semiconductor/driver/relay electronics, battery
  chemistries); supply & earthing (voltage levels, Hausanschluss/meter/HAK,
  TN-C-S vs TN-S vs TT vs IT with disconnection matrices and the Zs ≤ U0/(5·I_n)
  ready reckoners, PEN-split rule, equipotential bonding sizes, DIN 18014
  foundation electrode — the irreversible pre-pour items); load planning
  (device connected-load tables, DIN 18015-2 circuit counts 3–7, RAL-RG 678
  equipment levels, diversity-factor tables, Ik'' short-circuit estimate,
  voltage-drop and thermal cable checks with worked examples); distribution
  boards (niches per DIN 18013/43870/43871, 18 mm rail system, D0/NH fuses,
  MCB B/C/K/Z, RCD types AC/A/F/B and the no-single-central-30-mA rule, SPD
  T1/T2/T3 cascade per VDE 0100-443); cable types & wiring methods (NYM/NYY/
  H07V-U/NYIF/NHXH-E30 decoder, DIN 18015-3 installation zones with all
  dimensions, conduit vs plaster-embedded, separations to data/gas/water);
  room protection (bathroom zones 0–3, IP matrix, SELV, kitchen heights,
  laundry/garage/exterior, construction-site supply per VDE 0100-704);
  lightning & surge (EN 62305 classes I–IV with mesh/sphere/down-conductor
  spacing, separation distance s=ki·kc/km·l, bonding bar, cascade Up ladder);
  lighting engineering (lumen method n=Em·A/(Φ·ηLB·ηR) with MF and ηR tables,
  room index, UGR/BAP glare rules, EN 12464-1 lux anchors, lamp/LED data,
  DALI/KNX dimming, emergency lighting per EN 1838); PV/battery/EV/small-wind
  (cell physics & efficiency, yield 850–1050 kWh/kWp·a, −0.4%/K, string Voc
  cold check, VDE-AR-N 4105/4110, storage AC/DC coupling, wallbox RCD type B /
  A+6mA, duct duties per current building law); house networks & automation
  (APL/APG, Cat 5e→7A and fibre, ≤90 m links, pipe rules, KNX/DALI/PoE,
  door intercom ≥3 WE, smoke alarms DIN 14676, EMA grades, smart metering);
  existing installations & renovation (legacy colour codes, TN-C conversion,
  trust-protection doctrine, upgrade priority ladder, VDE 0100-610/0105-100
  test sequence incl. ≥1 MΩ and RCD trip times); one full worked single-family
  example (loads → circuits → Zs → Δu → RCD plan → PV strings → IFC export
  map); and a complete IFC-for-ELT chapter: verified IFC4.3 entity map
  (IfcElectricDistributionBoard, IfcProtectiveDevice incl. CIRCUITBREAKER/
  VARISTOR, IfcSwitchingDevice, IfcOutlet/IfcJunctionBox, IfcCableSegment with
  the full Pset_CableSegment* property list + Qto lengths, IfcLightFixture/
  IfcLamp, IfcSensor/IfcActuator, IfcSolarDevice, IfcElectricFlowStorageDevice),
  Pset_ElectricalDeviceCommon, IfcDistributionPort topology, the
  no-circuit-entity convention (IfcGroup + Pset_Circuit_Ext), ELT IDS rules
  and an IfcOpenShell recipe. Use whenever a house task touches electrical
  supply, wiring, protection, lighting, renewables, ICT or electrical BIM data.
---

# Electrical Installations & Electronics for Building Houses (DACH) — ELT Discipline Skill

> **Simple-first gate (governs how this skill is applied).** Default every choice here to the
> *simplest proven* solution at the agreed standard tier — see the governing skill
> `simple-first-building` (complexity ladder §1). The electrical ladder is short: **230/400 V
> TN-C-S service, DIN 18015-2 circuits under RCD 30 mA protection, B/C breakers, NYM/conduit
> wiring in the 18015-3 zones, foundation earth + SPD** is the "simple" answer for a house;
> bus systems, PV+storage+EV, LPS, IT networks and E30 safety circuits are escalations that
> need a client reason. Deviate **below** the VDE/18015 standard only via the documented
> risk-acceptance machinery (`simple-first-building` §3) — and note that in electrical work a
> downward deviation is mostly *not* contractually available at all, because VDE 0100 is a
> recognized rule of technique whose breach is simultaneously a defect **and** a safety/order
> violation the utility and insurers enforce.

Electricity is the TGA discipline with the least tolerance: mechanical mistakes rattle or leak,
electrical mistakes kill or burn — and the rulebook (DIN VDE 0100 series, DIN 18015, TAB) is law-hardened
through utility conditions, trade law (Handwerksrolle) and insurance. This skill exists to:

1. give **the planning chain with numbers** — from connected loads through circuits, risers,
   breaker/RCD selection, Zs and voltage-drop checks to the utility's connection request;
2. carry the **safety engineering core** (earthing systems, auto-disconnection, equipotential
   bonding, surge, bathroom zones) — the part non-electrical designers must get right *before*
   walls close, because most of it becomes impossible or lethal to retrofit;
3. make the **electronics and ICT layer** explicit (LED drivers, bus systems, PV inverters,
   EVSE, networks) — the loads and signals that decide cross-sections, separations and IFC data;
4. provide a **complete IFC/ELT data chapter** — which entity each component becomes, which
   PredefinedType, which verified `Pset_*`/`Qto_*` fields carry the circuit parameters, so an
   ELT model can be authored or audited without a CAD tool (see `ifcopenshell-bim-authoring`).

German terms stay in parentheses because the installer's schedule (Stromlaufplan, Anlagenblatt),
the utility's forms (Messanschlussbegehren) and the authorities speak German.

## 0. How to use this skill

Use it when the task involves ANY of:

- planning or checking a **house electrical installation**: circuits, distribution board,
  fusing, risers, meter/HAK, load estimate, connection request to the utility,
- **safety questions**: TN-C-S vs TT vs IT, RCD types, Zs/loop impedance, disconnection times,
  equipotential bonding, foundation electrode, surge protection, bathroom/wet-room zones,
- **wiring decisions**: cable type (NYM/H07V-U/NYY/NHXH), installation method (conduit, Stegleitung,
  in concrete, buried), DIN 18015-3 zones, chases, boxes, spare capacity, separations to data/gas/water,
- **lighting**: lux/lumen design, luminaire layout, UGR/glare, dimming, emergency lighting,
- **renewables & mobility**: PV sizing and strings, battery storage, wallbox/EV, small wind,
- **ICT & building automation**: network cabling, KNX/DALI, door intercom, alarms, smart metering,
- **renovation**: old TN-C installations, legacy colours, rubber cable, what must be modernized,
- **IFC/ELT modelling**: entities, PredefinedTypes, property sets, cable quantities, circuit data.

**Siblings** (load them when the task crosses over — do not duplicate their scope):

| Skill | Overlap |
|---|---|
| `building-services-tga` §14 | The TGA-coordination view of electrical work (space, risers, routing priority, interfaces to structure/fire/acoustics). This skill is the discipline itself; §14 there stays the coordination summary. |
| `simple-first-building` | Governing complexity ladder and civil-law default/deviation machinery (Rule zero). |
| `fire-protection-building` | E30/E60/E90 classification logic, escape-route rules, shaft fire classes behind the cable details in §9 and §12.3. |
| `building-physics-thermal-moisture` | Moist room classification feeding §9 IP/zone decisions; PV module temperature ↔ roof build-up. |
| `structural-systems` / `concrete-detailing` | Whether chase/sleeve/embedment is allowed, PV patch loads, transformer masses, reinforcement as LPS conductor (§10). |
| `masonry-construction` | Chase geometry (DIN 1053 practice) the electrical zones in §8 must live inside. |
| `openings-windows-doors` | Switch heights vs reveal geometry, roller-shutter drives, door-contact wiring (§13). |
| `building-renovation-refurbishment` | Component-level renovation workflow; §14 here owns the *electrical* existing-installation doctrine. |
| `bim-management` | IFC version discipline (2x3/4/4.3), pset override mechanics, EIR/LOIN — §15 assumes those rules. |
| `ifcopenshell-bim-authoring` | The `ifcopenshell.api` mechanics for writing the §15 recipes headlessly. |
| `ifc-model-validation` | How to prove the ELT export (schema rules + IDS in §15.8). |
| `cost-management-din276` | ELT is cost group 45 (DK 44/45 ⚠ VERIFY edition split); sizing here feeds the quantity framework, not the price. |
| `accessibility-universal-design` | DIN 18040-2 switch/socket heights 85 cm, ≥50 cm from corner (§8) restated there in full audit form. |

## 1. Reality Check — Who Signs What

**This skill produces planning aids, sizing heuristics, safety-rule digests and IFC data schemas.
It is not an electrical design (Elektroplanung) and not permission to touch a network.**

- In Germany, work on the consumer installation may be executed and contracted only by an
  **eintragungsfähiges Elektrotechniker-Handwerk** (Handwerksrolle; § 11a HandwO). The
  **-electrotechnically responsible person** (electrotechnisch verantwortliche Person) of that firm
  signs the installation; the utility connection (Netzanschluss) is exclusively the network
  operator's work. Meter cabinet (Zählerplatz, §7) and everything upstream is **EVU/TAB domain**.
- Every grid connection, meter placement, PV feed-in and (in TT) earthing question is decided by
  the **TAB** (Technische Anschlussbedingungen of the local operator) + **NAV**. Numbers marked
  "utility asks / gives" are form values, not physics — ask early (§5.6).
- The acceptance test protocol per **DIN VDE 0100-610** (§16.4) is what makes the installation
  legal to energize; the utility requires it for meter installation. An agent-produced circuit
  schedule can *feed* it, cannot *replace* it.
- **Nothing in this skill authorizes DIY work at 230/400 V.** Even in countries where self-build
  of parts of a house install is legal, the meter cabinet, RCD/bonding, and energization tests are
  professional acts. If the user is a homeowner asking "can I wire this socket myself": answer the
  knowledge question, state the legal execution duty and the lethal risk (30 mA fibrillation
  threshold band §3.4), and point to the registered installer.
- Austria: ÖNORM E 8001/-8002, NÖNORM, E-Control connection rules; Switzerland: NIV (Niederspannungs-
  Installationsverordnung), SEV/Esti recognition (NIV) ⚠ check current edition — this skill is
  written to German practice; every §-cross reference to "TAB/EVU" needs a local swap (Netzbetreiber
  → Netzbetreiber AT: OeNAP; CH: Esti-Vorschriften) before use.
- Every number marked **⚠ VERIFY** is edition-dependent, garbled in the extraction, or
  jurisdiction-dependent — confirm against the current standard text (VDE 0100-410/430/701,
  DIN 18015, EN 12464, EN 62305, current TAB) before putting it on a drawing. Schema names in §15
  were verified against the buildingSMART IFC4.3 (ADD2) documentation as published 2026 — still
  check the *target schema version* of your project before authoring.
- If the user is treating output as construction-ready — ordering cable from a cross-section "table
  here", energizing a board, submitting a load value to the utility — **say so unprompted**: what's
  missing is the installer's load-group calculation per DIN VDE 0100-420 + selective tripping proof
  (§6.7), the -610 protocol, and the utility's Anschlussbestätigung.

## 2. Which Rulebook Supplies Which Number

Cite the rulebook that carries the number. The law layer (EnWG/NAV/TAB, building law, trade law)
overhangs the standard layer; the standards of the **DIN VDE 0100 series** are "recognized rules of
technique" — breach = defect + regulatory exposure.

| Question | Rulebook | Key anchors used here |
|---|---|---|
| Voltage levels, network basics | **IEC 60038 / DIN VDE 0100-1** | NS 0.4 kV (230/400 V), MS 6/10/20/30 kV, HS 110, EHS 220/380 kV; MS take-off from ~100–300 kW ⚠ utility-specific |
| System forms (TN/TT/IT), auto-disconnection, touch voltage | **DIN VDE 0100-300 + -410 (IEC 60364-4-41)** | UL 50 V AC; TN 0.4/0.2/5 s; TT 0.2/0.4 s; IT tables 0.4/0.8 s; Zs ≤ U0/(m·In) |
| Overcurrent protection, conductor coordination | **DIN VDE 0100-430** | In ≤ Iz, I2 ≤ 1.45·In, Ia ≤ In ≤ Iz logic, B/C characteristics §6.4 |
| Cable ampacity, installation methods, derating | **DIN VDE 0298-4 / IEC 60364-5-52** | reference Iz, grouping f1, temperature f2 (example pair 0.79·0.79 §5.6) |
| Voltage drop, separation, conductors | **DIN VDE 0100-520 + -540** | Δu% = √3·I·l·cosφ/(κ·A) (3~), κ_Cu ≈ 56; PE/N rules §4 |
| Surge protection | **DIN VDE 0100-443 + -531, EN 62305-4** | T2 mandatory at supply point (new installs), cascade §10.4 |
| Bathrooms, pools, saunas | **VDE 0100-701/-702/-703** | zones 0–3, IP matrix, bonding, 6 cm wall rule §9 |
| Site/temporary, construction, agricultural, EV, PV, storage | **VDE 0100-704/-708/-722/-800** | Baustrom RCD; 722 EVSE RCD type A+6 mA or B; 800 PV/battery §11 |
| Dwelling installation scope & minimums | **DIN 18015-1/-2/-3/-4** | circuits 3–7 by area, socket counts, zones, riser 63/80/100 A, communications per dwelling §6/§8 |
| Comfort tiers | **RAL-RG 678** (private standard) | equipment levels 1/2/3 + *plus* (bus-ready) §7.3 |
| Meters & meter cabinets | **DIN 43870/43871, DIN 18013/18012, VDE-AR-N 4100** | meter centre 1.10–1.85 m (TAB) vs DIN 18013 lintel 1.80 m ⚠; niche table §7.1 |
| Distribution boards | **DIN EN 61439-1/-3 (VDE 0614-3)** | household board ≤1250 A, verified short-circuit rating §6.6 |
| Grid connection of generators (PV, CHP) | **VDE-AR-N 4105 (NS) / 4110 (MS), EnWG §19** | ≤30 kWp standard path ⚠ edition; interruptible feed-in device |
| Lightning protection | **DIN EN 62305-1…-4, DIN 18014, DIN VDE 0185/0101** | classes I–IV: mesh 5/10/15/20 m, sphere 20/30/45/60 m, down-conductor 10/10/15/20 m |
| Lighting levels | **DIN EN 12464-1 (indoor), DIN 5035, ASR A3.4** | office 500 lx UGR≤19 Ra≥80; MF reference 0.67 (offices) §12 |
| Emergency lighting | **DIN EN 1838, DIN VDE 0108-100/-1/-3** | 1 lx escape 1 h ≤15 s; anti-panic 0.5; high-risk ≥15 lx ≤0.5 s §12.3 |
| Testing & documentation | **DIN VDE 0100-610/-612, DGUV? / VDE 0105-100** | test sequence, ≥1 MΩ insulation, RCD 1×/5× trip §16.4 |
| Metering rollout | **MsbG/EnWG (post-NZVG) ⚠ VERIFY thresholds** | basis vs smart metering tiers §13.6 |
| Existing installations | **VDE 0105-100 (operation) + FNN Bestand guidance ⚠ VERIFY title** | trust-protection doctrine §14 |
| IFC entities/psets | **buildingSMART IFC4.3.2 / bsDD** | §15 verified tables |

**Rule 2.1 — one question, one owner.** The installer designs the board; this skill sizes the
*brief* (loads, circuits, zones, reserves, data) and checks a design against the rules. If a
number here and the installer's calculation disagree, the installer's wins — unless it violates a
VDE minimum, in which case both lose.

---

# Part I — Fundamentals and the Supply

## 3. Fundamentals You Actually Need on a House

### 3.1 Voltages, frequencies, DC vs AC risk

Public NS network: **230/400 V, 50 Hz** (IEC 60038; former 220/380 — legacy motors may carry the
old plate). Tolerance ±10% (EN 50160 ⚠ VERIFY band). DC is the newcomer in the house (PV strings
up to 1000/1500 V DC, batteries, USB-C PD 48 V, EV 400–800 V): **DC cannot be "over-zero" — a 65 V
DC arc across a body is already lethal**; DC breakers (e.g. PV string switches) are rated "DC" for a
reason; never substitute an AC device into a DC circuit ⚠ and never trust an isolator without a
printed DC rating.

### 3.2 Single-phase and three-phase power (the formulas every check in this skill uses)

```
Single-phase  S = U·I      P = U·I·cosφ   Q = U·I·sinφ   [VA, W, var]
Three-phase   S = √3·U_l·I_l  →  P = √3·U·I·cosφ, Q = √3·U·I·sinφ
Ohm's/loop    I = U/R,  R = ρ·l/A,  κ_Cu ≈ 56 S·m/mm² (ρ ≈ 0.0178 Ω·mm²/m)
                                  κ_Al ≈ 35 S·m/mm²
```

Planning shorthand (400 V, cosφ≈1): **1 A (3~) ≈ 0.7 kW** (P = √3·400·1 = 692 W); **16 A 3~ ≈ 11 kW;
16 A 1~ ≈ 3.68 kW** — that number is the ceiling of a 230 V circuit in DIN 18015 and of a Schuko
socket. Transformer rule §4.3: `P = √3·U·I·cosφ`.

### 3.3 Power factor and reactive power

Inductive loads (motors, old KVG ballasts: L18 W lamp draws 26 VA, L58 draws 69 VA incl. ballast —
cosφ ≈ 0.42 uncompensated, ≈ 0.95 compensated single/dual; chargers/LED: capacitive, low-power SMPS
push current peaks) draw **Q** without doing work; utility meters register **P in kWh** (Wirkstrom-
zähler) — Q is invisible in the bill but heats cables and trips nothing. House relevance:
(1) compensated/LED everywhere kills the old "power-factor clause"; (2) **harmonics** (3rd): triplen
currents add in the neutral → keep **N = 100% of L** in LED/IT-dominated MFH circuits ⚠ practice
rule, and dimension N on the table per VDE 0100-523 if many SMPS/LED per phase (see §5.7).

### 3.4 What current does to a person (why RCD 30 mA exists)

IEC 60479 (Böker Fig. 5.20 zones, 50 Hz AC, body impedance ~1–2 kΩ wet/dry):
**AC ≤ ~0.5 mA imperceptible · perception ~1–2 mA · let-go ~10 mA · fibrillation zone above
~30–50 mA with time** (Dalziel: IB = k/√t; k70 ≈ 0.157 → ~91 mA at 3 s for 99% of people; Biegelmeier
50–500 mA thresholds by duration). Touch voltage limit **U_L = 50 V AC / 120 V DC ripple-free**; a
person (R ≈ 1 kΩ) across 230 V would carry ~230 mA — lethal within seconds. **RCD 30 mA + <300 ms
(1× IΔn) / <40 ms (5× IΔn)** keeps the product below the fibrillation curve. DC: fibrillation
threshold rises (~2×) but arc damage and the inability to let go invert — treat all DC above 60 V
as AC-equivalent danger in practice. Numbers are physiology, not protection design; the protection
design is §4/§6.

### 3.5 Transformer primer (the MS→NS box at the end of the street)

u_k% (Kurzschlussspannung) is *the* number: **I_k3 = c·U_n / (√3·Z_k)**, **Z_k = (u_k/100)·U_r²/S_r**
(§5.5 worked). Typical distribution transformers 20(10)/0.42 kV: Dyn5/Dyn6, u_k ≈ 4% (≤ 250 kVA) and
6% (400–1000 kVA), P_kr ≈ 0.5–1.5% of S_r, P_0 (no-load) 0.1–0.5% ⚠ VERIFY per type series. One
secondary side = **star with N → 230/400 V**, TN system origin. Cast-resin (Gießharz) units are the
in-building choice (no oil tray, upper floors possible; mass and hum are structural cases — see TGA
§14.9). Electronics: nothing here — transformer = two windings + core; losses and hum rise with flux
density and harmonics.

### 3.6 Motor primer (every pump, fan, hoist, fridge and washing machine)

Squirrel-cage three-phase: **starting current I_A ≈ 3–8×I_N**, starting torque 0.5–2×M_N; a direct-on-
line **5.5 kW motor ≈ 11 A draws 35–90 A** — why (a) utility rules cap direct starts (Böker: allowed
if S < 5.2 kVA or I_A ≤ 60 A ⚠ TAB-specific), (b) **C-characteristic** breakers (trip 5–10×I_n) exist,
(c) star-delta (⅓ current, ⅓ torque), softstarters (phase-control) and VFDs (costliest, best) manage
the rest. Single-phase house motors (pumps, drives) use capacitor start (aux winding). Brushed DC
machines are nearly extinct in buildings; what remains of "electronics" in a motor is the SMPS/VFD
front end (see 3.8). Nameplate: cosφ 0.7–0.85, η 0.75–0.95 (IE3+), I_N = P/(√3·U·η·cosφ).

### 3.7 Electronics in a house — the working minimum (Fischer ch. 2)

- **Diode** (Si p-n): one-way, U_F ≈ 0.7 V; LED variant emits light (U_F 1.8–3.5 V by colour;
  current-limited — a bare LED on 230 V dies instantly; the driver §12.6 *is* the electronics).
  Zener = voltage clamp; Schottky = low-loss; rectifier bridges turn AC→DC in every device.
- **Transistor/MOSFET** = current/voltage-controlled switch; switching supplies (SMPS) chop at 20 kHz–1 MHz
  (efficiency 80–95%, small, with RFI → EMC filter + ferrites); old linear supplies: big, warm, clean.
  **Relay** = the electro-mechanical switch (coil ~12–24 V DC drawing tens of mA ⚠ type-dependent;
  contacts 16–2500 VA ratings; **freewheeling diode across DC coils** — the classic electronics bug);
  Stromstoßrelais (§7.6) is one. **Optocoupler** = galvanic signal isolation (why 24 V bus talks to 230 V power).
- Signals in building control: **0–10 V dimming, 0/4–20 mA analog field signals** (4 mA = live zero),
  dry contacts (potentialfrei!) for fire-alarm interlocks, Reed contacts for door/window sensing (§13.4).
- **Battery chemistries** (storage & drives): lead 2.0 V/cell (6 V/12 V blocks, heavy, 50% DoD,
  200–500 cycles), Li-ion NMC/LFP 3.6–3.7 V nominal (4.2 max / LFP 3.65 max ⚠, DoD 90%,
  3000–6000 cycles, thermal runaway ⇒ BMS mandatory), NiMH 1.2 V, button cells 1.35–3.8 V by chemistry.
  Galvanic series (Li −3.0, Zn −0.76, Cu +0.34, Au +1.5 V) is the corrosion reason copper/steel
  never sit bare in wet earth (§4.6 mixed-metal earth electrodes ⚠ VDE 0100-547 rules).

## 4. Earthing Systems: TN-C-S, TN-S, TT, IT

### 4.1 The vocabulary

N = neutral (return of load), PE = protective earth (touch protection, no load current), **PEN = both**
(split once at the service origin — in German practice: HAK/meter cabinet), **main equipotential
bonding (HPE)** ties PE + PEN + earth electrode + all metal services (water, gas, heating, drainage?,
LPS, antenna, telecom) at one bar (Potentialausgleichsschiene). Colour codes (DIN EN 60445): **PE/PEN
green-yellow, N light blue, L brown (L1), black (L2), grey (L3)**; PEN carries green-yellow with blue
rings at the ends; **legacy (pre-~1970): red = PE (!), grey = N, black = L — a renovation trap (§14).**
In circuits, all poles' conductors travel together (else inductive heating / no fault loop).

### 4.2 The four systems and their acceptance conditions

| System | What it is | German house relevance | Core condition |
|---|---|---|---|
| **TN-C-S** | PEN from transformer, split to N+PE at the house; then separate | *the* German residential standard | split **never before the cut-out**, PEN must not be broken by fuses/switches unless all poles simultaneously (main switch) ⚠ 0100-537 |
| **TN-S** | separate PE from origin (cable) | utility supply side, new cables | same auto-disconnection logic |
| **TT** | house electrode independent of network earth | rural/own supply, gardens; **mandatory RCD** | R_A·I_Δn ≤ U_L = 50 V (30 mA → R_A ≤ 1.67 kΩ; practice demands ≤ 25 Ω at the electrode ⚠ utility/land) |
| **IT** | earth-isolated (or high-impedance), first fault only *alarms* | hospitals (OP), mines, some industrial; NOT houses | insulation monitor + bonding; second fault disconnection: 230/400 V → 0.4 s (N undistributed) / 0.8 s (N distributed); 400/690 → 0.2/0.4; RA·Id small ⚠ Tab VDE-410 |

**Never extend a combined PEN into the installation ("klassische Nullung")** — a broken PEN puts
230 V on every earthed casing; in renovation it is a defect to eliminate at the HAK, not to wire
around. TN-C inside old dwellings = "bestandskräftig" (trust protection §14) but any extension
converts it to TN-C-S with 5-conductor wiring.

### 4.3 Protective bonding sizes (main/supplementary)

Main bonding conductor to services & electrode: **≥ 6 mm² Cu if mechanically protected, 10 mm² if not;
16 mm² where not of metal or not protected against corrosion** ⚠ VDE 0100-540 table (give exact: 540
§544.3.1); supplementary bonding (bathroom): **2.5 mm² with mechanical protection, 4 mm² without
(1.5 mm² if within conduit)**; PE cross-section of circuits: follows table (VDE 0100-540 Tab 54.7:
10 mm² → 4 mm² PE? classic rule: L ≤ 16 mm² → PE = L; 16 < L ≤ 35 → PE 16; L > 35 → PE = L/2 —
⚠ VERIFY edition and give as "equal up to 16, 16 above 16≤35, half above 35").

### 4.4 Foundation earth electrode (Fundamenterder, DIN 18014) — the one-shot decision

Closed ring in the footings of the outer walls: **round steel Ø 10 mm or flat 30 × 3.5 mm (hot-dip
galvanized or copper)**, laid **≥ 5 cm below the footing soffit and ≥ 5 cm from the sides** (concrete
cover all round = corrosion protection; vertical (hochkant) on spacers to avoid honeycombing), field
grid where > ~20 × 20 m bays, movement joints bridged outside the concrete, **connection tabs
(Anschlussfahnen) ≥ 1.5 m loose end to the HAK/PAS and test points brought up at every down-conductor
position if an LPS may ever follow**. Retrofit after the pour = ring electrode in the ground or nothing.
Reinforcement (Stahlfundament/Ringanker erder) may serve if bare-contacted per DIN 18014 — prestressed
steel never. The utility's TAB *require* a foundation electrode; put it in the concrete tender §16.3.

### 4.5 The bonding bar list (what physically ties in)

PE/PEN entry, water (behind meter), gas (behind valve), heating/cooling circuits, metallic drainage,
LPS (down-conductor bond at ground level ≥16 mm² Cu / equiv ⚠ 62305-3), antenna coax shield, telecom, structural metal, underfloor heating loops — each on a
terminal of the HPE. **Plastic pipe is no longer a ground; never rely on it** — leave the loop and
bridge with 6/10 mm².

## 5. From Transformer to Meter: Connection, Loads, the Utility Path

### 5.1 Supply choice

NS 230/400 V (meter cabinet, 3×63 A typical) up to roughly a large MFH/house block; **MS 10/20 kV own
transformer station** from ~100–300 kW and/or MV cable nearby ⚠ (utility decides; thresholds and
costs are TAB/NAR negotiation items — see TGA §14.9 for station rooms). Overhead vs underground entry
(§ Bohne 6.1): mast 4–5 m roof pipe (Dachständer, 1 m to trees/antennas, 36 mm spare duct), wall
anchor, or **cable 60–80 cm deep with 30 cm yellow warning tape, sleeve sloping outward, watertight
seal** — all EVU-routed, baulast owner.

### 5.2 Hausanschlusskasten (HAK) → Zählerplatz → Hauptverteilung

Order: service cable → **HAK/NHN (network fuses NH 3-pole or D0/E27 ⚠ TAB)** → house cable (typically
NYY 4×25…50 mm² CU ⚠ size by utility on load, common 25–35 mm² for EFH) → **Zählerschrank/Platz
(DIN 43870-1 layout, niche DIN 18013: meter centre 1.10–1.85 m per TAB wording ⚠ vs DIN 18013
"Sturzhöhe 1.80 m, Nischentiefe 20–40 cm, Breite ≥ 80 (100) cm" readings differ by edition)** →
main switch (SH load-break or Trenner; 63 A) → protective devices → **Wohnungs-/Hauptverteilung**.
Location rules: HAK/Zähler not in garages, wet rooms, ≥50 kW boiler rooms, explosion-risk rooms,
living rooms or inside flats (MFH), over stairs; accessible, dry, ~0–30 °C, no through-route.
Multi-meter: per dwelling + separate **community meter >2 WE (DIN 18015-1)**; iMSys/smart-gateway
reserve §13.6; separate meter for HP interruptible tariff (Rundsteuer TRE spot) and for storage/EV
⚠ rules shift with §19/§14a EnWG debates — current text before design.

### 5.3 DIN 18015-2 circuits per dwelling (the minimum backbone)

| Living area | Socket+lighting circuits |
|---|---|
| ≤ 50 m² | 3 |
| 50–75 | 4 |
| 75–100 | 5 |
| 100–125 | 6 |
| > 125 | **7** |

**plus one own final circuit for every fixed special load ≥ ~2 kW** (hob 400 V (induction 3.7–11 kW,
"e-stove" 11–14.5 kW), DW, washer/dryer, ironing, DHW heater, fridge-freezer on a circuit
**not behind a shared RCD group** (freezer must survive a bathroom trip), HP, lift, sewage pump,
garage/exterior). Every lighting+socket circuit ≤ **16 A = 3.68 kW**; fixed-device connection box ≥
3.7 kW is 3-pole (or perilex 400 V socket as the exchangeable variant). Socket counts per room by
equipment level: living 5/**10**/12 · kitchen ≥5 double (DIN 18015 minimums), bed/child/work per room
(1/2/3 lighting outlets etc.), bath 2 sockets (one may share mirror luminaire), + telecom/data
counts §13. RAL-RG 678: level 1 = DIN minimum, 2 = standard, 3 = comfort; **\*plus = bus-ready
(DIN 18015-4 functional areas: switching/dimming, scenes, blind control, HVAC control, security)** —
if the client wants KNX later without chase-hell, spec "1plus/2plus" from day one.

### 5.4 Connected loads table (Anschlusswerte, Bohne Tab 6.2 + Kasikci Tab 15.4 — plan inputs)

| Device | 1~ kW | 3~ kW | own circuit |
|---|---|---|---|
| Fridge / freezer | 0.1–0.3 | — | (fridge: own, outside RCD group) |
| Dishwasher | 2.5 | — (3.5) | yes |
| Washer / dryer | 2.2 / 2.1–3.3 | 6.2 | yes |
| Hob 4-ring / full elt stove | ~3.5–5 | **11–14 (16 max)** | 3-pole box 0.20 m high |
| Oven separate | 2.5 | 5.0 | yes |
| Microwave/grill/toaster/coffee | 0.5–3 | — | no |
| DHW under-counter 5–12 l / >15 l | 2.0 / 4.0 | 6.0 | yes |
| Instant water heater (Durchlauferhitzer) | 2.5–8 (> 4.6 kW ⇒ three-phase per 18015 ⚠) | **12/18/21/24/27** | 3-pole |
| Hood, pump, automation | 0.1–0.5 | — | no |
| EV wallbox | 3.7–7.4 | **11 (16 A), 22 (32 A)** | yes, own RCD |
| Heat pump (air, monovalent 6 kW class) | — | 1–2 (elec. aux 2–9 kW) | yes + separate meter |

### 5.5 Load estimate → demand value (what the utility's form asks)

Method (Kasikci ch.15): **P_max = Σ(P_i·g_i)** — connected loads times diversity/diversity factors.

- Outlet circuits planning: **0.2 kW/socket (dwelling) → max 16 sockets per circuit; agriculture 0.4
  → 8; commercial 0.5 → 6**.
- Riser/main for <10 WE with DHW storage: `P = P_H·g_H + 12·n·g_S` kW; with instant heaters
  `P = P_H·g_H + 10·n·g_A + P_DE·g_D`; gS (boilers) 1→1.0, 2→0.72, 3→0.60, 4→0.53, 5→0.47, 6→0.44,
  7→0.41, 8→0.39, 9→0.37, 10→**0.35**; gD (instant) 1→1.0, 2→0.63, 3→0.48, 4→0.38, 5→0.32, 6→0.28,
  7→0.26, 8→0.22, 9→0.20, 10→**0.19**; gF floor-storage 0.9, gZ central store 0.8.
- Whole-building demand factor at the main incoming: **residential ≈ 0.4 of connected** (office 0.7–0.9
  lighting etc. — Kasikci Tab 15.10/15.11). Lighting groups g ≈ 0.85–0.95; socket groups 0.1–0.2;
  lifts 0.7–1.
- **EFH quick band:** without HP/EV ≈ **8–12 kW connected, demand 4–8 kW**; with HP + wallbox + PV:
  14–22 kW connected — the 63 A TN-C-S connection survives (diversity), the load-group calculation
  (VDE 0100-420 with simultaneity) is the installer's signature item; 22 kW EV + 11 kW stove +
  instantaneous DHW at once can force 80–100 A or a load-management system (§11.4).
- Short-circuit: the utility's **Anschlussbestätigung states I_k″** at the connection point. If you
  must estimate: `Z_T = u_k/100·U_r²/S_r`; 630 kVA/6%/0.4 kV → Z = 0.06·0.16/0.63 = **15.2 mΩ** →
  `I_k3 = c·U_n/(√3·Z)` with c ≈ 1.0 → **≈ 15.2 kA** at the LV busbar; cable + source impedance to
  the HAK typically halves it to **4–12 kA** — household boards with **6 kA** breakers are only
  compliant when the incoming fuse/cable limits it (aD/NEOZED 50…63 A chokes fault energy; verify
  cascade tables 61439-3 or use 10 kA devices ⚠ safe default on modern installs: f_B ≥ 6 kA with
  upstream NH/D0 per TAB).
- Ask the utility (Messanschlussbegehren) with: planned kW, meter count, tariff structure (HP meter
  with RLM/TRE ⚠ edition, EV meter), HAK position, cable route — **before the slab**, because the HAK
  and the riser chase are structural reservations (DIN 18012 room or niche, TGA §17.1).

### 5.6 Derating the ampacity you looked up (the two factors people forget)

Iz from VDE 0298-4 assumes 30 °C air / 20 °C soil and isolated circuits. Corrections: **ambient f2**
(40 °C ≈ 0.88 for PVC in air ⚠ read the f2 table; soil temps likewise) and **grouping f1** (e.g. 5 cables
side-by-side on tray → ≈ 0.79; 8 circuits in a duct → ≈ 0.70…0.67 ⚠ use table; Kasikci worked pair
0.79·0.79 = 0.62 → 96 A cable must carry 60 A → upsize). Screed/insulation around NYM in a wall is a
*thermal* decision nobody re-checks at install — route high-load circuits where air moves, or size
one step up. Embedding in concrete = heat-sink for risers (method A), not a free pass.

## 6. The Distribution Board and Its Devices

### 6.1 Physical layout (DIN 43871 / 61439-3, Bohne niche numbers)

Rail **35 mm (TH35)**, unit width **18 mm (TE)**; everything quotes in TE. Household flush boards per
DIN 43871 niche: width **30 cm = 12×17.5 mm**, depth 10 cm, height **39 / 54 / 66 cm for 1 / 2 / 3 rows
of 12** (DIN 18015-2: multi-room flats ≥ 2 rows; more is normal: 2–3 rows for an EFH with PV/EV).
Meter panel per DIN 43870-1 layout (meter centre field, Wandlerfeld if needed, SH/Trenner field,
SPD field, reserve field — with utility all ⚠ TAB forms). Door/label plane for circuit schedule
(Anlagenblatt), no switchboards against sleeping-room walls (switching hum/clicks — TGA §14 noise).

### 6.2 Overcurrent devices

- **MCB characteristic**: B = instantaneous 3–5×I_n (sockets, mixed), C = 5–10× (motors, transformer/
  LED inrush groups — default in many boards; ⚠ check selectivity for large LED banks where B is right),
  K = motor spec (8–12×), Z = electronics (2–3×). Ratings 6–63 A; Neozed D0: 2–63 A, NH 00: 6–100 A
  (fuse-link sizes 00/0a/1… with conductor tables — Kasikci Tab 15.6: 00 6–100 A → 16–50 mm²).
  Coordination rule: I_b (load) ≤ I_n ≤ I_z (cable); tripping verifies via Zs (§6.5).
- **RCD (FI) types** (trip behaviour vs residual waveform): **AC** (sine only — no longer acceptable
  where electronics feed DC residual: EVSE, PV, most SMPS), **A** (sine + pulsing DC — floor for a
  modern house; mandatory ≥16 A 1~ / ≥25 A 3~), **F** (A + smooth DC, audio-frequency), **B / B+**
  (adds smooth DC + 6 mA DC ride-through — **wallboxes, inverters-side circuits**). 30 mA only is
  touch-protection-grade; 100/300/500 mA = fire-protection RCD (optional concept ⚠ not a substitute).
- **Architecture rule (DIN 18015 / 0100-410/531):** a **single central 30 mA RCD for a whole dwelling
  is not permissible**; group RCDs (typical: wet areas + exterior mandatory; per-circuit RCBOs for
  the freezer/HP/EV lines to keep nuisance trips local) — every RCD has downstream MCBs (RCD ≠
  overload protection; RCBO = both in one TE-cheap but bulky).
- **Main switch/load-break (SH/GH)**: isolates all live poles simultaneously, not the PE ⚠ (never
  switch a PE), limits fault energy (current-limiting), selective cascade tables with D0/NH up —
  from manufacturer's board documentation (61439-3).

### 6.3 Selectivity (brief — full theory is industry's)

Same device families down the board are naturally time-selective (melting integral); a mains fuse (NH)
upstream of MCBs is nearly always selective to ≈ several kA via cascade (hersteller table — do not
guess). The house practice: one RCD per group of circuits, per-circuit RCBOs where availability
matters (freezer, pump, PV monitoring, IT equipment). Nothing more is required in a dwelling.

### 6.4 SPD (surge) inside the board

Type 1/2/3 logic §10.4: modern default = **combined T1+T2 (Type I+II) module at the supply point**
(VDE 0100-443: **T2 mandatory at the main distribution for new/re-built installations in DACH; T1
mandatory where an LPS exists**); connection ≥ 2.5 mm² Cu for T2, ≥ 4–6 mm² for T1 branch ⚠ VERIFY
from the device datasheet + 0100-443 Annex; each SPD module = replaceable cartridge, fused ahead
(gG 125 A typical max ⚠ datasheet), status window. Sensitive electronics get T3 at the point of use.

### 6.5 Fault-loop impedance check (the compliance arithmetic)

For every final circuit: **Z_s ≤ U_0 / I_a** with I_a = guaranteed instantaneous trip current
(B character must trip at ≤5·I_n within the 0.4 s window): the ready reckoner at 230 V:

| I_n | B char. Z_s max (0.4 s) | C char. (0.4 s) |
|---|---|---|
| 10 A | 4.6 Ω | 2.3 Ω |
| 16 A | **2.9 Ω** | **1.4 Ω** |
| 20 A | 2.3 Ω | 1.15 Ω |
| 25 A | 1.8 Ω | 0.9 Ω |
| 32 A | 1.4 Ω | 0.7 Ω |

(= 230/(5·I_n) for B, 230/(10·I_n) for C; matches Kasikci Tab 16.5 ⚠ edition). Loop = source (from
§5.5, ~0.1–0.3 Ω at HAK) + L+PE conductor R (2×ρ/A at operating temp 70 °C: ≈ 1.2–1.4× the table R′).
Long 2.5 mm² circuits on C16 are the classic violation: 1.4 Ω budget ≈ 45–55 m of loop — measure at
commissioning (§16.4), don't assume.

### 6.6 Board compliance

Buy boards as **tested assemblies (DIN EN 61439-3, I_pfw 6/10 kA)** — a rail in a box with devices
from five brands has no verified short-circuit rating; the manufacturer's coordination table (fuse
type upstream, busbar current 63–125 A) is part of the delivery documents the installer owes the
owner (also the IFC data source §15).

## 7. Circuit Design Worked Anchors

(All house-relevant; installer's calculation is per VDE 0100-420/-520.)

```
Voltage drop, 3~:  Δu% = √3·I·l·(R'·cosφ + X'·sinφ)/U_n·100 ≈ √3·I·l·cosφ / (κ·A·U) ·100
Voltage drop, 1~:  replace √3·I by 2·I
Planning limit:    ≤ 4% of U_n from supply origin (HAK/meter) to the furthest socket (0100-520
                   practice; VDE Beiblatt 5 length tables; utility may impose stricter §9.2 TAB
                   ladder (load-dependent steps ~0.5–1.5% from the substation; read the
                   current TAB edition ⚠ — ask per connection)
```

Worked: kitchen circuit 2.5 mm², 1~, 16 A, l = 25 m, cosφ=1 → ΔU = 2·16·25/(56·2.5) = **5.7 V = 2.5%** ✓.
Hob 3~, 2.5 mm², 16 A, 30 m, φ≈0 → ΔU = √3·16·30/(56·2.5) ≈ 5.9 V = **1.5%** of 400 ✓.
Thermal short-circuit withstand: **A_min = I_k·√t / k**, k(PVC Cu 70→160 °C) ≈ 115, k(XLPE 90→250 °C)
≈ 143 ⚠ VDE 0103/60909 (a 10 kA, 100 ms shock needs A ≥ 10000·0.316/115 ≈ **27 mm²** for PVC — why
long thin feeders ride on upstream fuse cut <100 ms, not on copper mass; I²t tables of the fuse win).
Neutral: ≥ L up to 16 mm²; 16 < L ≤ 35 → N ≥ 16 mm²; > 35 → N ≥ L/2 ⚠ (0100-523) **but keep N = L
where LED/SMPS share a 3~ circuit** (§3.3). PE never switched/fused alone; N switched only with all
poles (4-pole isolators where multiple supplies/HPs can back-feed ⚠ 0100-537).

## 8. Wiring Methods, Zones and the Physical Route

### 8.1 Cable & conductor type decoder (national + harmonized)

```
H05 V-U  / H07 V-U : harmonized PVC core wire, 300/500 V / 450/750 V, solid (U) / stranded (R) /
                     fine-stranded (K) — pulled into conduit; "NYA" old name (dead for new work)
NYM-J 3G1.5 / 5G2.5: national Mantelleitung, PVC sheath, -J = g/y PE inside, -O without; 300/500 V;
                     the workhorse above/below/behind plaster (NOT in poured dense concrete, NOT
                     exposed in living rooms w/o protection, not in wet rooms as sole method)
NYY-J :      reinforced outdoor cable — buried (0.6 m + warning tape), ducts, facades, ground rings
NYFGbY :     armoured buried (no mechanical protection needed) — utility side/industrial
NYIF / NYIFY "Stegleitung" — plaster-buried flat band wire; dry rooms only; NEVER on wood/
             lightweight/insulation boards/feucht rooms; needs ≥ 4 mm plaster cover (VDE 0100-520)
NSYFYY :     special high-power Steg for instant heaters
N(H)XH.. E30 / NHXH E30: halogen-free fire-resistant (functional maintenance per DIN 4102-12 /
             IEC 60331) — safety circuits (§12.3), escape routes, public buildings
AsiR? single-core halogen-free H07V-K for bus ducts/panels; data: J-Y(St)Y (KNX),
     2×2×AWG24 TP Ethernet (Cat 6/6A/7), coax RG6/11, LWL G.652/G.657.
```

Sizes house-relevant (Cu): 1.5 (lighting/sockets), 2.5 (power circuits, stove 3~16 A), 4 (3~ 25 A,
instant DHW), 6/10 (risers, HP/EV 22–32 A, sub-mains), 16–50 (house→meter, service). Max fuse per
size (quick ladder, ⚠ against VDE 0298 Iz): **1.5 → 16 A; 2.5 → 20–25 A; 4 → 25–32 A; 6 → 32–40 A;
10 → 40–63 A.**

### 8.2 Installations methods and their honest trade-offs

| Method | Replaceable | Chases | Wet rooms | Note |
|---|---|---|---|---|
| **Conduit + H07V-U** (Rohrinstallation) | ✓ pull-through | vertical only in load-bearing <24 cm ⚠ structural; horizontals only within ±40 cm of slab band | plastic tube only | the reference "engineering" answer; needs early decisions (cast in ceiling) |
| **Stegleitung NYIF** | ✗ | none (laid in plaster bed) | ✗ except bathroom zone 3 plastered masonry | cheapest, late-decidable (site marking with client), thin-plaster trap (§ Bohne) |
| **NYM** | partly | 1 cm slit or surface | surface only | retrofit standard; not bare in vibrated concrete |
| **NYY** | ✓ (ducts) | in trench | ✓ | exterior, ground rings, PV fields |
| **Cable tray / ladder, trunking** | ✓ | none | IP-matched | commercial; zones §8.3; fire class §12.3 |

### 8.3 DIN 18015-3 zones (why the drill finds the cable)

Wall: horizontal bands **ZW-o 15–45 cm below finished ceiling**, **ZW-u 15–45 cm above FFL**, kitchen/
work band **ZW-m 90–120 cm**; vertical bands **ZS 10–30 cm from door lock-side reveal (both sides for
two-leaf), from window reveals both sides, from room corners**; diagonals only in conduit with 6 cm
cover, or in light-gauge cavities; ceiling = free route (shortest path OK, schedule it).
**Switches 1.05 m** FFL (barrier-free **0.85 m, ≥ 50 cm from corner**, DIN 18040-2), sockets 0.30 m,
counter band 1.15 m. Kitchen socket height ladder (Bohne): 1.65 hood / 1.30–1.40 task lighting /
1.15 work sockets / 0.60–0.75 microwave-tower taps / 0.30 fridge/freezer/DW / 0.20 hob box; tall-unit
connections reachable above at 2.15–2.25 m — agree with the kitchen planner and draw a wall elevation.
The zones are also the acoustic/fire story: pre-formed vertical chases only ≥24 cm walls (structural
rules: masonry skill §; chase closure is a VOB special service — decide at tender).

### 8.4 Separations (power vs everything else)

- Power vs **copper data**: never same pipe; shared trunk only with ≥ 10 mm clear or a metal divider
  (VDE 0100-520; Bohne: shared ≥6×10 cm chase with Trennsteg OK; coax may share a chase keeping 10 mm).
- Power vs **gas**: no shared shaft or chase (TRGI), parallel minimums per local rules ⚠; power vs
  water/heat: sockets/panels above pipes where possible, ≥ 150 mm parallel to hot pipes.
- Crossings at 90°. Antennas/EMA/GMA lines: dedicated pipes, ≥ 30 cm from 230 V where the security
  standard wants it (VdS/50131). **30 % spare conduits + draw wire in every riser/zone run** —
  retro-chasing RCC/masonry is the failure to prevent (TGA rule).

### 8.5 Boxes, channels and small parts

UP device box **Ø ≈ 60 mm, 40–46 mm deep; junction 70/80 mm, 36/65 mm deep**; volume per conductor
class per DIN VDE 0606 (20 cm³/×?) ⚠ — box count and depth grow with terminal blocks; signal caps
(red tablet) so plasterers find them; compensation rings for tiles/dry build-up; no boxes
back-to-back in classified walls < 14 cm (DIN 4102-4); **bathroom-zone walls: ≥ 6 cm residual wall
behind any box/cable on the other face** (Bohne/DIN 18015-3). Floor boxes/Trassen (non-residential):
subfloor channel grid 1.20–1.80 m, raised floor 14–20 cm construction height, loads per AGI A20
(office 3/6 kN classes). Cable management in false ceilings: tray in the corridor spine, 20–30% fill
(heat, pullability).

## 9. Rooms, Wet Areas, IP, and Special Installations

### 9.1 IP & protection classes (DIN EN 60529)

First digit = solids/finger (2 = 12 mm, 4 = 1 mm), second = water (1 drip vertical, 3 rain 60°,
**4 spray (Waschküche)**, 5 jet (massagedusche), 7 immersion-timed, 8 continuous). Class I = PE
required; II = double insulated (no PE); **III = SELV ≤ 50 V AC/120 V DC from a safety transformer
(two-winding/opto, PELV grounded)** — bathroom shaver supply, low-volt halogen 6/12/24 V (transformer
close to load: 5% over-voltage halves HV-halogen life; NV systems ≤6–8 m from trafo; LED typically
12–48 V DC-DC). Room defaults (Bohne 6.11): dry living **IP20**; bathroom zones 1–2 **IPX4** (IPX5 if
jet cleaning), zone 0 **IPX7** (fitted-in pool lights) / his older table reads IP27 for Wannenbereich ⚠
edition; laundry/unheated cellar **IPX1–4 + AP**; garage **IPX4** (explosion-risk-adjacent rules);
exterior sockets **IP44 on 30 mA RCD**, fixtures IP44–65, unswitched exterior lighting IPX3+.

### 9.2 Bathrooms (VDE 0100-701) — zones and what may live where

Zone 0 inside tub/shower basin; zone 1 above 0 to 2.25 m + (fixed shower head) radius ⚠ edition:
60 cm w/o cubicle vs 120 cm readings differ (current EN 60364-7-701:2020 changed radii — verify);
zone 2 = 60 cm beyond (older), to 2.25 m; zone 3 = beyond, to 2.4 m/3 m ⚠. **Switches, sockets,
junction boxes and concealed wiring forbidden in 0–2** (the 6 cm wall rule §8.5 covers the other face);
230 V socket in 3 only with 30 mA RCD (or SELV/Trafo for shavers); washing machine may *stand* in 2
(IPX4); **supplementary equipotential bonding of tub, all reachable metal (pipes, rail, heating) —
bond before enclosure, coordinate trade sequence**; no 230 V floor-heating mats in zones 0–2;
under-floor circuits may enter from zone 3 wiring route.

### 9.3 Kitchen / laundry / garage / cellar / exterior

Kitchen: 3–5 own circuits (hob, DW, oven/tower, microwave, fridge separate outside RCD), ZW-m band,
counter sockets ≥4 (DIN minimum 5 double per RAL level), pre-wire per kitchen planner elevation.
Laundry: 6 circuits full shared (lighting, sockets, washer, dryer, ironing, water heater), floor
outlet sealed against water, IP21–24 AP or moisture-proofed UP. Cellar (unheated/unvented = "damp
room"): NYM/AP, IPX1 dippers, 230 V sockets on RCD if tools ever plug there (DGUV for shared).
Garage: AP IPX4 devices, lighting ≥ 2 fittings or strip, door-drive circuit, RCD on socket,
**no socket reachable from outside** (crime tooling note Bohne; also fire-load). Exterior: buried
60 cm + tape, 30 mA, dusk/PIR sensors (16 m frontal, 6–8 m lateral, 220°, min 1.5 m to the switched
light; false-trigger mitigation), garden lighting = accent not flood, sockets switchable from inside.

### 9.4 Construction-site supply (VDE 0100-704) — because the build needs power first

Baustellenverteiler via EVU on the contractor's meter (rates higher than household — never tap a
neighbour); every socket behind **RCD 30 mA** (IPX4 minimum devices; hand tools IP2X, welding sets
IP23, lights IPX3), daily test-button check, −25 °C rated devices, split RCD groups so one fault
doesn't kill the site; cranes 5–35 kW, mixers/compressors 2–15 kW, welders ≤25 kW, lighting 2–4 W/m².

## 10. Lightning and Overvoltage (EN 62305 + DIN 18014)

### 10.1 Protection level (LSC/BLK I–IV) and what it means on the roof

Risk assessment per 62305-2 (loss of human life → assembly/heritage/explosive; **plain owner-occupied
EFH: usually "not required" by building law but a legitimate economic choice where PV + network +
exposed position**) → class I–IV: **mesh 5/10/15/20 m, rolling sphere 20/30/45/60 m, effectiveness
98/95/90/80%, down-conductors every 10/10/15/20 m**, >30 m height: horizontal band every ≤20 m
(side-strike protection), >20 m parts ≥1 m²/2 m length tie in; air terminals on ridge/eaves/ chimneys/
dormers (≤30 cm non-metal projections from mesh OK), gutter/metal roof edges as natural component if
thickness & joints qualify; a **Fangstange protects a cone whose angle reads from 62305-3 Fig. (10 m:
45° for I, 65° for IV — higher class → taller rod)**. Use the building's own steel: connected
reinforcement OK (never prestressed), façades, railings.

### 10.2 Down to earth

Down-conductors: Ø8/10 mm rod or 30×3.5 flat Cu/St (Al only where non-corrosive), straight, ≥50 cm
from doors/windows, every rod ≥1 discharge path, **test clamps (Trennstelle) a few cm above grade,
foundation electrode per DIN 18014 with external tabs planned before the pour (§4.4)**. Bond to
every incoming service at ground level on the main bonding bar; **LPS earth ≠ shared with telecom
antenna ground except via coordination** (old rule: separate electrodes ≥20 m? superseded by ring
bonding — follow 62305-3).

### 10.3 Separation distance (why the down-conductor cannot hug the gas pipe)

`s = k_i·k_c/k_m · l` (m; k_i 0.04/0.06/0.07/0.08 by class, k_c current sharing, k_m material —
1 air / 0.5 masonry/…; ⚠ values from 62305-3) — a 10 m conductor, class III, k_c=0.5: s ≈ 0.07·0.5·10/1
= **35 cm in air**. Violations → spark-over = fire/blast: either increase distance, or **bond via
Trennfunkenstrecke (spark-gap; firing rating per the device datasheet ⚠)** which forces equipotential only during the
stroke (used on gas/water entries, PV rails? never on telecom data lines without matching type).
Roof-top PV: mount rows ≥0.5 m from rods/bands per 62305-3 annex (or integrate metal frames into LPS
with gaps/bypass per designer).

### 10.4 Internal protection — the SPD cascade

Stroke energy arrives on *all* incoming lines; 62305-1: **coordinated SPD set mandatory from LSC III**
even without external LPS (TAB echo: "Überspannungsschutz always sensible"). Stages: **T1 (blitzcurrent
10/350; splits the total stroke, e.g. Iimp 12.5–100 kA/pole by class ⚠) → limits ≈1 MV to 1–3 kV;
T2 (8/20, In 20–40 kA, Up ≤1.5 kV) in every sub-board; T3 (Up ≤0.8 kV) at the IT/PV-monitor/EVSE
socket.** Separation ≥10 m cable or manufacturer's decoupling if not coordinated (T1+T2 combinable in
one module); **T2 at the supply point is mandatory by VDE 0100-443 in new installations; T1 in front
of the meter needs utility consent** (in Germany behind HAK/NGü is fine: install behind the main
switch where meter-protection rules allow ⚠ TAB). Data/coax/PV-DC lines: matching SPDs (antenna SPD
grounded to the bar, SAT LNB in-line, LAN panel, PV string DC-SPD at combiner/inverter ⚠ manufacturer
+ exposure). LPZ concept (0A outside, 0B under mesh, 1 after T1/T2, 2 inside) is the vocabulary the
lightning engineer uses with the IT planner; for a house, the practical summary is: one ring, one
bar, one cascade, measured `Up < U_imp of devices (1 kV class II typical)` ✓.

## 11. Generation, Storage, Mobility: PV, Battery, Wallbox, Wind

### 11.1 PV physics→yield numbers that survive vendor slides

Solar cell = big photodiode: **~0.6 V/cell**, 36-cell "12 V module" V_mp ≈ 17–18 V (charge controller
needed), 72-cell ≈ 34–37 V. Efficiencies: amorphous 5–10%, poly 15–20%, mono ~20% (2026 top-Si ~22–24%,
tandems lab ⚠). Global radiation DE (Bohne Tab 6.30 / TGA anchors): Berlin 985, mid ≈ 1100, south DE
~1200–1300 kWh/m²a at 35°S; **specific yield × PR 0.75–0.85 → 850–1050 kWh/kWp·a**; winter share ~25%.
Diffuse fraction 48–57% means east-west/vertical still earns: −2–3% for ±45° azimuth or 20–50° tilt;
**vertical façade ≈ 3/4 of optimum** in winter-leaning mix. Temperature: cell 70 °C surface →
**−0.35…−0.4%/K** power loss; ventilate ≥5 cm behind, UV+70 °C-rated cabling; module ≈ 25–30 kg/m²
wind+dead-load structural case + snow-drift/obstruction shadow ≥60% rule; one shaded cell drags a
whole series string (bypass diodes over 20–24 cells; per-module optimizer or DC-coupled microinverters
where roofs split) — shading plan against future trees/chimneys/vents/railings is a design freeze item.

### 11.2 Strings, inverter, grid

```
Voc_max check (cold): N_modules ≤ V_inv_max / (V_oc·(1+0.0037·ΔT))
  (−0.30…−0.37%/K crystalline Si; ΔT = (T_min−25) → at −10 °C: ×1.13)
  e.g. 40.4 V Voc module on a 1000 V inverter: N ≤ 21 at −10 °C; MPPT window overlap!
I_mp ≤ Isc×1.25 ≤ inverter input; two MPPTs = east-west or roof split;
DC/AC ratio ≤1.3 typical (utility ⚠), >1 pays only with load, not feed-in caps.
```

Inverter = DC→AC via IGBT bridge + HF transformer/LCL filter; **VDE-AR-N 4105 (NS): islanding
detection, max. 13.5 A per phase feed-in rule (historically ⚠ current text), §19 EnWG
Einschalteinrichtung/Rundsteuer (via mMe gateway now), ≤30 kWp = standard-attachment path**,
Marktstammdatenregister + grid-operator form before energizing; AC-side SPD (T2/T3) and DC-side
(§10.4) mandatory; string >600 V DC requires documented DC work safety (arc risk §3.1); fire:
rapid shutdown / optimizer / cable labels per current VdS/FF guidance ⚠ (edition-trap).

### 11.3 Battery storage

Lithium (NMC/LFP) 5–10 kWh EFH band (usable ~90%, LFP 100% ⚠ datasheet), round-trip η 85–92%,
BMS + temperature room (0–35 °C design, never beside the DHW tank's heat), **DC-coupled = one
hybrid inverter, AC-coupled = add a unit to an existing string inverter (retrofit friendly)**;
sizing: ≈ 1 kWh usable per 1 kWp PV, self-consumption jumps from ~30% (no storage) to 60–80%;
backup-capable ("Notfunktion") needs a hybrid inverter with backup port + grid relay ⚠ utility
conditions; installation per current **VDE 0100-800** (PV/BESS) with cell safety per **IEC 62619**
⚠ edition — the older VDE-AR-E 2623 practice is superseded; recycling/registration notes per local. Li-ion room: no sleeping/escape
adjacency debate ⚠ insurance guidance; keep the fire skill's compartment logic if in escape route.

### 11.4 EV charging (VDE 0100-722)

Wallbox 11 kW (3~16 A) is the dwelling default; 22 kW (32 A) needs load proof (§5.5) and often
load management across the board/HP/heat-storage; **RCD at the point: type B, or A + 6 mA DC
detection; built-in DC monitoring inside the EVSE can exempt the external RCD only if the
installation concept documents it** (⚠ current 722 text); own final circuit; cables from the board:
5×6 mm² (16 A) / 5×10 mm² (32 A) typical ⚠ per method; **GEG § 13?/§ 14 logic: new residential
with parking = one cable duct per space; non-residential >... 1 in 5 + 20% power ⚠ VERIFY current
edition and enforcement date before quoting**; in garages, the utility may insist on separate
metering per point (§14a EnWG controllable loads ⚠ pending rules); mounting height ~1.20 m, no
damage-by-car zone, and reserve conduit to the parking even if "no EV yet" — the cheapest line on
the drawing. Load math anchor: +11 kW EV on a 63 A TN-C-S house (≈14.4 kVA demand allowance) is
manageable with diversity; +22 kW + 11 kW stove + 21 kW DHW instantly is not — that is the moment
for load-protection relays (Wächter) or a bigger connection.

### 11.5 Small wind (recognition)

1–10 kW classes; Betz limit 59%, real horizontal 40–50%, vertical 30–40%; **mean wind ≥4 m/s
before a wind expert's report is pointless**; hub above all obstacles by ≥5 m or 20× obstacle distance
(C.A.R.M.E.N.); noise + structure: roof mounts only with vibration decoupling and dynamic check;
winter complement to PV (HP synergy).

## 12. Lighting (Engineering + Electronics)

### 12.1 Quantities

Φ [lm] luminous flux; E = Φ/A [lx] maintained level at desk 0.75 m / traffic 0.2 m / 85 cm reference;
L [cd/m²] (glare source), I [cd] (LVK polars), η = Φ/P [lm/W] (bohr: 10–20 · HV halogen 20–25 ·
TL old 58 W+13 W ballast ≈ 88 lm/W · ELV 180 · LED 90–180 system); Ra (>80 rooms, >90 colour work);
T_c bands <3300 K warm / 3300–5300 neutral / >5300 daylight — **rule: low lux wants warm (≤300 lx
warm), high lux wants cool; ≥1000 lx daylight-white works, dimmed daylight-white reads fahl.**

### 12.2 Level design — lumen method (the IFC-ready calculation)

```
E_m maintained (12464-1): corridor/traffic 100 (UGR28) · canteen 200 · living (practice)
   100–300 · office/reading 500 UGR≤19 U0≥0.4 Ra≥80 · reception 300 · teaching 300–500
   · colour-critical 750–1500 Ra≥90; vertical wall ≥50 lx, ≥75 in meeting rooms; Ez office ≥150.
E_n = E_m / MF      MF = LLMF·LSF·LMF·RSMF; reference MF: 0.80 clean (museums/banks),
   0.67 offices, 0.57 industrial/exterior, 0.50 dirty ⚠ log the assumption.
n = E_m·A / (Φ·η_LB·η_R·MF);  room index k = a·b / (h·(a+b));  h = H − p − h_N (p = pendant drop)
η_R from table (k × reflections high/med/low e.g. k=1 → 0.85/0.77/0.71; k=2 → 1.0/0.91/0.82 ⚠
   use the actual luminaire's data file — DIALux/Relux for real projects).
```

Luminaire layout: rows **parallel to the window**, ≥0.8 m from the façade; second row ~2/3 depth;
spacing/height ratio from manufacturer; ≥2.5 m floor clearance for general; batwing/dark-light for
BAP (≤200 cd/m² above 50°; museum angle 30° from vertical on pictures, 50–150 lx on sensitive objects).
Residential lighting design (Bohne): no single centre outlet — general + task + accent layers,
pendant over table 60 cm above surface, mirror side-lit (shadow-free), staircase = lit tread edges
from the top landing, corridor indirect/row, "preventive" 4-branch ceiling box + blank pipes for
rentals.

### 12.3 Lamp/Luminaire data anchors

Fluorescent legacy (renovation recognition): T8 58 W/1500 mm, 36 W/1200 mm, KVG losses +13 W,
starter 1–2 s, strobe risk near rotating machinery (multi-phase split or HF EVG 30 kHz), MF dip
at cold, mercury waste. LED: driver 12–60 V DC, **junction ≤ 60–80 °C decides life — L80B10/hours
rating**, dimming via DALI/0–10V/PWM/phase-cut matching (wrong trim = buzz/flicker/dead driver),
heat = electronics' enemy, beam is directional (no bare LED in a 360° pendant shade). Emergency
luminaire: single-battery (integrated, + network monitoring), central battery
(legacy 40/60/110/220 V DC/AC bank systems; modern = inverter-based central), **duration 1 h escape, ≤15 s switch-in, ≥15 lx ≤0.5 s at
hazard; EN 1838; VdS-type approvals; monthly test-button/annual protocol duty.** E30 wiring of the
escape/central-battery circuits: fire trunking or ≥115 mm screed cover on the raw slab ⚠ per
Land + fire concept (fire skill owns the class).

### 12.4 Controls

Switch ladder: on/off → interchange (2-way) → cross (3-way) → **Stromstoß (impulse relay: any
number of push buttons, fewer cores — the modern default for multi-control, also for Taster+
automation)**; dimmer (leading/trailing-edge resistive+electronic, **LED needs matched trim**),
sensors: twilight (5–5000 lx set), PIR (7–16 m, 220–270°, time 10 s–18 min, false-trim: fixed mount,
not across windows/heaters), HF/radar (through-material — watch), camera-based presence; DALI:
**≤64 control-gear per bus, addressable groups/scenes, DT8 tunable-white; two 1.5 mm² wires, any
polarity, not mains-rated (basic insulation!) ⚠ verify DALI-2 specifics**; KNX/1-bit/radio retrofit
(EnOcean/Zigbee) as bus layer (§13.5). Daylight-linked + presence = 30–75% office lighting savings
(Bohne), mandatory logic: manual override always available.

## 13. ICT, Building Electronics and Automation

### 13.1 Entrance and pipes (DIN 18015-1, FTZ/DIN EN 50173)

APL/APG (fibre termination) ~1.60 m FFL in a dry accessible room (cellar/technical); pipe from
plot boundary in ≥ 32–50 mm spare PE duct, buried 0.6/0.8 m (path/road), warning band, thermal
shrink seal or waterproof wall core (operator does the sealing ⚠); one **1.5–2 m reserve loop**
behind the APL; communications star to every room. Pipe rules: straight runs ≤ 25 m, ≤15 m with
2 bends to a pull box; replaceable always; **IuK (telecom/data) and RuK (antenna) pipes separate
from each other and from 230 V (shared duct only with ≥10 mm air / metal divider); GMA/BMA lines
own pipes + ≥30 cm from mains**; 30% spare conduits.

### 13.2 Copper and fibre tiers

Cat 5e (100 MHz) legacy · **Cat 6 (250 MHz) minimum new** · Cat 6A (500 MHz, 10GBASE-T, PoE++ heat!)
· Cat 7/7A (600/1000 MHz, S/FTP — Bohne recommends structured Cat 7A for future-proofing) ·
fibre OM1/OM2/OM3/OM4 mm (LED/laser VCSEL 50/125) to APG/room; OS2 singlemode 9/125 to the dwelling
(FTTH standard new-build ⚠ operator), LC/SC/APC connectors; PoE budget: af 13 W → at 25.5 → bt 51 →
type 4/5 up to ~100 W at the PD (cable heating: bundle derating for PoE ⚠). One drop ≈ 90 m
permanent link + 2×3 m patch (channel) — beyond: fibre or another floor cabinet. Room count: ≥1
data point per living/sleep/workspace (RAL-RG678 counts §5.3), ≥1 SAT/radio outlet per ≥1 room,
WLAN coverage planned by AP positions (≈1 ceiling AP per 100–150 m² light construction, fewer
with concrete ⚠ site survey; mesh a last resort), **PoE AP feeds from the network cabinet — power the cabinet from a UPS-
fed circuit if the network must survive outages (door/intercom/alarms)**.

### 13.3 Networks per use (Vormerkliste: keep them on separate physical drops behind the cabinet)

IP data (star, cabinet), KNX-TP (own cable, §13.5), DALI (own), BMA/EMA lines (own, security),
door intercom (IP now — Cat at the door module), antenna (coax/IP), metering bus (S0/Modbus to PV/
storage/EV/WP energy data — **the house's energy-monitoring backbone: meter each generation+storage
+wallbox+HP in the board plan (§5.2 meter reserve) and give the cabinet a free switch port**).

### 13.4 Alarms, intercom, security (DIN VDE 0833/0839, EN 50131)

Door intercom **mandatory ≥3 WE (DIN 18015-2)**; video at the front + gate; EMA grades A(1)/B/C
(VdS) / EN 50131 class 1–4 (house = 1–2, insured high-value 3); PIR curtain/ceiling, Reed contacts
(gap ≤20 mm), glass-break (passive double glazing, radius 1.5 m / acoustic 3.5 m / active all glass),
perimeter only with sabotage loop; **Ruhestrom principle + own pipe net + soldered joints on security
lines, alarm siren 2× ≥3 m high + strobe, max 3 min acoustic, dial-out AWUG/managed service**; BMA
in a house only when required (care homes etc. — fire skill) — smoke alarms **Rauchwarnmelder**
(MBO §48: sleeping + escape rooms, DIN 14676-1/-2, VdS device, networkable radio, 10 y battery life,
annual duty) **the one alarm every renovation touches**. Access: transponder/RFID ≥4 M codes,
motorized locks on schedules, time-of-use logging.

### 13.5 Bus / building automation (DIN 18015-4, VDI 3814)

**KNX**: twisted-pair dedicated bus cable J-Y(St)Y 2×2×0.8 mm (yellow), 29 V DC from a choke,
max 64 devices per line, segment ≤350 m, line ≤1000 m, couplers/repeaters
   extend toward a 5-segment/9,500 m system limit ⚠ verify current topology tables), free/line/star, 1 TP cable ≠ data cable ≠ power; sensors (T, lux, presence), actuators
(switch/dim/blind/heating), logic in the line-coupler/app or visualized; commissioning = ETS project
file → **an IFC-relevant asset: the GA database is the as-built truth for §15 sensor/actuator
objects**. DALI for lights (§12.4). Retrofit wireless: Zigbee/Z-Wave/EnOcean/Matter/Wi-Fi —
battery-free switches (EnOcean) in bedrooms; **decision ladder: DIN-minimum wired (simple) →
1plus bus-ready empty pipes (recommended middle) → full KNX comfort (only on explicit brief)**.
GA levels per VDI 3814 (field/automation/management — a house sits between field and automation,
"smart-home" ≠ GA: energy, blind, scene, HVAC functions, not just app-clicks; VdS/fire interlocks
stay hardwired potential-free, apps are convenience only).

### 13.6 Metering and monitoring (MsbG/ECC ⚠ VERIFY edition after NZVG)

E-Zähler: basis mMe (H+D?) vs iMSys (Smart Meter + Gateway) rollout tiers keyed on consumption
(>6,000 kWh/a ⚠) and feed-in — plan **space for mMe + gateway in every Zählerschrank, LAN drop, and
reserve meter positions for storage/EV/HP** (§5.2); S0/Modbus meters per PV/EV subload; the
gateway feeds utility + own display; sub-metering for rentals/communal
(DIN 18015-1: > 2 WE community separate).

### 13.7 Time/other

DCF77/IP clocks; door-open impulse 12 V/short duty; bell transformers 8/12 V; power-loss behaviour
decisions (LED indicator lamps: emergency wiring or not — §12.3).

## 14. Existing Installations and Renovation (Bestand)

### 14.1 Age diagnosis (what era you are wiring into)

| Era | Tells | Implies |
|---|---|---|
| pre-1930s | cloth, porcelain knobs, 2-wire no-PE | replace on touch |
| ~1930–1970 | rubber/early PVC, **red = PE, grey = N, black = L**, no PE anywhere in some runs (2-conductor lamps!) | convert TN-C→TN-C-S, re-core lamp drops |
| 1970–1990 | NYM/NYIF with gn-ge PE, **TN-C (4-core PEN!) still in some houses**, no RCD, no bonding | add RCD groups + bonding, never extend PEN |
| ~1990–2010 | TN-C-S, partial RCD (bath/exterior), SPDs absent | add SPD T2 on any board opening (§6.4); extend RCD groups as circuits are touched |
| post-2010 | full RCD groups, SPD, zones | usually extendable as-is |

**Trust protection (Vertrauensschutz/Bestandsschutz)** — the doctrine you must state precisely to
clients: an installation legally built to its contemporary rules may *continue to operate* as long
as it stays safe (VDE 0105-100 operation duties, periodic checks); **but every modification,
extension or room conversion must meet today's rules in the touched scope** — and rental/insurance/
utility audits (E-Check ⚠ recommendation, not law, unless ordered) pull it toward current state.
Extensions into old TN-C = convert; old rubber insulation (N-type, "Gummi") = brittle — megger (§14.3)
or replace; aluminium branch wiring ≤ 1960s = re-torque/replace terminations (creep); fuse removal
with pennies and bridged RCDs = live findings to log.

### 14.2 Upgrade priority ladder (what first after a fire/inspection)

1. **touch-protection integrity**: main/supplementary bonding (water/gas/heating/bath), PEN split,
   missing PE to metal parts; 2. **RCD 30 mA** for bathrooms, exterior, cellar; 3. HAK/meter-line
   condition (utility joint visit); 4. **cable cross-sections at modern loads** (1.5 mm² stove
   risers, shared neutrals under two RCDs = trips/fires); 5. SPD cascade; 6. zones/18015-3 (best
   effort, schedule it); 7. circuit documentation (as-built schedule = §15 IFC input); 8. bus-readiness
   (empty pipes in the next open-wall event — the once-per-decade window).

### 14.3 Measuring what you inherited (per VDE 0100-610 / 0105-100, installer instruments)

Continuity of PE + bonding (low-Ω ohm meter, ≥0.2 A ⚠ method), **insulation resistance: 500 V DC,
≥ 1 MΩ LV (250 V for circuits with electronics; SELV/PELV 250 V)**; loop/fault-impedance to each
final circuit vs §6.5 tables; **RCD function: trip at ≤1×I_Δn <300 ms? (AC: 0.3 s at 1×, 40 ms at
5×; A-types with the 2×? half-sine logic ⚠ device-specific), plus pre-trip reading**; phase sequence/
polarity (L/N not swapped at sockets); earth resistance where TT; functional tests; record everything —
existing-installation protocols are the baseline IFC "status=existing" data (§15.9).

## 15. IFC for ELT — Writing Electrical Data into the Model

> Schema facts in §15.1–15.5 were **checked against the buildingSMART IFC4.3.2 (ADD2)
> documentation (official release pages) in 2026**; where an enum has version drift we say
> "verify in target schema". Process rules (LoI, pset override, federation) are the `bim-management`
> skill's; authoring mechanics are `ifcopenshell-bim-authoring`'s; IDS/tooling is `ifc-model-validation`'s.
> **Choose IFC4 minimum, IFC4.3_ADD2 as the rich-ELT target** (IFC2x3 lacks IfcCableSegment/pset
> depth entirely and luminaire/sensor types — do not author ELT in 2x3 unless forced).

### 15.1 The ELT file's shape

One discipline file (ELT) federated against ARC/STR/HLS; spatial tree reused by reference or
re-imported; **IfcSystem per project convention**: at least one system per supply (HAK→meter→
board tree) and typically one `IfcSystem` per distribution board so device members can be grouped
via `IfcRelAssignsToSystem`; storeys carry the elements through `IfcRelContainedInSpatialStructure`;
circuits have **no native circuit entity** (§15.6). Naming/Tag discipline: every device `Name`/`Tag`
= board-circuit id (e.g. `W3-A12` — storey 3, circuit 12) — schedules and IDS rules key on it.

### 15.2 Component → entity → PredefinedType (verified enum names, IFC4.3)

| German object | Entity | PredefinedType / notes |
|---|---|---|
| Hausanschlusskasten / Zählerschrank / Wohnungs-/Unterverteilung | **IfcElectricDistributionBoard** | `CONSUMERUNIT` (dwelling meter+device board), `DISTRIBUTIONBOARD`, `SWITCHBOARD`, `MOTORCONTROLCENTRE`; HAK = CONSUMERUNIT/SWITCHBOARD by convention; **IfcDistributionBoard** (generic, 4.3) also usable |
| Zähler (electricity meter) | **IfcFlowMeter** `ENERGYMETER` (verified 4.3: "an electric meter … measures electrical energy supplied to or produced by a residence") — meter occurrence sits inside the `CONSUMERUNIT` board, `Name='Z1'`; PV-feed-in meter likewise `ENERGYMETER` | meter pset names drift across bsDD versions — pull the current `Pset_FlowMeterType*` from the target schema page, don't hardcode here |
| Lasttrennschalter/Hauptschalter | **IfcSwitchingDevice** | `SWITCHDISCONNECTOR` (+ `Pset_SwitchingDeviceTypeSwitchDisconnector`) |
| Sicherung (fuse link D0/NH) | **IfcProtectiveDevice** | `FUSEDISCONNECTOR` (+ Pset_ProtectiveDeviceTypeFuseDisconnector) |
| Leitungsschutzschalter MCB | **IfcProtectiveDevice** | `CIRCUITBREAKER` (+ **Pset_ProtectiveDeviceBreakerUnitTypeMCB**, Pset_ProtectiveDeviceTypeCircuitBreaker) |
| FI/RCD without overcurrent | **IfcProtectiveDevice** | `RESIDUALCURRENTSWITCH` |
| FI with overcurrent (RCBO) / RCCB | **IfcProtectiveDevice** | `RESIDUALCURRENTCIRCUITBREAKER` (+ TrippingUnit sub-entity `IfcProtectiveDeviceTrippingUnit` if modelled separately) |
| Überspannungsableiter SPD | **IfcProtectiveDevice** | `VARISTOR` (T2/T3 MOV) / `SPARKGAP` (T1 gas) / `EARTHLEAKAGECIRCUITBREAKER` as needed; record type class in pset |
| Wandschalter (rocker) | **IfcSwitchingDevice** | `TOGGLESWITCH` |
| Taster (push / impulse) | **IfcSwitchingDevice** | `MOMENTARYSWITCH` |
| Dimmer | **IfcSwitchingDevice** | `DIMMERSWITCH` |
| Stromstoßrelais / control relay | **IfcSwitchingDevice** | `RELAY` |
| Schütz | **IfcSwitchingDevice** | `CONTACTOR` |
| Not-Aus | **IfcSwitchingDevice** | `EMERGENCYSTOP` |
| Steckdose (Schuko) | **IfcOutlet** | classic `CURRENTCARRYINGHELPERS` family — confirm the exact enum value in the target schema's `IfcOutletTypeEnum` page; outlets are their own occurrence, `Pset_OutletType*` names per schema |
| Daten-/ Telefon-/ TV-Dose | **IfcOutlet** (`DATA`) / **IfcJunctionBox** (`DATA`, `TELECOM`) | coax outlet = Outlet/JunctionBox per convention; `Pset_CoaxialCable` belongs on the *cable* (§15.3), not the outlet |
| Abzweigdose 230 V | no dedicated power-junction entity — **IfcDistributionChamberElement** or omit geometry, carry as schedule row | state the convention in the EIR/IDS |
| Leerverrohrung / Installationsrohr | **IfcCableCarrierSegment** `CONDUITSEGMENT`; trunking `CABLETRUNKINGSEGMENT`; tray `CABLETRAYSEGMENT`; ladder `CABLELADDERSEGMENT` | bend/tee/cross/reducer → **IfcCableCarrierFitting** |
| Kabel/Leitung (NYM, NYY, H07V-U…) | **IfcCableSegment** `CABLESEGMENT` (+ `CORESEGMENT` per-conductor, `CONDUCTORSEGMENT`, `BUSBARSEGMENT` for rails, `WIREPAIRSEGMENT`/`OPTICALCABLESEGMENT`/`FIBERSEGMENT` for data) | psets §15.3; **the Qto Length is your BOQ driver** |
| Leuchte / luminnaire | **IfcLightFixture** (IFC4+; 4.3 keeps it — `IfcLuminaire` does *not* exist in 4.3; the Luminaire/WP lands in later schemas — check if targeting IFC4.4/5) | + **IfcLamp** (4.3, separate!) for the light source |
| Sensor (Bewegung/Präsenz, Lux, Rauch, Temperatur) | **IfcSensor** | `MOVEMENTSENSOR` (presence via MovementSensingType in Pset_SensorTypeMovementSensor), `LIGHTSENSOR` (SetPointIlluminance), `SMOKESENSOR`/`FIRESENSOR`, `TEMPERATURESENSOR` — enum list verified via psets §15.4 |
| Aktor (Jalousieantrieb, Stellantrieb) | **IfcActuator** | `ELECTRICACTUATOR` (+ Pset_ActuatorTypeElectricActuator: ActuatorInputPower, ElectricActuatorType, ControlPulseCurrent) |
| Bus-Controller/Regler | **IfcController** / **IfcUnitaryControlElement** | enum per schema page; convention: KNX line coupler = UnitaryControlElement, application logic = Controller |
| Zeitschaltuhr | **IfcElectricTimeControl** | `TIMEDELAY`/`TIMECONTACT` family — check enum in target schema |
| Elektroherd etc. appliances | **IfcElectricAppliance** | household-appliance psets live in bsDD — resolve the exact `Pset_*` name for the target schema there; always add `Pset_ElectricalDeviceCommon` |
| PV-Modul | **IfcSolarDevice** (4.3) — PredefinedType incl. solar-panel family (verify enum page; ports reference `SOLARPANEL`) | + Pset_SolarDeviceTypeCommon |
| Wechselrichter (inverter) | *no dedicated entity* — de-facto conventions: `IfcElectricGenerator` (USERDEFINED/ObjectType='Wechselrichter', or generator-as-system) **or** part of the IfcSolarDevice system decomposition | document the choice in the EIR; never silently invent |
| Batteriespeicher / USV | **IfcElectricFlowStorageDevice** `BATTERY` / `UPS` (+ Pset_ElectricFlowStorageDeviceTypeBattery: OpenCircuitVoltage, BatteryChargingType…) | enum verified: BATTERY, CAPACITOR, INDUCTOR, RECHARGER, UPS |
| Notstromgenerator | **IfcElectricGenerator** `ENGINEGENERATOR` (+ Pset_ElectricGeneratorTypeCommon: StartCurrentFactor, MaximumPower) | diesel genset room interface: TGA §14.9 |
| Transformator (MS station) | **IfcTransformer** (energy-conversion family) + Pset_TransformerTypeCommon (u_k etc. ⚠ field names per schema) |  |
| Wallbox / EVSE | **IfcElectricDistributionBoard** `USERDEFINED` (ObjectType='Wallbox') *or* **IfcOutlet** with `ObjectType='EV coupler outlet'` *or* part of a **CONSUMERUNIT** sub-board — three live conventions, none schema-native | pick one, state it in the EIR, IDS it (§15.6); carry rated current/voltage + RCD type in `Pset_ElectricalDeviceCommon` |
| Fundamenterder / Erdungsring | **IfcCableSegment** `CONDUCTORSEGMENT` (Function=PE, + Pset_CableSegmentTypeEarthingConductor ResistanceToGround) or linear element |  |
| Potentialausgleichsschiene (PAS) | no schema-native entity — convention: **IfcElectricDistributionBoard** `USERDEFINED` (ObjectType='PAS') or a tagged `IfcCableFitting`/junction object | every bonded service gets a `Pset_CableSegmentTypeEarthingConductor` conductor segment into it; document the convention |
| Blitzschutz Fangleitung/Ableiter | **IfcCableSegment** `CONDUCTORSEGMENT` along a polyline (Function per `PEnum_ConductorFunction` or a custom LPS tag convention) | alternative `IfcReinforcingElement` seen in the wild — pick one convention per EIR |

### 15.3 Cable property sets — the verified data model (§15.3 = the "many IFC parameters" request)

For each **IfcCableSegment** occurrence or type, the 4.3 psets carry exactly what sizing needs:

```
Pset_CableSegmentTypeCableSegment:
  Standard ('NYM-J 5×2.5'), NumberOfCores, OverallDiameter, RatedTemperature, ScreenDiameter,
  HasProtectiveEarth, MaximumOperatingTemperature, MaximumShortCircuitTemperature,
  SpecialConstruction, Weight, SelfExtinguishing60332_1, SelfExtinguishing60332_3,
  HalogenProof (BOOL — escape routes!), FunctionReliable (BOOL — E30 flag!),
  ACResistance, CurrentCarryingCapacity (Iz after derating), DCResistance, MassPerLength,
  MaximumCurrent, MaximumBendingRadius, NumberOfWires, InsulationVoltage, RatedVoltage.
Pset_CableSegmentTypeConductorSegment (single wires): CrossSectionalArea, Function (PEnum
  ConductorFunction: L1/L2/L3/N/PE/PEN), ConductorMaterial, Construction, ConductorShape,
  NominalCurrent, ACResistance, CurrentCarryingCapacity, …
Pset_CableSegmentTypeCoreSegment: CoreIdentifier, SheathColours, LayRatio, StrandingMethod, …
Pset_CableSegmentTypeBusBarSegment: NominalCurrent, IsHorizontalBusbar, CrossSectionalArea, …
Pset_CableSegmentOccurrence: DesignAmbientTemperature, UserCorrectionFactor (=f2),
  NumberOfParallelCircuits (=grouping n), InstallationMethod (enum A1..F),
  DistanceBetweenParallelCircuits, CarrierStackNumber, MountingMethod, IsHorizontalCable,
  IsMountedFlatCable, CurrentCarryingCapacity, MaximumCableLength, PowerLoss, SequentialCode
  — the derating audit trail of §5.6, IN the model.
Qto_CableSegmentBaseQuantities: Length, GrossWeight, CrossSectionArea, OuterSurfaceArea — BOQ.
Pset_CoaxialCable / Pset_SymmetricPairCable / Pset_TelecomCableGeneral / Pset_PatchCordCable /
  Pset_OpticalPigtail — the data-cable equivalents.
```

### 15.4 Devices, boards, luminaires, sensors — verified pset fields to fill

```
Pset_ElectricalDeviceCommon (all distribution devices): RatedCurrent (I_n), RatedVoltage
  (230/400), NominalFrequencyRange (50), PowerFactor, ConductorFunction (enum), NumberOfPoles,
  HasProtectiveEarth, InsulationStandardClass, IP_Code ('IP20'/'IP44'), IK_Code, EarthingStyle,
  HeatDissipation, Power, NominalPowerConsumption, NumberOfPowerSupplyPorts.
Pset_ElectricalDeviceCompliance: ElectroMagneticStandardsCompliance, Explosive..., FireProofing
  StandardsCompliance ('EN 60331 / E30'), LightningProtectionStandardsCompliance — the E30/LPS
  evidence fields (§9/§10).
Pset_ProtectiveDeviceTypeCircuitBreaker / …BreakerUnitTypeMCB / …TypeResidualCurrentSwitch… —
  characteristic, breaking capacity (6/10 kA), I_Δn — fill from the datasheet; occurrence
  Pset_ProtectiveDeviceOccurrence (coordination data).
Pset_LightFixtureTypeCommon: NumberOfSources, TotalWattage (W — the load the §5.5 estimate needs!),
  LightFixtureMountingType (recessed/surface/pendant… enum), LightFixturePlacingType,
  MaintenanceFactor (ties §12.2 MF), MaximumPlenumSensibleLoad / MaximumSpaceSensibleLoad /
  SensibleLoadToRadiant (the heat to the ceiling void / room — coordination-relevant §12.3).
Pset_LightFixtureTypeSecurityLighting (emergency): SecurityLightingType, FixtureHeight,
  SelfTestFunction, BackupSupplySystem, PictogramEscapeDirection, Addressablility.
IfcLamp + Pset_LampTypeCommon: LampType/LampCurrent/LampVoltage/RatedLuminousFlux/ColourRenderingIndex
  /LuminousEfficacy — photometrics live here (§12.1).
Pset_SensorType*: LIGHTSENSOR.SetPointIlluminance; MOVEMENTSENSOR.MovementSensingType/
  SetPointMovement; SMOKESENSOR.CoverageArea/SetPointConcentration/HasBuiltInAlarm;
  TEMPERATURESENSOR.SetPointTemperature — the GA data dictionary mapped onto devices (§13.5).
Pset_ManufacturerTypeInformation / ManufacturerOccurrence, Pset_ServiceLife, Pset_Warranty —
  asset/FO field for handover.
```

### 15.5 Connectivity: ports and "a circuit"

**IfcDistributionPort with `FlowType = ELECTRICAL`** on board/device/outlet/luminaire — 4.3 nests
ports under their host via `IfcRelNests` (the Port Nesting concept: board exposes SOURCE ports,
device SINK/SOURCE pair; port names carry 'L1'..'N'..'PE' / circuit ids). Element-to-element:
`IfcRelConnectsPorts` (port→port) — the schema-correct cable topology; element→cable via
`IfcCableSegment` endpoints attached to ports (or pragmatic `IfcRelConnectsElements`). Real-world
interop warning: most coordinators ignore ports — so **the circuit identity must ALSO live as data**
(§15.6) or every downstream tool "flattens" the ELT file.

### 15.6 Circuits without an entity — the convention table

No `IfcElectricalCircuit` exists. Working conventions (pick one, write it into the EIR):
1. `IfcSystem` per circuit (Name = `W1-L13`), members (breaker, cable, boxes, devices) via
   `IfcRelAssignsToSystem` — graph-rich, tool support spotty;
2. **circuit id in the `Tag`/`Reference` of every member + an `IfcGroup`** (lightweight, survives
   every importer);
3. custom property set **`Pset_Circuit_Ext`** on the circuit system/group carrying the schedule
   payload that IFC-standard psets *don't* model per circuit: `CircuitID`, `Polarity/Phases`,
   `MCB='B16'`, `RCD='A-40/0.03'`, `CableType`, `CableLength_m`, `Iz_A`, `I_n_A`, `Zs_measured_Ω`,
   `Δu_percent`, `Diversity_g`, `ConnectedLoad_kW`, `Function ('Schuko'/'Herd'/'WB11kW')`,
   `EscapeRoute (bool)`, `ReliableFunction (bool)`. That Pset is exactly what §16/§17 audits and
   the utility's load form need — model it once, reuse forever.

### 15.7 Authoring recipe (compact; mechanics in `ifcopenshell-bim-authoring`)

```python
import ifcopenshell, ifcopenshell.api.root as root, ifcopenshell.api.pset as pset
import ifcopenshell.api.aggregate as agg, ifcopenshell.api.system as sysapi
import ifcopenshell.api.type as typ, ifcopenshell.api.unit as unit
f = ifcopenshell.file(schema='IFC4X3_ADD2')                      # + project/site/building/storey
                                                                  #   chain per ifcopenshell-bim-authoring §4
board = root.create_entity(f, ifc_class='IfcElectricDistributionBoard',
                          predefined_type='CONSUMERUNIT', name='HV-W1')
brk   = root.create_entity(f, ifc_class='IfcProtectiveDevice',
                          predefined_type='CIRCUITBREAKER', name='W1-L13', tag='W1-L13')
agg.assign_object(f, relating_object=board, products=[brk])       # or nest/aggregate per EIR choice
ps = pset.add_pset(f, product=brk, name='Pset_ElectricalDeviceCommon')
pset.edit_pset(f, pset=ps, properties={'RatedCurrent': 16., 'RatedVoltage': 230.,
                                      'ConductorFunction': ['L1'], 'NumberOfPoles': 1,
                                      'HasProtectiveEarth': True, 'IP_Code': 'IP20'})
cab  = root.create_entity(f, ifc_class='IfcCableSegment', predefined_type='CABLESEGMENT',
                          name='W1-L13', tag='W1-L13')
# cable parameters: Pset_CableSegmentTypeCableSegment + Pset_CableSegmentOccurrence +
#   Qto_CableSegmentBaseQuantities.Length exactly as printed in §15.3 (create type, then
#   typ.assign_type occurrences, or add psets at occurrence level per the EIR override rule).
grp = root.create_entity(f, ifc_class='IfcGroup', name='Circuit W1-L13')
sysapi.assign_system(f, items=[brk, cab], group=grp)             # circuit convention §15.6
ext = pset.add_pset(f, product=grp, name='Pset_Circuit_Ext');  pset.edit_pset(
  f, pset=ext, properties={'CircuitID':'W1-L13','MCB':'B16','CableType':'NYM-J 3G2.5',
                           'CableLength_m':31.2,'Iz_A':19.,'Zs_measured_O':1.12,
                           'du_percent':2.1,'ConnectedLoad_kW':3.68,'EscapeRoute':False})
```

Every property via `api.run.pset.set_value` with the *exact* names §15.3–15.4 prints; geometry:
cables as polyline sweeps (`Path` rep) or just `IfcPolyline` reference geometry at LOD-B — the ELT
LoIN usually needs route-accurate risers/trunks and representative drops, not each 30 cm of NYM.

### 15.8 ELT IDS rules worth writing (validate per `ifc-model-validation`)

```
cardinality: every IfcCableSegment → Pset_CableSegmentTypeCableSegment.CurrentCarryingCapacity +
  .HalogenProof + .FunctionReliable (escape-route set), Qto...BaseQuantities.Length present.
every IfcProtectiveDevice → Pset_ElectricalDeviceCommon.RatedCurrent, + type set (§15.4).
every IfcLightFixture → Pset_LightFixtureTypeCommon.TotalWattage + NumberOfSources.
every IfcOutlet/IfcSwitchingDevice → Name/Tag matching ^(W\d+-[A-Z]?\d+)$ (§15.6 circuit key).
every IfcElectricDistributionBoard → IfcSystem assignment + Pset_ElectricalDeviceCommon.RatedVoltage.
attr: Luminaire in escape route → Pset_LightFixtureTypeSecurityLighting required;
      IfcSensor/IfcActuator → Pset_SensorType*/ActuatorType* matching its PredefinedType.
classification: link Uniclass/Masterformat/ national scheme consistently (26-... family ⚠ EIR choice).
```

### 15.9 Data exchange in both directions

IFC **out** from the installer's schedules: circuit list → systems + `Pset_Circuit_Ext` (§15.6);
luminaire photometrics (IES/LDT files stay as `IfcExternalReference`, not into psets). IFC **in** to
renovation: §14.3 measured data onto occurrences (`Pset_Condition`/`AssessmentCondition`, property
`Existing=True` + status tags per `construction-freecad-bim` §3.10 Bestand→Neu pattern); to FM:
manufacturer/warranty/service-life psets + port/circuit topology for later tracing. To the GEG
energy balance: TotalWattage + solar/battery/generator psets feed §22 there (TGA skill) — keep
consistent units (W vs kW ⚠ the classic import bug).

## 16. Coordination, Sequencing, Documentation

### 16.1 Sequence in a new build (where ELT can still be fixed cheaply)

```
LOI/EIR ELT scope agreed (§15 conventions)   ← before tender
Utility: connection request, load value, HAK position
Foundation: DIN 18014 earth ring + tabs + bonding stubs   ← irreversible
Basement/slabs: risers, sleeves, subfloor/ceiling routes
Wall build-up: pre-formed chases/boxes/zone bands + conduit
Roof closure: LPS/Fangstangen decision, PV rails + roof penetrations, antenna/CH
Plaster phase: pull-in (Rohrsystem) or Stegleitung embed
Floor build-up: floor boxes/trays (non-res)
Close-up: device installation, board build, bonding connections
Before energization: §16.4 tests → utility meter-in → commissioning logs → as-built IFC
```

Clash specifics (ELT lens): switch rows vs furniture elevations; board vs corridor egress width
(DIN 18012/43870 projection); downlight heat vs timber/I-joist fire ratings; floor boxes vs
underfloor loops (keep clearances ⚠ coordination detail); KNX actuators + DALI power supplies inside boards (heat!).

### 16.2 Tender & VOB reality (German)

Electrical works = VOB/C **DIN 18382** (Elektroinstallationsarbeiten) — chases/closures, openings and
core-drilling are **Besondere Leistungen** (§18.1 TGA echo): schedule them or own them; "Neben-
leistungen des AN" covers simple cut/fill for devices only; Stegleitung vs conduit choice is a
tender decision with acoustic/fire/renovation consequences (§8.2). Interface duties: Schuko/
device-connection box positions with kitchen planner; bonding before enclosure with plumbing;
test tabs with the LPS contractor; PV roof penetration with roofing; **all documented in the
coordination minutes — the electrician is the trade whose decisions get concreted earliest**.

### 16.3 What the design must hand the site (drawings = the IFC's parents)

Location plans per floor (zone bands implicit), circuit & schedule diagrams (board × circuit × cable
× load), riser/single-line (HAK→boards), special rooms (bath zone plan, kitchen elevation, server/
telecom rack layout, PV string plan + combiner diagram), bonding & earth plan (foundation tabs!),
escape-route wiring class list (E30 zones), external lighting/foundation cable routes.

### 16.4 Energize gate — test protocol per VDE 0100-610 (order matters)

1 visual + protective-measure review · 2 continuity (PE, PEN, bonding, LPS) · 3 **insulation
resistance ≥1 MΩ (500 V; 250 V with electronics)** · 4 protective impedance/loop Zs ≤ §6.5 table
· 5 polarity + phase sequence · 6 **RCD: 1× IΔn < 300 ms and 5× < 40 ms** (each device) ·
7 insulation monitor (IT) · 8 earth electrode where TT · 9 functional tests (control, drives,
emergency swap-over, PV protections §11.2 incl. shutdown device) — protocol signed → utility meter
→ owner documentation (single-line + circuit schedule + §14.3 baseline for the *next* renovation
and the as-built IFC §15.9).

## 17. Worked Example — EFH 140 m², HP + PV + Wallbox (the whole chain, one page)

```
Brief: 140 m², air-HP 6 kW, DHW 300 l (2 kW elem), hob 11 kW 3~, EV 11 kW, PV 9.6 kWp south 30°,
storage 10 kWh. System TN-C-S, HAK 3×NH 63 A → house cable NYY 4×25 (utility) → Zählerschrank
(EFH pattern: Zähler + SH + HV) → W3 boards (KG/OG/DG).
1 Circuits (18015-2): area >125 m² → 7 light+socket (each B16 1.5–2.5 mm² in zones)
  + specials: Herd 5G2.5 C16 3~ (11 kW→16 A ✓), Spülmaschine/Wasch/Trockner own 1~ B16/B20,
  Gefriergeräteigener outside shared RCD, HP 5G2.5 B16+C? (inrush→C16), WW-Elem own, Wallbox
  5G4?→ 5G4 mm² C16 w/ RCBO type A+6mADC built-in (722) or external B, Exterior B16+RCD30,
  PV AC string → own 5G4 with T2+T3? feed-in at HV (≤30 kWp 4105 ✓), Storage own circuit,
  IT/APPL cabinet circuit. RCD plan: group1 bath+ext, group2 cellar+laundry, rest split
  RCBO/B-only where required — never a single house RCD (18015).
2 Demand: P_anschluss ≈ lights 0.5 + sockets 7×0.2·16?→ planning 7×3.68=25.8 connected but
  with g≈0.4 → ~10 kW base + HP 2 + EV 11 + stove 11 + DHW 2 → instantaneous worst ~36 kW;
  with diversity (stove 11 kW g~0.3? table gS, EV not concurrent with DW+washer by habit)
  the 63 A/36.8 kVA TN-C-S connection is the envelope — declare ~14–20 kW demand value,
  utility confirms; load-management (wallbox throttles to 6 A with stove+HP running) buys the margin.
3 Zs: W1-K13 (kitchen, B16 3~ 5G2.5, 30 m): loop 2×30 m×(2.5 mm² 7.4→14.8 mΩ/m @70 °C ≈1.2× →
  ~0.53 Ω) + source ~0.35 → ~0.9 Ω vs C16 (stove circuit: 1.4) and B16 (2.9) ✓✓.
  Longest 1.5 mm² lighting B10: budget 4.6 Ω → fine (voltage drop binds first: ΔU 2·10·45/56/1.5
  = 10.7 V = 4.7% ✗ → upsize that run to 2.5 ✓ — the example proves why §7 checks both).
4 Δu full house ≤4% from HAK ✓ (risers short, specials 2.5–4).
5 Short-circuit: utility confirms I_k″(HAK)=8.5 kA → 61439-3 board f_B 6 kA with upstream NH
  cascade per manufacturer table ✓; SPD T1+T2 combined module (LSC none → T2 min; T1 optional-⚠).
6 PV: 24 modules ×405 Wp; Voc 49.2 V? string 18: at −10 °C 18×49.2×1.13=999 V ≤1000 ✓ (just);
  use 2×9 on 2 MPPT; 9.6 kWp × 1000 kWh/kWp ≈ 9600 kWh/a; self-consumption ~40%→70% w/ 10 kWh Li.
  Wallbox 11 kW → RCD type B RCBO; 722 ✓. Module psets: IfcSolarDevice Pset fields §15.2;
  structural: 25–30 kg/m² patch + wind lift (roofing/structural skills own the proof).
7 IFC export map (occurrences): HAK/Zählerschrank CONSUMERUNIT board + FUSEDISCONNECTORs + meter
  FlowMeter + SWITCHDISCONNECTOR SH; boards DISTRIBUTIONBOARD; 7+ circuits as IfcGroup +
  Pset_Circuit_Ext (values 1–3); cables IfcCableSegment with Iz/derating occurrence pset (grouping
  of the 3 parallel HP/PV/WB runs: f1 0.79 example §5.6); luminaires 42×IfcLightFixture (TotalWattage
  sum = 0.9 kW vs §2 lighting g-factor); KNX 2plus empty pipes as IfcCableCarrier CONDUITSEGMENT;
  sensors Pset_SensorType*; PAS as convention object §15.2; IDS §15.8 run green → ELT delivery ✓.
```

## 18. Failure Patterns and the Checklist Set

### 18.1 Design-phase failure patterns (the ones that bite at handover)

PEN continued past the split · single central 30 mA RCD (18015 violation §6.2) · 1.5 mm² on 20/25 A
· N shared between two RCD circuits (trips everything, fails both) · PE switched or fused alone ·
freezer/IT/monitoring behind the bathroom RCD group (nuisance = food loss) · **no test tabs on the
foundation electrode / no external LPS tabs after the pour** (§4.4 — irreversible) · SPD missing at
the supply point (0100-443) · T1 without utility consent in front of the meter · Zs table ignored
on long thin circuits (§6.5) · voltage-drop 4% only checked "per section" not origin→endpoint ·
IP classes from the room's *plan* label, not its use (unheated cellar = damp room) · bathroom zones
shifted by the actual tiled finish level/enclosure (verify after build-up, §9.2) · kitchen socket
heights vs the chosen furniture program (0.60/1.15 ladder) · switch rows vs bed-head/wardrobe ·
bus-readiness promised "cheap later" without empty pipes + reserve board space (§13.5) ·
KNX sensor positions vs acoustics/heat (PIR above a radiator) · **PV string over-Voc on a cold
morning** (§17.6 arithmetic, never "it worked in summer") · wallbox 22 kW on the connection without
the §5.5/§11.4 load proof · DC work on PV strings without the right switch/arc discipline (§3.1) ·
as-built circuit schedule never written (FM/renovation §15.9 starves).

### 18.2 Site-phase traps

Stegleitung on wood/insulation boards/feucht rooms (§8.2 table) · NYM directly in vibrated concrete ·
horizontal chases outside the ±40 cm slab band in load-bearing masonry (§8.3 / masonry skill) ·
boxes back-to-back in classified walls <14 cm · <6 cm residual wall behind bathroom boxes ·
conduit runs >15/25 m without pull boxes (§13.1) · power+data in one pipe · down-conductor clamped
at a gas/water pipe without spark-gap · 90° bends crushed flat in Stegleitung (Plaster bulge §8.2) ·
"test first, close after" skipped → retro-chasing (VOB special, acoustic bridges, fire seals) ·
screed over floor boxes without protection/height marks · labels (Adern, boards, circuit tags) as
afterthought — the IFC's `Tag` and the drill's safety both depend on them.

### 18.3 Verification checklists

**Design gate:** utility connection requested with demand value & meter concept (§5.5) · board
reserve ≥20% + empty field · zone plan on the drawings (18015-3 bands + bath zones + 6 cm rules) ·
Zs + Δu + selectivity checks per circuit table · RCD matrix (type by load AC/A/B §6.2) · SPD cascade
plan incl. DC (PV) + data lines · bonding list complete incl. future pipes · E30 circuit list vs
escape-route concept (fire skill) · LPS decision documented (risk assessment) · PV/EV/IT/WP
metering plan · IFC: LoI agreed + entity/pset conventions §15 pasted into the EIR + circuit
convention chosen · renovation: §14.3 protocol baseline + upgrade ladder agreed with client.
**Execution gates (before cover):** pre-pour earth ring + tabs · sleeves/embeds · riser & zone bands ·
conduit continuity + draw wire · boxes sealed/height-capped. **Before energizing:** §16.4 protocol
signed · utility approval · RCD/Zs measured values into the as-built (and into `Pset_Circuit_Ext`!).

---

*Sources distilled into this skill: I. Kasikci, Planung von Elektroanlagen (3rd ed., Springer Vieweg
2018); D. & M. Bohne, Gebäudetechnik (13th ed., Springer 2026 — cap. 6 Elektrotechnik, cap. 8
Energiekonzepte); R. Fischer, Elektrotechnik (16th ed., Springer Vieweg 2019); A. Böker, Grundlagen
der elektrischen Energietechnik (Springer 2026); cross-checked against DIN VDE 0100-series, DIN
18015, EN 62305/12464 rule anchors. IFC entity/property names verified against the buildingSMART
IFC4.3.2 (ADD2) official schema documentation, retrieved October 2026. The underlying books are
edition-sensitive: numbers marked ⚠ VERIFY must be re-read from the current standard text and the
local TAB before any drawing, order or signature.*

---

## Appendix S: Source Check 2026-10 — values re-read from the literature

Each line below was read again in the source books (`sources/`) in October 2026, with the
place it stands at. "Confirmed" means: a dated book prints the rule and names the standard
or law; it does not mean the current edition of that standard was opened. State law
(LBO) and local rules still override; `VERIFY` tags elsewhere in this skill stay in force
unless a line here names the edition.

### S.1 DIN 18015-2 minimum equipment per room (level 1 of RAL-RG 678)

| Room | Sockets | Lighting outlets |
|---|---|---|
| Kitchen | 5 (double) | 2 |
| Cooking niche | 3 | 1 |
| Bath | 2 | 2 |
| WC room | 1 | 1 |
| Utility room (Hausarbeitsraum) | 3 | 1 |
| Living room up to 20 m² / over 20 m² | 4 / 5 | 2 / 3 |
| Dining room | 3 | 1 |
| Bedroom, child's room, guest room, study up to 20 m² / over 20 m² | 4 / 5 | 1 / 2 |
| Hall up to 3 m / over 3 m long | 1 / 1 | 1 / 2 |
| Storage room | 1 | 1 |
| Hobby room | 3 | 1 |

— *Gebäudetechnik* Tab. 6.6 (after HEA), Tab. 2.3 and Tab. 2.9. This fills the counts
§5.3 left open for bedrooms, halls and utility rooms.

### S.2 Circuits and protection

- Confirmed (DIN 18015-2): lighting and socket circuits by living area: up to 50 m² 3,
  50–75 m² 4, 75–100 m² 5, 100–125 m² 6, over 125 m² 7. — *Gebäudetechnik* Tab. 2.3.
- Confirmed: one own circuit for each appliance from 2 kW (water heaters, cookers,
  dishwashers), also when it is plugged in; up to 4.6 kW a 20 A fuse on one phase, above
  that three phases. — *Gebäudetechnik* 6.2.
- Confirmed (DIN 18015-1): main line fuse without electric water heating, 1 to 5 dwellings:
  63 A. — *Planung von Elektroanlagen* Tab. 15.8.
- Confirmed (DIN VDE 0100-410): final circuits are protected by an RCD of 30 mA. — *Planung
  von Elektroanlagen* 17.2; *Elektrotechnik* 1.3.3.5.
- Confirmed (DIN VDE 0100-530): RCD type AC is not admitted in Germany; type A is the floor.
  — *Grundlagen der elektrischen Energietechnik* 5.2.2 (p. 392).
- Typical connected loads in kW: cooker 12, dishwasher 3.5, washing machine 3.5, dryer
  3.3–3.5, refrigerator 0.2, freezer 0.3. — *Planung von Elektroanlagen* Tab. 15.4. They
  are higher than the worked house of §17 (cooker 11 kW): size the circuit from the device.

### S.3 Bath zones

- Confirmed (DIN VDE 0100-701): in zones 0 to 2 of a tub or shower, as a rule up to 60 cm
  beside the tub and up to 2.25 m high, switches, sockets, junction boxes and concealed
  cables are not allowed. — *Gebäudetechnik* 6.2.
