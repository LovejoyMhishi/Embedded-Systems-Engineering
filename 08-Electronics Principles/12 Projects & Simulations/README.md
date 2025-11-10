<h1 align="center">Projects & Simulations</h1>

## Table of Contents
1. [SPICE Simulations](#1-spice-simulations)
2. [Analog Projects](#2-analog-projects)
3. [Power Electronics Projects](#3-power-electronics-projects)
4. [Control & Instrumentation Projects](#4-control--instrumentation-projects)

---

## 1. SPICE Simulations

### 1.1 SPICE Fundamentals

#### What is SPICE?
> Simulation Program with Integrated Circuit Emphasis

**SPICE History:**
- Developed at UC Berkeley (1970s)
- Industry standard for circuit simulation
- Multiple commercial variants: LTspice, PSpice, HSPICE

#### SPICE Netlist Structure
```
* Comment line
.Title Line
Circuit Elements
.Analysis Commands
.END
```

#### Basic Circuit Elements

**Resistor:**
```
R1 node1 node2 value
Example: R1 1 2 1k
```

**Capacitor:**
```
C1 node1 node2 value
Example: C1 2 0 100n
```

**Inductor:**
```
L1 node1 node2 value
Example: L1 3 4 10m
```

**Voltage Source:**
```
V1 node+ node- value
Example: V1 1 0 DC 5V
```

### 1.2 Analysis Types

#### DC Operating Point Analysis
```
.OP
```
Calculates DC voltages and currents

#### DC Sweep Analysis
```
.DC V1 0 10 0.1
```
Sweeps voltage source V1 from 0V to 10V in 0.1V steps

#### Transient Analysis
```
.TRAN 1us 10ms
```
Time-domain analysis for 10ms with 1μs time steps

#### AC Analysis
```
.AC DEC 10 1 1Meg
```
Frequency response from 1Hz to 1MHz with 10 points per decade

### 1.3 LTspice Tutorial

#### Basic Schematic Capture

**Creating a Simple RC Circuit:**
```
1. Place components:
   - Voltage source (F2)
   - Resistor (F2) 
   - Capacitor (F2)
   - Ground (F3)

2. Connect components (F3)

3. Set component values:
   - Voltage source: DC 5V
   - Resistor: 1k
   - Capacitor: 1u

4. Add simulation command:
   .tran 1ms
```

#### Advanced Features

**Parameter Sweeping:**
```
.step param Rval list 1k 2.2k 4.7k
R1 1 2 {Rval}
```

**Monte Carlo Analysis:**
```
.step param run 1 100 1
R1 1 2 {1k*(1+0.1*gauss(run))}
```

**Behavioral Sources:**
```
B1 out 0 V=V(1)*sin(2*pi*1k*time)
```

### 1.4 Practical SPICE Examples

#### Example 1: Common Emitter Amplifier
```
* Common Emitter Amplifier
Vcc 1 0 DC 12
Vin 2 0 AC 1 SIN(0 0.1 1k)
R1 1 3 22k
R2 3 0 4.7k
Rc 1 4 2.2k
Re 5 0 1k
C1 2 3 10u
C2 4 6 10u
C3 5 0 100u
Q1 4 3 5 NPN
.model NPN NPN(Is=1e-14 Bf=100 Vaf=100)

.OP
.AC DEC 10 10 1Meg
.TRAN 0.01ms 5ms
.END
```

#### Example 2: Active Filter
```
* Sallen-Key Low Pass Filter
Vin 1 0 AC 1
R1 1 2 10k
R2 2 3 10k
C1 3 0 10n
C2 2 4 10n
X1 2 4 4 5 opamp
R3 4 5 100k
R4 5 0 100k

.subckt opamp 1 2 3
E1 3 0 1 2 100k
.ends

.AC DEC 20 10 100k
.END
```

#### Example 3: Buck Converter
```
* Buck Converter Simulation
Vin 1 0 DC 12
S1 1 2 3 0 SW
D1 0 2 DIODE
L1 2 4 100u
C1 4 0 100u
Rload 4 0 10

Vpwm 3 0 PULSE(0 5 0 1n 1n 5u 10u)

.model SW SW(Ron=0.1 Roff=1Meg Vt=2.5 Vh=0.5)
.model DIODE D(Is=1e-14)

.TRAN 0.1u 1ms
.END
```

### 1.5 Model Libraries

#### Diode Models
```
.model 1N4148 D(Is=2.52n Rs=0.568 N=1.752 Cjo=4p 
+ M=0.4 tt=20n Iave=200m Vpk=75 mfg=OnSemi type=silicon)
```

#### BJT Models
```
.model 2N2222 NPN(Is=14.34f Xti=3 Eg=1.11 Vaf=74.03 
+ Bf=255.9 Ne=1.5 Ise=14.34f Ikf=0.2847 Xtb=1.5 
+ Br=6.092 Nc=2 Isc=0 Ikr=0 Rc=1 Cjc=7.306p 
+ Mjc=0.3416 Vjc=0.75 Fc=0.5 Cje=22.01p Mje=0.377 
+ Vje=0.75 Tr=46.91n Tf=411.1p Itf=0.6 Vtf=1.7 
+ Xtf=3 Rb=10)
```

#### MOSFET Models
```
.model IRF540 NMOS(Level=3 Gamma=0 Delta=0 Eta=0 
+ Theta=0 Kappa=0 Vmax=0 Xj=0 Tox=100n Uo=600 
+ Phi=0.6 Rs=1.624m Kp=20.53u W=0.887 L=2u Vto=3.831 
+ Rd=1.031m Rds=444.4K Cbd=3.229n Pb=0.8 Mj=0.5 
+ Fc=0.5 Cgso=9.027n Cgdo=1.679n Rg=1.031 Is=1.135p 
+ N=1 Tt=112n)
```

### 1.6 Simulation Best Practices

#### Convergence Help
```
.options reltol=0.01 abstol=1p vntol=1u
```

#### Initial Conditions
```
.IC V(node)=value
```

#### Temperature Sweep
```
.step temp -40 125 10
```

---

## 2. Analog Projects

### 2.1 Audio Amplifier Project

#### Design Specifications
```
Power Output: 10W RMS
Load Impedance: 8Ω
Frequency Response: 20Hz-20kHz (±1dB)
THD: <0.1%
Input Sensitivity: 1V RMS
Power Supply: ±15V
```

#### Circuit Design

**Input Stage:**
```
Differential amplifier with current mirror
Gain: 20dB
Input impedance: 47kΩ
```

**Voltage Amplification Stage:**
```
Common emitter with active load
Gain: 26dB
Miller compensation for stability
```

**Output Stage:**
```
Complementary emitter follower
Bias: Class AB
Current limiting protection
```

#### Complete Schematic
```
* 10W Audio Amplifier
* Input Stage
Q1 1 2 3 NPN
Q2 4 2 5 NPN
Q3 3 6 7 NPN
Q4 5 6 7 NPN
R1 8 1 2.2k
R2 8 4 2.2k
R3 3 9 1k
R4 5 9 1k

* VAS Stage
Q5 10 3 11 NPN
R5 8 10 4.7k
C1 10 11 100p

* Output Stage
Q6 12 11 13 NPN
Q7 13 11 14 PNP
R6 12 8 100
R7 9 14 100
R8 13 15 0.22
R9 16 13 0.22

* Power Supply
Vpos 8 0 15
Vneg 9 0 -15
Vin 2 0 AC 1

.model NPN NPN(Bf=200 Vaf=100)
.model PNP PNP(Bf=200 Vaf=100)

.AC DEC 20 10 100k
.TRAN 0.01ms 10ms
.FOUR 1k V(15)
.END
```

### 2.2 Instrumentation Amplifier Project

#### Design Requirements
```
Gain: 1 to 1000 (programmable)
CMRR: >100dB
Input Impedance: >1GΩ
Noise: <10nV/√Hz
Bandwidth: DC to 10kHz
```

#### Three Op-Amp Architecture
```
     ┌───┐   ┌───┐
V1 ──┤A1 ├─┐ │A3 ├─ Vout
     └─┬─┘ │ └─┬─┘
       │   │   │
      Rg   │   │
       │   │   │
     ┌─┴─┐ │ ┌─┴─┐
V2 ──┤A2 ├─┘ │   │
     └───┘   └───┘
       R1     R2
```

#### Complete Implementation
```
* Instrumentation Amplifier
* Input Stage
X1 1 2 3 4 5 opamp
X2 6 2 7 4 5 opamp
Rg 3 7 {Rgain}

* Output Stage
R1 3 8 10k
R2 7 8 10k
R3 8 9 10k
R4 9 0 10k
X3 8 9 10 4 5 opamp

* Power Supply
Vpos 4 0 15
Vneg 5 0 -15
Vin1 1 0 AC 1
Vin2 6 0 AC 1

* Programmable Gain
.param Rgain=49.9
.step param Rgain list 49.9 1.01k 10.1k 100k

.subckt opamp 1 2 3 4 5
Rin 1 2 1G
E1 6 0 1 2 100k
Rout 6 3 100
Vps 4 0 15
Vns 5 0 -15
.ends

.AC DEC 20 1 100k
.END
```

### 2.3 Active Filter Projects

#### 4th Order Low-Pass Filter

**Specifications:**
- Cutoff: 1kHz
- Response: Butterworth
- Stopband: -40dB at 5kHz
- Gain: 0dB

**Circuit Design:**
```
* 4th Order Butterworth LPF
* Stage 1 (Sallen-Key)
R1 1 2 11.25k
R2 2 3 11.25k
C1 2 4 10n
C2 3 0 10n
X1 2 3 4 5 6 opamp

* Stage 2 (Sallen-Key)
R3 4 7 6.25k
R4 7 8 6.25k
C3 7 9 10n
C4 8 0 10n
X2 7 8 9 5 6 opamp

* Power
Vpos 5 0 15
Vneg 6 0 -15
Vin 1 0 AC 1

.subckt opamp 1 2 3 4 5
E1 3 0 1 2 1e6
.ends

.AC DEC 20 10 100k
.END
```

### 2.4 Voltage Reference Project

#### Precision 5V Reference

**Specifications:**
- Output: 5.000V ± 1mV
- Temperature Coefficient: <10ppm/°C
- Load Regulation: <1mV (0-10mA)
- Line Regulation: <1mV (10-15V)

**Bandgap Reference Circuit:**
```
* Precision Voltage Reference
* Bandgap Core
Q1 1 2 3 NPN 1
Q2 4 2 3 NPN 8
R1 5 1 4.02k
R2 5 4 4.02k
R3 3 0 1k

* Op-Amp and Output
X1 1 4 6 7 0 opamp
R4 6 5 10k
R5 5 0 10k
R6 6 8 10k
R7 8 0 10k

* Startup Circuit
R8 7 9 100k
D1 9 0 DIODE
C1 6 0 100p

* Models
.model NPN NPN(Is=1e-16 Bf=100)
.model DIODE D(Is=1e-15)

.dc Vsupply 10 15 0.1
.temp -40 25 85
.END
```

---

## 3. Power Electronics Projects

### 3.1 Buck Converter Project

#### Design Specifications
```
Input: 12V-24V
Output: 5V ±2%
Current: 2A maximum
Efficiency: >85%
Switching Frequency: 100kHz
Ripple: <50mV
```

#### Component Selection

**Inductor Calculation:**
```
L_min = (Vin_max - Vout) × D_min / (f_sw × ΔI_L)
      = (24 - 5) × 0.208 / (100k × 0.4) ≈ 99μH
Use: 100μH, 3A saturation current
```

**Capacitor Calculation:**
```
C_min = ΔI_L / (8 × f_sw × ΔV_out)
      = 0.8 / (8 × 100k × 0.05) ≈ 20μF
Use: 47μF, 16V low-ESR
```

#### Complete Simulation
```
* Synchronous Buck Converter
Vin 1 0 DC 15
S1 1 2 3 0 NMOS
S2 2 0 4 0 NMOS
L1 2 5 100u
Cout 5 0 47u
Rload 5 0 2.5

* Gate Drivers
Vdrive1 3 0 PULSE(0 5 0 10n 10n 4u 10u)
Vdrive2 4 0 PULSE(0 5 5u 10n 10n 4u 10u)

* MOSFET Models
.model NMOS NMOS(Vto=2 Kp=0.1 Cgs=1n Cgd=200p)

* Analysis
.TRAN 0.1u 2ms
.MEAS TRAN Vout AVG V(5) FROM 1ms TO 2ms
.MEAS TRAN Iin AVG I(Vin) FROM 1ms TO 2ms
.MEAS TRAN Efficiency PARAM Vout*2/Iin/15
.END
```

### 3.2 Power Factor Correction (PFC) Project

#### Boost PFC Design

**Specifications:**
- Input: 85-265V AC, 50/60Hz
- Output: 400V DC
- Power: 150W
- Power Factor: >0.95
- THD: <10%

#### Control Strategy
- Average current mode control
- Voltage loop bandwidth: 10Hz
- Current loop bandwidth: 10kHz

#### Simulation Model
```
* PFC Boost Converter
Vac 1 0 SIN(0 170 50)
Dbridge 1 2 3 4 DBridge
L1 2 5 1m
S1 5 6 7 0 NMOS
D1 6 8 DIODE
Cout 8 0 220u
Rload 8 0 1k

* Current Sensing
Rsense 5 9 0.1
Xamp 9 0 10 opamp

* PWM Controller
Vref 11 0 DC 2.5
Xcomp 10 11 12 opamp
Vramp 13 0 PULSE(0 5 0 1n 1n 9u 10u)
Xpwm 12 13 14 comparator

* Gate Driver
Xdriver 14 0 7 buffer

.model DBridge D(Is=1e-14)
.model NMOS NMOS(Vto=4 Kp=0.5)
.model DIODE D(Is=1e-14 Cjo=100p)

.subckt opamp 1 2 3
E1 3 0 1 2 100k
.ends

.subckt comparator 1 2 3
Vref 4 0 2.5
E1 3 0 TABLE {V(1,2)} (-1,0) (1,5)
.ends

.subckt buffer 1 2 3
V1 4 0 12
V2 5 0 -12
E1 3 0 1 2 1
.ends

.TRAN 10u 40ms
.FOUR 50 I(Vac)
.END
```

### 3.3 Three-Phase Inverter Project

#### Design Specifications
```
Input: 400V DC
Output: 230V AC line-to-line, 50Hz
Power: 3kW
Switching: 10kHz SPWM
THD: <5%
```

#### Space Vector PWM Implementation

**Simulation Structure:**
```
* Three-Phase Inverter
Vdc 1 0 400

* Phase A
S1 1 2 10 0 NMOS
S2 2 0 11 0 NMOS

* Phase B  
S3 1 3 12 0 NMOS
S4 3 0 13 0 NMOS

* Phase C
S5 1 4 14 0 NMOS
S6 4 0 15 0 NMOS

* Load
RloadA 2 5 10
LloadA 5 6 10m
RloadB 3 6 10
LloadB 6 7 10m  
RloadC 4 7 10
LloadC 7 5 10m

* PWM Generation
VrefA 20 0 SIN(0 1 50 0 0 0)
VrefB 21 0 SIN(0 1 50 0 0 -120)
VrefC 22 0 SIN(0 1 50 0 0 -240)
Vcarrier 23 0 SIN(0 1 10k 0 0 0)

* Comparators
XcmpA 20 23 10 comparator
XcmpB 21 23 12 comparator  
XcmpC 22 23 14 comparator

* Inverted for low-side
XinvA 10 0 11 inverter
XinvB 12 0 13 inverter
XinvC 14 0 15 inverter

.model NMOS NMOS(Vto=4 Kp=1)

.subckt comparator 1 2 3
E1 3 0 TABLE {V(1)-V(2)} (-1,0) (1,5)
.ends

.subckt inverter 1 2 3
E1 3 0 TABLE {V(1,2)} (0,5) (5,0)
.ends

.TRAN 1u 40ms
.FOUR 50 V(2,3)
.END
```

### 3.4 Battery Management System (BMS) Project

#### Cell Balancing Simulation

**Specifications:**
- 4S Li-ion battery pack (16.8V max)
- Passive balancing: 100mA per cell
- Voltage monitoring: ±10mV accuracy
- Overvoltage: 4.20V/cell
- Undervoltage: 2.80V/cell

#### Simulation Model
```
* 4S Battery Pack with Balancing
* Battery Cells
B1 1 0 V=3.7
B2 2 1 V=3.7  
B3 3 2 V=3.7
B4 4 3 V=3.7

* Internal Resistance
R1 1 5 0.05
R2 2 6 0.05
R3 3 7 0.05  
R4 4 8 0.05

* Balancing Loads
Rbal1 5 9 40
Rbal2 6 9 40
Rbal3 7 9 40
Rbal4 8 9 40

* Balancing Control
Xcomp1 5 9 10 comparator(4.15)
Xcomp2 6 9 11 comparator(4.15)
Xcomp3 7 9 12 comparator(4.15)
Xcomp4 8 9 13 comparator(4.15)

* Balancing Switches
S1 5 14 10 0 NMOS
S2 6 14 11 0 NMOS
S3 7 14 12 0 NMOS
S4 8 14 13 0 NMOS

* Load
Rload 9 0 10

.model NMOS NMOS(Vto=2.5 Kp=0.1)

.subckt comparator thresh 1 2 3
E1 3 0 TABLE {V(1)-V(thresh)} (-1,0) (1,5)
.ends

.TRAN 1 3600
.END
```

---

## 4. Control & Instrumentation Projects

### 4.1 PID Controller Project

#### Digital PID Implementation

**Specifications:**
- Sampling: 1kHz
- Input: 0-3.3V
- Output: PWM, 0-100%
- Tuning: Ziegler-Nichols
- Anti-windup: Back calculation

#### Discrete PID Algorithm
```
// Position form
u[k] = Kp * e[k] + Ki * Ts * sum(e[j]) + Kd * (e[k] - e[k-1])/Ts

// Velocity form  
Δu[k] = Kp * (e[k] - e[k-1]) + Ki * Ts * e[k] + Kd * (e[k] - 2e[k-1] + e[k-2])/Ts
```

#### SPICE Behavioral Model
```
* Digital PID Controller
* Plant Model (First Order)
Vset 1 0 PULSE(0 1 10m 1m 1m 100m 200m)
Eplant 2 0 LAPLACE {V(3)} {1/(0.1*s+1)}

* PID Controller (Behavioral)
Kp=2.0 Ki=5.0 Kd=0.1 Ts=1m
Berror 4 0 V=V(1)-V(2)
Bintegral 5 0 V= V(5) + V(4)*{Ki*Ts} 
Bderivative 6 0 V= (V(4)-V(7))*{Kd/Ts}
Bcontrol 3 0 V= V(4)*{Kp} + V(5) + V(6)
Bdelay 7 0 V= delay(V(4),{Ts})

* Anti-windup (Clamping)
Blimit 8 0 V= limit(V(3),0,5)
Bsat 9 0 V= V(3)-V(8)
Bclamp 10 0 V= V(5) - {1/Ki}*V(9)

.TRAN 0.1m 200m
.END
```

### 4.2 Temperature Control System

#### PID Temperature Controller

**Specifications:**
- Sensor: PT100 RTD
- Range: 0-200°C
- Control: PWM heater
- Accuracy: ±1°C
- Sampling: 10Hz

#### Complete System Simulation
```
* Temperature Control System
* Temperature Setpoint
Vset 1 0 PULSE(20 100 10 1 1 50 100)

* Plant Model (Thermal Mass + Heater)
Cheat 2 0 1000
Rloss 2 0 10
Iheat 0 2 V={V(4)/10}  ; Heater power

* Sensor (PT100 Model)
Rsense 2 3 100
Rtemp 3 0 V={100 + 0.385*V(2)}  ; PT100: 100Ω at 0°C, 0.385Ω/°C

* Signal Conditioning
Vexcite 5 0 1
Rref 5 6 100
Xamp 6 3 7 instamp

* PID Controller
Kp=5.0 Ki=0.1 Kd=1.0
Berror 8 0 V=V(1)-V(7)
Bintegral 9 0 V= V(9) + V(8)*{Ki*0.1}
Bderivative 10 0 V= (V(8)-V(11))*{Kd/0.1}  
Bpid 4 0 V= V(8)*{Kp} + V(9) + V(10)
Bdelay 11 0 V= delay(V(8),0.1)

* PWM Output
Vcarrier 12 0 PULSE(0 5 0 1m 1m 49m 100m)
Xpwm 4 12 13 comparator

.subckt instamp 1 2 3
Rin 1 2 1G
E1 3 0 1 2 100
.ends

.subckt comparator 1 2 3
E1 3 0 TABLE {V(1)-V(2)} (-1,0) (1,5)
.ends

.TRAN 0.1 200
.END
```

### 4.3 Motor Speed Control Project

#### DC Motor PID Control

**Specifications:**
- Motor: 12V DC, 3000 RPM
- Load: 0.01 N·m·s² inertia
- Sensor: Optical encoder, 1000 PPR
- Control: PWM, 20kHz
- Response: <100ms settling time

#### Motor Model
```
Electrical: V = R·i + L·di/dt + Kb·ω
Mechanical: J·dω/dt + B·ω = Kt·i - τ_load
```

#### Complete Simulation
```
* DC Motor Speed Control
* Motor Electrical
Rarm 1 2 2
Larm 2 3 10m
Bbackemf 3 0 V={0.05*V(10)}  ; Kb = 0.05 V/(rad/s)

* Motor Mechanical  
Jrotor 10 0 0.01
Bfriction 10 0 0.001
Btorque 0 10 I={0.05*I(Varm)}  ; Kt = 0.05 N·m/A

* Load
Vload 11 0 PULSE(0 0.1 500m 10m 10m 100m 1)
Bload 10 0 I={V(11)}

* PWM Driver
Vpwm 4 0 PULSE(0 12 0 1u 1u 24u 50u)
S1 1 4 5 0 NMOS

* Speed Sensor
Bspeed 6 0 V={V(10)*60/(2*pi)}  ; Convert to RPM
Bencoder 7 0 V= {1000*V(10)/(2*pi)}  ; 1000 PPR

* PID Controller (RPM)
Vset 8 0 1500  ; 1500 RPM setpoint
Kp=0.01 Ki=0.1 Kd=0.001
Berror 9 0 V=V(8)-V(6)
Bintegral 12 0 V= V(12) + V(9)*{Ki*50u}
Bderivative 13 0 V= (V(9)-V(14))*{Kd/50u}
Bpid 5 0 V= V(9)*{Kp} + V(12) + V(13)
Bdelay 14 0 V= delay(V(9),50u)

.model NMOS NMOS(Vto=2.5 Kp=1)

.TRAN 10u 1
.END
```

### 4.4 Data Acquisition System Project

#### 8-Channel DAQ System

**Specifications:**
- Channels: 8 differential
- Resolution: 16 bits
- Sampling: 100kS/s total
- Input: ±10V
- Interface: SPI

#### System Simulation
```
* 8-Channel Data Acquisition System
* Analog Inputs
Vch1 1 0 SIN(1 2 1k)
Vch2 2 0 SIN(2 1.5 800)
Vch3 3 0 SIN(3 1 1200)
Vch4 4 0 SIN(4 0.8 1500)
Vch5 5 0 SIN(5 1.2 2000)
Vch6 6 0 SIN(6 0.9 2500)
Vch7 7 0 SIN(7 1.1 3000)
Vch8 8 0 SIN(8 1.3 3500)

* Multiplexer
S1 1 9 10 0 SW
S2 2 9 11 0 SW
S3 3 9 12 0 SW
S4 4 9 13 0 SW
S5 5 9 14 0 SW
S6 6 9 15 0 SW
S7 7 9 16 0 SW
S8 8 9 17 0 SW

* Control Logic
Vclk 18 0 PULSE(0 5 0 1u 1u 4u 10u)
Bcounter 19 0 V= floor(time/10u) % 8
Bdecode 20 0 V= bit(V(19),0)
Bdecode 21 0 V= bit(V(19),1)
Bdecode 22 0 V= bit(V(19),2)

* ADC Model
Vref 23 0 10
Badc 24 0 V= floor((V(9)+10)/20*65536)  ; 16-bit conversion

* SPI Output
Bspi 25 0 V= bit(V(24),15)*V(18)  ; MSB first
Bspi 26 0 V= bit(V(24),14)*V(18)
Bspi 27 0 V= bit(V(24),13)*V(18)
Bspi 28 0 V= bit(V(24),12)*V(18)
Bspi 29 0 V= bit(V(24),11)*V(18)
Bspi 30 0 V= bit(V(24),10)*V(18)
Bspi 31 0 V= bit(V(24),9)*V(18)
Bspi 32 0 V= bit(V(24),8)*V(18)
Bspi 33 0 V= bit(V(24),7)*V(18)
Bspi 34 0 V= bit(V(24),6)*V(18)
Bspi 35 0 V= bit(V(24),5)*V(18)
Bspi 36 0 V= bit(V(24),4)*V(18)
Bspi 37 0 V= bit(V(24),3)*V(18)
Bspi 38 0 V= bit(V(24),2)*V(18)
Bspi 39 0 V= bit(V(24),1)*V(18)
Bspi 40 0 V= bit(V(24),0)*V(18)

.model SW SW(Ron=100 Roff=1Meg Vt=2.5)

.TRAN 1u 100u
.END
```

### 4.5 Advanced Project: Digital Lock-In Amplifier

#### Lock-in Amplifier Principles

**Specifications:**
- Frequency: 1Hz - 100kHz
- Dynamic Reserve: 100dB
- Reference: Internal/external
- Output: R, θ, X, Y
- Time Constant: 10μs - 100ks

#### Implementation
```
* Digital Lock-In Amplifier
* Signal Input
Vsig 1 0 SIN(0 100u 1k)  ; Small signal at 1kHz
Vnoise 2 0 SIN(0 10m 60)  ; 60Hz interference
Vsum 3 0 V=V(1)+V(2)      ; Signal + noise

* Reference Oscillator
Vref 4 0 SIN(0 1 1k 0 0 0)  ; 1kHz reference

* Phase Shifter
Vref90 5 0 SIN(0 1 1k 0 0 90)  ; 90° phase shift

* Multipliers (Mixers)
BmixI 6 0 V=V(3)*V(4)     ; In-phase multiplier
BmixQ 7 0 V=V(3)*V(5)     ; Quadrature multiplier

* Low-Pass Filters (Integrators)
R1 6 8 10k
C1 8 0 1u
R2 7 9 10k
C2 9 0 1u

* Output Calculations
Bmagnitude 10 0 V= sqrt(V(8)*V(8) + V(9)*V(9))  ; R
Bphase 11 0 V= atan2(V(9), V(8))*180/pi         ; θ
Binphase 12 0 V= V(8)                           ; X
Bquad 13 0 V= V(9)                              ; Y

.TRAN 1u 10m
.END
```

---

## Practice Problems

### Problem 1: SPICE Amplifier Design
```
Design and simulate a two-stage operational amplifier with:
- DC gain > 80dB
- Unity gain bandwidth > 10MHz
- Phase margin > 60°
- Supply: ±15V
- Load: 10pF || 10kΩ

Provide complete netlist and performance analysis.
```

### Problem 2: Power Supply Design
```
Design a flyback converter with:
- Input: 85-265V AC, 50/60Hz
- Output: 12V DC, 2A
- Isolation: 3000V
- Efficiency: >85%

Simulate including transformer model and feedback loop.
```

### Problem 3: Motor Control System
```
Design a brushless DC motor controller with:
- Sensorless position detection
- Field-oriented control
- Speed range: 100-5000 RPM
- Current limiting

Provide complete simulation with mechanical load.
```

### Problem 4: Instrumentation System
```
Design a complete data acquisition system with:
- 8 differential channels
- 24-bit ADC
- Programmable gain: 1-1000
- Digital filtering
- SPI interface

Simulate signal chain from sensor to digital output.
```

### Problem 5: Control System Design
```
Design a temperature control system for:
- Range: -40°C to +125°C
- Accuracy: ±0.1°C
- Heating/cooling control
- PID with auto-tuning

Include thermal plant model and complete control loop.
```

## Conclusion

This comprehensive projects and simulations course provides practical experience with real-world electronic system design and analysis. Each project builds upon theoretical concepts to develop engineering intuition and problem-solving skills.

Key learning outcomes:
- SPICE simulation proficiency for circuit verification and optimization
- Complete system design from specifications to implementation
- Integration of analog, digital, and power electronics
- Control system design and stability analysis
- Practical considerations for manufacturability and reliability

These projects form the foundation for advanced electronic design and provide valuable experience for academic studies, research, and professional engineering careers. The simulation skills developed here are directly applicable to industry-standard design workflows.
