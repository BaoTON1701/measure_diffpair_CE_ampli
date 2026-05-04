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

There will be 3 differential pair on the same ASIC (R&T BiCMOS run 1) with input/output control by 2 analog switch.


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

#### 2.2.1. General Input noise measurement for each PCB 

In this measurement:

* Potentiometer adjusted to be in the middle of the track, proving $R_{C1} = R_{C2} = 2150 \Omega$
* Circuit bias with $I_{EE} = 1k \Omega$
* Gain of Stanford Research setted at 1000

Raw data measurement (overplot with instrument noise)

<figure>
  <img src="plot/measurement_raw_B1.png" alt="Raw noise B1">
  <figcaption>Noise density of Board 1</figcaption>
</figure>

<figure>
  <img src="plot/measurement_raw_B2.png" alt="Raw noise B2">
  <figcaption>Noise density of Board 2</figcaption>
</figure>

<figure>
  <img src="plot/measurement_raw_B3.png" alt="Raw noise B3">
  <figcaption>Noise density of Board 3</figcaption>
</figure>


We now show the cleaned spectrum (by subtracting the noise floor), apply a fit, divide by the differential gain and overplot with a post-layout simulation result.

<figure>
  <img src="plot/measurement_B1_intrinsic_noise_fit_vs_simulation.png" alt="input noise B1">
  <figcaption>Input referred noise measured Board 1</figcaption>
</figure>

<figure>
  <img src="plot/measurement_B2_intrinsic_noise_fit_vs_simulation.png" alt="input noise B2">
  <figcaption>Input referred noise measured Board 2</figcaption>
</figure>

<figure>
  <img src="plot/measurement_B3_intrinsic_noise_fit_vs_simulation.png" alt="input noise B3">
  <figcaption>Input referred noise measured Board 3</figcaption>
</figure>


#### 2.2.2. Input noise's variation due to mismatch
For this measurement, we adjust the potentiometer in between two load resistors in order to introduce mismatch. The results divide by 2 section

* Measurement while keeping the cutoff frequency near 1Hz for LPF at emitter, mismatch increase from 0 to 5 %

<figure>
  <img src="plot/Board_2_Noise_Spectrum_asymmetry_compare_medianfit.png" alt="Mismatch noise case 1">
  <figcaption>Mismatch=induced Input referred noise measured Board 2 (with LPF) </figcaption>
</figure>

* Measurement while removing LPF at emitter, mismatch increase from 0 to 15 %, in comparison with post-layout simulation 

<figure>
  <img src="plot/noise_vs_mismatch_simu.png" alt="Mismatch noise case 2 (simu)">
  <figcaption>Mismatch=induced Input referred noise measured Board 2 (simu) </figcaption>
</figure>

<figure>
  <img src="plot/noise_vs_mismatch_measure.png" alt="Mismatch noise case 2 (simu)">
  <figcaption>Mismatch-induced Input referred noise measured Board 2 (measure) </figcaption>
</figure>



<!-- The purpose of this measurement is to characterize the Heterojunction Bipolar Transistor (HBT) from IHP.

The test circuit consists of 6 groups of transistors, with each group containing 40 transistors in parallel. Each transistor has an emitter length ($E_l$) of $40 \mu m$. The circuit, designed by Jean Mesquida (APC), is part of the R&T BiCMOS project ASIC, which was taped out in November 2024. The test board was provided by Bao TON (APC). -->

------

# Measurement at cryogenic temperature

Context: In this section, we're going to do some measurement in cryogenic temperature (77K) using Liquid Nitrogen. We will: 
* Compare the gain between RT & CT 
* Measure and analyse the noise 
* Furthur more, we are going to operature in different bias to see if we can reduce the flicker noise as reducing the bias

## Result

### 1. Gain and Noise measurement with different biasing (Ic) and invariant load resistor (Rc)  
In this measurement, we change the $R_{EE}$ in turn $1k \Omega,~2k \Omega,~4k \Omega$, giving gain results below: 

<figure>
  <img src="plot/Gain_vs_Frequency_300K_77K.png" alt="gain_T_diff">
  <figcaption>Gain measurement results at RT and CT for different biasing condition. RT results shows in solid whether CT in dashed line. Color presents same biasing condition</figcaption>
</figure>

Measurement shows an increasing of 2 at CT compare to the one at RT, whether we are expeced the increasing of $\frac{I_C~@77K}{I_C~@300K} \times \frac{300}{77} \approx 2.33 $, The results is quite close to what we've expected. 

We are now presenting the noise measurement results

<figure>
  <img src="plot/Output_Noise_300K.png" alt="Output noise 300K">
  <figcaption>Output measured noise @300K overplot with instrument's noise</figcaption>
</figure>

<figure>
  <img src="plot/Output_Noise_77K.png" alt="Output noise 77K">
  <figcaption>Output measured noise @77K overplot with instrument's noise</figcaption>
</figure>

We see the reducing of noise while reducing the bias, but this could be due to the **reducing in Gain** of this amplifier. Noise we can divide this to the corresponding gain to present the **input referred noise**

<figure>
  <img src="plot/Input-Referred_Noise_300K.png" alt="input-referred noise 300K">
  <figcaption>Input-referred noise @300K. We observe the increasing in white noise (mainly due to shot noise), whether flicker noise unchanged </figcaption>
</figure>

<figure>
  <img src="plot/Input-Referred_Noise_77K.png" alt="input-referred noise 77K">
  <figcaption>Input-referred noise @77K. We see the plateau at high frequency starts to go up due to the increasing of white noise. However, the flicker noise still remain unchange. </figcaption>
</figure>

We see clearly the behavior of shot noise as it increasing inversely to the biasing. However, we don't see the change in flicker noise. Is that because there is another source of flicker noise that conteminate the circuit?

<u> Note: </u> different biasing at CT compare to RT due to the fact that base-emitter voltage ($V_{BE}$) depend on the temperature (normally 0.7V at RT and near 1V at CT)

### 2. Noise measurement while keeping the same gain (by increase Rc while reducing Ic)
In this measurement, we're going the keep the same gain, in order to keep the same output common mode voltage (as shown in the optimization) then try to compare them. 

<figure>
  <img src="plot/Input-Referred_Noise_300K_same_gain.png" alt="input-referred noise 300K same gain">
  <figcaption>Input-referred noise @300K . We observe flicker noise increase? WTF?  </figcaption>
</figure>

<figure>
  <img src="plot/Input-Referred_Noise_77K_same_gain.png" alt="input-referred noise 77K same gain">
  <figcaption>Input-referred noise @77K . We observe the increasing of the plateau but at higher frequency compared to the previous section  </figcaption>
</figure>

### 3. Results measured with new Power supply 

<figure>
  <img src="plot/Input-Referred_Noise_300K_same_gain_new_supply.png" alt="input-referred noise 300K same gain">
  <figcaption>Input-referred noise @300K . We still observe flicker noise increase...  </figcaption>
</figure>

<figure>
  <img src="plot/Input-Referred_Noise_77K_same_gain_new_supply.png" alt="input-referred noise 77K same gain">
  <figcaption>Input-referred noise @77K . We observe a decreasing of flicker noise in middle range  </figcaption>
</figure>




-------
Acknowledgement: ASICs and Measurement was done due to the contribution of **R&T BiCMOS** multi-wafer project and **Laboratory
of Astroparticles and Cosmology (APC)**