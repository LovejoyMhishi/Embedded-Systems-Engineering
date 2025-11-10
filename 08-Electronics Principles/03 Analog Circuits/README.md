<h1 align="center">Analog Circuits</h1> 

## Table of Contents
1. [Amplifiers & Filters](#1-amplifiers--filters)
2. [Oscillators](#2-oscillators)
3. [Feedback & Stability](#3-feedback--stability)
4. [Signal Conditioning](#4-signal-conditioning)

---

## 1. Amplifiers & Filters

### 1.1 Amplifier Fundamentals

#### Amplifier Classification

**By Frequency Response:**
- DC Amplifiers: Amplify down to 0 Hz
- AC Amplifiers: Capacitively coupled, block DC
- Video Amplifiers: Wide bandwidth (several MHz)
- RF Amplifiers: Radio frequency operation

**By Configuration:**
- Common Emitter/Source (Voltage Amplifier)
- Common Collector/Drain (Buffer/Current Amplifier)
- Common Base/Gate (Current Buffer)

#### Amplifier Parameters

**Voltage Gain:**
```
A_v = V_out / V_in
```

**Current Gain:**
```
A_i = I_out / I_in
```

**Power Gain:**
```
A_p = P_out / P_in = A_v × A_i
```

**Input Impedance:**
```
Z_in = V_in / I_in
```

**Output Impedance:**
```
Z_out = V_open / I_short
```

### 1.2 Single-Stage Amplifiers

#### Common Emitter Amplifier

**Circuit:**
```
     +Vcc
      │
     [Rc]
      │
      C←──[Rb1]─┐
      │         │
      B        V_in
      │         │
     [Re]      [Rb2]
      │         │
     [Ce]      GND
      │
     GND
```

**DC Analysis:**
```
V_b = Vcc × Rb2/(Rb1 + Rb2)
V_e = V_b - V_be (≈ 0.7V for Si)
I_e = V_e / Re
I_c ≈ I_e
V_ce = Vcc - I_c × (Rc + Re)
```

**AC Analysis:**
```
Voltage Gain: A_v ≈ -Rc / (r_e + Re)
where r_e = 25mV / I_e (thermal voltage)

Input Impedance: Z_in ≈ Rb1 ∥ Rb2 ∥ (β × (r_e + Re))
Output Impedance: Z_out ≈ Rc
```

**Design Example:**
```
Requirements: A_v = -50, Vcc = 12V, I_c = 2mA

Choose: Re = 100Ω (bypass with Ce)
r_e = 25mV / 2mA = 12.5Ω
A_v = -Rc / (r_e + Re) = -50
Rc = 50 × (12.5 + 100) = 5.625kΩ (use 5.6kΩ)

V_ce = 12V - 2mA × (5.6kΩ + 100Ω) = 12 - 11.4 = 0.6V (too low!)
Need to increase Re or decrease Rc for proper biasing.
```

#### Common Source Amplifier (MOSFET)

**Circuit:**
```
     +Vdd
      │
     [Rd]
      │
      D←──[Rg]─┐
      │        │
      G       V_in
      │        │
     [Rs]     GND
      │
     [Cs]
      │
     GND
```

**Analysis:**
```
Voltage Gain: A_v = -g_m × (Rd ∥ r_o)
where g_m = transconductance
r_o = output resistance

Input Impedance: Z_in ≈ Rg (very high)
Output Impedance: Z_out ≈ Rd ∥ r_o
```

### 1.3 Multi-Stage Amplifiers

#### Cascaded Amplifiers

**Overall Gain:**
```
A_total = A_v1 × A_v2 × A_v3 × ...
```

**Impedance Matching:**
- Output Z of stage n = Input Z of stage n+1
- Prevents loading effects

**Two-Stage CE Amplifier Example:**
```
Stage 1: High input impedance, moderate gain
Stage 2: Higher gain, drives load
Coupling: Capacitive between stages
```

#### Darlington Pair

**Circuit:**
```
     +Vcc
      │
     [Rc]
      │
      C2
      │
      B2←─C1
      │    │
      E2  B1←─V_in
      │    │
     [Re]  E1
      │    │
     GND  GND
```

**Characteristics:**
```
Current Gain: β_total ≈ β1 × β2
Input Impedance: Very high
V_be drop: ≈ 1.4V (2 × 0.7V)
```

### 1.4 Differential Amplifiers

#### Basic Differential Pair

**Circuit:**
```
     +Vcc
      │
     [Rc1]     [Rc2]
      │          │
      C1         C2
      │          │
      B1←─+──→B2
      │   │   │
     [Re1]   [Re2]
      │   │   │
      E1──┴──E2
            │
           [I_ee]
            │
           -Vee
```

**Differential Gain:**
```
A_d = V_out / (V1 - V2) = -g_m × Rc
```

**Common-Mode Gain:**
```
A_cm = V_out / V_cm ≈ -Rc / (2 × R_ee)
```

**Common-Mode Rejection Ratio (CMRR):**
```
CMRR = |A_d / A_cm| ≈ g_m × R_ee
```

### 1.5 Power Amplifiers

#### Class A Amplifier

**Characteristics:**
- Conducts for 360° of input cycle
- Low efficiency (theoretical max: 25%, practical: 15-20%)
- Simple design, low distortion

**Efficiency Calculation:**
```
η = (P_out / P_dc) × 100%
P_out_max = V_cc² / (8 × R_L)
P_dc = V_cc × I_cq
```

#### Class B Amplifier

**Push-Pull Configuration:**
```
     +Vcc
      │
      Q1 (NPN)
      │
V_in─┴─┐
       ├──→ V_out
      ┌┴─
      Q2 (PNP)
      │
     -Vcc
```

**Characteristics:**
- Each transistor conducts 180°
- Theoretical efficiency: 78.5%
- Crossover distortion problem

#### Class AB Amplifier

**Solution to Crossover Distortion:**
- Small bias current to keep transistors barely on
- Compromise between Class A and Class B

### 1.6 Active Filters

#### Filter Types and Characteristics

**Low-Pass Filter Response:**
```
    Gain
      ↑
      |‾‾‾‾‾‾‾‾⎯⎯⎯
      |         ⎯⎯⎯⎯⎯
      |           ⎯⎯⎯⎯⎯
      +--------------→ Frequency
           f_c
```

**High-Pass Filter Response:**
```
    Gain
      ↑
      |           ⎯⎯⎯⎯⎯
      |         ⎯⎯⎯⎯⎯
      |‾‾‾‾‾‾‾‾⎯⎯⎯
      +--------------→ Frequency
           f_c
```

#### First-Order Active Filters

**Low-Pass:**
```
     ┌──[R2]──┐
     │        │
V_in─┴─[R1]──┴─ V_out
           │
          [C]
           │
          GND
```
```
Cutoff: f_c = 1/(2π × R1 × C)
Gain: A_v = 1 + R2/R1
```

**High-Pass:**
```
     ┌──[R2]──┐
     │        │
V_in─┴─[C]───┴─ V_out
           │
          [R1]
           │
          GND
```
```
Cutoff: f_c = 1/(2π × R1 × C)
Gain: A_v = 1 + R2/R1
```

#### Second-Order Filters (Sallen-Key)

**Low-Pass Sallen-Key:**
```
     V_in─[R1]─┬─[R2]─┐
               │      │
              [C1]    ├─ V_out
               │      │
              GND    [C2]
                     │
                    GND
```
```
f_c = 1/(2π × √(R1×R2×C1×C2))
Q = √(R1×R2×C1×C2) / [C1×(R1+R2)]
```

#### Filter Design Example

**Design a 2nd-order Butterworth low-pass filter with f_c = 1kHz**

```
Choose equal components: R1 = R2 = R, C1 = C2 = C
f_c = 1/(2πRC) = 1000Hz

Let C = 0.01μF
Then R = 1/(2π × 1000 × 10⁻⁸) = 15.9kΩ (use 16kΩ)

For Butterworth: Q = 0.707
Gpass = 3 - 1/Q = 3 - 1/0.707 = 1.586
Set R2/R1 = 0.586 (choose R1=10kΩ, R2=5.86kΩ)
```

---

## 2. Oscillators

### 2.1 Oscillator Fundamentals

#### Barkhausen Criterion

**Oscillation Conditions:**
1. **Loop Gain**: |Aβ| ≥ 1
2. **Phase Shift**: ∠Aβ = 0° or 360°

**General Structure:**
```
     ┌─────────┐
     │         │
V_in─┴─→ Amp ─→ V_out
      ↑        │
      │        │
      └─ β Network ←┘
```

### 2.2 RC Oscillators

#### Phase Shift Oscillator

**Circuit:**
```
     +Vcc
      │
     [Rc]
      │
      C←─[R1]─[C1]─[R2]─[C2]─[R3]─┐
      │                            │
      B                           V_out
      │                            │
     [Re]                         GND
      │
     GND
```

**Analysis:**
```
Each RC section provides ≈ 60° phase shift
Total phase shift: 180° (3 sections)
Frequency: f = 1/(2πRC√6)
Gain requirement: A_v ≥ 29
```

#### Wien Bridge Oscillator

**Circuit:**
```
     ┌──[R1]──┐
     │        │
V_in─┴─[C1]──┴─┐
           │   │
          GND  │
               ├─ V_out
     ┌──[R2]──┐│
     │        ││
    [C2]      ││
     │        ││
    GND      GND│
               │
              [Rf]
               │
              [Rg]
               │
              GND
```

**Analysis:**
```
Frequency: f = 1/(2π√(R1×R2×C1×C2))
If R1=R2=R, C1=C2=C: f = 1/(2πRC)
Gain requirement: A_v ≥ 3 (set by Rf/Rg)
```

### 2.3 LC Oscillators

#### Colpitts Oscillator

**Circuit:**
```
     +Vcc
      │
     [Rc]
      │
      C←─── L ───┐
      │          │
      B         [C1]      [C2]
      │          │          │
     GND        GND        GND
               Tank Circuit
```

**Analysis:**
```
Frequency: f = 1/(2π√(L × C_eq))
where C_eq = (C1 × C2)/(C1 + C2)
```

#### Hartley Oscillator

**Circuit:**
```
     +Vcc
      │
     [Rc]
      │
      C←─── C ───┐
      │          │
      B         [L1]      [L2]
      │          │          │
     GND        GND        GND
               Tank Circuit
```

**Analysis:**
```
Frequency: f = 1/(2π√(C × L_eq))
where L_eq = L1 + L2
```

### 2.4 Crystal Oscillators

#### Crystal Equivalent Circuit
```
     ┌──[L]──[C]──┐
     │            │
     └───[R]──┴──[Co]─┘
```

**Characteristics:**
- Very high Q factor (10,000-1,000,000)
- Excellent frequency stability
- Two resonant frequencies:
  - Series resonance: f_s = 1/(2π√(LC))
  - Parallel resonance: f_p = f_s × √(1 + C/Co)

#### Pierce Crystal Oscillator

**Circuit:**
```
     +Vcc
      │
     [Rc]
      │
      C←───┐
      │    │
      B   [C1]  XTAL  [C2]
      │    │     │     │
     GND  GND   GND   GND
```

**Advantages:**
- Simple design
- Good stability
- Widely used in microcontrollers

### 2.5 Oscillator Design Example

**Design a 1MHz Colpitts Oscillator**

```
Choose: L = 10μH
f = 1/(2π√(L × C_eq)) = 1MHz

C_eq = 1/((2πf)² × L) = 1/((2π×10⁶)² × 10⁻⁵) = 2.53nF

Choose C1 = C2 for maximum output
C_eq = (C × C)/(C + C) = C/2
C = 2 × C_eq = 5.06nF (use 5nF)

Choose transistor with f_T > 10×f_osc = 10MHz
Bias for class C operation
```

---

## 3. Feedback & Stability

### 3.1 Feedback Concepts

#### Basic Feedback System
```
     ┌─────────┐
     │         │
V_in─┴─→ A ───→ V_out
      ↑        │
      │        │
      └─ β ←───┘
```

#### Closed-Loop Gain
```
A_f = A / (1 + Aβ)
```

#### Types of Feedback

**Voltage Series Feedback:**
- Samples output voltage
- Mixes in series with input
- Increases input impedance
- Decreases output impedance

**Voltage Shunt Feedback:**
- Samples output voltage
- Mixes in shunt with input
- Decreases both input and output impedance

**Current Series Feedback:**
- Samples output current
- Mixes in series with input
- Increases both input and output impedance

**Current Shunt Feedback:**
- Samples output current
- Mixes in shunt with input
- Decreases input impedance
- Increases output impedance

### 3.2 Effects of Negative Feedback

#### Desirable Effects:
- **Stabilizes gain**: A_f ≈ 1/β if Aβ >> 1
- **Reduces distortion**
- **Increases bandwidth**
- **Controls impedance levels**

#### Mathematical Relationships:

**Gain Stability:**
```
dA_f/A_f = (1/(1+Aβ)) × (dA/A)
```

**Bandwidth Extension:**
```
BW_f = BW × (1 + Aβ)
```

**Distortion Reduction:**
```
D_f = D / (1 + Aβ)
```

### 3.3 Stability Analysis

#### Gain and Phase Margin

**Gain Margin:**
```
GM = 20log₁₀(1/|Aβ|) at phase = -180°
```

**Phase Margin:**
```
PM = 180° + ∠Aβ at |Aβ| = 1
```

**Stability Criteria:**
- GM > 10dB and PM > 45° for good stability
- GM > 0dB and PM > 0° for marginal stability

#### Bode Plot Analysis

**Example System:**
```
A(s) = A₀ / [(1 + s/ω₁)(1 + s/ω₂)(1 + s/ω₃)]
```

**Stability Assessment:**
- Plot magnitude and phase vs frequency
- Check gain and phase margins
- Identify potential oscillation frequencies

### 3.4 Compensation Techniques

#### Dominant Pole Compensation

**Method:**
- Add a capacitor to create a dominant low-frequency pole
- Forces -20dB/decade slope at unity gain frequency

**Implementation:**
```
Miller Compensation: Add capacitor between input and output
```

#### Pole-Zero Compensation

**Method:**
- Add series RC network
- Cancels existing pole with new zero
- Places new pole at higher frequency

### 3.5 Practical Feedback Example

**Series-Shunt Feedback Amplifier:**
```
     +Vcc
      │
     [Rc]
      │
      C1←─[Rf]─┐
      │        │
      B1      V_out
      │        │
     [Re1]     │
      │        │
     GND      [R1]
              │
             GND
```

**Analysis:**
```
β = R1/(R1 + Rf)
A_vf ≈ 1/β = 1 + Rf/R1
Z_inf = Z_in × (1 + Aβ)
Z_outf = Z_out / (1 + Aβ)
```

---

## 4. Signal Conditioning

### 4.1 Amplifier Configurations

#### Instrumentation Amplifier

**Circuit:**
```
     V1 ──[Rg]── V2
           │
     ┌───[R1]───┐
     │          │
    [R2]       [R2]
     │          │
     ├─ A1 ─┐   ├─ A2 ─┐
     │      │   │      │
    GND     │  GND     │
            │          │
           [R3]       [R3]
            │          │
            └─ A3 ────→ V_out
```

**Advantages:**
- High input impedance
- High CMRR
- Easily programmable gain: G = 1 + (2R2/Rg)

#### Programmable Gain Amplifier (PGA)

**Digital Control:**
```
Gain = 1 + (R_feedback / R_selected)
Use analog switches or digital potentiometers
```

### 4.2 Analog Computation Circuits

#### Summing Amplifier
```
     V1 ─[R1]─┐
     V2 ─[R2]─┼─┐
     V3 ─[R3]─┘ │
               ├─ V_out
          ┌──[Rf]──┘
          │
         GND
```
```
V_out = -Rf × (V1/R1 + V2/R2 + V3/R3)
```

#### Difference Amplifier
```
     V1 ─[R1]─┐
              ├─ V_out
     V2 ─[R2]─┘
          │
         [R3]
          │
         GND
```
```
V_out = (R2/R1) × (V2 - V1)  (if R2/R1 = R4/R3)
```

#### Logarithmic Amplifier
```
     ┌───|>|───┐
     │         │
V_in─┴─[R]────┴─ V_out
           │
          GND
```
```
V_out = -V_T × ln(V_in / (I_s × R))
where V_T = thermal voltage (25mV)
```

### 4.3 Sample and Hold Circuits

**Basic Circuit:**
```
     V_in ────┬───→ V_out
             │
        Control ──○ S/H
             │
            [C_hold]
             │
            GND
```

**Key Parameters:**
- **Aperture Time**: Time to capture input
- **Acquisition Time**: Time to charge capacitor
- **Droop Rate**: Voltage decay during hold
- **Feedthrough**: Input signal leakage

### 4.4 Analog Switches

#### MOSFET Analog Switch
```
     Source ──○── Drain
              │
           Gate Control
```

**Important Parameters:**
- **On-Resistance (R_on)**: Typically 5-100Ω
- **Charge Injection**: Clock feedthrough
- **Breakdown Voltage**
- **Leakage Current**

### 4.5 Voltage References

#### Zener Diode Reference
```
     +V_in
      │
     [R_limit]
      │
      ├─|>|─┐
      │     │
     GND   V_ref
```

**Limitations:**
- Temperature drift
- Limited accuracy
- Noise

#### Bandgap Reference

**Principle:**
- Combines positive and negative TC voltages
- Theoretical output: 1.22V (silicon bandgap)

**Advantages:**
- Low temperature coefficient
- High accuracy
- Can generate any voltage

### 4.6 Complete Signal Conditioning System

**Temperature Measurement Example:**
```
Thermocouple → Instrumentation Amp → Low-Pass Filter → 
Sample/Hold → ADC → Microcontroller
```

**Design Specifications:**
- Thermocouple output: 0-50mV
- Required range: 0-5V for ADC
- Gain needed: 100
- Bandwidth: 0-10Hz (slow temperature changes)
- 50Hz noise rejection

**Circuit Implementation:**
```
Thermocouple → INA128 (G=100) → 
2nd-order LPF (f_c=10Hz) → 
LF398 Sample/Hold → 
ADC0804
```

**Filter Design:**
```
f_c = 10Hz, 2nd-order Butterworth
Use Sallen-Key configuration
R = 16kΩ, C = 1μF
f_c = 1/(2πRC) = 9.95Hz ✓
```

### 4.7 Noise Considerations

#### Types of Noise

**Thermal Noise (Johnson Noise):**
```
V_n = √(4kTRB)
Where:
k = Boltzmann's constant (1.38×10⁻²³ J/K)
T = Temperature (K)
R = Resistance (Ω)
B = Bandwidth (Hz)
```

**Shot Noise:**
```
I_n = √(2qI_dcB)
Where:
q = electron charge (1.6×10⁻¹⁹ C)
I_dc = DC current (A)
```

**1/f Noise (Flicker Noise):**
- Important at low frequencies
- Proportional to 1/f

#### Signal-to-Noise Ratio (SNR)
```
SNR = 20log₁₀(V_signal / V_noise)
```

#### Noise Reduction Techniques
- **Filtering**: Limit bandwidth to signal band
- **Shielding**: Prevent external interference
- **Grounding**: Proper star grounding
- **Component Selection**: Low-noise op-amps, metal film resistors

---

## Practice Problems

### Problem 1: Amplifier Design
```
Design a common emitter amplifier with:
- Voltage gain: -20
- Supply voltage: 12V
- Load resistance: 10kΩ
- Input impedance: > 5kΩ
Calculate all component values.
```

### Problem 2: Oscillator Design
```
Design a Wien bridge oscillator for 1kHz.
Calculate all component values and verify
the gain requirement is satisfied.
```

### Problem 3: Feedback Analysis
```
A amplifier has open-loop gain A = 100,000
and open-loop bandwidth = 10Hz.
With negative feedback β = 0.01, calculate:
- Closed-loop gain
- Closed-loop bandwidth
- Gain stability improvement
```

### Problem 4: Filter Design
```
Design a 2nd-order active low-pass filter with:
- Cutoff frequency: 2kHz
- Butterworth response
- DC gain: 10
Use Sallen-Key topology.
```

### Problem 5: Complete System
```
Design a signal conditioning system for a
strain gauge that outputs ±10mV.
The system should:
- Amplify to ±5V range
- Filter out 60Hz noise
- Provide high input impedance
Draw the complete circuit.
```

## Conclusion

This comprehensive analog circuits course covers the fundamental building blocks of analog electronic systems. From basic single-stage amplifiers to complex feedback systems and signal conditioning circuits, each topic builds upon the previous ones to provide a complete understanding of analog circuit design.

Key takeaways:
- Amplifiers form the core of analog signal processing
- Oscillators provide precise frequency generation
- Feedback enables control of amplifier characteristics
- Signal conditioning bridges sensors to digital systems

Remember that real-world analog design requires careful consideration of non-ideal effects, temperature stability, noise, and practical component limitations. Always simulate your designs before building and test thoroughly under various operating conditions!
