# Electronic Components
## Active and Passive Components

## Table of Contents
1. [Passive Components](#1-passive-components)
2. [Active Components](#2-active-components)
3. [Operational Amplifiers & ICs](#3-operational-amplifiers--ics)
4. [Sensors & Actuators](#4-sensors--actuators)

---

## 1. Passive Components

### 1.1 Resistors

#### Definition and Function
**Resistors** are passive components that oppose the flow of electric current, converting electrical energy into heat.

```
Circuit Symbol:
┌───╂───┐
     R
└───────┘
```

#### Ohm's Law Relationship
```
V = I × R
Where:
V = Voltage across resistor (Volts)
I = Current through resistor (Amps)
R = Resistance (Ohms, Ω)
```

#### Power Dissipation
```
P = I² × R = V² / R = V × I
```

#### Types of Resistors

**Fixed Resistors:**
- **Carbon Composition**: Inexpensive, high noise
- **Carbon Film**: Better tolerance than carbon comp
- **Metal Film**: High precision, low noise
- **Wirewound**: High power handling

**Variable Resistors:**
```
    1    2
    ┌───╂───┐
    │   │   │
    3   3   3
```
- **Potentiometers**: 3-terminal variable resistors
- **Rheostats**: 2-terminal variable resistors

#### Color Code System
```
Band 1: First digit
Band 2: Second digit  
Band 3: Multiplier
Band 4: Tolerance
```

**Example: 4.7kΩ resistor with 5% tolerance**
```
Yellow (4) - Violet (7) - Red (×100) - Gold (5%)
Calculation: 47 × 100 = 4700Ω = 4.7kΩ
```

#### Resistor Networks
- **Series**: R_total = R₁ + R₂ + R₃ + ...
- **Parallel**: 1/R_total = 1/R₁ + 1/R₂ + 1/R₃ + ...

**Example Calculation:**
```
Series: 1kΩ + 2.2kΩ = 3.2kΩ
Parallel: (1kΩ × 2.2kΩ)/(1kΩ + 2.2kΩ) = 687.5Ω
```

### 1.2 Capacitors

#### Definition and Function
**Capacitors** store electrical energy in an electric field and oppose changes in voltage.

```
Circuit Symbol:
┌───||───┐
     C
└────────┘
```

#### Fundamental Equation
```
Q = C × V
Where:
Q = Charge stored (Coulombs)
C = Capacitance (Farads)
V = Voltage (Volts)

I = C × dV/dt
```

#### Energy Storage
```
E = ½ × C × V²
```

#### Types of Capacitors

**Electrolytic Capacitors:**
- Polarized (+ and - terminals)
- High capacitance values (μF to mF)
- Used for power supply filtering

**Ceramic Capacitors:**
- Non-polarized
- Small values (pF to μF)
- Stable, low cost

**Film Capacitors:**
- Polyester, polypropylene
- Good for audio circuits
- Stable temperature characteristics

#### Capacitor Networks
- **Series**: 1/C_total = 1/C₁ + 1/C₂ + 1/C₃ + ...
- **Parallel**: C_total = C₁ + C₂ + C₃ + ...

**Example:**
```
Two 100μF capacitors in series:
C_total = (100 × 100)/(100 + 100) = 50μF

Two 100μF capacitors in parallel:
C_total = 100 + 100 = 200μF
```

#### RC Time Constant
```
τ = R × C
Where τ is the time constant in seconds

Charging: V_c(t) = V_s × (1 - e^(-t/τ))
Discharging: V_c(t) = V_0 × e^(-t/τ)
```

**Practical Example:**
```
R = 10kΩ, C = 100μF
τ = 10,000 × 0.0001 = 1 second

After 1 second: Capacitor charges to 63.2% of supply voltage
After 5 seconds: Capacitor charges to 99.3% of supply voltage
```

### 1.3 Inductors

#### Definition and Function
**Inductors** store energy in a magnetic field and oppose changes in current.

```
Circuit Symbol:
┌───͡───┐
     L
└──────┘
```

#### Fundamental Equations
```
V = L × di/dt
Where:
V = Voltage across inductor (Volts)
L = Inductance (Henries)
di/dt = Rate of change of current (A/s)

Energy: E = ½ × L × I²
```

#### Types of Inductors

**Air Core Inductors:**
- No magnetic core
- Low inductance, high frequency
- No core losses

**Ferrite Core Inductors:**
- High permeability
- Medium to high inductance
- Used in power supplies

**Iron Core Inductors:**
- Very high inductance
- Low frequency applications
- Subject to saturation

#### RL Time Constant
```
τ = L / R
Current buildup: I(t) = I_max × (1 - e^(-t/τ))
Current decay: I(t) = I_0 × e^(-t/τ)
```

**Example:**
```
L = 100mH, R = 100Ω
τ = 0.1 / 100 = 0.001 seconds = 1ms
```

#### Inductor Networks
- **Series**: L_total = L₁ + L₂ + L₃ + ...
- **Parallel**: 1/L_total = 1/L₁ + 1/L₂ + 1/L₃ + ...

---

## 2. Active Components

### 2.1 Diodes

#### Definition and Function
**Diodes** are semiconductor devices that allow current to flow in one direction only.

```
Circuit Symbol:
    A →|→ K
    Anode   Cathode
```

#### Ideal Diode Characteristics
- **Forward biased**: Short circuit (V > 0)
- **Reverse biased**: Open circuit (V < 0)

#### Real Diode Characteristics
```
Forward voltage drop:
- Silicon: ~0.7V
- Germanium: ~0.3V
- Schottky: ~0.2V
```

#### Diode Equation (Shockley Equation)
```
I = I_s × (e^(V/(nV_T)) - 1)
Where:
I_s = Reverse saturation current
V_T = Thermal voltage ≈ 25mV at room temperature
n = Ideality factor (1-2)
```

#### Types of Diodes

**Rectifier Diodes:**
- Power conversion
- High current capability

**Zener Diodes:**
```
Symbol: →|↗ (with bars)
```
- Voltage regulation
- Operate in reverse breakdown

**LED (Light Emitting Diode):**
```
Symbol: →|→ (with arrows)
```
- Emit light when forward biased
- Different colors = different materials

**Schottky Diodes:**
- Low forward voltage
- Fast switching

#### Diode Applications

**Half-Wave Rectifier:**
```
Input: AC sine wave
Output: Positive half-cycles only
```

**Full-Wave Bridge Rectifier:**
```
    AC Input
     ↓
┌─D1─┐ ┌─D3─┐
│    │ │    │
AC1  │ AC2  │ DC+
│    │ │    │
└─D2─┘ └─D4─┘
     │     │
     GND   DC-
```

**Voltage Regulation with Zener:**
```
     +--[R]--+--[Zener]--+
     |       |           |
    V_in    V_out        GND
     |       |           |
     +-------+-----------+

V_out remains constant at V_zener when V_in > V_zener
```

### 2.2 Transistors

#### Bipolar Junction Transistors (BJT)

**NPN Transistor:**
```
Symbol:
     Collector (C)
        │
        │
        ○
        │
     Base (B)
        │
        │
        ○
        │
     Emitter (E)
```

**PNP Transistor:**
```
Symbol: Same as NPN but arrow points inward
```

**Operating Regions:**
- **Cutoff**: No current flow (switch OFF)
- **Active**: Linear amplification
- **Saturation**: Full current flow (switch ON)

**Current Relationships:**
```
I_E = I_C + I_B
I_C = β × I_B  (where β = current gain)
```

**Common Emitter Amplifier:**
```
     +Vcc
      │
     [Rc]
      │
      C←B→[Rb]
      │    │
      E   V_in
      │    │
     [Re]  GND
      │
     GND
```

**Voltage Gain**: A_v ≈ -Rc / Re

#### Field Effect Transistors (FET)

**MOSFET Symbols:**
```
N-Channel:        P-Channel:
     Drain (D)         Source (S)
        │                │
        │                │
        ○                ○
        │                │
     Gate (G)         Gate (G)
        │                │
        │                │
        ○                ○
        │                │
     Source (S)        Drain (D)
```

**MOSFET Operating Regions:**
- **Cutoff**: V_GS < V_th
- **Triode/Linear**: V_DS < V_GS - V_th
- **Saturation**: V_DS ≥ V_GS - V_th

**Drain Current in Saturation:**
```
I_D = ½ × μ × C_ox × (W/L) × (V_GS - V_th)²
```

**Common Source Amplifier:**
```
     +Vdd
      │
     [Rd]
      │
      D←G
      │  │
      S  V_in
      │  │
     [Rs] GND
      │
     GND
```

### 2.3 Transistor Configurations

#### BJT Configurations

**Common Emitter:**
- Voltage and current gain
- Phase inversion
- Moderate input/output impedance

**Common Collector (Emitter Follower):**
- Voltage gain ≈ 1
- High input impedance
- Low output impedance

**Common Base:**
- Current gain ≈ 1
- High voltage gain
- Low input impedance

#### MOSFET Configurations

**Common Source:** Similar to common emitter
**Common Drain (Source Follower):** Similar to emitter follower
**Common Gate:** Similar to common base

---

## 3. Operational Amplifiers & ICs

### 3.1 Ideal Op-Amp Characteristics

#### Golden Rules:
1. **Infinite Input Impedance**: No current flows into inputs
2. **Infinite Gain**: A_v → ∞
3. **Zero Output Impedance**: Can drive any load
4. **Infinite Bandwidth**: Works at all frequencies
5. **Virtual Short**: V⁺ ≈ V⁻ when in negative feedback

#### Op-Amp Symbol:
```
     V⁺ ──┐
          │
          ├─── V_out
          │
     V⁻ ──┘
```

### 3.2 Basic Op-Amp Circuits

#### Inverting Amplifier
```
     ┌──[Rf]──┐
     │        │
V_in─┴─[R1]──┴─ V_out
           │
          GND
```

**Gain**: A_v = -Rf / R1

**Example**: R1 = 10kΩ, Rf = 100kΩ → Gain = -10

#### Non-Inverting Amplifier
```
     V_in ─┐
           ├──┐
          GND │
              ├── V_out
     ┌──[Rf]──┘
     │
    [R1]
     │
    GND
```

**Gain**: A_v = 1 + (Rf / R1)

**Example**: R1 = 10kΩ, Rf = 90kΩ → Gain = +10

#### Voltage Follower (Buffer)
```
     V_in ─┐
           ├── V_out
          GND
```

**Gain**: A_v = 1
**Purpose**: High input impedance, low output impedance

### 3.3 Advanced Op-Amp Circuits

#### Summing Amplifier
```
     V1 ─[R1]─┐
     V2 ─[R2]─┼─┐
     V3 ─[R3]─┘ │
               ├── V_out
          ┌──[Rf]──┘
          │
         GND
```

**Output**: V_out = -Rf × (V1/R1 + V2/R2 + V3/R3)

#### Difference Amplifier
```
     V1 ─[R1]─┐
              ├── V_out
     V2 ─[R2]─┘
          │
         [R3]
          │
         GND
```

**Output**: V_out = (R2/R1) × (V2 - V1)

#### Integrator
```
     ┌──[C]──┐
     │       │
V_in─┴─[R]──┴─ V_out
          │
         GND
```

**Output**: V_out = -1/(RC) × ∫V_in dt

#### Differentiator
```
     ┌──[R]──┐
     │       │
V_in─┴─[C]──┴─ V_out
          │
         GND
```

**Output**: V_out = -RC × dV_in/dt

### 3.4 Real Op-Amp Limitations

#### Non-Ideal Characteristics
- **Input Offset Voltage**: Typically 1-5mV
- **Input Bias Current**: Typically 10nA-1μA
- **Slew Rate**: How fast output can change (V/μs)
- **Gain-Bandwidth Product**: Frequency where gain drops to 1

#### Common Op-Amp Types
- **741**: General purpose, low cost
- **LM358**: Dual op-amp, single supply
- **TL072**: Low noise, JFET input
- **LM324**: Quad op-amp, single supply
- **OPA2134**: High performance, audio

---

## 4. Sensors & Actuators

### 4.1 Sensor Principles

#### What is a Sensor?
A device that detects physical quantities and converts them into electrical signals.

#### Sensor Classification
- **Active vs Passive**: Does it need external power?
- **Analog vs Digital**: Output signal type
- **Contact vs Non-contact**: Physical interaction

### 4.2 Common Sensors

#### Temperature Sensors

**Thermistor:**
- Resistance changes with temperature
- NTC (Negative Temperature Coefficient): R decreases with T
- PTC (Positive Temperature Coefficient): R increases with T

**Circuit:**
```
     +Vcc
      │
     [R_fixed]
      │
      ├── V_out
     [Thermistor]
      │
     GND
```

**LM35 Temperature Sensor:**
- Output: 10mV/°C
- Range: -55°C to +150°C
- Easy to interface with microcontroller

#### Light Sensors

**LDR (Light Dependent Resistor):**
- Resistance decreases with light intensity
- Typical dark resistance: 1MΩ
- Typical light resistance: 1kΩ

**Photodiode:**
- Operates in reverse bias
- Current proportional to light intensity
- Fast response

**Phototransistor:**
- Similar to photodiode but with amplification
- Higher sensitivity

#### Position and Motion Sensors

**Potentiometer:**
- Rotary or linear
- Voltage divider configuration

**Accelerometer:**
- Measures acceleration (including gravity)
- MEMS technology
- 3-axis capability

**Gyroscope:**
- Measures angular velocity
- Used for orientation

#### Proximity Sensors

**IR Sensor:**
- IR LED + phototransistor
- Reflectance-based detection

**Ultrasonic Sensor:**
- HC-SR04 module
- Measures distance using sound waves
- Range: 2cm - 400cm

### 4.3 Actuators

#### Definition
Devices that convert electrical signals into physical action.

#### Types of Actuators

**DC Motors:**
```
Electrical Input → Magnetic Field → Mechanical Rotation
```

**Motor Driver Circuit (H-Bridge):**
```
     +V_motor
      │
 Q1   Q3
┌─┴─┐ ┌─┴─┐
│   │ │   │
M   M M   M
│   │ │   │
└─┬─┘ └─┬─┘
 Q2   Q4
  │     │
 GND   GND
```

**Control:**
- Q1+Q4 ON: Motor spins clockwise
- Q2+Q3 ON: Motor spins counterclockwise
- PWM for speed control

**Servo Motors:**
- Position control
- Pulse width modulation (1-2ms pulse)
- 0° to 180° rotation

**Stepper Motors:**
- Precise position control
- Digital steps (1.8° per step common)
- Requires driver circuit

**Solenoids:**
- Linear motion
- Electromagnetic coil + plunger
- On/off control

**Relays:**
- Electromechanical switch
- Coil voltage vs. contact rating
- Isolation between control and load

### 4.4 Sensor Signal Conditioning

#### Amplification
- **Instrumentation Amplifier**: High CMRR, differential signals
- **Programmable Gain Amplifier**: Adjustable gain

#### Filtering
- **Low-pass**: Remove high-frequency noise
- **High-pass**: Remove DC offset
- **Band-pass**: Select frequency range of interest

#### Analog-to-Digital Conversion
- **Successive Approximation (SAR)**: Medium speed, good accuracy
- **Delta-Sigma (Σ-Δ)**: High resolution, slow
- **Flash**: Very fast, low resolution

### 4.5 Practical Interface Examples

#### Temperature Monitoring System
```
LM35 → Op-Amp (gain 10) → ADC → Microcontroller → Display
```

#### Light-Activated Switch
```
LDR → Comparator → Transistor Switch → Relay → Lamp
```

#### Motor Speed Control
```
Potentiometer → PWM Generator → H-Bridge → DC Motor
```

#### Smart Home Example
```
Temperature → Microcontroller → Relay → Heater
Light Sensor → Microcontroller → Transistor → LED Strip
Motion Sensor → Microcontroller → Buzzer
```

---

## Practice Problems

### Problem 1: Resistor Network Analysis
```
Calculate equivalent resistance between A and B:
     A──[1kΩ]──[2kΩ]──[3kΩ]──B
```

### Problem 2: Diode Circuit
```
For the circuit:
     +12V──[1kΩ]──|→|── GND
Calculate current if diode is silicon (V_f = 0.7V)
```

### Problem 3: Transistor Amplifier
```
Common emitter amplifier:
V_cc = 12V, R_c = 2.2kΩ, R_e = 470Ω, β = 100
Calculate voltage gain and input impedance
```

### Problem 4: Op-Amp Design
```
Design an inverting amplifier with gain of -25
using standard resistor values
```

### Problem 5: Sensor Interface
```
Design a circuit to interface an LDR (1kΩ in light, 1MΩ in dark)
to turn on an LED when it gets dark
```

## Conclusion

This comprehensive course material covers both passive and active electronic components, from basic resistors to complex sensor systems. Understanding these fundamental building blocks is essential for designing and analyzing electronic circuits in real-world applications.

Each component type has specific characteristics, applications, and limitations that must be considered during circuit design. The practical examples and interface circuits provide a foundation for building complete electronic systems.

Remember: Always consider datasheet specifications, power requirements, and real-world non-idealities when working with electronic components!
