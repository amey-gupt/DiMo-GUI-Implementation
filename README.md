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

### Test Case 1: PowerPoint - "Slide show from beginning"

The goal is to find the "From Beginning" button. The vanilla model is distracted by the pop-up window, while the DiMo-GUI framework, despite being led astray by the model's poor initial guess, attempts to refine the location.

**Without DiMo-GUI (Vanilla Result)**
*The model's unguided guess is incorrect, focusing on the top-left of the screen.*



**With DiMo-GUI (Full Framework Result)**
*The framework correctly follows its logic but refines an initial bad guess, leading to an incorrect final location within the pop-up.*



---

### Test Case 2: Google Maps - "Get directions"

The goal is to find the "Directions" icon or button. The vanilla model makes a large, inaccurate guess. The DiMo-GUI framework refines this into a nonsensical 1-pixel box, perfectly demonstrating the "no backtracking" limitation.

**Without DiMo-GUI (Vanilla Result)**
*The vanilla model makes a large, inaccurate guess in the top-left of the map area.*



**With DiMo-GUI (Full Framework Result)**
*The framework zooms in on a poor initial guess until the bounding box becomes too small, resulting in an incorrect final answer.*



---

## 🔬 Analysis and Conclusion

This implementation successfully replicates the logic of the DiMo-GUI framework. The experimental results clearly demonstrate the **model capability gap**:

While the framework's *process* is sound, the general-purpose `Llava-1.5-7b` model lacks the specialized training to make accurate initial guesses on complex GUIs. It is easily distracted by visual clutter and often "hallucinates" locations. As a result, the framework correctly refines these initial, incorrect predictions.

This project validates the paper's core premise: a sophisticated framework like DiMo-GUI, when paired with a highly capable, domain-specific model, can achieve significant performance gains in visual grounding.

---

## 🔧 How to Run

1.  Clone this repository.
2.  Open `DiMo_GUI_Implementation.ipynb` in Google Colab or a local Jupyter environment with a GPU.
4.  Run all cells in the notebook to execute the experiment and reproduce the results.
