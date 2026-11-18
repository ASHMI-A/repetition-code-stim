# Repetition Code Memory Simulation (Stim + PyMatching + sinter)

Circuit-level simulation of a quantum repetition code memory experiment, to study how the logical error rate changes with code distance and physical error rate.

![Logical error rate vs physical error rate](repetition_code_circuit_noise.png)

## What I did
- Built repetition-code memory circuits with Stim for distances 3, 5 and 7, using the same number of rounds (10) for every distance so the comparison is fair
- Decoded the syndrome data with PyMatching (minimum-weight perfect matching)
- Swept the physical error rate p over 18 log-spaced values from 0.5% to 30%
- Used sinter for sampling: each point runs until 400 logical failures are seen or 2,000,000 shots, whichever comes first, and the plots show error bars
- Sanity check: at p = 0 the logical error rate is exactly 0

## Noise model
The same probability p is used for three error sources:
- depolarizing noise on data qubits before each round (only the X and Y parts flip a data qubit, so the effective data bit-flip rate is about 2p/3)
- measurement flip errors
- reset flip errors

## Results
- Below p of about 0.1, larger distance gives a lower logical error rate (error suppression), and the gap grows as p decreases.
- The curves in the per-round plot meet near p of about 0.1, which marks the threshold for this simplified noise model. Above it, larger codes do no better, and all curves approach 0.5 per shot (a coin flip).
- This roughly 10% threshold belongs to this simple model. Real surface-code thresholds are closer to 1%.
- The lowest-p points for d = 7 have very few failures (for example 2 in 2,000,000 shots at p = 0.005), so their error bars are wide.

## How to run
Open `repetition_code_stim.ipynb` in Google Colab or Jupyter and run all cells. To install the libraries locally:

```
pip install stim pymatching sinter numpy matplotlib
```

Versions used: stim 1.16.0, pymatching 2.4.0, sinter 1.16.0.

## Tools
Python, Stim, PyMatching, sinter, NumPy, Matplotlib
