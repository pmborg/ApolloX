**Intended audience**
- Aerospace enthusiasts
- KSP / RO users
- Systems & architecture engineers
- Readers interested in launch vehicle design tradeoffs

## Can the Saturn V architecture be reborn using current and available technology?

**Yes — it can.**

ApolloX demonstrates that the Saturn V launch architecture remains viable when implemented with modern propulsion, materials, and avionics.
<table>
<tr>
<td valign=top>

By **replacing**:
- Engines
- Propellants
- Materials
- Avionics
</td>
<td valign=top>

By **Keeping**:

- Staging logic
- Mass-flow philosophy
- Mission decomposition
- The same mission goals and constraints
 </td>
  </tr>
</table>

There are 2 ApolloX programs addressed in my REPOS:

- **[1] ApolloX (Earth → Moon → Earth)** (this REPO)

- [2] ApolloXM (Earth → Mars → Earth)

---

## Repository Structure

- `/GameData` — Kerbal Space Program / Realism Overhaul configuration files
- `/Ships/VAB/Apollo-X` — Reference vehicle craft files (v3.2 / v3.3)
- `README.md` — Architectural definition and analysis
- `LICENSE` — MIT License


### Build notes
The plugin source is provided under `source/Plugins`.
Compiled binaries are not included and must be built locally.

### Installation
Download the release archive and extract the `GameData` folder into your KSP installation.

### Source code
The plugin source is provided in this repository under `source/Plugins`.
Compiled binaries are included only in release archives.

---

# [1] ApolloX (Earth → Moon → Earth)

**ApolloX** is a modern vehicle built on a very good architecture inspiration (**Saturn V**) that never stopped working.

- A good Architecture does not age.  
- Technology does — and it ages fast.

**ApolloX exists to prove exactly that.**

- Apollo Program succeeded because its **architecture was correct**.
- Saturn V did not age because **architecture does not age**.
- The **technology used to implement it did**.


---

## Architecture Scope Clarification (Launch Vehicle Only)

- The Saturn V–derived architecture applies to the **launch vehicle only**
- Lunar / Martian Modules (LM / MM) are **mission-specific spacecraft**
- They are **intentionally excluded** from the launch architecture
- This separation is **fundamental to the original Apollo design philosophy**

---

## Architectural Scalability

A good architecture scales without redesign.

- We do **not** need to reinvent the wheel
- We build **wheels for cars or for trucks**

The same launch architecture supports:
- Different payload masses
- Different mission profiles
- Different destination modules

Without structural redesign.

---

## Modern Implementation: ApolloX

**ApolloX** implements a Saturn V–derived architecture using **modern propulsion hardware**.

- High-performance engines developed for Starship provide the **core propulsion**
- Architecture, staging logic, and mission decomposition remain **Saturn V–derived**

> Out of 108 total vehicle parts, only **four** are SpaceX-derived propulsion elements.  
> The architecture itself remains classical.


---

## Payload Robustness (Launch Vehicle Only)

**v3.2** is based on Raptor engines, is retained as a baseline reference.

**v3.3** is based on RS-25 engines, represents the current production architecture.

v3.2 and v3.3 are technology variants of the same architecture, not competing designs.

All performance values are simulator-derived and include ascent margins unless explicitly stated otherwise.


The following payload sweep demonstrates that **ApolloX performance scales smoothly with mass**, confirming architectural robustness rather than payload-specific optimization:

| Payload (kg) | ApolloX v3.2 Total Δv (m/s) | ApolloX v3.3 Total Δv (m/s)|
|-------------:|---------------:|---------------:|
| 0            | 21222 | 22767
| 1000         | 20936 | 22469
| 1600         | 20777 | 22303
| 2200         | 20626 | 22144
| 2800         | 20483 | 21994
| 3400         | 20346 | 21850
| 4000         | 20216 | 21712
| 4600         | 20091 | 21580
| 5200         | 19971 | 21453
| 5800         | 19856 | 21331
| 6400         | 19746 | 21214
| 7000         | 19639 | 21100

| Oneway - Payload (kg) | Oneway - ApolloX v3.2 Total Δv (m/s) | Oneway - ApolloX v3.3 Total Δv (m/s)|
|-------------:|---------------:|---------------:|
| 7100        | 21222 | 22767
| 8100        | 20936 | 22469
| 8700        | 20777 | 22303
| 9300        | 20626 | 22144
| 9900        | 20483 | 21994
| 10500       | 20346 | 21850
| 11100       | 20216 | 21712
| 11700       | 20091 | 21580
| 12300       | 19971 | 21453
| 12900       | 19856 | 21331
| 13500       | 19746 | 21214
| 14100       | 19639 | 21100

Δv values include full ascent margin and exclude mission-specific payload propulsion.


---

### Reference Configuration

For consistency and technical clarity, **all Saturn V values in the following tables refer specifically to the Apollo 11 mission configuration**.

As there was no single fixed “Saturn V” design, each vehicle evolved across the Apollo program through incremental performance, mass, and reliability upgrades.  
Using **Saturn V – Apollo 11** as the reference provides a historically representative and well-documented baseline for comparison.

Unless otherwise stated, all Saturn V parameters (thrust, mass, ISP, tankage, and staging behavior) should be interpreted as **Apollo 11 flight hardware values**, not averaged or generalized Saturn V figures.


---

# ApolloX v3.2/v3.3

## Stage 1 — Atmospheric Lift (Launch Vehicle Only)

| Parameter | Saturn V (Saturn S-IC) | ApolloX v3.2/v3.3 (Saturn S-IC Custom) |
|---------|------------------------|----------------------------------|
| Role | Atmospheric lift | Atmospheric lift |
| Engines | 5 × F-1 | 1 × Super Heavy–class cluster |
| Propellant | RP-1 / LOX | LCH₄ / LOX |
| Total Thrust (ATM) | ~34 MN | ~65.7 MN |
| Total Thrust (Vac) | ~38 MN | ~71.3 MN |
| Isp (ATM) | ~263 s | ~364 s |
| Isp (Vac) | ~304 s | ~395 s |
| Engine Mass | ~42.2 t (5 × F-1) | 20.3 t (cluster) |
| Tank Wet Mass | ~2,300 t | ~3,590 t |
| Architecture | Thrust-first | Thrust-first |
| Reusability | No | Engine hardware reusable |


### Notes

- Saturn V achieved ~34 MN using five extremely large engines.
- ApolloX achieves ~71 MN using a **single clustered engine system**, enabled by:
  - higher chamber pressures
  - methalox efficiency
  - modern turbomachinery
- The thrust increase is intentional and compensates for:
  - heavier upper stages
  - higher total vehicle mass
  - modern safety margins

This is **architectural continuity**, not replication:
the role, staging logic, and thrust-first philosophy are preserved,
while the technology is modernized.


## Stage 2 — High-Altitude / Orbital Acceleration

| Parameter | Saturn V (S-II, Apollo 11) | ApolloX v3.2 (S-II Custom) | ApolloX v3.3 (S-II Custom) |
|---------|----------------------------|----------------------------|----------------------------|
| Role | High-altitude acceleration | High-altitude acceleration | High-altitude acceleration |
| Engines | 5 × J-2 | 1 × Raptor cluster | 3 × RS-25 |
| Propellant | LH₂ / LOX | LCH₄ / LOX | RP-1 / LOX |
| Total Thrust (Vac) | ~5.1 MN | ~9.4 MN | ~6.8 MN |
| Isp (Vac) | ~421 s | ~377 s | ~452 s |
| Engine Mass | ~9 t | ~3.5 t | ~10.2 t |
| Tank Wet Mass | ~456 t | ~299 t | ~300 t |
| Tank Pressurization | Helium | Helium | Helium |
| Architecture | Vacuum-optimized, thrust-first | Vacuum-optimized, thrust-first | Vacuum-optimized, thrust-first |
| Restart Capability | Limited | Multiple (×12) | Multiple (×12) |


### Operational Role (ApolloX)

Stage-2 performs:
- Ascent from ~5 km/s to orbital velocity
- Earth orbit insertion
- Orbit circularization
- Initial Trans-Lunar Injection (TLI) when beneficial

Stage-2 is **not payload-optimized**.  
It is **architecture-optimized**, preserving Saturn V staging logic
while allowing propulsion technology to evolve.

### Architectural Interpretation

- **v3.2 (Raptor)** emphasizes:
  - very high thrust
  - low engine mass
  - methalox simplicity

- **v3.3 (RS-25)** emphasizes:
  - maximum vacuum efficiency
  - reduced propellant requirements
  - tighter Δv margins for heavy payloads

Both preserve the **same architectural role**:
only the propulsion technology changes.

Architecture remains constant.  
Technology iterates.


---

## Stage 3 — Translunar Injection (TLI Only)

**Note:**  
In ApolloX, Earth orbit insertion and circularization are completed by the *final burn of Stage-2*.  
Stage-3 is therefore a **dedicated Translunar Injection stage**, responsible for completing the TLI burn.

| Parameter | Saturn V (S-IVB, Apollo 11) | ApolloX v3.2 (S-IVB Custom) | ApolloX v3.3 (S-IVB Custom) |
|---------|-----------------------------|-----------------------------|-----------------------------|
| Role | Translunar Injection (TLI) | Translunar Injection (TLI only) | Translunar Injection (TLI only) |
| Orbit Insertion | Partial (S-II → S-IVB overlap) | Completed by Stage-2 | Completed by Stage-2 |
| Engines | 1 × J-2 | 1 × Raptor SL | 1 × RS-25 (throttled) |
| Propellant | LH₂ / LOX | LCH₄ / LOX | LH₂ / LOX |
| Thrust (Vac) | ~1.0 MN | ~1.1 MN | ~2.28 MN (throttled) |
| Isp (Vac) | ~421 s | ~377 s | ~452 s |
| Engine Mass | ~1.8 t | ~2.4 t | ~3.4 t |
| Tank Wet Mass | ~119 t | ~70 t | ~71 t |
| Ignitions | 1 (TLI) | Multiple (restartable margin) | Multiple (restartable margin) |
| Architecture | Dedicated TLI stage | Dedicated TLI stage | Dedicated TLI stage |

---

### Architectural Interpretation

- **Mission role is preserved** across all vehicles:
  - a clean, single-purpose TLI stage
- **Responsibility boundary evolves**:
  - Apollo: orbit insertion shared between S-II and S-IVB
  - ApolloX: orbit insertion fully completed *before* Stage-3
- **Technology progression**:
  - Apollo 11: hydrolox, single-start
  - ApolloX v3.2: methalox, restartable
  - ApolloX v3.3: hydrolox, very high Isp, restartable

This is an **evolution of execution**, not a redesign of architecture.

> Architecture stays the same.  
> Responsibilities move upstream.  
> Propulsion efficiency increases — mission logic does not.


---

## Control–Propulsion Module (CPM)

| Parameter | Apollo Service Module (Apollo 11) | ApolloX CPM v3.2 | ApolloX CPM v3.3 |
|---------|-----------------------------------|------------------|------------------|
| Crew | No | No | No |
| Primary Role | Propulsion + life support | Propulsion + guidance + control | Propulsion + guidance + control |
| Main Engine | AJ10-137 (SPS) | 1 × Raptor (throttled) | 1 × RS-25 (throttled) |
| Propellant | Aerozine-50 / N₂O₄ | LCH₄ / LOX | RP-1 / LOX |
| Thrust (Vac) | ~91 kN | ~1.1 MN | ~1.1–2.3 MN (throttled) |
| Isp (Vac) | ~314 s | ~377 s | ~452 s |
| Engine Mass | ~0.65 t | ~2.4 t | ~3.4 t |
| Tank Wet Mass | ~18.6 t | ~37 t | ~37 t |
| Tank Pressurization | Helium | Helium | Helium |
| Restart Capability | Multiple | Multiple (×12) | Multiple (×12) |
| Reusability | Single mission | Multi-mission capable | Multi-mission capable |
| Architecture | Dedicated service module | Integrated control–propulsion core | Integrated control–propulsion core |

### CPM Operational Role

The Control–Propulsion Module (CPM):

Always performs:
- Lunar Orbit Insertion (LOI)
- Lunar orbit circularization
- Trans-Earth Injection (TEI)

• v3.2 CPM may additionally perform the final ~100–200 m/s of TLI  
• v3.3 CPM performs no TLI — Stage-3 completes it fully

This mirrors the **mandatory role of the Apollo SM**,
while allowing controlled overlap when architecturally beneficial.

### Operational Interpretation

- Apollo SM used a **low-thrust, high-reliability hypergolic engine** designed for long-duration mission support.
- ApolloX CPM consolidates **propulsion, guidance, and control** into a single reusable core.
- Version v3.2 prioritizes **methalox commonality** with launch stages.
- Version v3.3 prioritizes **maximum efficiency**, adopting RS-25 class performance for:
  - Lunar orbit insertion (LOI)
  - Trans-Earth injection (TEI)
  - Partial TLI support when required

This preserves Apollo mission logic while modernizing propulsion capability.

---

# Spacecraft Modules (Moon Only)

## Descent & Landing Module (DLM)
**Apollo 11 LM Descent Stage vs ApolloX DLM v3.2 / v3.3**

| Parameter | Apollo LM (Apollo 11 Descent Stage) | ApolloX DLM v3.2 / v3.3 |
|---------|-------------------------------------|--------------------------|
| Primary Role | Lunar descent, landing, surface support | Lunar descent, landing, surface support |
| Crew | No (crew housed in ascent stage) | No (remotely operated / autonomous) |
| Mission Domain | Lunar surface operations | Lunar surface operations |
| Architecture | Dedicated descent stage | Dedicated descent & landing module |
| Main Engines | 1 × LM Descent Engine (LMDE) | 2 × Agena rocket engines |
| Propellant | Aerozine-50 / N₂O₄ (hypergolic) | UDMH / IRFNA-III (hypergolic) |
| Engine Type | Deep-throttle, restartable | Vacuum-optimized, restartable |
| Thrust (Vac) | ~45 kN (throttleable ~10–100%) | ~90 kN total (2 × Agena) |
| Isp (Vac) | ~311 s | ~323 s |
| Engine Mass | ~0.18 t | ~0.14 t (2 × Agena) |
| Tank Pressurization | Helium | Helium |
| Ignition Capability | Multiple (hypergolic) | Multiple (hypergolic) |
| Throttle Capability | Yes (precision landing & hover) | Yes (deep throttle suitable for landing) |
| Redundancy | Single engine, multiple valves | Multi-engine + distributed tankage |
| Reusability | Single mission | Single mission (v3.2/v3.3 baseline) |
| Design Philosophy | Reliability-first, landing safety | Reliability-first, Apollo-style logic |

### Structural & Tankage Comparison

| Feature | Apollo LM Descent Stage | ApolloX DLM v3.2 / v3.3 |
|------|------------------------|--------------------------|
| Tank Architecture | Multiple distributed tanks | 8 peripheral + 1 central tank |
| Structural Role | Landing legs + load-bearing stage | Structural spine + distributed mass |
| Total Propellant (wet) | ~10.3 t | ~23.7 t (simulator measured) |
| Surface Support | Power, consumables, structure | Propellant + structure only |

### Architectural Interpretation (DLM)

- **Mission role is identical**: controlled lunar descent and safe landing.
- Apollo used **one highly throttleable engine**; ApolloX uses **engine redundancy** instead.
- Both rely on **hypergolic ignition** to eliminate start-up risk.
- ApolloX trades *minimum mass* for *fault tolerance* and controllability.

> This is not a redesign — it is a **redundancy-enhanced implementation of the same landing logic**.


### Propellant Tank Configuration

| Tank Group | Quantity | Diameter | Length | Wet Mass (per tank) | Role |
|-----------|----------|----------|--------|--------------------|------|
| Peripheral Tanks | 8 | 1.125 m | 2.000 m | ~2.37 t | Primary descent propellant |
| Central Tank | 1 | 4.500 m | 0.250 m | ~4.75 t | Trim, balance & redundancy |

**Total Tank Wet Mass:** ~11–12 t (simulator measured)


### Architectural Notes (v3.2 / v3.3)

- The DLM deliberately uses **hypergolic propulsion** to eliminate ignition risk during:
  - Powered descent  
  - Hover  
  - Final touchdown
- **Distributed tank architecture** provides:
  - Fault tolerance (no single-point tank failure)
  - Improved mass balance throughout descent
  - Stable center-of-mass evolution
- The **central 4.5 m tank** functions as:
  - A structural spine
  - A propellant trim reservoir
  - A redundancy buffer for terminal landing phases
- This configuration is **architecturally equivalent to the Apollo LM descent stage**, rather than a modern single-tank lander.

**Total Tank Wet Mass:** 8 x 2.37t + 4.75t = 23.71t  (simulator measured)

> Note: The DLM is unchanged between ApolloX v3.2 and v3.3.

---

## Ascent & Launch Module (ALM Propulsion Stack) — ApolloX v3.2/v3.3

| Parameter | Apollo LM (Apollo 11 Ascent Stage) | ApolloX ALM v3.2 / v3.3 |
|---------|-----------------------------------|--------------------------|
| Primary Role | Lunar ascent & rendezvous | Lunar ascent & rendezvous |
| Crew | Yes (2 astronauts) | No (autonomous / remotely guided) |
| Mission Domain | Lunar ascent only | Lunar ascent only |
| Architecture | Dedicated ascent stage | Dedicated ascent module |
| Main Engine | 1 × LM Ascent Engine | 1 × Agena rocket engine |
| Propellant | Aerozine-50 / N₂O₄ | UDMH / IRFNA-III |
| Engine Type | Fixed-thrust, restartable | Vacuum-optimized, restartable |
| Thrust (Vac) | ~16 kN | ~45 kN |
| Isp (Vac) | ~311 s | ~323 s |
| Engine Mass | ~0.08 t | ~0.07 t |
| Propellant Tank | 1 × central tank | 1 × central tank |
| Tank Diameter | ~1.9 m | 1.875 m |
| Tank Length | ~1.3 m | 1.250 m |
| Tank Wet Mass | ~2.4 t | ~4.1 t |
| Tank Pressurization | Helium | Helium |
| Ignition Capability | Multiple (hypergolic) | Multiple (hypergolic) |
| Throttle Capability | No (on/off) | Limited (ascent-optimized) |
| Redundancy | None (single engine, single tank) | None (single engine, single tank) |
| Reusability | Single mission | Single mission |
| Design Philosophy | Minimum mass, crew safety | Minimum mass, minimum complexity |

### Architectural Interpretation (ALM)

- **Mission logic is identical**:
  - Lift off from lunar surface
  - Achieve lunar orbit
  - Rendezvous with command module
- Apollo optimized for **crew survival and mass minimization**.
- ApolloX removes crew constraints and increases **performance margin**.
- Both use **simple, hypergolic, ignition-safe propulsion**.

> The ALM is intentionally conservative — because ascent failure is unrecoverable.

---

## Habitat Module (HM) — Crew Module

**Terminology Note:**  
The terms *Habitat* and *Crew Module* are synonymous in ApolloX documentation and refer to the same physical module.

The **Habitat Module (HM)** — also referred to as the **Crew Module** — is the **only pressurized and crewed volume** in the ApolloX mission.

- Pressurized
- Crew lives here **for the entire mission**
- Never separated from the crew

Astronauts:
- launch in it
- cruise in it
- land on the Moon in it
- return to Earth in it

The Habitat **does not perform propulsion, landing, ascent, or orbital maneuvering**.

It is treated as **payload** by all propulsion elements below it:
- ALM propulsion stack
- DLM descent system

> The crew survives by **architectural separation of concerns**, not by embedding propulsion or landing authority inside the Habitat.

The Habitat is **not disposable** and is the **only module that returns to Earth intact**.

---

## What ApolloX Is Not

ApolloX is **not**:
- a minimum-mass lunar lander
- a crew-on-landing-risk architecture
- a single-use or stunt vehicle
- an ISRU-dependent system
- a surface-operations–optimized design

**ApolloX deliberately prioritizes:**
- clear separation of concerns
- fault tolerance over mass minimization
- architectural correctness over local optimization

Performance margins are **intentional** and exist to validate the architecture,  
not to extract the last kilogram of payload.

ApolloX is a **reference architecture** — not the final form of lunar operations.

## Final Thought

> *ApolloX is a modern vehicle built on a very good architecture that never stopped working, but the technology used aged.*

---

**What This Repository Contains**

- Vehicle architecture definition
- Mass budgets and Δv analysis
- Simulator-derived performance sweeps
- Comparative tables against Apollo 11

**What This Repository Does Not Contain**
- Manufacturing drawings
- Cost modeling
- Program timelines
- Political or funding assumptions

This prevents misinterpretation **without weakening the work.**
