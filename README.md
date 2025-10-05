# Bank of England NLP Project — Data-Driven Analysis of Quarterly Announcements from Global Systemically Important Banks (G-SIBs)

## Overview
This project applies **Natural Language Processing (NLP)** to automate the analysis of quarterly announcements and earnings call transcripts from **Global Systemically Important Banks (G-SIBs)**.  
The goal is to help regulators — specifically the **Bank of England (BoE)** — detect early signs of risk, evasive communication, or sentiment shifts in financial disclosures. By replacing manual review with an automated NLP pipeline, the system improves regulatory oversight, consistency, and efficiency in identifying potential systemic risks.

---

## Business Context
The **Bank of England** and its **Prudential Regulation Authority (PRA)** rely heavily on quarterly disclosures from G-SIBs to assess institutional health. These reports are extensive, unstructured, and linguistically complex — making manual review slow and error-prone.  
Our solution leverages NLP and Large Language Models (LLMs) to classify responses, detect sentiment, and flag sensitive topics, ultimately scoring each question-and-answer (Q&A) session on a **“traffic light” scale** to support supervisory decision-making.

---

## Data Source
- **Primary Data:** Quarterly earnings call transcripts and investor Q&A sessions (publicly available).  
- **Pilot Bank:** JP Morgan Chase (proof-of-concept).  
- **Document Formats:** PDF, CSV, and text scraped from investor relations sites.  
- **Volume:** One complete quarterly transcript containing 60 + Q&A pairs.  

---

## Methods / Pipeline
The system uses a modular, multi-agent architecture consisting of three main NLP components:

### 1. Dodging Agent
- **Goal:** Determine whether executive responses genuinely address analyst questions.  
- **Model:** **Mistral-7B-Instruct LLM** via LangChain.  
- **Output:** “Well Answered,” “Partially Answered,” or “Dodged,” mapped to Green / Yellow / Red traffic-light scores.  
- **Prompting Strategy:** Custom template comparing question-answer similarity with short rationales.

### 2. Topic Agent
- **Goal:** Identify major discussion themes and flag “sensitive topics” relevant to the BoE (e.g., credit risk, capital allocation, profitability).  
- **Model:** **BERTopic** (transformer embeddings + clustering).  
- **Output:** Topic labels cross-referenced with a predefined list of sensitive financial KPIs.

### 3. Sentiment Agent
- **Goal:** Assess sentiment of executives’ responses.  
- **Model:** **FinBERT**, a BERT variant trained on financial text.  
- **Output:** Positive, Neutral, or Negative sentiment classifications.  
- **Integration:** Negative sentiment on sensitive topics triggers higher risk weighting.

### 4. Scoring Mechanism
- Combines results from Dodging + Sentiment + Topic Agents into an **aggregate “traffic light” score**.  
- Red flags are raised where negative sentiment and dodged responses overlap on sensitive topics.  
- Formula weights negative sentiment on sensitive topics more heavily to prioritise supervisory attention.

### 5. KPI Extraction
- Detects key financial indicators (Capital Allocation, Credit Risk, Financial Performance, Profitability) using regex-based keyword mapping.  
- Enhances domain focus and supports cross-bank benchmarking.

---

## Tools & Libraries
- **Languages:** Python  
- **Key Libraries:** Hugging Face Transformers, BERTopic, LangChain, FinBERT-Tone, PyPDF2, Pandas, Regex  
- **Environment:** Jupyter / Google Colab  

---

## Results / Outcomes
- **Dodging Agent:** ~10 – 15 % of responses flagged as “Dodged,” 30 – 35 % “Partially Answered.”  
- **Topic Agent:** Clustered Q&A around BoE-relevant concerns (credit risk, profitability, capital).  
- **Sentiment Agent:** Predominantly neutral-positive sentiment; negative tone concentrated in discussions of default and credit risk.  
- **Final Scoring:** Higher dodging rates and negative sentiment on sensitive topics produced elevated risk scores (Red zones).  
- **Validation:** ~80 – 90 % agreement with human review on “dodging” classifications.  

---

## Key Insights & Business Impact
- Automated analysis reduces manual review effort and highlights risk patterns early.  
- The **traffic-light scoring** provides interpretability and rapid triage for regulators.  
- Combines **LLMs** and **domain-specific models** for robust, finance-aware text analysis.  
- Offers a scalable, transparent, and open-source foundation for future regulatory NLP tools.  

---

## Challenges & Future Work
- **Complex Financial Language:** Requires further domain fine-tuning of LLMs.  
- **Data Quality:** Variation in transcript structure affects topic clustering accuracy.  
- **Computational Resources:** Large-scale LLM inference remains resource-intensive.  

**Next Steps:**  
- Broader dataset calibration across multiple banks and periods.  
- Integration with numeric KPIs for cross-validation.  
- Real-time transcript ingestion for continuous risk monitoring.  

---

## Skills Demonstrated
- Natural Language Processing (NLP)  
- Large Language Models (LLMs)  
- Topic Modelling (BERTopic)  
- Sentiment Analysis (FinBERT)  
- Prompt Engineering (LangChain + Mistral LLM)  
- Feature Extraction / Regex / Data Wrangling  
- Risk Scoring & Data Visualisation  

---

## Supplementary Materials
- **Project Report:** [Available on request]  
- **Presentation Slides:** [Available on request]  

