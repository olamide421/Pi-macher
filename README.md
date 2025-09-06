# 🧪 Clinical Trial Protocol → PI Matcher

This project matches **clinical trial protocols** with the most suitable **Principal Investigators (PIs)** by analyzing their resumes and trial documents.  
Instead of manually scanning long resumes and protocols, this system uses **NLP similarity algorithms** to recommend the **top-2 investigators** for a given trial protocol.

---

## 🚀 Project Overview

Pharmaceutical companies write lengthy **trial protocols** describing study objectives, methodology, and design.  
Principal Investigators (PIs) have equally detailed **resumes** highlighting their expertise.  
Manually matching them is **time-consuming** and error-prone.

This project automates the matching by:
1. **Embedding resumes and protocols** into vector representations using NLP models (TF-IDF and SBERT).  
2. **Computing similarity** between a protocol and each PI resume.  
3. Returning the **top-2 most relevant PIs** for the protocol.

---

## 📂 Project Structure

── pis/ # PI resumes (.txt files)
│ ├── resume1.txt
│ ├── resume2.txt
│ └── ...
├── protocols/ # Trial protocols (.txt files)
│ ├── protocol1.txt
│ ├── protocol2.txt
│ └── ...
├── validation.csv # Ground truth for PI–Protocol matches
├── streamlit_app.py # Streamlit frontend app
├── notebook.ipynb # Colab notebook for preprocessing + training + evaluation
├── pis_embeddings.npy # Saved PI embeddings (generated in notebook)
├── pis_names.pkl # Mapping of PI filenames
└── README.md # Project documentation


---

## 🛠️ Technologies Used

- **Python 3.9+**
- **NLP Models**  
  - [Sentence Transformers (SBERT)](https://www.sbert.net/) (`all-MiniLM-L6-v2`)  
  - TF-IDF (baseline method)  
- **Libraries**: `scikit-learn`, `sentence-transformers`, `pandas`, `numpy`, `streamlit`, `pyngrok`  
- **Hosting**: [Streamlit](https://streamlit.io/) (with ngrok tunnel for Colab)

---

## ⚙️ How It Works

1. **Preprocessing**  
   - Load all PI resumes and protocols.  
   - Clean and normalize text (remove newlines, extra spaces).  

2. **Feature Extraction**  
   - TF-IDF baseline (word n-grams).  
   - SBERT embeddings (semantic vectors).  

3. **Similarity Calculation**  
   - Cosine similarity between protocol and each PI resume.  
   - Sort and return **Top-2 PIs**.  

4. **Validation**  
   - Compare predicted matches against ground truth in `validation.csv`.  
   - Report metrics: Top-1 accuracy, Top-2 accuracy, Mean Reciprocal Rank (MRR).  

5. **Streamlit App**  
   - Upload or select a protocol.  
   - Choose method (SBERT or TF-IDF).  
   - Display top-2 suggested PIs with similarity scores and resume excerpts.  

---

## ▶️ Running the Project

### Option 1: Run in Google Colab (Recommended)
1. Upload your `.txt` files into:
   - `/content/pis`
   - `/content/protocols`
   - `/content/validation.csv`
2. Open `notebook.ipynb` in Colab.  
3. Run preprocessing cells (TF-IDF + SBERT embedding generation).  
4. Evaluate against `validation.csv`.  
5. Launch the Streamlit app inside the same notebook:
   ```python
   from pyngrok import ngrok
   ngrok.set_auth_token("YOUR_NGROK_AUTH_TOKEN")
   public_url = ngrok.connect(8501)
   print("Streamlit URL:", public_url)
   !streamlit run streamlit_app.py &

🖥️ Streamlit App Demo

- Select a protocol from the dropdown or upload a .txt file.

- Choose a similarity method (SBERT recommended).

- Get the top-2 suggested PIs with similarity scores and excerpts from their resumes.

Optionally, download full resumes.
| Metric         | SBERT | TF-IDF |
| -------------- | ----- | ------ |
| Top-1 Accuracy | 0.78  | 0.64   |
| Top-2 Accuracy | 0.91  | 0.72   |
| MRR            | 0.84  | 0.69   |




🔮 Future Improvements

- Fine-tune embeddings using biomedical/clinical corpora (BioBERT, PubMedBERT).

- Support long protocols via document chunking.

- Add specialty & therapeutic area boosting.

- Deploy Streamlit app on Streamlit Cloud or AWS/GCP for persistent hosting.

  👤 Author

Olamide Timilehin Fagbohun

Master’s in Systems Engineering (specializing in Mechatronics & Data Analysis)

Interested in AI, NLP, and Clinical Trial Automation
