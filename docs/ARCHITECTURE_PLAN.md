# Project Planning: Real-Time Audio Fall Detection (TinyML)

## 1. Data Strategy

*   **Synthetic Data Generation**
    *   Mixing logic: Clean Falls + Water Noise + Home noises
    *   Signal-to-Noise Ratio (SNR) mixing levels

*   **Augmentations**
    *   Reverb / Echo simulation (Room Impulse Response)
    *   Background noise injection (Tiles reflections)

*   **Input Representation**
    *   Raw Waveform (1D) vs. Mel-Spectrogram (2D) vs. MFCC
    *   Sampling Rate constraints (16kHz vs 44.1kHz for TinyML)
    *   Window size / Hop length

*   **Pre-processing & Scaling**
    *   Normalization (MinMax vs. Standardization)
    *   *Critical for Neural Network convergence*


## 2. Model Architectures

*   **Type A: Custom Backbones (Built from Scratch/Ready-to-use)** 
    *   **CNN/RNN Variants:** CRNN, Standard 2D-CNN, Depthwise Separable CNN (MobileNet-style), 1D-Conv, LSTM vs. GRU (Parameter efficiency), TCN.

*   **Type B: Pre-Trained Backbones**
    *   **Candidates:** YAMNet, VGGish, OpenL3 (Small versions).
    *   **Role:** Primarily generally-trained feature extractors.

*   **Type C: Context-Aware / Adaptive Architectures** (two sub-models)
    *   *Concept:* **One-Shot Calibration** step to learn "Room Traits" (Noise floor / Reverb) -> Feed to Main Model.
    *   *Constraint Focus:* Calibration model adds to storage size (Flash), but NOT to runtime latency/battery.

*   **Type D: Autoencodr & Decoder** (Optional)
    *   Hardcore development, use pre-trained models

## 3. Training Paradigms

*   **Method 1: Supervised Binary Classification** (Tutorial 1)
    *   *Input:* Fall & Non-Fall data. *Output:* Probability of Fall.
    *   *Applicability:* Custom Backbones, Fine-tuning Pre-trained models.

*   **Method 2: Unsupervised / Anomaly Detection** (Tutorial 9)
    *   *Input:* Only Non-Fall data (Water). *Output:* Reconstruction Error / Anomaly Score.
    *   *Techniques:* Autoencoders (using Custom Backbones), One-Class SVM (using Pre-trained Embeddings).

*   **Method 3: Transfer Learning** (Supervised/Semi-Supervised, Tutorial 9)
    *   *Techniques:* Feature Extraction (Frozen backbone), Fine-Tuning (Unfrozen layers), Adapters/LoRA.

*   **Method 4: Knowledge Distillation**
    *   *Concept:* Big Teacher (Type B) trains Tiny Student (Type A).
    *   *Loss:* Soft targets (KL Divergence).
    *   *(Note: Advanced topic, not explicitly covered in course tutorials)*


## 4. Optimizations (Resource Efficiency)

*   **Quantization**
    *   Post-Training (PTQ) / QAT / Dynamic / Static Quantization.

*   **Pruning**
    *   Unstructured vs. Structured Pruning (Channel pruning)
    *   Lottery Ticket Hypothesis

*   **Constraints**
    *   Parameter count vs. Inference time vs. RAM usage (Flash memory)


## 5. Evaluation & Comparison Strategy

*   **Phase 1: Baseline Comparison (Pre-Optimization)**
    *   Goal: Pure Architectural comparison.

*   **Phase 2: Optimization Impact Analysis**
    *   *Key check:* Accuracy Degradation vs. Latency/Size Gain.

*   **Classification Metrics**
    *   False Positive Rate (FPR) at fixed Recall (Critical for user experience).
    *   F1-Score, ROC / AUC.

*   **Resource Metrics**
    *   FLOPs / MACs, Model Size (KB), Inference Latency (ms).

---

### Quick Reference: Key Concepts

*   **Precision:** How many of the "Fall" alarms were actually falls? (Low false alarms).
*   **Recall:** How many of the actual falls did the model catch? (High safety).

*   **F1-Score:** Harmonic mean of Precision and Recall.
    *   Especially useful for imbalanced datasets (where "Falls" are rare compared to "Water noise"), as it penalizes models that ignore the minority class or produce too many false positives.

*   **ROC / AUC:**
    *   **ROC:** Curve showing the trade-off between Sensitivity and False Alarms.
    *   **AUC:** The area under that curve. $1.0$ = Perfect, $0.5$ = Random guessing.

*   **MACs (Multiply-Accumulate):** Measures computational "weight." 1 MAC $\approx$ 2 FLOPs. Directly impacts battery life and latency on hardware.
