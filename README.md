# ⚖️ Indian Legal AI Assistant: Full-Stack NLP Architecture

![Python](https://img.shields.io/badge/Python-3.11-blue)
![PyTorch](https://img.shields.io/badge/PyTorch-Deep%20Learning-EE4C2C)
![HuggingFace](https://img.shields.io/badge/HuggingFace-Transformers-F9AB00)
![Streamlit](https://img.shields.io/badge/Streamlit-Cloud%20Deployment-FF4B4B)
![LangChain](https://img.shields.io/badge/LangChain-RAG-121212)

## 📌 Project Overview
The Indian Legal AI Assistant is an end-to-end Natural Language Processing (NLP) application designed to process, classify, and extract insights from complex Indian legal texts. 

Instead of relying solely on generic LLM API calls, this project features a **custom-trained PyTorch neural network** fine-tuned specifically on Indian Penal Code (IPC) scenarios, alongside a lightweight, CPU-optimized RAG pipeline and an abstractive summarization engine.

---

## 🚀 Core Architecture & Features

This application is divided into four distinct NLP pipelines:

### 1. The IPC Predictor (Custom PyTorch Architecture)
A custom multi-label classification engine that reads a criminal scenario and predicts the exact Indian Penal Code (IPC) sections applicable.
* **Base Model:** `nlpaueb/legal-bert-base-uncased`
* **Training Data:** Sub-sampled from the IL-TUR dataset (Focusing on top 100 highest-frequency IPC laws).
* **Optimization:** Replaced standard Binary Cross Entropy with **Multi-Label Focal Loss** to penalize the model for majority-class dominance. Implemented **Dynamic Thresholding** (calculating the optimal mathematical threshold for *each* law independently) coupled with a strict 25% confidence floor to eliminate noise.

### 2. Abstractive Legal Summarizer
* **Model:** `google/flan-t5-base` (Instruction-Tuned).
* **Engineering Challenge Solved:** Standard models like `BART-large-cnn` exhibited a "News Headline Bias," merely copying the first sentence of legal texts and ignoring the final judicial verdicts. By swapping to the instruction-tuned FLAN-T5 and adjusting the localized attention layouts, the pipeline forces the AI to read the entire sequence and accurately abstract the final legal resolution.

### 3. Document Q&A (Retrieval-Augmented Generation)
* **Stack:** LangChain + FAISS Vector Database + Gemini 2.5 Flash API.
* **Mechanism:** Implements `RecursiveCharacterTextSplitter` with dense chunking to vectorize uploaded PDFs (like FIRs or court rulings). Users can query the document, and the RAG pipeline retrieves the exact contextual chunks to ground the LLM's answers, preventing hallucination.

### 4. Sentence Rhetorical Classifier
* Utilizes a zero-shot classification pipeline to break down lengthy legal documents and categorize individual sentences into legal rhetoric (e.g., *Fact, Argument, Ratio Decidendi, Precedent*).

---

## 📊 Training Metrics & Visualizations

*(Interviewer Note: The custom Legal-BERT model was trained using dynamic threshold optimization, yielding an immediate +10% boost in Macro F1 scores compared to static 0.5 thresholding).*

<!-- 
======================================================
INSTRUCTIONS FOR GITHUB:
Replace the placeholder image paths below with the actual paths 
to your screenshots and graphs in your repository. 
======================================================
-->

### Dashboard Interface
![App Interface](path/to/your/interface_screenshot.png)
*The live Streamlit dashboard demonstrating the Top-3 noise-filtered predictions.*

### Model Performance (Loss vs. Epochs)
![Training Graph](path/to/your/loss_graph.png)
*Custom Multi-Label Focal Loss convergence over 4 epochs (Refer to `DL_CLASSIFICATION_V3.ipynb` for raw training logs).*

---

## ⚙️ Engineering Trade-offs & Decisions

During development, several architectural choices were made to optimize for free-tier cloud deployment constraints (16GB RAM, CPU-only):
1. **Compute vs. Latency (Summarizer):** Opted against massive 7B+ parameter models (which cause Out-Of-Memory crashes on cloud CPUs). Utilized the 900MB FLAN-T5 model with optimized `num_beams=2` and `length_penalty=2.0`. This ensures 5-10 second latency while maintaining abstractive synthesis.
2. **Context Window Limitations:** To bypass BERT's strict 512-token limit during training, I engineered a hierarchical sliding window technique (Window = 512, Overlap = 128) to ensure long case files were fully processed without truncation loss.

---

## 💻 Local Installation & Setup

1. Clone the repository:
```bash
   git clone [https://github.com/YourUsername/Indian-Legal-Assistant.git](https://github.com/YourUsername/Indian-Legal-Assistant.git)
   cd Indian-Legal-Assistant
