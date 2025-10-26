# Analysis of the BB84 Quantum Key Distribution (QKD) Algorithm

## Overview

In this notebook, we implement and analyze the BB84 Quantum Key Distribution (QKD) protocol under a variety of conditions to study how eavesdropping and environmental noise affect the ability of Alice and Bob to securely generate a shared key. We simulate multiple cases, visualize quantum circuits, and apply post-processing techniques including error correction and privacy amplification.

### Simulation Cases

We model four scenarios to test how QBER and key generation behave under different conditions:

1. **No Eavesdropping, Low Noise**  
   Ideal conditions. Expected QBER ≈ 0.

2. **Eavesdropping, Low Noise**  
   Eve performs measurements on the quantum channel. Expected QBER ≈ 0.25.

3. **No Eavesdropping, High Noise**  
   Channel noise flips qubits randomly. Expected QBER ≈ noise level.

Each case includes:
- Circuit construction and visualization
- Statistical analysis across multiple trials
- Comparison to theoretical expectations

### Sifted Key Generation

After measurement, Alice and Bob compare their basis choices and retain only bits where their bases match. This forms the **sifted key**, which is used for further processing. We track:
- Sifted key length
- Number of discarded runs
- QBER per trial

#### Key Rate and QBER Analysis

We calculate the secure key rate using the binary entropy function:

$$H(e) = -e \log_2 e - (1 - e) \log_2 (1 - e)$$  
$$R = \max(0,\ 1 - 2H(e))$$

This quantifies how much usable key material remains after error correction and privacy amplification. We plot QBER and key rate vs. noise level with and without Eve.

### LDPC Error Correction

We apply Low-Density Parity-Check (LDPC) codes to correct mismatches in the sifted key. Using `pyldpc`, we:
- Encode Alice’s key
- Simulate transmission with QBER-induced bit flips
- Decode Bob’s received word
- Recover the corrected key

### Privacy Amplification

To ensure information-theoretic security, we hash the corrected key using SHA-256. This produces a final secure key that is resistant to both classical and quantum attacks.

### Final Outcome

The notebook demonstrates a complete BB84 pipeline:
- From quantum circuit simulation
- To sifted key extraction
- To secure key generation

It validates BB84’s robustness against noise and eavesdropping, and shows how post-processing techniques enable secure communication even under imperfect conditions.
