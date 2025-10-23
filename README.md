# DiMo-GUI: A Python Implementation

A Python implementation of the research paper **"DiMo-GUI: Advancing Test-time Scaling in GUI Grounding via Modality-Aware Visual Reasoning" ([arXiv:2507.00008v2](https://arxiv.org/pdf/2507.00008v2))**. This project replicates the core framework using a general-purpose Vision-Language Model to explore its effectiveness and limitations.

[![Python](https://img.shields.io/badge/Python-3.10-blue.svg)](https://www.python.org/downloads/)
[![Jupyter Notebook](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)](https://jupyter.org/)
[![Hugging Face](https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-Models-yellow.svg)](https://huggingface.co/llava-hf/llava-1.5-7b-hf)

---

## 📋 Overview

This project explores the challenge of **visual grounding** in Graphical User Interfaces (GUIs). The goal was to implement the DiMo-GUI framework, a training-free approach that enhances the ability of AI agents to accurately locate UI elements based on natural language commands.

The framework's core strategies are:
* **Modality Decoupling:** Separating the search for **text** and **icon** elements to prevent confusion.
* **Dynamic Zooming:** Iteratively refining the location of a target by progressively zooming in on the model's initial predictions.

---

## 🚀 The Experiment

To test the framework, I conducted a comparative experiment within a Jupyter Notebook (`DiMo_GUI_Implementation.ipynb`). The experiment compares the baseline performance of a general-purpose VLM (`Llava-1.5-7b`) against its performance when guided by the full DiMo-GUI framework.

1.  **"Vanilla" Run:** A single, generic prompt is sent to the model to get its raw, unguided prediction for a UI command.
2.  **"With DiMo-GUI" Run:** The full three-stage framework is executed to produce a final, refined prediction.

---

## 🖼️ Results and Demonstration

The results from both test cases consistently show the limitations of the general-purpose VLM for this specialized task.

### Test Case 1: PowerPoint - "Add Slide"

The goal is to find the "New Slide" button. Both the vanilla model and the DiMo-GUI framework fail, getting confused by the complex interface.

**Without DiMo-GUI (Vanilla Result)**
*The model's unguided guess is incorrect, focusing on the top-left of the screen.*
<img width="1200" height="743" alt="image" src="https://github.com/user-attachments/assets/ca2bfb53-d212-46d5-84de-e129d11cf6ec" />

**With DiMo-GUI (Full Framework Result)**
*The framework is led astray by the model's poor initial guesses and refines them into a meaningless 1-pixel box.*
<img width="1200" height="743" alt="image" src="https://github.com/user-attachments/assets/7061cfd7-8cfb-4e3e-9de5-87e57e44552b" />

---

### Test Case 2: Google Maps - "Begin Navigation"

The goal is to find the "Start" button. Both methods fail, highlighting the model's inability to correctly ground the command "Begin Navigation" to the correct visual element.

**Without DiMo-GUI (Vanilla Result)**
*The vanilla model makes an incorrect guess, bounding an empty black area instead of the "Start" button.*
<img width="1742" height="1240" alt="image" src="https://github.com/user-attachments/assets/da2fa5fc-09e9-4fc0-bf8a-cb98223b0f65" />

**With DiMo-GUI (Full Framework Result)**
*The framework's modality split does not help, as the initial guesses are poor. The process refines these bad guesses into tiny, incorrect boxes.*
<img width="1742" height="1240" alt="image" src="https://github.com/user-attachments/assets/84a43b6f-c6c3-4dfb-9ebb-6cf6cf52bd11" />

---

## 🔬 Analysis and Conclusion

This implementation successfully replicates the logic of the DiMo-GUI framework. The experimental results clearly and consistently demonstrate the **model capability gap**:

The underlying `Llava-1.5-7b` model, being a general-purpose VLM, lacks the specialized training to accurately understand complex GUIs. It is easily distracted by visual clutter and often "hallucinates" locations, causing *both* the simple vanilla prompt and the complex DiMo-GUI framework to fail.

This project validates the paper's core premise: a sophisticated framework like DiMo-GUI is not enough on its own. To achieve high accuracy in visual grounding, it must be paired with a powerful, domain-specific model that has been extensively trained on GUI interaction tasks.

---

## 🔧 How to Run

1.  Clone this repository.
2.  Open `DiMo_GUI_Implementation.ipynb` in Google Colab or a local Jupyter environment with a GPU.
4.  Run all cells in the notebook to execute the experiment and reproduce the results.
