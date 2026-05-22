# PCM and DM Modulation & Demodulation

# Aim
To write a simple Python program for the modulation and demodulation of:
- Pulse Code Modulation (PCM)
- Delta Modulation (DM)

---

# Tools Required
- Python 3.x
- NumPy Library
- Matplotlib Library

Install required libraries:

```bash
pip install numpy matplotlib
```

---

# Theory

## Pulse Code Modulation (PCM)
PCM converts an analog signal into digital form by:
1. Sampling
2. Quantization
3. Encoding

During demodulation, the digital signal is decoded back into analog form.

---

## Delta Modulation (DM)
Delta Modulation transmits only the difference between consecutive samples using binary values:
- 1 → Increase
- 0 → Decrease

Demodulation reconstructs the signal using step approximation.

---

# Program

```python
import numpy as np
import matplotlib.pyplot as plt

# Generate Analog Signal
t = np.linspace(0, 1, 1000)
f = 5
x = np.sin(2 * np.pi * f * t)

# ----------------------------------------
# PCM Modulation
# ----------------------------------------

# Sampling
fs = 20
ts = np.arange(0, 1, 1/fs)
samples = np.sin(2 * np.pi * f * ts)

# Quantization
levels = 16
quantized = np.round((samples + 1) * (levels - 1) / 2)

# Encoding
pcm_binary = [format(int(i), '04b') for i in quantized]

# PCM Demodulation
decoded = (quantized * 2 / (levels - 1)) - 1

# ----------------------------------------
# Delta Modulation (DM)
# ----------------------------------------

delta = 0.2
dm_signal = []
dm_output = []

prev = 0

for sample in samples:

    if sample >= prev:
        dm_signal.append(1)
        prev += delta
    else:
        dm_signal.append(0)
        prev -= delta

    dm_output.append(prev)

# ----------------------------------------
# Plotting
# ----------------------------------------

plt.figure(figsize=(12,10))

# Original Signal
plt.subplot(4,1,1)
plt.plot(t, x)
plt.title("Original Analog Signal")

# PCM Signal
plt.subplot(4,1,2)
plt.stem(ts, decoded)
plt.title("PCM Demodulated Signal")

# Delta Modulation Bits
plt.subplot(4,1,3)
plt.step(ts, dm_signal)
plt.title("Delta Modulated Signal")

# DM Reconstructed Signal
plt.subplot(4,1,4)
plt.step(ts, dm_output)
plt.title("DM Demodulated Signal")

plt.tight_layout()
plt.show()

# Display PCM Binary Codes
print("\nPCM Encoded Binary Values")
print("--------------------------------")

for i in pcm_binary:
    print(i)
```

---

# Output
<img width="1189" height="989" alt="image" src="https://github.com/user-attachments/assets/018ac433-2024-4eca-bd23-99c4cc48c359" />


## PCM Encoded Binary Values

```text
1111
1110
1100
1001
0111
0101
0011
0001
...
```

---

# Output Waveforms

## 1. Original Analog Signal
Attach the original sine waveform.

## 2. PCM Demodulated Signal
Attach the PCM reconstructed waveform.

## 3. Delta Modulated Signal
Attach the DM staircase binary waveform.

## 4. DM Demodulated Signal
Attach the reconstructed DM waveform.

---

# Results

Thus, the modulation and demodulation of:
- Pulse Code Modulation (PCM)
- Delta Modulation (DM)

were successfully implemented using Python. The corresponding modulated and demodulated waveforms were obtained and analyzed successfully.

---

# Applications
- Digital Communication Systems
- Telecommunication
- Audio Signal Processing
- Data Transmission
- Speech Communication

---

# Author
R.K. Vageesh Ragav  
B.E. Electronics and Communication Engineering (ECE)  
Saveetha Engineering College
