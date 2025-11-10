<h1 align="center">Signal Processing</h1>

## Table of Contents
1. [Analog Filters](#1-analog-filters)
2. [Sampling & Quantization](#2-sampling--quantization)
3. [FFT & Frequency Analysis](#3-fft--frequency-analysis)
4. [DSP Fundamentals](#4-dsp-fundamentals)

---

## 1. Analog Filters

### 1.1 Filter Fundamentals

#### What is a Filter?
A system that modifies the frequency content of a signal by allowing certain frequency components to pass while attenuating others.

#### Filter Classification

**By Frequency Response:**
- **Low-Pass Filter (LPF):** Passes low frequencies, attenuates high frequencies
- **High-Pass Filter (HPF):** Passes high frequencies, attenuates low frequencies
- **Band-Pass Filter (BPF):** Passes a specific frequency band
- **Band-Stop Filter (BSF):** Attenuates a specific frequency band

**By Implementation:**
- **Passive Filters:** Use resistors, capacitors, inductors
- **Active Filters:** Use op-amps with resistors and capacitors

### 1.2 Transfer Function Analysis

#### General Form of Transfer Function
```
H(s) = V_out(s) / V_in(s) = N(s) / D(s)
where s = σ + jω (complex frequency)
```

#### Magnitude and Phase Response
```
|H(jω)| = Magnitude response
∠H(jω) = Phase response
```

#### Decibel Scale
```
Gain in dB = 20 log₁₀(|H(jω)|)
```

### 1.3 First-Order Filters

#### Passive RC Low-Pass Filter

**Circuit:**
```
     ┌──[R]──┐
     │       │
V_in─┴──────┴─ V_out
           │
          [C]
           │
          GND
```

**Transfer Function:**
```
H(s) = 1 / (1 + sRC)
```

**Frequency Response:**
```
Cutoff frequency: ω_c = 1/(RC)
|H(jω)| = 1 / √(1 + (ω/ω_c)²)
∠H(jω) = -arctan(ω/ω_c)
```

**Bode Plot:**
```
Magnitude (dB)
  0 │‾‾‾‾‾‾‾‾⎯⎯⎯⎯⎯⎯
-20 │         ⎯⎯⎯⎯⎯⎯⎯⎯⎯
    │               ⎯⎯⎯⎯⎯⎯
    +--------------→ log(ω)
        ω_c

Phase (degrees)
  0 │
-45 │       ‾‾‾‾⎯⎯⎯⎯⎯
-90 │‾‾‾‾‾‾‾⎯
    +--------------→ log(ω)
        ω_c
```

#### Passive RC High-Pass Filter

**Circuit:**
```
     ┌──[C]──┐
     │       │
V_in─┴──────┴─ V_out
           │
          [R]
           │
          GND
```

**Transfer Function:**
```
H(s) = sRC / (1 + sRC)
```

**Frequency Response:**
```
Cutoff frequency: ω_c = 1/(RC)
|H(jω)| = (ω/ω_c) / √(1 + (ω/ω_c)²)
∠H(jω) = 90° - arctan(ω/ω_c)
```

### 1.4 Second-Order Filters

#### General Second-Order Transfer Function
```
H(s) = ω₀² / (s² + (ω₀/Q)s + ω₀²)
where:
ω₀ = resonant frequency (rad/s)
Q = quality factor
```

#### Quality Factor (Q) Effects
- **Low Q (Q < 0.5):** Overdamped, no peaking
- **Critical damping (Q = 0.5):** Fastest response without overshoot
- **High Q (Q > 0.5):** Underdamped, peaking in frequency response

#### RLC Series Resonant Circuit

**Circuit:**
```
     ┌──[R]──[L]──[C]──┐
     │                 │
V_in─┴─────────────────┴─ V_out
                       │
                      GND
```

**Transfer Function:**
```
H(s) = 1 / (s²LC + sRC + 1)
ω₀ = 1/√(LC)
Q = (1/R)√(L/C)
```

### 1.5 Active Filters

#### Sallen-Key Topology

**Low-Pass Sallen-Key:**
```
     V_in─[R1]─┬─[R2]─┐
               │      │
              [C1]    ├─ V_out
               │      │
              GND    [C2]
                     │
                    GND
     with op-amp buffer
```

**Transfer Function:**
```
H(s) = K / (s² + s(1/R₁C₁ + 1/R₂C₁ + (1-K)/R₂C₂) + 1/R₁R₂C₁C₂)
where K = 1 + R₃/R₄ (gain)
```

#### Butterworth Filter

**Characteristics:**
- Maximally flat passband
- Moderate roll-off rate
- No ripple in passband or stopband

**n-th Order Butterworth Magnitude Response:**
```
|H(jω)| = 1 / √(1 + (ω/ω_c)²ⁿ)
```

**Pole Locations:**
Equally spaced on left half of unit circle in s-plane

**Design Example: 2nd Order Butterworth LPF**
```
Poles at: s = -ω_c(1 ± j)/√2
Components: R1 = R2 = R, C1 = C2 = C
ω_c = 1/(RC)
Q = 1/√2 ≈ 0.707
```

#### Chebyshev Filter

**Characteristics:**
- Equiripple in passband
- Steeper roll-off than Butterworth
- Ripple amplitude determined by ε

**Magnitude Response:**
```
|H(jω)| = 1 / √(1 + ε²C_n²(ω/ω_c))
where C_n = Chebyshev polynomial of order n
```

#### Bessel Filter

**Characteristics:**
- Maximally flat group delay
- Linear phase response in passband
- Gradual roll-off

### 1.6 Filter Design Procedure

#### Design Steps:
1. **Specifications:**
   - Passband frequency (f_p)
   - Stopband frequency (f_s)
   - Passband ripple (A_p dB)
   - Stopband attenuation (A_s dB)

2. **Filter Order Calculation:**
   ```
   For Butterworth: n ≥ log[(10^(A_s/10) - 1)/(10^(A_p/10) - 1)] / [2 log(ω_s/ω_p)]
   ```

3. **Component Selection**
4. **Implementation**

#### Design Example: Audio Low-Pass Filter
```
Requirements:
- Cutoff frequency: 20kHz
- Stopband: 40kHz with 40dB attenuation
- Butterworth response

Calculation:
f_c = 20kHz, f_s = 40kHz
A_s = 40dB at f_s

n ≥ log[(10^(40/10) - 1)/(10^(3/10) - 1)] / [2 log(40k/20k)]
  ≥ log[(10000 - 1)/(2 - 1)] / [2 log(2)]
  ≥ log(9999) / (2 × 0.301) ≈ 4/0.602 ≈ 6.64

Use n = 7 (7th order Butterworth)
```

---

## 2. Sampling & Quantization

### 2.1 Sampling Theorem

#### Nyquist-Shannon Sampling Theorem
> A continuous-time signal can be completely recovered from its samples if the sampling frequency is at least twice the highest frequency component in the signal.

**Mathematically:**
```
f_s ≥ 2f_max
where:
f_s = sampling frequency
f_max = highest frequency in signal
```

#### Aliasing
**What is Aliasing?**
When f_s < 2f_max, higher frequencies appear as lower frequencies in the sampled signal.

**Aliasing Demonstration:**
```
Original: 7kHz sine wave
Sampled at: 10kHz
Appears as: 3kHz sine wave (10kHz - 7kHz)
```

#### Anti-Aliasing Filter
A low-pass filter placed before sampling to ensure f_max < f_s/2

**Specifications:**
- Passband: 0 to f_pass
- Stopband: f_s/2 to ∞
- Attenuation: Sufficient to prevent aliasing

### 2.2 Sampling Process

#### Mathematical Model

**Ideal Impulse Sampling:**
```
x_s(t) = x(t) × ∑ δ(t - nT_s)
        = ∑ x(nT_s) δ(t - nT_s)
where T_s = 1/f_s
```

**Frequency Domain Analysis:**
```
X_s(f) = f_s ∑ X(f - kf_s)
```

**Spectrum Visualization:**
```
Original: |X(f)|
          ↑
          |‾‾‾‾|       |
          |    |       |
          +-------+-------+--> f
          -f_max 0     f_max

Sampled: |X_s(f)|
         ↑
 ... |‾‾‾‾|       |‾‾‾‾|       |‾‾‾‾| ...
     |    |       |    |       |    |
     +-------+-------+-------+-------+--> f
        -f_s  -f_max 0     f_max  f_s
```

### 2.3 Quantization

#### Uniform Quantization

**Process:**
- Divide input range into L equal intervals
- Assign each sample to nearest quantization level

**Quantization Step Size:**
```
Δ = (V_max - V_min) / L
where L = 2ⁿ (n = number of bits)
```

#### Quantization Error
```
e(n) = x(n) - x_q(n)
```

**For Uniform Quantization:**
```
-Δ/2 ≤ e(n) ≤ Δ/2
```

**Quantization Noise Power:**
```
σ_e² = Δ² / 12
```

#### Signal-to-Quantization-Noise Ratio (SQNR)

**Calculation:**
```
SQNR = (Signal Power) / (Quantization Noise Power)
     = (σ_x²) / (Δ²/12)
```

**For Sinusoidal Signal:**
```
SQNR(dB) = 6.02n + 1.76 dB
where n = number of bits
```

**Examples:**
```
8-bit: SQNR ≈ 6.02×8 + 1.76 = 49.92 dB
16-bit: SQNR ≈ 6.02×16 + 1.76 = 98.08 dB
```

### 2.4 Analog-to-Digital Conversion

#### ADC Types

**Flash ADC:**
- Very fast (single cycle)
- High power consumption
- 2ⁿ comparators required
- Limited resolution (typically 4-8 bits)

**Successive Approximation ADC:**
- Medium speed (n cycles)
- Good accuracy
- Moderate complexity
- Most common type

**Sigma-Delta ADC:**
- High resolution (16-24 bits)
- Oversampling + noise shaping
- Digital filter required
- Excellent for audio

#### ADC Characteristics

**Resolution:**
```
Resolution = (V_ref) / 2ⁿ
```

**Conversion Time:** Time to complete one conversion

**Sampling Rate:** Maximum rate at which conversions can be performed

### 2.5 Digital-to-Analog Conversion

#### DAC Types

**Weighted Resistor DAC:**
```
     V_ref
      │
   ┌──┴──┐
   │ 2⁰R │← LSB
   └──┬──┘
      │
   ┌──┴──┐
   │ 2¹R │
   └──┬──┘
      │
   ┌──┴──┐
   │ 2²R │
   └──┬──┘
      │
   ┌──┴──┐
   │ 2³R │← MSB
   └──┬──┘
      │
      ├─→ V_out
     GND
```

**R-2R Ladder DAC:**
- Only two resistor values
- Better matching and accuracy

#### DAC Characteristics

**Settling Time:** Time to reach within specified error band

**Glitch Energy:** Short transient during code transitions

**Monotonicity:** Output always increases with increasing input code

### 2.6 Practical Sampling Systems

#### Complete Signal Chain
```
Sensor → Anti-aliasing Filter → Sample/Hold → ADC → Digital Processor
```

#### Sample-and-Hold Circuit
```
     ┌──────────┐
V_in─┤          ├─→ V_out
     │    S/H   │
Control ─┤      │
     └──────────┘
        │
       [C_hold]
        │
       GND
```

**Key Parameters:**
- **Aperture Time:** Uncertainty in sampling instant
- **Acquisition Time:** Time to charge hold capacitor
- **Droop Rate:** Voltage decay during hold mode

---

## 3. FFT & Frequency Analysis

### 3.1 Discrete Fourier Transform (DFT)

#### Definition
```
X[k] = ∑ x[n] e^(-j2πkn/N)
       n=0 to N-1
where:
k = 0, 1, 2, ..., N-1 (frequency index)
N = number of samples
```

#### Inverse DFT
```
x[n] = (1/N) ∑ X[k] e^(j2πkn/N)
        k=0 to N-1
```

#### DFT Properties

**Linearity:**
```
a·x₁[n] + b·x₂[n] ↔ a·X₁[k] + b·X₂[k]
```

**Time Shifting:**
```
x[n - m] ↔ X[k] e^(-j2πkm/N)
```

**Frequency Shifting:**
```
x[n] e^(j2πmn/N) ↔ X[k - m]
```

**Parseval's Theorem:**
```
∑ |x[n]|² = (1/N) ∑ |X[k]|²
```

### 3.2 Fast Fourier Transform (FFT)

#### What is FFT?
An efficient algorithm to compute the DFT, reducing complexity from O(N²) to O(N log₂N)

#### Radix-2 FFT Algorithm

**Decimation-in-Time:**
- Split input into even and odd samples
- Compute smaller DFTs
- Combine results with twiddle factors

**Butterfly Computation:**
```
x[m] ────→ ⊕ ────→ X[p]
      │        │
      × W      ×
      │        │
x[m+N/2] ─→ ⊕ ────→ X[q]
where W = e^(-j2π/N)
```

#### FFT Computational Savings

**DFT vs FFT Complexity:**
```
N = 1024 points:
DFT: N² = 1,048,576 operations
FFT: (N/2) log₂N = 512 × 10 = 5,120 operations
Speedup: ~200 times
```

### 3.3 FFT Implementation

#### Bit-Reversal Permutation
```
Input order: 0,1,2,3,4,5,6,7 (binary: 000,001,010,011,100,101,110,111)
Bit-reversed: 0,4,2,6,1,5,3,7 (binary: 000,100,010,110,001,101,011,111)
```

#### Twiddle Factors
```
W_N^k = e^(-j2πk/N) = cos(2πk/N) - j sin(2πk/N)
```

#### 8-point FFT Signal Flow
```
Stage 1      Stage 2      Stage 3
x[0] ──⊕───⊕───⊕─── X[0]
x[1] ──⊕───⊕───⊕─── X[4]
x[2] ──⊕───⊕───⊕─── X[2]
x[3] ──⊕───⊕───⊕─── X[6]
x[4] ──⊕───⊕───⊕─── X[1]
x[5] ──⊕───⊕───⊕─── X[5]
x[6] ──⊕───⊕───⊕─── X[3]
x[7] ──⊕───⊕───⊕─── X[7]
```

### 3.4 Spectral Analysis

#### Frequency Resolution
```
Δf = f_s / N
where:
f_s = sampling frequency
N = number of points
```

**Example:**
```
f_s = 1000 Hz, N = 1024 points
Δf = 1000/1024 ≈ 0.9766 Hz
```

#### Windowing

**Why Window?**
- Reduces spectral leakage
- Controls trade-off between main lobe width and side lobe level

**Common Window Functions:**

**Rectangular Window:**
```
w[n] = 1 for 0 ≤ n ≤ N-1
Main lobe width: 4π/N
Side lobe level: -13 dB
```

**Hanning Window:**
```
w[n] = 0.5 - 0.5 cos(2πn/(N-1))
Main lobe width: 8π/N
Side lobe level: -31 dB
```

**Hamming Window:**
```
w[n] = 0.54 - 0.46 cos(2πn/(N-1))
Main lobe width: 8π/N
Side lobe level: -41 dB
```

**Blackman Window:**
```
w[n] = 0.42 - 0.5 cos(2πn/(N-1)) + 0.08 cos(4πn/(N-1))
Main lobe width: 12π/N
Side lobe level: -58 dB
```

### 3.5 Power Spectral Density

#### Periodogram
```
P[k] = (1/N) |X[k]|²
```

#### Welch's Method
- Divide signal into overlapping segments
- Apply window to each segment
- Compute periodogram for each segment
- Average periodograms

**Advantages:**
- Reduced variance
- Smoother spectrum estimate

### 3.6 Practical FFT Applications

#### Vibration Analysis
```
Accelerometer → ADC → FFT → Frequency spectrum
Identify mechanical resonances and faults
```

#### Audio Spectrum Analysis
```
Microphone → Anti-aliasing → ADC → FFT → Frequency components
Used in equalizers, voice recognition
```

#### Power Quality Analysis
```
Voltage/current → Sampling → FFT → Harmonic analysis
Measure THD (Total Harmonic Distortion)
```

#### FFT Example: Two-Tone Signal
```
x(t) = sin(2π×100t) + 0.5 sin(2π×200t)
f_s = 1000 Hz, N = 1024 points

FFT shows peaks at:
k = (100/1000)×1024 ≈ 102 (bin 102)
k = (200/1000)×1024 ≈ 205 (bin 205)

Magnitudes: 1.0 and 0.5 (after proper scaling)
```

---

## 4. DSP Fundamentals

### 4.1 Discrete-Time Signals

#### Basic Sequences

**Unit Sample (Impulse):**
```
δ[n] = 1 if n = 0, 0 otherwise
```

**Unit Step:**
```
u[n] = 1 if n ≥ 0, 0 otherwise
```

**Exponential:**
```
x[n] = aⁿ
```

**Sinusoidal:**
```
x[n] = A cos(ωn + φ)
```

#### Digital Frequency
```
ω = 2πf / f_s (radians/sample)
where f = analog frequency, f_s = sampling frequency
```

**Important:** Digital frequency is periodic with period 2π

### 4.2 Discrete-Time Systems

#### System Properties

**Linearity:**
```
T{a·x₁[n] + b·x₂[n]} = a·T{x₁[n]} + b·T{x₂[n]}
```

**Time-Invariance:**
```
If y[n] = T{x[n]}, then y[n - k] = T{x[n - k]}
```

**Causality:**
Output depends only on present and past inputs

**Stability:**
Bounded input produces bounded output (BIBO)

#### Impulse Response
```
h[n] = T{δ[n]}
```

**Convolution Sum:**
```
y[n] = x[n] * h[n] = ∑ x[k] h[n - k]
                     k=-∞ to ∞
```

### 4.3 Z-Transform

#### Definition
```
X(z) = ∑ x[n] z⁻ⁿ
       n=-∞ to ∞
where z = complex variable
```

#### Region of Convergence (ROC)
Set of z-values for which the sum converges

#### Common Z-Transform Pairs

**Unit Sample:**
```
δ[n] ↔ 1, ROC: all z
```

**Unit Step:**
```
u[n] ↔ 1/(1 - z⁻¹), ROC: |z| > 1
```

**Exponential:**
```
aⁿ u[n] ↔ 1/(1 - a z⁻¹), ROC: |z| > |a|
```

#### Z-Transform Properties

**Linearity:**
```
a·x₁[n] + b·x₂[n] ↔ a·X₁(z) + b·X₂(z)
```

**Time Shifting:**
```
x[n - k] ↔ z⁻ᵏ X(z)
```

**Convolution:**
```
x[n] * h[n] ↔ X(z) H(z)
```

### 4.4 Digital Filters

#### Finite Impulse Response (FIR) Filters

**Difference Equation:**
```
y[n] = ∑ b[k] x[n - k]
       k=0 to M
```

**Transfer Function:**
```
H(z) = ∑ b[k] z⁻ᵏ
       k=0 to M
```

**Characteristics:**
- Always stable
- Linear phase possible
- No feedback
- Higher order for sharp cutoff

#### Infinite Impulse Response (IIR) Filters

**Difference Equation:**
```
y[n] = ∑ b[k] x[n - k] - ∑ a[k] y[n - k]
       k=0 to M         k=1 to N
```

**Transfer Function:**
```
H(z) = (∑ b[k] z⁻ᵏ) / (1 + ∑ a[k] z⁻ᵏ)
       k=0 to M         k=1 to N
```

**Characteristics:**
- Can be unstable
- Nonlinear phase
- Feedback used
- Lower order for sharp cutoff

### 4.5 Filter Design Methods

#### FIR Design

**Window Method:**
1. Specify ideal frequency response
2. Compute ideal impulse response (IDTFT)
3. Apply window to get finite length
4. Truncate to desired length

**Frequency Sampling Method:**
1. Specify desired frequency response at N points
2. Compute IDFT to get filter coefficients

**Optimal Methods:**
- Parks-McClellan algorithm
- Equiripple design

#### IIR Design

**Impulse Invariance:**
- Sample analog impulse response
- Preserves time-domain characteristics
- May cause aliasing

**Bilinear Transform:**
```
s = (2/T) (1 - z⁻¹)/(1 + z⁻¹)
```
- Maps analog to digital domain
- No aliasing
- Warps frequency axis

### 4.6 Multirate Signal Processing

#### Downsampling (Decimation)
```
y[n] = x[Mn]
where M = downsampling factor
```

**Frequency Domain:**
```
Y(e^jω) = (1/M) ∑ X(e^j(ω-2πk)/M)
           k=0 to M-1
```

**Anti-aliasing Filter Required**

#### Upsampling (Interpolation)
```
y[n] = x[n/L] if n/L integer, 0 otherwise
where L = upsampling factor
```

**Frequency Domain:**
```
Y(e^jω) = X(e^jωL)
```

**Anti-imaging Filter Required**

#### Fractional Rate Conversion
Combine interpolation and decimation:
```
New rate = (L/M) × original rate
```

### 4.7 Adaptive Filters

#### LMS Algorithm
```
y[n] = wᵀ[n] x[n]
e[n] = d[n] - y[n]
w[n+1] = w[n] + μ e[n] x[n]
where:
w = filter coefficients
μ = step size
```

**Applications:**
- Noise cancellation
- Echo cancellation
- System identification
- Channel equalization

### 4.8 Real-World DSP Applications

#### Audio Processing
- Equalization
- Compression
- Noise reduction
- Reverberation effects

#### Communications
- Modulation/demodulation
- Channel coding
- Equalization
- Synchronization

#### Image Processing
- Filtering
- Compression (JPEG)
- Edge detection
- Enhancement

#### Biomedical
- ECG analysis
- EEG processing
- Medical imaging
- Hearing aids

### 4.9 DSP Implementation

#### Fixed-Point Arithmetic
**Q-format:**
```
Qm.n format: m integer bits, n fractional bits
Range: -2ᵐ⁻¹ to 2ᵐ⁻¹ - 2⁻ⁿ
Resolution: 2⁻ⁿ
```

**Example: Q1.15**
```
Range: -1 to 1 - 2⁻¹⁵ ≈ 0.99997
Resolution: 2⁻¹⁵ ≈ 0.0000305
```

#### Floating-Point vs Fixed-Point
```
Parameter     | Fixed-Point | Floating-Point
-------------+-------------+---------------
Dynamic range | Limited     | Large
Precision     | Uniform     | Variable
Complexity    | Low         | High
Cost          | Low         | High
Power         | Low         | High
```

#### DSP Processors
**Features:**
- Harvard architecture
- Hardware multiplier
- Circular addressing
- Zero-overhead loops
- Multiple memory buses

**Examples:**
- Texas Instruments TMS320 series
- Analog Devices SHARC
- Microchip dsPIC

---

## Practice Problems

### Problem 1: Filter Design
```
Design a 3rd-order Butterworth low-pass filter with:
- Cutoff frequency: 1kHz
- DC gain: 1
Use Sallen-Key topology and calculate all component values.
```

### Problem 2: Sampling Analysis
```
A signal contains frequencies up to 8kHz.
The sampling frequency is 15kHz.
Determine:
a) If aliasing occurs
b) The apparent frequency of a 12kHz component
c) Required anti-aliasing filter specifications
```

### Problem 3: FFT Computation
```
Compute the 4-point DFT of:
x[n] = {1, 2, 3, 4}
Then compute the FFT using decimation-in-time and verify results match.
```

### Problem 4: Digital Filter Design
```
Design a length-5 FIR filter with cutoff frequency ω_c = π/2
using the window method with rectangular window.
Plot the frequency response.
```

### Problem 5: System Analysis
```
A system has impulse response: h[n] = (0.8)ⁿ u[n]
Determine:
a) Transfer function H(z) and ROC
b) Frequency response
c) Step response
d) Stability
```

## Conclusion

This comprehensive signal processing course covers the fundamental principles from analog filtering to advanced digital signal processing techniques. The material progresses from continuous-time systems through sampling theory to discrete-time analysis and practical implementations.

Key concepts to remember:
- Filters shape frequency content based on application requirements
- Sampling must satisfy Nyquist criterion to avoid aliasing
- FFT provides efficient frequency domain analysis
- Digital filters offer flexibility and precision
- Real-world applications span audio, communications, and biomedical fields

Signal processing continues to evolve with new algorithms, hardware implementations, and applications in emerging technologies like machine learning, 5G communications, and IoT devices.
