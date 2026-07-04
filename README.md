# AuraFrequencyAnalyzer

# 🎛️ Spectra: Real-Time Acoustic Anomaly Detector

<div align="center">

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![Web Audio API](https://img.shields.io/badge/Web_Audio_API-FF4B4B?style=for-the-badge&logo=webaudio&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Active-success?style=for-the-badge)

**A zero-dependency, browser-based FFT spectrum analyzer designed to detect, log, and visualize acoustic anomalies in real-time.**

[Features](#-features) • [Use Cases](#-use-cases) • [Getting Started](#-getting-started) • [Roadmap](#-roadmap) • [Contributing](#-contributing)

</div>

---

## 📖 Overview

**Spectra** is a high-performance, single-page web application that transforms your browser into a professional-grade acoustic analysis tool. By leveraging the **Web Audio API** and **Fast Fourier Transform (FFT)**, it continuously monitors the audio spectrum, compares live frequencies against a user-calibrated "normal" baseline, and instantly flags deviations.

Whether you are monitoring industrial machinery for bearing faults, hunting for electrical hums in a recording studio, or analyzing room acoustics, Spectra provides immediate visual and logged feedback when frequencies spike above or drop below expected thresholds.

---

## ✨ Features

### 🎯 Core Capabilities
*   **Real-Time FFT Analysis:** Processes audio in 4096-sample chunks (~10Hz resolution per bin) for highly accurate frequency isolation.
*   **Dynamic Baseline Calibration:** A 3-second "learning mode" that captures the ambient noise floor or normal operating state of a machine, establishing a custom reference spectrum.
*   **Anomaly Detection Engine:** Automatically detects and highlights frequencies that deviate beyond a user-defined decibel (dB) threshold.
    *   🔴 **Red Alerts:** Frequencies spiking *above* normal (e.g., new mechanical grinding, feedback squeal).
    *   🔵 **Blue Alerts:** Frequencies dropping *below* normal (e.g., a motor losing a specific harmonic, signal dropout).

### 📊 Advanced Visualizations
*   **Logarithmic Spectrum Graph:** A high-contrast, real-time line graph with a glowing fill, overlaying the live signal against the calibrated baseline and threshold boundaries.
*   **Waterfall Spectrogram:** A scrolling historical heatmap (time vs. frequency vs. amplitude) to identify intermittent or transient acoustic events.
*   **Anomaly Highlighting:** Visual "glow bars" and marker dots instantly draw the eye to problematic frequencies on the graph.

### 🎛️ Configurable Parameters
*   **Targeted Frequency Ranges:** Restrict analysis to specific bands to reduce visual clutter and focus on target acoustics:
    *   `< 500 Hz` (Bass, structural vibration, motor rumble)
    *   `< 2.5 kHz` (Human voice fundamentals, room resonances)
    *   `< 10 kHz` (General audio, speech intelligibility)
    *   `All (20 kHz)` (Full human hearing spectrum)
*   **Adjustable Sensitivity:** A dynamic threshold slider (3dB to 40dB) to tune the detector for highly sensitive laboratory environments or loud industrial floors.
*   **Debounced Event Logging:** Prevents log spam by intelligently throttling repeated alerts for the same frequency bin.

---

## 🏭 Use Cases

| Industry | Application |
| :--- | :--- |
| **Predictive Maintenance** | Detect early-stage bearing failures or misalignments in HVAC systems and motors by monitoring for new high-frequency metallic harmonics. |
| **Audio Engineering** | Hunt down 50Hz/60Hz electrical ground loops, microphone feedback frequencies, or unwanted room modes. |
| **Environmental Monitoring** | Detect anomalous low-frequency rumbles (e.g., heavy traffic, construction) or high-pitched mechanical whines in quiet server rooms. |
| **Acoustic Research** | Study the transmission loss of specific frequencies through walls and barriers in real-time. |

---

## 🚀 Getting Started

Because Spectra is a zero-dependency single-page application, no build tools or package managers are required.

### Prerequisites
*   A modern web browser (Chrome, Edge, Firefox, or Safari).
*   **Note:** Browser security policies require microphone access to be served over `HTTPS` or `localhost`. Opening the file directly via `file://` may block microphone permissions in some browsers.

### Installation & Usage
1.  **Clone the repository** or download the `index.html` file.
    ```bash
    git clone https://github.com/yourusername/spectra-analyzer.git
    cd spectra-analyzer
    ```
2.  **Serve locally** (optional but recommended for mic access):
    ```bash
    # Using Python 3
    python -m http.server 8000
    # Then open http://localhost:8000
    ```
3.  **Launch & Calibrate:**
    *   Click **Start Microphone** and grant browser permissions.
    *   Ensure the environment/machine is in its "normal" state.
    *   Click **Calibrate Baseline (3s)** and remain quiet/still for 3 seconds.
    *   Adjust the **Threshold** slider and select your **Frequency Range**.
    *   Watch the Event Log and Spectrum Graph for anomalies!

---

## 🗺️ Roadmap

This project is actively evolving. Future updates will bridge the gap between browser-based visualization and enterprise-grade IoT monitoring.

### Phase 1: Data & Export (Q3 2026)
- [ ] **Baseline Persistence:** Save and load calibration profiles to `localStorage` or export/import as `.json` files.
- [ ] **CSV Data Logging:** Export the timestamped event log and raw FFT data for post-analysis in Excel or Python.
- [ ] **A-Weighting / C-Weighting Toggles:** Apply standard acoustic weighting filters to match human loudness perception.

### Phase 2: Advanced DSP & AI (Q4 2026)
- [ ] **Dynamic EQ / Auto-Notch:** Introduce an active feedback suppression mode that automatically generates inverse phase signals to cancel out anomalous frequencies.
- [ ] **TensorFlow.js Integration:** Train a lightweight ML model in-browser to classify *types* of anomalies (e.g., "Bearing Fault" vs. "Electrical Hum" vs. "Voice").
- [ ] **Harmonic-to-Noise Ratio (HNR) Meter:** Real-time calculation of signal clarity for vocal and mechanical diagnostics.

### Phase 3: IoT & Distributed Monitoring (2027)
- [ ] **WebSocket Backend Integration:** Connect the web UI to a Python/FastAPI backend to aggregate data from remote Raspberry Pi/IoT microphones.
- [ ] **Multi-Channel Analysis:** Support stereo or multi-mic arrays for acoustic triangulation (pinpointing the physical location of the sound source).
- [ ] **Webhooks & Alerts:** Send SMS/Email or trigger Slack notifications when critical amplitude thresholds are breached.

---

## 🛠️ Tech Stack

*   **Frontend:** Vanilla JavaScript (ES6+), HTML5, CSS3
*   **Audio Processing:** Web Audio API (`AudioContext`, `AnalyserNode`, `MediaStreamSource`)
*   **Rendering:** HTML5 Canvas API (Hardware-accelerated 2D drawing for 60FPS spectrograms)
*   **Math:** Native JS `Math` and `TypedArrays` (`Float32Array`) for high-performance FFT bin calculations.

---

## 🤝 Contributing

Contributions are welcome! Whether you are an audio engineer who wants to add standard weighting curves, or a frontend dev who wants to improve the Canvas rendering performance, please feel free to submit a Pull Request.

1.  Fork the Project
2.  Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3.  Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4.  Push to the Branch (`git push origin feature/AmazingFeature`)
5.  Open a Pull Request

---

## 📄 License

Distributed under the MIT License. See `LICENSE` for more information.

---

<div align="center">
  <sub>Built with 🎧 for audio engineers, mechanics, and data scientists.</sub>
</div>
