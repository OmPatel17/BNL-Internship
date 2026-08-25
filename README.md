# sPHENIX Calorimeter Signal Reconstruction with Machine Learning

**Brookhaven National Laboratory — sPHENIX Collaboration**
Research Internship · Summer 2024 · Upton, NY

Applying deep learning to reconstruct particle-energy signals from high-noise
calorimeter waveforms for the sPHENIX experiment at the Relativistic Heavy Ion
Collider (RHIC).

---

## Overview

This project explores machine learning as a fast, accurate alternative to
traditional fitting methods for **calorimeter signal feature extraction** — the
task of recovering a particle's deposited energy (signal amplitude and timing)
from a noisy, digitized detector waveform.

At the scale sPHENIX operates (millions of readout channels per event, across
many runs), classical template-fitting is accurate but computationally
expensive. The goal here was to train deep learning models that match that
accuracy while running fast enough to be deployed across the full detector, and
to integrate them into the collaboration's production C++/ROOT software.

---

## Background: sPHENIX and Calorimetry

**sPHENIX** is a large detector experiment at RHIC (Brookhaven National
Laboratory) designed to study the quark–gluon plasma — the state of matter that
filled the early universe microseconds after the Big Bang.

Its **electromagnetic and hadronic calorimeters (EMCal / HCal)** measure the
energy of particles by digitizing the electrical pulse each particle produces.
Turning that raw, noisy waveform into a clean energy measurement — *signal
feature extraction* — is a core reconstruction problem, and doing it accurately
at scale is what this project targets.

---

## The Problem

> Given a high-noise, digitized calorimeter waveform, recover the underlying
> signal features (amplitude / energy and timing) — accurately, and fast enough
> to run across millions of channels in production.

---

## Approach

- **Deep learning models (TensorFlow / Keras)** trained to extract signal
  features directly from waveforms, benchmarked against the classical
  template-fit baseline.
- **Two data regimes:**
  1. *Simulated signals* with pulse shapes approximated by the **Landau
     function**.
  2. *Real data* from the **2018 EMCal prototype test-beam** run.
- **Training methods** compared: an approximated-Landau approach and a
  **template-fit** approach using a parametrized average pulse shape.
- **Distributed training** on Brookhaven's **HTCondor** high-performance
  computing cluster (~60,000 cores) to handle the dataset scale.
- **Automated evaluation pipeline** to validate model performance consistently
  across millions of waveform channels and multiple detector runs.
- **Production deployment via ONNX:** trained Keras models were exported to the
  **ONNX** format and served through high-performance C++ and Python ONNX
  runtimes, then integrated into the sPHENIX **C++/ROOT** analysis framework so
  other physicists could use them directly.

---

## Results

- **96% prediction accuracy** on 100,000+ high-noise calorimeter waveform
  samples.
- **~80% reduction in reconstruction error** versus the baseline, through model
  architecture and training optimizations on noisy detector data.
- **95% reduction in model validation time** via the automated evaluation
  pipeline, which processed **12M+ waveform channels** across multiple runs.
- Models **deployed into production for 50+ physicists** through the C++/ROOT
  sPHENIX analysis framework.

*(Full methodology and figures are in the research paper and poster below.)*

---

## Tech Stack

| Area                | Tools |
| ------------------- | ----- |
| Modeling            | Python, TensorFlow / Keras |
| Deployment          | ONNX (C++ & Python runtimes) |
| Data & Analysis     | NumPy, Pandas, ROOT |
| Framework / Compute | C++/ROOT (sPHENIX), HTCondor (distributed training) |

---

## Repository Contents

```
.
├── ml/            # Model training, evaluation, and ONNX-export code (waveform feature extraction)
├── paper/         # Research paper
├── poster/        # LISEF research poster
└── README.md
```

*(Adjust folder names to match your final layout.)*

---

## Publications & Presentations

- **Research Paper** — co-authored with Zen Pinkenburg (see `/paper`).
- **LISEF Poster** — Long Island Science and Engineering Fair (see `/poster`).

---

## Attribution

This work was completed as part of the **sPHENIX collaboration** at Brookhaven
National Laboratory. It builds on the collaboration's shared frameworks —
[`ml4cal`](https://github.com/sPHENIX-Collaboration/ml4cal) (machine learning
for calorimeters) and [`analysis`](https://github.com/sPHENIX-Collaboration/analysis)
(shared analysis modules). My contribution focused on the machine learning
pipeline for calorimeter waveform signal feature extraction — model development
and training, the evaluation pipeline, and ONNX-based deployment into the
sPHENIX software. Collaboration code and the broader detector software are the
work of many contributors and remain the property of the sPHENIX collaboration.

---

## Acknowledgments

Thanks to my mentors and the sPHENIX collaboration at Brookhaven National
Laboratory, and to the U.S. Department of Energy for supporting this research.
