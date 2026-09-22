
Repository Summary & Source Guide

​Synthetic Hamiltonian Engineering and Ground-State Preservation via Slaved Dual-Analog Cavity Confinement on a 156-Qubit Heavy-Hexagonal Processor

​Author: Matthew Michael-Scott Shaughnessy

Affiliation: Independent Researcher

Contact: shaughnessy101@gmail.com

Hardware Target: IBM Quantum Platform — ibm_fez (156-qubit Heron r2 heavy-hexagonal architecture)

​Overview & Source Guide

​The Stark Wave Model describes a method for optimizing quantum hardware by treating system errors as a predictable sinusoidal wave rather than random noise. By linking various control parameters to a central coordinate, qubit performance fluctuates in a rhythmic pattern, allowing the identification of interference troughs where gate fidelity is highest. Empirical testing on an IBM quantum processor (ibm_fez) successfully validated a Global Champion configuration, where drift and leakage were suppressed below standard measurement error thresholds.

​Slaving Equations & Standing Wave Model

​Control parameters were slaved to the Master Stark detuning coordinate:

​Δ = θ_stark - 0.15π

p₃₄ = 0.55π - Δ

t_bias = 0.24π + Δ

​Tracking the |10⟩ drift channel share (S = |10⟩ / Total Loss) over 21 continuous points in the negative hemisphere yielded an explicit sinusoidal wave equation:

​Fit Equation: S(θ) = 3.08% · cos(20.02θ + 2.52) + 94.78%

​Spatial Period: λ = (2π) / 20.02 ≈ 0.3138π (≈ 56.5°)

​Interference Cycles: ≈ 6.37 full wave periods per 2π rotation

​Empirical Benchmark Data

​Measurements executed at 2,000 shots per point on ibm_fez targeting the analytical extrema predicted by the wave equation:

​1. Deep Neg Trough (k = 1)

​Master Stark: -0.60π | Slaved p₃₄: +1.30π | Slaved t_bias: -0.51π

​Raw Fidelity (P₀₀): 99.25% | Preserved |00⟩: 1,985 / 2,000

​Total Loss: 15 shots | |10⟩ Drift: 13 | Leakage (|01⟩ + |11⟩): 2

​2. Neg Crest Barrier

​Master Stark: -0.44π | Slaved p₃₄: +1.14π | Slaved t_bias: -0.35π

​Raw Fidelity (P₀₀): 99.35% | Preserved |00⟩: 1,987 / 2,000

​Total Loss: 13 shots | |10⟩ Drift: 11 | Leakage (|01⟩ + |11⟩): 2

​3. Calibrated Baseline

​Master Stark: -0.29π | Slaved p₃₄: +0.99π | Slaved t_bias: -0.20π

​Raw Fidelity (P₀₀): 98.70% | Preserved |00⟩: 1,974 / 2,000

​Total Loss: 26 shots | |10⟩ Drift: 22 | Leakage (|01⟩ + |11⟩): 4

​4. Pos Crest Barrier

​Master Stark: +0.19π | Slaved p₃₄: +0.51π | Slaved t_bias: +0.28π

​Raw Fidelity (P₀₀): 99.05% | Preserved |00⟩: 1,981 / 2,000

​Total Loss: 19 shots | |10⟩ Drift: 16 | Leakage (|01⟩ + |11⟩): 3

​5. Global Champion (k = -2)

​Master Stark: +0.34π | Slaved p₃₄: +0.36π | Slaved t_bias: +0.43π

​Raw Fidelity (P₀₀): 99.40% | Preserved |00⟩: 1,988 / 2,000

​Total Loss: 12 shots | |10⟩ Drift: 10 | Leakage (|01⟩ + |11⟩): 2

​Physical Context Note: At +0.34π, |10⟩ drift dropped to 10 shots out of 2,000 (0.50%), operating strictly below the single-qubit measurement assignment error floor of Q₃₄ (0.696% ≈ 13.9 shots).

Verified Job Execution Registry
Phase Sweep (Negative Hemisphere): dak4dib9k43c73ahvau0, dak4epfi3e6s738r1bd0, dak4i839k43c73ahvfi0, dak4kkvi3e6s738r1hig, dak4n10mhr3c73e9nfc0, dak4ot9hvn6c73cv61fg
Extrema Validation (5-Node): dak7jj1hvn6c73cv90f0
Champion Standing-Wave Cancellation: damobvopqrnc7397s1fg (Achieving 99.45% raw retention)



​Execution Roadmap (Next QPU Window)

​When the monthly runtime allocation replenishes, experimental work will proceed in two structured phases:

​Phase 1: Continuous 360-Degree (2π) Stark Ring Sweep

​Objective: Map the unbroken multi-node wave profile across all four quadrants (-1.00π to +1.00π) in a single batch.

​Payload: 16 to 20 transpiled circuits executed at 2,000 shots.

​Goals:

​Empirically verify all 6 predicted interference troughs.

​Check for asymmetric envelope damping across positive vs. negative detuning hemispheres.

​Extract secondary Fourier harmonics to formalize the full system-wide Hamiltonian model.

​Phase 2: Uncoupling the Shadow Pole Drain (t_bias Sweep)

​Objective: Isolate the internal rotor dynamics of the Q₅₃ quadrature sink from cavity detuning.

​Execution:

​Lock Master Stark at the global champion node (+0.34π).

​Lock Witness Pin p₃₄ at its champion setting (+0.36π).

​Sever the slaved link: sweep t_bias independently of Δ across a full circle with Tap A (0.14π) and Tap B (0.36π) coupled to it.

​Goals:

​Map the non-commuting rotation plane between the bias angle and the orthogonal taps.

​Determine if fine-tuning the drain axis eliminates the final 10 counts of background error.

​Repository Contents

​data/: Raw count dictionaries and calibration snapshots directly from ibm_fez.

​circuits/: Transpiled OpenQASM 3.0 and Qiskit circuit templates for replication.

​notebooks/: Curve-fitting scripts and sinusoidal regression models.

​Citation

​Please cite this work via Zenodo DOI: (https://doi.org/10.5281/zenodo.22898763)
