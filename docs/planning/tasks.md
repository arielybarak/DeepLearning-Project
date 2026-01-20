
# Project Roadmap & Task List

### 1. Design - Model Type A (from Scratch/ready-to-use)
- **Research:** Identify relevant lightweight models on Edge Impulse & Hugging Face.
- **Constraints:** Limitations (memory, inference time) in HW_CONSTRAINTS.md

### 2. Implementation - Training Automation Pipeline
Build a generic automation script to handle bulk experiments. Use API_gide.md

- **Automated Training Script:**
    - **Input:** List of model architectures
    - **Process:** 
        - Auto-execute training sequentially.
        - Trigger Edge Impulse (EON Tuner).
        - Log metrics automatically to TensorBoard.
        - Generate reports (md).
    - **Output:** Consolidated report file containing:
        - Loss curves & Accuracy graphs.
        - Resource usage statistics.
        - Comparative performance metrics.

### 3. Design - Model Type B: Pre-Trained Backbones 
- **Research:** direct search for pre-trained audio backbones on Hugging Face.
- **Design:** Design model characteristics (layers to freeze, layer sizes, etc.)
- **Constraints:** Limitations (memory, inference time) in HW_CONSTRAINTS.md







