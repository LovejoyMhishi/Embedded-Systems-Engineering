# Digital Electronics

## Table of Contents
1. [Logic Gates & Boolean Algebra](#1-logic-gates--boolean-algebra)
2. [Sequential Logic](#2-sequential-logic)
3. [Counters & Timers](#3-counters--timers)
4. [Memory & PLDs](#4-memory--plds)

---

## 1. Logic Gates & Boolean Algebra

### 1.1 Number Systems

#### Binary System
**Base-2 Number System:**
```
Digits: 0, 1
Positional weights: 2ⁿ
```

**Binary to Decimal Conversion:**
```
1011₂ = 1×2³ + 0×2² + 1×2¹ + 1×2⁰
       = 8 + 0 + 2 + 1 = 11₁₀
```

**Decimal to Binary Conversion:**
```
13₁₀ to binary:
13 ÷ 2 = 6 remainder 1 ↑
6 ÷ 2 = 3 remainder 0  |
3 ÷ 2 = 1 remainder 1  |
1 ÷ 2 = 0 remainder 1  |
Result: 1101₂
```

#### Hexadecimal System
**Base-16 Number System:**
```
Digits: 0-9, A-F
A=10, B=11, C=12, D=13, E=14, F=15
```

**Hex to Binary Conversion:**
```
A3₁₆ = A    3
      = 1010 0011 = 10100011₂
```

#### Binary Arithmetic

**Binary Addition:**
```
   1 1 1    (carry)
   0 1 1 0  (6)
 + 0 1 1 1  (7)
 ---------
   1 1 0 1  (13)
```

**Binary Subtraction (2's Complement):**
```
13 - 7 = 13 + (-7)

7 in binary: 0111
1's complement: 1000
2's complement: 1001

  1101 (13)
+ 1001 (-7)
------
 10110 → discard carry → 0110 (6)
```

### 1.2 Basic Logic Gates

#### AND Gate
**Symbol:**
```
   ┌───┐
A ─┤ & ├─ Y
B ─┤   │
   └───┘
```

**Truth Table:**
```
A | B | Y
--+---+--
0 | 0 | 0
0 | 1 | 0
1 | 0 | 0
1 | 1 | 1
```

**Boolean Expression:** Y = A · B

#### OR Gate
**Symbol:**
```
   ┌───┐
A ─┤ ≥1 ├─ Y
B ─┤    │
   └───┘
```

**Truth Table:**
```
A | B | Y
--+---+--
0 | 0 | 0
0 | 1 | 1
1 | 0 | 1
1 | 1 | 1
```

**Boolean Expression:** Y = A + B

#### NOT Gate (Inverter)
**Symbol:**
```
   ┌───┐
A ─┤ 1 ├─ Y
   └───┘
```

**Truth Table:**
```
A | Y
--+--
0 | 1
1 | 0
```

**Boolean Expression:** Y = A̅

#### Universal Gates

**NAND Gate:**
```
   ┌───┐
A ─┤ &̅ ├─ Y
B ─┤   │
   └───┘
```
Y = A · B

**NOR Gate:**
```
   ┌───┐
A ─┤ ≥1├─ Y
B ─┤   │
   └───┘
```
Y = A + B

#### XOR Gate (Exclusive OR)
**Symbol:**
```
   ┌───┐
A ─┤ =1 ├─ Y
B ─┤    │
   └───┘
```

**Truth Table:**
```
A | B | Y
--+---+--
0 | 0 | 0
0 | 1 | 1
1 | 0 | 1
1 | 1 | 0
```

**Boolean Expression:** Y = A ⊕ B = A·B̅ + A̅·B

#### XNOR Gate (Exclusive NOR)
**Symbol:**
```
   ┌───┐
A ─┤ = ├─ Y
B ─┤   │
   └───┘
```
Y = A ⊙ B = A·B + A̅·B̅

### 1.3 Boolean Algebra Laws

#### Fundamental Identities

**Commutative Law:**
```
A + B = B + A
A · B = B · A
```

**Associative Law:**
```
(A + B) + C = A + (B + C)
(A · B) · C = A · (B · C)
```

**Distributive Law:**
```
A · (B + C) = A·B + A·C
A + (B·C) = (A + B) · (A + C)
```

#### De Morgan's Theorems
```
A · B = A̅ + B̅
A + B = A̅ · B̅
```

**Proof by Truth Table:**
```
A | B | A·B | A̅+B̅ | A+B | A̅·B̅
--+---+-----+-----+-----+-----
0 | 0 |  1  |  1  |  1  |  1
0 | 1 |  1  |  1  |  0  |  0
1 | 0 |  1  |  1  |  0  |  0
1 | 1 |  0  |  0  |  0  |  0
```

#### Other Important Theorems
```
A + A·B = A           (Absorption)
A · (A + B) = A       (Absorption)
A + A̅·B = A + B       (Reduction)
A · (A̅ + B) = A·B     (Reduction)
```

### 1.4 Karnaugh Maps (K-Maps)

#### 2-Variable K-Map
```
     B̅   B
A̅ |  0 |  1
A  |  2 |  3
```

**Example: F(A,B) = Σ(1,3)**
```
     B̅   B
A̅ |  0 |  1
A  |  0 |  1
```
F = B

#### 3-Variable K-Map
```
     B̅C̅  B̅C  BC  BC̅
A̅ |  0 |  1 |  3 |  2
A  |  4 |  5 |  7 |  6
```

**Example: F(A,B,C) = Σ(0,2,4,6)**
```
     B̅C̅  B̅C  BC  BC̅
A̅ |  1 |  0 |  0 |  1
A  |  1 |  0 |  0 |  1
```
F = C̅

#### 4-Variable K-Map
```
     C̅D̅  C̅D  CD  CD̅
A̅B̅ |  0 |  1 |  3 |  2
A̅B |  4 |  5 |  7 |  6
AB | 12 | 13 | 15 | 14
AB̅ |  8 |  9 | 11 | 10
```

**Grouping Rules:**
- Groups must be powers of 2 (1,2,4,8,16...)
- Groups must be rectangular
- Wrap-around allowed
- Largest groups possible

### 1.5 Combinational Logic Design

#### Design Procedure
1. **Problem Statement**
2. **Truth Table**
3. **Boolean Expression**
4. **Simplification (K-map)**
5. **Logic Diagram**

#### Example: 2-bit Comparator
**Compare A₁A₀ with B₁B₀**

**Truth Table:**
```
A1 A0 B1 B0 | A>B A=B A<B
------------+-------------
0  0  0  0  | 0   1   0
0  0  0  1  | 0   0   1
... (16 rows)
1  1  1  0  | 1   0   0
1  1  1  1  | 0   1   0
```

**Boolean Expressions:**
```
A>B = A1·B1̅ + A1·A0·B1̅·B0̅ + A0·B1̅·B0̅
A=B = (A1⊕B1̅)·(A0⊕B0̅)
A<B = A1̅·B1 + A1̅·A0̅·B1·B0 + A0̅·B1·B0
```

#### Multiplexers (MUX)

**2:1 Multiplexer:**
```
   ┌──────┐
I0─┤0     │
   │  MUX ├─ Y
I1─┤1     │
   │      │
S ─┤S     │
   └──────┘
```
Y = S̅·I₀ + S·I₁

**4:1 Multiplexer:**
```
   ┌──────┐
I0─┤0     │
I1─┤1     │
I2─┤2  MUX├─ Y
I3─┤3     │
   │      │
S1─┤S1    │
S0─┤S0    │
   └──────┘
```
Y = S₁̅·S₀̅·I₀ + S₁̅·S₀·I₁ + S₁·S₀̅·I₂ + S₁·S₀·I₃

#### Demultiplexers (DEMUX)

**1:4 Demultiplexer:**
```
   ┌──────┐
I ─┤      │
   │ DEMUX├─ Y0
S1─┤S1    ├─ Y1
S0─┤S0    ├─ Y2
   │      ├─ Y3
   └──────┘
```
Y₀ = S₁̅·S₀̅·I
Y₁ = S₁̅·S₀·I
Y₂ = S₁·S₀̅·I
Y₃ = S₁·S₀·I

#### Encoders and Decoders

**3:8 Decoder:**
```
   ┌──────┐
A2─┤2     ├─ Y0
A1─┤1     ├─ Y1
A0─┤0     ├─ Y2
   │DEC 3:8├─ Y3
E ─┤E     ├─ Y4
   │      ├─ Y5
   │      ├─ Y6
   │      ├─ Y7
   └──────┘
```
Y₀ = E·A₂̅·A₁̅·A₀̅
Y₁ = E·A₂̅·A₁̅·A₀
...
Y₇ = E·A₂·A₁·A₀

**8:3 Priority Encoder:**
```
   ┌──────┐
I0─┤0     ├─ A0
I1─┤1     ├─ A1
I2─┤2     ├─ A2
I3─┤3     ├─ V (Valid)
I4─┤4 PRIO│
I5─┤5 ENC │
I6─┤6     │
I7─┤7     │
   └──────┘
```

---

## 2. Sequential Logic

### 2.1 Latches

#### SR Latch (Set-Reset)

**NAND Implementation:**
```
   ┌───┐
S ─┤&̅  ├─ Q
   │   │
   └─┬─┘
     │
   ┌─┴─┐
   │&̅  │
R ─┤   ├─ Q̅
   └───┘
```

**Truth Table:**
```
S | R | Q | Q̅
--+---+---+---
0 | 0 | ? | ?  (Invalid)
0 | 1 | 0 | 1
1 | 0 | 1 | 0
1 | 1 | Q₀| Q̅₀ (Hold)
```

#### D Latch (Data Latch)

**Circuit:**
```
   ┌──────┐
D ─┤0     │
   │  MUX ├─ Q
Q ─┤1     │
   │      │
E ─┤S     │
   └──────┘
```

**Operation:**
- When E = 1: Q follows D
- When E = 0: Q holds previous value

### 2.2 Flip-Flops

#### D Flip-Flop (Positive Edge-Triggered)

**Symbol:**
```
   ┌───┐
D ─┤>D ├─ Q
   │   │
CLK─┤▷  ├─ Q̅
   └───┘
```

**Timing Diagram:**
```
CLK: __┐__┐__┐__┐__
D:   ______┐______┐
Q:   ______┐______┐
```
Q changes only at rising edge of CLK

**Characteristic Table:**
```
D | Q(t+1)
--+-------
0 |   0
1 |   1
```

#### JK Flip-Flop

**Symbol:**
```
   ┌───┐
J ─┤>J ├─ Q
   │   │
K ─┤>K ├─ Q̅
   │   │
CLK─┤▷  │
   └───┘
```

**Truth Table:**
```
J | K | Q(t+1)
--+---+--------
0 | 0 |   Q(t)  (Hold)
0 | 1 |    0    (Reset)
1 | 0 |    1    (Set)
1 | 1 |   Q̅(t)  (Toggle)
```

#### T Flip-Flop (Toggle)

**Symbol:**
```
   ┌───┐
T ─┤>T ├─ Q
   │   │
CLK─┤▷  ├─ Q̅
   └───┘
```

**Operation:**
- T = 0: Q(t+1) = Q(t) (Hold)
- T = 1: Q(t+1) = Q̅(t) (Toggle)

### 2.3 Registers

#### 4-bit Register
```
     ┌──────────┐
D3 ──┤>D      Q3├── Q3
D2 ──┤>D      Q2├── Q2
D1 ──┤>D      Q1├── Q1
D0 ──┤>D      Q0├── Q0
     │         │
CLK ─┤▷        │
     └──────────┘
```

#### Shift Register (Serial-in, Serial-out)

**4-bit SISO:**
```
Data ─→ [D]─Q→ [D]─Q→ [D]─Q→ [D]─Q → Output
        │     │     │     │
       CLK   CLK   CLK   CLK
```

**Operation:**
- Each clock pulse shifts data one position right
- After 4 clocks, input appears at output

#### Universal Shift Register

**Modes:**
- Parallel Load
- Shift Left
- Shift Right
- Hold

**Control Signals:**
```
S1 S0 | Mode
------+---------
0  0  | Hold
0  1  | Shift Right
1  0  | Shift Left
1  1  | Parallel Load
```

### 2.4 State Machines

#### Moore Machine
**Output depends only on current state**
```
Input → Next State Logic → State Register → Output Logic → Output
         ↑                             ↓
         └────── State Feedback ───────┘
```

#### Mealy Machine
**Output depends on current state AND input**
```
Input → Next State Logic → State Register → Output Logic → Output
         ↑                             ↓           ↑
         └────── State Feedback ───────┘           │
                                                   │
                         Input ────────────────────┘
```

#### State Diagram Example: 3-State Sequence Detector

**States:**
- S0: No 1's detected
- S1: One 1 detected
- S2: Two consecutive 1's detected

**State Transitions:**
```
     0/0   1/0   1/1
S0 ───→ S0 ───→ S1 ───→ S2
        ↑       │       │
        │ 0/0   │0/0    │0/0
        └───────┴───────┘
```

#### State Table
```
Present State | Input | Next State | Output
-------------+-------+------------+-------
     S0      |   0   |     S0     |   0
     S0      |   1   |     S1     |   0
     S1      |   0   |     S0     |   0
     S1      |   1   |     S2     |   0
     S2      |   0   |     S0     |   0
     S2      |   1   |     S2     |   1
```

#### Implementation with D Flip-Flops
```
State Encoding:
S0 = 00, S1 = 01, S2 = 10

D1 = Q1·Q0̅·X + Q1·Q0·X
D0 = Q1̅·Q0̅·X + Q1·Q0·X
Y = Q1·X
```

---

## 3. Counters & Timers

### 3.1 Asynchronous (Ripple) Counters

#### 4-bit Binary Ripple Counter
```
CLK ─→ [D]─Q0→ [D]─Q1→ [D]─Q2→ [D]─Q3
       │^     │^     │^     │^
      CLK    CLK    CLK    CLK
```

**Waveform:**
```
CLK: __┐__┐__┐__┐__┐__┐__┐__┐__┐
Q0:  __┐__┘__┐__┘__┐__┘__┐__┘
Q1:  ______┐__┘_____┐__┘_____
Q2:  ____________┐__┘_________
Q3:  ____________________┐__┘
```

**Count Sequence:** 0000, 0001, 0010, ..., 1111

#### MOD-N Ripple Counter
**MOD-10 (Decade) Counter:**
- Reset when count reaches 10 (1010₂)
- Uses NAND gate to detect 1010 and reset all flip-flops

### 3.2 Synchronous Counters

#### 4-bit Synchronous Binary Counter
```
All flip-flops clocked simultaneously
Toggle condition:
T0 = 1 (always toggle)
T1 = Q0
T2 = Q0·Q1
T3 = Q0·Q1·Q2
```

**Implementation with JK Flip-Flops:**
```
J0 = K0 = 1
J1 = K1 = Q0
J2 = K2 = Q0·Q1
J3 = K3 = Q0·Q1·Q2
```

#### MOD-6 Synchronous Counter (0 to 5)

**State Sequence:** 000, 001, 010, 011, 100, 101

**Flip-Flop Inputs (JK):**
```
J0 = K0 = 1
J1 = Q0·Q2̅
K1 = Q0
J2 = Q0·Q1
K2 = Q0·Q1
```

**Reset Logic:** Detect state 110 (6) and reset

### 3.3 Up/Down Counters

#### 4-bit Synchronous Up/Down Counter

**Control:**
- UP/DOWN = 1: Count up
- UP/DOWN = 0: Count down

**Toggle Conditions:**
```
T0 = 1
T1 = Q0 ⊕ UP/DOWN'
T2 = (Q0·Q1) ⊕ UP/DOWN'
T3 = (Q0·Q1·Q2) ⊕ UP/DOWN'
```

### 3.4 Shift Register Counters

#### Ring Counter
```
4-bit Ring Counter:
0001 → 0010 → 0100 → 1000 → 0001
```

**Implementation:**
```
Q3 → D0, Q0 → D1, Q1 → D2, Q2 → D3
Initial state: 0001 (preset)
```

#### Johnson Counter (Twisted Ring Counter)
```
4-bit Johnson Counter:
0000 → 1000 → 1100 → 1110 → 1111 → 0111 → 0011 → 0001 → 0000
```

**Implementation:**
```
Q3̅ → D0, Q0 → D1, Q1 → D2, Q2 → D3
```

### 3.5 Timer Circuits

#### 555 Timer IC

**Pinout:**
```
      ┌───┐
 GND ─┤1  └─ Vcc (8)
Trig ─┤2     ├─ Discharge (7)
 Out ─┤3     ├─ Threshold (6)
Reset ─┤4     ├─ Control (5)
      └───┘
```

#### Astable Multivibrator (Oscillator)

**Circuit:**
```
     +Vcc
      │
     [R1]
      │
      ├─→ Discharge (7)
     [R2]
      │
      ├─→ Threshold (6)
      │   Trigger (2)
     [C]
      │
     GND
```

**Frequency Calculation:**
```
t_high = 0.693 × (R1 + R2) × C
t_low = 0.693 × R2 × C
Frequency = 1.44 / [(R1 + 2R2) × C]
Duty Cycle = (R1 + R2) / (R1 + 2R2)
```

**Design Example: 1kHz, 60% duty cycle**
```
Choose C = 0.1μF
t_total = 1/1000 = 1ms
t_high = 0.6ms, t_low = 0.4ms

R2 = t_low / (0.693 × C) = 5.77kΩ
R1 = t_high / (0.693 × C) - R2 = 2.89kΩ
```

#### Monostable Multivibrator (One-shot)

**Operation:**
- Generates single pulse of fixed duration
- Triggered by negative edge on pin 2

**Pulse Width:**
```
t_pulse = 1.1 × R × C
```

---

## 4. Memory & PLDs

### 4.1 Memory Fundamentals

#### Memory Organization
```
       Address Bus
          ↓
┌───┬──────────────┐
│   │  Memory      │
│   │  Location    │ ← Data Bus
│   │              │
│   │  2ⁿ × m      │
└───┴──────────────┘
```
- n address lines → 2ⁿ locations
- m data lines → m bits per location

#### Memory Types

**Volatile Memory:**
- RAM (Random Access Memory)
- Loses data when power off

**Non-Volatile Memory:**
- ROM (Read Only Memory)
- Flash Memory
- Retains data when power off

### 4.2 RAM (Random Access Memory)

#### SRAM (Static RAM)
**Cell Structure:**
```
     ┌───┐       ┌───┐
Bit ─┤   ├───┐   │   │
     └─┬─┘   │   └─┬─┘
       │     ├─○   │
     ┌─┴─┐   │   ┌─┴─┐
Bit̅ ─┤   ├───┘   │   │
     └───┘       └───┘
     6 transistors per cell
```

**Characteristics:**
- Fast access time
- No refresh needed
- Higher power consumption
- More expensive

#### DRAM (Dynamic RAM)
**Cell Structure:**
```
     ┌───┐
Bit ─┤   ├───○───┐
     └─┬─┘       │
       │        ┌┴┐
Word ──┴───────○│ │ C
                └┬┘
                 │
                GND
1 transistor + 1 capacitor per cell
```

**Characteristics:**
- Needs refresh (every 2-64ms)
- Higher density
- Lower power
- Slower than SRAM

#### Memory Timing

**Read Cycle:**
```
Address ───┐
           │───────────
           │
CS̅ ────────┐
           │───────────
           │
Data ──────────────────┐
                       │─────
```

**Write Cycle:**
```
Address ───┐
           │───────────
           │
CS̅ ────────┐
           │───────────
WE̅ ────────┐
           │───────────
Data ──────┐
           │───────────
```

### 4.3 ROM (Read Only Memory)

#### Mask ROM
- Programmed during manufacturing
- Cannot be changed
- High volume, low cost

#### PROM (Programmable ROM)
- User programmable (once)
- Uses fuses/antifuses

#### EPROM (Erasable PROM)
- UV erasable
- Window package
- Multiple programming cycles

#### EEPROM (Electrically Erasable PROM)
- Byte-level erase/write
- Limited write cycles (~10⁵)
- Used for configuration data

### 4.4 Flash Memory

#### NAND Flash
- High density
- Block-oriented
- Used in SSDs, USB drives

#### NOR Flash
- Random access
- Execute-in-place capability
- Used for firmware storage

### 4.5 Programmable Logic Devices (PLDs)

#### PLA (Programmable Logic Array)
**Structure:**
```
Inputs → AND Array → OR Array → Outputs
         ˄          ˄
     Programmable Programmable
```

**Example Implementation:**
```
F1 = A·B + A̅·C
F2 = B·C + A
```

#### PAL (Programmable Array Logic)
**Structure:**
```
Inputs → AND Array → OR Array → Outputs
         ˄          Fixed
     Programmable
```

**Advantage:** Simpler than PLA, fixed OR array

#### CPLD (Complex PLD)
**Architecture:**
```
Multiple PAL-like blocks
+ Programmable interconnect
+ I/O blocks
```

**Characteristics:**
- Predictable timing
- Non-volatile configuration
- Good for complex combinational logic

### 4.6 FPGA (Field Programmable Gate Array)

#### Basic Architecture
```
┌─────────────────┐
│  Configurable   │
│  Logic Blocks   │  ← Programmable
│   (CLBs)        │     Interconnect
│                 │
│  I/O Blocks     │
│                 │
│  Block RAM      │
└─────────────────┘
```

#### CLB (Configurable Logic Block)
```
┌─────────────────┐
│  Look-Up Table  │
│     (LUT)       │
│                 │
│  Flip-Flops     │
│                 │
│  Multiplexers   │
└─────────────────┘
```

**4-input LUT Example:**
- Can implement any 4-input Boolean function
- Essentially a 16×1 memory
- Truth table stored in SRAM

#### FPGA vs CPLD
```
Parameter    | FPGA      | CPLD
-------------+-----------+-----------
Capacity     | High      | Medium
Speed        | High      | Medium
Flexibility  | High      | Medium
Power        | Higher    | Lower
Cost         | Higher    | Lower
Volatility   | Usually   | Non-volatile
```

### 4.7 Memory System Design

#### Address Decoding
**Example: 64K system with 4×16K chips**
```
A15 A14 | Chip Selected
--------+---------------
  0   0 | Chip 0 (0000-3FFF)
  0   1 | Chip 1 (4000-7FFF)
  1   0 | Chip 2 (8000-BFFF)
  1   1 | Chip 3 (C000-FFFF)
```

#### Memory Map
```
Address Range  | Device
---------------+---------------
0000 - 3FFF    | RAM (16K)
4000 - 7FFF    | ROM (16K)
8000 - BFFF    | I/O Devices
C000 - FFFF    | Unused
```

### 4.8 Cache Memory

#### Direct Mapped Cache
```
Main Memory Block → Cache Line = Block Address MOD Cache Size
```

**Address Format:**
```
Tag | Index | Block Offset
```

#### Cache Operation
- **Hit**: Data found in cache
- **Miss**: Data not in cache, fetch from main memory
- **Write-through**: Write to cache and main memory simultaneously
- **Write-back**: Write only to cache, update main memory later

---

## Practice Problems

### Problem 1: Boolean Algebra Simplification
```
Simplify using K-map:
F(A,B,C,D) = Σ(0,2,4,5,6,7,8,10,13,15)
```

### Problem 2: Sequential Circuit Design
```
Design a 3-bit synchronous counter that counts through
the sequence: 0,1,3,5,7,0... using JK flip-flops
```

### Problem 3: Memory System Design
```
Design a 64K×8 memory system using 16K×4 RAM chips.
Show the complete address decoding and chip organization.
```

### Problem 4: State Machine Design
```
Design a state machine to detect the sequence "1011"
with overlap allowed. Use D flip-flops and draw the
state diagram and logic circuit.
```

### Problem 5: Timer Design
```
Design a 555 timer circuit to produce a 2kHz square wave
with 75% duty cycle. Calculate all component values.
```

## Conclusion

This comprehensive digital electronics course covers the fundamental concepts from basic logic gates to complex memory systems and programmable logic devices. The material progresses from combinatorial logic through sequential circuits to system-level design.

Key concepts to remember:
- Boolean algebra and Karnaugh maps are essential for logic optimization
- Sequential circuits introduce the dimension of time and memory
- Counters and timers are fundamental building blocks for digital systems
- Memory hierarchy and organization are critical for computer architecture
- PLDs and FPGAs enable flexible digital system implementation

Digital electronics forms the foundation of modern computing, communication, and control systems. Mastery of these concepts is essential for any electrical or computer engineering student.
