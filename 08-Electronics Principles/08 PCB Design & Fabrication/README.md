<h1 align="center">PCB Design & Fabrication</h1>

## Table of Contents
1. [Schematic Design](#1-schematic-design)
2. [Layout Rules](#2-layout-rules)
3. [Grounding & Power Distribution](#3-grounding--power-distribution)
4. [Manufacturing & Assembly](#4-manufacturing--assembly)

---

## 1. Schematic Design

### 1.1 Schematic Capture Fundamentals

#### What is a Schematic?
A symbolic representation of an electronic circuit using standardized symbols and conventions.

#### Schematic Hierarchy
```
Top Level Schematic
    ├── Power Supply Module
    ├── Microcontroller Module
    ├── Sensor Interface Module
    └── Communication Module
```

#### Basic Schematic Symbols

**Passive Components:**
```
Resistor: ───╔╡╟─── or ───[R]───
Capacitor: ───| |─── (non-polarized) or ───| |─── (polarized)
Inductor: ───͡ ͡─── or ───(L)───
```

**Active Components:**
```
Transistor (NPN): 
     Collector
        │
        │
        ○
        │
      Base
        │
        │
        ○
        │
     Emitter

Op-Amp:
      V+ ──┐
           │
          ┌┴┐
       ─→│  ├─→ Output
          └┬┘
           │
      V- ──┘
```

### 1.2 Schematic Organization Best Practices

#### Sheet Organization
```
Main Sheet (Sheet 1)
├── Power Distribution
├── Microcontroller Core
├── Peripheral Interfaces
└── Connectors

Sub-sheets:
- Power_Supply.sch
- MCU_Circuit.sch
- Sensor_Inputs.sch
- Output_Drivers.sch
```

#### Net Naming Conventions
```
Power Nets:
- VCC_3V3, VCC_5V, VCC_12V
- GND, AGND, DGND

Signal Nets:
- SPI_MOSI, SPI_MISO, SPI_SCK, SPI_CS
- I2C_SDA, I2C_SCL
- UART_TX, UART_RX

Bus Nets:
- DATA[0:7], ADDR[0:15]
```

### 1.3 Component Selection and Management

#### Component Libraries
```
Library Structure:
├── Company_Standard.lib
│   ├── Passives
│   ├── Integrated_Circuits
│   ├── Connectors
│   └── Mechanical
├── Manufacturer_Libraries
└── Custom_Parts.lib
```

#### Component Parameters
```
Required Fields:
- Reference Designator (R1, C5, U3)
- Value (10k, 0.1uF, LM358)
- Footprint (0805, SOIC-8, QFP-44)
- Manufacturer Part Number
- Description

Optional Fields:
- Voltage Rating
- Power Rating
- Temperature Coefficient
- Supplier Information
```

### 1.4 Design Rule Checking (DRC)

#### Electrical Rules Check
```
Common ERC Checks:
- Unconnected pins
- Multiple net names on same net
- Power pin conflicts
- Input pins floating
- Output pins shorted
- Drive conflicts
```

#### Connectivity Verification
```
Net Connectivity:
- Verify all nets have proper sources and loads
- Check for unintentional open circuits
- Verify power and ground connections
```

### 1.5 Schematic Documentation

#### Annotation and Notes
```
Title Block:
- Project Name
- Revision Number
- Date
- Designer Name
- Company Information
- Sheet Number (X of Y)

Notes Section:
- Special instructions
- Test points
- Configuration options
- Design assumptions
```

#### Design Revisions
```
Revision History:
v1.0 - Initial release
v1.1 - Added filter capacitors
v1.2 - Changed crystal oscillator configuration
v1.3 - Updated connector pinout
```

### 1.6 Practical Schematic Example

#### Arduino-Compatible Microcontroller Section
```
Power Section:
     ┌─────┐    ┌─────┐    ┌─────┐
USB →│ 5V  ├──→│ LDO ├──→│ 3V3  ├──→ VCC_3V3
     └─────┘    └─────┘    └─────┘

Microcontroller:
     ┌─────────────────┐
     │   ATMEGA328P    │
     │                 │
VCC ─┤ VCC         PC5 ├─→ A0
     │             PC4 ├─→ A1
GND ─┤ GND         PC3 ├─→ A2
     │             PC2 ├─→ A3
     │             PC1 ├─→ A4 (SDA)
     │             PC0 ├─→ A5 (SCL)
     │             PD7 ├─→ D7
     │             PD6 ├─→ D6
     │             PD5 ├─→ D5 (PWM)
     │             PD4 ├─→ D4
     │             PD3 ├─→ D3 (PWM)
     │             PD2 ├─→ D2 (INT)
     │             PD1 ├─→ D1 (TX)
     │             PD0 ├─→ D0 (RX)
     │             PB5 ├─→ D13 (SCK)
     │             PB4 ├─→ D12 (MISO)
     │             PB3 ├─→ D11 (MOSI)
     │             PB2 ├─→ D10 (SS)
     │             PB1 ├─→ D9 (PWM)
     │             PB0 ├─→ D8
     └─────────────────┘

Crystal Circuit:
     ┌───┐    ┌───┐
     │16 │    │16 │
     │MHz│    │MHz│
     └─┬─┘    └─┬─┘
       │        │
XTAL1 ─┴─ 22pF  └─ 22pF ─┐
       │        │        │
      GND      GND      GND
```

---

## 2. Layout Rules

### 2.1 PCB Stackup Design

#### Common Layer Stackups

**2-Layer Board:**
```
Top Layer: Components + Signals
Core
Bottom Layer: Signals + Ground Pour
```

**4-Layer Board:**
```
Top Layer: Components + Signals
Prepreg
Inner Layer 1: Ground Plane
Core
Inner Layer 2: Power Plane
Prepreg
Bottom Layer: Signals
```

**6-Layer Board:**
```
Top Layer: Components + Signals
Prepreg
Inner Layer 1: Ground Plane
Core
Inner Layer 2: Signals
Prepreg
Inner Layer 3: Power Plane
Core
Inner Layer 4: Signals
Prepreg
Bottom Layer: Signals
```

#### Impedance Control

**Microstrip (Surface Trace):**
```
Z₀ = (87/√(ε_r+1.41)) × ln(5.98H/(0.8W+T))
Where:
Z₀ = Characteristic impedance
ε_r = Dielectric constant
H = Height to reference plane
W = Trace width
T = Trace thickness
```

**Stripline (Internal Trace):**
```
Z₀ = (60/√ε_r) × ln(4H/(0.67πW(0.8+T/W)))
```

### 2.2 Component Placement

#### Placement Strategy

**Functional Grouping:**
```
Power Section:
├── Input Connector
├── Filter Capacitors
├── Voltage Regulator
├── Output Capacitors
└── Output Connector

Digital Section:
├── Microcontroller
├── Crystal
├── Decoupling Capacitors
├── Programming Interface
└── Supporting Logic

Analog Section:
├── Sensors
├── Op-Amps
├── Filter Components
└── Shielded Areas
```

#### Placement Rules

**General Guidelines:**
- Group related components together
- Minimize trace lengths for high-speed signals
- Place decoupling capacitors close to IC power pins
- Consider thermal management during placement
- Allow space for test points and rework

**Orientation:**
- Place similar components in same orientation
- Polarized components should face same direction
- Consider automated assembly requirements

### 2.3 Routing Guidelines

#### Trace Width Calculations

**Current Carrying Capacity:**
```
I = k × ΔT^0.44 × A^0.725
Where:
I = Current (amps)
k = 0.024 for inner layers, 0.048 for outer layers
ΔT = Temperature rise (°C)
A = Cross-sectional area (mils²)
```

**Practical Trace Widths:**
```
Signal traces: 6-10 mil (0.15-0.25mm)
Power traces: 
- 1A: 10-20 mil
- 2A: 20-40 mil  
- 5A: 80-100 mil
- 10A: 200+ mil
```

#### Clearance Rules

**Basic Clearances:**
```
Trace to trace: 6 mil (0.15mm)
Trace to pad: 8 mil (0.20mm)
Pad to pad: 8 mil (0.20mm)
Copper to board edge: 20 mil (0.50mm)
```

**High Voltage Clearances:**
```
Voltage    Clearance
≤30V       8 mil
30-150V    15 mil
150-300V   25 mil
300-600V   50 mil
```

### 2.4 High-Speed Design Rules

#### Signal Integrity

**Transmission Line Effects:**
- Consider when: Trace length > (1/6) × (rise time / propagation delay)
- Typical: Traces longer than 1-2 inches for fast digital signals

**Controlled Impedance:**
- Match trace impedance to source and load
- Common values: 50Ω single-ended, 100Ω differential

#### Differential Pairs

**Routing Requirements:**
```
     ┌───┐   ┌───┐
P ───┤   ├─→ │   ├─→
     │   │   │   │
N ───┤   ├─→ │   ├─→
     └───┘   └───┘
```
- Maintain constant spacing (coupling)
- Equal length matching (phase matching)
- Route together from source to destination

#### Length Matching

**Timing Constraints:**
```
Maximum length mismatch = (timing skew) / (propagation delay)

Example: 
Timing budget: 50ps
Propagation delay: 150ps/inch
Max mismatch = 50ps / 150ps/inch = 0.33 inches
```

### 2.5 Design Rule Check (DRC)

#### Manufacturing DRC Rules

**Standard Rules Set:**
```
Minimum trace width: 6 mil
Minimum clearance: 6 mil
Minimum hole size: 8 mil
Minimum annular ring: 4 mil
Copper to edge: 20 mil
Solder mask sliver: 4 mil
```

**Advanced Rules:**
- Differential pair spacing
- Length matching tolerances
- Impedance control parameters
- Via-in-pad restrictions

#### Electrical Rule Check

**Common Electrical Rules:**
- Unconnected nets
- Short circuits
- Stubs (unterminated traces)
- Acute angles (<90°)
- Copper islands

### 2.6 Design for Manufacturing (DFM)

#### Panelization

**Board Array:**
```
┌───┬───┬───┬───┐
│   │   │   │   │
│ A │ A │ A │ A │
│   │   │   │   │
├───┼───┼───┼───┤
│   │   │   │   │
│ A │ A │ A │ A │
│   │   │   │   │
└───┴───┴───┴───┘
```

**Breakaway Tabs:**
- V-score (30% depth from each side)
- Mouse bites (small drilled holes)
- Tab routs (routed slots with small connections)

#### Fiducial Marks
```
Global Fiducials: Board corners
Local Fiducials: For fine-pitch components
Pattern: 
     ┌───┐
     │ ○ │  Copper circle with solder mask opening
     └───┘
```

---

## 3. Grounding & Power Distribution

### 3.1 Grounding Strategies

#### Ground System Types

**Single-Point Ground:**
```
        ┌───┐   ┌───┐   ┌───┐
Analog ─┤   │   │   │   │   ├─→ AGND
        └───┘   └───┘   └───┘
                          │
        ┌───┐   ┌───┐   ┌───┐      │
Digital ┤   │   │   │   │   ├─→ DGND ─→ System GND
        └───┘   └───┘   └───┘      │
                          │
        ┌───┐   ┌───┐   ┌───┐
Power ──┤   │   │   │   │   ├─→ PGND
        └───┘   └───┘   └───┘
```

**Multi-Point Ground:**
```
        ┌───┐   ┌───┐   ┌───┐
Analog ─┤   │   │   │   │   │
        └─┬─┘   └─┬─┘   └─┬─┘
          │       │       │
        ┌─┴───────┴───────┴─┐
        │    Ground Plane   │
        └───────────────────┘
```

#### Ground Plane Implementation

**Solid Ground Plane:**
- Provides lowest impedance return path
- Reduces electromagnetic interference
- Improves signal integrity
- Acts as heat spreader

**Split Ground Planes:**
```
┌─────────────────┐
│   Analog Ground │
├─────────────────┤
│   Digital Ground│
└─────────────────┘
```

**Connection Rules:**
- Connect split planes at single point
- Use 0Ω resistor or ferrite bead for isolation
- Keep analog and digital returns separate

### 3.2 Power Distribution Network (PDN)

#### PDN Impedance Target
```
Z_target = (V_noise_max) / (ΔI_max)

Example:
V_noise_max = 50mV
ΔI_max = 1A
Z_target = 50mΩ
```

#### Decoupling Strategy

**Multi-stage Decoupling:**
```
IC Power Pin
  │
  ├─ 0.1μF ceramic (0402/0603) ← High frequency
  ├─ 1μF ceramic (0603/0805)   ← Medium frequency  
  ├─ 10μF ceramic (0805/1206)  ← Low frequency
  └─ 100μF electrolytic        ← Bulk storage
```

**Placement Rules:**
- Smallest capacitors closest to IC pins
- Place on same layer as IC when possible
- Use multiple vias for low inductance
- Keep loop area small

#### Power Plane Design

**Solid Power Planes:**
- Lowest impedance distribution
- Good for digital circuits
- May require multiple voltages

**Power Routing:**
- Use wide traces for high current
- Star distribution for analog circuits
- Consider voltage drop calculations

### 3.3 Bypass Capacitor Selection

#### Capacitor Types and Applications

**Ceramic Capacitors:**
- **X7R:** General purpose, stable
- **X5R:** Higher capacitance, some variance
- **C0G/NP0:** High precision, stable

**Electrolytic Capacitors:**
- **Aluminum:** High capacitance, polarized
- **Tantalum:** High density, reliable

#### Capacitor Frequency Response

**Impedance vs Frequency:**
```
Impedance
   ↑
   |‾‾‾‾‾‾‾‾⎯⎯⎯⎯⎯⎯⎯
   |         ⎯⎯⎯⎯⎯⎯⎯⎯⎯
   |               ⎯⎯⎯⎯⎯⎯⎯⎯⎯
   +-----------------------→ Frequency
        SRF
```

**Self-Resonant Frequency (SRF):**
```
SRF = 1 / (2π√(LC))
Where L includes ESL (Equivalent Series Inductance)
```

#### Practical Decoupling Scheme

**For Digital IC:**
```
VCC Pin → 0.1μF (0402) → 1μF (0603) → 10μF (0805) → Bulk
Distance: < 2mm    < 5mm     < 10mm     < 20mm
```

### 3.4 Power Supply Routing

#### Voltage Regulator Layout

**Linear Regulator:**
```
     ┌─────────┐
Vin ─┤         ├─ Vout
     │   LDO   │
     │         │
GND ─┤         │
     └─────────┘

Critical components:
- Input capacitor: Close to Vin pin
- Output capacitor: Close to Vout pin
- Ground connections: Solid to ground plane
```

**Switching Regulator:**
```
     ┌─────────┐
Vin ─┤         ├─ Vout
     │   SMPS  │
     │         │
GND ─┤         │
     └─────────┘

Critical components:
- Input capacitors: High-frequency and bulk
- Inductor: Close to switch node
- Output capacitors: Multiple in parallel
- Feedback network: Away from noise sources
```

#### Current Path Analysis

**High Current Loops:**
```
Switch Mode Power Supply:
Input Cap → Switch → Inductor → Output Cap → Load
    │                                      │
    └──────────────────────────────────────┘

Keep this loop as small as possible!
```

### 3.5 Mixed-Signal Grounding

#### Analog-Digital Separation

**Partitioning Strategy:**
```
┌─────────────────────────────────┐
│        Analog Section           │
│  ┌───┐  ┌───┐  ┌───┐           │
│  │   │  │   │  │   │           │
│  └───┘  └───┘  └───┘           │
│                                 │
├─────────────────────────────────┤
│        Digital Section          │
│  ┌───┐  ┌───┐  ┌───┐  ┌───┐    │
│  │   │  │   │  │   │  │   │    │
│  └───┘  └───┘  └───┘  └───┘    │
└─────────────────────────────────┘
```

**ADC Grounding:**
- Place ADC at the boundary
- Use single ground connection under ADC
- Separate analog and digital power supplies
- Ferrite beads for power isolation

#### Shielded Cables and Connectors

**Cable Shield Connection:**
- Connect shield to chassis ground at one end
- Use low-inductance connection
- Consider RF gaskets for high frequency

---

## 4. Manufacturing & Assembly

### 4.1 PCB Fabrication Process

#### Manufacturing Steps

**1. Material Preparation:**
- Cut copper-clad laminate to size
- Clean and prepare surface

**2. Imaging:**
- Apply photoresist
- Expose with UV light through film
- Develop to remove unexposed resist

**3. Etching:**
- Chemical etching removes unwanted copper
- Ammonium persulfate or ferric chloride

**4. Drilling:**
- CNC drilling of holes
- Mechanical drills for larger holes
- Laser drilling for microvias

**5. Plating:**
- Electroless copper deposition
- Electrolytic copper plating
- Surface finish application

**6. Solder Mask:**
- Apply epoxy-based solder mask
- Expose and develop
- Cure in oven

**7. Silkscreen:**
- Apply component designators
- Add logos and markings
- Cure

**8. Testing:**
- Electrical test (flying probe or fixture)
- Visual inspection
- Impedance testing (if controlled)

### 4.2 Design for Manufacturing (DFM)

#### Panelization Design

**Board Array:**
```
┌───┬───┬───┬───┐
│   │   │   │   │
│ A │ A │ A │ A │
│   │   │   │   │
├───┼───┼───┼───┤
│   │   │   │   │
│ A │ A │ A │ A │
│   │   │   │   │
└───┴───┴───┴───┘
```

**Panel Clearances:**
- Board to board: 3mm minimum
- Tooling strip: 5mm minimum
- Fiducial clearance: 3mm diameter

#### Copper Balance

**Importance:**
- Prevents board warpage
- Ensures even plating
- Improves yield

**Techniques:**
- Add copper thieving (non-connected copper)
- Balance copper distribution across layers
- Use copper pour on outer layers

### 4.3 Assembly Processes

#### Surface Mount Technology (SMT)

**SMT Assembly Steps:**
```
1. Solder Paste Application
   - Stencil printing
   - Solder paste inspection (SPI)

2. Component Placement
   - Pick and place machines
   - Vision alignment

3. Reflow Soldering
   - Preheat → Soak → Reflow → Cool
   - Temperature profiling critical

4. Inspection
   - Automated optical inspection (AOI)
   - X-ray inspection (for BGAs)
```

#### Through-Hole Technology (THT)

**THT Assembly Steps:**
```
1. Component Insertion
   - Manual or automated
   - Wave soldering preparation

2. Wave Soldering
   - Flux application → Preheat → Wave solder → Cool

3. Manual Soldering
   - For large components or rework
   - Hand soldering with iron
```

#### Mixed Technology

**Process Sequence:**
```
1. SMT bottom side
2. Reflow bottom side
3. SMT top side  
4. Reflow top side
5. Through-hole insertion
6. Wave or selective soldering
7. Cleaning and inspection
```

### 4.4 Design for Assembly (DFA)

#### Component Placement Guidelines

**Orientation and Spacing:**
```
All polarized components in same direction
Minimum spacing between components: 0.3mm
Clearance for pick-and-place nozzles
Avoid shadowing during reflow
```

**Footprint Design:**
```
SMD pads: 
- 0.1-0.2mm extension beyond component
- Proper solder mask definition
- Thermal relief for ground pads

Through-hole pads:
- Adequate annular ring (0.15mm minimum)
- Plated holes with proper diameter
```

#### Solder Mask Design

**Solder Mask Clearance:**
```
Pad to mask clearance: 0.05-0.1mm
Minimum mask web: 0.1mm
Tented vias: Mask over via holes
Solder mask dams between pins
```

**Solder Mask Types:**
- **LPI (Liquid Photoimageable):** High precision
- **Dry Film:** For fine features
- **Epoxy:** Low cost, lower resolution

### 4.5 Testing and Validation

#### Bare Board Testing

**Electrical Testing:**
- Continuity testing (opens)
- Isolation testing (shorts)
- Impedance testing (controlled impedance)
- Hi-pot testing (dielectric strength)

**Visual Inspection:**
- Copper quality
- Drill registration
- Solder mask coverage
- Silkscreen legibility

#### Assembled Board Testing

**In-Circuit Test (ICT):**
- Bed-of-nails fixture
- Tests individual components
- Verifies assembly correctness
- Requires test points access

**Functional Test:**
- Tests complete board functionality
- Simulates operating conditions
- Validates system performance
- May require custom test fixtures

#### Design for Test (DFT)

**Test Point Requirements:**
```
Access to:
- All power rails
- Reset signals
- Clock signals
- Communication buses (SPI, I2C, UART)
- Critical control signals

Test point spacing: 2.54mm (0.1") grid
Test point size: 1.0mm diameter minimum
```

### 4.6 Documentation and Outputs

#### Manufacturing Files

**Gerber Files:**
```
Required layers:
- Top copper (.GTL)
- Bottom copper (.GBL)
- Inner layers (.G1, .G2, ...)
- Top solder mask (.GTS)
- Bottom solder mask (.GBS)
- Top silkscreen (.GTO)
- Bottom silkscreen (.GBO)
- Board outline (.GKO or .GM1)
- Drill drawing (.GD1)
```

**Drill Files:**
- Excellon format (.TXT or .DRL)
- Contains hole sizes and locations
- Plated vs non-plated holes
- Tool change information

#### Additional Files

**Bill of Materials (BOM):**
```
Required columns:
- Quantity
- Reference Designator
- Manufacturer Part Number
- Description
- Value/Tolerance
- Package/Footprint
- Supplier
```

**Assembly Drawings:**
- Component locations
- Orientation markings
- Special instructions
- Board dimensions
- Revision information

**Pick and Place File:**
- Component centroids (X,Y)
- Rotation angles
- Side of board (Top/Bottom)
- Reference designators

### 4.7 Quality Standards

#### IPC Standards

**IPC-A-600:** Acceptability of Printed Boards
**IPC-A-610:** Acceptability of Electronic Assemblies
**IPC-2221:** Generic Standard on PCB Design
**IPC-7351:** Land Pattern Design

#### Class Definitions

**Class 1:** Consumer Electronics
- Focus on function
- Cosmetic imperfections allowed
- Lowest cost

**Class 2:** Industrial/Commercial
- Extended service life
- High reliability
- Some cosmetic requirements

**Class 3:** Military/Aerospace/Medical
- Continuous performance critical
- Zero defects expected
- Highest reliability requirements

### 4.8 Cost Optimization

#### Design Choices Affecting Cost

**Board Size:**
- Standard panel sizes most economical
- Minimize board area
- Consider panelization efficiency

**Layer Count:**
- Each additional layer increases cost
- Balance performance vs cost
- Consider buried vias vs through vias

**Materials:**
- FR-4 standard for most applications
- High-Tg FR-4 for lead-free assembly
- Special materials for high frequency

**Features:**
- Minimum trace/space
- Hole sizes and aspect ratios
- Impedance control requirements
- Special finishes (ENIG, immersion silver, etc.)

---

## Practice Problems

### Problem 1: Schematic Design
```
Design a schematic for a 5V to 3.3V power supply using an LDO regulator.
Include:
- Input protection (reverse polarity, overvoltage)
- Filtering capacitors
- Status LED
- Test points
Create the BOM with actual component part numbers.
```

### Problem 2: Layout Exercise
```
Given a 4-layer board with the following stackup:
Top - GND - POWER - Bottom

Place and route a microcontroller circuit with:
- 32-pin QFP microcontroller
- 16MHz crystal
- 4 LEDs with current-limiting resistors
- 2 push buttons
- UART connector
Apply proper grounding and decoupling techniques.
```

### Problem 3: Power Distribution
```
Design the power distribution for a board with:
- 12V input (2A max)
- 5V rail (1A max) 
- 3.3V rail (500mA max)
- 1.8V rail (200mA max)

Select appropriate regulators and calculate:
- Trace widths for each power rail
- Decoupling capacitor values and placement
- Total power consumption
```

### Problem 4: Manufacturing Files
```
Generate the complete manufacturing package for a simple 2-layer board including:
- Gerber files for all layers
- Drill file
- Assembly drawings
- Bill of Materials
- Pick and place file
Use industry-standard naming conventions.
```

### Problem 5: Design Review
```
Perform a design review on a provided PCB layout, checking for:
- DFM violations
- DRC errors
- Signal integrity issues
- Power distribution problems
- Thermal considerations
Provide specific recommendations for improvement.
```

## Conclusion

This comprehensive PCB design and fabrication course covers the entire process from schematic creation to manufacturing and assembly. Each section builds upon fundamental principles to provide practical knowledge for designing reliable, manufacturable printed circuit boards.

Key takeaways:
- Proper schematic design is the foundation of successful PCB layout
- Layout rules ensure manufacturability and signal integrity
- Grounding and power distribution are critical for system performance
- Understanding manufacturing processes enables cost-effective designs

PCB design continues to evolve with higher speeds, smaller components, and more complex requirements. Modern design tools and manufacturing capabilities enable increasingly sophisticated electronic systems, but the fundamental principles covered in this course remain essential for successful PCB design.
