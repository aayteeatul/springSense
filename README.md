# Spring Stiffness Estimation from Natural Frequency (Smartphone / Phyphox)

Estimate the stiffness of a spring by identifying its natural frequency from smartphone acceleration data (e.g., exported from the **Phyphox** app). The script trims the initial portion of the recording, computes the FFT, detects the dominant frequency peak, and converts it to an estimated spring stiffness.

## How it works (overview)

1. **Load acceleration data** (CSV) exported from Phyphox (or any app with the same columns).
2. **Trim the first 1 second** to remove handling/settling effects.
3. **Compute the FFT** for each acceleration axis (x/y/z).
4. **Find the dominant peak frequency** (damped natural frequency, \( f_d \)).
5. **Convert to stiffness** using an effective mass model:

- Effective mass:
\[
m_{\text{eff}} \approx m_{\text{attached}} + \frac{1}{3}m_{\text{spring}}
\]

- Damped to undamped natural frequency:
\[
\omega_d = 2\pi f_d,\quad \omega_n = \frac{\omega_d}{\sqrt{1-\zeta^2}}
\]

- Stiffness:
\[
k = m_{\text{eff}}\omega_n^2
\]

> Note: If damping ratio \(\zeta\) is unknown, the stiffness estimate will vary with the assumed value.

---

## Requirements

Install dependencies:

```bash
pip install pandas numpy scipy plotly
