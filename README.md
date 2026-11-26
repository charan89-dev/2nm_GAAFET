# 2nm-Class 3-Stacked Silicon Nanosheet N-Type GAAFET

3D TCAD design, operating physics, and electrical characterization of a **2nm-class 3-Stacked Silicon Nanosheet N-Type Gate-All-Around Field-Effect Transistor (GAAFET)** simulated in **Synopsys Sentaurus TCAD**.

> **Confidentiality Notice:** All TCAD process/device decks, extraction scripts, parameter databases, and raw simulation datasets are kept private. This repository showcases the device architecture, working principles, structural visualizations, and characterization outcomes.

---

## 1. Device Architecture & Structural Overview

As CMOS scaling pushes past FinFET limits, short-channel effects (DIBL and subthreshold leakage) degrade electrostatic integrity. This design implements a **vertically stacked 3-channel Silicon Nanosheet Gate-All-Around (GAA)** N-Type architecture where the High-$\kappa$/Metal Gate (HKMG) wraps around all four sides of every nanosheet channel.

### Key Architectural Features
- **3-Stacked Si Nanosheets:** Maximizes effective channel width ($W_{\text{eff}}$) and drive current within a compact footprint while maintaining tight vertical confinement.
- **Wrap-Around HKMG Stack:** Interfacial $\text{SiO}_2$ paired with High-$\kappa$ $\text{HfO}_2$ and a Replacement Metal Gate (RMG) Molybdenum electrode for superior gate capacitance and near-ideal subthreshold control.
- **Inner Dielectric Spacers:** Silicon Nitride ($\text{Si}_3\text{N}_4$) inner spacers isolate the embedded metal gate layers from the Source/Drain epitaxial regions, suppressing gate-to-S/D parasitic fringe capacitance.
- **Schottky Molybdenum S/D Contacts:** Parameterized Molybdenum Source/Drain contacts engineered for NMOS work-function alignment and series contact resistance analysis.

| Structural Parameter | Specification (N-Type) |
| :--- | :--- |
| **Channel Architecture** | 3-Stacked Si Nanosheets |
| **Gate Length ($L_g$)** | `[e.g., 12 nm / 14 nm]` |
| **Sheet Thickness ($T_{si}$)** | `[e.g., 5 nm / 6 nm]` |
| **Sheet Width ($W_{sh}$)** | `[e.g., 10 nm]` |
| **Gate Dielectric** | $\text{SiO}_2 / \text{HfO}_2$ (`[Tox]`) |
| **Outer Spacer Length ($L_{\text{spacer}}$)** | $6\text{ nm}$ |
| **Contact Length ($L_{\text{contact}}$)** | $15\text{ nm}$ |
| **Gate Metal** | Molybdenum ($4.60 - 4.70\text{ eV}$) |
| **S/D Contact Work Function** | Molybdenum Schottky ($4.05\text{ eV}$) |
| **S/D Contact Resistance ($R_{c,SD}$)** | $15 - 150\ \Omega$ |
| **Supply Voltage ($V_{dd}$)** | $0.65\text{ V} - 0.75\text{ V}$ |

![3D N-Type GAAFET Structure](images/3d_gaafet_structure.png)

---

## 2. Working Principle & Fabrication Concept

### Virtual Fabrication Flow
1. **Superlattice Formation:** Alternating epitaxial layers of sacrificial $\text{SiGe}$ and Silicon channels are grown on a bulk Silicon substrate isolated by Shallow Trench Isolation (STI).
2. **Fin & Dummy Gate Definition:** The stacked superlattice is patterned into fins and crossed by a sacrificial dummy gate with outer Nitride spacers.
3. **Inner Spacer & S/D Epitaxy:** Source/Drain cavities are recessed, sacrificial $\text{SiGe}$ layers are laterally indented and filled with Nitride inner spacers, and in-situ Phosphorus-doped S/D regions are epitaxially grown and annealed.
4. **Channel Release & Replacement Metal Gate:** The dummy gate and sacrificial $\text{SiGe}$ layers are selectively etched away to suspend all three Silicon nanosheets, followed by conformal $\text{SiO}_2/\text{HfO}_2$ and Molybdenum wrap-around gate deposition.

### Operating Physics
- **Off-State ($V_{gs} = 0\text{ V}$):** Because the gate encloses all four surfaces of each thin Silicon nanosheet, the electrostatic potential barrier in the channel is tightly controlled, keeping subthreshold leakage ($I_{\text{off}}$) in the picoampere regime and achieving a near-ideal subthreshold swing ($\sim 63\text{ mV/dec}$ at $298\text{ K}$).
- **On-State ($V_{gs} = V_{dd}$):** Applying positive gate bias above $V_T$ forms strong electron inversion channels simultaneously across all three stacked nanosheets. Quantum confinement shifts the carrier charge centroid away from the $\text{Si}/\text{SiO}_2$ interface toward the core of each sheet.
- **S/D Junction Profile:** Controlled lateral Phosphorus diffusion from the S/D epitaxy into the nanosheet extensions lowers access resistance and boosts saturation drive current ($I_{\text{sat}}$) while preserving strong gate electrostatic control.

| 2D Cross-Section (Channel & Inner Spacers) | Active Doping Profile (Phosphorus S/D & Channel) |
| :---: | :---: |
| ![Cross Section](images/cross_section_cut.png) | ![Doping Profile](images/doping_profile.png) |

---

## 3. Physical Modeling Framework

3D electrostatics and carrier transport were evaluated under the Drift-Diffusion framework with advanced sub-10 nm physical corrections:

- **Carrier Statistics:** Fermi-Dirac statistics for degenerately doped Source/Drain junctions.
- **Quantum Confinement:** Modified Local-Density Approximation (`eMLDA` and `hMLDA`) to accurately model threshold voltage shift and charge distribution inside thin Silicon nanosheets.
- **Mobility Degradation:** Doping-dependent impurity scattering, transverse-field surface roughness and acoustic phonon scattering (Lombardi model), and high-field velocity saturation.
- **Band Structure & Recombination:** Bandgap narrowing (`OldSlotboom`), doping-dependent Shockley-Read-Hall (SRH), and Auger recombination.
- **AC Characterization:** Multi-terminal small-signal AC analysis at $1\text{ MHz}$ for total gate capacitance ($C_{gg}$) extraction.

![On-State Electron Density](images/carrier_density_on_state.png)

---

## 4. Electrical Characterization & Thermal Results

### Room-Temperature Metrics ($T = 298\text{ K}$)

| Parameter | Observed Range (N-Type) |
| :--- | :--- |
| **Threshold Voltage ($V_T$)** | $0.16\text{ V} \text{ to } 0.24\text{ V}$ |
| **Saturation Drive Current ($I_{\text{sat}}$)** | $167\ \mu\text{A} \text{ to } 341\ \mu\text{A}$ |
| **Off-State Leakage ($I_{\text{off}}$)** | $1.3 \times 10^{-11}\text{ A} \text{ to } 8.3 \times 10^{-11}\text{ A}$ |
| **Subthreshold Swing ($SS$)** | $63.3 - 63.8\text{ mV/dec}$ |
| **Peak Transconductance ($g_{\max}$)** | $0.99 - 1.36\text{ mS}$ |
| **Max Gate Capacitance ($C_{gg,\max}$ @ 1 MHz)** | `[Insert fixed aF value]` |

### Thermal Performance ($298\text{ K} \rightarrow 358\text{ K} \rightarrow 398\text{ K}$)
- **Subthreshold Swing:** Tracks fundamental Boltzmann thermal scaling ($k_B T / q$), shifting from **~63 mV/dec** (298 K) to **~76–77 mV/dec** (358 K) and **~85–86 mV/dec** (398 K).
- **Leakage Current:** $I_{\text{off}}$ rises by approximately two orders of magnitude from $298\text{ K}$ to $398\text{ K}$ as thermal carrier excitation over the channel barrier increases.
- **On-State Current:** Drive current and peak transconductance degrade moderately at elevated temperatures due to increased lattice phonon scattering.

### Output Characteristics Gallery

| Transfer Characteristics ($I_d - V_g$) | Output Characteristics ($I_d - V_d$) |
| :---: | :---: |
| ![Id-Vg Curves](images/idvg_lin_sat.png) | ![Id-Vd Curves](images/idvd_output.png) |

| Gate Capacitance ($C_{gg} - V_g$ @ 1 MHz) | Thermal Degradation ($298\text{ K} - 398\text{ K}$) |
| :---: | :---: |
| ![C-V Curves](images/cv_1mhz.png) | ![Thermal Scaling](images/thermal_scaling.png) |
