# DSP with a focus on audio signals — Homework Assignment

This notebook implements a complete audio signal processing pipeline, from signal generation to adaptive noise removal. It was developed as a homework assignment for the Basic DSP course taught by Prof. Fabio Antonacci at Politecnico di Milano.

The work reuses code patterns and utility functions from the course notebooks available at:
https://github.com/fabioantonacci79/BasicDSP

---

## Structure

### 1. Sinusoidal signal `s`
Generation of a clean sinusoidal signal of 2 seconds, sampled at 8 kHz, with frequency 400 Hz and magnitude 0.5, using `np.sin`.

### 2. Noise `v` and noisy signal `d`
A noise sequence `v` is obtained using `np.random.randn` and added to `s` to yield the observed noisy signal `d = s + v`.

### 3. Play and plot the clean and noisy signals
Both signals are played back and visualised in the time domain, frequency domain (magnitude spectrum) and time-frequency domain (spectrogram).

### 4. Lowpass filter design
A FIR lowpass filter `h` is designed using `scipy.signal.firwin` with cutoff frequency 600 Hz and 128 taps. The impulse response and frequency response are plotted.

### 5. Filtering with `np.convolve` → `s_hat`
The noisy signal `d` is filtered using `np.convolve` with the designed filter `h` to obtain the estimated clean signal `s_hat`.

### 6. Overlap-and-Add filtering (convolution via DFT)
The same filtering is performed using the online Overlap-and-Add (OLA) method — frame-by-frame FFT convolution — as an efficient alternative to direct convolution.

### 7. Reference signal `g`
A reference signal `g` is obtained by filtering the noise sequence `v` through a FIR filter `b` with taps [1, 0.5, 0.3, 0.2, 0.1], using `scipy.signal.lfilter`.

### 8. Adaptive filters: Wiener, Steepest Descent, LMS
Using the noisy signal `d` and the reference `g`, three adaptive filters are computed:
- **Wiener filter `w`**: batch closed-form solution via `scipy.linalg.solve`
- **Steepest Descent `w_sd`**: iterative convergence to the Wiener solution
- **LMS `w_LMS`**: online sample-by-sample stochastic gradient update

Each filter produces an enhanced signal: `s_h`, `s_sd`, `s_LMS`.

### 9. Spectrograms
Spectrograms of `s_hat`, `s_h`, `s_sd` and `s_LMS` are plotted side by side to compare the noise removal performance of each method visually.

---

## Dependencies

```
numpy
matplotlib
scipy
ipython
```

---

## Author
_(student name)_  
**Deadline:** March 20, 2026  
**Submission:** fabio.antonacci@polimi.it
