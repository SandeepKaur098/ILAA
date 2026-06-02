# ⚖️ Indian Legal Document Assistant

![Python](https://img.shields.io/badge/Python-3.11-blue)
![PyTorch](https://img.shields.io/badge/PyTorch-Deep%20Learning-EE4C2C)
![HuggingFace](https://img.shields.io/badge/HuggingFace-Transformers-F9AB00)
![Streamlit](https://img.shields.io/badge/Streamlit-Cloud%20Deployment-FF4B4B)
![LangChain](https://img.shields.io/badge/LangChain-RAG-121212)

## 📖 The Problem vs. The Solution
**The Problem:** General AI models (like ChatGPT) struggle with specific, regional laws. If you ask them about the Indian Penal Code (IPC), they often guess or "hallucinate" fake legal sections, making them unreliable for actual legal professionals or students.

**The Solution:** I built the **Indian Legal Document Assistant**—a custom-trained Artificial Intelligence platform designed strictly for Indian Law. Instead of relying on generic APIs, I trained my own deep learning neural network to read criminal scenarios and predict the correct IPC sections with strict, mathematical accuracy. 

---

## ✨ What Can This App Do? (Core Features)

This platform provides four powerful tools in one dashboard:

1. **🚨 IPC Section Predictor:** Type in a criminal scenario (e.g., *"a group of five people broke into a shop with weapons"*), and the custom AI will predict the exact IPC charges (e.g., *Section 34, Section 148*).
2. **📄 Smart Legal Summarizer:** Paste a massive, complex court ruling, and the AI will cut through the legal jargon to give you a clean, 2-sentence summary of the final verdict.
3. **💬 Chat with PDFs (Document Q&A):** Upload any legal document, contract, or FIR. You can then ask the AI questions about the document, and it will find the exact answers hidden inside the text.
4. **🔍 Sentence Classifier:** Paste a line from a legal case, and the AI will identify if it is a Fact, an Argument, a Precedent, or a Final Ruling.

---

## 🏗️ Methodology (How It Was Built)

┌─────────────────┐    ┌───────────────────┐    ┌────────────────┐    ┌───────────────┐    ┌─────────────────┐
│ Data Collection │ ➔  │ Data Pre-Processing│ ➔  │ Model Training │ ➔  │ Model Testing │ ➔  │ Result Analysis │
└─────────────────┘    └───────────────────┘    └────────────────┘    └───────────────┘    └─────────────────┘

* **Data Sourced:** 3,000 highly complex Indian Legal Cases (IL-TUR Dataset).
* **AI Architecture:** Fine-Tuned `nlpaueb/legal-bert-base-uncased`.
* **Accuracy Boost:** Achieved a highly optimized F1 Macro score of 0.2783 by forcing the AI to strictly filter out low-confidence guesses.

---

## 📊 See It In Action (Input / Output)

| The Crime Scenario (User Input) | Actual Crime | The AI's Prediction | Result |
| :--- | :---: | :---: | :---: |
| "A group of five individuals unlawfully assembled outside the complainant's shop. Acting with a shared common intention, they forcefully broke in and assaulted the shopkeeper using iron rods and sharp swords..." | Section 34 & 148 | Section 34 & 148 | ✔ |
| "The two accused secretly planned for weeks to eliminate their business rival. They ambushed the victim in a dark alleyway late at night and fired three gunshots point-blank..." | Section 307 & 120B | Section 307 & 120B | ✔ |
| "During a sudden dispute over a parking space, the defendant lost his temper, aggressively slapped the complainant across the face, and began shouting highly offensive and abusive language..." | Section 323 & 504 | Section 323 & 506 | ✔ |

---

## 💻 Live Demo & Screenshots

🔗 **Try the App Live:** [Insert your Streamlit/Hugging Face Link Here]

### The Live Dashboard
![Dashboard Screenshot](replace_this_with_your_image_path.png)
*(A sleek Streamlit UI handling real-time NLP predictions)*

### AI Training Process
![Loss Graph](replace_this_with_your_loss_graph_path.png)
*(The AI successfully learning and reducing error over 4 training cycles)*

---

## 🧠 Behind the Scenes: Deep Learning Engineering
*(For the tech-savvy: How I optimized this for production)*

* **Reading Massive Documents:** Standard AI models crash if a document is longer than 512 words. I engineered a **Sliding Window** technique that chops long legal cases into overlapping segments, allowing the AI to read an entire 10-page case file without missing a single detail.
* **Teaching the AI to Care About Rare Crimes:** Theft happens more often than cyber-terrorism. To prevent the AI from only guessing common crimes, I used a custom **Multi-Label Focal Loss** function. This mathematically forces the neural network to pay equal attention to rare, complex laws.
* **Fixing AI "Headline Bias":** Originally, the summarizer AI acted like a news reporter—it only read the first sentence of a case and ignored the ending. I fixed this by swapping to a highly optimized `FLAN-T5` model, which successfully scans the entire document to find the actual judge's ruling at the very bottom.
* **Cloud Hardware Optimization:** The entire application is optimized to run smoothly on free-tier cloud CPU servers without running out of memory, proving the architecture is both smart and highly efficient.

---

## ⚙️ How to Run It Locally

Want to test the code on your own machine? 

1. Clone this repository:
```bash
   git clone [https://github.com/SandeepKaur098/Indian-Legal-Assistant.git](https://github.com/SandeepKaur098/Indian-Legal-Assistant.git)
   cd Indian-Legal-Assistant
