# Assessing Data Privacy in Large Language Models

## 📄 Overview

This project provides a systematic assessment of privacy vulnerabilities in Large Language Models (LLMs), specifically focusing on the risks associated with Federated Learning (FL) and decentralized deployment. We categorize and implement various privacy risks including training data leakage and instruction prompt leakage, alongside analyzing their countermeasures.

The repository includes implementations and evaluations of:
* **Privacy Attacks:** Membership Inference Attacks (MIA), Prompt Leaking, and Jailbreaking.
* **Defense Mechanisms:** Differential Privacy, Defensive Prompting, and Machine Unlearning.

## 🔍 Taxonomy of Methods

We explore a comprehensive taxonomy of privacy-related methods:

### Attack Methodologies
1.  **Membership Inference Attacks (MIA):** Determining if a specific data sample was used during training.
2.  **Prompt Leaking Attacks (PLA):** Crafting malicious prompts to extract sensitive system instructions.
3.  **Jailbreaking:** Bypassing safety mechanisms (e.g., PAIR algorithm) to elicit unauthorized responses.

### Defense Methodologies
1.  **Differential Privacy (DP):** Obscuring gradients to prevent data memorization.
2.  **Machine Unlearning:** "Forgetting" private data using methods like Knowledge Gap Alignment (KGA).
3.  **Defensive Prompting:** Instructing models to handle sensitive content securely.
4.  **Data Scrubbing:** Removing PII using NER models.

## 🧪 Experimental Setup

We evaluated the performance of Membership Inference Attacks on state-of-the-art LLMs.

* **Target Model:** `llama-3.2-1B` (1 billion parameters).
* **Dataset:** `haritzpuerto/scaling_mia` (Benchmark for MIA).
* **Hardware:** Single NVIDIA L4 GPU.
* **Variable:** Training data size ranging from 10 to 500 samples.

### Key Metrics
* **AUC ROC:** Measures the attack's ability to distinguish between member and non-member samples.
* **F1-Score:** Harmonic mean of precision and recall.

## 📊 Results

Our experiments demonstrate a clear correlation between dataset size and attack success:

* **AUC ROC:** Increases consistently as the dataset size grows (from ~0.51 to >0.64), indicating that larger datasets allow attackers to better exploit model behavior patterns.
* **F1-Score:** Shows a similar upward trend, improving balanced performance as data availability increases.

> **Key Takeaway:** Larger datasets consistently improve MIA performance, highlighting the scalability of privacy attacks on LLMs.

## 🚀 Usage

### Prerequisites
* Python 3.8+
* PyTorch
* Transformers (Hugging Face)

### Running Attacks
To run the Membership Inference Attack benchmarks:

```bash
python run_mia.py --model llama-3.2-1B --dataset scaling_mia

```

### Running Defenses

To apply Knowledge Gap Alignment (KGA) unlearning:

```bash
python run_unlearning.py --method kga --target_data [TARGET_DATA]

```

*(Note: Adjust the command line arguments based on your specific script structure.)*

## 📚 Methodologies Implemented

### Membership Inference Attacks

* **Loss-based:** Evaluates sample loss.
* **Reference-based:** Calibrates loss against a reference model.
* **Zlib Entropy:** Calibrates loss with compression size.
* **Neighborhood Comparison:** Compares loss against modified "neighbor" samples.
* **Min-k% Probability:** Focuses on tokens with the lowest likelihoods.

### Jailbreaking

* **PAIR (Prompt Automatic Iterative Refinement):** Uses an "attacker" LLM to iteratively refine prompts to bypass the target LLM's safety filters.

## 🔗 References

1. *Extracting training data from large language models* (Carlini et al., 2021)
2. *Jailbreaking black box large language models in twenty queries* (Chao et al., 2023)
3. *Do membership inference attacks work on large language models?* (Duan et al., 2024)
4. *LLM-PBE: Assessing Data Privacy in Large Language Models* (Li et al., 2024)
