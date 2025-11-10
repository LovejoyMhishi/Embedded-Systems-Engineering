<h1 align="center">Power Electronics </h1>

## Table of Contents
1. [Rectifiers & Converters](#1-rectifiers--converters)
2. [Inverters & Motor Drives](#2-inverters--motor-drives)
3. [SMPS & Power Regulation](#3-smps--power-regulation)
4. [Battery Management](#4-battery-management)

---

## 1. Rectifiers & Converters

### 1.1 Power Semiconductor Devices

#### Power Diodes

**Structure and Symbol:**
```
    A →|→ K
  Anode   Cathode
```

**Reverse Recovery Characteristics:**
```
Current
  ↑
  |‾‾‾‾‾‾‾‾⎯⎯⎯⎯⎯⎯⎯⎯⎯
  |         ⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯
  |               ⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯
  +-----------------------→ Time
       t_rr    t_a   t_b
```

**Key Parameters:**
- Forward voltage drop (V_f): 0.7-1.2V
- Reverse recovery time (t_rr): 25ns - 5μs
- Maximum repetitive reverse voltage (V_RRM)
- Average forward current (I_FAV)

#### Thyristors (SCR)

**Structure and Symbol:**
```
    A →|→ K
       │
       G (Gate)
```

**VI Characteristics:**
```
Current ↑
        |     Conducting
        |‾‾‾‾‾⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯
        |    /
        |   /
        |  / Forward Blocking
        | /
        +--------------→ Voltage
        |
       Reverse Blocking
```

**Triggering Methods:**
- Gate trigger (most common)
- Light trigger (LASCR)
- dv/dt trigger
- Temperature trigger

**Latching Current (I_L):** Minimum anode current to maintain conduction
**Holding Current (I_H):** Minimum anode current to keep device ON

#### Power MOSFETs

**Symbol:**
```
     Drain (D)
        │
        │
        ○
        │
     Gate (G)
        │
        │
        ○
        │
     Source (S)
```

**Advantages:**
- Voltage-controlled device
- High switching speed
- No secondary breakdown
- Parallel operation capability

**Key Parameters:**
- R_DS(on): On-state resistance
- V_DS(max): Maximum drain-source voltage
- I_D(max): Maximum drain current
- Gate threshold voltage (V_GS(th))

#### IGBTs (Insulated Gate Bipolar Transistors)

**Symbol:**
```
     Collector (C)
        │
        │
        ○
        │
     Gate (G)
        │
        │
        ○
        │
     Emitter (E)
```

**Characteristics:**
- Combines MOSFET input and BJT output
- Lower conduction losses than MOSFETs
- Medium switching speed
- High current capability

### 1.2 Single-Phase Rectifiers

#### Half-Wave Rectifier

**Circuit:**
```
     AC Input
       │
      [D]
       │
       ├─→ [R_L] → V_out
       │
      GND
```

**Output Waveform:**
```
V_out
  ↑
  |‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾⎯
  |               ⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯
  |                           ⎯⎯⎯⎯
  +-------------------------------→ Time
```

**Analysis:**
```
Average DC voltage: V_dc = V_m / π
RMS voltage: V_rms = V_m / 2
Ripple factor: γ = √(π²/4 - 1) ≈ 1.21
```

#### Full-Wave Center-Tapped Rectifier

**Circuit:**
```
     AC + ──[D1]───┐
                   ├─→ [R_L] → V_out
     AC - ──[D2]───┘
            │
           CT
```

**Analysis:**
```
V_dc = 2V_m / π
V_rms = V_m / √2
PIV = 2V_m
```

#### Full-Wave Bridge Rectifier

**Circuit:**
```
     AC + ──[D1]───┐
         │         │
     AC - ──[D3]───┼─→ [R_L] → V_out
         │         │
         └─[D2]─┐ │
               │ │ │
         └─[D4]─┘ │
                   │
                  GND
```

**Analysis:**
```
V_dc = 2V_m / π
V_rms = V_m / √2
PIV = V_m
Ripple factor: γ ≈ 0.48
```

**With Capacitor Filter:**
```
     ┌──[D1]──┐
     │        │
AC ──┼──[D3]──┼─→ [C] → V_out
     │        │    │
     └──[D2]─┐│   GND
            │││
     └──[D4]─┘│
              │
             GND
```

**Ripple Voltage:**
```
V_ripple ≈ I_dc / (f × C)
where f = 2×f_line for full-wave
```

### 1.3 Three-Phase Rectifiers

#### Three-Phase Half-Wave Rectifier

**Circuit:**
```
     Phase A ──[D1]───┐
     Phase B ──[D2]───┼─→ [R_L] → V_out
     Phase C ──[D3]───┘
```

**Output:**
```
V_dc = (3√3)/(2π) × V_m_phase ≈ 1.17 × V_phase_rms
```

#### Three-Phase Bridge Rectifier

**Circuit:**
```
     A ──[D1]───┐   ┌──[D4]── A
     B ──[D3]───┼─┐ │ ┌──[D6]── B
     C ──[D5]───┘ │ │ │ ┌──[D2]── C
                 │ │ │ │
                 ├─┼─┼─┼─→ V_out
                 │ │ │ │
                GND GND GND
```

**Analysis:**
```
V_dc = (3√3)/π × V_m_phase ≈ 2.34 × V_phase_rms
V_rms = √(3/2 + 9√3/(4π)) × V_m_phase ≈ 1.655 × V_m_phase
Ripple frequency: 6×f_line
```

### 1.4 DC-DC Converters

#### Buck Converter (Step-Down)

**Circuit:**
```
     +V_in
       │
      [S]───[L]───┐
       │     │    │
      [D]    │   [C] → V_out
       │     │    │
      GND   GND  GND
```

**Operation:**
- **Switch ON:** Current flows through L to output
- **Switch OFF:** L current freewheels through D

**Analysis:**
```
V_out = D × V_in
where D = t_on / T (duty cycle)

Inductor current ripple:
ΔI_L = (V_in - V_out) × D × T / L

Output voltage ripple:
ΔV_out = ΔI_L / (8 × f × C)
```

**Design Example:**
```
V_in = 24V, V_out = 12V, I_out = 2A, f = 50kHz

D = V_out / V_in = 0.5
L_min = (V_in - V_out) × D / (f × ΔI_L)
Assume ΔI_L = 0.4 × I_out = 0.8A
L_min = (24-12) × 0.5 / (50000 × 0.8) = 150μH

C_min = ΔI_L / (8 × f × ΔV_out)
Assume ΔV_out = 0.01 × V_out = 0.12V
C_min = 0.8 / (8 × 50000 × 0.12) ≈ 16.7μF
```

#### Boost Converter (Step-Up)

**Circuit:**
```
     +V_in
       │
      [L]───[S]───┐
       │     │    │
       │    [D]  [C] → V_out
       │     │    │
      GND   GND  GND
```

**Analysis:**
```
V_out = V_in / (1 - D)
I_in = I_out / (1 - D)

Inductor current ripple:
ΔI_L = V_in × D × T / L

Output voltage ripple:
ΔV_out = I_out × D × T / C
```

#### Buck-Boost Converter

**Circuit:**
```
     +V_in
       │
      [S]───┐
       │    │
      [L]  [D]───[C] → V_out
       │    │    │
      GND  GND  GND
```

**Analysis:**
```
V_out = -V_in × D / (1 - D)  (inverts polarity)
Magnitude: |V_out| = V_in × D / (1 - D)
```

#### Ćuk Converter

**Circuit:**
```
     +V_in
       │
      [L1]───[S]───┐
       │     │    │
       │    [C1]  [D]───[L2]───[C2] → V_out
       │     │    │           │
      GND   GND  GND         GND
```

**Analysis:**
```
V_out = -V_in × D / (1 - D)
Advantages: Continuous input and output current
```

### 1.5 Phase-Controlled Rectifiers

#### Single-Phase Controlled Rectifier

**Circuit with Thyristor:**
```
     AC Input
       │
      [SCR]
       │
       ├─→ [R_L] → V_out
       │
      GND
       │
    Gate Drive
```

**Output Voltage vs Firing Angle (α):**
```
V_dc = (V_m / π) × (1 + cos α)

α = 0°: Full output (like diode)
α = 90°: Half output
α = 180°: Zero output
```

#### Three-Phase Controlled Rectifier

**Analysis:**
```
V_dc = (3√3 × V_m_line) / (2π) × cos α
       for 0° ≤ α ≤ 90° (rectification)
V_dc = (3√3 × V_m_line) / (2π) × cos α
       for 90° < α < 180° (inversion)
```

---

## 2. Inverters & Motor Drives

### 2.1 Inverter Fundamentals

#### What is an Inverter?
Converts DC to AC with controllable frequency and amplitude.

**Basic H-Bridge Inverter:**
```
     +V_dc
      │
 [S1]   [S3]
  │     │
  ├─A   ├─B→ Load
  │     │
 [S2]   [S4]
  │     │
 GND   GND
```

**Switching Sequence:**
- S1&S4 ON: V_AB = +V_dc
- S2&S3 ON: V_AB = -V_dc
- S1&S3 or S2&S4: Short circuit (avoid!)

### 2.2 PWM Techniques

#### Sinusoidal PWM (SPWM)

**Principle:**
```
Compare high-frequency triangle carrier
with low-frequency sine reference
```

**Modulation Index:**
```
m_a = V_control / V_triangle
m_f = f_carrier / f_reference
```

**Output Spectrum:**
- Fundamental at f_reference
- Harmonics around m_f, 2m_f, etc.

#### Space Vector PWM (SVPWM)

**Advantages:**
- 15% higher DC bus utilization
- Lower harmonic distortion
- Better dynamic response

**Six Active Vectors + Two Zero Vectors**

### 2.3 Three-Phase Inverters

#### Circuit Topology:
```
     +V_dc
      │
 [S1]   [S3]   [S5]
  │     │     │
  ├─A   ├─B   ├─C → 3-Phase Load
  │     │     │
 [S2]   [S4]   [S6]
  │     │     │
 GND   GND   GND
```

**120° Conduction Mode:**
- Each switch conducts for 120°
- Only two switches ON at any time
- Simple control, lower switching losses

**180° Conduction Mode:**
- Each switch conducts for 180°
- Three switches ON simultaneously
- Higher output voltage

### 2.4 Multilevel Inverters

#### Diode-Clamped (NPC) Inverter
```
     +V_dc/2
      │
     [S1]
      │
     [S2]─── A
      │
     [S3]
      │
     -V_dc/2
```

**Output Levels:** +V_dc/2, 0, -V_dc/2

**Advantages:**
- Reduced dv/dt stress
- Lower EMI
- Better harmonic spectrum

### 2.5 Motor Drive Systems

#### DC Motor Drives

**Speed Control Methods:**
1. **Armature voltage control:** Below base speed
2. **Field weakening:** Above base speed

**Four-Quadrant Operation:**
```
      Torque
        ↑
    Q2   |   Q1
   ------+---→ Speed
    Q3   |   Q4
```

**Chopper Control:**
```
     +V_dc
      │
     [S]
      │
      ├─→ DC Motor
     [D]
      │
     GND
```

#### Induction Motor Drives

**V/f Control:**
```
Maintain V/f ratio constant for constant torque
Below base speed: Constant torque
Above base speed: Constant power
```

**Slip Control:**
```
ω_m = ω_s × (1 - s)
where s = slip
```

**Vector Control (Field-Oriented Control):**
- Decouples torque and flux components
- DC motor-like performance
- Complex control required

#### Synchronous Motor Drives

**Brushless DC (BLDC) Motors:**
- Electronic commutation
- Hall sensors or sensorless control
- High efficiency, maintenance-free

**Permanent Magnet Synchronous Motors (PMSM):**
- Sinusoidal back-EMF
- Vector control
- High power density

### 2.6 Drive Protection and Control

#### Protection Features:
- Overcurrent protection
- Overvoltage/undervoltage protection
- Over temperature protection
- Short-circuit protection
- Ground fault protection

#### Control Techniques:
- **Scalar control (V/f):** Simple, for constant loads
- **Vector control:** High performance, dynamic loads
- **Direct torque control (DTC):** Fast torque response

---

## 3. SMPS & Power Regulation

### 3.1 Switch Mode Power Supply Topologies

#### Flyback Converter

**Circuit:**
```
     +V_in
       │
      [S]───┐
       │    │
       │   [T] : n
       │    │
      GND   │
           [D]───[C] → V_out
            │    │
           GND  GND
```

**Analysis:**
```
V_out = V_in × (N_s/N_p) × (D/(1-D))
Operates in DCM or CCM
Uses transformer for isolation
```

**Design Considerations:**
- Transformer design critical
- Snubber circuit for voltage spikes
- Good for multiple outputs

#### Forward Converter

**Circuit:**
```
     +V_in
       │
      [S]───[T] : n ──[D1]──[L]──[C] → V_out
       │         │     │           │
      GND       [D2]  GND         GND
```

**Analysis:**
```
V_out = V_in × (N_s/N_p) × D
Requires reset winding or active clamp
D_max < 0.5 for transformer reset
```

#### Push-Pull Converter

**Circuit:**
```
     +V_in
       │
     Center-Tapped Transformer
       │
      [S1]   [S2]
       │     │
      GND   GND
         │
        [L]──[C] → V_out
         │    │
        GND  GND
```

**Analysis:**
```
V_out = 2 × V_in × (N_s/N_p) × D
Advantages: Good transformer utilization
Disadvantages: Requires center-tap, flux walking
```

#### Half-Bridge Converter

**Circuit:**
```
     +V_in
       │
     [C1]   [S1]
      │     │
      ├─┐   ├─[T] : n ──[L]──[C] → V_out
      │ │   │         │      │
     [C2]  [S2]      GND    GND
      │     │
     GND   GND
```

**Analysis:**
```
V_out = V_in × (N_s/N_p) × D
Voltage stress on switches: V_in
Good for medium power applications
```

#### Full-Bridge Converter

**Circuit:**
```
     +V_in
       │
     [S1]   [S3]
      │     │
      ├─[T] : n─├─[L]──[C] → V_out
      │     │         │
     [S2]  [S4]      GND
      │     │
     GND   GND
```

**Analysis:**
```
V_out = 2 × V_in × (N_s/N_p) × D
Voltage stress on switches: V_in
Highest power capability
```

### 3.2 Control Techniques

#### Voltage Mode Control

**Block Diagram:**
```
V_ref → Error Amp → PWM → Power Stage → V_out
                ↑               |
                └─── Feedback ──┘
```

**Advantages:**
- Simple implementation
- Single feedback loop

**Disadvantages:**
- Slow response to input changes
- Poor line regulation

#### Current Mode Control

**Block Diagram:**
```
V_ref → Error Amp → Current Comp → PWM → Power Stage → V_out
                ↑               |              |
                └─── Voltage Feedback ─────────┘
                            |
                    Current Sense
```

**Advantages:**
- Faster response
- Automatic peak current limiting
- Better line regulation

**Disadvantages:**
- Subharmonic oscillation at D > 0.5
- Requires slope compensation

### 3.3 Power Factor Correction (PFC)

#### Why PFC?
- Reduces harmonic distortion
- Meets regulatory standards (IEC 61000-3-2)
- Improves power quality

#### Boost PFC Circuit:
```
     AC Input → Bridge Rectifier → [L]──[S]──┐
                         │         │    │    │
                        GND       [D]  [C] → V_out
                                  │    │
                                 GND  GND
```

**Control:**
- Shape input current to follow input voltage
- Maintain high power factor (PF > 0.99)
- Regulate output voltage

#### PFC Controller ICs:
- UC3854 (Classic average current mode)
- UCC28180 (Modern transition mode)
- L6562 (Critical conduction mode)

### 3.4 Thermal Management

#### Heat Transfer Mechanisms:
- **Conduction:** Through solid materials
- **Convection:** Through fluids (air/liquid)
- **Radiation:** Electromagnetic waves

#### Heat Sink Design:
```
θ_ja = θ_jc + θ_cs + θ_sa
where:
θ_ja = Junction-to-ambient thermal resistance
θ_jc = Junction-to-case
θ_cs = Case-to-sink
θ_sa = Sink-to-ambient
```

**Power Dissipation:**
```
P_diss = (T_j_max - T_amb) / θ_ja
```

#### Example Calculation:
```
MOSFET: T_j_max = 150°C, θ_jc = 1.5°C/W
Heat sink: θ_sa = 5°C/W, Thermal grease: θ_cs = 0.5°C/W
Ambient: T_amb = 40°C

θ_ja = 1.5 + 0.5 + 5 = 7°C/W
Max P_diss = (150 - 40) / 7 = 15.7W
```

### 3.5 EMI/EMC Considerations

#### EMI Sources:
- Switching transitions
- Diode reverse recovery
- Parasitic oscillations

#### Mitigation Techniques:
- **Input filters:** LC, π filters
- **Snubber circuits:** RC, RCD
- **Shielding:** Magnetic, electrostatic
- **Layout:** Proper grounding, trace routing

#### EMC Standards:
- **CISPR 22:** Conducted and radiated emissions
- **IEC 61000-4:** Immunity tests
- **FCC Part 15:** US emissions requirements

---

## 4. Battery Management

### 4.1 Battery Fundamentals

#### Battery Parameters

**Capacity (Ah):**
```
C = I × t
where I = discharge current, t = time to cutoff voltage
```

**C-rate:**
```
1C = current that discharges battery in 1 hour
2C = current that discharges battery in 0.5 hour
C/2 = current that discharges battery in 2 hours
```

**State of Charge (SOC):**
```
SOC = (Remaining Capacity / Total Capacity) × 100%
```

**Depth of Discharge (DOD):**
```
DOD = 100% - SOC
```

#### Battery Types

**Lead-Acid:**
- **Advantages:** Low cost, high surge current
- **Disadvantages:** Heavy, low energy density
- **Applications:** Automotive, UPS

**Nickel-Based:**
- NiMH, NiCd
- **Advantages:** Good cycle life, high power
- **Disadvantages:** Memory effect (NiCd), self-discharge

**Lithium-Ion:**
- **Advantages:** High energy density, low self-discharge
- **Disadvantages:** Protection circuit required, aging
- **Chemistry:** LCO, NMC, LFP, LTO

### 4.2 Battery Charging Techniques

#### Constant Current/Constant Voltage (CC/CV)

**Charging Profile:**
```
Current ↑
        |‾‾‾‾‾‾‾‾⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯
        |         ⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯
        |                       ⎯⎯⎯⎯⎯⎯⎯⎯
        +---------------------------→ Time

Voltage ↑
        |                       ‾‾‾‾‾‾⎯⎯⎯⎯⎯⎯⎯
        |         ‾‾‾‾‾‾‾‾‾‾‾‾⎯
        |‾‾‾‾‾‾‾⎯
        +---------------------------→ Time
```

**Stages:**
1. **Pre-charge:** For deeply discharged batteries
2. **Constant Current:** Bulk charging
3. **Constant Voltage:** Absorption charging
4. **Float/Trickle:** Maintenance charging

#### Charger Topologies

**Linear Chargers:**
- Simple, low noise
- Inefficient (power dissipation = (V_in - V_batt) × I_chg)
- Good for low current applications

**Switch-Mode Chargers:**
- High efficiency (>90%)
- More complex
- Buck, boost, or buck-boost topologies

### 4.3 Battery Management Systems (BMS)

#### BMS Functions:

**Protection:**
- Overvoltage protection (OVP)
- Undervoltage protection (UVP)
- Overcurrent protection (OCP)
- Short-circuit protection (SCP)
- Overtemperature protection (OTP)

**Monitoring:**
- Cell voltage monitoring
- Temperature monitoring
- Current monitoring
- State of Charge estimation

**Balance:**
- Passive balancing
- Active balancing

#### Cell Balancing Techniques

**Passive Balancing:**
```
     Cell
      │
     [R]
      │
     [S] (Switch)
      │
     GND
```
- Dissipates excess energy as heat
- Simple, low cost
- Inefficient

**Active Balancing:**
- **Capacitive:** Flying capacitor
- **Inductive:** Transformer-based
- **DC-DC converter:** Bidirectional

### 4.4 SOC Estimation Methods

#### Coulomb Counting (Current Integration)
```
SOC(t) = SOC(t₀) + (1/C_nominal) × ∫ I(τ) dτ
```
**Advantages:** Simple implementation
**Disadvantages:** Accumulates error over time

#### Voltage-Based Methods
- Open Circuit Voltage (OCV) vs SOC curve
- Requires rest period for accurate measurement

#### Kalman Filter
- Model-based estimation
- Accounts for process and measurement noise
- Computationally intensive

#### Hybrid Methods
Combine coulomb counting with voltage/current corrections

### 4.5 Battery Pack Design

#### Series-Parallel Configuration

**Example: 3S2P Configuration:**
```
Cell11 → Cell12 → Cell13
   │        │        │
Cell21 → Cell22 → Cell23
```
- **Voltage:** 3 × V_cell
- **Capacity:** 2 × C_cell

#### Fuse and Protection
- **Main fuse:** Overcurrent protection
- **Cell fuses:** Individual cell protection
- **Contactors:** High-current switching
- **Pre-charge circuit:** Limits inrush current

#### Thermal Management

**Air Cooling:**
- Natural convection
- Forced air (fans)
- Simple, low cost

**Liquid Cooling:**
- Coolant plates
- Higher cooling capacity
- More complex

**Phase Change Materials:**
- Passive cooling
- For high-power applications

### 4.6 Battery Testing and Characterization

#### Capacity Test:
```
Discharge at constant current to cutoff voltage
Measure time to calculate capacity
```

#### Internal Resistance Measurement:
```
DC method: R = ΔV / ΔI
AC method: Impedance spectroscopy
```

#### Cycle Life Testing:
```
Charge/discharge cycles until capacity drops to 80%
of initial capacity
```

#### Safety Tests:
- Overcharge test
- Short-circuit test
- Crush test
- Thermal abuse test

### 4.7 Applications

#### Electric Vehicles:
- High energy density requirements
- Fast charging capability
- Thermal management critical

#### Renewable Energy Storage:
- Deep cycle capability
- Long cycle life
- Cost sensitivity

#### Portable Electronics:
- Small size, lightweight
- Safety paramount
- Fast charging desired

#### UPS Systems:
- Reliability critical
- Float operation
- High surge capability

---

## Practice Problems

### Problem 1: Buck Converter Design
```
Design a buck converter with:
V_in = 48V, V_out = 12V, I_out = 5A, f_sw = 100kHz
Output ripple: <1% of V_out
Current ripple: <30% of I_out
Calculate L and C values.
```

### Problem 2: Three-Phase Inverter
```
A three-phase inverter has V_dc = 600V.
Calculate the RMS line voltage for:
a) Square wave operation
b) SPWM with m_a = 0.8
```

### Problem 3: Battery Pack Design
```
Design a 48V, 10kWh battery pack using 3.2V, 100Ah LFP cells.
Calculate:
a) Series-parallel configuration
b) Number of cells
c) Approximate weight (assume 3kg per cell)
```

### Problem 4: PFC Design
```
A boost PFC operates from 230VAC, 50Hz.
Output: 400VDC, 500W
Calculate:
a) Input current at full load
b) Boost inductor value for CCM operation
c) Output capacitor for <5V ripple
```

### Problem 5: Thermal Design
```
A MOSFET dissipates 25W in a converter.
θ_jc = 1.0°C/W, θ_cs = 0.5°C/W
Maximum junction temperature: 125°C
Ambient temperature: 40°C
Calculate the required heat sink thermal resistance.
```

## Conclusion

This comprehensive power electronics course covers the fundamental principles and practical design considerations for modern power conversion systems. From basic rectifiers to advanced battery management, each topic builds upon foundational concepts to provide a complete understanding of power electronic systems.

Key takeaways:
- Power semiconductor devices are the building blocks
- Converter topologies trade off complexity vs performance
- Control techniques determine system dynamics
- Thermal management is critical for reliability
- Battery systems require sophisticated management

Power electronics continues to evolve with wide-bandgap semiconductors (SiC, GaN), digital control, and advanced battery technologies driving innovation across transportation, renewable energy, and industrial applications.
