## VTA DA Neuron Model

This is a model I hold very dear to heart. It was my first real introduction to the mathematical modeling of biological systems, and it ultimately pushed me toward taking more mathematics courses and learning programming so I could understand more deeply how to build, tune, and interpret models like this one.
It was particularly challenging because it was the first time I tried to build a model from scratch without having a reference codebase to follow. On top of that, I was ambitious enough to try to replicate actual experimental data rather than just generate qualitatively plausible behavior. One of the first major problems I encountered was how to maintain the target `Rn` and `Cm` values while still reaching the desired membrane and `Ih`-related time constants. 
To deal with this, I incorporated an explicit calibration strategy in which the model size was scaled to match the target capacitance, the `H` conductance was adjusted to reproduce the desired `Gh`, and leak was then tuned to recover the target input resistance. This made the fitting process much more stable and allowed the same model structure to be adapted to different experimental groups. 
Similarly, I ran into difficulty reproducing the desired `Ih` amplitudes, activation curves, and kinetics at the same time. A single parameter change would often improve one feature while worsening another. To address this, I separated the control of `Ih` steady-state behavior from the control of its kinetics by introducing independent tuning parameters for the activation midpoint, slope, and time-course scaling. I also distinguished between the conditions used to display traces and the conditions used to extract metrics, since the fitted values depend strongly on the clamp configuration and pharmacological assumptions. That design choice made it much easier to compare the model to the experimental measurements in a more realistic way.

The notebook implements a conductance-based VTA dopamine neuron model built primarily on the framework described in **Arencibia et al. (2021)**, while also incorporating parameter targets and experimental constraints drawn from the **2012** and **2016** studies to shape the `Ih` current and its kinetics. In that sense, this project is both a mechanistic model and a replication effort: it uses a modern multi-compartment structure, but aims to reproduce the physiological behavior reported in earlier electrophysiological work.

The main focus of the model is the hyperpolarization-activated current `Ih`. The code calibrates the model to reproduce target conductance and input-resistance measurements, and then compares saline and cocaine-like conditions through the same kinds of analyses used experimentally. This includes replication of:

- `Ih` voltage-clamp families
- gating curves and normalized conductance-voltage relationships
- activation kinetics across voltages
- tail-current behavior and reversal estimates
- alpha-EPSP and temporal summation protocols
- evoked spike responses

This project is still evolving. One of the next steps is to integrate the same `.abf` analysis pipeline used for the experimental recordings so that the model outputs can be compared against the **2016** paper using the same extracted metrics and analysis logic. I may also continue developing this model to examine questions related to our most recent work from **2025** [Neuropharmacology](https://doi.org/10.1016/j.neuropharm.2025.110699).

Over time, this project became more than just a simulation notebook. It became a way for me to learn the nuts and bolts of mathematical modeling, to develop ingenuity in situations where there were no clear instructions or playbook to follow, and to appreciate coding as the most important tool for bringing all of those pieces together.
