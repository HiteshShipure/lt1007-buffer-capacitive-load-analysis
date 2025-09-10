# Unity‑Gain Buffer Driving Capacitive Loads (LT1007, ±15 V) — LTspice Simulations

This project studies a unity‑gain buffer based on LT1007 driving capacitive loads from 100 pF to 10 nF, using LTspice to analyze stability, step response, open‑loop gain/phase, and output noise, with and without a small output isolation resistor. 

## What this project shows (at a glance)
- Why unity‑gain buffers can ring or oscillate with capacitive loads, and how a small series resistor at the output restores phase margin and clean settling. 
- 100 pF case: small‑signal step settles in ≈5.43 µs with <~1 dB peaking when the loop has adequate phase margin. 
- 10 nF case: adding ~220 Ω isolation suppresses oscillations and yields ≈5.50 µs small‑signal settling with no sustained ringing. 
- Open‑loop Bode correlates phase margin to time‑domain overshoot, and noise density sits in the ~4 nV/√Hz class for the LT1007 model conditions used. 

## Why capacitive loads are hard (one paragraph)
The load capacitor introduces an additional pole at the op‑amp output node that adds phase lag inside the feedback loop; in unity gain this erodes phase margin, causing peaking or outright oscillation depending on the op‑amp’s open‑loop roll‑off and the size of the capacitance. 
A small output resistor (R_series ≈ 100–330 Ω) forms a lead network that places a helpful zero and decouples the heavy capacitive load from the op‑amp’s high‑gain node, which recovers phase margin and converts ringing into well‑damped settling. 

## How to reproduce (LTspice)
- Open the 100 pF schematic, run a small‑signal transient step, and export the plot for “Step — 100 pF.” 
- Open the 10 nF schematic, set R_series ≈ 220 Ω, run the same step, and export the plot for “Step — 10 nF + 220 Ω.”  
- Open the open‑loop/Bode schematic, run AC analysis to get loop gain and phase margin, and export the Bode plot and optional noise density. 

## Key results (embed 2–4 hero plots)
- Step — 100 pF: ![100 pF Step](assets/step_100pF.png) with ≈5.43 µs small‑signal settling and minimal overshoot.
- <img width="959" height="457" alt="100p_1v_step_ip" src="https://github.com/user-attachments/assets/594cdc2e-e338-49cf-9d4f-88899152fa0f" />

 
- Step — 10 nF + 220 Ω: ![10 nF Step (R=220 Ω)](assets/step_10nF_Rseries220.png) with ≈5.50 µs and no sustained ringing. 
- Open‑loop Bode: ![Open‑Loop Bode](assets/bode_openloop.png) showing crossover and phase margin consistent with time‑domain behavior. 
- Noise density: ![Noise Density](assets/noise_density.png) in the ~4 nV/√Hz region for the device model and setup used. 








## Files in this repo
- README.md — summary, theory in one paragraph, and hero plots for quick understanding. [2]  
- docs/results.md — full plot set with deep explanations and “what‑if” guidance. [2][3]  
- sims/ltspice/*.asc — LTspice schematics for 100 pF, 10 nF + R_series, and open‑loop Bode/noise. [2]  
- assets/*.png — exported plots used by README and docs/results.md. [2]
