<h1 align="center">Electromagnetics & Physics</h1>

## Table of Contents
1. [Electric & Magnetic Fields](#1-electric--magnetic-fields)
2. [Inductance & Capacitance Theory](#2-inductance--capacitance-theory)
3. [Transmission Lines](#3-transmission-lines)
4. [EMI/EMC Principles](#4-emi-emc-principles)

---

## 1. Electric & Magnetic Fields

### 1.1 Electrostatics Fundamentals

#### Coulomb's Law

**Force between Point Charges:**
```
       q₁ q₂
F = k ──────
       r²

Where:
k = 1/(4πε₀) = 8.9875 × 10⁹ N⋅m²/C²
ε₀ = 8.854 × 10⁻¹² F/m (permittivity of free space)
```

**Vector Form:**
```
       q₁ q₂   ^
F = k ────── r
       r²
```

#### Electric Field Intensity

**Definition:**
```
    F
E = ─
    q

Units: V/m or N/C
```

**Point Charge Field:**
```
       Q   ^
E = k ─── r
       r²
```

### 1.2 Gauss's Law

#### Integral Form
```
∮ E ⋅ dA = Q_enclosed / ε₀
```

**Physical Meaning:** The total electric flux through a closed surface equals the charge enclosed divided by ε₀.

#### Applications

**Infinite Line Charge:**
```
     λ
E = ────
    2περ
Where λ = charge per unit length
```

**Infinite Sheet:**
```
     σ
E = ───
    2ε
Where σ = surface charge density
```

**Spherical Symmetry:**
```
     Q
E = ────
    4περ²
```

### 1.3 Electric Potential

#### Potential Difference
```
       B
V_AB = - ∫ E ⋅ dl
       A
```

**Point Charge Potential:**
```
     Q
V = ───
    4περ
```

#### Equipotential Surfaces
- Surfaces where potential is constant
- Electric field lines perpendicular to equipotential surfaces
- No work done moving charge along equipotential

### 1.4 Magnetostatics

#### Biot-Savart Law

**Magnetic Field from Current Element:**
```
     μ₀ I dl × r̂
dB = ── ──────
     4π  r²
```

**Where:**
```
μ₀ = 4π × 10⁻⁷ H/m (permeability of free space)
```

#### Applications

**Straight Wire:**
```
     μ₀ I
B = ────
    2πr
```

**Circular Loop (Center):**
```
     μ₀ I
B = ───
     2R
```

**Solenoid (Long):**
```
B = μ₀ n I
Where n = turns per unit length
```

### 1.5 Ampere's Law

#### Integral Form
```
∮ B ⋅ dl = μ₀ I_enclosed
```

**Applications:**
- Infinite straight wire
- Solenoid
- Toroid

### 1.6 Maxwell's Equations

#### Time-Varying Form

**Gauss's Law for Electricity:**
```
∇ ⋅ D = ρ_v
```

**Gauss's Law for Magnetism:**
```
∇ ⋅ B = 0
```

**Faraday's Law:**
```
∇ × E = -∂B/∂t
```

**Ampere-Maxwell Law:**
```
∇ × H = J + ∂D/∂t
```

#### Integral Form

**Gauss's Law:**
```
∮ D ⋅ dA = Q_enclosed
```

**No Magnetic Monopoles:**
```
∮ B ⋅ dA = 0
```

**Faraday's Law:**
```
∮ E ⋅ dl = -d/dt ∫ B ⋅ dA
```

**Ampere's Law:**
```
∮ H ⋅ dl = I_enclosed + d/dt ∫ D ⋅ dA
```

### 1.7 Boundary Conditions

#### Electric Fields
```
E₁ₜ = E₂ₜ
D₁ₙ - D₂ₙ = ρ_s
```

#### Magnetic Fields
```
H₁ₜ - H₂ₜ = J_s
B₁ₙ = B₂ₙ
```

---

## 2. Inductance & Capacitance Theory

### 2.1 Capacitance Fundamentals

#### Definition
```
     Q
C = ───
     V
```

**Parallel Plate Capacitor:**
```
     εA
C = ───
     d
```

#### Energy Storage
```
     1
W = ── C V²
     2
```

### 2.2 Capacitor Types & Configurations

#### Common Geometries

**Parallel Plate:**
```
     ε₀εᵣ A
C = ─────
       d
```

**Cylindrical:**
```
     2πε₀εᵣ L
C = ───────
     ln(b/a)
```

**Spherical:**
```
     4πε₀εᵣ ab
C = ──────
      b - a
```

#### Dielectric Materials

**Polarization:**
```
P = ε₀χₑE
D = ε₀E + P = εE
```

**Relative Permittivity:**
```
εᵣ = ε/ε₀ = 1 + χₑ
```

### 2.3 Inductance Fundamentals

#### Self-Inductance
```
     NΦ
L = ───
      I
```

#### Energy Storage
```
     1
W = ── L I²
     2
```

### 2.4 Inductor Types & Configurations

#### Solenoid
```
     μ₀μᵣ N² A
L = ──────
        l
```

#### Toroid
```
     μ₀μᵣ N² h   b
L = ────── ln(─)
       2π      a
```

### 2.5 Mutual Inductance

#### Definition
```
     N₂Φ₂₁
M = ────
      I₁
```

**Coupling Coefficient:**
```
       M
k = ──────
    √L₁L₂
```

#### Dot Convention
```
     ┌───┐    ┌───┐
     │ L₁│    │ L₂│
     │   │    │   │
• ───┤   ├──•─┤   ├──•
     │   │    │   │
     └───┘    └───┘
```

### 2.6 Magnetic Materials

#### Permeability
```
μ = μ₀μᵣ
B = μH
```

#### Material Classification

**Diamagnetic:** μᵣ < 1
**Paramagnetic:** μᵣ > 1
**Ferromagnetic:** μᵣ >> 1

#### Hysteresis
```
B
↑   ┌─────────┐
│  ⁄         ⁄
│∕         ∕
├─────────→ H
│         ∕
│        ∕
│
```
- **Remanence (Bᵣ):** Residual magnetism
- **Coercivity (H꜀):** Field to demagnetize

### 2.7 Time-Varying Fields

#### Faraday's Law Applications

**Moving Conductor:**
```
ε = -dΦ/dt = B l v
```

**Transformer EMF:**
```
ε = -N dΦ/dt
```

#### Lenz's Law
> The induced EMF always opposes the change in magnetic flux that produced it.

---

## 3. Transmission Lines

### 3.1 Transmission Line Fundamentals

#### Distributed Parameter Model
```
     ┌───[R]───[L]───┐
     │               │
Input               Output
     │               │
     └───[G]───[C]───┘
```

**Per Unit Length:**
- R: Series resistance (Ω/m)
- L: Series inductance (H/m)
- G: Shunt conductance (S/m)
- C: Shunt capacitance (F/m)

### 3.2 Telegrapher's Equations

#### Wave Equations
```
∂²V   ∂V     ∂²V
─── = RG V + (RC + LG) ── + LC ───
∂z²         ∂t        ∂t²
```

#### Sinusoidal Steady State
```
d²V
─── = γ² V
dz²

Where:
γ = √( (R + jωL)(G + jωC) ) = α + jβ
```

### 3.3 Characteristic Impedance

#### Definition
```
        R + jωL
Z₀ = √ ──────
        G + jωC
```

#### Lossless Line Approximation
```
       L
Z₀ = √ ─
       C
```

### 3.4 Propagation Constant

#### Components
```
γ = α + jβ
Where:
α = attenuation constant (Np/m)
β = phase constant (rad/m)
```

#### Phase Velocity
```
     ω
vₚ = ─
     β
```

#### Wavelength
```
     2π
λ = ───
     β
```

### 3.5 Reflection Coefficient

#### Definition
```
     Z_L - Z₀
Γ = ──────
     Z_L + Z₀
```

**Special Cases:**
- **Open circuit (Z_L = ∞):** Γ = +1
- **Short circuit (Z_L = 0):** Γ = -1
- **Matched load (Z_L = Z₀):** Γ = 0

### 3.6 Standing Wave Ratio (SWR)

#### Voltage Standing Wave Ratio (VSWR)
```
     1 + |Γ|
VSWR = ──────
     1 - |Γ|
```

#### Applications
- **VSWR = 1:** Perfect match
- **VSWR = ∞:** Total reflection
- **Typical:** VSWR < 2:1 for good systems

### 3.7 Impedance Transformation

#### Input Impedance
```
        Z_L + jZ₀ tan(βl)
Z_in = Z₀ ──────────────
        Z₀ + jZ_L tan(βl)
```

#### Quarter-Wave Transformer
```
Z_in = Z₀² / Z_L
```

**Impedance Matching:**
```
Z₀ = √(Z_s Z_L)
```

### 3.8 Smith Chart

#### Basic Construction
```
     Imaginary
        ↑
        │
        │
   ┌────┼────┐
   │    │    │
   │    │    │
───┼────┼────┼──→ Real
   │    │    │
   │    │    │
   └────┼────┘
        │
        │
```

**Features:**
- Constant resistance circles
- Constant reactance circles
- VSWR circles
- Wavelength scales

#### Applications
- Impedance matching
- Reflection coefficient determination
- Admittance calculations

### 3.9 Common Transmission Lines

#### Coaxial Cable
```
     μ₀   b
L = ─── ln(─)
     2π   a

     2πε₀εᵣ
C = ──────
     ln(b/a)

      1    μ₀   b
Z₀ = ─── √ ─── ln(─)
     2π    ε₀    a
```

#### Microstrip
```
For W/h > 1:
      120π
Z₀ ≈ ────────────
     √ε_eff [W/h + 1.393 + 0.667 ln(W/h + 1.444)]

Where:
     εᵣ + 1   εᵣ - 1     1
ε_eff = ──── + ──── ──────────
       2       2   √(1 + 12h/W)
```

#### Stripline
```
      30π      4b
Z₀ ≈ ─── ───────────
     √εᵣ W_eff + 0.441b

Where:
     W   ⎧ 0 for W/b > 0.35
W_eff = ─ - ⎨
     b   ⎩ (0.35 - W/b)² for W/b < 0.35
```

---

## 4. EMI/EMC Principles

### 4.1 EMI Fundamentals

#### Definitions

**EMI (Electromagnetic Interference):**
> Unwanted electromagnetic energy that disrupts system performance

**EMC (Electromagnetic Compatibility):**
> Ability of equipment to function satisfactorily in its electromagnetic environment without introducing intolerable disturbances

#### EMI Types

**Conducted EMI:**
- Through power lines
- Through signal cables
- Frequency range: 150kHz - 30MHz

**Radiated EMI:**
- Through electromagnetic fields
- Frequency range: 30MHz - 1GHz+

### 4.2 EMI Sources

#### Natural Sources
- Atmospheric noise (lightning)
- Cosmic noise
- Solar flares
- Electrostatic discharge (ESD)

#### Man-Made Sources
- Digital electronics (clock harmonics)
- Switching power supplies
- Motors and relays
- Radio transmitters

### 4.3 EMI Coupling Mechanisms

#### Conducted Coupling

**Common Impedance Coupling:**
```
     ┌───┐   ┌───┐
     │ A │   │ B │
     └─┬─┘   └─┬─┘
       │       │
       ├─[Z]───┤
       │       │
      GND     GND
```

**Solution:** Star grounding, separate returns

#### Radiated Coupling

**Electric Field Coupling:**
```
     ┌───┐      ┌───┐
     │   │ Cₘ   │   │
Noise│   ├───┐  │   │ Victim
     └───┘   │  └───┘
             │
            GND
```

**Magnetic Field Coupling:**
```
     ┌───┐      ┌───┐
     │   │ M    │   │
Noise│   ├─͡─┐  │   │ Victim
     └───┘   │  └───┘
             │
            GND
```

### 4.4 EMC Design Techniques

#### Shielding

**Shielding Effectiveness:**
```
SE = R + A + B (dB)
Where:
R = Reflection loss
A = Absorption loss
B = Multiple reflection correction
```

**Far Field Shielding:**
```
         Z_w
R ≈ 20 log ─── (dB)
         4Z_s

A ≈ 8.686 t √(πfμσ) (dB)
```

#### Filtering

**Low-Pass Filters:**
- **LC filters:** For power lines
- **Ferrite beads:** For high-frequency suppression
- **Common-mode chokes:** For differential signals

**Filter Placement:**
- At cable entries/exits
- Close to noise sources
- Before sensitive circuits

#### Grounding

**Grounding Strategies:**
- **Single-point:** For low frequencies
- **Multi-point:** For high frequencies
- **Hybrid:** Combination approach

**Ground Plane Design:**
- Solid ground planes preferred
- Minimize slots in ground planes
- Use multiple vias for connections

### 4.5 PCB Layout for EMC

#### Component Placement
- Group related circuits together
- Separate analog and digital sections
- Place noisy components away from sensitive ones
- Keep high-speed traces short

#### Routing Guidelines
- Use 45° corners, not 90°
- Minimize loop areas
- Route critical signals first
- Use guard traces for sensitive signals

#### Power Distribution
- Use multiple decoupling capacitors
- Implement power planes
- Minimize power loop areas
- Use star distribution for analog circuits

### 4.6 EMC Standards

#### Regulatory Bodies
- **FCC (USA):** Part 15 for digital devices
- **CISPR (International):** Emission standards
- **IEC (International):** Immunity standards
- **MIL-STD (Military):** Military requirements

#### Common Standards

**Emissions:**
- **CISPR 22/EN 55022:** Information technology equipment
- **CISPR 25:** Automotive
- **FCC Part 15:** Unintentional radiators

**Immunity:**
- **IEC 61000-4-2:** ESD immunity
- **IEC 61000-4-3:** Radiated RF immunity
- **IEC 61000-4-4:** Electrical fast transients
- **IEC 61000-4-5:** Surge immunity

### 4.7 EMC Testing

#### Emissions Testing

**Conducted Emissions:**
```
Frequency: 150kHz - 30MHz
Equipment: LISN (Line Impedance Stabilization Network)
Limit: dBμV quasi-peak and average
```

**Radiated Emissions:**
```
Frequency: 30MHz - 1GHz (or higher)
Setup: Open area test site or semi-anechoic chamber
Antenna: Varies with frequency
Limit: dBμV/m at specified distance
```

#### Immunity Testing

**ESD Testing:**
```
Levels: 2kV (contact), 4kV, 8kV (air discharge)
Points: All accessible surfaces
Criteria: Performance degradation categories
```

**Radiated Immunity:**
```
Frequency: 80MHz - 1GHz (or 2.7GHz)
Field strength: 3V/m to 10V/m
Modulation: 80% AM, 1kHz
```

### 4.8 EMC Troubleshooting

#### Common Problems
- Clock harmonics exceeding limits
- Power supply switching noise
- Cable radiation
- Ground bounce
- Simultaneous switching noise

#### Diagnostic Tools
- **Spectrum analyzer:** Frequency domain analysis
- **Near-field probes:** Localizing radiation sources
- **Current probes:** Conducted emissions measurement
- **Oscilloscope:** Time domain analysis

#### Fixes and Solutions
- Add ferrite beads on cables
- Improve shielding
- Add filtering
- Modify PCB layout
- Change grounding strategy

---

## Practice Problems

### Problem 1: Electric Field Calculation
```
Two point charges: Q₁ = +2μC at (0,0), Q₂ = -1μC at (3m, 4m)
Calculate:
a) Electric field at point P(6m, 0)
b) Force on a +0.5μC charge placed at P
c) Electric potential at P
```

### Problem 2: Transmission Line Analysis
```
A 50Ω transmission line is 0.3λ long and terminated with Z_L = 75 + j50Ω
Find:
a) Reflection coefficient
b) VSWR
c) Input impedance
d) Return loss
```

### Problem 3: Inductance Design
```
Design a solenoid inductor with:
L = 100μH, I_max = 2A, core μᵣ = 100
Given: Core cross-section = 1cm², mean length = 10cm
Calculate:
a) Number of turns required
b) Wire size based on current density of 5A/mm²
c) Energy stored at maximum current
```

### Problem 4: EMC Analysis
```
A digital clock oscillator operates at 25MHz with 1ns rise time.
Estimate:
a) Significant harmonic frequencies
b) Required shielding effectiveness for 40dB attenuation at 500MHz
c) Filter requirements for power line conducted emissions
```

### Problem 5: Capacitor Selection
```
Select capacitors for decoupling a 3.3V digital IC with:
- Maximum current transient: 500mA
- Maximum allowed voltage droop: 50mV
- Operating frequency: 100MHz
Calculate:
a) Required capacitance
b) ESR requirement
c) Self-resonant frequency requirement
```

## Conclusion

This comprehensive electromagnetics and physics course covers the fundamental principles governing electric and magnetic fields, energy storage in reactive components, signal propagation in transmission lines, and electromagnetic compatibility. Each section builds upon mathematical foundations to provide practical engineering insights.

Key concepts to remember:
- Maxwell's equations form the foundation of all electromagnetic phenomena
- Energy storage in capacitors and inductors follows quadratic relationships with voltage and current
- Transmission line behavior becomes critical when electrical lengths approach signal wavelengths
- EMC design requires proactive consideration of emissions, immunity, and coupling mechanisms

Modern electronic systems continue to push the boundaries of speed and integration, making thorough understanding of these electromagnetic principles essential for successful circuit and system design. The principles covered in this course provide the foundation for advanced topics in RF design, high-speed digital systems, and electromagnetic modeling.
