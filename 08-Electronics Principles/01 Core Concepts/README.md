<h1 align="center">Electrical Circuit Analysis</h1>

## Table of Contents
1. [Core Concepts](#1-core-concepts)
2. [Basic Electrical Laws](#2-basic-electrical-laws)
3. [Circuit Theorems](#3-circuit-theorems)
4. [AC & DC Analysis](#4-ac--dc-analysis)
5. [Frequency Response](#5-frequency-response)

---

## 1. Core Concepts

### 1.1 Fundamental Quantities

#### Electric Charge (Q)
- **Definition**: Fundamental property of matter that causes it to experience force in electromagnetic field
- **Unit**: Coulomb (C)
- **Elementary charge**: e = 1.602 × 10⁻¹⁹ C
- **Symbol**: Q

#### Electric Current (I)
- **Definition**: Rate of flow of electric charge
- **Formula**: I = dQ/dt
- **Unit**: Ampere (A) = Coulomb/second
- **Symbol**: I

**Example**: 
If 2 Coulombs of charge pass through a point in 4 seconds:
```
I = Q/t = 2C/4s = 0.5 A
```

#### Voltage (V)
- **Definition**: Electric potential difference between two points
- **Also called**: Electromotive Force (EMF)
- **Unit**: Volt (V) = Joule/Coulomb
- **Symbol**: V or E

**Physical Analogy**:
```
Think of water flowing through a pipe:
- Voltage = Water Pressure
- Current = Water Flow Rate
- Resistance = Pipe Constriction
```

#### Resistance (R)
- **Definition**: Opposition to current flow
- **Unit**: Ohm (Ω)
- **Symbol**: R
- **Formula**: R = ρL/A (where ρ = resistivity, L = length, A = cross-sectional area)

### 1.2 Circuit Components

#### Resistor
```
┌───╂───┐
     R
└───────┘
```
- **Function**: Limits current flow
- **Power Dissipation**: P = I²R = V²/R

#### Capacitor
```
┌───||───┐
     C
└────────┘
```
- **Function**: Stores energy in electric field
- **Formula**: C = Q/V
- **Unit**: Farad (F)

#### Inductor
```
┌───͡───┐
     L
└──────┘
```
- **Function**: Stores energy in magnetic field
- **Formula**: V = L di/dt
- **Unit**: Henry (H)

### 1.3 Power and Energy

#### Electrical Power
```
P = V × I
```
- **Unit**: Watt (W)

#### Electrical Energy
```
E = P × t = V × I × t
```
- **Unit**: Joule (J) or Watt-hour (Wh)

**Example Calculation**:
```
A 100W light bulb operates at 120V:
I = P/V = 100W/120V = 0.833A
R = V/I = 120V/0.833A = 144Ω
```

---

## 2. Basic Electrical Laws

### 2.1 Ohm's Law

#### Fundamental Relationship
```
V = I × R
```
Where:
- V = Voltage (Volts)
- I = Current (Amperes)
- R = Resistance (Ohms)

#### Ohm's Law Triangle
```
    V
   / \
  I × R
```

**Example Problem**:
```
Given: R = 10Ω, V = 20V
Find: I

Solution: I = V/R = 20V/10Ω = 2A
```

### 2.2 Kirchhoff's Current Law (KCL)

#### Statement
> The sum of currents entering a node equals the sum of currents leaving the same node.

#### Mathematical Form
```
Σ I_in = Σ I_out
```
or
```
Σ I = 0 (with sign convention)
```

**Visual Representation**:
```
     I₁ → ● ← I₂
          |
          ↓ I₃
```
```
Equation: I₁ + I₂ = I₃
```

**Example**:
```
     2A → ● ← 3A
          |
          ↓ Iₓ
```
```
KCL: 2A + 3A = Iₓ
Therefore: Iₓ = 5A
```

### 2.3 Kirchhoff's Voltage Law (KVL)

#### Statement
> The sum of all voltage drops around any closed loop equals zero.

#### Mathematical Form
```
Σ V = 0
```

**Sign Convention**:
- Voltage drop: Positive when going from + to -
- Voltage rise: Negative when going from + to -

**Example Circuit**:
```
     +--R1--+--R2--+
     |      |      |
    V1     V2     V3
     |      |      |
     +------+------+
```
```
KVL: V1 + V2 + V3 = 0
```

### 2.4 Detailed KVL Example

**Circuit**:
```
     +12V---[R1=2Ω]---[V2=?]---[R3=3Ω]---(-5V)
                    |
                   [I=2A]
```

**Solution**:
```
Using KVL: 12V - V_R1 - V2 - V_R3 - (-5V) = 0

Calculate voltage drops:
V_R1 = I × R1 = 2A × 2Ω = 4V
V_R3 = I × R3 = 2A × 3Ω = 6V

Substitute: 12V - 4V - V2 - 6V + 5V = 0
Simplify: 7V - V2 = 0
Therefore: V2 = 7V
```

---

## 3. Circuit Theorems

### 3.1 Superposition Theorem

#### Statement
> In a linear circuit with multiple independent sources, the response (voltage or current) can be found by summing the individual responses caused by each independent source acting alone, with all other independent sources turned off.

#### Turning Off Sources:
- **Voltage Source → Short Circuit**
- **Current Source → Open Circuit**

#### Procedure:
1. Turn off all sources except one
2. Calculate the desired response
3. Repeat for each source
4. Sum all individual responses

**Example Circuit**:
```
     +--[R1]--+
     |        |
    V1       [R2]
     |        |
     +--I1----+
```

**Step-by-step Solution**:

*Step 1: V1 active, I1 off*
```
V1 → Short circuit for I1
Calculate contribution from V1
```

*Step 2: I1 active, V1 off*
```
V1 → Short circuit
Calculate contribution from I1
```

*Step 3: Superposition*
```
Total response = Response₁ + Response₂
```

### 3.2 Thevenin's Theorem

#### Statement
> Any linear electrical network with voltage and current sources and resistances can be replaced by an equivalent circuit consisting of a single voltage source (V_th) in series with a single resistance (R_th).

#### Thevenin Equivalent:
```
     +---[R_th]---+
     |           |
    V_th        [Load]
     |           |
     +-----------+
```

#### Finding Thevenin Parameters:

1. **V_th**: Open-circuit voltage across terminals
2. **R_th**: Equivalent resistance looking into terminals with all independent sources turned off

**Example**:
```
Circuit: 
     +--[R1=4Ω]--+--[R2=6Ω]--+
     |           |           |
   12V          A ●         B ●
     |           |           |
     +-----------+-----------+
```

**Solution**:
```
V_th = Voltage between A and B with open circuit
Using voltage divider: V_th = 12V × (6Ω)/(4Ω+6Ω) = 7.2V

R_th = Resistance between A and B with 12V shorted
R_th = R1∥R2 = (4×6)/(4+6) = 2.4Ω
```

### 3.3 Norton's Theorem

#### Statement
> Any linear electrical network can be replaced by an equivalent circuit consisting of a single current source (I_n) in parallel with a single resistance (R_n).

#### Norton Equivalent:
```
     +---[I_n]---+
     |          |
     +---[R_n]---+
           |
         [Load]
```

#### Finding Norton Parameters:

1. **I_n**: Short-circuit current through terminals
2. **R_n**: Same as R_th (equivalent resistance with sources off)

### 3.4 Maximum Power Transfer Theorem

#### Statement
> Maximum power is transferred from source to load when the load resistance equals the Thevenin resistance of the source.

#### Condition for Maximum Power:
```
R_load = R_th
```

#### Maximum Power Formula:
```
P_max = V_th² / (4 × R_th)
```

**Proof**:
```
P_load = I² × R_load = [V_th/(R_th + R_load)]² × R_load

Differentiate with respect to R_load and set to zero:
dP/dR_load = 0 when R_load = R_th
```

---

## 4. AC & DC Analysis

### 4.1 DC Analysis

#### Resistive Circuits Only
- Capacitors → Open circuits
- Inductors → Short circuits

**Example RC Circuit DC Analysis**:
```
     +--[R]--+--[C]--+
     |       |       |
    V_dc     |       |
     |       |       |
     +-------+-------+
```
```
At DC: Capacitor acts as open circuit
I = 0 through capacitor branch
V_c = V_dc
```

### 4.2 AC Fundamentals

#### Sinusoidal Signals
```
v(t) = V_m × sin(ωt + φ)
```
Where:
- V_m = Peak amplitude
- ω = Angular frequency = 2πf
- φ = Phase angle
- f = Frequency (Hz)

#### RMS Values
```
V_rms = V_m / √2
I_rms = I_m / √2
```

### 4.3 Phasor Representation

#### Complex Number Form:
```
V = V_m ∠ φ = V_m e^(jφ) = V_m (cos φ + j sin φ)
```

#### Impedance (Z)
- **Resistor**: Z_R = R
- **Capacitor**: Z_C = 1/(jωC) = -j/(ωC)
- **Inductor**: Z_L = jωL

**Impedance Triangle**:
```
     Z
    /|
   / | 
  /  | X (Reactance)
 /___|
 R (Resistance)
```
```
Z = R + jX
|Z| = √(R² + X²)
θ = arctan(X/R)
```

### 4.4 AC Circuit Analysis Example

**Circuit**:
```
     +--[R=10Ω]--+--[L=0.1H]--+
     |           |            |
    v_s(t)      [i(t)]       [v_L(t)]
     |           |            |
     +-----------+------------+
```
Where: v_s(t) = 100 sin(377t) V

**Solution**:
```
1. Convert to phasor: V_s = 100∠0° V
2. Calculate impedance:
   Z_R = 10Ω
   Z_L = jωL = j×377×0.1 = j37.7Ω
   Z_total = 10 + j37.7 = 39.1∠75.1° Ω

3. Calculate current:
   I = V_s / Z_total = 100∠0° / 39.1∠75.1° = 2.56∠-75.1° A

4. Convert back to time domain:
   i(t) = 2.56 sin(377t - 75.1°) A
```

### 4.5 Power in AC Circuits

#### Instantaneous Power:
```
p(t) = v(t) × i(t)
```

#### Average Power (Real Power):
```
P = V_rms × I_rms × cos(θ)
```
Where θ = phase difference between voltage and current

#### Reactive Power:
```
Q = V_rms × I_rms × sin(θ)
```

#### Apparent Power:
```
S = V_rms × I_rms = P + jQ
```

#### Power Triangle:
```
     S (VA)
    /|
   / | Q (VAR)
  /__|
 P (W)
```

---

## 5. Frequency Response

### 5.1 Transfer Function

#### Definition:
```
H(ω) = V_out / V_in
```
Usually expressed as: H(jω) = |H(ω)| ∠ φ(ω)

### 5.2 Bode Plots

#### Magnitude Plot:
- **Horizontal axis**: Frequency (log scale)
- **Vertical axis**: Gain in dB = 20 log₁₀|H(ω)|

#### Phase Plot:
- **Horizontal axis**: Frequency (log scale)
- **Vertical axis**: Phase angle in degrees

### 5.3 First-Order Filters

#### Low-Pass Filter:
```
     +--[R]--+--[C]--+
     |       |       |
    V_in     V_out   GND
     |       |       |
     +-------+-------+
```
```
Transfer Function: H(ω) = 1 / (1 + jωRC)
Cutoff Frequency: ω_c = 1/(RC)
```

#### High-Pass Filter:
```
     +--[C]--+--[R]--+
     |       |       |
    V_in     V_out   GND
     |       |       |
     +-------+-------+
```
```
Transfer Function: H(ω) = jωRC / (1 + jωRC)
Cutoff Frequency: ω_c = 1/(RC)
```

### 5.4 Resonance

#### Series RLC Circuit:
```
     +--[R]--+--[L]--+--[C]--+
     |       |       |       |
    V_in     |      V_out    |
     |       |       |       |
     +-------+-------+-------+
```

#### Resonant Frequency:
```
ω₀ = 1 / √(LC)
```

#### Quality Factor:
```
Q = ω₀L / R = 1 / (ω₀CR)
```

#### Bandwidth:
```
BW = ω₀ / Q
```

### 5.5 Filter Types

#### Low-Pass Filter Characteristics:
```
Gain
  ↑
  |──────⎯⎯⎯⎯⎯⎯⎯⎯⎯
  |               ⎯⎯⎯⎯⎯⎯
  |                    ⎯⎯⎯⎯
  +-----------------------→ Frequency
        ω_c
```

#### High-Pass Filter Characteristics:
```
Gain
  ↑
  |                    ⎯⎯⎯⎯
  |               ⎯⎯⎯⎯⎯⎯
  |──────⎯⎯⎯⎯⎯⎯⎯⎯⎯
  +-----------------------→ Frequency
        ω_c
```

#### Band-Pass Filter Characteristics:
```
Gain
  ↑
  |         ⎯⎯⎯⎯⎯⎯⎯
  |      ⎯⎯⎯     ⎯⎯⎯
  |   ⎯⎯⎯         ⎯⎯⎯
  +--------⎯⎯⎯⎯⎯⎯⎯--------→ Frequency
        ω₁  ω₀  ω₂
```

### 5.6 Detailed Example: Low-Pass Filter Design

**Design a low-pass filter with cutoff frequency 1 kHz**:

```
Given: f_c = 1000 Hz
Choose: C = 0.01 μF

Calculate R:
f_c = 1/(2πRC)
R = 1/(2πf_cC) = 1/(2π×1000×10⁻⁸) = 15.9 kΩ

Circuit:
     +--[15.9kΩ]--+--[0.01μF]--+
     |            |            |
    V_in         V_out         GND
     |            |            |
     +------------+------------+
```

**Transfer Function**:
```
H(f) = 1 / (1 + jf/1000)
```

**Bode Plot Calculations**:
```
At f = 100 Hz: |H| ≈ 1 (0 dB)
At f = 1000 Hz: |H| = 1/√2 ≈ 0.707 (-3 dB)
At f = 10 kHz: |H| ≈ 0.1 (-20 dB)
```

---

## Practice Problems

### Problem 1: Basic Circuit Analysis
```
     +--[R1=2Ω]--+--[R2=3Ω]--+
     |           |           |
   12V          [R3=6Ω]     [I=2A]
     |           |           |
     +-----------+-----------+
```
Find all branch currents and node voltages.

### Problem 2: Thevenin Equivalent
Find the Thevenin equivalent between points A and B:
```
     +--[4Ω]--+--[6Ω]--A
     |        |        |
   20V       [3Ω]      |
     |        |        |
     +--------+--------B
```

### Problem 3: AC Analysis
For a series RLC circuit with R=10Ω, L=50mH, C=100μF, connected to 120V, 60Hz source:
- Calculate impedance
- Find current
- Calculate power factor
- Determine resonant frequency

## Conclusion

This comprehensive course material covers the fundamental concepts of electrical circuit analysis from basic DC circuits to advanced AC frequency response. Each section builds upon the previous one, providing a solid foundation for understanding and analyzing electrical circuits in both time and frequency domains.

Remember to practice with real circuits and simulation software to reinforce these theoretical concepts!
