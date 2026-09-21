import numpy as np
import matplotlib.pyplot as plt

# Step 1: Generate Analog Signal (Sine Wave)
duration = 0.05  # Duration in seconds
f_signal = 100   # Frequency of the signal (100 Hz)
fs = 2000        # Sampling frequency
t = np.linspace(0, duration, int(fs * duration), endpoint=False)
analog_signal = np.sin(2 * np.pi * f_signal * t)

# Step 2: Delta Modulation Algorithm
delta = 0.15     # Step size (Delta)
approximated_signal = np.zeros_like(analog_signal)
encoded_bits = []

current_value = 0.0
for i in range(len(analog_signal)):
    if analog_signal[i] >= current_value:
        encoded_bits.append(1)
        current_value += delta
    else:
        encoded_bits.append(0)
        current_value -= delta
    approximated_signal[i] = current_value

print(f"Step Size ($\Delta$): {delta}")
print(f"First 20 Delta Encoded Bits: {encoded_bits[:20]}")

# Step 3: Visualization
plt.figure(figsize=(12, 6))
plt.plot(t, analog_signal, label='Original Analog Signal', color='#38bdf8', linewidth=2.5, alpha=0.8)
plt.step(t, approximated_signal, label='Delta Modulated (Staircase) Signal', color='#ef4444', linewidth=2, where='mid')

plt.title('Delta Modulation (DM) Simulation', fontsize=12, fontweight='bold')
plt.xlabel('Time (seconds)')
plt.ylabel('Amplitude')
plt.axhline(0, color='black', linewidth=0.8, linestyle='--')
plt.legend(loc='upper right')
plt.grid(True, linestyle=':', alpha=0.6)
plt.tight_layout()
plt.show()
