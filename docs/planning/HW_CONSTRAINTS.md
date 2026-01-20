# Hardware Constraints & Model Size Targets

## 1. System Memory Constraints
* **Flash (Non-volatile):** $16$ MB total — $14$ MB usable for code and models.
* **PSRAM (Volatile):** $8$ MB total — $6$ MB limit for **Tensor Arena** (computing area in RAM) to ensure system stability.

---

## 2. Main Model (Real-time Classification)
* **Post-shrink Size:** $\le 3$ MB maximum due to computing constraints.
* **Pre-shrink Size:** $4$–$7$ MB (Full $TFLite$ format).
* **Performance Goal:** Maintain inference latency $< 100$ ms for immediate fall detection.

---

## 3. Secondary Model (One-time Calibration)
* **Post-shrink Size:** $\le 6$ MB due to PSRAM constraints.
* **Pre-shrink Size:** Up to $10$ MB.

---

## 4. Shrinkage Metrics (Edge Impulse Optimization)
* **Flash Reduction:** $\approx 25\%$–$30\%$.
* **RAM (Tensor Arena) Reduction:** $\approx 35\%$–$40\%$.
* **Mandatory Quantization:** **8-bit integer ($int8$)** is required to utilize ESP32-S3 vector instructions.
