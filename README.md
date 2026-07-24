# Analog-Metal-Detector
[![EDA](https://img.shields.io/badge/PCB-Altium-blue)]()
[![Simulation](https://img.shields.io/badge/Simulation-LTspice-orange)]()
[![Type](https://img.shields.io/badge/Design-Discrete%20Analog-brightgreen)]()

A fully analog metal detector using oscillators and multistage MOSFET amplifier circuits. This project explores the practical application of analog circuit design principles, including LC oscillators, frequency mixing, filtering, amplification, and PCB implementation.

The goal of the project was to create a metal detector where the output frequency changes based on proximity to metal. The final design successfully detected various metal objects, including small objects such as bolts.

---

## Demo

Final metal detector in action (turn up volume):



https://github.com/user-attachments/assets/b60bb2e3-ef44-4690-8b94-47a947424f01



Manufactured PCB with all components soldered:

<p align="center"><img src="Images/Assembled_PCB.jpg" alt="Manufactured PCB with all components soldered" width="60%"></p>


Detailed PCB schematic and layout included in the [`PCB_Files`](PCB_Files/) folder.

---

## Project Overview

The metal detector operates by comparing the frequency difference between two LC oscillators:

- A **static oscillator** using a shielded inductor that remains unaffected by nearby objects
- A **variable oscillator** using a [custom-wound exposed "inductor"](Images/Detecting_Coil.JPG) that changes frequency when near metal

When metal approaches the variable inductor, eddy currents affect the inductance, shifting the LC oscillator frequency. The difference between the two oscillator frequencies is extracted and converted into an audible signal known as a heterodyne beat-frequency using a mixer and amplifier stages.

[Schematic](PCB_Files/Schematic_PDF.pdf)

---

## System Architecture

The circuit consists of several analog processing stages:

### 1. LC Oscillators

Two LC oscillators generate signals near 50 kHz.

- Static oscillator: approximately 50 kHz
- Variable oscillator: approximately 50.1 kHz at idle (100 Hz idle buzz tone)

The frequency difference increases when metal is near, producing a higher pitch.

---

### 2. Frequency Mixer

The oscillator outputs are combined through a nonlinear MOSFET mixer stage.

The mixer generates multiple frequency components, with the heterodyne beat-frequency: $$f_{\text{diff}} = |f_{\text{static}} - f_{\text{variable}}|$$
being the signal used for detection.

---

### 3. Low-Pass Filter

A low-pass filter removes unwanted high-frequency mixer products, effectively outputting only the difference frequency.

Designed cutoff frequency:

- ~15 kHz (humans can't hear over 20kHz anyways)

---

### 4. MOSFET Amplifier Stages

The filtered signal is amplified through:

- Common-source (CS) amplifier
  - Provides voltage gain

- Common-drain (CD) amplifier
  - Acts as an output buffer
  - Drives the speaker load

---

## Design Process

The project involved the complete hardware development cycle:

- Hand calculations (LC frequencies, gains, filter cutoff...)
- LTspice simulation
- PCB schematic design + layout + assembly 
- Oscilloscope measurements
- Manual tuning and optimization

Because practical circuit behavior differs from ideal calculations, final performance required tuning component values and MOSFET bias points based on measured waveforms to achieve the loudest signal (highest gain).

---

## Results

The completed metal detector achieved:

- Stable oscillator operation near 50 kHz
- Audible frequency variation when approaching metal
- Successful detection of over 90% of objects (20/22) including small metallic objects such as bolts under a tarp

The final design prioritized practical detection performance through hardware tuning rather than purely theoretical optimization.

---

## Lessons Learned

This project demonstrated the challenges of transitioning from circuit theory to real hardware.

Key takeaways:

- Simulation results do not always perfectly predict physical behavior
- Component tolerances and parasitics significantly affect analog circuits
- Bias point tuning is critical for MOSFET amplifier performance
- Hardware debugging and measurement are essential parts of engineering design

