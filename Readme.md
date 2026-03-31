# Noise measurement for Differential Common-Emitter from R&T BiCMOS Run1 HBT pairs

*Prepared by Bao TON - APC*

-----------------------------------------------

Results obtained from the measurement from 3 PCB boards of Differential Common-Emitter Amplifier 

## 1. Measuremnt Setup: 

### 1.1. Instrument:

* +- 2.5V Power Supply (Resulting +-1.65V by the regulator)
* Signal was amplified by Stanford Research SR560 by a factor of 1000
* Vector Analyser 89410A 

### 1.2. Test board: 

<figure>
  <img src="plot/pcb_schema/PCB_build.png" alt="Schematic of PCB">
  <figcaption>Schematic of the Test PCB.</figcaption>
</figure>
<figure>
  <img src="plot/pcb/Screenshot 2026-03-31 at 10.20.17.png" alt="PCB">
  <figcaption>3D view of the Test PCB</figcaption>
</figure>

### 1.3. Measurement description

The main objective of the measurement is to measure the **input referred noise** of the differential amplifier. 

Anyway, there is some improvement on the PCB board that we're expected to see: 

* Voltage Regulator was implemented in term of reducing the noise from power supply. 
* Two potentiometer was implemented: 

    1. Parallel with Load resistor to generate the **mismatch** of interest.

    2. Parallel with Resistive bias ($R_e$) to adjust the bias current.
* A LPF with fc down to 1 Hz was implemented in biasing stage in order to reduce common-mode noise adding from this stage into the amplifier.


## 2. Results

### 2.1. Noise measure from the SR560

<figure>
  <img src="plot/SR560_comparison.png" alt="Instrument noise">
  <figcaption>Noise density of SR560 Pre-Amplifier</figcaption>
</figure>


### 2.2. Noise measurement 

The purpose of this measurement is to characterize the Heterojunction Bipolar Transistor (HBT) from IHP.

The test circuit consists of 6 groups of transistors, with each group containing 40 transistors in parallel. Each transistor has an emitter length ($E_l$) of $40 \mu m$. The circuit, designed by Jean Mesquida (APC), is part of the R&T BiCMOS project ASIC, which was taped out in November 2024. The test board was provided by Bao TON (APC).

Measurements were performed using a **B1500A Semiconductor Device Parameter Analyzer** at two distinct temperatures:
- **Room temperature:** 300K
- **Cryogenic temperature:** 77K

# Aknowledgement 

ASICs and Measurement was done due to the contribution of **R&T BiCMOS** multi-wafer project and **Laboratory
of Astroparticles and Cosmology (APC)**