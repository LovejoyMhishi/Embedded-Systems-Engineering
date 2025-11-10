<h1 align="center">Control Systems</h1>

## Table of Contents
1. [Feedback Theory](#1-feedback-theory)
2. [Transfer Functions](#2-transfer-functions)
3. [PID Control](#3-pid-control)
4. [Sensors & Actuators (Control Context)](#4-sensors--actuators-control-context)

---

## 1. Feedback Theory

### 1.1 Introduction to Control Systems

#### What is a Control System?
A system that manages, commands, directs, or regulates the behavior of other devices or systems to achieve desired performance.

#### Basic Block Diagram
```
     ┌─────────┐    ┌─────────┐    ┌─────────┐
R(s)─┤         │    │         │    │         │
    →│Compare  ├───→│Controller├───→│ Plant   ├───→ C(s)
     │         │    │         │    │         │
     └─────────┘    └─────────┘    └─────────┘
          ↑                             │
          │                             │
          └─────── Feedback Path ───────┘
```

**Variables:**
- **R(s)**: Reference input (desired output)
- **C(s)**: Controlled output
- **E(s)**: Error signal = R(s) - C(s)

#### Types of Control Systems

**Open-Loop Control:**
```
Input → Controller → Plant → Output
```
- No feedback
- Simple, inexpensive
- Sensitive to disturbances
- Examples: Toaster, washing machine timer

**Closed-Loop Control:**
```
Input → Compare → Controller → Plant → Output
                 ↑                      │
                 └─── Feedback ─────────┘
```
- Uses feedback
- Complex, expensive
- Reduces sensitivity to disturbances
- Examples: Cruise control, thermostat

### 1.2 Feedback System Components

#### Standard Feedback System
```
     ┌─────────┐         ┌─────────┐
R(s)─┤         │    U(s) │         │
    →│Compare  ├───┐ ┌──→│   G(s)  ├───→ C(s)
     │         │   │ │   │         │
     └─────────┘   │ │   └─────────┘
          ↑        │ │         │
          │        │ │         │
          │        └─┼─────────┘
          │          │
          └──────────┘
               H(s)
```

**Components:**
- **G(s)**: Forward path transfer function (Plant + Controller)
- **H(s)**: Feedback path transfer function (Sensor)
- **U(s)**: Control signal
- **E(s)**: Error signal = R(s) - H(s)C(s)

#### Closed-Loop Transfer Function
```
C(s)     G(s)
---- = ----------
R(s)   1 + G(s)H(s)
```

### 1.3 Benefits of Feedback

#### Disturbance Rejection
```
     ┌─────────┐    ┌─────────┐
R(s)─┤Compare  ├───→│Controller├──┐
     └─────────┘    └─────────┘  │
                                │
     ┌─────────┐    ┌─────────┐  │  ┌─────────┐
D(s)─┤         │    │         │  │  │         │
    →│Disturbance├─→│  Plant  ├─┼─→│ Output  ├─→ C(s)
     │         │    │         │    │         │
     └─────────┘    └─────────┘    └─────────┘
                                │
                                │
                                └─── Feedback ─┘
```

**Output due to disturbance:**
```
C(s)          G_plant(s)
---- = ------------------------
D(s)   1 + G_controller(s)G_plant(s)H(s)
```

#### Sensitivity Reduction
**Sensitivity Function:**
```
         ΔT/T         dT/T
S_H^T = ------- ≈ ---------
         ΔH/H        dH/H

For closed-loop: S_H^T = 1 / (1 + G(s)H(s))
```

**Key Insight:** High loop gain reduces sensitivity to parameter variations.

#### Other Benefits:
- **Improved stability** (when properly designed)
- **Reduced nonlinearity effects**
- **Bandwidth extension**
- **Noise reduction** (in certain frequency ranges)

### 1.4 Stability Analysis

#### Routh-Hurwitz Criterion

**Characteristic Equation:**
```
1 + G(s)H(s) = 0
a_n sⁿ + a_{n-1} sⁿ⁻¹ + ... + a_1 s + a_0 = 0
```

**Routh Array:**
```
sⁿ   | a_n     a_{n-2}   a_{n-4}   ...
sⁿ⁻¹ | a_{n-1} a_{n-3}   a_{n-5}   ...
sⁿ⁻² | b_1     b_2       b_3       ...
sⁿ⁻³ | c_1     c_2       c_3       ...
...  | ...     ...       ...       ...
s⁰   | ...
```

**Where:**
```
b_1 = (a_{n-1}a_{n-2} - a_na_{n-3}) / a_{n-1}
b_2 = (a_{n-1}a_{n-4} - a_na_{n-5}) / a_{n-1}
c_1 = (b_1a_{n-3} - a_{n-1}b_2) / b_1
```

**Stability Criterion:** All elements in first column must be positive.

#### Example: Third-Order System
```
Characteristic equation: s³ + 4s² + 6s + 4 = 0

Routh array:
s³ | 1   6
s² | 4   4
s¹ | (4×6 - 1×4)/4 = 5
s⁰ | 4

All positive → System is stable
```

### 1.5 Steady-State Error Analysis

#### Error Constants

**Position Error Constant (K_p):**
```
K_p = lim G(s)H(s)
      s→0

For step input: e_ss = 1 / (1 + K_p)
```

**Velocity Error Constant (K_v):**
```
K_v = lim s G(s)H(s)
      s→0

For ramp input: e_ss = 1 / K_v
```

**Acceleration Error Constant (K_a):**
```
K_a = lim s² G(s)H(s)
      s→0

For parabola input: e_ss = 1 / K_a
```

#### System Type and Steady-State Error

| System Type | Step Input | Ramp Input | Parabola Input |
|-------------|------------|------------|----------------|
| Type 0      | 1/(1+K_p)  | ∞          | ∞              |
| Type 1      | 0          | 1/K_v      | ∞              |
| Type 2      | 0          | 0          | 1/K_a          |

**Example:**
```
G(s)H(s) = K / [s(s+2)]

Type 1 system (one integrator)
K_v = lim s × K/[s(s+2)] = K/2
s→0

For ramp input: e_ss = 1/K_v = 2/K
```

---

## 2. Transfer Functions

### 2.1 Laplace Transform Fundamentals

#### Definition
```
F(s) = L{f(t)} = ∫ f(t) e^{-st} dt
                0→∞
```

#### Common Laplace Transforms

| Time Domain | Laplace Domain |
|-------------|----------------|
| δ(t)        | 1              |
| u(t)        | 1/s            |
| t           | 1/s²           |
| e^{-at}     | 1/(s+a)        |
| sin(ωt)     | ω/(s²+ω²)      |
| cos(ωt)     | s/(s²+ω²)      |

#### Properties
- **Linearity:** L{af(t) + bg(t)} = aF(s) + bG(s)
- **Differentiation:** L{f'(t)} = sF(s) - f(0)
- **Integration:** L{∫f(τ)dτ} = F(s)/s
- **Final Value Theorem:** lim f(t) = lim sF(s)
                         t→∞       s→0
- **Initial Value Theorem:** lim f(t) = lim sF(s)
                            t→0+      s→∞

### 2.2 Transfer Function Definition

#### What is a Transfer Function?
The ratio of the Laplace transform of the output to the Laplace transform of the input, with zero initial conditions.

```
       Output(s)   C(s)
G(s) = --------- = ----
       Input(s)    R(s)
```

#### Mechanical System Example: Mass-Spring-Damper
```
        ┌───┐
        │ m │
        └─┬─┘
          │
    ┌─────┴─────┐
   [k]   [b]   F(t)
    │     │     │
   Fixed Wall  Input
```

**Differential Equation:**
```
m d²x/dt² + b dx/dt + kx = F(t)
```

**Transfer Function:**
```
      X(s)         1
G(s) = ---- = ------------
      F(s)    ms² + bs + k
```

### 2.3 Block Diagram Algebra

#### Basic Rules

**Series Connection:**
```
     ┌───┐   ┌───┐
R(s)→│G1 ├──→│G2 ├→ C(s)
     └───┘   └───┘

Equivalent: G(s) = G1(s)G2(s)
```

**Parallel Connection:**
```
     ┌───┐
    →│G1 ├─┐
     └───┘ │ ⊕
           ├→ C(s)
     ┌───┐ │
    →│G2 ├─┘
     └───┘

Equivalent: G(s) = G1(s) + G2(s)
```

**Feedback Connection:**
```
     ┌───┐
    →│ G ├─┐
     └───┘ │
           ├→ C(s)
        ┌──┴──┐
        │  H  │
        └──┬──┘
           │

Equivalent: G_cl(s) = G(s) / [1 + G(s)H(s)]
```

#### Reduction Techniques

**Moving Summing Junction:**
```
Before:    After:
  ┌─┐        ┌─┐
→⊕│ ├→ G →   → G →⊕│ ├→
 ↑│ │              ↑│ │
 X│ │             X/G│ │
  └─┘               └─┘
```

**Moving Pickoff Point:**
```
Before:    After:
  → G →⊕→     →⊕→ G →
       │          │
       │         1/G
       │          │
      ...        ...
```

### 2.4 Signal Flow Graphs

#### Basic Elements
- **Node:** Represents variable
- **Branch:** Represents transfer function
- **Source:** Input node (only outgoing branches)
- **Sink:** Output node (only incoming branches)

#### Mason's Gain Formula
```
       ∑ P_k Δ_k
T = --------------
          Δ

Where:
P_k = Path gain of k-th forward path
Δ = 1 - ∑(all individual loop gains)
     + ∑(gain products of all non-touching loop pairs)
     - ∑(gain products of all non-touching loop triplets) + ...
Δ_k = Δ with loops touching k-th forward path removed
```

#### Example: Two-Path System
```
     ┌───┐   ┌───┐
R →→│G1 ├→│G2 ├→ C
     └───┘   └───┘
       ↑       ↑
       │       │
      ┌┴┐     ┌┴┐
      │H1│    │H2│
      └┬┘     └┬┘
       │       │
       └───┬───┘
```

**Forward Paths:**
- P₁ = G1G2
- P₂ = G3

**Loops:**
- L₁ = -G1H1
- L₂ = -G2H2
- L₃ = -G1G2H1H2

**Apply Mason's Rule:**
```
Δ = 1 - (L₁ + L₂ + L₃) + (L₁L₂)  [L₁ and L₂ don't touch]
T = (P₁Δ₁ + P₂Δ₂) / Δ
```

### 2.5 System Response Analysis

#### First-Order System
```
       K
G(s) = ---
       τs + 1
```

**Step Response:**
```
c(t) = K(1 - e^{-t/τ})
```

**Characteristics:**
- **Time Constant (τ):** Time to reach 63.2% of final value
- **Rise Time (t_r):** Time from 10% to 90% ≈ 2.2τ
- **Settling Time (t_s):** Time to within 2% of final value ≈ 4τ

#### Second-Order System
```
          ω_n²
G(s) = -----------------
       s² + 2ζω_n s + ω_n²
```

**Step Response Characteristics:**
- **Natural Frequency (ω_n):** Undamped oscillation frequency
- **Damping Ratio (ζ):** Determines response type
- **Overshoot (%OS):** = 100 × e^{-ζπ/√(1-ζ²)}

**Response Types:**
- **ζ = 0:** Undamped (continuous oscillation)
- **0 < ζ < 1:** Underdamped (oscillatory)
- **ζ = 1:** Critically damped (fastest without overshoot)
- **ζ > 1:** Overdamped (slow, no overshoot)

**Performance Measures:**
- **Peak Time (t_p):** = π / (ω_n√(1-ζ²))
- **Rise Time (t_r):** ≈ (1.8) / ω_n (for 0.5 < ζ < 1.5)
- **Settling Time (t_s):** ≈ 4 / (ζω_n) (2% criterion)

### 2.6 Frequency Response Analysis

#### Bode Plots

**Magnitude Plot:**
- Horizontal axis: log(ω)
- Vertical axis: 20log₁₀|G(jω)| (dB)

**Phase Plot:**
- Horizontal axis: log(ω)
- Vertical axis: ∠G(jω) (degrees)

#### Straight-Line Approximations

**Simple Pole:**
```
      1
G(s) = ---
      s + a

Magnitude: 0 dB for ω < a, -20 dB/dec for ω > a
Phase: 0° for ω < a/10, -45° at ω = a, -90° for ω > 10a
```

**Integrator:**
```
      1
G(s) = -
      s

Magnitude: -20 dB/dec slope, 0 dB at ω = 1
Phase: Constant -90°
```

**Second-Order Term:**
```
          ω_n²
G(s) = -----------------
       s² + 2ζω_n s + ω_n²

Magnitude: 0 dB for ω < ω_n, -40 dB/dec for ω > ω_n
Peak at resonance if ζ < 0.707
```

#### Gain and Phase Margins

**Gain Margin (GM):**
```
GM = 1 / |G(jω_φ)| where ∠G(jω_φ) = -180°
In dB: GM(dB) = -20log₁₀|G(jω_φ)|
```

**Phase Margin (PM):**
```
PM = 180° + ∠G(jω_c) where |G(jω_c)| = 1
```

**Stability Criteria:**
- GM > 0 dB and PM > 0° for stability
- GM > 6 dB and PM > 30° for good relative stability

---

## 3. PID Control

### 3.1 PID Controller Structure

#### Continuous-Time PID
```
                 ┌────────────┐
                 │   1        │
u(t) = K_p e(t) +│K_i ∫e(t)dt│+ K_d de(t)/dt
                 │            │
                 └────────────┘
```

**Transfer Function:**
```
G_c(s) = K_p + K_i/s + K_d s
```

**Alternative Form:**
```
G_c(s) = K_p [1 + 1/(T_i s) + T_d s]
Where:
T_i = K_p/K_i (integral time)
T_d = K_d/K_p (derivative time)
```

### 3.2 PID Components Analysis

#### Proportional Term (P)
```
u(t) = K_p e(t)
```

**Effects:**
- **Reduces rise time**
- **Reduces steady-state error**
- **Can cause overshoot**
- **May lead to instability if too high**

#### Integral Term (I)
```
u(t) = K_i ∫e(t)dt
```

**Effects:**
- **Eliminates steady-state error**
- **Increases overshoot**
- **Worsens transient response**
- **Can cause windup**

#### Derivative Term (D)
```
u(t) = K_d de(t)/dt
```

**Effects:**
- **Reduces overshoot**
- **Improves stability**
- **Sensitive to noise**
- **No effect on steady-state error**

### 3.3 PID Tuning Methods

#### Ziegler-Nichols Open-Loop Method

**Step 1:** Obtain process reaction curve
```
Apply step input, measure:
L = dead time (time delay)
T = time constant
K = process gain
```

**Step 2:** Apply tuning rules

| Controller | K_p       | T_i    | T_d     |
|------------|-----------|--------|---------|
| P          | T/(K·L)   | -      | -       |
| PI         | 0.9T/(K·L)| 3.33L  | -       |
| PID        | 1.2T/(K·L)| 2.0L   | 0.5L    |

#### Ziegler-Nichols Closed-Loop Method

**Step 1:** Find ultimate gain (K_u) and period (P_u)
- Use only proportional control
- Increase K_p until sustained oscillations occur
- K_u = critical gain, P_u = oscillation period

**Step 2:** Apply tuning rules

| Controller | K_p      | T_i     | T_d     |
|------------|----------|---------|---------|
| P          | 0.5K_u   | -       | -       |
| PI         | 0.45K_u  | P_u/1.2 | -       |
| PID        | 0.6K_u   | P_u/2   | P_u/8   |

#### Cohen-Coon Method
More refined version of Ziegler-Nichols, better for processes with significant dead time.

### 3.4 Practical PID Implementation

#### Derivative Filtering
**Problem:** Pure derivative amplifies high-frequency noise
**Solution:** Use filtered derivative
```
         s
s → ----------
     1 + sT_f

Where T_f = N/K_d, typically N = 5-20
```

#### Anti-Windup

**Problem:** Integral windup during saturation
**Solution:** Implement anti-windup schemes

**Back-Calculation:**
```
     ┌─────────┐
e(t)→│   PID   ├─→ u(t) ──┐
     └─────────┘         │
                      ┌──┴──┐
                      │ Sat │→ u_actual(t)
                      └──┬──┘
                         │
                ┌────────┴────────┐
                │1/T_t (u - u_act)│
                └────────┬────────┘
                         │
                ┌───────┴───────┐
                │    Integrator │
                └───────┬───────┘
                        │
```

#### Discrete PID Implementation

**Position Form:**
```
u[k] = K_p e[k] + K_i T_s ∑ e[j] + K_d (e[k] - e[k-1])/T_s
                          j=0→k
```

**Velocity Form:**
```
Δu[k] = K_p (e[k] - e[k-1]) + K_i T_s e[k] + K_d (e[k] - 2e[k-1] + e[k-2])/T_s
```

**Advantages of Velocity Form:**
- Automatic anti-windup
- Bumpless transfer
- Safer implementation

### 3.5 Advanced PID Techniques

#### Gain Scheduling
Adjust PID parameters based on operating conditions
```
         ┌─────────────┐
y_ref ─→│             ├─→ u
         │ PID with    │
y ─────→│ Gain        │
         │ Scheduling  │
θ ─────→│             │
         └─────────────┘
```

#### Fuzzy PID
Use fuzzy logic to adapt PID parameters based on error and error derivative.

#### Auto-Tuning
- Relay feedback auto-tuning
- Pattern recognition methods
- Model-based auto-tuning

### 3.6 PID Applications

#### Temperature Control
```
         ┌─────────┐    ┌─────────┐
T_ref ─→│   PID   ├─→│ Heater  ├─→ Temperature
         │Controller│   │         │
T_actual ─┤         │   └─────────┘
         └─────────┘
```

**Typical Settings:**
- Slow process → Use PI control
- Large thermal mass → Higher integral time
- Noise from sensors → Limit derivative action

#### Motor Speed Control
```
         ┌─────────┐    ┌─────────┐    ┌─────────┐
ω_ref ─→│   PID   ├─→│Power Amp├─→│  Motor   ├─→ Speed
         │Controller│   │         │   │         │
ω_actual ─┤         │   └─────────┘   └─────────┘
         └─────────┘
```

**Typical Settings:**
- Fast process → Can use full PID
- Load disturbances → Important integral action
- Mechanical resonance → Careful with derivative

---

## 4. Sensors & Actuators (Control Context)

### 4.1 Control System Sensors

#### Position Sensors

**Potentiometers:**
```
     V_ref
      │
     [ ]
      │
      ├─→ V_out (position)
      │
     [ ]
      │
     GND
```
- **Range:** ±60° to multi-turn
- **Accuracy:** 0.1-1%
- **Applications:** Rotary position, linear position

**Encoders:**
- **Incremental:** Pulses for relative position
- **Absolute:** Unique code for each position
- **Resolution:** Up to 24 bits
- **Applications:** Motor position, CNC machines

**LVDT (Linear Variable Differential Transformer):**
```
      Primary
    ┌─────────┐
    │  Coil   │
    └─────────┘
         │
    ┌─── Core ───┐
    │            │
    └─────────┘
     Sec1   Sec2
```
- **Range:** mm to meters
- **Accuracy:** 0.1-0.5%
- **Applications:** Precision linear displacement

#### Velocity Sensors

**Tachogenerators:**
- DC output proportional to speed
- **Range:** 0-10,000 RPM
- **Linearity:** 0.1-1%
- **Applications:** Motor speed feedback

**Encoder-based Velocity:**
- Measure pulse frequency or period
- **Methods:** M/T method, frequency method
- **Applications:** High-precision speed control

#### Force/Torque Sensors

**Strain Gauge Load Cells:**
```
     ┌─────────┐
     │  Strain │← Force
     │ Gauges  │
     └─────────┘
        │ │ │
    Wheatstone Bridge
```
- **Range:** grams to tons
- **Accuracy:** 0.03-0.5%
- **Applications:** Weighing, force control

**Torque Sensors:**
- **Reaction torque:** Measure stationary reaction
- **Rotary torque:** Slip rings or wireless
- **Applications:** Motor torque control, dynamometers

### 4.2 Control System Actuators

#### Electric Actuators

**DC Motors:**
```
Electrical: V, I → Mechanical: τ, ω
τ = K_t I
V = K_e ω + I R
```

**Brushless DC Motors:**
- Electronic commutation
- Higher efficiency
- Longer lifespan
- Requires controller

**Stepper Motors:**
- Digital positioning
- Open-loop control possible
- High holding torque
- Can lose steps under load

**Servo Motors:**
- Closed-loop position control
- Integrated encoder
- High acceleration
- Precision applications

#### Hydraulic Actuators

**Hydraulic Cylinder:**
```
     ┌─────────┐
P₁ → │         │ ← P₂
     │ Piston  │
     │         │
     └─────────┘
        │
        → Force
```

**Characteristics:**
- **High force density**
- **Stiff response**
- **Complex infrastructure**
- **Applications:** Heavy machinery, aircraft

#### Pneumatic Actuators

**Pneumatic Cylinder:**
Similar to hydraulic but using compressed air

**Characteristics:**
- **Lower force than hydraulic**
- **Compliant response**
- **Clean operation**
- **Applications:** Packaging, robotics

### 4.3 Signal Conditioning

#### Amplification

**Instrumentation Amplifier:**
```
     ┌─────────┐
V⁺ → │         │
     │   INA   ├→ V_out
V⁻ → │         │
     └─────────┘
      Gain = 1 + 2R/R_g
```
- **High CMRR**
- **High input impedance**
- **Applications:** Bridge circuits, sensor interfaces

#### Filtering

**Anti-aliasing Filters:**
- Low-pass filter before ADC
- Cutoff: f_s/2 to f_s/10
- **Types:** Active, passive, switched capacitor

**Noise Reduction:**
- Band-pass filtering around signal frequency
- Notch filters for specific interference (e.g., 50/60Hz)

#### Isolation

**Methods:**
- **Optical isolators:** LEDs and phototransistors
- **Transformers:** Magnetic coupling
- **Capacitive coupling**

**Applications:**
- Ground loop elimination
- High voltage isolation
- Noise immunity

### 4.4 Sensor-Actuator Integration

#### Complete Control Loop
```
     ┌─────┐  ┌─────┐  ┌─────┐  ┌─────┐
Ref→│Error├→│ PID ├→│Drive ├→│Actuator├→Plant
     └─────┘  └─────┘  │ Amp │  └─────┘  │
        ↑              └─────┘           │
        │                                │
        └────────── Sensor ←─────────────┘
```

#### Drive Electronics

**Motor Drivers:**
```
     ┌─────────┐
PWM →│   H-    │→ Motor
Dir →│  Bridge │
     └─────────┘
```

**Specifications:**
- **Voltage/current rating**
- **Switching frequency**
- **Protection:** Overcurrent, overtemperature
- **Efficiency**

#### Power Considerations

**Actuator Power Requirements:**
```
P_electrical = V × I
P_mechanical = τ × ω
Efficiency = P_mechanical / P_electrical
```

**Peak vs Continuous Power:**
- **Peak:** Short-term overload capability
- **Continuous:** Sustained operation limits

### 4.5 Practical Implementation Issues

#### Calibration
```
         Known Input
            ↓
Sensor → Output → Compare → Correction
```

**Methods:**
- **Zero calibration:** Apply zero input, adjust offset
- **Span calibration:** Apply full-scale input, adjust gain
- **Multi-point calibration:** Multiple points, curve fitting

#### Nonlinearity Compensation

**Types of Nonlinearity:**
- **Saturation:** Output limits at extremes
- **Dead zone:** No response near zero
- **Hysteresis:** Different up/down characteristics
- **Backlash:** Mechanical play

**Compensation Methods:**
- **Lookup tables**
- **Polynomial fitting**
- **Inverse model compensation**

#### Reliability and Safety

**Redundancy:**
- **Dual sensors:** Vote or average
- **Triple modular redundancy:** Majority voting
- **Watchdog timers:** Detect controller failure

**Fail-Safe Design:**
- **Spring return actuators**
- **Brake mechanisms**
- **Safe state transitions**

### 4.6 Case Studies

#### Robotic Arm Control
```
         ┌─────┐    ┌─────┐    ┌─────┐
θ_ref →│ PID ├→│Driver├→│Motor├→ Arm
         └─────┘    └─────┘    └─────┘
                            │
                    ┌─────┴─────┐
                    │  Encoder  │
                    └─────┬─────┘
```

**Sensors:** Absolute encoder, torque sensor
**Actuators:** Brushless servo motors
**Challenges:** Flexibility, backlash, gravity compensation

#### Process Temperature Control
```
         ┌─────┐    ┌─────┐    ┌─────┐
T_ref →│ PID ├→│  SSR  ├→│Heater├→ Process
         └─────┘    └─────┘    └─────┘
                            │
                    ┌─────┴─────┐
                    │ Thermocouple│
                    │ + Cold    │
                    │ Junction  │
                    └─────┬─────┘
```

**Sensors:** Thermocouple with cold junction compensation
**Actuators:** Solid-state relay controlling heater
**Challenges:** Thermal lag, disturbance rejection

---

## Practice Problems

### Problem 1: Stability Analysis
```
Given: G(s)H(s) = K / [s(s+1)(s+5)]
Determine:
a) Range of K for stability using Routh-Hurwitz
b) Gain and phase margins for K = 10
c) Steady-state error for unit ramp input
```

### Problem 2: PID Design
```
A temperature control system has transfer function:
G(s) = 2e^{-2s} / (10s + 1)

Design a PID controller using:
a) Ziegler-Nichols tuning rules
b) Cohen-Coon method
Compare the performance of both designs.
```

### Problem 3: Sensor Selection
```
Select appropriate sensors for:
a) Precision position control of a robotic arm (0.1mm accuracy)
b) Speed control of a conveyor belt (0-1000 RPM)
c) Force control in a robotic gripper (0-100N)
Justify your selections with technical reasoning.
```

### Problem 4: System Response
```
A second-order system has:
ω_n = 10 rad/s, ζ = 0.6, K = 1
Calculate:
a) Peak overshoot and peak time
b) Rise time and settling time
c) Steady-state error for step input
Plot the expected step response.
```

### Problem 5: Complete System Design
```
Design a DC motor position control system with:
- Range: ±180°
- Resolution: 0.1°
- Maximum velocity: 100°/s
- Load inertia: 0.01 kg·m²

Specify:
a) Appropriate sensor and its specifications
b) Actuator type and power requirements
c) Controller structure and initial tuning
```

## Conclusion

This comprehensive control systems course covers the fundamental principles from basic feedback theory to practical implementation with sensors and actuators. The material progresses from mathematical foundations through controller design to real-world system integration.

Key concepts to remember:
- Feedback enables disturbance rejection and performance improvement
- Transfer functions provide powerful analysis tools in frequency domain
- PID control remains the workhorse of industrial control systems
- Proper sensor and actuator selection is critical for system performance
- Practical implementation requires addressing real-world limitations

Control systems engineering bridges theory and practice, requiring both mathematical understanding and practical knowledge of components and their limitations. Modern control continues to evolve with adaptive control, model predictive control, and intelligent control techniques building upon these fundamental principles.
