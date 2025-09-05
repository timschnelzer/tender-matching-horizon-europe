# Tender Matching – Horizon Europe

## Project Abstract
This project explores the idea of automatically matching project ideas with the most relevant funding opportunities from **Horizon Europe (2021–2027)**.

The idea was inspired by a conversation with a potential client (webvalid.de), who needed a system to match companies with services. Since I cannot use their proprietary data, I looked for a similar problem with **open data** — and found one: matching **CORDIS project descriptions** with their corresponding **Horizon Europe calls**.

The challenge is very similar:

- **Input:** a project idea (title, abstract, keywords).  
- **Output:** the most relevant Horizon Europe funding call.  

By leveraging public datasets (CORDIS + Funding & Tenders), this project aims to deliver a working MVP where users can input a project description and receive the **Top-5 matching calls** ranked by relevance.

---

## Exploratory Data Analysis (EDA)
Before building models, the project starts with an **exploratory data analysis (EDA)**.  

The EDA is designed to be **open-ended and context-driven**, aiming to:
- Understand the structure and richness of the **CORDIS project dataset**.  
- Explore the **Horizon Europe calls** (titles, descriptions, deadlines, budgets, etc.).  
- Investigate relationships between projects and their assigned calls.  
- Provide insights into:
  - Total funding allocated per call or topic.  
  - Most frequent research areas and keywords.  
  - Distribution of project durations, budgets, and organizations involved.  

This step not only prepares the data but also adds valuable **context** that can later be integrated into the report or future iterations of the project.

---

## Approach
1. **Baseline (TF-IDF + Cosine Similarity)**  
   - Simple keyword-based similarity to establish a reference point.  

2. **Alternative Baseline (Keyword Overlap / Jaccard Similarity)**  
   - Measures how many keywords from a project appear in the call description.  
   - Helps show limitations of purely lexical methods.  

3. **Semantic Matching (Sentence-BERT Bi-Encoder)**  
   - Projects and calls are embedded into a semantic vector space.  
   - FAISS is used for efficient Top-N retrieval.  

4. **(Optional) Cross-Encoder Re-ranking**  
   - A more powerful model that re-scores the Top-N candidates for improved precision.  

5. **Prototype API**  
   - Flask-based API with `/recommend` endpoint.  
   - Returns the Top-5 calls for a given project description.  

---

## Project Timeline

**Week 1 – Data & Baseline**  
- Collect & clean CORDIS project data.  
- Fetch Horizon Europe Calls via Funding & Tenders API.  
- Merge datasets on `call ID`.  
- Run TF-IDF + Cosine Similarity baseline.  
- Deliverable: Clean dataset + first baseline results.  

**Week 2 – Semantic Matching (Bi-Encoder)**  
- Implement Sentence-BERT embeddings.  
- Index calls in FAISS.  
- Run retrieval experiments and evaluate (Top-1 Accuracy, Precision@5, Recall@10).  
- Deliverable: Working semantic retrieval pipeline.  

**Week 3 – (Optional) Cross-Encoder & Improvements**  
- Re-rank Top-N results with Cross-Encoder.  
- Compare against Bi-Encoder baseline.  
- Start building Flask API.  
- Deliverable: Improved accuracy, working API prototype.  

**Week 4 – Deployment & Report**  
- Finalize API deployment (local or cloud).  
- Write monitoring plan (logging requests, retraining with new data).  
- Prepare final written report (data, models, evaluation, deployment).  
- Optional: Build demo UI (Streamlit).  
- Deliverable: End-to-end system, report, and demo.  

---

## Deliverables
- **Exploratory Data Analysis (EDA)** notebook.  
- **Clean merged dataset** of projects and calls.  
- **Baseline and semantic models** with evaluation.  
- **Deployed prototype API** for recommendations.  
- **Final report** with methodology, findings, and future directions.  

---

## Optional Stretch Goals
- Compare results with **LLM embeddings** (e.g., OpenAI).  
- Build a **user-friendly UI** for non-technical users.  
